# Jour 28 — Ch.7 : Snapshot Isolation + MVCC

📖 Lecture · ~45 min de lecture + 15 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 7, section « Snapshot Isolation and Repeatable Read »

Snapshot Isolation est le niveau d'isolation utilisé par défaut dans Postgres pour les transactions longues (ex : sauvegardes, rapports analytiques). Son mécanisme d'implémentation — **MVCC** (Multi-Version Concurrency Control) — est l'un des concepts les plus élégants de Ch.7.

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, réponds AVANT d'ouvrir le livre :

1. Qu'est-ce qu'une **non-repeatable read** ? (Tu lis la même donnée 2 fois dans la même transaction et tu vois 2 valeurs différentes)
2. Pourquoi les sauvegardes de bases de données ont-elles besoin d'un snapshot cohérent ?
3. Comment fonctionnerait une base de données qui garde **toutes les versions** d'une ligne plutôt que juste la dernière ?

---

## 📚 Points à remarquer pendant la lecture

- **Non-repeatable read** : T1 lit X = 50, T2 modifie X = 100 et commit, T1 relit X = 100. T1 voit des données différentes dans la même transaction
- **Snapshot Isolation** : chaque transaction voit un **snapshot cohérent** de la BDD au moment de son début — elle ne voit pas les changements committés après son début
- **MVCC** : la BDD garde **plusieurs versions** de chaque ligne (avec timestamp/transaction ID de création et suppression)
- Comment une transaction décide quelle version d'une ligne lire : la règle des IDs de transaction
- **Repeatable Read** = nom ISO pour Snapshot Isolation (mais les implémentations varient selon les BDD)
- Les index et MVCC : comment les index gèrent plusieurs versions

---

## ✏️ Exercices (15 min)

### Ex 1 — Non-repeatable read : le problème de la sauvegarde (7 min)

Dans `notes.md`, explique ce scénario :

```
T1 (backup)                     T2 (virement)
BEGIN
SELECT compte_A → 500
                                BEGIN
                                UPDATE compte_A = 400  (retrait 100)
                                UPDATE compte_B = 600  (dépôt 100)
                                COMMIT
SELECT compte_B → 600   ← lit la valeur après commit de T2
```

**Questions :**
- La sauvegarde montre compte_A = 500 et compte_B = 600. Quel est le problème ?
- Snapshot Isolation résout-il ce problème ? Comment ?

### Ex 2 — MVCC : comment les versions fonctionnent (5 min)
Imagine qu'une ligne a été modifiée 3 fois :
- Version 1 : `valeur=100`, créée par tx_id=1
- Version 2 : `valeur=150`, créée par tx_id=5
- Version 3 : `valeur=200`, créée par tx_id=8

Si une transaction a commencé avec tx_id=6, quelle version voit-elle ? Pourquoi ?

### Ex 3 — Impact sur Postgres (3 min)
MVCC signifie que Postgres garde plusieurs versions des lignes sur disque.  
Quel est l'impact en termes d'espace disque ? Qu'est-ce que le processus `VACUUM` fait dans Postgres ?

---

## ✅ Terminé quand

- [ ] Lecture (Snapshot Isolation + MVCC) terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (problème de la sauvegarde) fait
- [ ] Ex 2 (MVCC + versions) fait
- [ ] Ex 3 (VACUUM Postgres) fait
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.7 — Prévention des mises à jour perdues (lost updates) : 4 approches, de l'opération atomique au SELECT FOR UPDATE.
