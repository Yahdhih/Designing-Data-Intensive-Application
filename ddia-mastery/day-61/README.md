# Jour 61 — Conception finale : pipeline de données à grande échelle

🛠️ Conception système · ~60 min · Feuille blanche

---

## 🎯 Objectif du jour

Le dernier grand exercice de conception. Cette fois, tu pars d'une description vague (comme en entretien) et tu construis tout.

---

## 🛠️ Problème : Analytics Platform pour une plateforme musicale

### Description (intentionnellement vague)

Tu rejoins une startup qui fait du streaming musical (type Spotify, 50M d'utilisateurs actifs).  
Le CTO te dit :

> « On veut pouvoir répondre à ces questions en temps réel et en historique :
> - Quels sont les 100 artistes les plus écoutés en ce moment (dernières 15 min) ?
> - Quel est le nombre total d'écoutes par utilisateur ce mois-ci ?
> - Si un artiste est signalé comme inapproprié, on veut supprimer ses écoutes de toutes les statistiques sous 1 heure.
> Le système doit gérer 100K écoutes/seconde aux heures de pointe. »

---

## ✏️ Exercices (60 min)

### Partie 1 — Clarification des contraintes (10 min)

Avant de concevoir, identifie dans `notes.md` :
1. Les **3 cas d'usage** à traiter (temps réel, historique, suppression)
2. Les **contraintes de latence** pour chaque cas
3. Les **contraintes de cohérence** (est-ce que le top 100 doit être exact ou approximatif ?)
4. Le **volume** à absorber : 100K events/s × 3600s × 24h = combien de Go/jour ?

### Partie 2 — Architecture (20 min)

Dans `notes.md`, propose une architecture en décrivant :

1. **Ingestion** : comment captureras-tu les 100K écoutes/seconde ?
2. **Traitement temps réel** : comment calculeras-tu le top 100 des 15 dernières minutes ?
3. **Stockage historique** : comment stockeras-tu les données pour les requêtes mensuelles ?
4. **Suppression d'artiste** : comment implementeras-tu la suppression dans tous les systèmes en < 1h ?

Cite des technologies concrètes et les chapitres DDIA qui justifient tes choix.

### Partie 3 — Les compromis (15 min)

Pour chaque choix technique, identifie dans `notes.md` le compromis principal :

| Choix | Avantage | Compromis | Chapitre DDIA |
|-------|---------|----------|--------------|
| Kafka pour l'ingestion | | | |
| Flink pour temps réel | | | |
| Parquet sur S3 pour historique | | | |
| Redis pour le top 100 | | | |
| CDC pour la suppression | | | |

### Partie 4 — La question difficile (15 min)

> « On veut que le top 100 soit exact (pas approximatif). Est-ce possible à 100K events/s ? »

Dans `notes.md` :
1. Pourquoi c'est difficile (lien avec Ch.8 et Ch.9) ?
2. Propose une solution exacte et estime son coût en ressources
3. Propose une solution approximative (HyperLogLog, Count-Min Sketch) et son erreur acceptable

---

## ✅ Terminé quand

- [ ] Contraintes clarifiées (Partie 1)
- [ ] Architecture proposée avec technologies (Partie 2)
- [ ] Tableau des compromis complété (Partie 3)
- [ ] Question difficile (top 100 exact) traitée (Partie 4)
- [ ] Coché dans PROGRESS.md

## → Demain
Avant-dernier jour : retour sur Ch.1 — relire le premier chapitre après avoir lu tout le livre.
