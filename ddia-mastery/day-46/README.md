# Jour 46 — 🔁 Revue Ch.10 + Prédictions Ch.11

🔁 Rappel actif + transition · ~60 min

---

## 🎯 Objectif du jour

Consolider Ch.10 et préparer mentalement Ch.11 (Stream Processing). Le batch et le stream sont complémentaires — Ch.11 répondra à la question : que faire quand on ne peut pas attendre d'avoir toutes les données ?

---

## ✏️ Exercices (60 min)

### Ex 1 — Page blanche Ch.10 (20 min)

Ferme tout. Dans `notes.md`, retrouve de mémoire :

**Philosophie batch processing :**
- Inputs immuables (pourquoi important ?)
- Outputs déterministes (pourquoi utile ?)
- Fault tolerance via retry (comment ça marche ?)

**MapReduce :**
- Phases Map → Shuffle → Reduce (résumé en 3 lignes)
- Sort-merge join vs broadcast hash join : quand ?
- Problème principal de MapReduce vs Spark

**Spark / Dataflow engines :**
- DAG à la place du Map→Reduce séquentiel
- Pourquoi plus rapide que MapReduce
- Fault tolerance différente

### Ex 2 — 5 questions flash Ch.10 (15 min)

Réponds sans aide :

1. Quelle est la différence entre un **job batch** et une **requête SQL** en termes d'architecture ?
2. Pourquoi MapReduce écrit-il les sorties intermédiaires sur HDFS et quel problème ça crée ?
3. Qu'est-ce qu'un sort-merge join ? Quel est son coût en réseau ?
4. Pourquoi la philosophie « inputs immuables + outputs en lecture seule » rend-elle le batch processing plus simple que les mises à jour en base ?
5. Quel est le lien conceptuel entre les pipes Unix (`|`) et les DAGs de Spark ?

### Ex 3 — Connexion avec ton stack (10 min)

Tu utilises Spark dans ton travail. Dans `notes.md`, réponds :

- Quels jobs Spark tu as écrits ou vus sont du **batch processing pur** (lire des données historiques, produire une sortie) ?
- Est-ce que tu utilises des checkpoints dans tes jobs ? Si oui, pourquoi ? Si non, que se passe-t-il en cas de panne ?
- Dans ton expérience, quel est le goulot d'étranglement le plus fréquent dans un job Spark (shuffle ? I/O ? mémoire ?)

### Ex 4 — Prédictions Ch.11 (15 min)

Ch.11 traite du **stream processing** — traiter les données **en temps réel** au fur et à mesure qu'elles arrivent.  
Dans `notes.md`, réponds AVANT de lire Ch.11 :

1. Quelle est la différence fondamentale entre batch et stream processing ?
2. Tu connais Kafka. En quoi Kafka est-il au cœur du stream processing ?
3. Qu'est-ce qu'une **fenêtre de temps** (time window) dans le traitement en flux ? Donne un exemple.
4. Comment gère-t-on un événement qui **arrive en retard** dans un stream ? (Ex : un log qui arrive 5 min après son timestamp)

---

## ✅ Terminé quand

- [ ] Page blanche Ch.10 (3 sections) complète
- [ ] 5 questions flash répondues
- [ ] Connexion Spark et ton stack faite
- [ ] Prédictions Ch.11 notées (4 questions)
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.11 — Stream Processing : systèmes de messagerie, Kafka, event sourcing, change data capture.
