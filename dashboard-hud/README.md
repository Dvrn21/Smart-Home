# 📊 Dashboard HUD — Tableau de bord web

Interface d'exploitation : plan de la maison en temps réel, graphes, prédictions IA et ajout de capteurs.

## Contenu
- `index.html` — application web autonome (un seul fichier).

## Utilisation

### Mode démo (immédiat)
Ouvre simplement `index.html` dans un navigateur (double-clic). Il démarre en **mode démo** : les 8 pièces sont simulées, le plan s'anime, les graphes se remplissent. Aucune configuration requise.

### Mode réel (HiveMQ)
1. Renseigne tes identifiants, au choix :
   - en haut du fichier : `const HMQ = { host:"wss://…:8884/mqtt", user:"…", pass:"…" };`
   - ou directement dans l'interface via le bouton de connexion (badge en haut à droite).
2. Décoche **Mode démo** → **Appliquer**. Le HUD se connecte en **WebSocket sécurisé (WSS, port 8884)** et affiche les données réelles.

## Pages
- **Plan** — plan des 8 pièces ; par pièce : température + indicateurs présence / lumière / fenêtre, journal d'événements.
- **Capteurs** — registre des capteurs + **formulaire d'ajout** (publie sur `smarthome/config/sensors`).
- **Données** — graphes (température par pièce, occupation, fenêtres ouvertes).
- **IA · Prédictions** — probabilité de présence par pièce, température prévue, synthèse des modèles.

## Dépendances
Chargées via CDN au moment de l'exécution : [MQTT.js](https://github.com/mqttjs/MQTT.js) et [Chart.js](https://www.chartjs.org/). Une connexion internet est nécessaire pour le mode réel.

## Sécurité
Les identifiants saisis dans `index.html` sont visibles côté client. **Ne publie pas** ce fichier avec de vrais identifiants sur un dépôt public.
