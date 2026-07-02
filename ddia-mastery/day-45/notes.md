# Mes notes — Jour 45

## Prédictions (avant lecture)

1. 

2. 

3. 

---

## Ex 1 — MapReduce vs Spark

| | MapReduce | Spark |
|-|-----------|-------|
| Résultats intermédiaires | Écrits sur HDFS | |
| Fault tolerance | Relit HDFS | |
| Pipelining | Non | |
| Langage | Java (bas niveau) | |
| Cas idéal | | |

---

## Ex 2 — DAG Spark

```
parquet read
    ↓
filter (event_type = "purchase")
    ↓
groupBy user_id  ← shuffle ici ?
    ↓
sum(amount)
    ↓
filter total > 1000
    ↓
join df_users    ← shuffle ici ?
    ↓
parquet write
```

Opérations avec shuffle :

Opérations pipelinées sans shuffle :

---

## Ex 3 — Résumé Ch.10 (5 phrases)


---

## Autres notes


