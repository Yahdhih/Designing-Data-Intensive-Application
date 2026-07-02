# Jour 49 — Ch.11 : Traitement des streams (temps, fenêtres, watermarks)

📖 Lecture · ~45 min de lecture + 15 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 11, section « Processing Streams » (opérateurs, temps, fenêtres, joins en flux)

La section la plus technique de Ch.11. Comment traiter un flux d'événements infini ? Kleppmann détaille les types de fenêtres temporelles, le problème du **temps d'événement vs temps de traitement**, et les **watermarks**.

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, réponds AVANT d'ouvrir le livre :

1. Un utilisateur clique sur une publicité à 14h00 (timestamp de l'événement), mais le log n'arrive à Kafka qu'à 14h05 (à cause d'un réseau lent). Pour calculer le nombre de clics par heure, quelle heure utilises-tu : 14h00 ou 14h05 ?
2. Qu'est-ce qu'une **fenêtre glissante** (sliding window) vs une **fenêtre tumbling** (tumbling window) ?
3. Quelle est la différence entre un **stream join** (deux flux) et un **stream-table join** (un flux + une table) ?

---

## 📚 Points à remarquer pendant la lecture

- **Event time vs Processing time** : le timestamp de l'événement vs le moment où il arrive dans le système. La différence est le **lag**
- **Fenêtres temporelles** :
  - **Tumbling window** : fenêtres fixes et non-chevauchantes (ex : toutes les 1 heure)
  - **Hopping window** : fenêtres fixes mais chevauchantes (ex : 1h, toutes les 15 min)
  - **Sliding window** : fenêtre qui glisse sur chaque événement
  - **Session window** : regroupe les événements par session d'activité (gap-based)
- **Watermarks** : signal qui dit « tous les événements avant ce timestamp sont arrivés » → quand fermer la fenêtre ?
- **Late data** : événements qui arrivent après la fermeture de leur fenêtre → ignorer ou recalculer ?
- **Stream joins** : stream-stream (les deux côtés bougent), stream-table (enrichissement)

---

## ✏️ Exercices (15 min)

### Ex 1 — Les 4 types de fenêtres (7 min)

Pour chacun, donne dans `notes.md` un cas d'usage concret :

| Type | Description | Exemple cas d'usage |
|------|------------|---------------------|
| Tumbling (1h) | Fenêtres fixes, pas de chevauchement | |
| Hopping (1h/15min) | Fenêtres fixes, chevauchantes | |
| Sliding (30 min) | Fenêtre autour de chaque événement | |
| Session (inactivité 30 min) | Regroupement par session | |

### Ex 2 — Event time vs Processing time (5 min)

Scénario : tu calcules le nombre de pages vues par heure avec Flink.  
Un événement arrive avec `event_timestamp = 14h00` mais `processing_timestamp = 14h07`.

- Sans watermark : dans quelle fenêtre tombe cet événement ?
- Avec un watermark de 5 min de délai maximal : la fenêtre 14h-15h se ferme à quelle heure de processing time ?
- Un événement arrive à 14h10 avec `event_timestamp = 13h55` — que fait le système ?

### Ex 3 — Stream join dans Kafka Streams (3 min)
Dans Kafka Streams, le **stream-table join** enrichit les événements avec des données de référence.  
Donne un exemple concret de stream-table join que tu ferais dans un pipeline de logs applicatifs.

---

## ✅ Terminé quand

- [ ] Lecture (Processing Streams : temps, fenêtres, watermarks) terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (4 types de fenêtres) fait
- [ ] Ex 2 (event time vs processing time) fait
- [ ] Ex 3 (stream join Kafka Streams) fait
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.11 — Résumé + 🔁 Revue Ch.11. Lambda architecture vs Kappa architecture.
