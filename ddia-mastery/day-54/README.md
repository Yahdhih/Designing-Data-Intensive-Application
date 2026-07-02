# Jour 54 — 🔁 Revue Partie III (Ch.10 + Ch.11 + Ch.12)

🔁 Rappel actif · ~60 min

---

## 🎯 Objectif du jour

Consolider la Partie III complète. Ces 3 chapitres forment un arc : comment **calculer** (batch), **réagir** (stream), et **assembler** (intégration + éthique) des systèmes de données.

---

## ✏️ Exercices (60 min)

### Ex 1 — Page blanche Partie III (20 min)

Ferme tout. Dans `notes.md`, retrouve de mémoire les points clés :

**Ch.10 — Batch Processing :**
- Philosophie Unix (principe) :
- MapReduce : Map → Shuffle → Reduce (résumé)
- Sort-merge join vs broadcast hash join :
- Spark vs MapReduce (différence principale) :

**Ch.11 — Stream Processing :**
- Queue vs Log-based (Kafka) — différence clé :
- CDC : ce que c'est + exemple pipeline :
- Event Sourcing : principe + avantage :
- Event time vs Processing time + watermarks :
- Les 4 types de fenêtres (noms) :
- Lambda vs Kappa architecture :

**Ch.12 — Future of Data Systems :**
- Problème d'intégration des données (2-3 lignes) :
- Unbundling the database (principe) :
- CQRS : command vs query (1 ligne chacun) :
- Données dérivées = reconstructibles (pourquoi important) :

### Ex 2 — 6 questions flash (15 min)

Réponds sans aide :

1. Quelle est la différence entre un job Spark et une requête Postgres ? (architecture, non fonctionnalités)
2. Pourquoi Kafka est-il un log-based system plutôt qu'une queue classique ? Quel avantage concret ?
3. Qu'est-ce que le CDC ? Cite un outil qui l'implémente.
4. Un événement stream arrive avec event_time = 14h00 mais processing_time = 14h08. Qu'est-ce qu'un watermark de 5 min décide de faire ?
5. Pourquoi la Kappa architecture est-elle souvent préférable à la Lambda architecture ?
6. Qu'est-ce qu'une vue dérivée ? Citez 3 exemples dans un système typique.

### Ex 3 — Le grand arc Partie I → Partie III (15 min)

DDIA a 3 parties. Dans `notes.md`, explique comment chacune s'appuie sur la précédente :

- **Partie I (Ch.1-4)** : pose les fondations — fiabilité, modèles de données, stockage, encodage
- **Partie II (Ch.5-9)** : distribue ces fondations — réplication, partitionnement, transactions, consensus
- **Partie III (Ch.10-12)** : construit par-dessus — calcul batch, stream, intégration

Quelle est la **question centrale** que chaque partie répond ?

### Ex 4 — Vérification (10 min)

Ouvre les Summaries de Ch.10, Ch.11, Ch.12 et compare tes réponses.  
Note les 3 points oubliés les plus importants.

---

## ✅ Terminé quand

- [ ] Page blanche Partie III complète
- [ ] 6 questions flash répondues
- [ ] Arc Partie I → III expliqué
- [ ] Vérification faite + lacunes notées
- [ ] Coché dans PROGRESS.md

## → Demain
Synthèse DDIA complète 1/2 — Parties I et II en une seule page blanche.
