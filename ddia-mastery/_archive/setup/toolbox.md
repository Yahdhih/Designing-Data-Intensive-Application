# toolbox.md — Boîte à outils méthodologique

> Document de référence. Relis-le quand tu sens que ta méthode dérive. Les 10 principes sont délibérément répétés dans chaque fichier-jour.

---

## Les 10 principes pédagogiques

### 1. Rappel actif (retrieval) — toujours en premier

Avant toute lecture ou révision, passe **5 minutes à récupérer** ce que tu sais déjà sur le sujet — page blanche, voix haute, mini-schéma.

**Pourquoi :** la récupération active est 2 à 3× plus efficace que la relecture pour ancrer l'information à long terme (*testing effect*). Si rien ne vient, c'est un signal — pas un échec. Note ce qui manque et lis pour combler le trou.

### 2. Répétition espacée

Les cartes Anki reviennent automatiquement à **J+1, J+3, J+7, J+16, J+35** après création. Ne saute **jamais** la session Anki du jour (même 5 minutes).

**Règle pratique :** crée 2-3 cartes minimum par jour d'étude. Toujours avec un exemple concret au verso.

### 3. Feynman / enseigner

Après avoir étudié un concept, essaie de l'expliquer à voix haute **comme à un ami qui ne l'a jamais vu**. Note chaque trou dans ton explication — c'est ton programme de révision.

**La règle de Feynman :** si tu ne peux pas l'expliquer simplement, tu ne l'as pas compris.

### 4. Entrelacement lecture ↔ pratique

Ne jamais enchaîner plus de **2-3 jours de lecture pure**. Alterner systématiquement :
- Lecture de chapitre → Jouet Python → Labo Docker → Article fondateur → Revue

**Pourquoi :** l'alternance (*interleaving*) force le cerveau à récupérer le contexte à chaque changement, renforçant les connexions entre concepts.

### 5. Predict-then-verify

**Avant** de lire une section, écris **2 lignes** sur ce que tu anticipes. **Après** avoir lu, relis tes prédictions et note explicitement les erreurs.

Les erreurs de prédiction créent des traces mémorielles plus fortes que les confirmations.

### 6. Trois voies de pratique (les tourner toutes les trois)

**(a) Implémentation jouet** — Python par défaut, Go optionnel.  
*Règle d'or :* **si je ne peux pas le réimplémenter ou le redessiner de mémoire, je ne l'ai pas compris.**  
Les jouets sont délibérément simplifiés : pas de production-readiness, juste capturer le mécanisme essentiel.

**(b) Labo sur vrai système** — Docker (Postgres, Kafka, Cassandra, etcd…).  
Reproduire le concept, puis **casser les choses** (pannes, partitions réseau, inversion de latence) et observer. La meilleure compréhension vient des comportements inattendus.

**(c) Article fondateur** — Dynamo, Raft, MapReduce, The Log…  
Méthode de lecture : **abstract → intro → conclusion → figures → corps**. Répondre aux 3 questions :
1. Quel problème résout cet article ?
2. Quelle est l'idée clé (le « truc » )?
3. Quel est le compromis principal ?

### 7. Muscle « matrice de compromis »

Pour chaque technique : *quand l'utiliser · ce que ça coûte · ses modes de défaillance*.  
Tiens `reference/tradeoffs.md` à jour — c'est ton document de référence pour les exercices « Conçois X ».

**Template d'entrée :**
```
| Technique | Quand l'utiliser | Coûts & limites | Modes de défaillance | Exemple |
```

### 8. Muscle « conçois X »

Exercices réguliers : concevoir un système (raccourcisseur d'URL, fil d'actualité, système de paiement) **en utilisant le vocabulaire DDIA** et en remplissant une matrice de compromis.

**Gabarit de réponse :**
1. Quels sont les paramètres de charge ? (load parameters)
2. Quelle architecture de stockage ? (OLTP vs OLAP · SQL vs NoSQL · réplication)
3. Quels compromis CAP / fiabilité / cohérence ?
4. Quels modes de défaillance ? Comment les tolérer ?

### 9. Double codage

**Dessine systématiquement.** Un schéma dessiné à la main active des zones cérébrales différentes du texte :
- LSM-tree : chemin d'une écriture (memtable → SSTable → compaction) puis d'une lecture
- B-tree : structure en pages, WAL, arbre de recherche
- Réplication : topologies mono/multi/sans-leader avec flux de données
- Anneau de hachage cohérent avec nœuds virtuels
- Niveaux d'isolation : tableau anomalies × niveaux
- Machine d'état Raft
- Fenêtres de flux : tumbling · sliding · session

Ces schémas vont dans `reference/diagrams/`.

### 10. Consolidation quotidienne + revue hebdomadaire

**Chaque jour (15 min finales) :**
- Résumé 3-5 puces dans tes mots → `reference/notes/jour-NNN.md`
- 2-3 cartes ajoutées à `flashcards/cards.tsv`
- 1 schéma → `reference/diagrams/`
- 1 question ouverte notée

**Chaque 7ᵉ jour :**
- Pas de matière neuve
- Page blanche de la semaine
- Redessiner les schémas clés de mémoire
- Réexpliquer 3 concepts à voix haute
- Balayer toutes les cartes Anki dues
- Compléter `reference/tradeoffs.md`

---

## Comment lire un article de recherche

**Stratégie en 3 passes (≤ 40 min) :**

**Passe 1 (5 min) — Vue aérienne :** abstract → intro → conclusion → titres de sections.  
Objectif : comprendre quel problème, quelle solution, quel résultat.

**Passe 2 (15 min) — Figures et tableaux :** lit chaque figure/tableau avec sa légende.  
Les figures concentrent souvent l'idée principale.

**Passe 3 (20 min) — Corps sélectif :** lis les sections pertinentes pour ta compréhension actuelle. Skip les preuves mathématiques à la première lecture.

**Après la lecture, réponds à ces 3 questions dans `papers/notes/<article>.md` :**
1. **Quel problème ?** (1-2 phrases)
2. **Quelle idée clé ?** (le « truc » — ce qui n'était pas évident avant)
3. **Quel compromis ?** (ce que cette approche gagne vs ce qu'elle sacrifie)

---

## Comment déboguer un vrai système

**Démarche pour les labos Docker :**

1. **Lire les logs** : `docker compose logs -f <service>` — cherche les erreurs, les warnings, les métriques.
2. **Observer l'état** : `psql \d+`, `kafka-topics.sh --describe`, `etcdctl get --prefix /`.
3. **Mesurer les performances** : `EXPLAIN (ANALYZE, BUFFERS)` pour Postgres · `lag` pour Kafka Consumer Groups.
4. **Injecter une panne** : `docker pause` · `tc netem` · couper un réseau bridge Docker.
5. **Observer la réaction** : logs d'élection, timeouts, backoffs, données périmées.
6. **Restaurer et valider** : `docker unpause` · vérifier la convergence.

---

## Anti-décrochage

Si tu sautes **2 jours ou plus** :
1. Ne reprends pas depuis le début — reprends au dernier **fichier de revue hebdo** complété.
2. Fais une session de 20 min de cartes Anki pour te remettre dans le bain.
3. Relance le prochain jour d'étude en mode « léger » (lecture + 1 carte) avant de retrouver le rythme complet.

**Rappel de la règle des 2 jours :** si tu sautes 1 jour — reprends simplement. La culpabilité est une perte de temps.
