# papers/reading-list.md — Articles fondateurs

> Cartés par chapitre DDIA. Pour chaque article : **quel problème ? · idée clé · compromis**.  
> Méthode de lecture : abstract → intro → conclusion → figures → corps sélectif (≤ 40 min).  
> Tes fiches de lecture vont dans `papers/notes/<article>.md`.

---

## Phase 1 — Fondations (Partie I)

### Ch.3 — Stockage & récupération

**[1] Bigtable: A Distributed Storage System for Structured Data**  
Chang et al., Google, OSDI 2006  
— Trouver : recherche web `Bigtable OSDI 2006 PDF`  
- **Quel problème :** stocker des pétaoctets de données semi-structurées à l'échelle Google (crawl web, Maps, Analytics)
- **Idée clé :** table clairsemée multi-dimensionnelle (row key + column family + timestamp) sur un LSM-tree distribué (SSTable + GFS)
- **Compromis :** cohérence ligne-par-ligne (pas de transactions multi-lignes) · compaction coûteuse · opérations complexes pour les applications
- **Lien DDIA :** *implémentation de référence* des SSTables et du LSM-tree distribué

**[2] The Log-Structured Merge-Tree (LSM-Tree)**  
O'Neil, Cheng, Gawlick, O'Neil, 1996  
— Trouver : recherche `O'Neil LSM-Tree 1996 ACM`  
- **Quel problème :** le B-tree classique est limité par l'I/O aléatoire pour les workloads write-heavy
- **Idée clé :** tamponner les écritures en mémoire (C0), les fusionner séquentiellement vers des niveaux sur disque (C1, C2…)
- **Compromis :** écritures rapides et séquentielles vs lectures potentiellement lentes (plusieurs niveaux à chercher) · compaction en fond
- **Lien DDIA :** fondement théorique de RocksDB, Cassandra, LevelDB

---

## Phase 2 — Données distribuées (Partie II)

### Ch.5 — Réplication

**[3] Dynamo: Amazon's Highly Available Key-Value Store**  
DeCandia et al., Amazon, SOSP 2007  
— Trouver : recherche `Dynamo Amazon SOSP 2007 PDF`  
- **Quel problème :** disponibilité maximale pour le panier d'achat Amazon — même en cas de pannes partielles, l'écriture ne doit jamais échouer
- **Idée clé :** modèle sans leader · quorums ajustables (N, W, R) · *sloppy quorum* + *hinted handoff* · vecteurs d'horloge pour la résolution de conflits · hachage cohérent
- **Compromis :** cohérence éventuelle (pas de garantie de lecture récente) · conflits à résoudre par l'application · "always writeable" sacrifie la cohérence forte
- **Lien DDIA :** article fondateur de la réplication sans leader et du hachage cohérent · influence Cassandra, Riak

### Ch.7 — Transactions

**[4] A Critique of ANSI SQL Isolation Levels**  
Berenson, Bernstein, Gray, Melton, O'Neil, O'Neil, SIGMOD 1995  
— Trouver : recherche `Berenson ANSI SQL Isolation SIGMOD 1995`  
- **Quel problème :** les définitions ANSI SQL des niveaux d'isolation sont ambiguës et incomplètes — elles ne couvrent pas toutes les anomalies
- **Idée clé :** formalisation rigoureuse des anomalies (dirty read, non-repeatable read, phantom, write skew, lost update) et des niveaux qui les évitent
- **Compromis :** le niveau SERIALIZABLE élimine toutes les anomalies mais au prix de performances
- **Lien DDIA :** DDIA s'appuie directement sur cette taxonomie (Ch.7, niveaux d'isolation)

### Ch.8 — Problèmes des systèmes distribués

**[5] Time, Clocks, and the Ordering of Events in a Distributed System**  
Lamport, Communications of the ACM, 1978  
— Trouver : recherche `Lamport 1978 Time Clocks ACM`  
- **Quel problème :** comment ordonner des événements dans un système distribué où il n'y a pas d'horloge globale fiable ?
- **Idée clé :** relation *happens-before* (→) · horloges logiques (compteurs) · *total order* par tie-breaking · les horloges vectorielles (extension) pour détecter la concurrence
- **Compromis :** l'horloge de Lamport donne un ordre total mais pas un ordre causal complet (ne détecte pas la concurrence)
- **Lien DDIA :** fondement théorique de Ch.8 (horloges), Ch.9 (total order broadcast), Ch.11 (event ordering dans les streams)

### Ch.9 — Cohérence & consensus

**[6] In Search of an Understandable Consensus Algorithm (Raft)**  
Ongaro & Ousterhout, USENIX ATC 2014  
— Trouver : recherche `Raft Ongaro 2014 PDF` ou `raft.github.io`  
- **Quel problème :** Paxos est correct mais incompréhensible — personne ne sait l'implémenter fidèlement sans introduire des bugs subtils
- **Idée clé :** décomposer le consensus en sous-problèmes indépendants (élection de leader · réplication de log · sécurité) + propriété de **Log Matching** + **Leader Completeness**
- **Compromis :** légèrement moins efficace que Paxos en termes de messages · nécessite un leader stable (latence si pas de leader)
- **Lien DDIA :** Raft est le consensus de référence dans DDIA (etcd, CockroachDB, TiKV)

**[7] Paxos Made Simple**  
Lamport, ACM SIGACT News, 2001  
— Trouver : `Paxos Made Simple Lamport 2001 PDF`  
- **Quel problème :** l'article original de Paxos était délibérément obscur — celui-ci réexplique simplement
- **Idée clé :** deux phases (Prepare/Promise · Accept/Accepted) · la majorité garantit la cohérence · un seul décideur (*distinguished proposer*)
- **Compromis :** n'assure pas la vivacité (*liveness*) sans élection de leader stable · plus difficile à implémenter correctement que Raft
- **Lien DDIA :** comprendre les bases du consensus avant de lire Raft

**[8] Spanner: Google's Globally Distributed Database**  
Corbett et al., Google, OSDI 2012 · aussi dans TODS 2013  
— Trouver : `Spanner OSDI 2012 Google PDF`  
- **Quel problème :** transactions distribuées globales avec cohérence externe (linéarisabilité) à l'échelle planétaire
- **Idée clé :** **TrueTime API** — horloges GPS + atomic qui bornent l'incertitude de temps → utiliser `commit_wait` pour garantir l'ordre causal entre transactions dans différents datacenters
- **Compromis :** `commit_wait` ajoute de la latence (typiquement 1-7ms) · infrastructure hardware spécialisée (GPS + atomic clocks)
- **Lien DDIA :** illustre comment des horloges précises peuvent résoudre des problèmes de cohérence distribués (alternative au consensus pur)

**[9] Jepsen — analyses de cohérence (Kyle Kingsbury)**  
jepsen.io · divers systèmes · 2013-présent  
— Trouver : `jepsen.io` · choisir une analyse récente (MongoDB, Postgres, etcd)  
- **Quel problème :** vérifier empiriquement les garanties de cohérence annoncées par les systèmes de bases de données
- **Idée clé :** injecter des pannes réseau réelles pendant des opérations concurrentes · vérifier les traces avec `Knossos` (vérificateur de linéarisabilité) · les bugs trouvés sont souvent réels et exploitables
- **Compromis :** les vendors annoncent des garanties que les tests empiriques révèlent comme fausses (ex. MongoDB affirmait la cohérence forte avant Jepsen)
- **Lien DDIA :** exemples concrets des problèmes de Ch.8-9 en production réelle

---

## Phase 3 — Données dérivées (Partie III)

### Ch.10 — Traitement par lots

**[10] MapReduce: Simplified Data Processing on Large Clusters**  
Dean & Ghemawat, Google, OSDI 2004  
— Trouver : `MapReduce Google OSDI 2004 PDF`  
- **Quel problème :** traiter des téraoctets de données sur des milliers de machines sans que les ingénieurs aient à gérer la distribution, la tolérance aux pannes et le parallélisme
- **Idée clé :** abstraction Map (transformation locale) + Reduce (agrégation par clé) · re-exécution automatique en cas de panne · input/output immuables sur GFS
- **Compromis :** pas optimisé pour les pipelines itératifs (relit depuis disque entre chaque étape) · latence élevée · shuffle réseau coûteux
- **Lien DDIA :** fondement conceptuel du Ch.10 · Spark améliore les compromis (in-memory, DAG)

### Ch.11 — Traitement de flux

**[11] The Log: What every software engineer should know about real-time data**  
Jay Kreps (LinkedIn), blog post, 2013  
— Trouver : recherche `Jay Kreps The Log 2013`  
- **Quel problème :** pourquoi les systèmes distribués convergent-ils tous vers un journal append-only (WAL, réplication log, event sourcing, Kafka) comme primitive centrale ?
- **Idée clé :** le **log ordonné et distribué** est la primitive universelle qui unifie bases de données, réplication, flux de données et intégration de systèmes
- **Compromis :** stockage log-first = coût de rétention · nécessite une architecture « état dérivé » plutôt que mutable
- **Lien DDIA :** concept transversal reliant Ch.3 (WAL), Ch.5 (réplication), Ch.11 (Kafka), Ch.12 (futur)

**[12] The Dataflow Model: A Practical Approach to Balancing Correctness, Latency, and Cost in Massive-Scale, Unbounded, Out-of-Order Data Processing**  
Akidau et al., Google, VLDB 2015  
— Trouver : `Dataflow Model VLDB 2015 Google`  
- **Quel problème :** unifier batch et stream dans un modèle unique qui gère les données en retard (*late data*), les fenêtres temporelles et les watermarks
- **Idée clé :** **fenêtres** (quoi grouper) · **déclencheurs** (*triggers*, quand émettre) · **raffinement** (que faire des données tardives) · distinction *event time* vs *processing time*
- **Compromis :** complexité du modèle · watermarks imparfaits (données très en retard peuvent être ignorées)
- **Lien DDIA :** base conceptuelle du Ch.11 (fenêtrage, watermarks) · fondement de Apache Beam / Flink

---

## Article bonus

**[13] FLP Impossibility**  
Fischer, Lynch, Paterson, JACM 1985  
— Titre : *Impossibility of Distributed Consensus with One Faulty Process*  
- **Résultat :** dans un système asynchrone (délais de messages non bornés), il est impossible de résoudre le consensus de manière déterministe même avec une seule panne possible
- **Pourquoi le lire :** comprendre *pourquoi* Raft et Paxos ont des timeouts et de l'aléatoire — et pourquoi c'est inévitable
- **Niveau :** mathématique · lit uniquement le théorème et la preuve intuitive (abstract + intro)
