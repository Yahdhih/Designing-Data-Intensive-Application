# Jour 11 — Ch.3 : Comparaison B-Tree vs LSM + Autres index

📖 Lecture · ~40 min de lecture + 20 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 3, sections « Comparing B-Trees and LSM-Trees » + « Other Indexing Structures »

C'est la section clé de Ch.3 — le **vrai débat** entre les deux familles d'index. Kleppmann ne donne pas de réponse universelle : le choix dépend du workload.

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, reprends ta réponse de l'Ex 3 d'hier (ton intuition) :
- Qu'est-ce qui était juste dans ton intuition ?
- Qu'est-ce qui manquait ?

---

## 📚 Points à remarquer pendant la lecture

- **Write amplification** : une écriture logique → N écritures physiques. Comparer LSM vs B-Tree sur ce point
- **Read amplification** : une lecture logique → N lectures physiques. Qui gagne ?
- **Space amplification** : qui utilise plus d'espace disque ?
- Les situations où LSM est meilleur (beaucoup d'écritures, SSD) et où B-Tree est meilleur (beaucoup de lectures, transactions)
- **Index multi-colonnes** (concatenated index) — exemple name + phone
- **Full-text search** et sa différence avec les index classiques
- Les **in-memory databases** — pourquoi stocker en RAM si on peut tout reconstruire ?

---

## ✏️ Exercices (20 min)

### Ex 1 — Matrice de comparaison (10 min)

Remplis ce tableau dans `notes.md` (de mémoire après lecture) :

| Critère | LSM-Tree | B-Tree |
|---------|----------|--------|
| Vitesse d'écriture | | |
| Vitesse de lecture | | |
| Write amplification | | |
| Read amplification | | |
| Fragmentation disque | | |
| Prévisibilité latence | | |
| Utilisé par | Cassandra, RocksDB... | Postgres, MySQL... |

### Ex 2 — Quand choisir quoi ? (7 min)
Décris 2 scénarios concrets où tu choisirais LSM et 2 où tu choisirais B-Tree.  
Appuie-toi sur ton expérience avec Cassandra vs Postgres.

### Ex 3 — Surprise ? (3 min)
Qu'est-ce qui t'a le plus surpris dans cette comparaison ?  
Ton intuition d'hier était-elle correcte ?

---

## ✅ Terminé quand

- [ ] Lecture (comparaison + autres index) terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (matrice comparaison) complète
- [ ] Ex 2 (2 scénarios LSM + 2 scénarios B-Tree) fait
- [ ] Ex 3 (surprise) noté
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.3 — OLTP vs OLAP + Data Warehouses + stockage orienté colonnes. Le passage des bases transactionnelles aux bases analytiques.
