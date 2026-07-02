# Jour 51 — Ch.12 : Intégration des données + Données dérivées

📖 Lecture · ~45 min de lecture + 15 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 12, du début jusqu'à la fin de la section « Derived Data Versus Distributed Transactions »

Ch.12 est le dernier chapitre — et le plus synthétique. Kleppmann ne présente plus de nouvelles technologies mais réfléchit à comment **assembler** tous les composants des chapitres précédents en un système cohérent. Il commence par une question clé : dans un système avec plusieurs bases de données, comment garder les données synchronisées ?

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, réponds AVANT d'ouvrir le livre :

1. Dans un système typique, on a souvent : une base SQL (source of truth), un index de recherche (OpenSearch), un cache (Redis), une BDD analytique. Comment maintenir ces 4 systèmes synchronisés ?
2. Les transactions distribuées (2PC, Ch.9) peuvent synchroniser plusieurs systèmes. Quel est le problème de cette approche à grande échelle ?
3. Qu'est-ce qu'une **vue dérivée** (derived view) selon ton intuition ?

---

## 📚 Points à remarquer pendant la lecture

- Le problème de l'**intégration des données** : dans un système réel, les données doivent souvent exister dans plusieurs formes (SQL pour les transactions, index pour la recherche, colonnes pour l'analytique...)
- **Total Order Broadcast** (Ch.9) comme solution : si tous les événements passent par le même log ordonné, tous les consommateurs peuvent maintenir une vue cohérente
- **Données dérivées** : un index de recherche, un cache, un tableau de bord sont tous des **vues dérivées** de la base principale — ils peuvent toujours être reconstruits à partir des données sources
- Pourquoi les **transactions distribuées** (2PC) ne passent pas à l'échelle : coordination bloquante, hétérogénéité des systèmes
- L'approche par **événements asynchrones** (CDC + Kafka) : plus tolérante aux pannes, mais cohérence éventuelle

---

## ✏️ Exercices (15 min)

### Ex 1 — Le système complet : synchroniser 4 datastores (8 min)

Dans `notes.md`, dessine un schéma (texte ou ASCII) du pipeline suivant :

```
Application → Postgres (source of truth)
                   ↓ CDC (Debezium)
              Kafka (log ordonné)
              ↙         ↓         ↘
     OpenSearch    Redis cache    Spark (DWH)
```

Questions :
- Si OpenSearch est en retard de 2 secondes par rapport à Postgres, est-ce un problème pour la recherche ? Pour les transactions ?
- Si Kafka retient les événements 7 jours, peut-on reconstruire l'index OpenSearch complet depuis zéro ?
- Quelle est la différence avec une approche 2PC qui synchroniserait les 4 en même temps ?

### Ex 2 — Données dérivées : implication pratique (4 min)
Kleppmann dit que les vues dérivées peuvent être reconstruites.  
En 3 phrases, explique pourquoi cette propriété est utile lors d'un **bug en production** qui a corrompu l'index de recherche.

### Ex 3 — Connexion Ch.9 + Ch.12 (3 min)
Le Total Order Broadcast de Ch.9 et le CDC via Kafka de Ch.12 sont liés.  
Explique en 2 phrases comment le log Kafka joue le rôle de « source d'ordre » dans l'intégration des données.

---

## ✅ Terminé quand

- [ ] Lecture (début Ch.12 → Derived Data vs Distributed Transactions) terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (schéma pipeline 4 datastores) fait
- [ ] Ex 2 (vues dérivées reconstructibles) fait
- [ ] Ex 3 (connexion Ch.9 + Ch.12) fait
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.12 — Concevoir des applications autour du dataflow. Les écriture et les lectures comme événements.
