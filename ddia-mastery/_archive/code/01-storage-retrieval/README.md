# code/01-storage-retrieval/ — Stockage & récupération

> Chapitre 3 · Jours 11-16 (jouets) · `PLAN.md` Phase 1

---

## Objectif

Implémenter les trois grandes structures d'index de fond en comble, en Python :
1. **Bitcask** : log append-only + index hachage en mémoire (byte offsets)
2. **mini-LSM** : SSTables triées + compaction par fusion + filtre de Bloom
3. **mini-B-tree** : arbre équilibré en pages avec insertion et recherche

---

## Jalons progressifs

### `bitcask.py` (Jour 11)

```
Jalon 1 : log append-only → écriture séquentielle, lecture O(n)
Jalon 2 : index hachage {clé → byte_offset} → lecture O(1)
Jalon 3 : segmentation des fichiers + compaction basique (supprimer les doublons)
```

**Lancer :**
```bash
python code/01-storage-retrieval/bitcask.py
```

**Attendu :**
```
put("user:1", "Alice") → offset 0
put("user:2", "Bob")   → offset 24
get("user:1")          → "Alice" (lecture directe à l'offset 0)
put("user:1", "Alicia")→ nouvelle entrée à l'offset X, ancienne marquée obsolète
get("user:1")          → "Alicia"
compaction()           → espace récupéré, index mis à jour
```

**Compromis à observer :** toutes les clés doivent tenir en RAM (index hachage). Si la base a 100M de clés uniques, c'est un problème.

---

### `lsm.py` (Jour 12)

```
Jalon 1 : memtable (dict trié) + flush vers SSTable (fichier trié sur disque)
Jalon 2 : recherche dans N SSTables (du plus récent au plus ancien)
Jalon 3 : compaction par fusion (merge sort de 2 SSTables)
Jalon 4 : index creux (1 entrée sur K dans l'index)
Jalon 5 : filtre de Bloom (réduire les lectures inutiles)
```

**Lancer :**
```bash
python code/01-storage-retrieval/lsm.py
# ou les tests :
pytest code/01-storage-retrieval/test_lsm.py -v
```

**Attendu :**
- Écriture rapide (toujours séquentielle)
- Lecture correcte même avec plusieurs SSTables
- Après compaction : 1 seule SSTable, doublons supprimés

**Compromis à observer :**
- Amplification lecture : avec N SSTables non compactées, une lecture peut toucher N fichiers
- Amplification écriture : compaction réécrit des données plusieurs fois

---

### `btree.py` (Jour 15)

```
Jalon 1 : nœud B-tree (clés + enfants) + recherche d'une clé
Jalon 2 : insertion avec split de nœud quand plein
Jalon 3 : traversée en ordre (range scan)
```

**Lancer :**
```bash
pytest code/01-storage-retrieval/test_btree.py -v
```

**Attendu :**
- Insertion de 100 clés aléatoires → recherche correcte de n'importe laquelle
- Range scan sur [10..50] → toutes les clés dans l'intervalle

**Compromis à observer :**
- Modification en place → besoin du WAL pour récupération après crash
- Arbre équilibré → O(log n) toujours garanti pour lecture ET écriture

---

## Comparaison finale (après les 3 jouets)

Documente dans `reference/notes/` :

| Métrique | Bitcask | mini-LSM | mini-B-tree |
|----------|---------|----------|-------------|
| Amplification écriture | Faible | Moyenne (compaction) | Élevée (split + WAL) |
| Amplification lecture | Élevée (compaction non faite) | Moyenne | Faible |
| Range scan | Impossible | Bon (SSTables triées) | Excellent |
| Mémoire requise | Toutes clés en RAM | Memtable seulement | Pages chargées |
| Récupération crash | WAL ou rebuild | WAL | WAL obligatoire |
