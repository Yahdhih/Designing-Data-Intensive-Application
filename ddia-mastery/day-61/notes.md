# Mes notes — Jour 61 (Conception : analytics musicale)

## Partie 1 — Contraintes

3 cas d'usage :
1. 
2. 
3. 

Latences :

Cohérence (exact vs approximatif) :

Volume : 100K/s × 3600 × 24 = ___ Go/jour

---

## Partie 2 — Architecture

**Ingestion :**

**Traitement temps réel :**

**Stockage historique :**

**Suppression d'artiste :**

---

## Partie 3 — Compromis

| Choix | Avantage | Compromis | Ch. DDIA |
|-------|---------|----------|---------|
| Kafka | | | |
| Flink | | | |
| Parquet/S3 | | | |
| Redis top 100 | | | |
| CDC suppression | | | |

---

## Partie 4 — Top 100 exact

Pourquoi difficile :

Solution exacte + coût :

Solution approximative + erreur :

