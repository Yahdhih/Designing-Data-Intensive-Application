# Jour 43 — Ch.10 : MapReduce et la philosophie Unix

📖 Lecture · ~45 min de lecture + 15 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 10, du début jusqu'à la fin de la section « MapReduce and Distributed Filesystems »

Ch.10 ouvre la Partie III — les **données dérivées** (données calculées à partir d'autres données). Le batch processing est le paradigme fondateur : prendre un grand volume de données en entrée, appliquer un traitement, produire une sortie. Kleppmann commence par la philosophie Unix, puis explique MapReduce.

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, réponds AVANT d'ouvrir le livre :

1. Tu utilises Spark. Spark est souvent décrit comme « MapReduce amélioré ». Qu'est-ce que MapReduce fait à ton avis que Spark reprend ?
2. Kleppmann cite la philosophie Unix (pipes, stdin/stdout, outils simples composables). En quoi cette philosophie s'applique-t-elle aux pipelines de données ?
3. Quelle est la différence entre un traitement **batch** (par lots) et un traitement **stream** (en flux) ?

---

## 📚 Points à remarquer pendant la lecture

- La **philosophie Unix** : chaque outil fait une chose, les outils se composent via des pipes — c'est le modèle mental de tout pipeline de données
- Les **inputs immuables** : dans le batch processing, on ne modifie jamais l'entrée — on crée toujours de nouvelles sorties. C'est fondamentalement différent des bases de données qui modifient les données en place
- **MapReduce** : le job se découpe en Map (appliquer une fonction à chaque enregistrement → émettre des paires clé-valeur) puis Reduce (regrouper par clé et agréger)
- **HDFS (Hadoop Distributed File System)** : stockage distribué sur lequel tourne MapReduce — les données sont dupliquées sur 3 noeuds
- Le principe **« move computation to data »** : plutôt que de lire les données sur le réseau, exécuter le code là où les données sont stockées

---

## ✏️ Exercices (15 min)

### Ex 1 — MapReduce : le comptage de mots (7 min)

L'exemple classique de MapReduce est le comptage de mots dans un corpus de textes.  
Dans `notes.md`, décris les 2 phases :

**Map** : pour chaque ligne de texte →
```
"hello world hello" → [("hello", 1), ("world", 1), ("hello", 1)]
```

**Shuffle** : regroupement par clé →
```
("hello", [1, 1]), ("world", [1])
```

**Reduce** : agrégation →
```
("hello", 2), ("world", 1)
```

Questions :
- Combien de mappers peut-on lancer en parallèle si on a 1000 fichiers ?
- Quel est le goulot d'étranglement entre Map et Reduce ?

### Ex 2 — Philosophie Unix vs MapReduce (5 min)

La commande Unix suivante compte les mots d'un fichier :
```bash
cat text.txt | tr ' ' '\n' | sort | uniq -c | sort -rn
```

En quoi cette commande est-elle conceptuellement similaire à un job MapReduce ?  
Quelle est la grande différence entre les deux ?

### Ex 3 — Move computation to data (3 min)
Dans Spark (ou HDFS/MapReduce), les données sont stockées sur 100 noeuds.  
Pourquoi est-il plus efficace d'envoyer le code sur les noeuds que d'amener les données vers un seul noeud de calcul ?  
Dans quel cas ce principe devient-il moins important ? (Hint : stockage objet comme S3)

---

## ✅ Terminé quand

- [ ] Lecture (intro Ch.10 + MapReduce + HDFS) terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (MapReduce word count) fait
- [ ] Ex 2 (Unix pipe vs MapReduce) fait
- [ ] Ex 3 (move computation to data) fait
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.10 — Joins et groupements dans MapReduce : comment faire des jointures sur des données distribuées ?
