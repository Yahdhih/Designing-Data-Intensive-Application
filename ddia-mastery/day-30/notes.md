# Mes notes — Jour 30

## Prédictions (avant lecture)

1. Mon exemple de write skew :

2. 

3. 

---

## Ex 1 — Write skew : médecins

```
T1 (Alice)                    T2 (Bob)
BEGIN SI                       BEGIN SI
n = COUNT(on_call) → 2         n = COUNT(on_call) → 2
IF n >= 2:                     IF n >= 2:
  UPDATE alice = off              UPDATE bob = off
COMMIT                         COMMIT
Résultat : 0 médecins !
```

Pourquoi SI ne protège pas :

Différence avec lost update :

Solution :

---

## Ex 2 — Phantom + salle de réunion

Pourquoi SELECT FOR UPDATE ne suffit pas :

Materializing conflicts :

---

## Ex 3 — Write skew dans mon stack


---

## Autres notes


