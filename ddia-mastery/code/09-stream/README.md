# code/09-stream/ — Traitement de flux

> Chapitre 11 · Jours 101-106 · `PLAN.md` Phase 3  
> **Exploite ton expérience Kafka** — ce chapitre est la théorie de ce que tu pratiques déjà.

---

## `log_broker.py` (Jour 101)

Broker à log append-only (style Kafka simplifié).

**Ce qu'on construit :**
- Topics avec partitions
- Producteur : `produce(topic, partition, message)` → retourne un offset
- Consommateur : `consume(topic, partition, group_id, offset)` → lit depuis un offset
- Groupes de consommateurs : chaque groupe a son propre offset indépendant
- Replay : relire depuis un offset arbitraire

**Jalons :**
```
Jalon 1 : log append-only par partition (fichier texte ou liste en mémoire)
Jalon 2 : consommateur avec offset → lire message par message
Jalon 3 : groupes de consommateurs → 2 groupes consomment la même partition indépendamment
Jalon 4 : replay → rembobiner à l'offset 0 → traiter tous les messages depuis le début
```

**Lancer :**
```bash
pytest code/09-stream/test_log_broker.py -v
```

---

## `windowing.py` (Jour 103)

Implémentation des 3 types de fenêtres temporelles.

```python
# Tumbling window (5s)
# [0-5s] [5-10s] [10-15s] → fenêtres non-chevauchantes

# Sliding window (5s toutes les 2s)
# [0-5s] [2-7s] [4-9s] → chevauchement

# Session window (inactivité > 3s = nouvelle session)
# [t1, t2, t3] pause [t4, t5] → 2 sessions
```

---

## `cdc_wal.py` (Jour 106)

CDC depuis le WAL Postgres → flux d'événements.

**Ce qu'on construit :**
- Connexion à Postgres avec `psycopg` en mode replication logique
- Écoute du slot de réplication (`pgoutput`)
- Décodage des événements INSERT/UPDATE/DELETE
- Émission vers une file (ou `log_broker.py`)

**Lancer :**
```bash
# Démarrer Postgres (déjà configuré avec wal_level=logical dans compose.full.yml)
docker compose -f labs/compose.full.yml up -d postgres

# Lancer le CDC consumer
python code/09-stream/cdc_wal.py

# Dans un autre terminal, faire des INSERT dans Postgres et observer les événements
```

---

## Connexion avec Kafka (Labo Jours 107-108)

| Concept jouet | Équivalent Kafka |
|--------------|-----------------|
| `log_broker.py` | Kafka Broker |
| Partitions | Kafka Partitions (clé → partition déterministe) |
| Groupes de consommateurs | Kafka Consumer Groups |
| Replay depuis offset 0 | `auto.offset.reset=earliest` |
| Log compaction | `cleanup.policy=compact` |
| `cdc_wal.py` | Debezium PostgreSQL Connector |
