# Mes notes — Jour 27

## Prédictions (avant lecture)

1. 

2. 

3. 

---

## Ex 1 — Diagramme dirty read

```
T1 (virement)          T2 (affichage solde)
BEGIN
UPDATE compte_A = 500
UPDATE compte_B = 1500
                       SELECT compte_A → 
                       SELECT compte_B → 
ROLLBACK
```

Problème si T2 lit avant ROLLBACK :

---

## Ex 2 — Dirty write : la voiture


---

## Ex 3 — Mécanisme de Postgres (ancienne valeur pendant écriture)


---

## Autres notes


