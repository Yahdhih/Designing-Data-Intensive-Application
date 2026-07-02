# Jour 39 — Ch.9 : Ordre causal + Total Order Broadcast

📖 Lecture · ~45 min de lecture + 15 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 9, sections « Ordering Guarantees » + « Distributed Transactions and Consensus » (jusqu'à la fin de « Total Order Broadcast »)

La linéarisabilité est forte mais coûteuse. Il existe une garantie plus faible mais souvent suffisante : la **causalité** (si A cause B, alors tout le monde voit A avant B). Et le **Total Order Broadcast** est le mécanisme fondamental qui permet de construire des systèmes cohérents.

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, réponds AVANT d'ouvrir le livre :

1. Si Alice envoie un message « j'ai froid » et Bob répond « porte un manteau » — il est essentiel que tout le monde voie le message d'Alice **avant** la réponse de Bob. Comment garantir ça sans horloge globale ?
2. Qu'est-ce que le **Total Order Broadcast** selon ton intuition ? En quoi est-ce utile ?
3. Quelle est la relation entre le Total Order Broadcast et le log de Kafka ?

---

## 📚 Points à remarquer pendant la lecture

- **Ordre causal (causal consistency)** : plus faible que la linéarisabilité mais plus fort que la consistance éventuelle. Préserve les relations cause-effet
- **Lamport timestamps** : garantissent un ordre total sur les événements, mais avec un problème : ne permettent pas de savoir si une opération est *terminée* avant d'assigner un timestamp
- **Total Order Broadcast** : tous les noeuds reçoivent les messages dans le **même ordre** — c'est la propriété du log de Kafka (et de ZooKeeper)
- Équivalence : Total Order Broadcast ≡ Consensus ≡ Linearizable read-write register — ce sont les mêmes problèmes sous des angles différents
- Comment implémenter un **verrou distribué** avec Total Order Broadcast

---

## ✏️ Exercices (15 min)

### Ex 1 — Kafka comme Total Order Broadcast (7 min)

Kafka garantit un ordre total des messages **dans une partition**.  
Grâce à Ch.9 :
- En quoi Kafka est-il une implémentation de Total Order Broadcast ?
- Pourquoi Kafka ne garantit **pas** un ordre total **entre partitions** ?
- Quel problème cela crée-t-il pour un consommateur qui lit depuis plusieurs partitions ?

### Ex 2 — Lamport timestamps : la limite (5 min)

Kleppmann montre que les Lamport timestamps ne suffisent pas pour certains problèmes.  
Exemple : deux utilisateurs s'enregistrent avec le même username en même temps.  
Pourquoi ne peut-on pas utiliser les Lamport timestamps pour résoudre ce conflit ?

### Ex 3 — Connexion : Consensus = Total Order Broadcast (3 min)
Kleppmann dit que ces problèmes sont **équivalents** :
- Consensus
- Total Order Broadcast
- Linearizable compare-and-set register

Explique intuitivement pourquoi résoudre l'un résout les autres.

---

## ✅ Terminé quand

- [ ] Lecture (Ordering Guarantees + Total Order Broadcast) terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (Kafka + Total Order Broadcast) fait
- [ ] Ex 2 (Lamport timestamps + limite) fait
- [ ] Ex 3 (équivalence des 3 problèmes) fait
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.9 — Algorithmes de consensus distribué (Raft, ZooKeeper/ZAB, Paxos) + Résumé Ch.9.
