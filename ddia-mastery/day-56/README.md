# Jour 56 — Synthèse DDIA 2/2 : Partie III + Vue globale

🔁 Grande synthèse finale · ~60 min · Pas de nouvelle lecture

---

## 🎯 Objectif du jour

Compléter la synthèse globale de DDIA avec la Partie III, puis construire la vision unifiée du livre en entier.

---

## ✏️ Exercices (60 min)

### Ex 1 — Page blanche Partie III (15 min)

De mémoire, sans aide :

**Ch.10 — Batch :**
- Inputs immuables → pourquoi c'est important :
- MapReduce : les 3 phases :
- Spark vs MapReduce — différence principale :
- Quel type de join pour un petit dataset vs deux grands :

**Ch.11 — Stream :**
- Kafka vs RabbitMQ — différence fondamentale :
- CDC : définition + exemple :
- Event time vs Processing time — quelle différence concrète :
- Lambda vs Kappa — lequel Kleppmann préfère et pourquoi :

**Ch.12 — Future :**
- Données dérivées — ce que ça veut dire :
- Unbundling — analogie à retenir :
- CQRS — séparation de quoi :

### Ex 2 — La vision unifiée de DDIA en 10 phrases (20 min)

Dans `notes.md`, écris 10 phrases qui capturent le message global de tout DDIA.  
Une phrase par chapitre, dans l'ordre. Commence chaque phrase par « Ch.X montre que... »

Exemple (à compléter) :
- Ch.1 montre que...
- Ch.2 montre que...
- ...
- Ch.12 montre que...

### Ex 3 — Exercice de conception transversal (15 min)

Tu dois concevoir un **système de recommandation de produits** pour un site e-commerce :
- 100M d'utilisateurs, 10M de produits
- Log de clicks + achats → générer des recommandations personnalisées
- Latence cible : < 100ms pour afficher les recs
- Fraîcheur : les recs doivent tenir compte des achats de moins de 1h

Dans `notes.md`, pour chacun des composants, cite le(s) chapitre(s) de DDIA qui s'applique :

| Composant | Technologie choisie | Chapitres DDIA |
|-----------|---------------------|---------------|
| Stockage des clicks (source of truth) | | |
| Pipeline de calcul des recs (batch) | | |
| Pipeline temps réel (achats récents) | | |
| Stockage des recs (serving) | | |
| Synchronisation source → serving | | |
| Tolérance aux pannes | | |

### Ex 4 — Ce que j'ai appris (10 min)

Dernière question. Dans `notes.md`, réponds honnêtement :

1. Quelle est **la chose la plus surprenante** que tu as apprise en lisant DDIA ?
2. Quelle est **la chose la plus utile** pour ton travail quotidien avec Spark/Kafka/OpenSearch ?
3. Qu'est-ce que tu aurais voulu comprendre **avant** de commencer à utiliser ces outils ?

---

## ✅ Terminé quand

- [ ] Page blanche Partie III complète
- [ ] 10 phrases sur DDIA (une par chapitre) écrites
- [ ] Exercice de conception transversal fait
- [ ] Réflexion personnelle faite
- [ ] Coché dans PROGRESS.md

## → Demain
Exercice de conception avancé : système de détection de fraude en temps réel. Appliquer Parties II et III ensemble.
