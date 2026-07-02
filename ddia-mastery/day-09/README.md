# Jour 09 — Ch.3 : Hash Indexes + SSTables

📖 Lecture · ~45 min de lecture + 15 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 3, du début jusqu'à la fin de la section sur les SSTables (avant LSM-Trees)

Ch.3 est l'un des chapitres les plus importants du livre. Kleppmann commence par expliquer les structures de données **sous-jacentes** aux bases de données — comment les données sont réellement stockées sur disque.

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, réponds AVANT d'ouvrir le livre :

1. Imagine que tu dois créer la base de données la plus simple possible en Python. Quelles structures de données utiliserais-tu ?
2. Qu'est-ce qu'un « index » dans une base de données ? À quoi ça sert concrètement ?
3. Quelle est la différence entre écrire sur disque en **append-only** (ajouter à la fin) vs **in-place** (écraser l'ancienne valeur) ?

---

## 📚 Points à remarquer pendant la lecture

- La base de données « à 2 lignes bash » que Kleppmann présente — comprenez bien pourquoi c'est lent
- **Hash index** : stocker un dictionnaire clé → position sur disque. Quelle est la limite principale ?
- **Segments + compaction** : pourquoi log-structured (append-only) est plus rapide à l'écriture
- **SSTables** (Sorted String Tables) : les segments sont triés par clé — qu'est-ce que ça apporte ?
- Crash recovery : comment la base se remet d'une panne dans ces architectures ?

---

## ✏️ Exercices (15 min)

### Ex 1 — Schéma du Hash Index (7 min)
Dans `notes.md`, dessine (en texte ASCII ou en description) comment un hash index fonctionne :
- Les données sur disque (segments append-only)
- Le dictionnaire en mémoire (clé → byte offset)
- Ce qui se passe lors d'un `get(key)` et d'un `set(key, value)`

### Ex 2 — Limite du Hash Index (5 min)
Le hash index a une limite fondamentale qui le rend inutilisable dans certains cas.  
Quelle est cette limite ? Et quel type de requêtes ne peut-on pas faire avec un hash index ?

### Ex 3 — SSTables : avantage sur hash index (3 min)
Les SSTables résolvent une partie des problèmes du hash index.  
Quel avantage principal les SSTables apportent-elles par rapport au hash index basique ?

---

## ✅ Terminé quand

- [ ] Lecture (hash indexes + SSTables) terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (schéma hash index) fait
- [ ] Ex 2 (limite du hash index) identifiée
- [ ] Ex 3 (avantage SSTables) expliqué
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.3 — LSM-Trees (de SSTables aux arbres de fusion) et B-Trees (l'index le plus répandu en bases de données).
