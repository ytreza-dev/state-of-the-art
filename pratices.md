# A discuter (inbox)

- Tests
    - Définir notre ubiquitous language sur ce que sont les tests (avoir peut-être une section dédiée voire même un fichier à part)
    - Minimiser les tests e2e et les tests d'intégration
    - On entend quoi par test "rapide"
    - Préciser comment un stub parametré s'utiliser (feed vs constructor vs etc.)
- Conventions
    - Nommage
        - Repository / DataSource etc.
- Architecture
    - Définir un ensemble d'architectures permettant de répondre avec un minimum de code au besoin
    - Quels raccourcis se permet-on sur une archi ?
    - Rendre les morceaux de code modulaires (création de librairie)
    - Choisir une manière de représenter l'orgnaisation des répertoires (vertical architecture, etc...)
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
    - Linter/Prettier 

- A part
    - pour le futur, mettre en place l'event sourcing et devenir expert dessus
    - déterminer des experts sur chaque pratique
    - Un référentiel de pratiques générale (puis par langage / stack ?)
        - Avantage : on peut filer ce référentiel aux clients. Ca montre qu'on ne fait pas les choses au hasard et leur permet de reprendre avec le contexte du pourquoi telle ou telle pratique
    - On peut / on doit / on ne doit pas
    - Voir via git blame le mob complet qui a participé à la modification (Jonathan)
- Management
    - Demander en permanence où en sont les membres vis-à-vis du collectif

- Collaboration
    - Qui choisi les outils (driver vs navigator)
- Outils imposés
    - mob.sh
- Notre définition de CQRS / séparer read & write?

# Objectif du doc

[A préciser ...]

# Ubiquitous Language

# Battle


## Stratégie de test

### Backend

#### Controllers
 
Nous utilisons du contract testing pour nous assurer du bon comportement de nos controllers.
- Une vraie requête HTTP est réalisée sur un serveur lancé par la suite de test.
- Dans le monde du write, nous utilisons un Spy de notre use case.
- Dans le monde du read, nous utilisons un Stub parametré de notre use case. Nous dissocions la valeur retournée attendue de la valeur retournée parametrée dans le Stub. Le changement de l'un n'entraîne pas le changement de l'autre. Cela permet de garantir le contrat même en cas de renommage

#### Hexagon

Nous appliquons la stratégie F.I.R.S.T. (voir chapitre 9 de Clean Code, section "F.I.R.S.T") pour la création de ces tests.

#### Infrastructure

Très peu de test pour conserver une vitesse d'exécution "relativement" correcte.
Eviter d'avoir des tests qui couvrent de la logique -> ca voudrait dire que la logique aurait sa place dans l'hexagon.
"Ce sont des tests de communication"
Nous essayons de respecter F.I.R.S.T.

Infra externe :
Infra interne : 

**** A compléter la prochaine fois ****


### Frontend




## Les tests doivent être rapides

Jonathan: Pour pouvoir les lancer continuellement
Fred: Avoir un feedback que c'est cassé rapidement
Dimitri: Pour écrire du code de prod rapidement

Dépend de [inbox: On entend quoi par test "rapide"]

# En cours de test

## Le terme use case est viable dans la lecture et l'écriture

Accéder à mon panier et ajouter des articles à mon panier sont deux cas d'utilisation de l'application. Nous choisissons donc d'utiliser le terme "use case" pour ces deux opérations

## Utiliser Git Gamble

Dimitri et Jonathan vont l'essayer

# Validées

## Systématiser la création d'un hexagon

Que ce soit dans la lecture ou l'écriture, nous avons choisi de systématiser la création d'un hexagon (port + use case).
C'est très rapide à mettre en place et ça facilite la testabilité notamment à gauche tout comme la stabilité dans son ensemble.

Nous avons conscience que ça fait émerger un test à gauche très similaire au test d'hexagon (je m'assurer que j'ai bien collaborer avec mon port)

## Séparer le monde de la lecture de celui de l'écriture

Nous avons choisi de séparer les use cases de lecture de ceux d'écriture. Cette séparation est a minima effective dans la couche hexagonal et les secondary adapters.
Nous nous laissons libre choix de définir si les primary adapters sont concernés ou non. "It depends" 🤷‍♂️

## Notre définition de test doubles (-> a bouger dans notre UL)

Quelques liens sur lesquels on s'appuie pour notre interprétation des test doubles :
- [The Little Mocker](https://blog.cleancoder.com/uncle-bob/2014/05/14/TheLittleMocker.html)
- [Mocks Aren't Stubs](https://martinfowler.com/articles/mocksArentStubs.html)

Dummy: Pour compléter la définition d'Oncle Bob sur ce type de test double, nous avons choisi de toujours lever une erreur dans l'implémentation. Ca permet de mettre en évidence les appels non attendus à ce collaborateur et donc qu'on s'est trompé de test double

Stub: Pour compléter la définition d'Oncle Bob sur ce type de test double, nous avons choisi d'ajouter la notion de stub paramétrable. C'est-à-dire que le résultat d'exécution du stub sera parametré par le test

Spy: Pas de changement changement à la définition d'Oncle Bob sur ce type de test double. On n'impose pas de contrainte pour nous permettre de faire évoluer notre interprétation

Mock: On suggère de le remplacer par un simple Spy sur lequel le test viendra faire l'assert. Ca permet au test double de ne pas avoir de connaissance du bon comportement attendu

Fake: Test double qui permet de couvrir un cas métier particulier

InMemory: Adapter viable pour de la production et du testing si on décide de le paramétrer

## Minimiser l'utilisation des librairies de mock

Nous savons faire sans et de manière efficace. Nous préférons éviter l'implicite et créons nos propres test doubles réutilisables.

## Maintenir ce référentiel en français

Le français étant notre langue maternelle, lire et écrire dans cette langue n'ajoute pas de charge mentale.

## On timebox

Nous avons choisi de time-box nos discussions à 10 minutes par pratique. Si besoin de plus de temps, nous pouvons nous caler un point/atelier dédié.

