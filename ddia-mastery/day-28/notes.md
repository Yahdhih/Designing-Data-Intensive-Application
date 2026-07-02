# Mes notes — Jour 28

## Prédictions (avant lecture)

1. 

2. 

3. 

---

## Ex 1 — Non-repeatable read : la sauvegarde

```
T1 (backup)                     T2 (virement)
BEGIN
SELECT compte_A → 500
                                UPDATE compte_A = 400
                                UPDATE compte_B = 600
                                COMMIT
SELECT compte_B → 600
```

Problème :

Snapshot Isolation résout ça comment :

---

## Ex 2 — MVCC : quelle version voit tx_id=6 ?

Version vue : 
Raison :

---

## Ex 3 — VACUUM Postgres


---

## Autres notes


