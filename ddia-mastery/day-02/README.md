# Jour 02 — Ch.1 : Reliability (fiabilité)

📖 Lecture · ~45 min de lecture + 15 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 1, du début jusqu'à la fin de la section « Reliability »

Kleppmann commence par définir les 3 préoccupations centrales de tout système de données : **reliability**, **scalability**, **maintainability**. Aujourd'hui tu lis uniquement la partie **reliability**.

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, réponds AVANT d'ouvrir le livre :

1. Qu'est-ce que « fiabilité » signifie pour toi dans le contexte d'un système distribué ? Donne ta définition personnelle.
2. Quelle est la différence entre un **bug** et une **panne** (fault) selon toi ?
3. Comment est-ce qu'on peut rendre un système tolérant aux pannes s'il y a toujours un risque de panne matérielle ?

---

## 📚 Points à remarquer pendant la lecture

- La distinction **fault** vs **failure** — c'est précis et important
- Les 3 types de pannes : hardware, software, humain — pour chacun, note la **stratégie de mitigation**
- Pourquoi Netflix a créé le « Chaos Monkey » — qu'est-ce que ça dit sur l'approche de la fiabilité ?
- La phrase clé : « it is impossible to reduce the probability of a fault to zero »

---

## ✏️ Exercices (15 min)

### Ex 1 — Résumé par type de panne (5 min)
Remplis ce tableau dans `notes.md` de mémoire (sans recopier le livre) :

| Type de panne | Exemple concret | Stratégie de mitigation |
|---------------|----------------|------------------------|
| Hardware | | |
| Software | | |
| Humain | | |

### Ex 2 — Feynman : explique à quelqu'un (5 min)
Imagine que tu expliques à un ami non-informaticien ce qu'est une panne « en cascade » (cascading failure).  
Écris 3-4 phrases simples, sans jargon.

### Ex 3 — Vérification des prédictions (5 min)
Reprends tes 3 prédictions. Pour chacune :
- Est-ce que tu avais raison ? Partiellement ? Complètement faux ?
- Note ce qui était surprenant.

---

## ✅ Terminé quand

- [ ] Lecture de la section « Reliability » terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (tableau des 3 types de panne) fait
- [ ] Ex 2 (Feynman) fait
- [ ] Ex 3 (vérification prédictions) fait
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.1 — Scalability : comment mesurer la charge ? L'exemple Twitter. Les percentiles de latence.
