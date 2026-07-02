# Jour 45 — Ch.10 : Au-delà de MapReduce (Spark, Flink, Tez) + Résumé

📖 Lecture · ~40 min de lecture + 20 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 10, section « Beyond MapReduce » + « Summary »

MapReduce a révolutionné le traitement de données massives, mais il a des limites majeures (tout passe par le disque, pas de pipeline en mémoire). Spark, Flink et Tez ont résolu ces problèmes. Kleppmann explique pourquoi et comment.

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, réponds AVANT d'ouvrir le livre :

1. MapReduce écrit les résultats intermédiaires sur disque (HDFS) entre chaque étape Map et Reduce. Pourquoi est-ce lent ? Spark fait quoi à la place ?
2. Qu'est-ce qu'un DAG (Directed Acyclic Graph) dans le contexte de Spark ?
3. Pourquoi Spark est-il « 10x à 100x plus rapide » que MapReduce selon la publicité ?

---

## 📚 Points à remarquer pendant la lecture

- Le problème de MapReduce : **matérialisation intermédiaire** — chaque étape écrit sur HDFS et attend que l'étape précédente soit terminée
- **Dataflow engines (Spark, Flink, Tez)** : les opérations forment un graphe (DAG) — les résultats intermédiaires restent en mémoire (RDD/Dataset) et ne sont écrits que si nécessaire
- **Pipelining** : les données passent directement d'une opération à la suivante sans matérialisation
- La **fault tolerance différente** : MapReduce relit depuis HDFS en cas de panne. Spark relit depuis le checkpoint le plus proche ou depuis le début (lineage)
- Les **sorties immutables** : dans tous ces systèmes, les sorties ne modifient jamais les entrées — ce qui permet le **retry** automatique
- **Pregel** (modèle pour les graphes) : GraphX dans Spark

---

## ✏️ Exercices (20 min)

### Ex 1 — MapReduce vs Spark : tableau (8 min)

| | MapReduce | Spark |
|-|-----------|-------|
| Résultats intermédiaires | Écrits sur HDFS | |
| Fault tolerance | Relit HDFS | |
| Pipelining | Non | |
| Langage de programmation | Java (bas niveau) | |
| Cas d'usage idéal | | |

### Ex 2 — Le DAG Spark en pratique (7 min)

Pour ce code Spark :
```python
df = spark.read.parquet("s3://events/")
result = (df
    .filter(df.event_type == "purchase")
    .groupBy("user_id")
    .agg(sum("amount").alias("total"))
    .filter(col("total") > 1000)
    .join(df_users, "user_id")
)
result.write.parquet("s3://output/")
```

Dans `notes.md`, dessine le DAG des opérations (en texte) :
- Quelles opérations nécessitent un shuffle réseau ?
- Où Spark peut-il pipeliner sans shuffle ?

### Ex 3 — Résumé Ch.10 en 5 phrases (5 min)
Page blanche. Écris 5 phrases qui résument Ch.10.  
Commence par : « Ch.10 explique pourquoi le batch processing... »

---

## ✅ Terminé quand

- [ ] Lecture (Beyond MapReduce + Summary) terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (tableau MapReduce vs Spark) fait
- [ ] Ex 2 (DAG Spark) dessiné
- [ ] Ex 3 (résumé Ch.10 en 5 phrases) fait
- [ ] Coché dans PROGRESS.md

## → Demain
🔁 Revue Ch.10 — rappel actif, puis prédictions Ch.11 (Stream Processing).
