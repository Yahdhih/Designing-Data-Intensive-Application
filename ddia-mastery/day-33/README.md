# Jour 33 — 🔁 Revue Ch.7 (Transactions)

🔁 Rappel actif complet · ~60 min

---

## 🎯 Objectif du jour

Ch.7 est le chapitre le plus dense de la Partie II. Le but est de tout retrouver de mémoire et de construire la hiérarchie complète des anomalies et solutions.

---

## ✏️ Exercices (60 min)

### Ex 1 — Hiérarchie complète des anomalies (20 min)

Ferme tout. Dans `notes.md`, remplis ce tableau **de mémoire** :

| Anomalie | Ce qui se passe | Niveau minimal qui protège | Solution SQL |
|----------|----------------|--------------------------|-------------|
| Dirty read | | | |
| Dirty write | | | |
| Non-repeatable read | | | |
| Lost update | | | |
| Write skew | | | |
| Phantom read | | | |

### Ex 2 — MVCC en 5 points (10 min)

Sans aide, explique MVCC en 5 points :
1. Pourquoi garder plusieurs versions ?
2. Comment une transaction choisit quelle version lire ?
3. Qu'est-ce que `VACUUM` dans Postgres ?
4. Comment MVCC permet-il la lecture sans bloquer les écritures ?
5. Quelle est la limite de MVCC pour les write skew ?

### Ex 3 — 2PL vs SSI en 3 phrases chacun (10 min)

**2PL en 3 phrases :**

**SSI en 3 phrases :**

**Quand choisir l'un plutôt que l'autre :**

### Ex 4 — 5 questions flash (10 min)

Réponds sans aide :

1. ACID : quelle lettre ne dépend **pas** de la base de données ?
2. Quelle est la différence entre dirty read et non-repeatable read ?
3. Pourquoi `SELECT FOR UPDATE` ne protège pas contre les phantoms ?
4. Dans SSI, que se passe-t-il quand un conflit est détecté ?
5. Postgres utilise quel niveau d'isolation par défaut ?

### Ex 5 — Vérification et lacunes (10 min)

Ouvre le livre (Summary de Ch.7) et compare.  
Note dans `notes.md` les 2-3 points que tu avais mal mémorisés.

---

## ✅ Terminé quand

- [ ] Tableau des 6 anomalies complété de mémoire
- [ ] MVCC en 5 points fait
- [ ] 2PL vs SSI en 3 phrases chacun
- [ ] 5 questions flash répondues
- [ ] Vérification + lacunes notées
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.8 — Les problèmes des systèmes distribués : réseaux non fiables, horloges non synchronisées, processus qui peuvent geler.
