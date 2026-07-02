# Jour 35 — Ch.8 : Horloges non fiables

📖 Lecture · ~45 min de lecture + 15 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 8, section « Unreliable Clocks »

Si le réseau est non fiable (Ch.8 partie 1), les horloges le sont aussi. Deux machines ne partagent jamais la même heure exacte — et les conséquences pour les systèmes distribués sont profondes.

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, réponds AVANT d'ouvrir le livre :

1. Si deux serveurs se synchronisent via NTP (Network Time Protocol), à quelle précision peut-on s'y attendre ? Quelques ms ? Quelques secondes ?
2. Qu'est-ce qu'une **horloge monotone** (monotonic clock) vs une **horloge murale** (wall clock) ?
3. Si tu utilises les timestamps des serveurs pour ordonner des événements dans Kafka — quel problème cela pose-t-il ?

---

## 📚 Points à remarquer pendant la lecture

- **Time-of-day clock** (horloge murale) : peut reculer à cause de la synchronisation NTP — **ne jamais l'utiliser pour mesurer des durées**
- **Monotonic clock** : toujours croissante — convenable pour mesurer des intervalles de temps
- **Drift** des horloges : les quartz dérivent de quelques ppm → en 30 jours, plusieurs secondes d'erreur sans NTP
- **Précision NTP** : en pratique 10-100ms sur Internet, 1ms sur réseau local
- **Last Write Wins et les timestamps** : dangereux si deux horloges ne sont pas synchronisées — une écriture « plus ancienne » peut écraser une écriture « plus récente »
- **Logical clocks** (Lamport timestamps) : pas besoin d'horloge murale — juste un ordre des événements
- **Google TrueTime** : l'approche de Spanner — borner l'incertitude temporelle plutôt que l'éliminer

---

## ✏️ Exercices (15 min)

### Ex 1 — Last Write Wins et les timestamps (7 min)

Scénario : 2 serveurs A et B. L'horloge de B est en avance de 100ms sur A.

```
t=0    Client 1 → Serveur A : écrit x = "alice"   (timestamp local : 1000ms)
t=50ms Client 2 → Serveur B : écrit x = "bob"     (timestamp local : 1100ms)
```

Si on utilise LWW (Last Write Wins basé sur timestamp) :
- Quelle valeur « gagne » ?
- Est-ce que c'est correct ? Qui a écrit en dernier réellement ?

### Ex 2 — Logical clocks vs physical clocks (5 min)

Explique en 3 phrases pourquoi les **Lamport timestamps** (logical clocks) résolvent le problème d'ordre sans avoir besoin d'horloge précise.  
Quelle information un Lamport timestamp capte-t-il qu'un timestamp physique ne capte pas ?

### Ex 3 — Kafka et les timestamps (3 min)
Les messages Kafka ont un champ `timestamp`. Par défaut, c'est le timestamp du producteur ou du broker ?  
Maintenant que tu comprends les risques des horloges non fiables — dans quel cas cette valeur peut-elle être trompeuse ?

---

## ✅ Terminé quand

- [ ] Lecture (Unreliable Clocks) terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (LWW + timestamps) fait
- [ ] Ex 2 (logical vs physical clocks) fait
- [ ] Ex 3 (Kafka timestamps) fait
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.8 — Processus qui peuvent geler + Vérité, mensonges et connaissance dans les systèmes distribués. La philosophie des systèmes distribués.
