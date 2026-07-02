# Jour 24 — Ch.6 : Rééquilibrage + Routage des requêtes

📖 Lecture · ~45 min de lecture + 15 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 6, sections « Rebalancing Partitions » + « Request Routing » + « Summary »

Deux questions pratiques : (1) quand on ajoute ou retire un noeud, comment **migrer les données** sans bloquer le système ? (2) comment un client sait-il **sur quel noeud** envoyer sa requête ?

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, réponds AVANT d'ouvrir le livre :

1. Si tu as 3 noeuds avec 100 partitions chacun et que tu ajoutes un 4ème noeud — que doit-il se passer ? Comment éviter de tout migrer ?
2. Quand un client Cassandra fait une requête, comment sait-il à quel noeud s'adresser ?
3. Qu'est-ce que ZooKeeper fait dans un système distribué selon ta connaissance actuelle ?

---

## 📚 Points à remarquer pendant la lecture

**Rééquilibrage :**
- À éviter : `hash(key) % N` — quand N change, tout se déplace
- Stratégie 1 : **nombre fixe de partitions** — les partitions se déplacent entre noeuds (Riak, Elasticsearch)
- Stratégie 2 : **partitionnement dynamique** — les partitions se divisent ou fusionnent selon la taille (HBase, RethinkDB)
- Stratégie 3 : **proportionnel au nombre de noeuds** — Cassandra, Ketama
- Toujours faire le rééquilibrage **manuellement ou semi-automatiquement** — l'automatique peut être dangereux

**Routage des requêtes :**
- Option 1 : le client sait tout (tier of clients)
- Option 2 : un routeur de requêtes (partition-aware load balancer)
- Option 3 : n'importe quel noeud, il redirige si nécessaire
- **ZooKeeper** : registre des métadonnées (quelle partition sur quel noeud)

---

## ✏️ Exercices (15 min)

### Ex 1 — Pourquoi `hash % N` est dangereux (5 min)
Tu as 4 noeuds. La clé "user_42" → `hash("user_42") % 4 = 2` → Noeud 2.  
Tu passes à 5 noeuds. `hash("user_42") % 5 = ?`  
Calcule mentalement pourquoi **presque toutes les clés changent de noeud** lors d'un ajout de noeud.

### Ex 2 — Stratégies de rééquilibrage (7 min)

| Stratégie | Comment ça fonctionne | Avantage | Inconvénient |
|-----------|----------------------|---------|-------------|
| Nombre fixe de partitions | | | |
| Partitionnement dynamique | | | |
| Proportionnel aux noeuds | | | |

### Ex 3 — ZooKeeper dans Kafka (3 min)
Tu as utilisé Kafka avec ZooKeeper (avant KRaft). Maintenant que tu comprends Ch.6 :  
Quel rôle exact jouait ZooKeeper dans Kafka pour le routage des requêtes vers les bons brokers/partitions ?

---

## ✅ Terminé quand

- [ ] Lecture (rebalancing + request routing + Summary) terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (danger de hash % N) compris
- [ ] Ex 2 (tableau stratégies rééquilibrage) fait
- [ ] Ex 3 (ZooKeeper dans Kafka) fait
- [ ] Coché dans PROGRESS.md

## → Demain
Exercice de conception : concevoir le partitionnement d'un système réel. Puis revue Ch.6.
