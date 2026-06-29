# recall-prompts.md — Consignes de récupération « page blanche »

> Utilise ces consignes chaque matin (5 min) et lors des revues hebdo.  
> Règle : **pas de notes ouvertes**. Écris/dessine de mémoire. Note chaque lacune.

---

## Grappe 0 — Fiabilité · Scalabilité · Maintenabilité (Ch.1)

1. **Explique** la différence fault vs failure à voix haute. Donne un exemple concret de chacun tiré de ta propre expérience (stage, projet).
2. **Dessine** le graphe : Fault → (mécanisme de tolérance) → Failure évitée. Place les 3 types de pannes.
3. **Calcule** de tête : si tu as 1000 valeurs de latences (la plupart entre 50-100ms, quelques-unes à 5s), comment estimes-tu grossièrement le p99 ? Pourquoi la moyenne ne te le dirait pas ?
4. **Liste** les 3 aspects de la maintenabilité. Pour chaque aspect, donne une pratique d'ingénierie concrète qui l'améliore.
5. **Sketche** le compromis scale-up vs scale-out sur deux axes : coût et complexité.

---

## Grappe 1 — Modèles de données & langages de requête (Ch.2)

1. **Dessine** les 3 modèles de données (relationnel · document · graphe) avec un exemple de données qui convient naturellement à chacun.
2. **Explique** l'impedance mismatch : pourquoi les ORMs existent, quels problèmes ils résolvent, quels problèmes ils créent.
3. **Écris** une requête SQL déclarative et son équivalent impératif en Python pour filtrer des animaux par type. Explique pourquoi SQL permet plus d'optimisations.
4. **Quand** choisirais-tu MongoDB sur Postgres ? Donne 2 critères précis.
5. **Décris** un cas d'usage où le modèle graphe est clairement supérieur aux deux autres. Pourquoi ?

---

## Grappe 2 — Stockage & récupération (Ch.3)

1. **Dessine de mémoire** le chemin d'une **écriture** dans un LSM-tree : depuis l'API `put(key, value)` jusqu'au disque (memtable → WAL → flush → compaction).
2. **Dessine de mémoire** le chemin d'une **lecture** dans un LSM-tree : comment cherches-tu une clé qui pourrait être dans N SSTables ?
3. **Dessine** la structure d'un B-tree : racine · nœuds internes · feuilles · pages de taille fixe. Montre comment une recherche de clé descend l'arbre.
4. **Compare** LSM vs B-tree sur 4 axes : amplification écriture · amplification lecture · fragmentation · crash recovery.
5. **Explique** pourquoi le stockage en colonnes est meilleur pour `SELECT AVG(prix) FROM ventes WHERE année = 2024` que le stockage en lignes.
6. **Cite** 2 systèmes réels qui utilisent un LSM-tree et 2 qui utilisent un B-tree.

---

## Grappe 3 — Encodage & évolution (Ch.4)

1. **Compare** JSON vs Protobuf : taille approximative pour `{user_id: 12345, name: "Alice"}`. Pourquoi Protobuf est plus compact ?
2. **Explique** la différence entre compatibilité ascendante (*forward compatibility*) et descendante (*backward compatibility*). Donne un exemple d'ajout de champ.
3. **Dessine** les 3 modes de dataflow : via base de données · via services REST/RPC · via message queue. Pour chaque mode, quel est le défi de compatibilité principal ?
4. **Cite** un cas où Avro est préférable à Protobuf (hint : Kafka + schéma dynamique).
5. **Explique** ce que Protobuf fait si un décodeur reçoit un champ avec un numéro qu'il ne connaît pas (forward compatibility).

---

## Grappe 4 — Réplication (Ch.5)

1. **Dessine** les 3 topologies de réplication (mono-leader · multi-leader · sans leader) avec les flux de données.
2. **Explique** « read-your-writes » : quel problème cela résout-il ? Comment l'implémenter avec une réplication mono-leader asynchrone ?
3. **Démontre** avec des chiffres : si N=3, W=1, R=1 → peux-tu lire une valeur périmée ? Et si W=2, R=2 ?
4. **Décris** un scénario de *write skew* dans un système sans leader avec quorum.
5. **Cite** le papier Dynamo : quel est son paramètre de charge clé ? Quelle est son idée centrale pour la haute disponibilité ?

---

## Grappe 5 — Partitionnement (Ch.6)

1. **Dessine** un anneau de hachage cohérent avec 4 nœuds. Montre ce qui se passe quand un 5ᵉ nœud rejoint.
2. **Compare** partitionnement par plage de clés vs par hachage : pour quelles requêtes chacun est-il meilleur ?
3. **Explique** le problème du *hot spot* avec une clé de partitionnement mal choisie. Donne un exemple concret (ex. clé = timestamp).
4. **Qu'est-ce qu'un nœud virtuel** (*virtual node*) dans le hachage cohérent ? Quel problème résout-il ?
5. **Comment** fonctionne un index secondaire dans un système partitionné ? (scatter/gather)

---

## Grappe 6 — Transactions (Ch.7)

1. **Cite** les 4 propriétés ACID. Laquelle est la plus mal comprise ? Explique *consistency* (C) — c'est une propriété de l'application, pas du DB.
2. **Dessine** le tableau niveaux d'isolation × anomalies : pour chaque cellule, ✓ (évitée) ou ✗ (possible).
3. **Décris** un scénario de *write skew* (deux médecins se retirent simultanément de l'astreinte). Quel niveau d'isolation le prévient ?
4. **Explique** MVCC : comment un snapshot est-il créé ? Comment une transaction « voit » les données ?
5. **Compare** 2PL (*Two-Phase Locking*) et SSI (*Serializable Snapshot Isolation*) : avantages et inconvénients de chacun.

---

## Grappe 7 — Problèmes des systèmes distribués (Ch.8)

1. **Explique** le problème des réseaux non fiables : pourquoi un timeout ne te dit pas si la requête a été reçue ou non ?
2. **Dessine** une horloge de Lamport pour 3 processus échangeant des messages. Montre comment l'horloge avance.
3. **Explique** la différence entre horloge de Lamport et horloge vectorielle : quand a-t-on besoin de l'une vs l'autre ?
4. **Décris** le problème de NTP et des horloges de processus : pourquoi ne peut-on pas utiliser `System.currentTimeMillis()` pour ordonner des événements distribués ?
5. **Cite** une application de TrueTime (Google Spanner) : quel problème résout-il ? Quel est son compromis ?

---

## Grappe 8 — Cohérence & consensus (Ch.9)

1. **Définis** la linéarisabilité : en quoi est-ce plus fort que la cohérence sérialisable ?
2. **Explique** le *total order broadcast* : pourquoi est-il équivalent au consensus ?
3. **Dessine** la machine d'état Raft : états d'un nœud (follower · candidate · leader) et transitions.
4. **Explique** l'élection de leader Raft : que se passe-t-il si un candidat n'obtient pas la majorité ?
5. **Qu'est-ce qu'un fencing token** ? Pourquoi les verrous distribués seuls ne suffisent-ils pas ?
6. **Explique** pourquoi 2PC est bloquant en cas de panne du coordinateur.

---

## Grappe 9 — Traitement par lots (Ch.10)

1. **Décris** le paradigme MapReduce en 3 étapes. Donne un exemple concret (word count).
2. **Explique** la philosophie Unix appliquée au batch : immutabilité de l'input · composition de pipelines · idempotence.
3. **Compare** MapReduce et Spark : quel est le principal avantage de Spark pour les pipelines itératifs ?
4. **Qu'est-ce qu'un reduce-side join** vs un map-side join (*broadcast hash join*) ? Lequel choisir selon la taille des données ?

---

## Grappe 10 — Traitement de flux (Ch.11)

1. **Décris** la différence entre un système de messagerie *at-least-once*, *at-most-once* et *exactly-once*.
2. **Explique** ce qu'est un *watermark* dans le traitement de flux : quel problème résout-il pour les fenêtres de temps ?
3. **Dessine** les 3 types de fenêtres : tumbling · sliding · session. Donne un cas d'usage pour chacune.
4. **Qu'est-ce que le CDC** (*Change Data Capture*) ? Comment Debezium capture-t-il les changements Postgres ?
5. **Explique** *event sourcing* : quelle est la différence avec un système CRUD classique ?
