# TP IAA — Développer une application de prédiction du churn avec l’IAG

## Contexte

Une équipe commerciale souhaite identifier les clients susceptibles de résilier leur abonnement. Développez avec l’IAG une application permettant de charger un CSV, calculer un score de churn, classer les clients et exporter une sélection.

Vous parcourrez le cycle de développement, du besoin métier à une première évolution de l’application.

## Ressources

- VS Code avec Copilot en mode Agent ; Python, pandas, scikit-learn et Streamlit.
- `customer_churn.csv` : 900 lignes ; cible `Churn` (`1` = résiliation, `0` = absence de résiliation). Aucun horizon de prédiction n’est précisé.
- Skill fourni : `besoin-vers-specification`, à placer dans `.github/skills/besoin-vers-specification/SKILL.md`.

## Description des variables

| Variable | Description |
| --- | --- |
| `Names` | Nom du client ou du contact. |
| `Age` | Âge du client, en années. |
| `Total_Purchase` | Montant total des achats du client. |
| `Account_Manager` | Présence d’un responsable de compte : `1` = oui, `0` = non. |
| `Years` | Ancienneté du client, en années. |
| `Num_Sites` | Nombre de sites associés au client. |
| `Onboard_date` | Date d’entrée en relation avec le client. |
| `Location` | Adresse du client. |
| `Company` | Nom de l’entreprise du client. |
| `Churn` | Résiliation : `1` = le client a résilié, `0` = il n’a pas résilié. C’est la variable à prédire. |

## Travail à réaliser

### 1. Clarifier le besoin

Lancez le Skill dans le chat :

> /besoin-vers-specification Je veux une application pour aider les commerciaux à identifier les clients à rappeler à partir de customer_churn.csv.

Répondez aux questions en jouant le responsable métier. L’entretien est limité à **cinq questions, validation comprise**. Relisez les spécifications produites dans `specifications.md`.

### 2. Préparer le développement

À partir des spécifications, demandez à l’agent quels fichiers créer, à quoi ils serviront et dans quel ordre les développer. Par exemple :

- `train.py` pour entraîner et sauvegarder le modèle ;
- `app.py` pour importer un CSV et afficher les scores ;
- `tests/` pour vérifier les traitements.

Retenez une organisation, puis demandez à l’agent de la consigner dans `AGENTS.md`, avec les règles à suivre pendant le développement. Exemple : « L’interface charge le modèle sauvegardé ; elle ne le réentraîne pas à chaque import. »

**Résultat :** un plan de travail et un fichier `AGENTS.md` qui conserve vos décisions pour la suite.

### 3. Entraîner le modèle et expliquer les résultats

Faites examiner le CSV, puis entraîner une régression logistique avec les variables `Age`, `Total_Purchase`, `Account_Manager`, `Years` et `Num_Sites`.

Demandez un découpage 80 % entraînement / 20 % test, mélangé et stratifié : les lignes du CSV sont regroupées par classe. Le prétraitement est appris uniquement sur l’entraînement ; `Churn` reste la cible.

**Deux livrables attendus :**

1. **Un modèle entraîné et sauvegardé**, qui sera utilisé par l’application à l’étape suivante.
2. **Un rapport de synthèse des résultats expliqués** : présenter les résultats obtenus et expliquer ce qu’ils signifient, notamment les résiliations détectées, celles qui sont manquées et les fausses alertes.

### 4. Construire l’application

Faites créer une interface Savec Flask qui utilise le modèle sauvegardé : l'interface doit permettre à l'utilisateur de saisir les valeurs des différents champs (Age, Num_Sites, etc.). Elle renvoie un score de churn et une alerte de type le client est fidèle ou le client va churner.


### 5. Tester et corriger

1. **Vous demandez à l’agent IAG de proposer les tests** à partir des spécifications : import d’un fichier valide, colonne manquante, export et association entre clients et scores après un tri.
2. **Vous relisez ses propositions** et choisissez les cas à tester.
3. **L’agent écrit et exécute les tests**, puis vous présente les résultats.
4. **Vous lui demandez de corriger les erreurs détectées**, puis de relancer les tests concernés.

**Résultat attendu :** les tests, leurs résultats et les corrections effectuées.

### 6. Générer la documentation

Demandez à l’agent de générer la documentation du projet dans un `README.md`, en précisant les éléments souhaités : objectif de l’application, installation, lancement et exemple d’utilisation.




