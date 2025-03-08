# SampleSuperstore - Analyse Exploratoire de Données (EDA)

## Description du Projet

Ce projet consiste en une analyse exploratoire de données (EDA) sur un jeu de données provenant d'un supermarché fictif appelé "SampleSuperstore". L'objectif principal est d'explorer les données pour en extraire des insights pertinents, identifier des tendances, et proposer des recommandations stratégiques pour améliorer les performances de l'entreprise.

Le jeu de données contient des informations sur les ventes, les profits, les remises, les catégories de produits, les régions, les segments de clients, et bien d'autres variables. L'analyse est réalisée en utilisant Python avec des bibliothèques telles que Pandas, Seaborn, Matplotlib, et Scikit-learn pour le clustering.

---

## Structure du Projet

Le projet est structuré en plusieurs étapes clés :

1. **Importation des données** : Chargement du jeu de données et vérification des informations générales.
2. **Nettoyage des données** : Identification et suppression des doublons, vérification des valeurs manquantes.
3. **Analyse des profits** : Calcul des profits positifs et négatifs, identification des transactions atypiques.
4. **Analyse des ventes et des profits par région** : Comparaison des performances par région.
5. **Analyse des variables catégorielles** : Exploration des modes de livraison et des segments de clients.
6. **Impact des remises sur les profits** : Analyse de l'effet des remises sur les profits et identification des catégories de produits où les remises sont trop élevées.
7. **Clustering des clients** : Utilisation de l'algorithme K-means pour identifier les clients qui profitent principalement des périodes de remise.

---

## Visualisation des Données

### 1. **Distribution des Profits**
   - **Graphique** : Un histogramme ou un boxplot pour visualiser la distribution des profits.
   - **Insight** : Identifier les transactions avec des profits très élevés ou très faibles.
   - **Code Exemple** :
     ```python
     import seaborn as sns
     import matplotlib.pyplot as plt

     sns.boxplot(x=df_cleaned['Profit'])
     plt.title("Distribution des Profits")
     plt.xlabel("Profit")
     plt.show()
     ```
    
    ![Boxplot_colonne_profit]([Boxplot_colonne_profit.png](https://github.com/Marc-Gael/Supersotore_EDA/blob/main/Assets/Boxplot_colonne_profit.png))
    

### 2. **Ventes et Profits par Région**
   - **Graphique** : Un barplot pour comparer les ventes et les profits par région.
   - **Insight** : Identifier les régions les plus performantes.
   - **Code Exemple** :
     ```python
     sns.barplot(x='Region', y='Sales', data=df_cleaned, estimator=sum)
     plt.title("Ventes par Région")
     plt.show()

     sns.barplot(x='Region', y='Profit', data=df_cleaned, estimator=sum)
     plt.title("Profits par Région")
     plt.show()
     ```

### 3. **Segments de Clients**
   - **Graphique** : Un pie chart pour visualiser la répartition des segments de clients.
   - **Insight** : Comprendre la distribution des clients entre Consumer, Corporate, et Home Office.
   - **Code Exemple** :
     ```python
     df_cleaned['Segment'].value_counts().plot(kind='pie', autopct='%1.1f%%')
     plt.title("Répartition des Segments de Clients")
     plt.show()
     ```

### 4. **Impact des Remises sur les Profits**
   - **Graphique** : Un histogramme pour visualiser le nombre de transactions par discount.
   - **Insight** : Identifier les niveaux de remise qui maximisent les profits.
   - **Code Exemple** :
     ```python
     plt.figure(figsize=(8, 5))
     sns.histplot(df_cleaned["Discount"], bins=20, kde=True, color="blue")

    # Ajouter des labels et un titre
     plt.xlabel("Discount (%)")
     plt.ylabel("Nombre de transactions")
     plt.title("Distribution des Discounts dans le Dataset")
     plt.show()
     ```

    ![Boxplot_colonne_profit](Distribution_des_discounts_dans_le_dataset.png)
    

### 5. **Clustering des Clients avec K-means**
   - **Graphique** : Un scatter plot pour visualiser les clusters de clients basés sur leur comportement d'achat pendant les périodes de remise.
   - **Insight** : Identifier les clients qui achètent principalement pendant les périodes de remise.
   - **Code Exemple** :
     ```python
     from sklearn.cluster import KMeans
     import matplotlib.pyplot as plt

     # Sélection des variables pertinentes pour le clustering
     X = df_cleaned[['Discount', 'Sales']]

     # Application de l'algorithme K-means
     kmeans = KMeans(n_clusters=3, random_state=42)
     df_cleaned['Cluster'] = kmeans.fit_predict(X)

     # Visualisation des clusters
     sns.scatterplot(x='Discount', y='Sales', hue='Cluster', data=df_cleaned, palette='viridis')
     plt.title("Clustering des Clients basé sur les Remises et les Ventes")
     plt.xlabel("Remise (%)")
     plt.ylabel("Ventes ($)")
     plt.show()
     ```

---

## Résultats Clés

### 1. **Transactions avec profits positifs et négatifs**
   - **Transactions avec profits positifs** : 8043
   - **Transactions avec profits négatifs** : 1869

### 2. **Ventes totales et profit net**
   - **Ventes totales** : 2,296,195.59$
   - **Profit net** : 286,241.42$
   - **Pourcentage du profit net dans le CA** : 12.47%

### 3. **Ventes et profits par région**
   - **Ventes par région** :
     - West : 725,255.64$
     - East : 678,435.20$
     - Central : 500,782.85$
     - South : 391,721.91$
   - **Profits par région** :
     - West : 108,329.81$
     - East : 91,506.31$
     - South : 46,749.43$
     - Central : 39,655.88$

### 4. **Modes de livraison les plus utilisés**
   - **Standard Class** : 5955
   - **Second Class** : 1943
   - **First Class** : 1537
   - **Same Day** : 542

### 5. **Segments de clients les plus fréquents**
   - **Consumer** : 5183
   - **Corporate** : 3015
   - **Home Office** : 1779

### 6. **Impact des remises sur les profits**
   - Les remises ont un impact significatif sur les profits. Les transactions avec des remises élevées (supérieures à 20%) ont tendance à générer des profits négatifs.
   - Les catégories de produits où les remises sont trop élevées doivent être revues pour éviter des pertes.

### 7. **Clustering des Clients**
   - **Cluster 0** : Clients qui achètent **uniquement avec remise**.
   - **Cluster 1** : Clients qui profitent **modérément des remises**.
   - **Cluster 2** : Clients qui achètent **principalement sans remise**.

---

## Recommandations Stratégiques

1. **Optimisation des remises** :
   - Réduire les remises sur les catégories de produits où elles entraînent des pertes.
   - Cibler les remises sur les produits à forte marge pour maximiser les profits.

2. **Amélioration des performances par région** :
   - Concentrer les efforts marketing sur les régions les plus rentables (West et East).
   - Analyser les causes des faibles performances dans la région Central et proposer des actions correctives.

3. **Segmentation des clients** :
   - Développer des campagnes marketing ciblées pour les segments de clients les plus rentables (Consumer).
   - Proposer des offres personnalisées pour fidéliser les clients Corporate et Home Office.

4. **Analyse approfondie des transactions atypiques** :
   - Identifier les causes des transactions avec des profits négatifs et proposer des solutions pour les éviter.
   - Surveiller les transactions avec des profits très élevés pour comprendre les facteurs de succès et les reproduire.

5. **Amélioration des modes de livraison** :
   - Promouvoir les modes de livraison les plus rentables (Standard Class).
   - Réduire les coûts associés aux modes de livraison moins utilisés (Same Day).

6. **Stratégies pour les clients sensibles aux remises** :
   - **Cluster 0 (Clients qui achètent uniquement avec remise)** : Ces clients sont très sensibles aux promotions et attendent des offres avant d'acheter. Limitez les remises excessives pour ces clients tout en maintenant leur intérêt avec des offres personnalisées et des promotions ciblées.
   - **Cluster 1 (Clients modérés)** : Ces clients profitent occasionnellement des remises. Maintenez un équilibre entre les offres promotionnelles et les prix réguliers pour maximiser leur engagement.
   - **Cluster 2 (Clients qui achètent principalement sans remise)** : Ces clients sont moins sensibles aux remises. Proposez-leur des offres de fidélité ou des avantages exclusifs pour les encourager à acheter davantage.

---

## Technologies Utilisées

- **Python** : Langage de programmation principal pour l'analyse des données.
- **Pandas** : Bibliothèque pour la manipulation et l'analyse des données.
- **Seaborn** : Bibliothèque pour la visualisation des données.
- **Matplotlib** : Bibliothèque pour la création de graphiques.
- **Scikit-learn** : Bibliothèque pour le clustering avec K-means.
