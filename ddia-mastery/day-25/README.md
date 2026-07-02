# Jour 25 — Exercice de conception + 🔁 Revue Ch.6

🛠️ Conception + rappel actif · ~20 min conception + 40 min revue

---

## 🎯 Objectif du jour

Pas de nouvelle lecture — consolider Ch.6 par un exercice de conception concret, puis page blanche complète.

---

## 🛠️ Exercice de conception (20 min)

### Contexte : système de logs distribué

Tu dois concevoir le partitionnement pour un système de logs (type Kafka ou un stockage de logs centralisé) :
- **Volume :** 10 millions d'événements/minute
- **Accès typiques :**
  - Écriture : logs en continu, clé = `service_id + timestamp`
  - Lecture 1 : « Tous les logs du service X entre 14h et 15h » (lecture de plage temporelle)
  - Lecture 2 : « Tous les logs de niveau ERROR dans la dernière heure » (tous services)
  - Lecture 3 : « Quel est l'événement 42_abc_123 ? » (accès par ID exact)
- **Infrastructure :** 10 noeuds, tu peux en ajouter

Dans `notes.md`, réponds :

**Q1.** Quel type de partitionnement choisirais-tu pour la clé primaire (`service_id + timestamp`) ?  
Range ou hash ? Justifie en 2-3 phrases avec les concepts de Ch.6.

**Q2.** Pour la Lecture 2 (tous les logs ERROR), as-tu besoin d'un index secondaire ? Si oui, local ou global ? Pourquoi ?

**Q3.** Si tu ajoutes 5 noeuds supplémentaires en cours de route, quelle stratégie de rééquilibrage utiliserais-tu et pourquoi ?

**Q4.** Comment un client sait-il sur quel noeud envoyer sa requête ? Décris le mécanisme de routage que tu choisirais.

---

## 🔁 Revue Ch.6 — Page blanche (40 min)

### Partie 1 — Rappel sans aide (20 min)

Ferme tout. Dans `notes.md`, reproduis de mémoire :

```
Ch.6 — Partitionnement
├── Pourquoi partitionner ?
├── Partitionnement par clé
│   ├── Range partitioning : mécanisme + avantage + problème
│   └── Hash partitioning : mécanisme + avantage + problème
├── Index secondaires
│   ├── Local (scatter-gather) : lecture + écriture
│   └── Global (term-partitioned) : lecture + écriture
├── Rééquilibrage
│   ├── Stratégie 1 :
│   ├── Stratégie 2 :
│   └── Stratégie 3 :
└── Routage des requêtes
    ├── Option 1 :
    ├── Option 2 :
    └── Option 3 :
```

### Partie 2 — Vérification (10 min)

Ouvre le Summary de Ch.6 et compare. Note les lacunes.

### Partie 3 — Connexion Ch.5 → Ch.6 (10 min)

Dans `notes.md`, réponds :  
Ch.5 = réplication. Ch.6 = partitionnement.  
Ces deux techniques s'utilisent **ensemble** dans tout système distribué réel.  
Comment sont-elles combinées dans Cassandra ? Dans Kafka ?

---

## ✅ Terminé quand

- [ ] Exercice de conception (4 questions) fait
- [ ] Page blanche Ch.6 complète
- [ ] Vérification + lacunes notées
- [ ] Connexion Ch.5 + Ch.6 expliquée
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.7 — Transactions : ACID, pourquoi les bases de données ont besoin de transactions, le concept fondamental.
