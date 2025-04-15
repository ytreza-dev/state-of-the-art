# A discuter (inbox)

- Tests
    - Définir quels niveaux de tests on veut implémenter selon le besoin
        - TU
        - Tests d'intégration
        - Tests E2E
    - Minimiser les tests e2e et les tests d'intégration
    - On entend quoi par test "rapide"
- Conventions
    - Nommage
        - Test double
- Architecture
    - Définir un ensemble d'architectures permettant de répondre avec un minimum de code au besoin
    - Quels raccourcis se permet-on sur une archi ?
    - Archi hexagonale, ce doit être un non événement d'en mettre une en place
    - Rendre les morceaux de code modulaires (création de librairie)
- Outillage
    - Définir, par stack, les outils qu'on préfère utiliser
        - ex : Front : Angular, un outil de state, un outil de gestion event driven, un outil d'injection de dépendances
    - De l'injection de dépendances
- Méthodologie
    - TDD
    - Déploiement continu (envisager de déployer toutes les 30 minutes)
    - Adapter contract testing
    - Avoir le moins de logique possible dans les composants
    - Des contracts tests
    - Avoir un watch mode par type de test (local vs acceptance)
    - Quand tester quoi

- A part
    - pour le futur, mettre en place l'event sourcing et devenir expert dessus
    - déterminer des experts sur chaque pratique
    - Un référentiel de pratiques générale (puis par langage / stack ?)
        - Avantage : on peut filer ce référentiel aux clients. Ca montre qu'on ne fait pas les choses au hasard et leur permet de reprendre avec le contexte du pourquoi telle ou telle pratique
    - On peut / on doit / on ne doit pas
- Management
    - Demander en permanence où en sont les membres vis-à-vis du collectif
- Collaboration
    - Qui choisi les outils (driver vs navigator)
- Outils imposés
    - mob.sh



# Objectif du doc

[A préciser ...]

# Battle

## Définir notre ubiquitous language sur ce que sont les tests

**** Reprendre ICI ****
Dimitri: https://blog.cleancoder.com/uncle-bob/2014/05/14/TheLittleMocker.html.

Dummy: Une valeur par défaut retourné non paramétrable OU throw error -> on sait qu'il ne sera pas appelé ou que son appel n'impactera rien
Stub:
    - Parametré:
    - Non parametré:
        Une valeur par défaut retourné paramétrable par le test
Spy:
    Expose la liste des méthodes avec leur paramètres appelés. Permet de s'assurer 
Fake

Mock
InMemory


## Les tests doivent être rapides

Jonathan: Pour pouvoir les lancer continuellement
Fred: Avoir un feedback que c'est cassé rapidement
Dimitri: Pour écrire du code de prod rapidement

Dépend de [inbox: On entend quoi par test "rapide"]

# En cours de test

## Utiliser Git Gamble

Dimitri et Jonathan vont l'essayer

# Validées

## Maintenir ce référentiel en français

Le français étant notre langue maternelle, lire et écrire dans cette langue n'ajoute pas de charge mentale.

## On timebox

Nous avons choisi de time-box nos discussions à 10 minutes par pratique. Si besoin de plus de temps, nous pouvons nous caler un point/atelier dédié.

