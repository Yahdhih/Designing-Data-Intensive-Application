# Jour 07 — Ch.2 : Modèles en graphe + Résumé Ch.2

📖 Lecture + consolidation · ~35 min lecture + 25 min consolidation

---

## 📖 Lecture du jour

**Section :** Chapitre 2, section « Graph-Like Data Models » jusqu'à la fin + « Summary »

Les modèles en graphe sont utilisés quand les **relations entre les données** sont aussi importantes que les données elles-mêmes. Kleppmann présente le property graph, RDF/SPARQL, et Datalog.

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, réponds AVANT d'ouvrir le livre :

1. Donne un exemple de données où le graphe est plus naturel que le relationnel (hints : réseaux sociaux, routes, connaissances...)
2. Tu as entendu parler de Neo4j ? Qu'est-ce que tu sais sur les bases de données graphe ?
3. Quelle est la différence entre un graphe orienté et non-orienté ? Et quand choisit-on l'un ou l'autre ?

---

## 📚 Points à remarquer pendant la lecture

- Le **property graph** : noeuds + arêtes, chacun avec des propriétés arbitraires
- Pourquoi le graphe permet des requêtes **récursives** (ex : trouver tous les amis d'amis) plus naturellement que le SQL avec jointures récursives
- **RDF (Resource Description Framework)** — triple-store : (sujet, prédicat, objet) — c'est le web sémantique
- **SPARQL** vs **Cypher** — deux langages, même idée de pattern matching sur graphes
- **Datalog** — un langage logique (ancêtre de Prolog) pour les requêtes récursives

---

## ✏️ Exercices — Consolidation Ch.2 (25 min)

### Ex 1 — Résumé global Ch.2 (10 min)
Page blanche : liste les **3 modèles de données** que Kleppmann couvre dans Ch.2, avec pour chacun :
- Son nom
- Sa structure principale
- 1 cas d'usage typique
- 1 limite principale

### Ex 2 — Tableau des modèles (10 min)

| Modèle | Structure | Requêtes | Cas d'usage idéal |
|--------|-----------|----------|-------------------|
| Relationnel | Tables, clés étrangères | SQL | |
| Document | JSON/BSON imbriqué | | |
| Graphe | Noeuds + arêtes | Cypher/SPARQL | |

### Ex 3 — Question ouverte (5 min)
Kleppmann couvre 3 modèles, mais il en existe d'autres (time-series, vector, clé-valeur...).  
Selon toi, pourquoi y a-t-il autant de modèles différents ? Quel problème chaque modèle résout-il que les autres ne peuvent pas résoudre ?

---

## ✅ Terminé quand

- [ ] Lecture des modèles en graphe + Summary Ch.2 terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (résumé 3 modèles) fait
- [ ] Ex 2 (tableau comparatif) fait
- [ ] Ex 3 (question ouverte) répondu
- [ ] Coché dans PROGRESS.md

## → Demain
Revue semaine 1 : rappel actif complet de Ch.1 + Ch.2. Pas de nouvelle lecture.
