# 🧠 Module IA — Google Colab

Réseaux de neurones qui apprennent les habitudes de la maison et publient des prédictions pour l'automatisation.

## Contenu
- `SmartHome_IA_Colab.ipynb` — notebook complet (collecte → entraînement → prédiction).

## Utilisation

1. Ouvre [Google Colab](https://colab.research.google.com/) → *Fichier* → *Importer un notebook* → `SmartHome_IA_Colab.ipynb`.
2. Renseigne tes identifiants HiveMQ dans la cellule **2. Configuration** (`HIVEMQ_HOST`, `HIVEMQ_USER`, `HIVEMQ_PASS`).
3. Exécute les cellules dans l'ordre (menu *Exécution → Tout exécuter*).

> 💡 Sans capteurs branchés, le notebook fonctionne en **mode démonstration** grâce à un générateur de données synthétiques : toute la chaîne IA s'exécute immédiatement.

## Ce que fait le notebook
1. **Collecte MQTT** (TLS) — abonnement à `smarthome/#`, enregistrement horodaté.
2. **Données synthétiques** — 14 jours de routines réalistes pour l'entraînement hors-ligne.
3. **Ingénierie des caractéristiques** — encodage cyclique de l'heure / du jour, indicateur week-end.
4. **Modèle A — présence par pièce** : un perceptron multicouche par pièce (apprentissage séparé).
5. **Modèle B — température (LSTM)** : prévision au pas suivant pour le chauffage anticipé.
6. **Prédiction & publication** — résultats publiés sur `smarthome/predictions/<piece>` (consommés par Node-RED et le HUD).

## Dépendances
Installées par la première cellule : `paho-mqtt==1.6.1`, `tensorflow` (préinstallé sur Colab), `scikit-learn`, `pandas`, `numpy`, `matplotlib`, `joblib`.

## Données apprises
Quatre grandeurs par pièce : **température** (°C), **présence** (0/1), **lumière** (0/1), **fenêtre** (0 = fermée, 1 = ouverte).
