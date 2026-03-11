# Prédiction du salaire total en carrière en NBA (1985–2018)

## Objectif
Ce projet vise à prédire le salaire total gagné au cours de la carrière d’un joueur NBA à partir d’informations individuelles sur les joueurs, entre 1985 et 2018.
Le principal défi était d’éviter la fuite temporelle (temporal leakage), car le jeu de données mélange des variables au niveau de la saison et des variables au niveau de la carrière.
**Pour résoudre ce problème, j’ai reformulé l’objectif : au lieu de prédire le salaire par saison, j’ai choisi de prédire le salaire total en carrière**.

## Dataset
- Source : Kaggle — NBA Player Salaries (1985–2018) : https://www.kaggle.com/datasets/ulrikthygepedersen/nba-player-salaries/data?select=salaries_1985to2018.csv  
- Fichiers principaux : salaries_1985to2018.csv et players.csv
- Contient l’historique des salaires des joueurs, les informations d’identification et biographiques ainsi que les statistiques cumulées de carrière.
- Combine des variables au niveau de la saison et au niveau de la carrière  

## Approche
### Préparation des données
- Importation et exploration des deux jeux de données
- Fusion de salaries_1985to2018.csv et players.csv
- Conservation uniquement des variables au niveau de la carrière, avec agrégation de certaines caractéristiques liées à des saisons spécifiques lorsque nécessaire
- Nettoyage des données, imputation des valeurs manquantes et suppression des colonnes présentant trop de valeurs manquantes
- Détection et plafonnement des valeurs extrêmes afin de limiter l’impact des outliers
- Application du one-hot encoding (numérisation des variables catégorielles) pour la régression linéaire
- Conservation de la gestion native des variables catégorielles pour XGBoost lorsque cela était possible



### Modélisation

J’ai entraîné et comparé deux modèles de régression : la régression linéaire, choisie comme baseline simple et interprétable, et XGBoost, sélectionné pour sa plus grande flexibilité et sa capacité à modéliser des relations plus complexes.  

### Transformations des données

La variable cible (variable Y "Total_salary") était fortement asymétrique à droite:  
<img width="1046" height="880" alt="image" src="https://github.com/user-attachments/assets/43c4300e-62e1-4d6d-97ce-9f0da182c3c1" />
J’ai donc appliqué une transformation logarithmique sur la variable "Total_salary" qui permet de réduire l’asymétrie de la variable cible, de limiter l’effet des valeurs extrêmes et de rendre la modélisation plus stable.  

J’ai également testé l’application d’un StandardScaler pour la régression linéaire, mais cette mise à l’échelle n’a pas permis d’améliorer les performances du modèle. Cette dernière n'est pas nécessaire pour XGBoost qui est génralement peu sensible à l'écart des échelles.  

**J’ai donc conservé uniquement la transformation logarithmique de la variable cible**.




### Résultats
| Model | RMSE | R² | MAE | Median AE |
|---|---:|---:|---:|---:|
| XGBoost + log(y) | 4411183 | 0.9873 | 2038471 | 516751 |
| Linear Regression + log(y) | 21410359 | 0.4739 | 8901897 | 2875696 |

XGBoost + log(y) a obtenu des performances nettement supérieures à celles de la régression linéaire + log(y) sur l’ensemble des métriques d’évaluation. Il présente un RMSE, un MAE et une erreur absolue médiane beaucoup plus faibles, **ce qui indique des erreurs de prédiction globalement plus faibles**, tandis que son R² beaucoup plus élevé montre qu’**il explique une part bien plus importante de la variance des salaires**.



## Conclusion
<img width="1111" height="881" alt="image" src="https://github.com/user-attachments/assets/dc988116-c4c7-4ed4-a773-569236f27c62" />    

XGBoost a obtenu les meilleures performances globales. La plupart des points du graphique de prédiction se situent près de la ligne de référence à 45 degrés, ce qui indique une forte concordance entre les salaires prédits et les salaires réels. Quelques points correspondant aux salaires les plus élevés sont légèrement plus éloignés de cette ligne, **ce qui suggère que les valeurs extrêmes sont plus difficiles à prédire**. Globalement, le modèle est performant et fournit des prédictions fiables.
