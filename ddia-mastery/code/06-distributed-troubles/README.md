# code/06-distributed-troubles/ — Problèmes des systèmes distribués

> Chapitre 8 · Jours 67-68 · `PLAN.md` Phase 2

---

## `clocks.py` (Jour 67)

Implémentation des horloges de Lamport et des horloges vectorielles.

**Ce qu'on construit :**
- 3 processus (A, B, C) échangeant des messages via une file simulée
- **Horloge de Lamport** : compteur entier monotone, incrémenté à chaque événement local et mis à jour à la réception d'un message
- **Horloge vectorielle** : vecteur de compteurs (un par processus), permettant de détecter la concurrence
- **Vérificateur de causalité** : étant donné deux événements e1 et e2 avec leurs vecteurs d'horloge, déterminer si e1 → e2, e2 → e1, ou e1 || e2 (concurrents)

**Jalons :**
```
Jalon 1 : 3 processus + file de messages + ordonnancement aléatoire
Jalon 2 : horloge de Lamport → ordre total des événements
Jalon 3 : horloge vectorielle → détecter la concurrence
Jalon 4 : vérificateur → e1 → e2 ? e2 → e1 ? ou || ?
```

**Lancer :**
```bash
python code/06-distributed-troubles/clocks.py
pytest code/06-distributed-troubles/test_clocks.py -v
```

**Attendu :**
```
A envoie msg1 à B (Lamport A=1)
B reçoit msg1 (Lamport B=2, car max(1, B_clock)+1)
B envoie msg2 à C (Lamport B=3)
C envoie msg3 à A indépendamment (Lamport C=1 → concurrent avec msg2)

Vecteurs d'horloge :
  msg2: (0, 3, 0)   → "B a fait 3 événements, A et C rien"
  msg3: (0, 0, 1)   → "C a fait 1 événement"
  Relation : msg2 || msg3  (concurrents — aucun n'a vu l'autre)
```

**Pourquoi c'est important :**
- Lamport clock : peut ordonner tous les événements mais ne détecte pas la concurrence
- Horloge vectorielle : détecte la concurrence mais consomme O(N) espace (N = nb nœuds)
- Application directe : résolution de conflits dans les systèmes sans leader (Dynamo, CouchDB)

---

## Lien avec le labo (Jour 69)

Après le jouet, injecter de vraies perturbations réseau :
```bash
# Simuler une partition réseau entre postgres et le client
docker network disconnect ddia-net ddia-postgres
# Observer : timeout ? erreur ? réessai automatique ?
docker network connect ddia-net ddia-postgres
```
