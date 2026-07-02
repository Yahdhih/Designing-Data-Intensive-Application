# Mes notes — Jour 31

## Prédictions (avant lecture)

1. 

2. 

3. 

---

## Ex 1 — 2PL vs SSI

| | Two-Phase Locking | SSI |
|--|------------------|-----|
| Approche | Pessimiste | Optimiste |
| Verrous ? | Oui | |
| Deadlocks ? | Oui | |
| Perfo forte contention | | |
| Retry nécessaire ? | Non | |
| Implémenté dans | | |

---

## Ex 2 — Deadlock

```
T1 : verrouille ___ → attend ___
T2 : verrouille ___ → attend ___
→ Deadlock !
```

Détection Postgres :

Conséquence :

---

## Ex 3 — Hiérarchie niveaux d'isolation

1. Read Uncommitted → empêche :
2. Read Committed → empêche en plus :
3. Snapshot Isolation → empêche en plus :
4. Serializable → empêche en plus :

---

## Autres notes


