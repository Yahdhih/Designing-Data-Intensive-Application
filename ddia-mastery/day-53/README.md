# Jour 53 — Ch.12 : Correctness, Contraintes, Confiance et Éthique

📖 Lecture · ~40 min de lecture + 20 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 12, section « Doing the Right Thing » + « Summary » (fin du livre)

La dernière section de DDIA sort du technique pour aborder des questions humaines et éthiques : comment concevoir des systèmes qui font ce qu'ils promettent ? Qui traitent les utilisateurs avec dignité ? Kleppmann termine par un appel à la responsabilité des ingénieurs de données.

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, réponds AVANT d'ouvrir le livre :

1. Tu as conçu un système de données. Comment vérifies-tu qu'il fait ce qu'il est censé faire ? (Pas juste « les tests passent »)
2. Kleppmann parle de « predictive analytics » (ex : scoring de crédit, ciblage publicitaire). Quels risques vois-tu dans l'utilisation de ces systèmes pour des décisions qui impactent des personnes ?
3. En tant qu'ingénieur de données, as-tu une responsabilité sur l'**utilisation** des systèmes que tu construis ?

---

## 📚 Points à remarquer pendant la lecture

- **Correctness** dans les systèmes distribués : les garanties ACID et les quorums ne sont pas des garanties absolues — il faut tester end-to-end et mesurer
- **Enforcement des contraintes** sans transactions distribuées : utiliser les unicité via le log ordonné (opération de compare-and-set sur le stream)
- **Timeliness vs Integrity** : la fraîcheur des données vs leur exactitude. Parfois une vue légèrement en retard est acceptable si elle est exacte
- **Auditabilité** des systèmes de données : qui a accédé à quoi, quand, pourquoi → logs immuables comme preuves
- **Surveillance des données** et vie privée : les données personnelles agrégées permettent des inférences non consenties
- L'appel à la **responsabilité professionnelle** des ingénieurs de données

---

## ✏️ Exercices (20 min)

### Ex 1 — Correctness end-to-end (8 min)

Un système de paiement Kafka + Postgres traite 10 000 transactions/jour.  
Dans `notes.md`, décris **3 façons de vérifier** que le système est correct end-to-end :
1. Une vérification **en temps réel** (ex : monitoring, alertes)
2. Une vérification **a posteriori** (ex : réconciliation, audit)
3. Une vérification **structurelle** dans la conception (ex : idempotence, event sourcing)

### Ex 2 — Éthique des données (7 min)

Tu conçois un système de scoring qui prédit la probabilité qu'un utilisateur rembourse un prêt.  
Dans `notes.md`, identifie :
1. Quelles données utiliserais-tu ? Lesquelles éviterais-tu (et pourquoi) ?
2. Comment détecterais-tu un **biais discriminatoire** dans ton modèle ?
3. Comment rendrais-tu le système **auditable** si un utilisateur conteste une décision ?

### Ex 3 — Résumé final Ch.12 (5 min)
Dans `notes.md`, écris en 5 phrases le message principal de Ch.12.  
Commence par : « Ch.12 soutient que les ingénieurs de données... »

---

## ✅ Terminé quand

- [ ] Lecture (Doing the Right Thing + Summary) terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (3 vérifications de correctness) fait
- [ ] Ex 2 (éthique du scoring) fait
- [ ] Ex 3 (résumé Ch.12) fait
- [ ] Coché dans PROGRESS.md

## → Demain
🔁 Revue Partie III (Ch.10 + Ch.11 + Ch.12) — rappel actif des 3 chapitres.
