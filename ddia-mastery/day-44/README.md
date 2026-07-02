# Jour 44 — Ch.10 : Joins et groupements dans MapReduce

📖 Lecture · ~45 min de lecture + 15 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 10, section « MapReduce Workflows » (joins, grouping, sort-merge join, broadcast hash join)

La section la plus technique de Ch.10. Faire une **jointure** dans MapReduce est très différent d'un JOIN SQL — les données sont sur des centaines de noeuds, et il n'y a pas de serveur central pour orchestrer la jointure.

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, réponds AVANT d'ouvrir le livre :

1. Si tu as une table `users` (100 Mo) et une table `events` (100 Go) sur HDFS, et tu veux joindre par `user_id` — quelle serait la stratégie naïve ? Pourquoi serait-elle lente ?
2. Dans Spark, as-tu déjà rencontré un **skew join** (jointure déséquilibrée) ? Qu'est-ce qui se passe sur les executors ?
3. Qu'est-ce qu'un « broadcast join » dans Spark ? Dans quelle situation l'utilise-t-on ?

---

## 📚 Points à remarquer pendant la lecture

- **Sort-merge join** : les deux datasets sont triés par la clé de jointure, puis fusionnés. Efficace mais nécessite un tri distribué (le shuffle)
- **Broadcast hash join** : si un dataset est petit, on l'envoie à tous les noeuds (broadcast). L'autre dataset n'a pas besoin d'être trié
- **Partitioned hash join** : si les deux datasets sont partitionnés de la même façon, chaque noeud peut faire son join localement
- **Grouping** : similaire à un GROUP BY SQL — implique aussi un shuffle par clé de groupe
- Le problème des **hot keys** (clés chaudes) dans les joins : si 99% des enregistrements ont la même clé, un seul reducer reçoit tout → goulot d'étranglement
- **Output** du batch processing : les sorties sont des fichiers, pas des lignes modifiées en BDD

---

## ✏️ Exercices (15 min)

### Ex 1 — 3 types de joins (8 min)

Remplis ce tableau dans `notes.md` (de mémoire après lecture) :

| Type de join | Quand l'utiliser | Ce qui se passe sur le réseau | Équivalent Spark |
|-------------|-----------------|------------------------------|-----------------|
| Sort-merge join | | | SortMergeJoin |
| Broadcast hash join | | | BroadcastHashJoin |
| Partitioned hash join | | | BucketedHashJoin |

### Ex 2 — Spark et les joins (5 min)
Tu fais `df_users.join(df_events, "user_id")` dans Spark.  
Spark choisit automatiquement le type de join. Décris les critères que Spark utilise :
- Si `df_users` est < 10 Mo → quelle stratégie ?
- Si les deux sont > 10 Mo et **non** partitionnés de la même façon → ?
- Si les deux sont **déjà** partitionnés par `user_id` (bucketed) → ?

### Ex 3 — Hot key problem (2 min)
Dans un log de clicks, l'`event_type = "page_view"` représente 95% des événements.  
Si tu fais un `GROUP BY event_type`, que se passe-t-il sur le reducer de « page_view » ?  
Comment Spark gère-t-il ce problème avec le Adaptive Query Execution (AQE) ?

---

## ✅ Terminé quand

- [ ] Lecture (joins + groupements MapReduce) terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (tableau 3 types de join) fait
- [ ] Ex 2 (Spark + choix de join) fait
- [ ] Ex 3 (hot key problem) fait
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.10 — Au-delà de MapReduce : Spark, Flink, Tez — les moteurs de dataflow qui ont remplacé MapReduce. Résumé Ch.10.
