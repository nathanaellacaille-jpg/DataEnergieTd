# Clustering de Courbes de Charge Électrique

Segmentation non supervisée de profils de consommation utilisant K-Means et l'ACP.

## Objectif

Ce projet transforme des timeseries brutes (puissance au pas 30 minutes) en segments clients intelligibles. L'objectif principal est de distinguer les Résidences Principales (RP) des Résidences Secondaires (RS) et d'identifier les profils de chauffage électrique, en se basant uniquement sur la structure temporelle des consommations.

## Méthodologie

Le pipeline de traitement des données suit les étapes suivantes :

1.  **Prétraitement** : Conversion de la puissance (kW) en énergie journalière (kWh).
2.  **Création de variables (Feature Engineering)** :
    * [cite_start]**Scoring d'activité** : Définition d'un seuil de présence basé sur le quantile 20% des consommations journalières positives [cite: 748-750].
    * [cite_start]**Saisonnalité** : Calcul des taux d'occupation par saison (Hiver vs Été) [cite: 762-793].
    * [cite_start]**Continuité** : Analyse des séquences de jours actifs consécutifs ("runs") pour différencier l'usage sporadique de l'usage continu [cite: 815-832].
3.  [cite_start]**Modélisation** : Algorithme K-Means ($k=3$) appliqué sur les variables normalisées (StandardScaler) [cite: 853-854].
4.  [cite_start]**Visualisation** : Projection des clusters sur un plan 2D via une ACP (Analyse en Composantes Principales) [cite: 688-697].

## Résultats

L'analyse a permis d'isoler trois profils comportementaux distincts :

![Projection ACP](images/clustering_results.png)

### Profils des clusters (Heatmap)

![Heatmap des profils](images/clustering_heatmap.png)

* **Cluster 0 (Résidences Secondaires)** : Forte consommation estivale, activité quasi-nulle en hiver.
* **Cluster 1 (Résidences Principales Stables)** : Consommation régulière toute l'année, faible sensibilité saisonnière.
* **Cluster 2 (Résidences Principales à Chauffage Électrique)** : Forte activité hivernale et continuité élevée.

## Installation et exécution

1.  Cloner le dépôt :
    ```bash
    git clone [https://github.com/nathanaellacaille-jpg/DataEnergieTd.git](https://github.com/nathanaellacaille-jpg/DataEnergieTd.git)
    ```
2.  Installer les dépendances :
    ```bash
    pip install pandas numpy scikit-learn matplotlib seaborn
    ```
3.  Lancer le notebook d'analyse :
    ```bash
    jupyter notebook notebooks/analyse_clustering.ipynb
    ```
