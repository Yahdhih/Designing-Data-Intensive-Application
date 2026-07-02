# Jour 59 — Questions d'entretien technique DDIA

🎤 Préparation entretien · ~60 min · Pratique orale

---

## 🎯 Objectif du jour

DDIA est le livre de référence pour les entretiens de système design. Ces questions sont typiques des entretiens Senior Data Engineer / Software Engineer chez des entreprises tech. Entraîne-toi à **répondre à voix haute** (ou à l'écrit de façon structurée).

---

## Format de réponse recommandé

Pour chaque question, structure ta réponse :
1. **Reformule** la question (10 sec)
2. **Clarifier les contraintes** (volume, latence, cohérence)
3. **Présente l'approche** (2-3 options)
4. **Défends ton choix** avec les compromis

---

## ✏️ Questions d'entretien (60 min — 6 questions, 10 min chacune)

### Q1 — Replica lag (Ch.5)

> « Dans une architecture single-leader avec réplication asynchrone, un utilisateur poste un tweet et rafraîchit immédiatement sa page — il ne voit pas son tweet. Pourquoi ? Comment résoudrais-tu ce problème ? »

Dans `notes.md`, donne une réponse structurée.

---

### Q2 — Partitionnement et hot spots (Ch.6)

> « Tu conçois un système de compteurs en temps réel (nombre de vues par vidéo YouTube). 10M de vidéos, 500K vues/seconde sur les top 100 vidéos. Comment partitionnes-tu pour éviter les hot spots ? »

Dans `notes.md`, donne une réponse structurée.

---

### Q3 — Transactions et isolation (Ch.7)

> « Deux utilisateurs réservent le dernier billet d'avion simultanément. Sans transaction, que peut-il se passer ? Avec quel niveau d'isolation Postgres règle-t-il ce problème ? »

Dans `notes.md`, donne une réponse structurée.

---

### Q4 — Systèmes distribués (Ch.8)

> « Un service A envoie une requête au service B et ne reçoit pas de réponse dans le délai imparti. Que peut-on conclure ? Quelles décisions peut-on prendre de façon sûre ? »

Dans `notes.md`, donne une réponse structurée.

---

### Q5 — Pipeline batch vs stream (Ch.10+11)

> « Tu dois calculer le nombre de transactions frauduleuses par heure pour un tableau de bord interne (fraîcheur : 1 heure) ET pour une alerte temps réel (fraîcheur : < 5 secondes). Deux systèmes ou un seul ? Quel(s) outil(s) ? »

Dans `notes.md`, donne une réponse structurée.

---

### Q6 — CDC et intégration (Ch.11+12)

> « Tu as Postgres comme base principale. Tu veux maintenir OpenSearch synchronisé pour la recherche full-text et un cache Redis pour les lookups rapides. Comment architecture-tu ça ? Que se passe-t-il si OpenSearch est en retard de 30 secondes ? »

Dans `notes.md`, donne une réponse structurée.

---

## ✅ Terminé quand

- [ ] Q1 (replica lag) répondue et structurée
- [ ] Q2 (hot spots) répondue et structurée
- [ ] Q3 (isolation + billets) répondue et structurée
- [ ] Q4 (timeout + systèmes distribués) répondue et structurée
- [ ] Q5 (batch vs stream) répondue et structurée
- [ ] Q6 (CDC + intégration) répondue et structurée
- [ ] Coché dans PROGRESS.md

## → Demain
Révision ciblée : reprends les lacunes du Quiz (Jour 58) et des entretiens (Jour 59).
