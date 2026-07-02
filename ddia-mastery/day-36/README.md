# Jour 36 — Ch.8 : Processus qui gèlent + Vérité et connaissance

📖 Lecture · ~40 min de lecture + 20 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 8, sections « Process Pauses » + « Knowledge, Truth, and Lies » + « Summary »

La dernière partie de Ch.8 est la plus philosophique. Elle pose des questions fondamentales : dans un système distribué, qu'est-ce qu'un noeud peut **vraiment savoir** ? Peut-il savoir qu'il est le leader ? Qu'un autre noeud est mort ?

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, réponds AVANT d'ouvrir le livre :

1. Un processus peut se « mettre en pause » sans savoir qu'il a été en pause (ex : garbage collection, VM migration). Quelles conséquences cela a-t-il pour un leader de réplication ?
2. Qu'est-ce qu'un **split brain** (cerveau divisé) dans un système distribué ?
3. Est-ce qu'un noeud peut savoir avec certitude que les autres noeuds le considèrent comme le leader ?

---

## 📚 Points à remarquer pendant la lecture

- **Process pauses** : GC stops, VM migrations, page faults → un leader peut croire qu'il est toujours leader alors qu'il a été remplacé
- **Split brain** : deux noeuds croient tous deux être le leader — dangereux car ils peuvent tous deux accepter des écritures
- **Fencing tokens** : solution au split brain — le leader a un token croissant, le storage rejette les tokens périmés
- **The Truth is Defined by the Majority** : un noeud ne peut pas décider seul — il faut un quorum
- **Byzantine faults** : un noeud qui **ment** (envoie des données fausses délibérément ou à cause d'un bug)
- **System models** : synchronous, partially synchronous, asynchronous — quel modèle correspond à Internet ?

---

## ✏️ Exercices (20 min)

### Ex 1 — Le scénario du leader mort-vivant (8 min)

Dans `notes.md`, décris ce scénario :

```
1. Noeud L est élu leader
2. L fait une longue GC pause (10 secondes)
3. Les followers ne reçoivent plus de heartbeat → élisent L2 comme nouveau leader
4. L se réveille de la GC pause → croit toujours être le leader
5. L continue d'accepter des écritures
```

Questions :
- Que se passe-t-il si L **et** L2 acceptent des écritures en même temps ?
- Comment les **fencing tokens** résolvent-ils ce problème ?
- Est-ce que L peut savoir, après sa GC pause, qu'il n'est plus le leader ?

### Ex 2 — Modèles du système (7 min)

Kleppmann définit 3 modèles du système :

| Modèle | Hypothèse sur le réseau | Hypothèse sur le temps |
|--------|------------------------|----------------------|
| Synchrone | | |
| Partiellement synchrone | | |
| Asynchrone | | |

Lequel décrit le mieux Internet ? Et un réseau datacenter interne ?

### Ex 3 — Connexion Ch.5 + Ch.8 (5 min)
Ch.5 décrivait comment un leader est élu. Ch.8 montre pourquoi l'élection de leader est difficile.  
En 3 phrases, explique pourquoi Kafka (ou ZooKeeper/KRaft) doit gérer les cas de Ch.8 pour que l'élection de leader fonctionne correctement.

---

## ✅ Terminé quand

- [ ] Lecture (Process Pauses + Truth + Summary) terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (leader mort-vivant + fencing tokens) fait
- [ ] Ex 2 (3 modèles système) fait
- [ ] Ex 3 (connexion Ch.5 + Ch.8) fait
- [ ] Coché dans PROGRESS.md

## → Demain
🔁 Revue Ch.8 + connexion globale Ch.5→Ch.9. Puis entrée en Ch.9 : consensus.
