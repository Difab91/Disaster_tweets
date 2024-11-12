L'objectif de mon projet est d'explorer et d'expérimenter différentes techniques de traitement du langage naturel (NLP) pour évaluer leur efficacité en fonction du contexte. À travers un concours Kaggle, je cherche à classifier des tweets pour distinguer ceux qui décrivent un danger réel de ceux qui sont ironiques, malgré des mots-clés souvent identiques. Par exemple :

"Attention, il y a un feu dans la forêt" (danger réel)
"J'ai plein d'énergie aujourd'hui, je suis en feu" (aucun danger)
Pour cela, je dispose d'un jeu de données d'entraînement comprenant des labels, des textes, des localisations et des mots-clés.

Solutions envisagées

I) Vectorisation et classification :

Utilisation de GloVe avec une SVM (en Spark et Python)
Utilisation de GloVe avec une régression logistique (en Spark et Python)
Utilisation de GloVe avec un perceptron multicouche (en Spark et Python)

II) Utilisation de modèles de type transformers avec fine-tuning de DistilBERT (en Spark et Python)

Je vais explorer ces méthodes successivement, en appliquant trois niveaux de tri/prétraitement différents :

Tri basique : J'effectue un tri minimal et n’utilise que le texte comme variable explicative.
Tri avancé : J'applique un tri plus poussé en supprimant les mentions et autres éléments non pertinents dans le texte, tout en gardant uniquement text comme variable explicative.
Tri complet avec variables supplémentaires : Je prends en compte le mot-clé et la localisation en plus du texte comme variables explicatives après un tri complet.

À chaque étape, j'entraîne les modèles en Spark et en Python afin de comparer les performances en termes de rapidité d'exécution et de cohérence d'utilisation, et surout pour explorer les différentes bibliothèques Spark et Python. Pour l'entrainement en Python, je génère les vecteurs dans Spark et les importe ensuite dans l'environnement Python standard.

Pour la vectorisation, j'ai choisi un pipeline basé sur GloVe, qui m'a semblé être la méthode la plus adaptée à ce type de classification de tweets (aprés documentation, qui était aussi le but de ce travail) . Contrairement au TF-IDF, qui privilégie les mots-clés, et  Word2Vec étant sensiblement similaire.

Note : Ce projet est purement exploratoire et n'a aucun objectif concret/buisness. Il s'agit uniquement d'une démarche de recherche pour approfondir mes connaissances et expérimenter différentes méthodes pour me faire progresser.

Résultats sur les données de test
Voici les résultats obtenus selon la formule de F1 (F1=2∗précision∗rappel/(précision+rappel), avec précision=VP/(VP+FP) et rappel=VP/(VP+FN)) :


| TRI          | Plateforme | GloVe + SVM | GloVe + RL | GloVe + MLP | Transformers (DistilBERT) |
|--------------|------------|-------------|------------|-------------|----------------------------|
| basique      | Python     |             |            |             |                            |
|              | Spark      |   0.78577   |  0.78026   |             |                            |
| avancé       | Python     |             |            |             |                            |
|              | Spark      |             |            |             |                            |
|with loc,key  | Python     |             |            |             |                            |
|              | Spark      |             |            |             |                            |

Pour en savoir plus sur mes méthodes d'entraînement, mes optimisations et les traitements appliqués aux données, je vous invite à consulter directement le code associé.


conclusion: 
