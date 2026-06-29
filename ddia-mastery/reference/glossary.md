# glossary.md — Glossaire DDIA

> Enrichi à chaque chapitre. Écris les définitions dans tes propres mots — pas de copier-coller du livre.

Format : **terme** (*terme anglais*) : définition · chapitre(s) de référence.

---

## A

**Atomicité** (*atomicity*) : propriété ACID — une transaction est soit entièrement appliquée, soit entièrement annulée. Pas d'état intermédiaire visible. · Ch.7

## B

**B-tree** : structure d'index en arbre équilibré où les données sont stockées dans des pages de taille fixe. Les mises à jour se font en place (avec WAL pour la récupération). · Ch.3

## C

**CDC — Change Data Capture** : technique pour capturer chaque modification d'une base de données comme un flux d'événements, généralement depuis le WAL. · Ch.11

**Cohérence éventuelle** (*eventual consistency*) : garantie faible — si aucune nouvelle écriture n'est faite, toutes les répliques convergeront *éventuellement* vers la même valeur. · Ch.5

**Compaction** : processus de fusion et suppression des versions obsolètes dans un LSM-tree. · Ch.3

## D

**Durabilité** (*durability*) : propriété ACID — les données commitées survivent aux pannes (écrites sur disque). · Ch.7

## F

**Fault (panne)** : un composant qui s'écarte de sa spécification (≠ failure). · Ch.1

**Failure (défaillance)** : le système entier cesse de rendre le service attendu à l'utilisateur (≠ fault). · Ch.1

**Fan-out** : nombre de destinataires d'une action. Ex. : un tweet distribué à 30M d'abonnés a un fan-out de 30M. · Ch.1

**Filtre de Bloom** (*Bloom filter*) : structure probabiliste qui permet de tester rapidement si une clé *pourrait* exister dans un SSTable (faux positifs possibles, faux négatifs impossibles). · Ch.3

## H

**Hachage cohérent** (*consistent hashing*) : algorithme de partitionnement sur un anneau qui minimise le rééquilibrage lors de l'ajout/retrait de nœuds. · Ch.6

**Horloge de Lamport** (*Lamport clock*) : compteur logique monotone qui préserve l'ordre causal des événements dans un système distribué. · Ch.8

**Horloge vectorielle** (*vector clock*) : vecteur de compteurs Lamport (un par nœud) qui permet de détecter les relations de concurrence entre événements. · Ch.8

## I

**Isolation** (*isolation*) : propriété ACID — les transactions concurrentes ne s'interferent pas. Plusieurs niveaux (read committed, snapshot, sérialisable). · Ch.7

## L

**Lag de réplication** (*replication lag*) : retard entre le moment où une écriture arrive sur le leader et le moment où elle est visible sur les répliques. · Ch.5

**Linéarisabilité** (*linearizability*) : garantie forte — le système se comporte comme s'il y avait un seul exemplaire des données, modifié atomiquement. · Ch.9

**LSM-tree** (*Log-Structured Merge-Tree*) : structure de stockage optimisée pour les écritures séquentielles — les données arrivent dans un memtable en mémoire, sont flushées en SSTables immutables, puis compactées. · Ch.3

## M

**MVCC** (*Multi-Version Concurrency Control*) : technique d'implémentation de l'isolation par snapshot — plusieurs versions d'un objet coexistent, chaque transaction voit un snapshot cohérent. · Ch.7

## P

**Paramètre de charge** (*load parameter*) : métrique qui décrit la charge du système (ex. req/s, ratio lecture/écriture, fan-out). · Ch.1

**Partitionnement** (*sharding*) : division des données en partitions réparties sur plusieurs nœuds. · Ch.6

**Percentile** : valeur en-dessous de laquelle se situe X% des mesures. p99 = 99e percentile. · Ch.1

**Phantom read** : anomalie de concurrence — une transaction lit un ensemble de lignes correspondant à une condition, une autre transaction insère/supprime des lignes, la première transaction re-lit et trouve un ensemble différent. · Ch.7

## Q

**Quorum** : nombre minimal de nœuds devant répondre pour qu'une opération soit considérée réussie. Condition : W + R > N pour cohérence forte (N = total, W = nœuds écriture, R = nœuds lecture). · Ch.5

## R

**Réplication** (*replication*) : maintenir des copies des mêmes données sur plusieurs nœuds pour la tolérance aux pannes et les performances de lecture. · Ch.5

## S

**Scalabilité** (*scalability*) : capacité du système à continuer à fonctionner correctement lorsque la charge augmente. · Ch.1

**SLA** (*Service Level Agreement*) : contrat avec le client définissant les pénalités si les SLO ne sont pas respectés. · Ch.1

**SLO** (*Service Level Objective*) : objectif interne de performance (ex. p99 < 200 ms, 99,9% disponibilité). · Ch.1

**Snapshot isolation** : niveau d'isolation — chaque transaction voit un snapshot cohérent des données au moment de son début. · Ch.7

**SSTable** (*Sorted String Table*) : fichier de données immuable où les clés sont triées, utilisé dans les LSM-trees. · Ch.3

## T

**Tolérance aux pannes** (*fault tolerance*) : capacité à continuer à fonctionner même quand des composants tombent en panne. · Ch.1

**Total order broadcast** : primitive de consensus — tous les nœuds reçoivent les messages dans le même ordre. · Ch.9

## W

**WAL** (*Write-Ahead Log*) : journal d'opérations écrit avant toute modification de données, permettant la récupération après crash. · Ch.3, Ch.5

**Write skew** : anomalie de concurrence — deux transactions lisent les mêmes données, prennent des décisions indépendantes, et leurs écritures viole une invariante qui aurait tenu si elles avaient été sérialisées. · Ch.7
