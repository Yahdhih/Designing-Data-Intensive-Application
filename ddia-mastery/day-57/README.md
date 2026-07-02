# Jour 57 — Exercice de conception avancé : Détection de fraude en temps réel

🛠️ Conception système · ~60 min · Pas de lecture

---

## 🎯 Objectif du jour

Appliquer tout DDIA sur un problème de conception réel. La détection de fraude est un cas d'usage qui mobilise Ch.5 (réplication), Ch.6 (partitionnement), Ch.7 (transactions), Ch.9 (consensus), Ch.11 (stream), Ch.12 (données dérivées).

---

## 🛠️ Problème : système de détection de fraude bancaire

### Contexte

- **Volume :** 10 000 transactions/seconde
- **Contrainte critique :** détecter et bloquer les transactions frauduleuses **avant** d'autoriser le paiement (latence < 200ms)
- **Signal de fraude :** utilisation d'une même carte depuis 2 pays différents en < 1 heure
- **Infrastructure :** cluster de 20 noeuds, stockage distribué, budget raisonnable

---

## ✏️ Exercices (60 min)

### Partie 1 — Architecture globale (15 min)

Dans `notes.md`, dessine le flux de données du système :

```
Transaction entrante
    ↓
[Composant A : ??? ]     ← quel rôle ?
    ↓
[Composant B : ??? ]     ← quel rôle ?
    ↓
Décision : APPROVE / BLOCK
    ↓
[Composant C : ??? ]     ← quel rôle ?
```

Remplis les composants avec des technologies concrètes et leur rôle.

### Partie 2 — Partitionnement (10 min)

Les transactions doivent être partitionnées pour paralléliser le traitement.  
Dans `notes.md`, réponds :

1. Partitionnes-tu par `card_id` (hash) ou par `timestamp` (range) ? Pourquoi ?
2. Pour détecter « même carte, 2 pays différents en < 1h » : toutes les transactions de la même carte doivent être sur le même noeud. Quel problème ça crée si Beyoncé utilise sa carte 1000 fois/seconde ?
3. Comment résous-tu le hot spot de la Partie 2.2 ?

### Partie 3 — Fenêtres temporelles (10 min)

Le signal de fraude est détecté via une fenêtre glissante de 1 heure par card_id.

Dans `notes.md`, décris :
1. Quel type de fenêtre utilises-tu ? (tumbling / hopping / sliding / session)
2. Que se passe-t-il si une transaction arrive avec 10 minutes de retard par rapport à son event time ?
3. Comment stockes-tu l'état « transactions des dernières 60 minutes par card_id » ? (In-memory ? RocksDB local ? Redis ?)

### Partie 4 — Cohérence et transactions (10 min)

Problème : la décision doit être prise **avant** que la transaction soit validée.  
Mais le système de détection peut être en retard de quelques secondes.

Dans `notes.md` :
1. Est-ce acceptable d'avoir un système de fraude en **eventual consistency** ? Explique les conséquences.
2. Comment garantis-tu l'**idempotence** (une transaction n'est analysée qu'une seule fois même si Kafka livre le message 2 fois) ?
3. Que fait le système si le service de détection est en panne (timeout) — approuve-t-il ou bloque-t-il ?

### Partie 5 — Tolérance aux pannes (15 min)

Dans `notes.md` :
1. Si un noeud qui traite les transactions de card_id = "4242" tombe, que se passe-t-il ? Comment le système récupère-t-il ?
2. Si le stream processing perd son état (RocksDB corrompu), comment reconstruit-il l'état des dernières 60 minutes ?
3. Quel est le **pire scénario** pour ce système en termes de panne ? Comment l'atténues-tu ?

---

## ✅ Terminé quand

- [ ] Architecture globale dessinée
- [ ] Partitionnement + hot spot traités
- [ ] Fenêtres temporelles + late data traités
- [ ] Cohérence + idempotence traités
- [ ] Tolérance aux pannes traitée
- [ ] Coché dans PROGRESS.md

## → Demain
Quiz DDIA — 20 questions de compréhension couvrant les 12 chapitres.
