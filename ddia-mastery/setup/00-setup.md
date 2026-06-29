# 00-setup.md — Mise en route de l'environnement

> **Lis ce fichier une seule fois (Jour 1), puis complète `reference/toc.md` et ouvre `days/day-001.md`.**

---

## 1. Mon édition

**Complète cette section maintenant :**

- [ ] **1ʳᵉ édition (2017)** — Kleppmann seul · 12 chapitres · 3 parties
- [ ] **2ᵉ édition (2026)** — Kleppmann & Riccomini · chapitres réorganisés

**Édition choisie :** _____________________________________

**Note :** Si tu lis la 1ʳᵉ éd., les encarts **📌 Contexte 2026** dans les fichiers-jours te rappellent les mises à jour majeures à intégrer (stockage objet comme modèle dominant, streaming → maintenance incrémentale de vues type Materialize, cloud-natif).

---

## 2. Calibration de la table des matières

Ouvre ton livre. Remplis `reference/toc.md` en notant le numéro de chapitre, le titre exact, la page de début et la page de fin.

**Pourquoi c'est critique :** tous les fichiers `days/day-NNN.md` utilisent des placeholders `p. ___` qui renvoient à ta TOC réelle. Sans calibration, les indications de lecture sont approximatives.

Consacre **15 min** à ce remplissage au Jour 1.

---

## 3. Environnement Python

```bash
# Depuis la racine de ddia-mastery/
python -m venv .venv

# Activer
source .venv/bin/activate          # macOS / Linux
# .venv\Scripts\activate           # Windows PowerShell

# Installer les dépendances
pip install -r code/common/requirements.txt

# Vérifier
python -c "import psycopg, redis; print('Python OK')"
```

---

## 4. Docker & labos

Docker et docker compose sont supposés installés (tu les as déjà). Tu n'as pas besoin de les réinstaller.

```bash
# Vérifier les versions
docker --version
docker compose version

# Lancer le stack léger (Postgres 16 + Redis 7)
docker compose -f labs/compose.light.yml up -d

# Vérifier Postgres
docker compose -f labs/compose.light.yml exec postgres \
    psql -U ddia -c "SELECT version();"

# Arrêter
docker compose -f labs/compose.light.yml down
```

### Stack léger vs stack complet

| Compose | Services | RAM estimée | Usage |
|---------|----------|-------------|-------|
| `compose.light.yml` | Postgres 16 + Redis 7 | ~512 MB | Phase 0-1 · Ch.2-4 |
| `compose.full.yml` | + Kafka + ZK + Cassandra + Mongo + Debezium + etcd | ~8 GB | Phase 2-3 · Ch.5-11 |

**Recommandation :** ne lance que le service du jour. Kafka + ZooKeeper + Cassandra sont gourmands — ne les démarre que pour les labos correspondants.

```bash
# Exemple : lancer seulement Kafka + ZooKeeper pour le Jour 107
docker compose -f labs/compose.full.yml up -d zookeeper kafka

# Arrêter uniquement ces services
docker compose -f labs/compose.full.yml stop zookeeper kafka
```

---

## 5. Voie Go (optionnelle)

Python est suffisant pour tout le plan. La voie Go est recommandée pour les **briques distribuées** (mini-Raft, simulateur de quorum, horloges vectorielles) car les goroutines et les canaux Go modélisent naturellement la concurrence distribuée.

```bash
# Vérifier Go (si installé)
go version   # >= 1.21 recommandé

# Initialiser un module Go dans code/07-consensus/
cd code/07-consensus
go mod init ddia-mastery/consensus
```

Si tu préfères rester en Python — c'est très bien, tous les jouets fonctionnent.

---

## 6. Import Anki (cartes de répétition espacée)

Ouvre Anki :
1. **Fichier → Importer** → sélectionne `flashcards/cards.tsv`
2. Type de note : Basique
3. Séparateur de champs : **Tabulation**
4. Champ 1 → Recto (Question) · Champ 2 → Verso (Réponse) · Champ 3 → Tags
5. Importer

Les cartes sont organisées par tags (`ch01::fiabilité`, `ch03::storage`, etc.) — crée un deck par phase ou un seul deck global.

**Calendrier de répétition espacée (intégré dans Anki) :**
Nouvelle carte créée à J → Anki la programme automatiquement à J+1, J+3, J+7, J+16, J+35.

---

## 7. Outils d'observation

| Outil | Usage |
|-------|-------|
| `psql -U ddia` | Requêtes Postgres · `EXPLAIN ANALYZE` |
| `redis-cli` | Inspecter Redis |
| `kafka-console-consumer.sh` | Lire des sujets Kafka |
| `etcdctl` | Requêtes etcd |
| `mongosh` | Requêtes MongoDB |

---

## 8. Injection de pannes (Phase 2 · Jour 69)

Pour les labos « ressentir CAP » tu auras besoin d'injecter des pannes réseau :

```bash
# Ajouter une latence de 200ms sur l'interface réseau d'un conteneur
CONTAINER=ddia-postgres
PID=$(docker inspect -f '{{.State.Pid}}' $CONTAINER)
sudo nsenter -t $PID -n tc qdisc add dev eth0 root netem delay 200ms 50ms

# Simuler une perte de paquets (20%)
sudo nsenter -t $PID -n tc qdisc add dev eth0 root netem loss 20%

# Supprimer la règle
sudo nsenter -t $PID -n tc qdisc del dev eth0 root

# Pausé un conteneur (simule une panne totale)
docker pause ddia-postgres
docker unpause ddia-postgres
```

> ⚠️ Ces commandes nécessitent `sudo` et `iproute2`. Sur macOS utilise `pumba` (outil de chaos Docker) ou connecte-toi à une VM Linux.

---

## ✅ Checklist Jour 1

- [ ] Édition déclarée dans ce fichier
- [ ] `reference/toc.md` rempli (tous les chapitres)
- [ ] venv Python créé + `pip install` OK
- [ ] `docker compose -f labs/compose.light.yml up -d` → Postgres répond
- [ ] Cartes Anki importées
- [ ] `reference/notes/jour-001.md` créé avec une note libre
