# Jour 18 — Ch.5 : Problèmes de décalage de réplication

📖 Lecture · ~45 min de lecture + 15 min d'exercices

---

## 📖 Lecture du jour

**Section :** Chapitre 5, section « Problems with Replication Lag » (jusqu'à « Multi-Leader Replication »)

La réplication asynchrone est rapide mais crée un problème : les followers ont un **décalage** (lag) par rapport au leader. Kleppmann décrit 3 anomalies qui en résultent et leurs solutions.

---

## 🎯 Avant de lire — Prédis (5 min)

Dans `notes.md`, réponds AVANT d'ouvrir le livre :

1. Si un client écrit sur le leader et lit immédiatement sur un follower — que peut-il voir ?
2. Imagine que tu lis deux fois la même donnée depuis deux followers différents. Que peut-il se passer ?
3. Est-ce que selon toi le replication lag est un problème grave ou mineur en pratique ?

---

## 📚 Points à remarquer pendant la lecture

- **Read-your-writes (read-after-write consistency)** : l'utilisateur doit voir ses propres écritures, même si elles ne sont pas encore répliquées
- **Monotonic reads** : si un utilisateur lit depuis plusieurs followers, il ne doit pas voir une donnée « dans le passé » après l'avoir vue dans le futur
- **Consistent prefix reads** : les lectures doivent respecter l'**ordre causal** des écritures
- Pour chaque anomalie : la solution que Kleppmann propose (lire depuis le leader, mémoriser le timestamp, etc.)

---

## ✏️ Exercices (15 min)

### Ex 1 — 3 anomalies en 1 tableau (8 min)

| Anomalie | Description (1 phrase) | Exemple concret | Solution |
|----------|----------------------|----------------|---------|
| Read-your-writes | | | |
| Monotonic reads | | | |
| Consistent prefix reads | | | |

### Ex 2 — Scénario Twitter (4 min)
Tu tweetes quelque chose. Tu actualises immédiatement ta page et ton tweet n'apparaît pas.  
Quelle anomalie est-ce ? Comment Twitter pourrait-il la résoudre ?

### Ex 3 — Compromis fondamental (3 min)
La réplication asynchrone est plus performante mais crée des anomalies.  
La réplication synchrone est cohérente mais plus lente.  
Quel compromis choisirais-tu pour un système comme Kafka ? Pour une base de données bancaire ?

---

## ✅ Terminé quand

- [ ] Lecture (Problems with Replication Lag) terminée
- [ ] Prédictions remplies avant lecture
- [ ] Ex 1 (tableau 3 anomalies) fait
- [ ] Ex 2 (scénario Twitter) fait
- [ ] Ex 3 (compromis) noté
- [ ] Coché dans PROGRESS.md

## → Demain
Ch.5 — Réplication multi-leader : que se passe-t-il quand plusieurs noeuds acceptent des écritures ?
