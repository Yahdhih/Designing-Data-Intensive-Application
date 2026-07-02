# Jour 03 — Ch.1 : Scalability (scalabilité)

📖 Lecture · ~45 min de lecture + 15 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 1, section « Scalability » (du début de la section jusqu'à la fin)

C'est la section la plus riche de Ch.1. Elle couvre comment **mesurer** la charge, l'étude de cas Twitter, et comment **mesurer** les performances (throughput, latence, percentiles).

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, réponds AVANT d'ouvrir le livre :

1. Quand un ingénieur dit « ce système ne scale pas » — qu'est-ce que ça veut dire concrètement ?
2. Tu connais Kafka. Comment Kafka gère-t-il la montée en charge ? C'est du horizontal scaling ou du vertical scaling ?
3. Tu as entendu parler du p99 de latence. Pourquoi est-ce plus utile que la latence moyenne ?

---

## 📚 Points à remarquer pendant la lecture

- La définition de **load parameters** — ce sont les variables qui décrivent la charge d'un système. Pour Twitter, lesquelles choisit Kleppmann ?
- L'étude de cas Twitter : **2 approches pour le fan-out** des tweets. Comprends les deux schémas.
- La distinction **throughput** vs **latence** — ce sont deux métriques orthogonales
- **Percentiles** : p50, p95, p99, p999 — pourquoi le p999 est parfois crucial (SLO)
- Le concept de **tail latency amplification** dans les architectures de microservices

---

## ✏️ Exercices (15 min)

### Ex 1 — Schéma Twitter (7 min)
Sans regarder le livre, dessine (ou décris) les **2 approches** de fan-out que Kleppmann explique pour Twitter :
- Approche 1 (pull à la lecture)
- Approche 2 (push à l'écriture — home timeline cache)

Pour chacune, note : quel est le compromis principal ?

### Ex 2 — Percentiles : explique le paradoxe (5 min)
Kleppmann donne un exemple de tail latency amplification dans les services distribués.  
Reformule ce problème dans tes propres mots : pourquoi une requête qui appelle N services a-t-elle une probabilité élevée de toucher un p99 quelque part ?

### Ex 3 — Connexion à ton stack (3 min)
Tu utilises OpenSearch. Quel serait un bon **load parameter** pour décrire la charge sur un cluster OpenSearch ? Et quelle métrique de performance surveillerais-tu en priorité — throughput ou p99 ?

---

## ✅ Terminé quand

- [ ] Lecture de la section « Scalability » terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (schéma Twitter 2 approches) fait
- [ ] Ex 2 (percentiles + tail latency) expliqué
- [ ] Ex 3 (connexion OpenSearch) fait
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.1 — Maintainability : opérabilité, simplicité, évolutivité. Puis résumé complet Ch.1.
