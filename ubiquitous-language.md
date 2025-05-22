# Objectif du document

Ce document a pour but de recenser le vocabulaire que nous utilisons quotidiennement.
Il est voué à évoluer tout comme notre compréhension des concepts. 

# Testing

## Test double

Quelques liens sur lesquels on s'appuie pour notre interprétation des test doubles :
- [The Little Mocker](https://blog.cleancoder.com/uncle-bob/2014/05/14/TheLittleMocker.html)
- [Mocks Aren't Stubs](https://martinfowler.com/articles/mocksArentStubs.html)

### Dummy

Pour compléter la définition d'Oncle Bob sur ce type de test double, nous avons choisi de toujours lever une erreur dans l'implémentation. Ca permet de mettre en évidence les appels non attendus à ce collaborateur et donc qu'on s'est trompé de test double

### Stub

Pour compléter la définition d'Oncle Bob sur ce type de test double, nous avons choisi d'ajouter la notion de stub paramétrable. C'est-à-dire que le résultat d'exécution du stub sera parametré par le test

### Spy

Pas de changement changement à la définition d'Oncle Bob sur ce type de test double. On n'impose pas de contrainte pour nous permettre de faire évoluer notre interprétation

### Mock

On suggère de le remplacer par un simple Spy sur lequel le test viendra faire l'assert. Ca permet au test double de ne pas avoir de connaissance du bon comportement attendu

### Fake

Test double qui permet de couvrir un cas métier particulier

### InMemory

Adapter viable pour de la production et du testing si on décide de le paramétrer