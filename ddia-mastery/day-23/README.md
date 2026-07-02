# Jour 23 — Ch.6 : Index secondaires partitionnés

📖 Lecture · ~45 min de lecture + 15 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 6, section « Partitioning and Secondary Indexes »

Un index secondaire permet de chercher par autre chose que la clé primaire (ex : chercher des voitures par couleur, alors que la clé est l'ID). Comment gérer ces index quand les données sont partitionnées ? Kleppmann présente deux approches opposées.

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, réponds AVANT d'ouvrir le livre :

1. Si tes voitures sont partitionnées par ID (ID 1-1000 sur noeud 1, 1001-2000 sur noeud 2...) et que tu veux trouver toutes les voitures rouges — comment ferais-tu ?
2. Quelle est la différence entre un index **local** (par partition) et un index **global** (sur toutes les données) selon ton intuition ?
3. Qu'est-ce qui coûte plus cher : une lecture sur tous les noeuds, ou une écriture sur plusieurs noeuds ?

---

## 📚 Points à remarquer pendant la lecture

- **Index secondaire local (document-partitioned)** :
  - Chaque partition maintient son propre index pour ses données locales
  - Lecture = interroger TOUTES les partitions + fusionner les résultats (**scatter-gather**)
  - Écriture = simple (1 seule partition concernée)
- **Index secondaire global (term-partitioned)** :
  - L'index est lui-même partitionné (ex : couleurs A-M sur noeud 1, N-Z sur noeud 2)
  - Lecture = interroger 1 seule partition de l'index (efficace)
  - Écriture = mettre à jour potentiellement PLUSIEURS partitions d'index (coûteux)
- Les systèmes réels : Elasticsearch → local, DynamoDB → les deux, Cassandra → local

---

## ✏️ Exercices (15 min)

### Ex 1 — Tableau comparatif (7 min)

| | Index local (scatter-gather) | Index global (term-partitioned) |
|-|------------------------------|--------------------------------|
| Écriture (coût) | | |
| Lecture (coût) | | |
| Cohérence de l'index | | |
| Utilisé par | | |

### Ex 2 — OpenSearch et les index (5 min)
Tu utilises OpenSearch. OpenSearch est basé sur Elasticsearch, qui utilise des index **locaux**.  
Maintenant que tu comprends Ch.6 :
- Quand tu fais un `search` sur OpenSearch, que se passe-t-il sur les shards ?
- Pourquoi OpenSearch appelle ça « scatter-gather » ?
- Quel est l'impact sur la latence si tu as 20 shards vs 3 shards ?

### Ex 3 — Choix de conception (3 min)
Tu dois concevoir un catalogue de produits e-commerce partitionné sur 10 noeuds.  
Les utilisateurs cherchent souvent par catégorie et par prix.  
Choisirais-tu un index local ou global pour l'index `catégorie + prix` ? Justifie en 3 phrases.

---

## ✅ Terminé quand

- [ ] Lecture (index secondaires partitionnés) terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (tableau comparatif) fait
- [ ] Ex 2 (OpenSearch scatter-gather) fait
- [ ] Ex 3 (choix de conception) fait
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.6 — Rééquilibrage des partitions (rebalancing) + routage des requêtes. Comment un système sait quelle donnée est sur quel noeud ?
