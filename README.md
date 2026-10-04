# Speed Dating : qu'est-ce qui fait qu'on a envie de se revoir ?

## Le projet

Tinder constate une baisse du nombre de matchs et veut comprendre ce qui rend deux personnes intéressées l'une par l'autre. Les données viennent d'une expérience de speed dating menée entre 2002 et 2004 : chaque participant rencontre quatre minutes toutes les personnes de l'autre sexe présentes, dit s'il souhaite les revoir et les note sur six attributs (attractivité, sincérité, intelligence, humour, ambition, intérêts communs). Des questionnaires recueillent aussi ce que chacun recherche et ce qu'il pense de lui-même.

Nous avons mené une analyse exploratoire pour répondre à une question : ce que les participants déclarent rechercher correspond-il à ce qui détermine réellement leur décision ?

## Les données

- **Speed_Dating_Data.csv** : une ligne par rencontre vue par un participant. 8 378 lignes, 195 colonnes, 551 participants, 21 soirées. Décision, match, notes données au partenaire, préférences déclarées, auto-évaluation, âge, origine, ordre de passage.
- **Speed+Dating+Data+Key.doc** : le codebook qui décrit chaque colonne et les échelles. Il comporte quelques coquilles sur les noms de colonnes, le CSV fait foi.

## Comment ça marche

1. **Chargement des données.**
2. **Analyse descriptive** : participants, âges, taux de « oui » et de match, nombre de rencontres par personne, valeurs manquantes.
3. **Problématique.**
4. **Analyse exploratoire** : attributs préférés déclarés par sexe, importance déclarée contre réelle, intérêts et origine communs, validité de l'auto-évaluation, effet de l'ordre de passage.
5. **Conclusion.**

Trois choix :

- **Soirées 6 à 9 exclues des préférences déclarées** : elles notaient de 1 à 10 au lieu de répartir 100 points, les deux échelles ne se comparent pas.
- **Une ligne par participant** pour les statistiques individuelles (âge, sexe, préférences), puisque chaque personne apparaît sur autant de lignes que de rencontres.
- **Un test de Student** (il mesure si l'écart entre deux moyennes peut venir du hasard) pour confirmer que hommes et femmes n'accordent pas la même importance à l'attractivité.

Les valeurs manquantes ne sont pas remplacées : les colonnes très vides ne sont pas utilisées, les moyennes et corrélations ignorent les cases vides. Les notes étant bornées de 1 à 10, il n'y avait pas de valeur aberrante à traiter.

## Les résultats

Avant la soirée, les femmes placent l'intelligence en tête, les hommes l'attractivité. Après la rencontre, c'est l'attractivité qui décide, pour les deux sexes.

| Attribut | Points déclarés, femmes | Points déclarés, hommes | Corrélation avec le « oui » |
|---|---|---|---|
| Attractivité | 18,8 | 29,4 | 0,49 |
| Humour | 17,2 | 17,5 | 0,41 |
| Intérêts communs | 12,3 | 10,3 | 0,40 |
| Intelligence | 21,5 | 19,4 | 0,22 |
| Sincérité | 18,2 | 16,1 | 0,21 |
| Ambition | 12,0 | 7,8 | 0,18 |

- **Le taux de « oui »** passe de 6 % pour un partenaire noté 3 en attractivité à 85 % pour un partenaire noté 10. Les hommes disent oui dans 47 % des cas, les femmes dans 37 % ; 16,5 % des rencontres donnent un match.
- **L'origine commune** n'ajoute que deux points de « oui ». Avoir réellement les mêmes centres d'intérêt ne change presque rien, mais l'impression d'en avoir compte (corrélation de 0,40).
- **Les participants se surévaluent** d'environ un point sur dix, et leur auto-évaluation prédit mal la note reçue (corrélation au plus de 0,29).
- **L'ordre de passage** n'a pas d'effet, hormis un léger avantage pour le premier rendez-vous.

Ce qui déclenche un match tient à l'attractivité perçue et à une impression d'affinité immédiate, bien plus qu'aux qualités que les gens disent rechercher.

## Exécuter le projet

```
tinder/
├── 01-Speed_Dating.ipynb
├── data/raw/
│   ├── Speed_Dating_Data.csv
│   └── Speed+Dating+Data+Key.doc
└── README.md
```

Prérequis : Python 3.13 avec pandas, numpy, plotly, scipy et Jupyter (l'environnement conda `base` d'Anaconda convient). Aucune clé ni fichier `.env`. Depuis la racine du projet :

```bash
jupyter notebook 01-Speed_Dating.ipynb
```

## Limites et suites possibles

- **Une expérience de 2002-2004** sur 551 personnes jeunes (âge médian 26 ans) : rien ne garantit que les conclusions valent pour les utilisateurs de Tinder.
- **Des corrélations, pas des causes** : les six notes sont corrélées entre elles, on ne peut pas isoler l'effet propre de chaque attribut.
- **Les relances à trois semaines** sont vides à plus de 75 %, l'évolution des préférences dans le temps n'a pas pu être étudiée.
- **Suite possible** : refaire l'analyse soirée par soirée pour voir si les résultats tiennent quand le groupe change.
