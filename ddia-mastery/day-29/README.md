# Jour 29 — Ch.7 : Lost Updates (mises à jour perdues)

📖 Lecture · ~40 min de lecture + 20 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 7, section « Preventing Lost Updates »

Le **lost update** est l'anomalie de concurrence la plus fréquente en pratique : deux transactions lisent la même valeur, la modifient, et l'une écrase l'autre. Kleppmann présente 4 solutions — de la plus simple à la plus robuste.

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, réponds AVANT d'ouvrir le livre :

1. Voici le scénario classique :
   - T1 : lit x = 100, calcule x+10, écrit x = 110
   - T2 : lit x = 100 (en même temps), calcule x+20, écrit x = 120
   - Résultat final : x = 120. Qu'est-ce qui aurait dû être le résultat ?
2. Comment résoudrais-tu ce problème sans transaction ? (Ex : avec un mécanisme de verrouillage)
3. Connais-tu une opération SQL qui fait « lire + modifier + écrire » en une seule étape atomique ?

---

## 📚 Points à remarquer pendant la lecture

- **Read-modify-write cycle** : le pattern qui crée le lost update (lire, modifier en mémoire, écrire)
- 4 solutions que Kleppmann présente :
  1. **Opérations atomiques** : `UPDATE counter = counter + 1` (pas de read-modify-write)
  2. **Verrouillage explicite** : `SELECT FOR UPDATE` (pessimiste)
  3. **Détection automatique** : la BDD détecte et annule (optimiste) — Postgres le fait en Repeatable Read
  4. **Compare-and-set** : écrire seulement si la valeur n'a pas changé depuis la lecture
- Pourquoi le compare-and-set peut échouer dans certains cas (BDD sans snapshot isolation)

---

## ✏️ Exercices (20 min)

### Ex 1 — 4 solutions : tableau (10 min)

| Solution | Mécanisme | Exemple SQL | Optimiste/Pessimiste | Limite |
|----------|-----------|-------------|----------------------|--------|
| Atomique | | `UPDATE x = x + 1` | — | |
| SELECT FOR UPDATE | | | | |
| Détection auto | | | | |
| Compare-and-set | | | | |

### Ex 2 — Quelle solution pour Kafka (5 min)
Dans Kafka Streams, quand tu fais du comptage (ex : nombre d'événements par clé), le mécanisme de state store utilise du read-modify-write sur le RocksDB local.  
Pourquoi le lost update n'est-il **pas** un problème dans ce cas précis ?  
(Indice : pense à qui peut accéder au state store d'une partition)

### Ex 3 — Scénario Wikipedia (5 min)
Deux utilisateurs éditent simultanément le même article Wikipedia.  
Quel mécanisme de prévention du lost update Wikipedia utilise-t-il selon toi ?  
Est-ce plutôt du compare-and-set, du SELECT FOR UPDATE, ou quelque chose d'autre ?

---

## ✅ Terminé quand

- [ ] Lecture (Preventing Lost Updates) terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (tableau 4 solutions) fait
- [ ] Ex 2 (Kafka + lost update) fait
- [ ] Ex 3 (Wikipedia) fait
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.7 — Write Skew et Phantoms : les anomalies que Snapshot Isolation ne peut pas prévenir.
