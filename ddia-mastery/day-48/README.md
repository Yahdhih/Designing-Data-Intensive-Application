# Jour 48 — Ch.11 : Bases de données et streams (CDC + Event Sourcing)

📖 Lecture · ~45 min de lecture + 15 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 11, section « Databases and Streams »

Une idée puissante de Ch.11 : une **base de données** peut être vue comme un **log d'événements** — chaque écriture est un événement. Le **Change Data Capture (CDC)** extrait ce log, et **l'Event Sourcing** en fait un principe de conception. C'est le pont entre les bases de données relationnelles et le monde du streaming.

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, réponds AVANT d'ouvrir le livre :

1. Qu'est-ce que le **WAL (Write-Ahead Log)** de Postgres ? (Tu l'as vu dans Ch.3 et Ch.5). Comment Postgres utilise-t-il ce log pour la réplication ?
2. Qu'est-ce que le **Change Data Capture** selon ton intuition ? Comment Debezium (que tu connais peut-être) fonctionne-t-il ?
3. Qu'est-ce que **l'Event Sourcing** ? En quoi est-ce différent de stocker l'état courant d'une entité ?

---

## 📚 Points à remarquer pendant la lecture

- **CDC (Change Data Capture)** : lire le log de réplication d'une base (WAL de Postgres, binlog de MySQL) pour capturer chaque changement et le publier dans Kafka → les autres systèmes peuvent se mettre à jour en temps réel
- **Event Sourcing** : au lieu de stocker l'état actuel (« le compte a 500€ »), stocker l'**historique des événements** (« dépôt +100€, retrait -50€, ... »). L'état est une **vue dérivée** calculée en rejorejoignant les événements
- **Log comme source de vérité** : si on a le log complet depuis le début, on peut reconstruire n'importe quel état
- **Command vs Event** : une commande peut échouer, un événement est un fait accompli immuable
- **State stores** dans Kafka Streams : tables locales maintenues par les consumers

---

## ✏️ Exercices (15 min)

### Ex 1 — CDC avec Debezium + Kafka (7 min)

Décris dans `notes.md` le pipeline suivant :

```
Postgres (base principale)
  → WAL (replication log)
    → Debezium (connector CDC)
      → Kafka (topic "postgres.public.users")
        → Consumer A (mise à jour OpenSearch)
        → Consumer B (mise à jour cache Redis)
        → Consumer C (analytics Spark Streaming)
```

Questions :
- Si Consumer A tombe et redémarre, que se passe-t-il ? Perd-il des événements ?
- Si on ajoute Consumer D 3 mois après — peut-il rejouer tous les événements depuis le début ?
- Qu'est-ce qui se passe si Postgres fait un `UPDATE` de 1000 lignes en une seule requête ?

### Ex 2 — Event Sourcing vs état courant (5 min)

Modèle 1 (état courant) : table `accounts(id, balance)`  
Modèle 2 (event sourcing) : table `account_events(id, type, amount, timestamp)`

Pour chacun, note dans `notes.md` :
- Comment obtient-on le solde d'un compte ?
- Comment annule-t-on une transaction passée ?
- Quel est l'avantage principal de l'event sourcing ?
- Quel est son inconvénient principal ?

### Ex 3 — Log comme source de vérité (3 min)
Kleppmann dit que le log est la « source de vérité ».  
En quoi les anciens systèmes (state-machine approach) et les nouveaux (event sourcing) diffèrent-ils dans leur rapport à l'erreur et à la récupération ?

---

## ✅ Terminé quand

- [ ] Lecture (CDC + Event Sourcing) terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (pipeline CDC Debezium + Kafka) fait
- [ ] Ex 2 (event sourcing vs état courant) fait
- [ ] Ex 3 (log comme source de vérité) fait
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.11 — Traitement des streams : temps, fenêtres temporelles, watermarks, joins en flux.
