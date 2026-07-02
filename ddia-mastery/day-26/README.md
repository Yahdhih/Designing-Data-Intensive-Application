# Jour 26 — Ch.7 : ACID + le concept de transaction

📖 Lecture · ~45 min de lecture + 15 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 7, du début jusqu'à la fin de la section « Single-Object and Multi-Object Operations »

Ch.7 est l'un des chapitres les plus profonds du livre. Il démonte des intuitions souvent fausses sur les transactions et l'ACID. Lis lentement — chaque mot compte.

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, réponds AVANT d'ouvrir le livre :

1. ACID : qu'est-ce que chaque lettre signifie selon ta mémoire actuelle ?
2. Pourquoi une base de données aurait-elle besoin de transactions ? Donne un exemple où sans transaction, quelque chose tourne mal.
3. Est-ce qu'une transaction concerne toujours **plusieurs** lignes/tables, ou peut-elle concerner **1 seul** objet ?

---

## 📚 Points à remarquer pendant la lecture

- **Atomicity (A)** : tout ou rien — si une partie échoue, tout est annulé. ≠ atomique au sens CPU
- **Consistency (C)** : la propriété la plus floue — c'est une propriété de l'**application**, pas de la BDD
- **Isolation (I)** : les transactions concurrentes ne se voient pas mutuellement pendant leur exécution
- **Durability (D)** : une fois confirmée (committed), la transaction est permanente même après crash
- La distinction **single-object** vs **multi-object** transactions — pourquoi les multi-object sont plus difficiles ?
- Le besoin de transactions multi-objets : exemple du virement bancaire, du compteur de messages non lus

---

## ✏️ Exercices (15 min)

### Ex 1 — ACID : 4 définitions précises (7 min)

Sans regarder tes notes, remplis ce tableau dans `notes.md` :

| Propriété | Définition précise (1-2 phrases) | Ce que ça garantit |
|-----------|--------------------------------|--------------------|
| Atomicity | | |
| Consistency | | |
| Isolation | | |
| Durability | | |

### Ex 2 — Pourquoi C est la propriété bizarre (5 min)
Kleppmann dit que le C dans ACID est différent des 3 autres.  
Explique pourquoi la consistance (C) dépend de **l'application** et pas de la base de données.  
Donne un exemple de règle de consistance que la base de données ne peut pas vérifier seule.

### Ex 3 — Exemple multi-objets (3 min)
Donne 2 exemples de cas où une transaction **multi-objets** est indispensable (on ne peut pas s'en passer avec des opérations single-object séquentielles).

---

## ✅ Terminé quand

- [ ] Lecture (début Ch.7 → Single/Multi-Object) terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (tableau ACID) fait
- [ ] Ex 2 (pourquoi C est différent) expliqué
- [ ] Ex 3 (exemples multi-objets) fait
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.7 — Niveaux d'isolation faibles : Read Committed. Ce que garantit (et ne garantit pas) le niveau le plus commun.
