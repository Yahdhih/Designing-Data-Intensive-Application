# tradeoffs.md — Matrices de compromis DDIA

> **Enrichi à chaque chapitre.** C'est ton document de référence pour les exercices « Conçois X ».  
> Format : **Technique | Quand l'utiliser | Coûts & limites | Modes de défaillance | Exemple**

---

## Chapitre 1 — Fiabilité · Scalabilité · Maintenabilité

| Technique | Quand l'utiliser | Coûts & limites | Modes de défaillance | Exemple de système |
|-----------|-----------------|-----------------|---------------------|-------------------|
| **Redondance matérielle** (RAID, multi-PSU, double NIC) | Pannes matérielles fréquentes, SLA élevé | Coût hardware × 2 · complexité opérationnelle | SPOF sur le contrôleur RAID | AWS EC2 multi-AZ |
| **Scale-up** (vertical) | Charge croissante, architecture simple, budget disponible | Limite physique du matériel · SPOF · coût élevé | Panne totale de la machine | Postgres sur grosse instance RDS |
| **Scale-out** (horizontal) | Charge dépassant une seule machine · résilience | Complexité de distribution · cohérence à gérer | Nœud lent (tail latency amplification) | Cassandra · Kafka |
| **Chaos engineering** | Systèmes complexes · vérification des mécanismes de tolérance | Risque de vrais incidents si mal calibré | Panne provoquée non contenue | Netflix Chaos Monkey |
| **Monitoring / alerting** | Tout système en production | Faux positifs · bruit | Alerte non déclenchée lors d'une vraie panne | Prometheus + Grafana |

---

## Chapitre 2 — Modèles de données

| Technique | Quand l'utiliser | Coûts & limites | Modes de défaillance | Exemple de système |
|-----------|-----------------|-----------------|---------------------|-------------------|
| **Modèle relationnel** (SQL) | Données structurées · jointures · transactions ACID | Schéma rigide · impedance avec les OOP · scalabilité horizontale complexe | N+1 queries · jointures lentes sur données massives | Postgres · MySQL |
| **Modèle document** (JSON/BSON) | Données hiérarchiques · one-to-many · lecture par document entier | Jointures difficiles · duplication de données · transactions multi-documents complexes | Données incohérentes si pas de transactions | MongoDB · CouchDB |
| **Modèle graphe** | Relations many-to-many · traversées de graphes (recommandations, fraude) | Scalabilité horizontale difficile · outils spécialisés | Explosion mémoire sur traversées profondes | Neo4j · Amazon Neptune |
| **Déclaratif** (SQL) | Requêtes sur données structurées · optimisations automatiques | Perte de contrôle sur l'exécution | Mauvais plan d'exécution (fix : `EXPLAIN`, hints) | SQL · Datalog |
| **Impératif** (code applicatif) | Logique métier complexe · contrôle total | Code verbeux · pas d'optimisation automatique | Boucles N+1 · fuites mémoire | Java/Python ORM |

---

## Chapitre 3 — Stockage & récupération

| Technique | Quand l'utiliser | Coûts & limites | Modes de défaillance | Exemple de système |
|-----------|-----------------|-----------------|---------------------|-------------------|
| **Index hachage (Bitcask)** | KV simple · accès par clé exacte · écriture rapide | Toutes les clés en RAM · pas de range scan · compaction périodique | Perte des données en RAM si crash sans WAL | Riak Bitcask |
| **LSM-tree** | Workload write-heavy · ingestion massive | Amplification lecture (SSTs multiples) · compaction en fond consomme I/O | Compaction lagging → lecture très lente | RocksDB · LevelDB · Cassandra |
| **B-tree** | Workload read-heavy · range scans · OLTP | Amplification écriture (split de pages) · fragmentation | B-tree corrompu si crash pendant écriture → WAL requis | Postgres · MySQL InnoDB |
| **Stockage colonne** (Parquet, ORC) | OLAP · agrégations sur sous-ensemble de colonnes | Mise à jour lente · requêtes par ligne inefficaces | Données incohérentes si partitions incomplètes | BigQuery · Redshift · Spark |
| **Filtre de Bloom** | Éviter des lectures disque inutiles sur SSTables | Faux positifs (taux configurable) · RAM pour le filtre | Faux positif → lecture inutile mais pas incorrecte | RocksDB · HBase |

---

## Chapitre 4 — Encodage & évolution

| Technique | Quand l'utiliser | Coûts & limites | Modes de défaillance | Exemple de système |
|-----------|-----------------|-----------------|---------------------|-------------------|
| **JSON / XML** | APIs publiques · lisibilité humaine · schéma flexible | Taille élevée · pas de types stricts · évolution de schéma non validée | Champ manquant non détecté → NullPointerException silencieux | REST APIs |
| **Protobuf / Thrift** | Communication inter-services · taille critique | Dépendance au fichier `.proto` · lisibilité humaine nulle | Numéro de champ modifié → incompatibilité silencieuse | gRPC · Thrift (Facebook) |
| **Avro** | Pipelines de données · schéma enregistré séparément · Kafka | Schéma requis pour décoder · Schema Registry à opérer | Incompatibilité de schéma → erreur de désérialisation | Kafka + Confluent Schema Registry |

---

## À compléter — grappes suivantes

*(Ajoute ici au fur et à mesure de la Phase 2 et 3)*

### Chapitre 5 — Réplication

| Technique | Quand l'utiliser | Coûts & limites | Modes de défaillance | Exemple |
|-----------|-----------------|-----------------|---------------------|---------|
| **Mono-leader** | Cohérence forte des lectures · transactions simples | Leader = goulot d'étranglement écriture · failover complexe | Split-brain si failover automatique mal configuré | Postgres · MySQL · Kafka |
| **Multi-leader** | Écriture multi-datacenter · disponibilité offline | Conflits d'écriture à résoudre · complexité | Conflit non résolu → données incohérentes | CouchDB · Google Docs (CRDT) |
| **Sans leader (Dynamo-style)** | Haute disponibilité · partition tolerance · écriture rapide | Cohérence éventuelle · lectures potentiellement périmées | Quorum non atteint si W+R ≤ N | Cassandra · DynamoDB · Riak |

### Chapitre 7 — Transactions

| Niveau d'isolation | Anomalies évitées | Anomalies possibles | Performance |
|-------------------|------------------|--------------------| ------------|
| Read uncommitted | (aucune) | Dirty read · Non-repeatable read · Phantom | Très élevée |
| Read committed | Dirty read | Non-repeatable read · Write skew · Phantom | Élevée |
| Snapshot isolation | Dirty read · Non-repeatable read | Write skew · Phantom (parfois) | Moyenne |
| Sérialisable | Toutes | (aucune) | Faible |

### Chapitre 9 — Consensus

| Algorithme | Tolérance aux pannes | Garantie | Complexité | Exemple |
|-----------|---------------------|----------|------------|---------|
| **2PC** (Two-Phase Commit) | 0 panne (bloquant si coordinateur tombe) | Atomicité distribuée | O(n) messages | JDBC XA · MySQL NDB |
| **Raft** | (n-1)/2 pannes (majorité) | Safety + Liveness | O(n log n) | etcd · CockroachDB |
| **Paxos** | (n-1)/2 pannes | Safety (Liveness nécessite extensions) | Plus complexe | Chubby (Google) · Zab (ZooKeeper) |
