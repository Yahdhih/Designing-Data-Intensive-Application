# code/03-replication/ — Réplication

> Chapitre 5 · Jours 31, 34 · `PLAN.md` Phase 2

---

## Objectif

Simuler les anomalies de la réplication asynchrone et illustrer les quorums.

---

## `single_leader.py` (Jour 31)

Simulateur de réplication mono-leader avec retard artificiel.

**Ce qu'on construit :**
- 1 leader + 2 répliques avec retard configurable
- Démonstration des anomalies :
  - **Read-your-writes violation** : l'utilisateur écrit sur le leader, lit sur une réplique en retard
  - **Monotonic reads violation** : deux lectures successives d'un utilisateur atteignent des répliques différentes → il « revient en arrière »

**Lancer :**
```bash
python code/03-replication/single_leader.py
```

**Attendu :**
```
Écriture "user:1 = Alice" sur leader (t=0)
Lecture sur réplique 2 (lag=500ms) → None (violation read-your-writes)
Lecture sur réplique 1 (lag=100ms) → "Alice"
Lecture sur réplique 2 → None encore (violation monotonic reads)
```

---

## `quorum_sim.py` (Jour 34)

Simulateur de quorum Dynamo-style.

**Ce qu'on construit :**
- N nœuds, chacun stockant une valeur + numéro de version
- Écriture : envoyer à W nœuds, succès si W répondent
- Lecture : interroger R nœuds, retourner la valeur avec la version la plus haute

**Jalons :**
```
Jalon 1 : N=3, W=2, R=2 → W+R>N → cohérence forte → aucune lecture périmée
Jalon 2 : N=3, W=1, R=1 → W+R<N → montrer une lecture périmée
Jalon 3 : nœud en panne → sloppy quorum (écriture sur un nœud de remplacement)
```

**Lancer :**
```bash
pytest code/03-replication/test_quorum.py -v
```

**Attendu :**
- Avec W=R=2, N=3 : après une écriture, toute lecture retourne la valeur récente
- Avec W=R=1 : montrer un cas où une lecture retourne une valeur obsolète

**Compromis à observer :**
- W+R > N → cohérence mais latence + élevée (plus de nœuds à attendre)
- W+R ≤ N → latence faible mais lectures potentiellement périmées

---

## Lien avec Dynamo (Article · Jour 36)

Après le jouet, lis le papier Dynamo. Cherche :
- Comment Amazon a choisi ses valeurs de W, R, N par défaut
- Le rôle des *vector clocks* pour la résolution de conflits
- Pourquoi *sloppy quorum* + *hinted handoff* améliorent la disponibilité
