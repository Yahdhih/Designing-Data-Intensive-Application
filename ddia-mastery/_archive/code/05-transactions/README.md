# code/05-transactions/ — Transactions & isolation

> Chapitre 7 · Jours 54-55 · `PLAN.md` Phase 2

---

## `mvcc_store.py` (Jour 54)

Store clé-valeur en mémoire avec MVCC et snapshot isolation.

**Ce qu'on construit :**
- Chaque valeur stockée avec un `(txn_id, value)` → multi-versions
- `begin()` → nouvelle transaction avec un `start_txn_id`
- `read(key)` → version visible par cette transaction (start_txn_id)
- `write(key, value)` → version en attente (non encore committée)
- `commit()` → rend les écritures visibles
- `abort()` → annule les écritures

**Jalons :**
```
Jalon 1 : store mono-version basique
Jalon 2 : multi-versions + snapshot (lecture de la version au moment de begin())
Jalon 3 : détection de write skew (vérifier qu'aucune autre txn a modifié les données lues)
```

**Lancer :**
```bash
pytest code/05-transactions/test_mvcc.py -v
```

**Attendu :**
```python
# Scénario : deux médecins se retirent simultanément de l'astreinte
# (write skew classique de DDIA)
txn1 = store.begin()
txn2 = store.begin()
# Les deux voient 2 médecins de garde
assert store.read("on_call_count", txn1) == 2
assert store.read("on_call_count", txn2) == 2
# Les deux décident de retirer leur garde
store.write("alice_on_call", False, txn1)
store.write("bob_on_call", False, txn2)
store.commit(txn1)
store.commit(txn2)  # → ici, avec snapshot isolation, les DEUX commits passent
# Résultat : 0 médecins de garde ! Write skew !
```

---

## `anomalies.py` (Jour 55)

Démonstration de toutes les anomalies de concurrence :

| Anomalie | Niveau minimum pour l'éviter |
|----------|------------------------------|
| Dirty read | Read committed |
| Non-repeatable read | Snapshot isolation |
| Write skew | Serializable (SSI ou 2PL) |
| Phantom read | Serializable |

**Lancer :**
```bash
python code/05-transactions/anomalies.py
```

**Attendu :** chaque anomalie démontrée avec un scénario clair et le comportement attendu à chaque niveau d'isolation.

---

## Lien avec les labos (Jours 58-59)

Reproduire les mêmes anomalies dans Postgres :
```sql
-- Read uncommitted (Postgres implémente read committed au minimum)
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;

-- Snapshot isolation
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;

-- Serializable (SSI dans Postgres)
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
```
