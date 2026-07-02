# Mes notes — Jour 57 (Conception : détection de fraude)

## Partie 1 — Architecture globale

```
Transaction entrante
    ↓
[Composant A : ___ ]
    ↓
[Composant B : ___ ]
    ↓
Décision : APPROVE / BLOCK
    ↓
[Composant C : ___ ]
```

---

## Partie 2 — Partitionnement

1. Hash par card_id ou range par timestamp → choix :
   Raison :

2. Problème si Beyoncé utilise sa carte 1000x/s :

3. Solution au hot spot :

---

## Partie 3 — Fenêtres temporelles

1. Type de fenêtre choisi :

2. Transaction en retard de 10 min :

3. Stockage de l'état « 60 dernières minutes » :

---

## Partie 4 — Cohérence et transactions

1. Eventual consistency pour la fraude — acceptable ? :

2. Idempotence (message Kafka reçu 2x) :

3. Si service de détection en panne → :

---

## Partie 5 — Tolérance aux pannes

1. Noeud qui tombe :

2. RocksDB corrompu — reconstruction :

3. Pire scénario + atténuation :

