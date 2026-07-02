# Jour 17 — Ch.5 : Leaders and Followers (réplication single-leader)

📖 Lecture · ~45 min de lecture + 15 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 5, du début jusqu'à la fin de la section « Setting Up New Followers » (avant Replication Lag)

Ch.5 commence la Partie II du livre — la partie la plus importante. La **réplication** consiste à maintenir une copie des données sur plusieurs machines. C'est fondamental pour la tolérance aux pannes et la scalabilité des lectures.

---

## 🎯 Avant de lire — Prédis (5 min)

Reprends tes prédictions du Jour 16 (Ex 4). Note lesquelles seront confirmées.

---

## 📚 Points à remarquer pendant la lecture

- Les **3 raisons** de répliquer les données (tolérance aux pannes, latence géographique, scalabilité des lectures)
- Le modèle **single-leader** : 1 leader (writes) + N followers (reads)
- **Replication log** : comment le leader transmet ses changements aux followers (statement-based, WAL shipping, logical row-based)
- La différence entre **réplication synchrone** et **asynchrone** — compromis durabilité vs disponibilité
- Comment **ajouter un nouveau follower** sans bloquer le leader (snapshot + log replay)

---

## ✏️ Exercices (15 min)

### Ex 1 — Schéma single-leader (7 min)
Dans `notes.md`, dessine (ASCII ou description) l'architecture single-leader :
- Le leader reçoit une écriture
- Comment le changement arrive-t-il aux followers ?
- Quelle est la différence si la réplication est synchrone vs asynchrone ?

### Ex 2 — Les 3 méthodes de replication log (5 min)
Kleppmann décrit 3 façons pour le leader de transmettre ses changements :
- Statement-based
- WAL shipping  
- Logical (row-based) log

Pour chacune, note : quel est son problème ou sa limite principale ?

### Ex 3 — Vérification des prédictions (3 min)
Compare avec tes prédictions du Jour 16.  
Qu'est-ce qui était juste ? Qu'est-ce que tu n'avais pas anticipé ?

---

## ✅ Terminé quand

- [ ] Lecture (début Ch.5 → Setting Up New Followers) terminée
- [ ] Ex 1 (schéma single-leader) fait
- [ ] Ex 2 (3 méthodes replication log) fait
- [ ] Ex 3 (vérification prédictions) fait
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.5 — Problèmes de décalage de réplication : read-your-writes, monotonic reads, consistent prefix reads.
