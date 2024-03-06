# tp2_airpumtl
Au cours de ce projet, nous avons travaillé avec des données en temps réel sur la qualité de l'air (IQA). La première étape a consisté à nettoyer et préparer les données pour une analyse ultérieure.

J'ai commencé par nettoyer le tableau de données IQA en modifiant et en corrigeant les noms des stations, ainsi qu'en les organisant de manière logique, de la station 1 à la station 11. Cette tâche a été réalisée à l'aide des transformateurs FME tels que _StringReplacer_ pour renommer les attributs, et _Sorter_ pour organiser les stations par numéro.&#x20;

Ensuite, j'ai procédé à la reprojection des données pour garantir leur cohérence spatiale. L'outil _Reprojector_ a été utilisé pour cette étape, permettant de convertir les données dans un système de coordonnées spatial commun, assurant ainsi une analyse géospatiale précise.&#x20;

Par la suite, j'ai travaillé avec les données des stations de qualité de l'air (IQA), où j'ai également entrepris de renommer les stations pour une meilleure compréhension. Après avoir effectué cette tâche, j'ai une nouvelle fois procédé à la reprojection de l'ensemble des données.

Une autre étape importante a été la connexion des données traitées à une base de données, facilitant ainsi leur stockage et leur utilisation ultérieure. Pour ce faire, j'ai utilisé les outils de connexion à la base de données. En parallèle, j'ai travaillé avec les limites administratives des agglomérations. Après avoir utilisé l'outil _AttributeKeeper_ pour supprimer les parties inutiles pour mon travail, j'ai intégré ces données à la base de données principale, suivie d'une reprojection pour garantir leur compatibilité avec les autres données. Pour affiner mon analyse, j'ai filtré les stations par arrondissement, puis j'ai effectué une jointure spatiale pour associer les données de qualité de l'air aux limites administratives correspondantes. Encore une fois, j'ai reprojeté les données pour assurer leur cohérence spatiale.

Enfin, j'ai travaillé avec une liste de stations au format CSV, que j'ai classée par ordre de 1 à 11 et nettoyée en supprimant les stations fermées. Après avoir renommé les stations, j'ai fusionné tous les tableaux de données pour obtenir un seul ensemble de données consolidé. Ce dernier a été reprojeté une dernière fois en utilisant le système de coordonnées _EPSG 3857_.

Or, pour travailler au mieux avec les données de station de la qualité de l’air dans QGIS il est nécessaire de les transformer dans FME en données raster et les insérer dans une grille H3 pour obtenir une représentation plus homogène de la qualité de l’air à Montréal. Nous ne sommes pas parvenu à réaliser cette manipulation.

Ensuite, concernant les données de Traffic routier, elles se sont avéré plus compliqué que nous estimions à nettoyer. Ces données étaient composé d’énormément de données car elle considérées les villes de Calgary, Toronto, Ontario, en plus de celle de Montréal. De plus, pour de nombreuse dates, il n’y avait pas d’enregistrement de véhicules aux intersections de rue ce qui rendait le jeu de données incomplet. L’idée d’un traitement statistique était de remplacer les valeurs \<null> par la médiane, plus représentatif que la moyenne (pour chaque jour) calculée à l’aide du transformer _StaistiqueCalculator_. Mais je ne suis pas parvenu à  remplacer les valeurs null par leur médiane respective.

Puis, le format des coordonnées nous a posé problème pour la suite du traitement. En effet, nous n’avons pas réussi à extraire les longitude et latitude de chaque caméras car les coordonnées étaient sous un même attribut que l’on a renommé <_position>_ (sous la forme POINT (75.635335 45.63228)). Le traitement ce jeu de donnée dégradé n’a pu aboutir comme on le souhaité c’est-à-dire à le joindre spatialement au arrondissement de la ville de Montréal selon la position des caméras.&#x20;

Ainsi, nous obtenons à ce jour 3 couches dans QGIS après les avoir enregistré dans la base de données GEO7630H24, avec seulement des données vectorielles : à savoir les stations IQA, les arrondissements et les secteurs (Nord, Est, Sud, Ouest) de la ville de Montréal.

Nous avons rencontré de nombreux problème lors de ce TP2 que ce soit une mauvaise qualité des données et une sous-estimation du temps de traitement des jeux de données nécessaire pour la création d’un rendu géographique intéressant.
