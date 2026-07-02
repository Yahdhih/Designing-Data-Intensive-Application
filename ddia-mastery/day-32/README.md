# Jour 32 — Exercice de conception : système de réservation

🛠️ Conception appliquée · ~60 min

---

## 🎯 Objectif du jour

Appliquer les concepts de Ch.7 sur un problème concret de conception. Pas de nouvelle lecture — uniquement de la pratique.

---

## 🛠️ Problème : système de réservation de billets

### Contexte

Tu conçois un système de réservation de billets de concert :
- 1000 places disponibles par concert
- Contrainte : jamais vendre plus de places qu'il n'en reste
- Charge : jusqu'à 10 000 requêtes simultanées lors de l'ouverture des ventes
- Stack : Postgres + backend Python

---

## ✏️ Exercices (60 min)

### Partie 1 — Identifier l'anomalie (10 min)

Dans `notes.md`, réponds :

**Scénario :**
```
T1 : SELECT places_restantes → 1
T2 : SELECT places_restantes → 1
T1 : -- décide de réserver
T2 : -- décide de réserver
T1 : UPDATE places_restantes = places_restantes - 1
T2 : UPDATE places_restantes = places_restantes - 1
T1 : COMMIT  (places_restantes = 0)
T2 : COMMIT  (places_restantes = -1) ← PROBLÈME
```

1. Quelle anomalie de Ch.7 est-ce ? (dirty read / lost update / write skew / phantom ?)
2. Quel niveau d'isolation **minimal** suffit à protéger contre ça ?

### Partie 2 — 3 approches de solution (25 min)

Pour chacune des 3 approches ci-dessous, note dans `notes.md` :
- Ce que fait exactement le SQL
- Quel niveau d'isolation il faut
- L'avantage et le problème de cette approche

**Approche A — Opération atomique SQL :**
```sql
UPDATE concerts
SET places_restantes = places_restantes - 1
WHERE id = 42 AND places_restantes > 0
-- Vérifier ROWCOUNT = 1, sinon la place n'était plus disponible
```

**Approche B — SELECT FOR UPDATE (verrou pessimiste) :**
```sql
BEGIN;
SELECT places_restantes FROM concerts WHERE id = 42 FOR UPDATE;
-- Si places_restantes > 0 :
UPDATE concerts SET places_restantes = places_restantes - 1 WHERE id = 42;
INSERT INTO reservations (concert_id, user_id) VALUES (42, 123);
COMMIT;
```

**Approche C — Niveau d'isolation SERIALIZABLE :**
```sql
BEGIN ISOLATION LEVEL SERIALIZABLE;
SELECT places_restantes FROM concerts WHERE id = 42;
-- Si places_restantes > 0 :
UPDATE concerts SET places_restantes = places_restantes - 1 WHERE id = 42;
INSERT INTO reservations (concert_id, user_id) VALUES (42, 123);
COMMIT;
-- En cas de conflit SSI → ERROR → retry côté application
```

### Partie 3 — Ton choix pour la production (15 min)

Dans `notes.md`, réponds :

1. Laquelle des 3 approches choisirais-tu pour gérer 10 000 requêtes simultanées à l'ouverture des ventes ? Justifie avec les concepts de Ch.7.
2. Comment l'approche C (SERIALIZABLE) se comporte-t-elle sous très forte contention ? (Hint : SSI vs 2PL)
3. Si tu utilises l'Approche B (FOR UPDATE), comment évites-tu un **deadlock** si la réservation implique 2 concerts en même temps (package deal) ?

### Partie 4 — Extension : Kafka dans le pipeline (10 min)

Imagine que les réservations passent par Kafka avant d'arriver en base :
- Un service publie `reservation_requested` sur Kafka
- Un consumer insère dans Postgres

Dans `notes.md` : quel nouveau problème apparaît ? (Pense aux garanties de Kafka : at-least-once delivery)  
Comment le résoudre ?

---

## ✅ Terminé quand

- [ ] Anomalie identifiée (Partie 1)
- [ ] 3 approches analysées (Partie 2)
- [ ] Choix de production justifié (Partie 3)
- [ ] Extension Kafka traitée (Partie 4)
- [ ] Coché dans PROGRESS.md

## → Demain
🔁 Revue Ch.7 — rappel actif complet de tout le chapitre. Hiérarchie des anomalies + solutions.
