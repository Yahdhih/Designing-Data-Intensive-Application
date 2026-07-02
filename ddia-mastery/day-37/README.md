# Jour 37 — 🔁 Revue Ch.8 + Prédictions Ch.9

🔁 Rappel actif + transition · ~60 min

---

## 🎯 Objectif du jour

Consolider Ch.8 et préparer mentalement Ch.9 (Consensus). Ch.8 a posé les problèmes — Ch.9 va proposer des solutions.

---

## ✏️ Exercices (60 min)

### Ex 1 — Page blanche Ch.8 (20 min)

Ferme tout. Dans `notes.md`, liste de mémoire les **3 grandes familles de problèmes** de Ch.8 :

**Réseau :**
- Le problème fondamental :
- Pourquoi timeout ne suffit pas :
- La conséquence : un noeud ne peut pas...

**Horloges :**
- Time-of-day vs monotonic :
- Précision NTP en pratique :
- Pourquoi LWW + timestamp est dangereux :
- La solution : logical clocks (Lamport) font quoi ?

**Processus :**
- Les causes de pause (3 exemples) :
- Split brain :
- Fencing tokens :
- Ce qu'un noeud ne peut pas savoir :

### Ex 2 — 5 questions flash Ch.8 (15 min)

Réponds sans aide :

1. Quelle est la différence entre un réseau partiellement synchrone et un réseau asynchrone ?
2. Pourquoi les timeouts sont-ils la seule façon de détecter une panne — et en quoi c'est insuffisant ?
3. Qu'est-ce qu'un fencing token et pourquoi il protège contre le split brain ?
4. Pourquoi NTP ne peut pas garantir une synchronisation parfaite entre deux serveurs ?
5. Dans quel cas un noeud peut-il envoyer des données **incorrectes** (pas juste indisponible) ?

### Ex 3 — Connexion Ch.5 → Ch.8 → Ch.9 (15 min)

Dans `notes.md`, complète ce fil conducteur :

```
Ch.5 — Réplication : comment copier les données sur plusieurs noeuds ?
  ↓ Mais comment élire un leader de façon fiable ?

Ch.6 — Partitionnement : comment diviser les données ?
  ↓ Mais comment savoir quelle partition est sur quel noeud ?

Ch.7 — Transactions : comment garantir des opérations correctes ?
  ↓ Mais tout ça supposait un seul noeud fiable...

Ch.8 — Problèmes distribués : les réseaux et horloges ne sont pas fiables
  ↓ Alors comment prendre des décisions collectives malgré ça ?

Ch.9 — Consensus : ???
```

Complète la dernière flèche avec ce que tu penses que Ch.9 va proposer.

### Ex 4 — Prédictions Ch.9 (10 min)

Dans `notes.md`, réponds AVANT de lire Ch.9 :

1. Qu'est-ce que le « problème du consensus » dans les systèmes distribués ?
2. Tu connais Raft (utilisé dans etcd, CockroachDB, Kafka KRaft). Comment fonctionne-t-il à haut niveau ?
3. Qu'est-ce qu'une « linearizable » lecture ? En quoi est-ce plus fort que la consistance éventuelle (eventual consistency) ?

---

## ✅ Terminé quand

- [ ] Page blanche Ch.8 (3 familles de problèmes) complète
- [ ] 5 questions flash répondues
- [ ] Fil conducteur Ch.5→Ch.9 complété
- [ ] Prédictions Ch.9 notées
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.9 — Consistance et consensus : linéarisabilité, causalité, total order broadcast, Raft.
