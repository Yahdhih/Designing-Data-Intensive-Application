# Jour 14 — Ch.4 : Formats d'encodage (JSON, XML, Thrift, Protobuf)

📖 Lecture · ~45 min de lecture + 15 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 4, du début jusqu'à la fin de la section sur Protobuf/Thrift (avant Avro)

Ch.4 traite de l'**encodage** des données : comment transformer des structures de données en octets pour les stocker ou les transmettre. C'est un sujet critique pour les systèmes distribués.

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, réponds AVANT d'ouvrir le livre :

1. Quels problèmes tu as rencontré (ou tu imagines) quand deux services communiquent via JSON et que l'un ajoute un nouveau champ ?
2. Qu'est-ce que la « compatibilité ascendante » et « descendante » (backward / forward compatibility) ?
3. Tu utilises probablement JSON dans tes projets. Quels sont ses problèmes selon toi ?

---

## 📚 Points à remarquer pendant la lecture

- Les problèmes de JSON/XML : pas de types stricts, taille des données, ambiguïtés (nombres, Unicode)
- **Backward compatibility** : nouveau code peut lire les données écrites par l'ancien code
- **Forward compatibility** : ancien code peut lire les données écrites par le nouveau code
- Thrift et Protobuf : les **field tags** (numéros de champs) — pourquoi c'est la clé de la compatibilité
- Comment ajouter ou supprimer un champ sans casser la compatibilité dans Protobuf

---

## ✏️ Exercices (15 min)

### Ex 1 — Tableau des formats (7 min)

| Format | Type-safe | Taille | Lisible par humain | Compatibilité évolution |
|--------|-----------|--------|--------------------|-----------------------|
| JSON | | | | |
| XML | | | | |
| Thrift/Protobuf | | | | |

### Ex 2 — Les field tags expliqués (5 min)
Dans Protobuf, chaque champ a un **tag numérique** (ex: `field 1`, `field 2`).  
Pourquoi ce numéro est-il plus important que le nom du champ pour la compatibilité ?  
Que se passe-t-il si tu changes le numéro d'un champ existant ?

### Ex 3 — Connexion à Kafka (3 min)
Kafka utilise souvent Avro ou Protobuf pour sérialiser les messages. Maintenant que tu comprends ces formats, pourquoi éviterait-on JSON dans Kafka pour un système à fort volume ?

---

## ✅ Terminé quand

- [ ] Lecture (JSON/XML/binaire, Thrift, Protobuf) terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (tableau des formats) complété
- [ ] Ex 2 (field tags) expliqué
- [ ] Ex 3 (connexion Kafka) fait
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.4 — Avro (le format de Kafka/Hadoop) + Modes de flux de données + Résumé Ch.4.
