# Jour 19 — Ch.5 : Réplication multi-leader

📖 Lecture · ~45 min de lecture + 15 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 5, section « Multi-Leader Replication » (jusqu'à « Leaderless Replication »)

Dans la réplication **multi-leader**, plusieurs noeuds acceptent des écritures. Ça résout des problèmes de latence (datacenters multiples, mode offline) mais crée un nouveau problème : les **conflits d'écriture**.

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, réponds AVANT d'ouvrir le livre :

1. Pourquoi voudrait-on avoir plusieurs leaders plutôt qu'un seul ?
2. Si deux leaders acceptent des écritures sur la même donnée simultanément — qu'est-ce qui se passe ?
3. Tu utilises ton application offline (ex : Google Docs sans connexion). Comment les modifications sont-elles synchronisées après reconnexion ?

---

## 📚 Points à remarquer pendant la lecture

- Les **cas d'usage** du multi-leader : datacenters multiples, clients offline (calendrier mobile), édition collaborative temps-réel
- Le problème des **conflits d'écriture** — ils ne peuvent pas être évités en multi-leader
- Les stratégies de **résolution de conflits** :
  - Last Write Wins (LWW) — basé sur le timestamp
  - Merge des valeurs
  - Résolution par l'application (laisser l'utilisateur choisir)
  - CRDTs (structures de données sans conflit)
- Les **topologies de réplication** multi-leader : circular, star, all-to-all

---

## ✏️ Exercices (15 min)

### Ex 1 — Cas d'usage multi-leader (5 min)
Pour chacun des 3 cas d'usage identifiés dans la lecture :
- Quel problème du single-leader résout-il ?
- Quel nouveau problème le multi-leader crée-t-il ?

### Ex 2 — Stratégies de résolution de conflits (7 min)
Imagine que deux utilisateurs modifient le même document Google Docs simultanément offline.  
Quelle stratégie de résolution de conflit serait la meilleure ? Pourquoi ?  
Est-ce que Last Write Wins serait acceptable ici ?

### Ex 3 — Connexion à Kafka (3 min)
Kafka est single-leader (un leader par partition). Pourquoi Kafka a-t-il choisi single-leader plutôt que multi-leader pour ses partitions ?

---

## ✅ Terminé quand

- [ ] Lecture (Multi-Leader Replication) terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (3 cas d'usage multi-leader) fait
- [ ] Ex 2 (résolution de conflits Google Docs) fait
- [ ] Ex 3 (connexion Kafka single-leader) fait
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.5 — Réplication sans leader (Dynamo-style, quorums, sloppy quorum). Le modèle de Cassandra.
