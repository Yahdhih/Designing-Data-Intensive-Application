# Jour 10 — Ch.3 : LSM-Trees + B-Trees

📖 Lecture · ~45 min de lecture + 15 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 3, sections « LSM-Trees » et « B-Trees »

Aujourd'hui tu lis les **deux grandes familles** d'index qui existent dans les bases de données modernes. LSM-Tree est utilisé par RocksDB, Cassandra, LevelDB. B-Tree est utilisé par Postgres, MySQL, SQLite.

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, réponds AVANT d'ouvrir le livre :

1. Tu sais que Cassandra utilise LSM-Tree. Selon toi, qu'est-ce que ça signifie pour ses performances d'écriture vs de lecture ?
2. Un arbre B (B-Tree) — qu'est-ce que c'est selon ta mémoire ? Pourquoi est-ce utile pour une base de données ?
3. Quelle structure serait plus rapide pour écrire beaucoup de données rapidement — un arbre en mémoire ou une structure append-only sur disque ?

---

## 📚 Points à remarquer pendant la lecture

- **LSM-Tree** : de SSTables vers un arbre de fusion. L'écriture passe par un **memtable** en mémoire, puis des SSTables sur disque en niveaux
- La **compaction** des SSTables — comment les niveaux se fusionnent progressivement (tiered vs leveled compaction)
- **B-Tree** : les pages sur disque, la mise à jour **in-place**, le Write-Ahead Log (WAL)
- La structure d'un noeud B-Tree : combien de clés, combien de pointeurs, pourquoi cette forme

---

## ✏️ Exercices (15 min)

### Ex 1 — Schéma LSM-Tree (7 min)
Dans `notes.md`, décris (texte ou ASCII) la structure d'un LSM-Tree :
- Où va une écriture en premier ?
- Qu'est-ce qui se passe quand le memtable est plein ?
- Comment les niveaux de SSTables se fusionnent ?

### Ex 2 — Schéma B-Tree (5 min)
Décris le processus d'une **écriture** dans un B-Tree :
- Qu'est-ce qui se passe sur disque ?
- Qu'est-ce que le WAL (Write-Ahead Log) et à quoi sert-il ?

### Ex 3 — Première intuition sur le compromis (3 min)
Avant de lire la section de comparaison (demain), quelle est ton intuition sur le compromis LSM vs B-Tree ?  
Quel est plus rapide à l'écriture ? À la lecture ? Pourquoi ?

---

## ✅ Terminé quand

- [ ] Lecture (LSM-Trees + B-Trees) terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (schéma LSM-Tree) fait
- [ ] Ex 2 (schéma B-Tree + WAL) fait
- [ ] Ex 3 (intuition compromis) noté
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.3 — Comparaison B-Tree vs LSM-Trees (le vrai débat) + autres structures d'index (index multi-colonnes, full-text, in-memory).
