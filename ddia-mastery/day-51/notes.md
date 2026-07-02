# Mes notes — Jour 51

## Prédictions (avant lecture)

1. 

2. 

3. 

---

## Ex 1 — Pipeline 4 datastores

```
Application → Postgres
                 ↓ CDC
           Kafka
           ↙       ↓       ↘
   OpenSearch   Redis   Spark DWH
```

Retard 2s OpenSearch — problème pour :

Reconstruction depuis Kafka 7j → 

Différence avec 2PC :

---

## Ex 2 — Vues dérivées reconstructibles (3 phrases)


---

## Ex 3 — Connexion Ch.9 + Ch.12 (2 phrases)


---

## Autres notes


