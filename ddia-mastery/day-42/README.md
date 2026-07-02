# Jour 42 — 🔁 Revue globale : Partie I + Partie II

🔁 Grande synthèse · ~60 min

---

## 🎯 Objectif du jour

Tu as lu 9 chapitres de DDIA. Ce jour est une **synthèse totale** : reconstruire le raisonnement de tout le livre jusqu'ici en une seule vue.

---

## ✏️ Exercices (60 min)

### Ex 1 — La grande carte mentale (20 min)

Ferme tout. Dans `notes.md`, construis de mémoire une carte des chapitres :

```
DDIA — Partie I : Fondations
├── Ch.1 : Reliability, Scalability, Maintainability
│   ├── [3 concepts clés]
├── Ch.2 : Modèles de données
│   ├── [3 modèles]
├── Ch.3 : Stockage
│   ├── [LSM vs B-Tree + OLTP vs OLAP]
└── Ch.4 : Encodage
    └── [JSON vs binaire + backward/forward compat]

DDIA — Partie II : Données distribuées
├── Ch.5 : Réplication
│   ├── [3 modèles + 3 anomalies lag]
├── Ch.6 : Partitionnement
│   ├── [range vs hash + index secondaires]
├── Ch.7 : Transactions
│   ├── [ACID + 4 niveaux isolation + 6 anomalies]
├── Ch.8 : Problèmes distribués
│   ├── [réseau + horloges + processus]
└── Ch.9 : Consensus
    └── [linearizability + TOB + Raft + 2PC]
```

Remplis les crochets [...] avec les points clés.

### Ex 2 — La question « pourquoi » pour chaque chapitre (15 min)

Pour chaque chapitre, réponds « Pourquoi ce chapitre existe-t-il dans le livre ? » en 1 phrase :

- Ch.1 : « Ce chapitre définit... »
- Ch.2 : « Ce chapitre explique... »
- Ch.3 : « Ce chapitre révèle... »
- Ch.4 : « Ce chapitre prépare... »
- Ch.5 : « Ce chapitre introduit... »
- Ch.6 : « Ce chapitre résout... »
- Ch.7 : « Ce chapitre outille... »
- Ch.8 : « Ce chapitre brise... »
- Ch.9 : « Ce chapitre répond... »

### Ex 3 — Le compromis universel (15 min)

Kleppmann revient souvent sur un compromis fondamental.  
Dans `notes.md`, explique en 5 phrases le compromis central qui traverse tous les chapitres :

- **Consistance vs Performance** : pourquoi ne peut-on pas avoir les deux ?
- **Disponibilité vs Cohérence** : (théorème CAP) — dans quelles situations choisit-on quoi ?
- **Simplicité vs Flexibilité** : pourquoi les modèles de données moins flexibles sont-ils souvent plus rapides ?

### Ex 4 — Ce que je suis capable de faire maintenant (10 min)

Dans `notes.md`, liste 5 choses concrètes que tu peux faire maintenant que tu n'aurais pas pu faire avant de lire ces 9 chapitres :

1. 
2. 
3. 
4. 
5. 

---

## ✅ Terminé quand

- [ ] Grande carte mentale (Partie I + II) construite de mémoire
- [ ] « Pourquoi » de chaque chapitre en 1 phrase
- [ ] Compromis universel expliqué en 5 phrases
- [ ] 5 compétences nouvelles identifiées
- [ ] Coché dans PROGRESS.md

## → Demain (Jour 43)
Ch.10 — Batch Processing : MapReduce, Spark, le paradigme du traitement par lots. La Partie III commence.
