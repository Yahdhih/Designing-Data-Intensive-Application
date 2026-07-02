# Jour 50 — Ch.11 : Lambda vs Kappa + Résumé + 🔁 Revue Ch.11

📖 Lecture + consolidation · ~30 min lecture + 30 min revue

---

## 📖 Lecture du jour

**Section :** Chapitre 11, section « Summary » + les paragraphes sur la Lambda Architecture et la Kappa Architecture

La dernière section de Ch.11 discute deux architectures célèbres : **Lambda** (batch + stream en parallèle) et **Kappa** (stream seulement). Kleppmann explique pourquoi la Kappa architecture est souvent préférable.

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, réponds AVANT d'ouvrir le livre :

1. Pourquoi voudrait-on maintenir **deux** systèmes en parallèle (un batch + un stream) pour les mêmes données ?
2. Quel est le problème principal de la Lambda Architecture selon ton intuition ?
3. Si on pouvait relire tout l'historique des événements depuis Kafka aussi vite qu'un job Spark, aurait-on encore besoin du batch processing ?

---

## 📚 Points à remarquer pendant la lecture

- **Lambda Architecture** : batch layer (ex: Spark sur HDFS, résultats exacts) + speed layer (ex: Spark Streaming / Flink, résultats approximatifs en temps réel) + serving layer
- Problème de Lambda : deux systèmes différents pour la même logique → bugs de divergence, double maintenance
- **Kappa Architecture** : stream uniquement — le stream est assez rapide pour traiter l'historique en mode replay. Plus simple, une seule codebase

---

## ✏️ Exercices — Consolidation Ch.11 (30 min)

### Ex 1 — Lambda vs Kappa (8 min)

| | Lambda | Kappa |
|-|--------|-------|
| Systèmes maintenus | Batch + Stream | |
| Code dupliqué ? | Oui | |
| Résultats exacts | Oui (batch) | |
| Replay de l'historique | Via batch | |
| Problème principal | | |
| Quand utiliser | | |

### Ex 2 — Page blanche Ch.11 (15 min)

Ferme tout. Dans `notes.md`, retrouve de mémoire les 4 grandes idées de Ch.11 :

1. **Messagerie** : queue vs log-based (2-3 lignes chacun)
2. **CDC et Event Sourcing** : ce qu'ils ont en commun et leur différence principale
3. **Temps et fenêtres** : event time vs processing time + les 4 types de fenêtres (noms + 1 ligne chacun)
4. **Lambda vs Kappa** : principe + différence + pourquoi Kappa gagne souvent

### Ex 3 — Connexion Ch.10 → Ch.11 (7 min)

Batch Processing (Ch.10) et Stream Processing (Ch.11) sont souvent présentés comme opposés.  
Dans `notes.md`, explique :
- En quoi sont-ils **complémentaires** plutôt qu'opposés ?
- Quel problème Ch.11 résout que Ch.10 ne peut pas résoudre ?
- Et inversement : quel problème Ch.10 résout mieux que Ch.11 ?

---

## ✅ Terminé quand

- [ ] Lecture (Summary Ch.11 + Lambda/Kappa) terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (Lambda vs Kappa) fait
- [ ] Ex 2 (page blanche Ch.11) fait
- [ ] Ex 3 (connexion Ch.10 + Ch.11) fait
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.12 — Le futur des systèmes de données : intégration des données, unbundling des bases de données, correctness, éthique.
