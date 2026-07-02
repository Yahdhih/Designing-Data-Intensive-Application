# Jour 38 — Ch.9 : Consistance et Linéarisabilité

📖 Lecture · ~45 min de lecture + 15 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 9, du début jusqu'à la fin de la section « Linearizability »

Ch.9 répond aux problèmes de Ch.8. Il commence par définir précisément ce que « consistance » signifie — un terme qui est utilisé partout avec des sens différents. La **linéarisabilité** est la garantie de consistance la plus forte possible.

---

## 🎯 Avant de lire — Prédis (5 min)

Reprends tes prédictions du Jour 37 (Ex 4). Note lesquelles seront confirmées.

---

## 📚 Points à remarquer pendant la lecture

- La distinction entre les **garanties de consistance** (Ch.9) et les **niveaux d'isolation** (Ch.7) — deux choses différentes malgré la terminologie commune
- **Linearizability** (cohérence atomique) : le système se comporte comme s'il n'y avait qu'une seule copie des données, mise à jour de façon atomique. Après qu'une écriture est confirmée, toute lecture voit la nouvelle valeur — partout, immédiatement
- Les exemples de tests de linéarisabilité : les diagrammes de séquence avec les lignes d'opérations chevauchantes
- Quand la linéarisabilité est nécessaire : élection de leader, verrous distribués, unicité des contraintes
- Le **coût** de la linéarisabilité : performance et disponibilité (préfigure CAP)

---

## ✏️ Exercices (15 min)

### Ex 1 — Vérification de tes prédictions (3 min)

Compare tes prédictions du Jour 37 avec ce que tu viens de lire.  
Qu'est-ce qui était juste ? Qu'est-ce qui était faux ou imprécis ?

### Ex 2 — Test de linéarisabilité (7 min)

Voici un scénario. Déterminer s'il est linéarisable :

```
Client A écrit x = 1 (opération démarre à t=0, finit à t=10)
Client B lit x    (opération démarre à t=5, finit à t=8) → voit x = 0
Client C lit x    (opération démarre à t=12, finit à t=15) → voit x = 1
```

Questions :
- Client B peut-il légitimement voir x = 0 ? Pourquoi ?
- Que se passerait-il si Client C voyait x = 0 ? Est-ce linéarisable ?

### Ex 3 — Consistance vs Isolation (5 min)
Kleppmann distingue « consistance » (Ch.9) et « isolation » (Ch.7).  
Explique la différence en 3 phrases.  
Pourquoi un système peut-il avoir Serializable Isolation (Ch.7) sans être Linearizable (Ch.9) ?

---

## ✅ Terminé quand

- [ ] Lecture (début Ch.9 → Linearizability) terminée
- [ ] Vérification des prédictions faite
- [ ] Ex 2 (test de linéarisabilité) fait
- [ ] Ex 3 (consistance vs isolation) fait
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.9 — Ordre causal et Total Order Broadcast. Comment ordonner les événements sans horloge globale ?
