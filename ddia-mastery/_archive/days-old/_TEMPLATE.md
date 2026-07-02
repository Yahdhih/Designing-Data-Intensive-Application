# Jour NNN — Phase {n} · {thème du jour}

> ⏱ 60 min  |  {icône} {type} 40 · 🧠 Consolidation 15 · 🔁 Réveil 5
> 💡 **Rappel méthode :** {une astuce parmi les 10 principes, tournante}

---

## 🔁 Réveil mémoire — 5 min

- **Page blanche :** {consigne de récupération sur le jour/chapitre précédent}. Écris de mémoire sans ouvrir tes notes. Note les trous.
- **Cartes dues :** reviens sur Anki → balaye les cartes du tag `{tag}` dues aujourd'hui.

---

## {📖 Lecture | 🛠️ Jouet | 🧪 Labo | 📄 Article} — 40 min

<!-- ═══════════════════════════════════════════════════ si LECTURE -->
### Avant de lire — Predict (3 min)
*Écris sur papier ou dans `reference/notes/jour-NNN.md` :*
> « Selon moi, {sujet du jour}, c'est... »

### Lis {Chapitre X, §Y} (p. ___ → p. ___, voir `reference/toc.md`)
- Repère les termes en gras → alimente `reference/glossary.md`.
- Pour chaque technique rencontrée : ajoute une ligne dans `reference/tradeoffs.md`.

### Verify (3 min)
Relis tes prédictions. Note explicitement là où tu t'es trompé.

### Points clés à retenir
1. {point 1}
2. {point 2}
3. {point 3}

<!-- ═══════════════════════════════════════════════════ si JOUET -->
### Objectif
{Ce qu'on construit et pourquoi}

### Fichiers
- `code/{dossier}/{fichier}.py`

### Lancer
```bash
python code/{dossier}/{fichier}.py
# ou
pytest code/{dossier}/test_{fichier}.py -v
```

### Attendu
```
{comportement vérifiable}
```

### Compromis à observer
{Ce qu'on apprend de ce jouet sur les compromis}

<!-- ═══════════════════════════════════════════════════ si LABO -->
### Démarrer le stack
```bash
docker compose -f labs/compose.{light|full}.yml up -d {service}
```

### Manipulation
1. {étape 1}
2. {étape 2}
3. {étape 3}

### Observe
- {ce qu'on doit voir/mesurer}

### Casse les choses (optionnel si temps)
```bash
# {commande d'injection de panne}
```
Observe : {comportement attendu après la panne}

<!-- ═══════════════════════════════════════════════════ si ARTICLE -->
### Article
**{Titre}** — {Auteurs}, {Année}  
→ Voir `papers/reading-list.md` pour le résumé et où le trouver.

### Méthode (3 passes)
1. **Passe 1 (5 min) :** abstract → intro → conclusion → titres de sections
2. **Passe 2 (15 min) :** toutes les figures et tableaux
3. **Passe 3 (20 min) :** corps sélectif — les sections qui répondent aux 3 questions

### Réponds à ces 3 questions dans `papers/notes/{article}.md`
1. Quel problème résout cet article ?
2. Quelle est l'idée clé ?
3. Quel est le compromis principal ?

---

## 🧠 Consolidation — 15 min

- [ ] Résumé 3-5 puces **dans tes mots** → `reference/notes/jour-NNN.md`
- [ ] 2-3 cartes ajoutées à `flashcards/cards.tsv` (un exemple concret par carte)
- [ ] 1 schéma dessiné → `reference/diagrams/jour-NNN-{sujet}.png` (photo de ton dessin)
- [ ] 1 ligne ajoutée dans `reference/tradeoffs.md`
- [ ] 1 question ouverte notée

---

## ✅ Terminé quand

- [ ] {Critère principal vérifiable}
- [ ] Résumé écrit dans `reference/notes/jour-NNN.md`
- [ ] 2-3 cartes ajoutées
- [ ] PROGRESS.md coché ✅

## ↪ Demain
{Teaser en une ligne sur le Jour NNN+1}
