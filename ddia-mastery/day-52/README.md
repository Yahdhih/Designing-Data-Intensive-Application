# Jour 52 — Ch.12 : Concevoir autour du dataflow

📖 Lecture · ~45 min de lecture + 15 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 12, section « Designing Applications Around Dataflow »

Kleppmann propose une vision de l'architecture orientée données : au lieu de traiter la base de données comme un **composant central** où tout écrit et lit, on peut construire des systèmes où les **données coulent** d'un composant à l'autre via des événements — plus résilient, plus scalable.

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, réponds AVANT d'ouvrir le livre :

1. Dans une architecture microservices, comment deux services partagent-ils des données aujourd'hui dans ton expérience ? Via API REST ? Via base de données partagée ?
2. Quels problèmes pose une **base de données partagée** entre microservices ?
3. Si chaque service écoutait un log d'événements (Kafka) et maintenait sa propre vue locale des données — quels avantages cela aurait-il ?

---

## 📚 Points à remarquer pendant la lecture

- **Unbundling the database** : les bases de données modernes sont un bundle de plusieurs fonctionnalités (stockage, indexation, transactions, query language). On peut « décomposer » ce bundle en composants séparés (Kafka pour le log, RocksDB pour le stockage local, Flink pour les requêtes)
- **Application as a dataflow** : chaque écriture est un événement dans le log → les autres composants réagissent en construisant leurs vues locales
- **Reads as derived data** : les lectures ne touchent que des caches locaux pré-calculés → très rapides
- **Writes and reads separation** (CQRS — Command Query Responsibility Segregation)
- La distinction **mutable state vs immutable log** : le log est la source de vérité, l'état est une vue dérivée

---

## ✏️ Exercices (15 min)

### Ex 1 — CQRS : Command vs Query (7 min)

CQRS sépare les écritures (commands) des lectures (queries) en deux modèles différents.

Dans `notes.md`, décris ce pattern sur un exemple :  
**Système de commandes e-commerce** :
- Command model : comment une commande est-elle créée (PostgreSQL, event sourcing) ?
- Query model : comment le tableau de bord « mes commandes » est-il servi (cache Redis, Elasticsearch) ?
- Comment les deux sont-ils synchronisés (CDC + Kafka) ?

### Ex 2 — Unbundling en pratique (5 min)
Dans ton stack (Spark + Kafka + OpenSearch + Postgres), tu as déjà « débundlé » la base de données.  
Identifie quel composant de ton stack joue quel rôle dans le modèle de Kleppmann :

| Fonctionnalité | Composant traditionnel (BDD) | Ton stack |
|---------------|------------------------------|----------|
| Log de changements | WAL | |
| Stockage durable | Tables | |
| Index de recherche | B-Tree index | |
| Traitement en flux | Stored procedures | |
| Analytique | SQL GROUP BY | |

### Ex 3 — Question ouverte (3 min)
Kleppmann dit que « les applications pourraient être conçues comme des pipelines de dataflow plutôt que comme des requêtes contre une base de données ».  
Quel est le plus grand obstacle pratique à cette vision dans une équipe de 5 ingénieurs ?

---

## ✅ Terminé quand

- [ ] Lecture (Designing Applications Around Dataflow) terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (CQRS e-commerce) fait
- [ ] Ex 2 (unbundling dans ton stack) fait
- [ ] Ex 3 (question ouverte) répondu
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.12 — Correctness, enforcement de contraintes, confiance, et éthique. La conclusion de DDIA.
