# Jour 06 — Ch.2 : Langages de requête

📖 Lecture · ~45 min de lecture + 15 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 2, section « Query Languages for Data » (SQL déclaratif, MapReduce, CSS comparaison)

Kleppmann explique pourquoi SQL est **déclaratif** (tu dis quoi, pas comment) et compare avec l'approche **impérative** (MapReduce). Il montre aussi les requêtes graphe (Cypher, SPARQL).

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, réponds AVANT d'ouvrir le livre :

1. Quelle est selon toi la différence entre un langage de requête **déclaratif** et un langage **impératif** ?
2. Tu connais Spark avec son API DataFrame. Est-ce que c'est du déclaratif ou de l'impératif selon toi ?
3. Pourquoi voudrait-on interroger des données en graphe différemment d'une base relationnelle ?

---

## 📚 Points à remarquer pendant la lecture

- La distinction **déclaratif** vs **impératif** — et l'analogie CSS que Kleppmann utilise (remarquable)
- Pourquoi l'approche déclarative permet au moteur de **choisir comment** exécuter (parallélisation, indexation) — c'est un point clé
- Comment Kleppmann montre MapReduce avec l'exemple des pingouins — suis l'exemple en détail
- La syntaxe Cypher pour les graphes — pas besoin de la mémoriser, comprends juste la **logique de pattern matching**

---

## ✏️ Exercices (15 min)

### Ex 1 — Déclaratif vs impératif (5 min)
Dans `notes.md`, écris un avantage et un inconvénient de chaque approche :

| | Avantage | Inconvénient |
|--|---------|-------------|
| Déclaratif (SQL) | | |
| Impératif (MapReduce) | | |

### Ex 2 — L'analogie CSS (5 min)
Kleppmann fait une analogie entre SQL et CSS pour illustrer le déclaratif.  
Ré-explique cette analogie dans tes propres mots. En quoi CSS est-il « déclaratif » ?

### Ex 3 — Spark et toi (5 min)
Tu utilises Spark. L'API DataFrame de Spark est-elle déclarative ou impérative ?  
Et l'API RDD ? En quoi cette distinction affecte-t-elle les performances de ton code Spark ?

---

## ✅ Terminé quand

- [ ] Lecture de la section « Query Languages » terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (tableau avantages/inconvénients) fait
- [ ] Ex 2 (analogie CSS) expliqué
- [ ] Ex 3 (Spark déclaratif/impératif) fait
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.2 — Modèles en graphe (property graph, RDF, SPARQL, Datalog) + résumé Ch.2.
