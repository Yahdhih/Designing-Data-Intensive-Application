# code/99-capstone/ — Projet de synthèse

> Jours 113-119 · `PLAN.md` Phase 4

---

## Objectif

Concevoir et implémenter partiellement un **store clé-valeur distribué** qui synthétise toutes les parties du livre :

```
┌─────────────────────────────────────────────────────────────┐
│                    KV Store Distribué                        │
│                                                             │
│  Couche client                                              │
│    ↓ get(key) / set(key, value)                             │
│  Routage (hachage cohérent)  ←── Partitionnement (Ch.6)    │
│    ↓                                                        │
│  Nœud leader (Raft)          ←── Consensus (Ch.9)          │
│    ↓                                                        │
│  WAL + Storage (LSM-tree)    ←── Stockage (Ch.3)           │
│    ↓ réplication                                            │
│  Nœuds répliques             ←── Réplication (Ch.5)        │
│    ↓ CDC                                                    │
│  Flux d'événements           ←── Stream (Ch.11)            │
└─────────────────────────────────────────────────────────────┘
```

---

## Livrable

1. **Document de conception** (`design_doc.md`) incluant :
   - Paramètres de charge (load parameters) choisis
   - Architecture choisie et alternatives rejetées
   - Matrices de compromis pour chaque décision majeure
   - Modes de défaillance et stratégies de tolérance

2. **Prototype partiel** :
   - Routage par hachage cohérent (`consistent_hash.py` de Ch.6)
   - Storage LSM simplifié (`lsm.py` de Ch.3)
   - Réplication via log repliqué (emprunté à `raft_sim.py` de Ch.9)
   - CDC : émettre les changements comme événements (de `cdc_wal.py` de Ch.11)

---

## Exercices « Conçois X » complémentaires (Jours 120-123)

### « Conçois un raccourcisseur d'URL »
- Volume : 100M URLs · 10B lectures/jour
- Quel stockage ? Quel partitionnement ? Quelle cohérence ?

### « Conçois un fil d'actualité »
- Fan-out faible (read-time computation) vs fan-out fort (write-time fan-out)
- Quel seuil de basculement ? Pourquoi Twitter hybride ?

### « Conçois un système de paiement idempotent »
- Exactement-une-fois · idempotence · transactions distribuées
- 2PC ou sagas ? Quel compromis ?

---

## Critère « terminé »

- [ ] `design_doc.md` rempli (au moins 2 pages, matrices de compromis incluses)
- [ ] Prototype : routing + storage + réplication de base fonctionnelle
- [ ] 3 exercices « Conçois X » documentés dans `reference/notes/`
- [ ] Tu peux expliquer chaque décision architecturale avec le vocabulaire DDIA
