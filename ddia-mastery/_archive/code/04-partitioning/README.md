# code/04-partitioning/ — Partitionnement

> Chapitre 6 · Jours 45, 47 · `PLAN.md` Phase 2

---

## `consistent_hash.py` (Jour 45)

Anneau de hachage cohérent avec nœuds virtuels.

**Ce qu'on construit :**
- Anneau circulaire de 2^32 positions
- N nœuds physiques, chacun ayant V nœuds virtuels (V ≥ 100 recommandé)
- `get_node(key)` : renvoie le nœud responsable de la clé
- `add_node(node)` : ajoute un nœud, ne rééquilibre que les clés voisines
- `remove_node(node)` : retire un nœud, ne rééquilibre que ses clés

**Jalons :**
```
Jalon 1 : anneau + placement de N nœuds sans nœuds virtuels
Jalon 2 : get_node(key) → nœud successeur sur l'anneau
Jalon 3 : nœuds virtuels → distribution plus uniforme
Jalon 4 : add_node() → montrer que seulement K/N clés sont déplacées
Jalon 5 : démo de point chaud → clé populaire toujours sur le même nœud physique
```

**Lancer :**
```bash
python code/04-partitioning/consistent_hash.py
pytest code/04-partitioning/test_consistent_hash.py -v
```

**Attendu :**
```
Distribution avec 4 nœuds, 10000 clés :
  node-A : 24.8%  node-B : 25.1%  node-C : 24.9%  node-D : 25.2%

Ajout de node-E :
  Clés déplacées : 20.1% (≈ K/N comme attendu)
  Les autres nœuds non affectés
```

**Compromis :**
- Sans nœuds virtuels : distribution très inégale (nœuds sur l'anneau = positions aléatoires mais peu nombreuses)
- Avec 150 nœuds virtuels/nœud : distribution ~uniforme
- Rééquilibrage proportionnel (O(K/N)) vs rééquilibrage total (O(K)) pour le partitionnement fixe
