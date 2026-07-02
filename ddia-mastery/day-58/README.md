# Jour 58 — Quiz DDIA : 20 questions sur les 12 chapitres

🧪 Auto-évaluation · ~60 min · Pas de lecture (répondre de mémoire d'abord)

---

## 🎯 Règle du jeu

Réponds à toutes les questions **sans ouvrir le livre ni tes notes**.  
Ensuite seulement, vérfie tes réponses.  
Note ton score : ___/20

---

## 20 questions

### Partie I — Fondations (Ch.1-4)

**1.** Quelle est la différence entre un **fault** (panne) et un **failure** (défaillance) ? Donne un exemple de chacun.

**2.** Qu'est-ce que l'**impedance mismatch** ? Dans quel modèle de données ce problème est-il absent ?

**3.** Un B-Tree et un LSM-Tree pour la même charge (80% lectures, 20% écritures) : lequel choisirais-tu et pourquoi ?

**4.** Qu'est-ce que la **forward compatibility** dans le contexte de l'encodage ? Donne un exemple concret avec Protobuf.

### Partie II — Données distribuées (Ch.5-9)

**5.** Dans la réplication single-leader, quelle est la différence entre **réplication synchrone** et **asynchrone** ? Quand choisir l'une ou l'autre ?

**6.** Qu'est-ce qu'un **read-your-writes** consistency ? Pourquoi est-ce difficile avec la réplication ?

**7.** Tu as n=5 noeuds, w=3, r=3. Un noeud tombe. Peut-on encore lire ? Encore écrire ? Justifie.

**8.** Dans le partitionnement par hash, pourquoi est-ce que `hash(key) % N` est une mauvaise idée quand N change ?

**9.** Qu'est-ce qu'un **scatter-gather** dans le contexte des index secondaires partitionnés ? Quel est son coût ?

**10.** Explique la propriété **Atomicity** dans ACID. En quoi est-elle différente de l'atomicité CPU ?

**11.** Un utilisateur lit son propre compte bancaire deux fois dans la même transaction et voit deux soldes différents. Quelle anomalie est-ce ? Quel niveau d'isolation la prévient ?

**12.** Dans le **write skew** des médecins de garde : pourquoi le Snapshot Isolation ne protège-t-il pas ? Quelle est la seule solution ?

**13.** Explique **SSI (Serializable Snapshot Isolation)** en 3 phrases : mécanisme, avantage, quand ça abort une transaction.

**14.** Pourquoi un processus peut-il ne pas savoir qu'il a été en pause (GC stop) ? Quelles conséquences pour l'élection de leader ?

**15.** Qu'est-ce que la **linéarisabilité** ? Donne un exemple de système qui en a besoin.

### Partie III — Données dérivées (Ch.10-12)

**16.** Quelle est la différence entre un **sort-merge join** et un **broadcast hash join** dans MapReduce/Spark ? Quand utiliser chacun ?

**17.** Pourquoi Kafka peut-il être vu comme un **Total Order Broadcast** (lien avec Ch.9) ?

**18.** Qu'est-ce que le **Change Data Capture (CDC)** ? Comment Debezium l'implémente-t-il pour Postgres ?

**19.** Dans le stream processing, un watermark de 5 minutes signifie quoi exactement ? Que se passe-t-il avec un événement qui arrive 10 minutes après son event time ?

**20.** Quelle est la différence entre la **Lambda architecture** et la **Kappa architecture** ? Quel problème la Kappa résout-elle ?

---

## ✅ Terminé quand

- [ ] 20 questions répondues sans aide
- [ ] Vérification faite avec le livre/tes notes
- [ ] Score noté : ___/20
- [ ] Lacunes identifiées pour les derniers jours
- [ ] Coché dans PROGRESS.md

## → Demain
Questions d'entretien technique : comment répondre aux questions DDIA dans un contexte d'entretien d'ingénieur.
