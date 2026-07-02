# Jour 27 — Ch.7 : Niveaux d'isolation faibles — Read Committed

📖 Lecture · ~45 min de lecture + 15 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 7, section « Weak Isolation Levels » jusqu'à la fin de « Read Committed »

L'isolation parfaite (serializable) est coûteuse. Les bases de données offrent donc des niveaux d'isolation plus faibles — avec des garanties moindres mais de meilleures performances. Kleppmann commence par **Read Committed**, le niveau par défaut de la plupart des bases de données (Postgres, Oracle, SQL Server).

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, réponds AVANT d'ouvrir le livre :

1. Qu'est-ce qu'un **dirty read** selon toi ? Donne un exemple où ça pose un problème.
2. Qu'est-ce qu'un **dirty write** ? En quoi est-ce dangereux ?
3. Si deux transactions s'exécutent en même temps, que peut voir l'une que l'autre n'a pas encore committé ?

---

## 📚 Points à remarquer pendant la lecture

- **Dirty read** : lire les données d'une transaction qui n'a pas encore été committée → dangereux si elle est ensuite annulée (rollback)
- **Dirty write** : écraser les données d'une transaction non committée → l'exemple de la voiture (deux acheteurs, une voiture)
- **Read Committed** garantit : pas de dirty reads, pas de dirty writes
- **Row-level locking** : comment Read Committed prévient les dirty writes
- **Pour les dirty reads** : Postgres/Oracle ne bloquent pas → ils gardent l'**ancienne valeur** pendant qu'une transaction est en cours

---

## ✏️ Exercices (15 min)

### Ex 1 — Dirty read : scénario concret (6 min)

Dans `notes.md`, complète ce diagramme de séquence :

```
T1 (virement)          T2 (affichage solde)
BEGIN
UPDATE compte_A = 500 (de 1000)
UPDATE compte_B = 1500 (de 1000)
                       SELECT compte_A → ??? dirty read !
                       SELECT compte_B → ???
ROLLBACK (erreur réseau)
```

**Question :** Qu'est-ce que T2 lit si on autorise les dirty reads ?  
Quel est le problème si T1 fait un ROLLBACK après ?

### Ex 2 — Dirty write : l'exemple de la voiture (5 min)

Reproduis le scénario de Kleppmann avec 2 acheteurs pour 1 voiture.  
Explique pourquoi les dirty writes peuvent créer une situation incohérente même si chaque transaction individuelle semble correcte.

### Ex 3 — Postgres et les lectures (4 min)

Postgres évite les dirty reads sans bloquer les lecteurs.  
Explique brièvement le mécanisme qu'il utilise pour qu'un lecteur voit l'ancienne valeur pendant qu'une écriture est en cours.

---

## ✅ Terminé quand

- [ ] Lecture (Weak Isolation + Read Committed) terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (diagramme dirty read) fait
- [ ] Ex 2 (dirty write + voiture) fait
- [ ] Ex 3 (mécanisme Postgres) fait
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.7 — Snapshot Isolation et Repeatable Read. Comment MVCC (Multi-Version Concurrency Control) fonctionne ?
