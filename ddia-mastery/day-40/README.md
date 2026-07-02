# Jour 40 — Ch.9 : Algorithmes de consensus (Raft, ZooKeeper) + Résumé

📖 Lecture · ~40 min de lecture + 20 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 9, section « Distributed Transactions and Consensus » (suite : algorithmes de consensus, ZooKeeper) + « Summary »

Les algorithmes de consensus (Raft, Paxos, ZAB) sont ce qui permet à des noeuds de se mettre d'accord malgré les pannes. C'est le coeur de ZooKeeper, etcd, et Kafka KRaft.

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, réponds AVANT d'ouvrir le livre :

1. Raft élit un leader. Comment sait-on qu'un candidat a « gagné » l'élection ?
2. Qu'est-ce que le **Two-Phase Commit (2PC)** selon ta mémoire ? (Transaction distribuée sur plusieurs noeuds)
3. ZooKeeper offre des « primitives » de coordination : verrous, élection de leader, configuration distribuée. Comment ces primitives sont-elles liées au consensus ?

---

## 📚 Points à remarquer pendant la lecture

- **Two-Phase Commit (2PC)** : le coordinateur demande à tous les participants si they can commit (prepare), puis envoie commit ou abort. Le problème : si le coordinateur tombe après prepare → **blocage**
- **Three-Phase Commit (3PC)** : tente de résoudre le blocage de 2PC, mais suppose un réseau borné → ne fonctionne pas sur un réseau asynchrone
- **Consensus distribué (Raft, Paxos)** : élire un leader, répliquer les entrées de log, garantir que tous les noeuds voient le même log dans le même ordre
- **ZooKeeper** : implémente le consensus (ZAB, similar to Paxos) et expose des primitives de haut niveau
- Les **limitations du consensus** : il faut une majorité de noeuds disponibles → si on perd la majorité, le système bloque (favour consistency over availability)

---

## ✏️ Exercices (20 min)

### Ex 1 — 2PC : le problème du coordinateur (8 min)

Dans `notes.md`, complète ce scénario :

```
Phase 1 (Prepare) :
  Coordinateur → Participant A : "Peux-tu committer ?"
  Coordinateur → Participant B : "Peux-tu committer ?"
  A → Coordinateur : "Oui"
  B → Coordinateur : "Oui"
  
[Coordinateur tombe ici]

Phase 2 (Commit) : ??? — jamais envoyée
```

**Questions :**
- A et B sont dans quel état ? Peuvent-ils décider seuls ?
- Pourquoi 2PC est-il appelé un protocole « bloquant » ?
- Comment Raft/Paxos évite-t-il ce blocage ?

### Ex 2 — ZooKeeper dans ton stack (7 min)
Tu as utilisé Kafka avec ZooKeeper (ancienne architecture) ou KRaft (nouvelle architecture).  
Grâce à Ch.9, explique :
- Quel rôle jouait ZooKeeper dans Kafka ? (coordination, leader election, configuration)
- Pourquoi Kafka a-t-il décidé de remplacer ZooKeeper par KRaft ?
- KRaft utilise Raft — en quoi est-ce une amélioration pour Kafka ?

### Ex 3 — Résumé Ch.9 : la hiérarchie de consistance (5 min)

Dans `notes.md`, place ces garanties du plus fort au plus faible :

- Linearizability
- Causal consistency
- Eventual consistency
- Serializable isolation (Ch.7)
- Read-your-writes

---

## ✅ Terminé quand

- [ ] Lecture (2PC + consensus + ZooKeeper + Summary) terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (2PC blocage) fait
- [ ] Ex 2 (ZooKeeper dans Kafka) fait
- [ ] Ex 3 (hiérarchie de consistance) fait
- [ ] Coché dans PROGRESS.md

## → Demain
🔁 Revue Ch.9 + Revue globale de la Partie II (Ch.5→Ch.9).
