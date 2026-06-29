# labs/ — Labos Docker

> **Principe :** Reproduis le concept sur un vrai système, puis **casse les choses** et observe.

---

## Stacks disponibles

### `compose.light.yml` — Stack léger (~512 MB RAM)

Services : **Postgres 16** + **Redis 7**

Usage : Phase 0-1 (Ch.1-4) — modèles de données, stockage, encodage.

```bash
# Démarrer
docker compose -f labs/compose.light.yml up -d

# Vérifier
docker compose -f labs/compose.light.yml ps
docker compose -f labs/compose.light.yml exec postgres psql -U ddia -c '\l'

# Arrêter
docker compose -f labs/compose.light.yml down

# Arrêter + supprimer les volumes (reset complet)
docker compose -f labs/compose.light.yml down -v
```

### `compose.full.yml` — Stack complet (~8 GB RAM)

Services : Postgres 16 + Redis 7 + **MongoDB 7** + **ZooKeeper** + **Kafka** + **Cassandra 4** + **Debezium** + **etcd**

Usage : Phase 2-3 (Ch.5-11) — réplication, partitionnement, consensus, stream, CDC.

⚠️ **Ne lance que les services du jour** — le stack complet simultanément nécessite ~8 GB de RAM libre.

```bash
# Lancer seulement Kafka + ZooKeeper (labo Ch.11)
docker compose -f labs/compose.full.yml up -d zookeeper kafka

# Lancer seulement etcd (labo Ch.9)
docker compose -f labs/compose.full.yml up -d etcd

# Lancer Postgres + Debezium (labo CDC)
docker compose -f labs/compose.full.yml up -d postgres kafka debezium

# Tout arrêter
docker compose -f labs/compose.full.yml down
```

---

## Commandes de base par service

### Postgres
```bash
# Connexion psql
docker compose -f labs/compose.light.yml exec postgres psql -U ddia

# Commandes utiles dans psql
\l                              -- lister les bases
\dt                             -- lister les tables
\d+ nom_table                   -- structure d'une table
EXPLAIN (ANALYZE, BUFFERS) ...  -- plan d'exécution
SELECT * FROM pg_stat_replication; -- état de la réplication
```

### Redis
```bash
docker compose -f labs/compose.light.yml exec redis redis-cli
# Dans redis-cli :
SET foo bar
GET foo
DEBUG SLEEP 2   -- simuler une lenteur
```

### Kafka
```bash
# Lister les topics
docker compose -f labs/compose.full.yml exec kafka \
    kafka-topics.sh --list --bootstrap-server kafka:9092

# Créer un topic
docker compose -f labs/compose.full.yml exec kafka \
    kafka-topics.sh --create --topic test --partitions 3 --replication-factor 1 \
    --bootstrap-server kafka:9092

# Consommer depuis le début
docker compose -f labs/compose.full.yml exec kafka \
    kafka-console-consumer.sh --topic test --from-beginning \
    --bootstrap-server kafka:9092
```

### Cassandra
```bash
docker compose -f labs/compose.full.yml exec cassandra cqlsh
# Dans cqlsh :
CREATE KEYSPACE ddia WITH replication = {'class': 'SimpleStrategy', 'replication_factor': 1};
USE ddia;
CONSISTENCY ONE;
CONSISTENCY QUORUM;
```

### etcd
```bash
docker compose -f labs/compose.full.yml exec etcd \
    etcdctl put /ddia/test "hello"

docker compose -f labs/compose.full.yml exec etcd \
    etcdctl get /ddia/test

# Observer les changements en temps réel
docker compose -f labs/compose.full.yml exec etcd \
    etcdctl watch /ddia/ --prefix
```

---

## Injection de pannes (Jour 69)

```bash
# Mettre en pause un conteneur (simule une panne totale)
docker pause ddia-postgres
docker unpause ddia-postgres

# Déconnecter du réseau (simule une partition réseau)
docker network disconnect ddia-mastery_default ddia-postgres
docker network connect ddia-mastery_default ddia-postgres

# Latence réseau sur un conteneur (nécessite sudo + iproute2 sur Linux)
CONTAINER=ddia-postgres
PID=$(docker inspect -f '{{.State.Pid}}' $CONTAINER)
sudo nsenter -t $PID -n tc qdisc add dev eth0 root netem delay 500ms 100ms
sudo nsenter -t $PID -n tc qdisc del dev eth0 root
```

---

## Dossiers par thème

| Dossier | Chapitre | Services utilisés |
|---------|----------|------------------|
| `labs/storage/` | Ch.2-3 | Postgres, MongoDB |
| `labs/replication/` | Ch.5 | Postgres (streaming replication), Cassandra |
| `labs/transactions/` | Ch.7 | Postgres |
| `labs/consensus/` | Ch.9 | etcd, ZooKeeper |
| `labs/batch/` | Ch.10 | Spark (local) |
| `labs/stream/` | Ch.11 | Kafka, Debezium, Postgres |
