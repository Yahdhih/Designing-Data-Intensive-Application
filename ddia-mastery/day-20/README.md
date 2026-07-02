# Jour 20 — Ch.5 : Réplication sans leader (Dynamo-style)

📖 Lecture · ~45 min de lecture + 15 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 5, section « Leaderless Replication » (jusqu'à la fin du chapitre, avant Summary)

La réplication **sans leader** (leaderless) est le modèle utilisé par Cassandra, Riak, et le papier original Amazon Dynamo. Au lieu d'un leader unique, chaque noeud peut accepter des écritures. La cohérence est gérée par les **quorums**.

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, réponds AVANT d'ouvrir le livre :

1. Si tout noeud peut accepter des écritures, comment s'assure-t-on que les données sont cohérentes ?
2. Qu'est-ce qu'un **quorum** ? Donne ta définition intuitive.
3. Tu utilises Cassandra. Qu'est-ce que le paramètre `consistency_level` fait selon toi ?

---

## 📚 Points à remarquer pendant la lecture

- **Quorum reads/writes** : n noeuds au total, w écritures confirmées, r lectures consultées → si `w + r > n`, garantie de lire la valeur la plus récente
- **Read repair** : lors d'une lecture, si un noeud retourne une valeur ancienne, le coordinateur la corrige
- **Anti-entropy** : processus de fond qui compare les répliques et corrige les différences
- **Sloppy quorum** et **hinted handoff** : que se passe-t-il quand des noeuds ne sont pas disponibles ?
- Les **limites** des quorums : ils ne garantissent pas toujours la cohérence (edge cases avec concurrent writes)
- **Conflits en leaderless** : comment Cassandra résout les conflits (Last Write Wins basé sur timestamp)

---

## ✏️ Exercices (15 min)

### Ex 1 — Calcul de quorum (5 min)
Pour n=5 noeuds :
- Si w=3 et r=3 : est-ce qu'on a `w + r > n` ? Que garantit-on ?
- Si w=1 et r=5 : qu'est-ce que ça optimise (write ou read) ?
- Si w=5 et r=1 : qu'est-ce que ça optimise ?

### Ex 2 — Cassandra et ton expérience (7 min)
Tu as probablement utilisé Cassandra. Maintenant que tu comprends les quorums, explique :
- Que fait `CONSISTENCY QUORUM` dans Cassandra ?
- Que fait `CONSISTENCY ONE` ?
- Dans quel cas choisirais-tu `CONSISTENCY ALL` ?

### Ex 3 — Schéma de la famille de modèles (3 min)
Dans `notes.md`, fais un rapide résumé des 3 modèles de réplication vus dans Ch.5 :

| Modèle | Qui accepte les écritures | Exemple système |
|--------|--------------------------|----------------|
| Single-leader | | |
| Multi-leader | | |
| Leaderless | | |

---

## ✅ Terminé quand

- [ ] Lecture (Leaderless Replication) terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (calcul de quorum) fait
- [ ] Ex 2 (Cassandra + consistency levels) fait
- [ ] Ex 3 (tableau 3 modèles) fait
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.5 — Résumé + revue complète du chapitre. Avant-goût de Ch.6 (partitionnement).
