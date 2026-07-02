# code/08-batch/ — Traitement par lots

> Chapitre 10 · Jours 87-90 · `PLAN.md` Phase 3  
> **Exploite ton expérience Spark** — ce chapitre est le cadre conceptuel de ce que tu connais déjà.

---

## `mapreduce.py` (Jour 87)

Mini-MapReduce en Python pur.

**Jalons :**
```
Jalon 1 : word count (le Hello World du batch)
           map(doc) → [(word, 1), ...]
           reduce(word, [1,1,1,...]) → (word, count)

Jalon 2 : jointure reduce-side (join by key)
           Deux datasets → même phase map, reduce joint par clé
           Analogue à : Spark RDD join

Jalon 3 : jointure par diffusion (broadcast/map-side join)
           Petit dataset entier en mémoire côté map
           Analogue à : Spark broadcast join
```

**Lancer :**
```bash
python code/08-batch/mapreduce.py
pytest code/08-batch/test_mapreduce.py -v
```

**Attendu :**
```
Word count sur ["the quick fox", "the lazy dog"] :
  the: 2, quick: 1, fox: 1, lazy: 1, dog: 1

Jointure reduce-side : users + orders → commandes enrichies par utilisateur

Jointure broadcast : small_table (100 lignes) diffusée dans tous les mappers
  → pas de shuffle réseau pour la table broadcast
```

**Connexion avec Spark (Jour 89) :**
| Concept MapReduce | Équivalent Spark |
|------------------|-----------------|
| Map | `rdd.map()` · `df.select()` |
| Shuffle | Shuffle automatique lors des joins/groupBy |
| Reduce | `rdd.reduceByKey()` · `df.groupBy().agg()` |
| Broadcast join | `spark.broadcast()` · join hint `BROADCAST` |
| DAG de jobs | Spark DAG (stages + tasks) |

---

## Labo Spark (Jour 89)

Reprend un de tes jobs Spark existants (ou en crée un simple). Regarde :
1. Le DAG dans Spark UI — combien de stages ? Pourquoi des stages ?
2. Où est le shuffle ? (exchange dans le plan physique)
3. Essaie de forcer/éviter un broadcast join et mesure la différence

```bash
# Lancer Spark en local (pas besoin du compose.full.yml)
pip install pyspark
python code/08-batch/spark_demo.py
```
