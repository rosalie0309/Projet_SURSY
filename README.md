# Projet\_SURSY
Projet de stage M1, réalisé au CIRAD (Montpellier, France)

### 1. Contexte du projet

**SURSY** mis pour SURveillance Syndromique est un projet visant à améliorer la détection précoce des maladies touchant les plantes.
L’un des défis majeurs de la veille syndromique en santé végétale est la rareté et la diversité limitée des données textuelles disponibles.

### 2. Objectif général du projet

Il est donc question de développer une approche robuste de classification et d’augmentation de données textuelles pour la veille syndromique en santé végétale.
Le projet a été structuré en trois phases principales.
Dans ce dépôt, nous détaillons principalement les phases 1 et 2.

### 3. Phase1 : Classification par thématique 

### 3.1 Objectif
Classer les articles en trois thématiques :
**SA** : Santé Animale
**SV** : Santé Végétale
**SP** : Santé Publique

### 3.2 Données et principaux défis
Le principal défi à cette étape était de trouver un moyen d’équilibrer efficacement les données entre les thématiques.
Cet équilibrage ne pose pas de problème particulier, car dans un contexte réel, on peut supposer qu’il existe un volume comparable d’articles dans les trois thématiques (SA, SV, SP).
Ce constat diffère de la classification par type (phase 2), où l’équilibrage est plus critique.

Pour remédier au déséquilibre initial — avec SA et SP sur-représentées par rapport à SV — nous avons appliqué deux stratégies de sélection :
- **Approche UMAP + K-Means** : représentation vectorielle des articles avec UMAP, clustering avec K-Means, puis sélection d’articles dans chaque cluster pour maximiser la diversité.
- **Approche par maladie** : regroupement des articles par maladie, puis sélection équilibrée par maladie. Si une maladie disposait de peu d’articles, tous ses articles étaient conservés.


### 3.3 Approche de classification appliquéé qui a mieux fonctionné
Plusieurs méthodes ont été testées. La meilleure performance a été obtenue avec :
- Vectorisation : SBERT (all-MiniLM-L6-v2)
- Classifieur : Perceptron multicouches (MLP)
  
Ces approches sont détaillées dans :
- *classification_avec_data_umap&kmeans.ipynb* (approche 1)
- *classification_avec_data_par_maladie.ipynb* (approche 2)

### 3.4. Résultats de la phase 1
À l’issue de cette phase les résultats sont:
- Modèle final retenu : **SBERT + MLP** entraîné sur les données issues de l’approche 1.

- Trois jeux de données conservés:
  - Jeu original 
  - Jeu équilibré via UMAP + K-Means
  - Jeu équilibré via sélection par maladie

  ### 4. Phase 2: Classification binaire VS / NVS

  ### 4.1 Objectif
Classer les articles selon leur pertinence pour la veille syndromique (*type_article*) :
- **VS** : Veille Syndromique
- **NVS** : Non Veille Syndromique

  ### 4.2 Les données
  Contrairement à la phase 1, le déséquilibre entre classes est problématique ici. En effet, la classe VS est sous-représentée.
