# Mes notes — Jour 32

## Partie 1 — Identifier l'anomalie

Anomalie :

Niveau d'isolation minimal :

---

## Partie 2 — 3 approches

**Approche A — Opération atomique :**
Ce que fait le SQL :
Avantage :
Problème :

**Approche B — SELECT FOR UPDATE :**
Ce que fait le SQL :
Avantage :
Problème :

**Approche C — SERIALIZABLE :**
Ce que fait le SQL :
Avantage :
Problème :

---

## Partie 3 — Mon choix pour la production

Choix :

Justification :

Comportement de SERIALIZABLE sous très forte contention :

Comment éviter le deadlock avec 2 concerts (FOR UPDATE) :

---

## Partie 4 — Kafka dans le pipeline

Nouveau problème (at-least-once) :

Solution :

