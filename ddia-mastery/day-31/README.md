# Jour 31 — Ch.7 : Sérialisabilité — 2PL et SSI

📖 Lecture · ~45 min de lecture + 15 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 7, section « Serializability » (Two-Phase Locking + Serializable Snapshot Isolation) + « Summary »

La **sérialisabilité** est le niveau d'isolation le plus fort : le résultat de N transactions concurrentes est identique à ce qu'on obtiendrait si elles s'exécutaient séquentiellement, une par une. Kleppmann présente les deux implémentations modernes.

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, réponds AVANT d'ouvrir le livre :

1. Two-Phase Locking : qu'est-ce que ça veut dire selon ton intuition ? Quelles sont les 2 phases ?
2. Qu'est-ce qu'un **deadlock** dans le contexte de verrous ? Donne un exemple avec 2 transactions.
3. Si les verrous sont coûteux et les deadlocks possibles, quelle alternative optimiste imagines-tu ?

---

## 📚 Points à remarquer pendant la lecture

**Two-Phase Locking (2PL) :**
- Phase 1 — Acquisition : une transaction acquiert des verrous (partagés pour la lecture, exclusifs pour l'écriture) et **ne les libère pas**
- Phase 2 — Libération : après le commit/abort, tous les verrous sont relâchés d'un coup
- **Shared lock** (lecture) : plusieurs transactions peuvent lire simultanément
- **Exclusive lock** (écriture) : personne d'autre ne peut lire ni écrire
- **Predicate locks** : verrouiller toutes les lignes qui correspondent à une condition (solution aux phantoms)
- **Deadlocks** : 2PL les génère naturellement → la BDD doit les détecter et annuler une transaction

**Serializable Snapshot Isolation (SSI) :**
- Approche **optimiste** : toutes les transactions lisent un snapshot, sans verrouiller
- À la fin, la BDD vérifie si des conflits ont eu lieu → si oui, abort + retry
- Détection des cycles de dépendances read-write
- Plus performant que 2PL sous faible contention, mais requiert des retries

---

## ✏️ Exercices (15 min)

### Ex 1 — 2PL vs SSI : tableau (8 min)

| | Two-Phase Locking | SSI |
|--|------------------|-----|
| Approche | Pessimiste | Optimiste |
| Verrous ? | Oui | |
| Deadlocks ? | Oui | |
| Performance sous forte contention | | |
| Retry nécessaire ? | Non | |
| Implémenté dans | Postgres (LOCK), MySQL | |

### Ex 2 — Deadlock : le diagramme (4 min)

Dans `notes.md`, décris un deadlock simple avec 2 transactions et 2 ressources :

```
T1 : verrouille A → attend B
T2 : verrouille B → attend A
→ Deadlock !
```

Comment Postgres détecte-t-il un deadlock ? Que se passe-t-il ensuite ?

### Ex 3 — Résumé final Ch.7 : la hiérarchie (3 min)

Liste les niveaux d'isolation de Ch.7 du plus faible au plus fort, avec l'anomalie que chacun **empêche** :

1. Read Uncommitted → empêche rien
2. Read Committed → empêche ...
3. Repeatable Read / Snapshot Isolation → empêche en plus ...
4. Serializable → empêche en plus ...

---

## ✅ Terminé quand

- [ ] Lecture (2PL + SSI + Summary) terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (tableau 2PL vs SSI) fait
- [ ] Ex 2 (deadlock) fait
- [ ] Ex 3 (hiérarchie niveaux d'isolation) fait
- [ ] Coché dans PROGRESS.md

## → Demain
Exercice de conception : système de réservation sans double-booking. Choisir le bon niveau d'isolation.
