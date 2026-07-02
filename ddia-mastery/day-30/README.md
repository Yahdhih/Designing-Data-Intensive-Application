# Jour 30 — Ch.7 : Write Skew et Phantoms

📖 Lecture · ~45 min de lecture + 15 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 7, sections « Write Skew and Phantoms »

Le **write skew** est l'anomalie la plus subtile de Ch.7. Elle survient quand deux transactions lisent le même ensemble de données, prennent des décisions basées sur cet ensemble, et écrivent chacune sur des **objets différents** — violant une contrainte globale. Snapshot Isolation ne protège pas contre ça.

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, réponds AVANT d'ouvrir le livre :

1. Tu as compris le lost update : 2 transactions écrivent sur le **même** objet. Dans le write skew, elles écrivent sur des **objets différents** mais la contrainte est globale. Essaie de deviner un exemple.
2. Qu'est-ce qu'un **phantom read** (lecture fantôme) selon ton intuition ?
3. Pourquoi est-ce qu'une transaction qui voit un snapshot cohérent n'est pas forcément « sérialisable » ?

---

## 📚 Points à remarquer pendant la lecture

- **Write skew** : exemple des médecins de garde — chacun vérifie qu'il y a assez de médecins puis se déconnecte. Résultat : 0 médecins de garde. Les écritures sont sur des objets différents (alice_on_call, bob_on_call) mais la contrainte est globale
- Autres exemples de write skew : réservation de salle de réunion, username unique (race condition), transaction double-spend
- La **structure générale** du write skew :
  1. SELECT (lire pour vérifier une condition)
  2. Décider d'agir selon cette condition
  3. UPDATE/INSERT (écrire sur un objet **différent** de ce qu'on a lu)
- **Phantom read** : une transaction lit un ensemble de lignes, une autre insère une nouvelle ligne dans cet ensemble → la première transaction « voit un fantôme »
- **Materializing conflicts** : transformer un phantom en un lock sur un objet concret

---

## ✏️ Exercices (15 min)

### Ex 1 — Write skew : le diagramme des médecins (7 min)

Dans `notes.md`, complète ce diagramme :

```
T1 (Alice se déconnecte)      T2 (Bob se déconnecte)
BEGIN SI                       BEGIN SI
n = COUNT(on_call) → 2         n = COUNT(on_call) → 2
IF n >= 2:                     IF n >= 2:
  UPDATE alice = off             UPDATE bob = off
COMMIT                         COMMIT
```

**Questions :**
- Pourquoi Snapshot Isolation ne protège pas ici ?
- Alice et Bob ont écrit sur des objets **différents** — en quoi est-ce différent du lost update ?
- Quelle est la seule solution pour éviter ça ?

### Ex 2 — Phantom read : l'exemple de la salle de réunion (5 min)

Scénario : deux personnes réservent simultanément la salle A de 14h à 15h.  
Explique pourquoi `SELECT FOR UPDATE` ne suffit pas ici (il n'y a pas encore de ligne à verrouiller).  
Comment le « materializing conflicts » résout-il ce problème ?

### Ex 3 — Write skew dans ton stack (3 min)
Donne un exemple de write skew possible dans un système que tu connais (Kafka + base de données, microservices, etc.).

---

## ✅ Terminé quand

- [ ] Lecture (Write Skew + Phantoms) terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (diagramme médecins) fait
- [ ] Ex 2 (phantom + salle de réunion) fait
- [ ] Ex 3 (exemple dans ton stack) fait
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.7 — Sérialisabilité : Two-Phase Locking (2PL) et Serializable Snapshot Isolation (SSI). Les solutions robustes.
