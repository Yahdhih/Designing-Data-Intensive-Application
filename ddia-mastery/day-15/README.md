# Jour 15 — Ch.4 : Avro + Modes de flux de données + Résumé Ch.4

📖 Lecture + consolidation · ~40 min lecture + 20 min consolidation

---

## 📖 Lecture du jour

**Section :** Chapitre 4, section « Avro » + « Modes of Dataflow » + « Summary »

Avro est le format d'encodage de Hadoop et Kafka. Il adopte une approche différente de Protobuf : pas de field tags, le schéma est transmis séparément. Les modes de flux de données clôturent le chapitre en montrant comment l'encodage impacte l'architecture des systèmes.

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, réponds AVANT d'ouvrir le livre :

1. Avro n'a pas de field tags (contrairement à Protobuf). Comment peut-il alors gérer la compatibilité entre versions de schéma ?
2. Quels sont les 3 façons principales dont des données « circulent » dans un système distribué selon toi ?
3. Quand tu déploies une nouvelle version d'un service qui change son format de données — comment est-ce que le rolling deployment impacte les systèmes qui communiquent avec lui ?

---

## 📚 Points à remarquer pendant la lecture

- **Avro** : le schéma du **writer** et le schéma du **reader** peuvent être différents — Avro fait la résolution
- Le **Schema Registry** dans Kafka (Confluent) : comment le schéma est stocké et transmis
- 3 modes de flux de données : via **bases de données**, via **appels de service** (REST/RPC), via **messages asynchrones** (Kafka, queues)
- Pour chaque mode : quelles contraintes de compatibilité s'appliquent ?

---

## ✏️ Exercices de consolidation Ch.4 (20 min)

### Ex 1 — Avro vs Protobuf (7 min)

| | Avro | Protobuf |
|-|------|---------|
| Field tags | Non — schéma séparé | Oui — dans le message |
| Résolution de schéma | | |
| Convient pour | | |
| Schema Registry nécessaire | | |

### Ex 2 — 3 modes de flux de données (8 min)
Dans `notes.md`, décris les 3 modes que Kleppmann identifie :
- Quelles contraintes de **backward/forward compatibility** chaque mode impose-t-il ?
- Quel mode permet le plus de flexibilité lors des déploiements ?

### Ex 3 — Résumé Ch.4 page blanche (5 min)
Ferme tout. Écris en 5 phrases ce que tu retiens de Ch.4.  
Commence par : « Ch.4 parle de... »

---

## ✅ Terminé quand

- [ ] Lecture (Avro + Modes de dataflow + Summary) terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (Avro vs Protobuf) complété
- [ ] Ex 2 (3 modes de flux) expliqués
- [ ] Ex 3 (résumé Ch.4 en 5 phrases) fait
- [ ] Coché dans PROGRESS.md

## → Demain
Revue Ch.3 + Ch.4 ensemble — rappel actif et connexions entre les deux chapitres.
