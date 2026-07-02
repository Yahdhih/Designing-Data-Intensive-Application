# Jour 05 — Ch.2 : Modèle relationnel vs modèle document

📖 Lecture · ~45 min de lecture + 15 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 2, du début jusqu'à la fin de la section sur le modèle document (avant les langages de requête)

Ch.2 couvre les différents modèles de données. Aujourd'hui : pourquoi le **modèle relationnel** a dominé, et pourquoi le **modèle document** (JSON/NoSQL) est revenu sur le devant de la scène.

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, réponds AVANT d'ouvrir le livre :

1. Pourquoi selon toi le SQL/relationnel a-t-il dominé pendant 30 ans alors qu'il n'existait pas d'autre chose avant ?
2. Qu'est-ce que le « NoSQL » apporte que le SQL ne peut pas faire selon toi ?
3. C'est quoi l'**impedance mismatch** selon ta compréhension actuelle ?

---

## 📚 Points à remarquer pendant la lecture

- La notion d'**impedance mismatch** — le fossé entre les objets dans le code et les tables en base
- Kleppmann montre un exemple concret de CV (curriculum vitae) en relationnel puis en JSON — compare les deux
- Les **jointures** dans le modèle relationnel vs la **dénormalisation** dans le modèle document
- Quand le modèle document est **meilleur** que le modèle relationnel (et vice-versa)
- La notion de **schema-on-read** vs **schema-on-write** — c'est une distinction importante

---

## ✏️ Exercices (15 min)

### Ex 1 — Comparaison des deux modèles (7 min)
Remplis ce tableau dans `notes.md` (de mémoire après lecture) :

| Critère | Modèle relationnel | Modèle document |
|---------|-------------------|-----------------|
| Structure | | |
| Jointures | | |
| Flexibilité schema | | |
| Meilleur pour | | |
| Moins bon pour | | |

### Ex 2 — L'impedance mismatch expliqué (5 min)
Explique l'impedance mismatch en 3 phrases simples, comme si tu expliquais à quelqu'un qui ne fait pas de bases de données.

### Ex 3 — Exemple de ton stack (3 min)
Tu connais OpenSearch qui stocke des documents JSON.  
Donne un exemple de cas où le stockage document d'OpenSearch est **plus naturel** que de mettre les mêmes données en SQL.

---

## ✅ Terminé quand

- [ ] Lecture de la section (modèle relationnel vs document) terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (tableau comparatif) fait
- [ ] Ex 2 (impedance mismatch) expliqué
- [ ] Ex 3 (exemple OpenSearch) fait
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.2 — Langages de requête : SQL déclaratif vs MapReduce impératif. Les graph queries.
