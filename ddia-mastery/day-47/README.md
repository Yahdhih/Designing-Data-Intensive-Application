# Jour 47 — Ch.11 : Systèmes de messagerie + Kafka

📖 Lecture · ~45 min de lecture + 15 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 11, du début jusqu'à la fin de la section « Partitioned Logs » (Kafka)

Ch.11 commence par la question fondamentale : comment transmettre des événements d'un producteur à un consommateur ? Kleppmann compare les queues de messages classiques (RabbitMQ) avec les **logs partitionnés** (Kafka) — deux philosophies radicalement différentes.

---

## 🎯 Avant de lire — Prédis (5 min)

Reprends tes prédictions du Jour 46 (Ex 4). Note lesquelles seront confirmées aujourd'hui.

---

## 📚 Points à remarquer pendant la lecture

- **Messaging systems** : deux paradigmes fondamentaux
  - **Queue (point-à-point)** : un message est consommé par **1 seul** consommateur, puis supprimé
  - **Pub/Sub (publish-subscribe)** : un message est livré à **tous** les abonnés
- **Backpressure** : que faire si le consommateur est plus lent que le producteur ?
- **Durabilité** : que faire si le consommateur est en panne au moment de la livraison ?
- **Log-based messaging (Kafka)** : les messages sont écrits dans un **log append-only** et ne sont **jamais supprimés** après lecture. Chaque consommateur maintient son propre offset
- Pourquoi Kafka est différent des queues classiques : les messages peuvent être relus, plusieurs groupes de consommateurs indépendants, le log est la source de vérité
- **Throughput** de Kafka : écriture séquentielle sur disque → très rapide

---

## ✏️ Exercices (15 min)

### Ex 1 — Queue vs Log-based : tableau (7 min)

| | Queue classique (RabbitMQ) | Log-based (Kafka) |
|-|---------------------------|-------------------|
| Message consommé par | 1 seul consommateur | |
| Message supprimé après lecture | Oui | |
| Plusieurs groupes de consommateurs | Difficile | |
| Relecture des anciens messages | Non | |
| Ordre des messages | Par queue | |
| Cas d'usage idéal | | |

### Ex 2 — L'offset Kafka (5 min)
Kafka stocke l'offset du consommateur. Dans `notes.md`, explique :
- Qu'est-ce qu'un offset ?
- Qui gère l'offset : Kafka ou le consommateur ?
- Que se passe-t-il si un consommateur plante et repart depuis l'offset précédent ?
- Que se passe-t-il si un consommateur repart depuis l'offset 0 (replay complet) ?

### Ex 3 — Kafka dans ton stack (3 min)
Tu utilises Kafka. Maintenant que tu lis Ch.11, y a-t-il un comportement de Kafka que tu comprends différemment ?  
Exemple : pourquoi as-tu besoin de plusieurs partitions pour paralléliser la consommation ?

---

## ✅ Terminé quand

- [ ] Lecture (messagerie + Kafka log-based) terminée
- [ ] Vérification des prédictions faite
- [ ] Ex 1 (tableau queue vs log-based) fait
- [ ] Ex 2 (offset Kafka) expliqué
- [ ] Ex 3 (Kafka dans ton stack) fait
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.11 — Databases and Streams : Change Data Capture (CDC), Event Sourcing — les bases de données comme sources d'événements.
