# Jour 22 — Ch.6 : Partitionnement par clé (range + hash)

📖 Lecture · ~45 min de lecture + 15 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 6, du début jusqu'à la fin de la section sur le partitionnement par hash (avant les index secondaires)

Ch.6 traite de la **partition** des données sur plusieurs noeuds. Là où Ch.5 copiait les mêmes données sur plusieurs machines, Ch.6 **divise** les données pour qu'aucun noeud ne porte tout. C'est la base de toute base de données distribuée à grande échelle.

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, réponds AVANT d'ouvrir le livre :

1. Kafka divise ses topics en **partitions**. Comment Kafka décide-t-il dans quelle partition va un message ?
2. Qu'est-ce qu'un **hot spot** (point chaud) dans une base de données distribuée ? Donne un exemple intuitif.
3. Si tu partitionnes des données par ordre alphabétique (A-F, G-M, N-Z), quel problème peux-tu avoir sur un système comme Twitter si tout le monde s'appelle « Smith » ?

---

## 📚 Points à remarquer pendant la lecture

- La définition de **partition** (shard chez MongoDB, region chez HBase, tablet chez Bigtable, vnode chez Cassandra)
- **Partitionnement par plage de clés (range)** : les clés sont triées, on assigne des plages à des noeuds. Avantage : lectures de plage efficaces. Problème : hot spots sur les plages populaires
- L'exemple des **timestamps comme clé** — pourquoi c'est une mauvaise idée en range partitioning
- **Partitionnement par hash** : on distribue uniformément mais on perd les lectures de plage
- **Consistent hashing** : comment les noeuds sont répartis sur un anneau virtuel
- Le problème des **celebrity writes** (Justin Bieber) — hash ne résout pas tout

---

## ✏️ Exercices (15 min)

### Ex 1 — Schéma des deux approches (8 min)
Dans `notes.md`, décris (ASCII ou texte) les deux approches :

**Range partitioning :**
```
Clés A-F → Noeud 1
Clés G-M → Noeud 2
Clés N-Z → Noeud 3
```
Avantage :
Problème :

**Hash partitioning :**
```
hash(key) % 3 → Noeud 0, 1, ou 2
```
Avantage :
Problème :

### Ex 2 — Kafka et le partitionnement (5 min)
Tu utilises Kafka. Kafka utilise du **hash partitioning** par défaut (hash de la clé du message).  
Maintenant que tu comprends Ch.6 :
- Pourquoi les messages sans clé sont répartis en round-robin ?
- Pourquoi tous les messages avec la même clé vont dans la même partition ?
- Quel est le risque si une clé est très populaire (ex : tous les logs d'un même service) ?

### Ex 3 — Hot spot des timestamps (2 min)
Kleppmann donne l'exemple des capteurs de température qui utilisent le timestamp comme clé.  
Pourquoi est-ce que ça crée un hot spot ? Comment le résoudre ?

---

## ✅ Terminé quand

- [ ] Lecture (range + hash partitioning) terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (schéma 2 approches) fait
- [ ] Ex 2 (Kafka + partitionnement) fait
- [ ] Ex 3 (hot spot timestamps) fait
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.6 — Index secondaires partitionnés : deux stratégies radicalement différentes (scatter-gather vs global index).
