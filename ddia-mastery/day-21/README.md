# Jour 21 — Ch.5 : Résumé + 🔁 Revue Ch.5

📖 Lecture Summary + rappel actif · ~20 min lecture + 40 min consolidation

---

## 📖 Lecture du jour

**Section :** Chapitre 5, section « Summary » (la fin du chapitre)

Relis le **Summary** de Ch.5 lentement. C'est le condensé de tout ce que tu as appris cette semaine. Kleppmann y rassemble les 3 modèles de réplication et leurs compromis.

---

## 🎯 Avant de lire le Summary — Prédis (5 min)

Dans `notes.md`, écris ce que tu t'attends à trouver dans ce summary (les points clés que tu te souviens de Ch.5).

---

## ✏️ Exercices de revue Ch.5 (40 min)

### Ex 1 — Page blanche Ch.5 (15 min)

Ferme tout. Dans `notes.md`, écris de mémoire :

**Single-leader :**
- Mécanisme en 2-3 phrases
- 3 anomalies de replication lag et leurs solutions

**Multi-leader :**
- Cas d'usage (3 exemples)
- Problème principal + stratégie de résolution

**Leaderless :**
- Mécanisme des quorums (w, r, n)
- Read repair et anti-entropy
- Exemple système

### Ex 2 — 5 questions de compréhension (15 min)

Réponds dans `notes.md` :

1. Quelle est la différence entre réplication **synchrone** et **asynchrone** ? Quel est le compromis exact ?
2. Tu as n=3 noeuds, w=2, r=2. Un noeud tombe. Peut-on encore lire ? Encore écrire ?
3. Que fait exactement le **WAL (Write-Ahead Log)** dans la réplication ?
4. Dans le multi-leader, pourquoi le **Last Write Wins** basé sur timestamp est-il dangereux ?
5. Quelle est la différence entre un **follower** (single-leader) et une **réplique** (leaderless) ?

### Ex 3 — Schéma mental : Ch.5 en un dessin (10 min)

Dans `notes.md`, dessine (ASCII) un schéma qui montre les 3 architectures de réplication côte à côte.  
Pour chacune, montre où va une écriture et comment elle se propage.

---

## ✅ Terminé quand

- [ ] Summary Ch.5 relu
- [ ] Prédictions du summary notées
- [ ] Ex 1 (page blanche Ch.5 complet) fait
- [ ] Ex 2 (5 questions) répondues
- [ ] Ex 3 (schéma des 3 architectures) dessiné
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.6 — Partitionnement : quand les données sont trop grandes pour un seul noeud, comment les diviser ?
