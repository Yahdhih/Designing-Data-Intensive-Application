# code/02-encoding/ — Encodage & évolution de schéma

> Chapitre 4 · Jours 20, 22 · `PLAN.md` Phase 1

---

## Objectif

1. Implémenter un encodeur binaire longueur-préfixé (*length-prefixed binary encoding*)
2. Démontrer la compatibilité ascendante et descendante lors de l'évolution du schéma

---

## `encoder.py` (Jour 20)

Encodeur binaire minimal pour un message avec champs typés :

```python
# Schéma v1 : {user_id: int, name: str}
msg_v1 = encode({"user_id": 42, "name": "Alice"})

# Schéma v2 : {user_id: int, name: str, email: str}  ← champ ajouté
msg_v2 = encode({"user_id": 42, "name": "Alice", "email": "alice@example.com"})

# Compatibilité descendante : décodeur v1 lit un message v2 → ignore email
decode_v1(msg_v2)  # → {"user_id": 42, "name": "Alice"}

# Compatibilité ascendante : décodeur v2 lit un message v1 → email = None
decode_v2(msg_v1)  # → {"user_id": 42, "name": "Alice", "email": None}
```

**Lancer :**
```bash
python code/02-encoding/encoder.py
pytest code/02-encoding/test_encoder.py -v
```

**Attendu :**
- Encoder un message v1 → bytes plus petits que JSON (au moins 2× pour des champs courts)
- Décodeur v1 lit message v2 sans erreur (forward compat)
- Décodeur v2 lit message v1 sans erreur (backward compat)

**Principe implémenté :**
- Chaque champ est préfixé par : `[field_id: 1 byte][type: 1 byte][length: 2 bytes][data: N bytes]`
- Le décodeur ignore les field_id inconnus (forward compatibility)
- Les champs manquants reçoivent leur valeur par défaut (backward compatibility)

---

## `protobuf_demo.py` (Jour 22 — labo)

Même démonstration avec la vraie librairie `protobuf` Python :

```bash
pip install protobuf
python code/02-encoding/protobuf_demo.py
```

**Ce qu'on observe :**
- Taille du message v1 encodé en Protobuf vs JSON
- Ajout d'un champ optionnel → compatibilité préservée
- Changement du numéro de champ → incompatibilité silencieuse (danger !)

---

## Compromis à documenter dans `reference/tradeoffs.md`

| Format | Taille | Lisibilité | Évolution schéma | Tooling |
|--------|--------|------------|------------------|---------|
| JSON | Élevée | Excellente | Fragile (pas de contrat) | Universel |
| Protobuf | Faible | Nulle | Robuste si numéros stables | gRPC, Google |
| Avro | Faible | Nulle | Robuste (schéma enregistré) | Kafka |
| Notre encodeur | Faible | Nulle | Démonstratif | Pédagogique |
