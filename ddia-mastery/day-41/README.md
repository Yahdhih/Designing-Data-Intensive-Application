# Jour 41 — 🔁 Revue Ch.9 + Revue globale Partie II

🔁 Rappel actif · ~60 min

---

## 🎯 Objectif du jour

Consolider Ch.9 et faire une revue de toute la Partie II (Ch.5 à Ch.9). C'est le chapitre final de la partie la plus importante du livre.

---

## ✏️ Exercices (60 min)

### Ex 1 — Page blanche Ch.9 (15 min)

Ferme tout. Dans `notes.md`, retrouve de mémoire :

**Linearizability :**
- Définition :
- Quand en a-t-on besoin ?
- Coût ?

**Ordre causal :**
- Plus fort que :
- Plus faible que :
- Comment le garantir ?

**Total Order Broadcast :**
- Définition :
- Équivalent à :
- Exemple système :

**2PC :**
- Mécanisme (2 phases) :
- Problème fondamental :

**Consensus (Raft) :**
- Ce que ça garantit :
- Condition nécessaire (quorum) :

### Ex 2 — Le grand fil conducteur Partie II (20 min)

Dans `notes.md`, réponds à chaque question :

1. **Ch.5 → Ch.6** : Pourquoi a-t-on besoin de partitionnement après avoir répliqué ?
2. **Ch.6 → Ch.7** : Si les données sont sur plusieurs noeuds, pourquoi les transactions sont-elles plus difficiles ?
3. **Ch.7 → Ch.8** : Les transactions de Ch.7 supposent quoi sur l'infrastructure ?
4. **Ch.8 → Ch.9** : Les problèmes de Ch.8 rendent-ils le consensus impossible ? Ou juste difficile ?
5. **Ch.9 → Partie III** : Maintenant qu'on sait faire du consensus, que peut-on construire dessus ?

### Ex 3 — 5 systèmes réels, 5 chapitres (15 min)

Pour chacun, identifie quel chapitre de la Partie II est le plus pertinent pour comprendre son comportement :

| Système | Chapitre clé | Pourquoi |
|---------|-------------|--------|
| Cassandra | | |
| Kafka | | |
| Postgres (avec réplication) | | |
| etcd | | |
| MongoDB (cluster) | | |

### Ex 4 — Vérification (10 min)

Ouvre les Summaries de Ch.8 et Ch.9. Compare avec tes notes.  
Note les 2-3 points que tu n'avais pas bien mémorisés.

---

## ✅ Terminé quand

- [ ] Page blanche Ch.9 complète
- [ ] Fil conducteur Partie II (5 questions) fait
- [ ] Tableau 5 systèmes complété
- [ ] Vérification + lacunes notées
- [ ] Coché dans PROGRESS.md

## → Demain
Revue globale Partie I + II — synthèse de tout DDIA jusqu'ici avant d'attaquer la Partie III.
