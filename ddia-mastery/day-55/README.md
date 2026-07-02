# Jour 55 — Synthèse DDIA 1/2 : Parties I et II

🔁 Grande synthèse · ~60 min · Pas de nouvelle lecture

---

## 🎯 Objectif du jour

Reconstruire de mémoire l'ensemble des Parties I et II en une session. C'est le test de compréhension le plus exigeant — et le plus utile.

---

## ✏️ Exercices (60 min)

### Ex 1 — La grande carte mentale DDIA (25 min)

Ferme tout. Dans `notes.md`, construis de mémoire une vue complète :

```
DDIA — Partie I : Un seul noeud
├── Ch.1 : ___ (3 préoccupations) → ___, ___, ___
├── Ch.2 : ___ (3 modèles) → ___, ___, ___
├── Ch.3 : ___ (2 familles d'index) → ___ vs ___ + OLTP vs ___
└── Ch.4 : ___ (4 formats) → ___, ___, ___, ___

DDIA — Partie II : Plusieurs noeuds
├── Ch.5 : ___ (3 modèles) → ___, ___, ___
│          (3 anomalies de lag) → ___, ___, ___
├── Ch.6 : ___ (2 stratégies) → ___ vs ___
│          (2 types d'index secondaires) → ___ vs ___
├── Ch.7 : ___ (4 niveaux d'isolation)
│          (6 anomalies) → ___, ___, ___, ___, ___, ___
│          (2 implémentations sérialisables) → ___ vs ___
├── Ch.8 : ___ (3 familles de problèmes) → ___, ___, ___
└── Ch.9 : ___ (3 concepts clés) → ___, ___, ___
```

Remplis les blancs. Si tu bloques sur quelque chose, coche-le comme lacune.

### Ex 2 — Le fil rouge : le compromis fondamental (15 min)

DDIA est construit autour d'un compromis omniprésent.  
Dans `notes.md`, explique comment ce compromis apparaît dans chaque chapitre :

| Chapitre | Compromis principal |
|---------|---------------------|
| Ch.1 | Reliability vs Cost |
| Ch.2 | Flexibilité vs Consistance du schéma |
| Ch.3 | Vitesse lecture vs Vitesse écriture (LSM vs B-Tree) |
| Ch.4 | Lisibilité vs Performance (JSON vs binaire) |
| Ch.5 | |
| Ch.6 | |
| Ch.7 | |
| Ch.8 | |
| Ch.9 | |

### Ex 3 — 3 systèmes, 9 chapitres (10 min)

Pour chacun des 3 systèmes, identifie dans `notes.md` quels chapitres sont les plus critiques pour comprendre son comportement et pourquoi :

**Cassandra :**
Chapitres critiques : Ch.___, Ch.___, Ch.___
Pourquoi :

**Kafka :**
Chapitres critiques : Ch.___, Ch.___, Ch.___
Pourquoi :

**Postgres avec réplication :**
Chapitres critiques : Ch.___, Ch.___, Ch.___
Pourquoi :

### Ex 4 — Vérification rapide (10 min)

Ouvre n'importe quel Summary (Ch.5, Ch.7, ou Ch.9 — au choix).  
Vérifie 5 points de ta carte mentale. Note ce qui était incorrect.

---

## ✅ Terminé quand

- [ ] Grande carte mentale Partie I+II complète
- [ ] Tableau des compromis par chapitre complété
- [ ] 3 systèmes → chapitres critiques identifiés
- [ ] Vérification rapide faite
- [ ] Coché dans PROGRESS.md

## → Demain
Synthèse DDIA 2/2 — Partie III + vue globale de tout le livre.
