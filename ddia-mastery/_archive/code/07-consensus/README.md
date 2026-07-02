# code/07-consensus/ — Consensus & mini-Raft

> Chapitre 9 · Jours 75-76 · `PLAN.md` Phase 2 · **LE SOMMET DU CŒUR**

---

## Objectif

Implémenter une version simplifiée de Raft pour *ressentir* les problèmes que Raft résout :
1. **Élection de leader** : qui commande ?
2. **Réplication de log** : comment les entrées sont-elles validées ?
3. **Sécurité** : comment garantir qu'aucune entrée committée n'est perdue ?
4. **Fencing token** : comment éviter les actions d'un leader zombie ?

---

## Architecture du jouet

```
raft_sim.py       # Nœuds Raft avec passage de messages simulé (files de messages)
raft_state.py     # Machine d'état : RaftLog + StateMachine (KV store)
fencing.py        # Démo de fencing token
```

---

## `raft_sim.py` (Jour 75)

**Simplifications :**
- Réseau simulé par des files Python (pas de vraie communication réseau)
- Les délais aléatoires sont simulés par `random.random()`
- Pas de persistance sur disque (pour simplicité)

**Jalons :**
```
Jalon 1 : 3 nœuds + heartbeat + détection de panne du leader
Jalon 2 : élection → un seul leader élu (terme + votes)
Jalon 3 : réplication de log → AppendEntries → commit majoritaire
Jalon 4 : machine d'état KV → les clients lisent depuis le leader
Jalon 5 : simuler la panne du leader → nouvelle élection → log cohérent
```

**Lancer :**
```bash
python code/07-consensus/raft_sim.py
pytest code/07-consensus/test_raft.py -v
```

**Attendu :**
```
Nœud 1 démarre : follower (terme 0)
Nœud 2 démarre : follower (terme 0)
Nœud 3 démarre : follower (terme 0)

[t=150ms] Nœud 1 timeout → candidate (terme 1) → RequestVote
[t=151ms] Nœud 2 vote pour Nœud 1
[t=152ms] Nœud 3 vote pour Nœud 1
[t=152ms] Nœud 1 : LEADER élu (terme 1, 2 votes sur 3)

Client: set("x", 42) → Nœud 1 (leader)
  AppendEntries envoyé à Nœud 2 et Nœud 3
  Majorité atteinte → COMMITTÉ (index 1)
  Machine d'état : x = 42

[t=300ms] Nœud 1 (leader) paused → timeout sur Nœud 2 + 3
[t=450ms] Nœud 3 élu leader (terme 2)
[t=451ms] get("x") → 42 (log cohérent préservé)
```

---

## `fencing.py` (Jour 76)

Démonstration du problème d'un leader zombie + solution par fencing token.

```python
# Sans fencing : leader zombie peut écrire après avoir perdu sa position
# Avec fencing : le numéro de terme Raft sert de fencing token monotone
# Le storage rejette les écritures avec un terme < terme courant
```

---

## Voie Go (recommandée pour ce jouet)

```bash
cd code/07-consensus
go mod init ddia-mastery/consensus
go run raft_sim.go
```

Les goroutines Go modélisent naturellement les nœuds Raft concurrents et les canaux simulent le réseau.
