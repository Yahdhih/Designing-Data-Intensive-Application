# PLAN.md — Curriculum DDIA Mastery

## Durées estimées à 1 h/jour

| Phase | Thème | Jours | Partie DDIA (1ʳᵉ éd.) |
|-------|-------|-------|----------------------|
| **0** | Mise en route | 1–4 | Intro + Ch. 1 |
| **1** | Fondations | 5–28 | Partie I · Ch. 2-4 |
| **2** | Données distribuées ← **LE CŒUR** | 29–84 | Partie II · Ch. 5-9 |
| **3** | Données dérivées | 85–112 | Partie III · Ch. 10-12 |
| **4** | Synthèse & capstone | 113–126 | Transversal |
| **Total** | | **~126 jours** | |

> ⚠️ Ces durées se **recalibrent** une fois `reference/toc.md` rempli.  
> Vise ~5-10 pages de lecture *active* par session de 40 min (la pratique consomme le reste du temps).  
> La **Partie II seule** = ~2 mois bien tassés avec pratique profonde.  
> Arc complet avec jouets + labos + articles ≈ **5-8 mois** selon ton rythme.

---

## Note sur les deux éditions

Le plan est ancré sur des **grappes de concepts stables** d'une édition à l'autre.

**1ʳᵉ éd. (2017)** — structure de référence :
- Partie I : Ch.1 (fiabilité/scalabilité) · Ch.2 (modèles de données) · Ch.3 (stockage) · Ch.4 (encodage)
- Partie II : Ch.5 (réplication) · Ch.6 (partitionnement) · Ch.7 (transactions) · Ch.8 (problèmes distribués) · Ch.9 (consensus)
- Partie III : Ch.10 (batch) · Ch.11 (stream) · Ch.12 (futur)

**2ᵉ éd. (2026)** — chapitres réorganisés, à mapper via `reference/toc.md`.  
Différences majeures : stockage objet comme modèle dominant · streaming → maintenance incrémentale de vues · cloud-natif.

---

## Tableau curriculum complet

### Phase 0 — Mise en route (jours 1-4)

| Jour | Activité | Type | Jouet | Labo | Article |
|------|----------|------|-------|------|---------|
| 1 | Setup : édition · Docker · venv · TOC calibration · cartes Anki | 🔧 Setup | — | `compose.light.yml` test | — |
| 2 | Ch.1 § Fiabilité : fault vs failure · 3 types de pannes · chaos engineering | 📖 Lecture | — | — | — |
| 3 | Ch.1 § Scalabilité : percentiles p50/p95/p99 vs moyenne | 🛠️ Jouet | `percentiles.py` | — | — |
| 4 | Ch.1 § Maintenabilité : opérabilité · simplicité · évolvabilité · consolidation | 📖 Lecture | — | — | — |

---

### Phase 1 — Fondations (jours 5-28, Partie I)

| Jours | Grappe de concepts | Type | Jouet | Labo | Article |
|-------|-------------------|------|-------|------|---------|
| 5 | Ch.2 — Modèle relationnel vs document : impédance, JSON imbriqué, one-to-many | 📖 | — | — | — |
| 6 | Ch.2 — Modèle graphe · langages de requête : déclaratif vs impératif, SQL vs MapReduce, Datalog | 📖 | — | — | — |
| **7** | **REVUE HEBDO #1** — Page blanche Ch.1-2 · redessine schémas · cartes | 🔁 | — | — | — |
| 8 | Ch.2 — Labo : Postgres vs MongoDB sur même domaine · `EXPLAIN` · requêtes déclaratives | 🧪 | — | Postgres + Mongo | — |
| 9 | Ch.3 — Index par hachage · SSTables · compaction · filtre de Bloom | 📖 | — | — | — |
| 10 | Ch.3 — B-trees · WAL · OLTP vs OLAP · stockage en colonnes | 📖 | — | — | — |
| 11 | Ch.3 — Jouet Bitcask : log append-only + index hachage (byte offsets) | 🛠️ | `bitcask.py` | — | — |
| 12 | Ch.3 — Jouet mini-LSM : SSTables triées + compaction par fusion | 🛠️ | `lsm.py` | — | — |
| 13 | Article : **Bigtable** (Chang et al. 2006) ou **LSM-Tree** (O'Neil 1996) | 📄 | — | — | Bigtable/LSM |
| **14** | **REVUE HEBDO #2** — Ch.2-3 · redessine LSM + B-tree · compare amplification | 🔁 | — | — | — |
| 15 | Ch.3 — Jouet mini-B-tree (nœuds + insertion + recherche) | 🛠️ | `btree.py` | — | — |
| 16 | Ch.3 — Labo Postgres : `EXPLAIN ANALYZE` · B-tree vs hash vs GIN index | 🧪 | — | Postgres | — |
| 17 | Ch.3 — Stockage en colonnes : compression bitmap · vectorisé · Parquet (lien Spark) | 📖 | — | — | — |
| 18 | Ch.4 — Encodage : JSON/XML vs Thrift/Protobuf/Avro · tailles binaires | 📖 | — | — | — |
| 19 | Ch.4 — Compatibilité ascendante/descendante · rolling upgrade · modes de dataflow | 📖 | — | — | — |
| 20 | Ch.4 — Jouet encodeur binaire longueur-préfixé + démo évolution de schéma | 🛠️ | `encoder.py` | — | — |
| **21** | **REVUE HEBDO #3** — Bilan Phase 1 · matrices de compromis · preview Phase 2 | 🔁 | — | — | — |
| 22 | Ch.4 — Labo : sérialiser avec `protobuf` Python, ajouter un champ, vérifier compat | 🧪 | — | — | — |
| 23 | Ch.3-4 — Exercice « Conçois X » : conçois le stockage d'un système de journalisation | 🛠️ | — | — | — |
| 24 | Ch.4 — Article : **The Log** (Jay Kreps 2013) — premiers éléments du stream Ch.11 | 📄 | — | — | The Log |
| 25-27 | Consolidation Phase 1 · enrichir `tradeoffs.md` · fiches de révision | 📖/🛠️ | — | — | — |
| **28** | **REVUE HEBDO #4** — Fin Phase 1 · teach-back Ch.1-4 complet | 🔁 | — | — | — |

---

### Phase 2 — Données distribuées (jours 29-84, Partie II · CŒUR)

#### Réplication (jours 29-42)

| Jours | Grappe de concepts | Type | Jouet | Labo | Article |
|-------|-------------------|------|-------|------|---------|
| 29 | Ch.5 — Réplication mono-leader : WAL shipping · retard · read-your-writes | 📖 | — | — | — |
| 30 | Ch.5 — Anomalies : monotonic reads · consistent prefix reads · retard de réplication | 📖 | — | — | — |
| 31 | Ch.5 — Jouet sim mono-leader : retard artificiel → montrer les anomalies de lecture | 🛠️ | `single_leader.py` | — | — |
| 32 | Ch.5 — Réplication multi-leader : conflits · CRDTs · last-write-wins | 📖 | — | — | — |
| 33 | Ch.5 — Sans leader (Dynamo-style) : quorums W+R>N · sloppy quorum · hinted handoff | 📖 | — | — | — |
| 34 | Ch.5 — Jouet simulateur quorum : montrer quand W=R=1 donne une lecture périmée | 🛠️ | `quorum_sim.py` | — | — |
| **35** | **REVUE HEBDO #5** | 🔁 | — | — | — |
| 36 | Article : **Dynamo** (DeCandia et al. 2007) — quorums, vector clocks, hinted handoff | 📄 | — | — | Dynamo |
| 37 | Ch.5 — Labo Postgres : streaming replication · mesurer le lag · `pg_stat_replication` | 🧪 | — | Postgres | — |
| 38 | Ch.5 — Labo Cassandra : cohérence ONE / QUORUM / ALL · observer les compromis | 🧪 | — | Cassandra | — |
| 39 | Ch.5 — Exercice « Conçois X » : fil d'actualité read-your-writes avec réplication | 🛠️ | — | — | — |
| 40 | Ch.5 — Synthèse réplication : matrice mono/multi/sans-leader · modes de défaillance | 📖 | — | — | — |
| 41 | Ch.5 — Redessine de mémoire toutes les topologies de réplication | 🛠️ | — | — | — |
| **42** | **REVUE HEBDO #6** | 🔁 | — | — | — |

#### Partitionnement (jours 43-49)

| Jours | Grappe de concepts | Type | Jouet | Labo | Article |
|-------|-------------------|------|-------|------|---------|
| 43 | Ch.6 — Partitionnement par plage vs par hachage · hot spots | 📖 | — | — | — |
| 44 | Ch.6 — Hachage cohérent + nœuds virtuels · rééquilibrage | 📖 | — | — | — |
| 45 | Ch.6 — Jouet anneau de hachage cohérent avec rééquilibrage et démo de point chaud | 🛠️ | `consistent_hash.py` | — | — |
| 46 | Ch.6 — Index secondaires par partition · scatter/gather · routage des requêtes | 📖 | — | — | — |
| 47 | Ch.6 — Labo : sharding manuel dans Postgres (partitionnement de table) | 🧪 | — | Postgres | — |
| 48 | Ch.6 — Synthèse partitionnement · matrice de compromis | 📖 | — | — | — |
| **49** | **REVUE HEBDO #7** | 🔁 | — | — | — |

#### Transactions (jours 50-63)

| Jours | Grappe de concepts | Type | Jouet | Labo | Article |
|-------|-------------------|------|-------|------|---------|
| 50 | Ch.7 — ACID : atomicité · cohérence · isolation · durabilité | 📖 | — | — | — |
| 51 | Ch.7 — Niveaux d'isolation : read uncommitted · read committed | 📖 | — | — | — |
| 52 | Ch.7 — Snapshot isolation · MVCC · *write skew* · *phantom reads* | 📖 | — | — | — |
| 53 | Ch.7 — Sérialisabilité : 2PL · SSI (Serializable Snapshot Isolation) | 📖 | — | — | — |
| 54 | Ch.7 — Jouet KV en mémoire avec MVCC + snapshot isolation + détecter write skew | 🛠️ | `mvcc_store.py` | — | — |
| 55 | Ch.7 — Jouet suite : démo *lost update*, write skew, phantom | 🛠️ | `anomalies.py` | — | — |
| 56 | **REVUE HEBDO #8** | 🔁 | — | — | — |
| 57 | Article : **A Critique of ANSI SQL Isolation Levels** (Berenson et al. 1995) | 📄 | — | — | Critique ANSI |
| 58 | Ch.7 — Labo Postgres : reproduire *lost update* + *write skew* en changeant `SET TRANSACTION ISOLATION LEVEL` | 🧪 | — | Postgres | — |
| 59 | Ch.7 — Labo Postgres suite : `SELECT FOR UPDATE` · `FOR SHARE` · SSI | 🧪 | — | Postgres | — |
| 60 | Ch.7 — Exercice « Conçois X » : système de réservation sans double-booking | 🛠️ | — | — | — |
| 61 | Ch.7 — Synthèse transactions : matrice niveaux d'isolation × anomalies | 📖 | — | — | — |
| 62 | Ch.7 — Redessine : hiérarchie des niveaux d'isolation + exemples d'anomalies | 🛠️ | — | — | — |
| **63** | **REVUE HEBDO #9** | 🔁 | — | — | — |

#### Problèmes des systèmes distribués (jours 64-70)

| Jours | Grappe de concepts | Type | Jouet | Labo | Article |
|-------|-------------------|------|-------|------|---------|
| 64 | Ch.8 — Réseaux non fiables : retards · pertes · détection de panne | 📖 | — | — | — |
| 65 | Ch.8 — Horloges : temps monotone vs temps mur · NTP · Google TrueTime | 📖 | — | — | — |
| 66 | Ch.8 — Horloges de Lamport + horloges vectorielles | 📖 | — | — | — |
| 67 | Ch.8 — Jouet : implémentation horloges de Lamport + vectorielles + vérificateur de causalité | 🛠️ | `clocks.py` | — | — |
| 68 | Article : **Time, Clocks, and the Ordering of Events** (Lamport 1978) | 📄 | — | — | Lamport Clocks |
| 69 | Ch.8 — Labo : injection de latence réseau (`tc netem` · `docker pause`) → ressentir CAP | 🧪 | — | Tous | — |
| **70** | **REVUE HEBDO #10** | 🔁 | — | — | — |

#### Cohérence & consensus (jours 71-84)

| Jours | Grappe de concepts | Type | Jouet | Labo | Article |
|-------|-------------------|------|-------|------|---------|
| 71 | Ch.9 — Linéarisabilité vs cohérence éventuelle · modèles de cohérence | 📖 | — | — | — |
| 72 | Ch.9 — Total order broadcast · 2PC (Two-Phase Commit) | 📖 | — | — | — |
| 73 | Ch.9 — Consensus : Paxos (vue haut niveau) · Raft (introduction) | 📖 | — | — | — |
| 74 | Ch.9 — Raft : élection de leader + réplication de log + sécurité | 📖 | — | — | — |
| 75 | Ch.9 — Jouet mini-Raft : élection de leader + réplication log (messages simulés) | 🛠️ | `raft_sim.py` | — | — |
| 76 | Ch.9 — Jouet mini-Raft suite : machine d'état · commit index · fencing token | 🛠️ | `raft_sim.py` | — | — |
| **77** | **REVUE HEBDO #11** | 🔁 | — | — | — |
| 78 | Article : **Raft** (Ongaro & Ousterhout 2014) — *In Search of an Understandable Consensus Algorithm* | 📄 | — | — | Raft |
| 79 | Article : **Paxos Made Simple** (Lamport 2001) — lecture comparative | 📄 | — | — | Paxos |
| 80 | Ch.9 — Labo etcd : élection · verrous · watch · fencing token | 🧪 | — | etcd | — |
| 81 | Ch.9 — ZooKeeper : rôle · recipes (leader election, distributed lock) | 📖/🧪 | — | ZooKeeper | — |
| 82 | Lecture bonus : **analyse Jepsen** (Kingsbury) sur un vrai système | 📄 | — | — | Jepsen |
| 83 | Exercice « Conçois X » : conçois une base distribuée avec cohérence forte | 🛠️ | — | — | — |
| **84** | **REVUE HEBDO #12** — Bilan Phase 2 · redessine : hiérarchie cohérence · Raft FSM · arbres de décision | 🔁 | — | — | — |

---

### Phase 3 — Données dérivées (jours 85-112, Partie III)

#### Traitement par lots (jours 85-98)

| Jours | Grappe de concepts | Type | Jouet | Labo | Article |
|-------|-------------------|------|-------|------|---------|
| 85 | Ch.10 — Philosophie Unix + MapReduce : input/output immuables · scatter/gather | 📖 | — | — | — |
| 86 | Ch.10 — Jointures MapReduce : reduce-side join · map-side join (hash join) | 📖 | — | — | — |
| 87 | Ch.10 — Jouet mini-MapReduce : word count → jointure reduce-side → broadcast hash join | 🛠️ | `mapreduce.py` | — | — |
| 88 | Article : **MapReduce** (Dean & Ghemawat, Google 2004) | 📄 | — | — | MapReduce |
| 89 | Ch.10 — Labo : Spark avec le cadre conceptuel batch · DAG · shuffle | 🧪 | — | Spark | — |
| 90 | Ch.10 — Moteurs de dataflow : Flink, Spark vs MapReduce · amélioration des compromis | 📖 | — | — | — |
| **91** | **REVUE HEBDO #13** | 🔁 | — | — | — |
| 92-98 | Ch.10 suite · Labo Spark avancé · exercice de conception batch | 📖/🧪 | — | Spark | — |

#### Traitement de flux (jours 99-112)

| Jours | Grappe de concepts | Type | Jouet | Labo | Article |
|-------|-------------------|------|-------|------|---------|
| 99 | Ch.11 — Flux d'événements : sources · journaux · messagerie · at-least-once vs exactly-once | 📖 | — | — | — |
| 100 | Ch.11 — CDC (Change Data Capture) · event sourcing · état dérivé | 📖 | — | — | — |
| 101 | Ch.11 — Jouet broker append-only : offsets · groupes de consommateurs · replay | 🛠️ | `log_broker.py` | — | — |
| 102 | Ch.11 — Fenêtrage : tumbling · sliding · session · watermarks | 📖 | — | — | — |
| 103 | Ch.11 — Jouet fenêtres : implémentation tumbling/sliding/session | 🛠️ | `windowing.py` | — | — |
| 104 | Article : **The Log** (Jay Kreps 2013) — *What every software engineer should know about real-time data* | 📄 | — | — | The Log |
| **105** | **REVUE HEBDO #15** | 🔁 | — | — | — |
| 106 | Ch.11 — Jouet CDC depuis WAL Postgres → émettre des événements | 🛠️ | `cdc_wal.py` | Postgres | — |
| 107 | Ch.11 — Labo Kafka : log compaction · groupes de consommateurs · ordre par partition | 🧪 | — | Kafka | — |
| 108 | Ch.11 — Labo Debezium : CDC Postgres → Kafka · replay · exactement-une-fois | 🧪 | — | Kafka + Debezium | — |
| 109 | Article : **The Dataflow Model** (Akidau et al., Google 2015) — fenêtres/watermarks | 📄 | — | — | Dataflow |
| 110 | Ch.12 — L'avenir : débundler la base · état dérivé · correction de bout en bout | 📖 | — | — | — |
| 111 | Ch.12 — Si 2ᵉ éd. : streaming → maintenance incrémentale de vues (Materialize) | 📖 | — | — | — |
| **112** | **REVUE HEBDO #16** — Bilan Phase 3 · exercice « conçois un pipeline CDC complet » | 🔁 | — | — | — |

---

### Phase 4 — Synthèse & capstone (jours 113-126)

| Jours | Activité | Type |
|-------|----------|------|
| 113-115 | Capstone : document de conception d'un **KV partitionné + répliqué** (WAL + hachage cohérent + quorums + CDC) | 🛠️ |
| 116-119 | Prototype partiel du capstone : `code/99-capstone/` | 🛠️ |
| 120 | Exercice « conçois X » #1 : raccourcisseur d'URL distribué | 🛠️ |
| 121 | Exercice « conçois X » #2 : fil d'actualité (fan-out read vs write) | 🛠️ |
| **122** | **REVUE HEBDO #17** | 🔁 |
| 123 | Exercice « conçois X » #3 : système de paiement idempotent | 🛠️ |
| 124 | Passe finale : re-dériver de mémoire hiérarchie de cohérence + arbres de décision | 🛠️ |
| 125 | Teach-back : ré-explique DDIA complet comme si tu enseignais à un pair | 🛠️ |
| **126** | **REVUE FINALE** — Balayage de toutes les cartes · `tradeoffs.md` complet · célèbre 🎉 | 🔁 |

---

## Règles de rotation des types d'activité

- **Ne jamais enchaîner plus de 2 lectures consécutives.**
- Alterner les 4 types sur chaque semaine : au moins 1 jouet, 1 labo, 1 lecture, 1 article ou revue.
- Sur l'ensemble du plan : ~1/3 lecture · ~1/3 jouet+labo · ~1/3 articles+consolidation.

## Critères « terminé » par type

| Type | Terminé quand… |
|------|---------------|
| 📖 Lecture | Résumé 3-5 puces en tes mots · 2-3 cartes ajoutées · 1 entrée tradeoffs |
| 🛠️ Jouet | Le test passe OU le comportement attendu est observé et documenté |
| 🧪 Labo | Les 3 questions (que se passe-t-il ? pourquoi ? quel compromis ?) sont répondues |
| 📄 Article | Problème · idée clé · compromis rédigés dans `papers/notes/` |
| 🔁 Revue | Page blanche faite · schémas redessinés · cartes balayées · `tradeoffs.md` mis à jour |
