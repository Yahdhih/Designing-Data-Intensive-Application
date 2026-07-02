# Mes notes — Jour 49

## Prédictions (avant lecture)

1. 

2. 

3. 

---

## Ex 1 — 4 types de fenêtres

| Type | Description | Cas d'usage |
|------|------------|-------------|
| Tumbling (1h) | | |
| Hopping (1h/15min) | | |
| Sliding (30 min) | | |
| Session (inactivité) | | |

---

## Ex 2 — Event time vs Processing time

Sans watermark, événement event_ts=14h00, proc_ts=14h07 → fenêtre :

Watermark 5 min → fenêtre 14h-15h se ferme à :

Événement proc_ts=14h10, event_ts=13h55 → système fait :

---

## Ex 3 — Stream-table join en pratique


---

## Autres notes


