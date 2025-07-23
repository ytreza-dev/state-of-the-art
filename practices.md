# Objectif du document

Nous sommes tous plutôt familiers avec la notion de bonnes et de mauvaises pratiques.
Pour autant, ce qui semble pour certains être une bonne pratique peut être l'opposé pour d'autres.
Les pratiques sont contextuelles, subjectives et changeantes.

Ce document a pour objectif de recenser, de manière non figée, nos pratiques actuelles en apportant au besoin :

- du contexte
- des "bons" et "mauvais" exemples 
- des liens vers ressources externes

# Instructions

## Préparation

Dès lors qu'une personne identifie une nouvelle pratique dont l'équipe pourrait profiter, elle l'ajoute dans [Inbox](#inbox).

Plus la description et les avantages/inconviénents sont riches, plus simple sera sa compréhension et son adoption.
Fournir également des liens vers du code source est bénéfique pour accélérer la prochaine étape.

## Revue de pratiques - Inbox

Régulièrement, nous faisons ensemble le tour des nouvelles pratiques identifiées et discutons de leur adoption ou non.

Si l'équipe est en faveur de cette pratique, elle passe dans [Validées](#validées).
Son contenu peut être enrichi de manière asynchrone ou non suite aux discussions.

Si l'équipe n'est pas en faveur de cette pratique, elle est rejetée et pourra revenir plus tard au besoin.
Il n'est pas nécessaire de la référence dans ce document.

Si toutefois l'équipe n'arrive pas à se mettre d'accord, la pratique est déplacée dans [Battle](#battle).

## Revue de pratiques - Challenge

La deuxième partie de l'atelier consiste à échanger autour des pratiques misent en battle durant la session précédente.

Chacune de ces pratiques est rediscutée et son adoption ou non suit un schéma similaire à celui indiqué précédemment.
La seule différence est la suivante :

Si l'équipe n'arrive toujours pas à se mettre d'accord, la pratique est automatiquement validée.
Cette approche permet la place au changement et à l'expérimentation pour aller chercher du feedback constructif basé sur l'expérience. 

## Évolution d'une pratique

N'importe qui est libre de compléter une pratique en y ajoutant du contexte, des exemples ou des liens pour en faciliter la compréhension et l'adoption.

# Inbox

# Ubiquitous Language

Externe / extérieur : en dehors de l'hexagone
F.I.R.S.T. : Fast, Independent, Repeatable, Self-Validating, Timely - Clean Code - Chapitre 9
SUT : System Under Test : Dans une suite de test, représente la partie du code que l'on souhaite tester

# Battle

- les différentes couches du front

JL :

- couche infrastructure (secondary)
- couche applicative (hexagon) (données, et les comportements liés à l'application) (facile à tester unitairement) gestion de la route ici
- couche description de l'ui (lecture des données)
- couche de présentation (primary) (react / tsx, html, css) : dedans très peu de logique, pour une entrée on doit avoir une sortie, on peut appeler les uses cases dedans (tester
  via cypress ou testing library)

Fred :
injection de dépendance indépendante du framework
tout ne doit pas être dans redux
En raccord avec JL, sauf pour les routes qui devraient être dans la couche présentation

couche applicative
couche redux
couche présentation

## Les tests doivent être rapides

Jonathan: Pour pouvoir les lancer continuellement
Fred: Avoir un feedback que c'est cassé rapidement
Dimitri: Pour écrire du code de prod rapidement

Dépend de [inbox: On entend quoi par test "rapide"]

# En cours de test

## Le terme use case est viable dans la lecture et l'écriture

Accéder à mon panier et ajouter des articles à mon panier sont deux cas d'utilisation de l'application. Nous choisissons donc d'utiliser le terme "use case" pour ces deux
opérations

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

## Minimiser l'utilisation des librairies de mock

Nous savons faire sans et de manière efficace. Nous préférons éviter l'implicite et créons nos propres test doubles réutilisables.

## Maintenir ce référentiel en français

Le français étant notre langue maternelle, lire et écrire dans cette langue n'ajoute pas de charge mentale.

## On timebox

Nous avons choisi de time-box nos discussions à 10 minutes par pratique. Si besoin de plus de temps, nous pouvons nous caler un point/atelier dédié.

## Évolution de l'état de l'art en cours de projet
De changements sur l'état de l'art peuvent survenir au cours d'un projet, par exemple, l'établissement d'une convention de nommage.
Lorsque ceci survient, le code étant un livrable au client, il est important que la base de code soit uniforme et respecte donc un même état de l'art.
Ainsi, 2 possibilités existent :
1. Garder l'état de l'art initial. Ce choix est préférable lorsque la base de code est importante et que la plus-value ne serait pas si importante, ou trop coûteuse.
2. Changer l'état de l'art, et organiser une session d'uniformisation de la base de code. Ce choix peut être plus coûteux, mais reste à envisager pour afficher un bon niveau de qualité de livrable.

Dans les 2 cas, la nouvelle pratique, une fois validée, doit être formalisée et ajoutée dans ce fichier.

## Organisation des dossiers et fichiers d'un projet
Afin de faciliter la prise en main d'un projet par un membre du collectif, nous uniformisons l'organisation des dossiers et fichiers.
Ainsi, tant que le projet reste petit, la structure doit rester aussi flat que possible.
Lorsque le projet grossit, on réorganise pour éviter la charge cognitive de recherche dans un répertoire.

On part sur une base de 7 fichiers ou répertoires dans un répertoire implique la création d'un nouveau niveau.
Le premier niveau d'une structure contiendra les répertoires suivants : 
1-primaries
2-domain
3-secondaries

## Outils

### Frontend

#### Injection de dépendances

[Piqure](https://github.com/Gnuk/piqure) est l'outil d'injection de dépendances favorisé pour les applications Frontend.
Il est agnostique du framework, ne fais que l'injection de dépendance et est très simple à implémenter.

## Stratégie de test

### Backend

#### Controllers

Nous utilisons du contract testing pour nous assurer du bon comportement de nos controllers.

- Une vraie requête HTTP est réalisée sur un serveur lancé par la suite de test.
- Dans le monde du write, nous utilisons un Spy de notre use case.
- Dans le monde du read, nous utilisons un Stub parametré de notre use case. Nous dissocions la valeur retournée attendue de la valeur retournée parametrée dans le Stub. Le
  changement de l'un n'entraîne pas le changement de l'autre. Cela permet de garantir le contrat même en cas de renommage

#### Hexagon

Nous appliquons la stratégie F.I.R.S.T. (voir chapitre 9 de Clean Code, section "F.I.R.S.T") pour la création de ces tests.

Tests très rapides / beaucoup de tests

#### Infrastructure

Tests pouvant faire preuve de lenteur et peu de tests
On teste la communication avec les collaborateurs externes sur lesquels on n'a pas de maîtrise
On évite d'utiliser le sut pour faire les given / then sauf s'il propose déjà les éléments testés séparément

Exemple : Un repository BDD a comme responsabilité pour save une entité métier
On développe un adapter dans lequel on fait la sauvegarde d'une entité
On écrit un test qui a pour SUT cet adapter et cette sauvegarde
Ce test utilise un moyen écrit spécifiquement pour vérifier dans la BDD la bonne écriture de l'entité

Nous essayons de respecter F.I.R.S.T.

Infra externe : test que l'on ne maîtrise pas (ils peuvent être flacky)
Infra interne : test que l'on maîtrise (ils faut veiller à ce qu'ils ne soient pas flacky)

## Ne pas utiliser les outils comme `it.only`

Bien que l'intention soit bonne, devoir manipuler les tests pour n'en lancer qu'une partie introduit le risque de déployer ce changement sur la branche principale. Par défaut, la CI lancera donc uniquement cet ensemble réduit de tests et ne verra pas les régressions que d'autres tests pourraient identifier.

Il existe des solutions pre-commit ou pre-push pour s'en protéger.Pour autant, cela ne traite pas le problème à sa source : l'incapacité de lancer un test rapidement et d'avoir un résultat prédictif via l'IDE.

Nous devons concentrer notre effort pour que les tests puissent être exécutés naturellement et sans altération préalable.

## Déclarer le SUT dans la suite de test

Lorsque l'instanciation du SUT est faite dans chaque cas de test, elle est redondante et introduit du bruit technique lié à l'instruction en elle-même. Cela a pour avantage de n'avoir à intervenir à une seule endroit si un nouveau collaborateur au SUT est introduit.

Nous favorisons le déplacement de cette partie avant l'exécution de chaque test. En TypeScript, cela peut être accompli avec la méthode `beforeEach`.

```typescript
// Bad example
describe('AcceptPractice', () => {
  it('Moves practice from inbox to validated ones', async () => {
    const repository = new InMemoryPracticeRepository();
    const sut = new AcceptPractice(repository);
    const practice = aPractice();
    repository.Feed(practice);

    await sut.Execute(practice.id);
    
    const actual = repository.by(practice.id);
    expect(actual).toBe({ ...practice, status: 'Accepted' });
  });
});

// Good example
describe('AcceptPractice', () => {
  let repository: InMemoryPracticeRepository;
  let sut: AcceptPractice;

  beforeEach(() => {
    repository = new InMemoryPracticeRepository();
    sut = new AcceptPractice(repository);
  });

  it('Moves practice from inbox to validated ones', async () => {
    const practice = aPractice();
    repository.Feed(practice);

    await sut.Execute(practice.id);
    
    const actual = repository.by(practice.id);
    expect(actual).toBe({ ...practice, status: 'Accepted' });
  });
});
```

## Factoriser ensemble l'action et l'assertion

L'appel (action) au SUT est toujours le même car sa signature ne change pas en fonction du cas de test. Bien souvent, c'est aussi le cas pour la manière d'observer (assertion) le bon comportement du système.

Si la signature du SUT est amenée à changer, ce serait dommage de devoir repasser sur chaque test un par un. Ce constat s'applique donc également à un changement de comportement observable (ajout d'un collaborateur qui introduit un effet de bord).

```typescript
// Bad example
describe('AcceptPractice', () => {
  let repository: InMemoryPracticeRepository;
  let sut: AcceptPractice;

  beforeEach(() => {
    repository = new InMemoryPracticeRepository();
    sut = new AcceptPractice(repository);
  });

  it('Moves practice from inbox to validated ones', async () => {
    const practice = aPractice();
    repository.Feed(practice);

    await sut.Execute(practice.id);
    
    const actual = repository.by(practice.id);
    expect(actual).toBe({ ...practice, status: 'Accepted' });
  });
});

// Good example
describe('AcceptPractice', () => {
  let repository: InMemoryPracticeRepository;
  let sut: AcceptPractice;

  beforeEach(() => {
    repository = new InMemoryPracticeRepository();
    sut = new AcceptPractice(repository);
  });

  it('Moves practice from inbox to validated ones', async () => {
    const practice = aPractice();
    repository.Feed(practice);
    await verify(practice.id, { ...practice, status: 'Accepted' });
  });

  async function verify(practiceId: string, expected: Practice) {
    await sut.Execute(practice.id);
    
    const actual = repository.by(practice.id);
    expect(actual).toBe(expected);
  }
});
```

## Encapsuler chaque appel à des collaborateurs

Les collaborateurs d'un SUT sont stables tant que le SUT l'est. Dès lors que le SUT change sa manière de collaborer avec un port (signature), chaque test référençant ce collaborateur se voit impacter. D'un point de vue extérieur, cela consitue aussi du bruit technique.

Pour solutionner ces deux problèmes, il suffit que chaque test s'appuie sur une indirection vers le collaborateur pour en réduire le couplage

```typescript
// Bad example
describe('AcceptPractice', () => {
  let repository: InMemoryPracticeRepository;
  let sut: AcceptPractice;

  beforeEach(() => {
    repository = new InMemoryPracticeRepository();
    sut = new AcceptPractice(repository);
  });

  it('Moves practice from inbox to validated ones', async () => {
    const practice = aPractice();
    repository.Feed(practice);
    await verify(practice.id, { ...practice, status: 'Accepted' });
  });

  async function verify(practiceId: string, expected: Practice) {
    await sut.Execute(practice.id);
    
    const actual = repository.by(practice.id);
    expect(actual).toBe(expected);
  }
});

// Good example
describe('AcceptPractice', () => {
  let repository: InMemoryPracticeRepository;
  let sut: AcceptPractice;

  beforeEach(() => {
    repository = new InMemoryPracticeRepository();
    sut = new AcceptPractice(repository);
  });

  it('Moves practice from inbox to validated ones', async () => {
    const practice = aPractice();
    feed(practice);
    await verify(practice.id, { ...practice, status: 'Accepted' });
  });

  async function verify(practiceId: string, expected: Practice) {
    await sut.Execute(practice.id);
    
    const actual = repository.by(practice.id);
    expect(actual).toBe(expected);
  }

  function feed(practice: Practice) {
    repository.feed(practice);
  }
});
```

## Time boxing

Gérer un time boxing en fonction du mob et du changement de rôle  
On se demande à ce moment si on avance dans la bonne direction ou non
Mini-retro du rôle d'avant
On compte sur un membre en dehors de la discussion pour proposer d'arrêter :

lorsqu'on n'avance pas, outils à disposition :

- brain dump quelque part (à définir)
- le dernier motiste ? On désigne celui qui a le dernier mot mais c'est l'équipe qui a la responsabilité
- fixer une plus petite hypothèse, pour la valider plus simplement
- autres outils à définir

