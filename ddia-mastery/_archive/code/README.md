# code/ — Implémentations jouets

> **Règle d'or :** *Si je ne peux pas le réimplémenter ou le redessiner de mémoire, je ne l'ai pas compris.*  
> Les jouets sont délibérément simplifiés — l'objectif est de capturer le **mécanisme essentiel**, pas de faire du code de production.

---

## Organisation

```
code/
  common/              # helpers partagés, venv, requirements
  01-storage-retrieval/  # Bitcask, mini-LSM, mini-B-tree
  02-encoding/         # encodeur binaire, évolution de schéma
  03-replication/      # simulateur mono-leader, quorum
  04-partitioning/     # anneau de hachage cohérent
  05-transactions/     # KV MVCC, anomalies d'isolation
  06-distributed-troubles/  # horloges Lamport + vectorielles
  07-consensus/        # mini-Raft
  08-batch/            # mini-MapReduce
  09-stream/           # broker log, fenêtres, CDC WAL
  99-capstone/         # KV distribué bout-en-bout
```

---

## Choix de langage

**Python (défaut) :** tous les jouets sont en Python. Simple, lisible, idéal pour capturer les concepts sans bruit syntaxique.

**Go (optionnel, recommandé pour Ch.7-9) :** les goroutines et canaux modélisent naturellement la concurrence distribuée (mini-Raft, simulateur de quorum, horloges vectorielles). Si tu veux t'y mettre :

```bash
# Initialiser Go pour un module
cd code/07-consensus
go mod init ddia-mastery/consensus
go run raft_sim.go
```

---

## Mise en place de l'environnement Python

```bash
# Depuis la racine de ddia-mastery/
python -m venv .venv
source .venv/bin/activate

pip install -r code/common/requirements.txt

# Lancer les tests d'un jouet
pytest code/01-storage-retrieval/ -v
```

---

## Motif « jouet → vrai système »

Pour chaque thème :
1. **Jouet Python** : implémente le mécanisme de zéro en quelques dizaines de lignes.
2. **Vrai système** (labo Docker) : reproduis le même concept sur un système de production, observe les différences.

Exemple :
- Jouet : `code/01-storage-retrieval/lsm.py` (mini-LSM en 80 lignes)
- Vrai système : RocksDB via Cassandra dans `labs/storage/`

---

## Critères « terminé » pour chaque jouet

Chaque `README.md` de sous-dossier définit un **comportement attendu et vérifiable**.  
Un jouet est terminé quand :
- Les tests passent (`pytest`) **OU**
- Le comportement attendu est observé et documenté dans `reference/notes/`
- Tu peux redessiner le mécanisme de mémoire

---

## Jalons progressifs (ne saute pas d'étapes)

Pour `01-storage-retrieval/` par exemple :

```
Jalon 1 : log append-only + lecture séquentielle
Jalon 2 : index hachage (byte offsets) → lecture O(1)
Jalon 3 : segmentation + compaction basique
Jalon 4 : SSTables triées → lectures par range
Jalon 5 : multi-niveaux → compaction hiérarchique
Jalon 6 : filtre de Bloom → skip SSTables inutiles
```

Chaque jalon = 1 test vert ou 1 observation documentée.
