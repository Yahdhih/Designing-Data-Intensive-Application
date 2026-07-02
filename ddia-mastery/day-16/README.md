# Jour 16 — 🔁 Revue Semaine 3 (Ch.3 + Ch.4)

🔁 Rappel actif + connexions · ~60 min

---

## 🎯 Objectif du jour

Consolider Ch.3 et Ch.4 ensemble et voir comment ils se connectent. Ch.3 = comment stocker, Ch.4 = comment sérialiser. Les deux sont nécessaires pour comprendre la Partie II qui arrive.

---

## ✏️ Exercices (60 min)

### Ex 1 — Questions flash Ch.3 (15 min)

Réponds dans `notes.md` sans aide :

1. Quelle est la différence entre un index LSM-Tree et un B-Tree en termes de **writes** ?
2. Qu'est-ce que le « write amplification » ? Quel index en souffre le plus ?
3. Pourquoi Cassandra (LSM) est-il préféré pour les workloads write-heavy ?
4. Qu'est-ce qu'un data warehouse ? Comment les données y arrivent-elles ?
5. Pourquoi le stockage orienté colonnes compresse-t-il mieux ?

### Ex 2 — Questions flash Ch.4 (15 min)

Réponds dans `notes.md` sans aide :

1. Quelle est la différence entre backward compatibility et forward compatibility ?
2. Pourquoi Protobuf utilise des **field tags** plutôt que des noms de champs ?
3. Comment Avro gère-t-il la compatibilité sans field tags ?
4. Dans quel mode de flux de données (BDD / service / message) est-il le plus facile de faire évoluer les schémas ?
5. Qu'est-ce qu'un Schema Registry et pourquoi Kafka en a-t-il besoin avec Avro ?

### Ex 3 — Connexion Ch.3 + Ch.4 (15 min)

Réponds dans `notes.md` :

Imagine un pipeline : **Kafka → Spark → Parquet → Postgres**

Pour chaque flèche, explique :
- Quel format d'encodage est utilisé typiquement (et pourquoi) ?
- Quelle structure de stockage est utilisée (et pourquoi) ?

### Ex 4 — Préparation Ch.5 (15 min)

Ch.5 traite de la **réplication** — copier les données sur plusieurs machines.  
Dans `notes.md`, préds :
1. Pourquoi voudrait-on copier les données sur plusieurs machines ?
2. Quels problèmes ça crée (consistency, latence, conflits...) ?
3. Si tu avais 3 serveurs avec les mêmes données et qu'un client écrit sur le serveur 1 — comment les serveurs 2 et 3 sont-ils mis à jour ?

---

## ✅ Terminé quand

- [ ] 5 questions flash Ch.3 répondues
- [ ] 5 questions flash Ch.4 répondues
- [ ] Connexion pipeline Kafka→Spark→Parquet→Postgres expliquée
- [ ] Prédictions Ch.5 notées
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.5 — Réplication : comment copier les données sur plusieurs serveurs ? Single-leader replication.
