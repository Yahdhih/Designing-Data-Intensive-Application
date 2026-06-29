# DDIA Mastery — Système d'étude quotidien

**Livre :** *Designing Data-Intensive Applications* (DDIA)  
**Auteurs :** Martin Kleppmann (1ʳᵉ éd. 2017) · Kleppmann & Riccomini (2ᵉ éd. 2026)  
**Rythme :** 1 heure par jour · **Durée estimée :** 5-8 mois (Partie II seule ≈ 2 mois bien tassés)

---

## Mode d'emploi quotidien

1. Ouvre `PROGRESS.md` → trouve le prochain jour non coché.
2. Ouvre `days/day-NNN.md`.
3. Suis les instructions minute par minute.
4. Coche ✅ dans `PROGRESS.md` avant de fermer.

---

## Les 3 règles d'or

**(a) Predict-then-verify.**  
Avant de lire une section, écris 2 lignes sur ce que tu anticipes. Sans cette friction, la lecture passive ne laisse aucune trace durable.

**(b) Si je ne peux pas le réimplémenter ou le redessiner de mémoire, je ne l'ai pas compris.**  
La lecture seule ne suffit pas. Chaque concept clé doit être redécrit avec tes propres mots, dessiné à la main ou codé en jouet.

**(c) Règle des 2 jours.**  
Ne jamais sauter 2 jours de suite. Si tu sautes un jour, **ne double pas la dose** — reprends simplement le lendemain. La régularité bat l'intensité.

---

## Structure du dépôt

| Dossier | Contenu |
|---------|---------|
| `days/` | Un fichier par jour — exactement quoi faire en 1 heure, minuté |
| `setup/` | Environnement, calibration TOC, boîte à outils méthodologique |
| `reference/` | Glossaire, matrices de compromis, notes quotidiennes, schémas |
| `flashcards/` | Cartes Anki importables `.tsv` + consignes « page blanche » |
| `code/` | Implémentations jouets Python (± Go) par thème |
| `labs/` | Labos Docker (Postgres, Kafka, Cassandra, etcd, Debezium…) |
| `papers/` | Articles fondateurs cartés par chapitre + fiches de lecture |
| `reviews/` | Gabarit de revue hebdomadaire (chaque 7ᵉ jour) |
| `PLAN.md` | Curriculum complet : phases, grappes, jouets, labos, articles |
| `PROGRESS.md` | Suivi jour par jour + compteur de série (streak) |

---

## Deux éditions — note importante

Ce dépôt gère les **deux éditions** :
- **1ʳᵉ éd. (2017, Kleppmann)** : 12 chapitres, la version canonique que possède la plupart des lecteurs.
- **2ᵉ éd. (2026, Kleppmann & Riccomini)** : chapitres réorganisés, cloud-natif, stockage objet comme modèle dominant, streaming → vues incrémentales.

**Ton premier geste :** déclare ton édition dans `setup/00-setup.md` et remplis `reference/toc.md` avec ta vraie table des matières. Tous les fichiers-jours utilisent des placeholders `p. ___` à calibrer sur ta TOC réelle.

Si tu lis la **1ʳᵉ éd.**, les encarts **📌 Contexte 2026** dans les fichiers-jours te rappellent les évolutions récentes (stockage objet, Materialize, cloud-natif).

---

## Profil de l'apprenant (mémorisé dans le plan)

Tu es étudiant ingénieur HPC / Big Data / Data Engineering. Stack connue : **Spark, Kafka, OpenSearch, Docker, Kubernetes** · Python, Java, C/C++, OCaml. Le plan exploite ton expérience Kafka/Spark à fond en Phase 3, et ne ré-explique pas Docker.

---

## Étendre le plan

Quand tu arrives à la fin des jours générés, lance dans Claude Code :
```
Génère days/day-022.md à day-042.md selon PLAN.md et PROGRESS.md.
```

---

## Méthode en 5 lignes

1. **Rappel actif** avant de lire (5 min page blanche ou cartes dues).
2. **Predict-then-verify** à chaque section.
3. **Alterner** lecture / jouet / labo / article — jamais 3 lectures d'affilée.
4. **Consolider** 15 min : résumé en tes mots + 2-3 cartes + 1 schéma + 1 question ouverte.
5. **Revue hebdo** chaque 7ᵉ jour : pas de matière neuve, redessine et réexplique tout.
