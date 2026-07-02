# Jour 34 — Ch.8 : Réseaux non fiables

📖 Lecture · ~45 min de lecture + 15 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 8, du début jusqu'à la fin de la section « Unreliable Networks »

Ch.8 est le chapitre le plus philosophique de DDIA. Après avoir étudié la réplication (Ch.5), le partitionnement (Ch.6) et les transactions (Ch.7) dans un contexte « idéal », Ch.8 brise les hypothèses : **les réseaux ne sont pas fiables, les horloges ne sont pas synchronisées, et les processus peuvent geler à n'importe quel moment**.

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, réponds AVANT d'ouvrir le livre :

1. Si tu envoies un message à un autre service et tu n'obtiens pas de réponse dans les 5 secondes — qu'est-ce que ça veut dire ? Liste toutes les interprétations possibles.
2. Quelle est la différence entre un réseau **synchrone** (comme le réseau téléphonique) et un réseau **asynchrone** (comme Internet) ?
3. Qu'est-ce qu'un **timeout** ? Quel est le problème si le timeout est trop court ? Trop long ?

---

## 📚 Points à remarquer pendant la lecture

- Les **9 choses qui peuvent mal se passer** quand on envoie un message sur le réseau (liste exhaustive de Kleppmann)
- Pourquoi un **timeout** est la seule façon de détecter une panne — mais il ne dit pas **ce qui** a échoué
- Le problème fondamental : il est **impossible de distinguer** un noeud lent d'un noeud mort
- La comparaison réseau téléphonique (circuit switching) vs Internet (packet switching) — pourquoi Internet choisit la variabilité de latence
- **Unbounded delay** : il n'y a pas de borne supérieure sur la latence réseau dans un réseau asynchrone

---

## ✏️ Exercices (15 min)

### Ex 1 — Que peut-il se passer ? (7 min)

Tu envoies une requête HTTP à un service distant. Avant de regarder la liste de Kleppmann, liste dans `notes.md` tout ce qui peut empêcher la réponse d'arriver.

Ensuite, compare ta liste avec celle de Kleppmann. Qu'est-ce qui manquait ?

### Ex 2 — Timeout : le dilemme (5 min)

Dans `notes.md`, explique :
- **Timeout trop court** : quel est le problème ? (Que peut-on faire à tort ?)
- **Timeout trop long** : quel est le problème ? (Que se passe-t-il pour l'utilisateur ?)
- Comment Kafka ou Kubernetes choisissent-ils leurs timeouts en pratique ?

### Ex 3 — Réseau téléphonique vs Internet (3 min)
Le réseau téléphonique garantit une latence bornée. Internet ne le garantit pas.  
Quelle est la raison de cette différence (hint : circuit switching vs packet switching) ?  
Et pourquoi Internet a-t-il quand même « gagné » malgré cette limitation ?

---

## ✅ Terminé quand

- [ ] Lecture (Unreliable Networks) terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (liste des pannes réseau) fait
- [ ] Ex 2 (timeout dilemme) fait
- [ ] Ex 3 (circuit vs packet switching) fait
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.8 — Horloges non fiables : NTP, monotonic clocks, problèmes d'ordre des événements dans le temps.
