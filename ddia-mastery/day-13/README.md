# Jour 13 — 🔁 Revue Ch.3 (Stockage et récupération)

🔁 Rappel actif · Pas de nouvelle lecture · ~60 min

---

## 🎯 Objectif du jour

Ch.3 est le chapitre le plus dense de la Partie I. Le but aujourd'hui est de tout retrouver de mémoire et de construire un schéma mental global.

---

## ✏️ Exercices (60 min)

### Ex 1 — Arbre de rappel (20 min)

Ferme tout. Reproduis dans `notes.md` cet arbre en le remplissant de mémoire :

```
Ch.3 — Stockage et récupération
├── Index log-structured
│   ├── Hash index
│   │   ├── Mécanisme : ?
│   │   └── Limite principale : ?
│   ├── SSTables
│   │   └── Avantage vs hash index : ?
│   └── LSM-Tree
│       ├── Memtable : ?
│       ├── Compaction : ?
│       └── Utilisé par : ?
├── Index update-in-place
│   └── B-Tree
│       ├── Structure : ?
│       ├── WAL : ?
│       └── Utilisé par : ?
├── LSM vs B-Tree
│   ├── LSM meilleur pour : ?
│   └── B-Tree meilleur pour : ?
└── OLTP vs OLAP
    ├── OLTP : ?
    ├── OLAP : ?
    ├── Data Warehouse : ?
    └── Stockage colonne : ?
```

### Ex 2 — 5 questions sans aide (20 min)

Réponds de mémoire dans `notes.md` :

1. Un utilisateur fait `db.set("k", "v")` sur une base LSM-Tree. Décris étape par étape ce qui se passe physiquement.
2. Pourquoi un B-Tree écrit-il dans un WAL **avant** de modifier la page sur disque ?
3. Qu'est-ce que la « write amplification » ? Donne un ordre de grandeur pour LSM vs B-Tree.
4. Pourquoi le stockage orienté colonnes compresse-t-il mieux que le stockage orienté lignes ?
5. Quelle est la différence entre un **data warehouse** et une base de données de production ?

### Ex 3 — Vérification et lacunes (20 min)

Ouvre le livre ou tes notes et compare.  
Note dans `notes.md` :
- Ce que tu avais bien retenu
- Les 2-3 points que tu avais mal compris ou oubliés

---

## ✅ Terminé quand

- [ ] Arbre de rappel complété de mémoire
- [ ] 5 questions répondues sans aide
- [ ] Vérification faite + lacunes notées
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.4 — Encodage : JSON, XML, binaire, Thrift, Protobuf. Comment sérialiser des données pour les envoyer ou les stocker ?
