# 🖥️ Node-RED — Cerveau du poste d'exploitation

Flux Node-RED qui centralisent la télémétrie, appliquent l'automatisation, exploitent les prédictions de l'IA et exposent une API d'état.

## Contenu
- `flows.json` — flux importables dans Node-RED.

## Installation

```bash
npm install -g --unsafe-perm node-red
node-red                       # éditeur sur http://localhost:1880
```

1. Éditeur → menu ☰ → **Import** → colle le contenu de `flows.json` → *Import*.
2. Double-clique un nœud MQTT → édite le broker *HiveMQ Cloud* : hôte, port **8883**, **TLS activé**, onglet *Security* pour les identifiants.
3. Clique **Deploy**.

## Les flux (voir `docs/schema_flux_node-red.png`)

| Nœud | Rôle |
|---|---|
| `mqtt in` **Capteurs** (`smarthome/+/+`) | réception de la télémétrie |
| `function` **Parser capteurs** | écrit l'état dans le contexte (`flow.state`) |
| `function` **Automatisation** | 4 règles → commandes MQTT |
| `mqtt in` **Prédictions IA** (`smarthome/predictions/+`) | reçoit les prédictions du module Colab |
| `mqtt in` **Config capteurs** | registre des capteurs (ajout depuis le HUD) |
| `http in` **/api/state** | expose l'état courant en JSON |

## Règles d'automatisation
1. **Éclairage auto** — présence la nuit → `light/set`.
2. **Alerte intrusion** — présence en mode absent (garage / terrasse) → `alerts`.
3. **Chauffage anticipé** — prédiction `temp_next < 19 °C` → `heating/set`.
4. **Routine café** — prédiction présence cuisine élevée le matin → `coffee/set`.

## Servir le dashboard via Node-RED *(optionnel)*
Place `dashboard-hud/index.html` dans un dossier statique et ajoute dans `~/.node-red/settings.js` :
```js
httpStatic: '/chemin/vers/dashboard-hud',
```
Le HUD est alors disponible sur `http://localhost:1880/index.html`.
