# Mes notes — Jour 21

## Prédictions pour le Summary de Ch.5


---

## Ex 1 — Page blanche Ch.5

**Single-leader :**

Anomalies de replication lag :
1. 
2. 
3. 

**Multi-leader :**

**Leaderless :**

---

## Ex 2 — 5 questions de compréhension

1. 

2. 

3. 

4. 

5. 

---

## Ex 3 — Schéma des 3 architectures

```
Single-leader :
  Client (write) → [LEADER] → [F1] [F2] [F3]

Multi-leader :
  Client (write) → [LEADER 1] ←→ [LEADER 2]
                      ↓                ↓
                  [F1][F2]         [F3][F4]

Leaderless :
  Client (write) → [N1][N2][N3][N4][N5]
                   (w=3 : attend 3 confirmations)
```

Mes annotations :

---

## Autres notes


