# PROGRESS.md — Suivi quotidien

## Compteur de série (streak)

```
Jours consécutifs : ___
Meilleure série   : ___
Dernier jour fait : ___
```

**Règle anti-décrochage :**
- Si tu sautes **1 jour** → reprends simplement le lendemain, sans doubler.
- Si tu sautes **2 jours** → reprends et lis `setup/toolbox.md §Anti-décrochage`.
- Si tu sautes **1 semaine** → recommence au dernier jour de revue hebdo (pas depuis le début).

---

## Phase 0 — Mise en route

| Jour | Date | Activité | ✅ | Note libre |
|------|------|----------|---|-----------|
| 001 | | 🔧 Setup : édition · Docker · venv · TOC · Anki | ☐ | |
| 002 | | 📖 Ch.1 — Fiabilité (fault vs failure) | ☐ | |
| 003 | | 🛠️ Jouet : percentiles p50/p95/p99 en Python | ☐ | |
| 004 | | 📖 Ch.1 — Scalabilité + Maintenabilité | ☐ | |

## Phase 1 — Fondations (Partie I)

| Jour | Date | Activité | ✅ | Note libre |
|------|------|----------|---|-----------|
| 005 | | 📖 Ch.2 — Modèle relationnel vs document | ☐ | |
| 006 | | 📖 Ch.2 — Modèle graphe + langages de requête | ☐ | |
| **007** | | **🔁 REVUE HEBDO #1** | ☐ | |
| 008 | | 🧪 Labo — Postgres vs MongoDB | ☐ | |
| 009 | | 📖 Ch.3 — Hash index + SSTables + compaction | ☐ | |
| 010 | | 📖 Ch.3 — B-trees + OLTP vs OLAP | ☐ | |
| 011 | | 🛠️ Jouet — Bitcask (log + index hachage) | ☐ | |
| 012 | | 🛠️ Jouet — mini-LSM (SSTables + compaction) | ☐ | |
| 013 | | 📄 Article — Bigtable / LSM-Tree | ☐ | |
| **014** | | **🔁 REVUE HEBDO #2** | ☐ | |
| 015 | | 🛠️ Jouet — mini-B-tree | ☐ | |
| 016 | | 🧪 Labo — Postgres EXPLAIN + types d'index | ☐ | |
| 017 | | 📖 Ch.3 — Stockage en colonnes (OLAP) | ☐ | |
| 018 | | 📖 Ch.4 — Encodage : JSON/Thrift/Protobuf/Avro | ☐ | |
| 019 | | 📖 Ch.4 — Compatibilité + modes de dataflow | ☐ | |
| 020 | | 🛠️ Jouet — Encodeur binaire + évolution schéma | ☐ | |
| **021** | | **🔁 REVUE HEBDO #3** | ☐ | |
| 022 | | 🧪 Labo — Protobuf Python + évolution champ | ☐ | |
| 023 | | 🛠️ Exercice « conçois X » — Stockage de journalisation | ☐ | |
| 024 | | 📄 Article — The Log (Jay Kreps) | ☐ | |
| 025 | | 📖 Consolidation Ch.3-4 — tradeoffs enrichis | ☐ | |
| 026 | | 🛠️ Re-dériver de mémoire : LSM vs B-tree | ☐ | |
| 027 | | 📖 Consolidation Phase 1 — teach-back | ☐ | |
| **028** | | **🔁 REVUE HEBDO #4** | ☐ | |

## Phase 2 — Données distribuées (Partie II) ← LE CŒUR

| Jour | Date | Activité | ✅ | Note libre |
|------|------|----------|---|-----------|
| 029 | | 📖 Ch.5 — Réplication mono-leader + lag | ☐ | |
| 030 | | 📖 Ch.5 — Anomalies de réplication | ☐ | |
| 031 | | 🛠️ Jouet — Simulateur mono-leader + anomalies | ☐ | |
| 032 | | 📖 Ch.5 — Multi-leader + conflits | ☐ | |
| 033 | | 📖 Ch.5 — Sans leader + quorums | ☐ | |
| 034 | | 🛠️ Jouet — Simulateur quorum W+R>N | ☐ | |
| **035** | | **🔁 REVUE HEBDO #5** | ☐ | |
| 036 | | 📄 Article — Dynamo | ☐ | |
| 037 | | 🧪 Labo — Postgres streaming replication + lag | ☐ | |
| 038 | | 🧪 Labo — Cassandra cohérence ONE/QUORUM/ALL | ☐ | |
| 039 | | 🛠️ Exercice « conçois X » — Fil d'actualité | ☐ | |
| 040 | | 📖 Synthèse réplication | ☐ | |
| 041 | | 🛠️ Redessine toutes les topologies | ☐ | |
| **042** | | **🔁 REVUE HEBDO #6** | ☐ | |
| 043 | | 📖 Ch.6 — Partitionnement par range vs hash | ☐ | |
| 044 | | 📖 Ch.6 — Hachage cohérent + nœuds virtuels | ☐ | |
| 045 | | 🛠️ Jouet — Anneau de hachage cohérent | ☐ | |
| 046 | | 📖 Ch.6 — Index secondaires + routage | ☐ | |
| 047 | | 🧪 Labo — Sharding Postgres | ☐ | |
| 048 | | 📖 Synthèse partitionnement | ☐ | |
| **049** | | **🔁 REVUE HEBDO #7** | ☐ | |
| 050 | | 📖 Ch.7 — ACID | ☐ | |
| 051 | | 📖 Ch.7 — Read uncommitted + read committed | ☐ | |
| 052 | | 📖 Ch.7 — Snapshot isolation + MVCC + write skew | ☐ | |
| 053 | | 📖 Ch.7 — Sérialisabilité : 2PL + SSI | ☐ | |
| 054 | | 🛠️ Jouet — KV MVCC + snapshot isolation | ☐ | |
| 055 | | 🛠️ Jouet — Démonstration anomalies | ☐ | |
| **056** | | **🔁 REVUE HEBDO #8** | ☐ | |
| 057 | | 📄 Article — Critique ANSI SQL Isolation Levels | ☐ | |
| 058 | | 🧪 Labo — Postgres isolation levels + lost update | ☐ | |
| 059 | | 🧪 Labo — Postgres SELECT FOR UPDATE / SSI | ☐ | |
| 060 | | 🛠️ Exercice « conçois X » — Réservation sans double-booking | ☐ | |
| 061 | | 📖 Synthèse transactions | ☐ | |
| 062 | | 🛠️ Redessine hiérarchie isolation | ☐ | |
| **063** | | **🔁 REVUE HEBDO #9** | ☐ | |
| 064 | | 📖 Ch.8 — Réseaux non fiables + détection de panne | ☐ | |
| 065 | | 📖 Ch.8 — Horloges : NTP + TrueTime | ☐ | |
| 066 | | 📖 Ch.8 — Horloges Lamport + vectorielles | ☐ | |
| 067 | | 🛠️ Jouet — Lamport + vecteur clocks + causalité | ☐ | |
| 068 | | 📄 Article — Time, Clocks (Lamport 1978) | ☐ | |
| 069 | | 🧪 Labo — Injection latence réseau (tc netem) | ☐ | |
| **070** | | **🔁 REVUE HEBDO #10** | ☐ | |
| 071 | | 📖 Ch.9 — Linéarisabilité + modèles de cohérence | ☐ | |
| 072 | | 📖 Ch.9 — Total order broadcast + 2PC | ☐ | |
| 073 | | 📖 Ch.9 — Paxos (vue haut niveau) + intro Raft | ☐ | |
| 074 | | 📖 Ch.9 — Raft : élection + log + sécurité | ☐ | |
| 075 | | 🛠️ Jouet — mini-Raft : élection de leader | ☐ | |
| 076 | | 🛠️ Jouet — mini-Raft : log + commit + fencing | ☐ | |
| **077** | | **🔁 REVUE HEBDO #11** | ☐ | |
| 078 | | 📄 Article — Raft (Ongaro & Ousterhout 2014) | ☐ | |
| 079 | | 📄 Article — Paxos Made Simple (Lamport 2001) | ☐ | |
| 080 | | 🧪 Labo — etcd : élection + verrous + watch | ☐ | |
| 081 | | 📖/🧪 ZooKeeper recipes | ☐ | |
| 082 | | 📄 Article — Jepsen analysis | ☐ | |
| 083 | | 🛠️ Exercice « conçois X » — base distribuée forte cohérence | ☐ | |
| **084** | | **🔁 REVUE HEBDO #12** — Bilan Partie II | ☐ | |

## Phase 3 — Données dérivées (Partie III)

| Jour | Date | Activité | ✅ | Note libre |
|------|------|----------|---|-----------|
| 085-112 | | Phase 3 — Batch + Stream + Futur | ☐ | voir PLAN.md |

## Phase 4 — Synthèse & capstone

| Jour | Date | Activité | ✅ | Note libre |
|------|------|----------|---|-----------|
| 113-126 | | Phase 4 — Capstone + design exercises + revue finale | ☐ | voir PLAN.md |
