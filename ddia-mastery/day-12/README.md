# Jour 12 — Ch.3 : OLTP vs OLAP + Stockage Colonne

📖 Lecture · ~40 min de lecture + 20 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 3, sections « Transaction Processing or Analytics? » + « Data Warehousing » + « Column-Oriented Storage » + « Summary »

La deuxième moitié de Ch.3 traite d'un changement de perspective : non plus *comment* stocker les données, mais *pour quoi* — les workloads transactionnels (OLTP) vs analytiques (OLAP) ont des besoins radicalement différents.

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, réponds AVANT d'ouvrir le livre :

1. Tu utilises Spark pour de l'analytique. Quelle est selon toi la différence entre une requête transactionnelle (ex : « quel est le solde du compte 42 ? ») et une requête analytique (ex : « quel est le montant total des transactions en janvier ? »)
2. Pourquoi aurait-on besoin d'une base de données séparée pour l'analytique, plutôt d'utiliser la même base de production ?
3. Qu'est-ce que le stockage orienté colonnes selon toi ? Pourquoi ce serait utile pour l'analytique ?

---

## 📚 Points à remarquer pendant la lecture

- La définition précise de **OLTP** (Online Transaction Processing) vs **OLAP** (Online Analytical Processing)
- Le **Data Warehouse** : copie séparée des données de production, optimisée pour l'analyse
- **ETL** (Extract-Transform-Load) — comment les données passent de la prod au warehouse
- Le modèle en étoile (**star schema**) : table de faits + tables de dimensions
- **Stockage orienté colonnes** : pourquoi stocker toutes les valeurs d'une colonne ensemble améliore la compression et l'analytique
- **Compression par colonne** : run-length encoding, bitmap encoding — pourquoi ça marche bien sur les colonnes

---

## ✏️ Exercices (20 min)

### Ex 1 — Tableau OLTP vs OLAP (8 min)

| Caractéristique | OLTP | OLAP |
|----------------|------|------|
| Type de requête | | |
| Données lues | quelques lignes | |
| Données écrites | | |
| Utilisateurs | | |
| Taille BDD | | |
| Exemples | MySQL, Postgres | |

### Ex 2 — Pourquoi les colonnes pour l'analytique (7 min)
Imagine une table avec 100 colonnes et 1 milliard de lignes. Une requête analytique typique lit **5 colonnes**.  
Explique pourquoi le stockage orienté colonnes est **10x plus rapide** que le stockage orienté lignes pour ce cas.

### Ex 3 — Connexion Spark (5 min)
Tu utilises Spark avec des fichiers Parquet. Parquet est un format de stockage orienté colonnes.  
Grâce à Ch.3, explique maintenant pourquoi Parquet est le format recommandé pour Spark analytique.

---

## ✅ Terminé quand

- [ ] Lecture (OLTP/OLAP + data warehouse + stockage colonne + Summary) terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (tableau OLTP vs OLAP) complété
- [ ] Ex 2 (pourquoi colonnes) expliqué
- [ ] Ex 3 (connexion Spark/Parquet) fait
- [ ] Coché dans PROGRESS.md

## → Demain
Revue Ch.3 — rappel actif complet du chapitre le plus dense de la Partie I.
