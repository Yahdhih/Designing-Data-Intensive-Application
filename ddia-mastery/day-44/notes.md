# Mes notes — Jour 44

## Prédictions (avant lecture)

1. 

2. 

3. 

---

## Ex 1 — 3 types de joins

| Type de join | Quand l'utiliser | Ce qui passe sur le réseau | Équivalent Spark |
|-------------|-----------------|--------------------------|-----------------|
| Sort-merge join | | | SortMergeJoin |
| Broadcast hash join | | | BroadcastHashJoin |
| Partitioned hash join | | | BucketedHashJoin |

---

## Ex 2 — Spark : critères de choix

Si df_users < 10 Mo → 

Si les deux > 10 Mo, non partitionnés de la même façon → 

Si déjà partitionnés par user_id → 

---

## Ex 3 — Hot key problem


---

## Autres notes


