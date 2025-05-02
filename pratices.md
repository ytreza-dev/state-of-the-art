# A discuter (inbox)

- Tests
    - Minimiser les tests e2e et les tests d'intégration
        - JL > Je veux que la suite de test soit rapide à lancer. Si les tests e2e et intégration respecte cette contrainte, il peut y en avoir beaucoup.
        - DK > Pas d'envie de minimiser les tests d'intégration. Quand ce sont des adapters ciblant des collaborateurs qu'on ne maîtrise pas, la logique est distante donc c'est
          souvent juste le happy path + un cas d'erreur qui est testé. Quand c'est des adapters ciblant des collaborateurs qu'on maîtrise (data source, repository, file storage),
          je couvre chaque WHERE, ORDER BY, etc. surtout pour les repos (si tu te foires sur ton repo autant dire que toutes tes règles de gestion ne servent à rien car tu pourrais
          persister le mauvais état -> critique pour moi ce type d'adapter)
        - AG > Pour moi il faudrait que les tests soient rapide E2E et intégration. Pour autant il ne faut pas minimiser les intégrations. les E2E doivent être choisi correctement.
          J'entends E2E qui passe toutes les couches avec les vraies injections (pas de mock sur un secondary, etc). seule les date provider, idGenerator, peuvent être moquer/faker
          pour prédire l'output
        - FJ > Je pense que pour l'instant on n'a pas trouvé une bonne stratégie de test pour les tests E2E ne soient pas fragiles, ni maitrisable (avec Cypress en tout cas, on ne
          peut pas changer l'injection de dépendence)

    - On entend quoi par test "rapide"
      - JL > Je considère qu'un test (ou surtout une suite de tests) est lent lorsque je n'ai plus envie de le lancer entre l'écriture de deux lignes de code.
      - DK > Hexagon: 3sec max pour 1000 tests (pour y mettre du mutation test les yeux fermés). intégration: même idée que celle de JL, faut pas que la lenteur by design m'encourage à prendre des raccourcis
      - AG > OK sans pour autant aller contre le point de minimiser les tests d'intégration

- Préciser comment un stub paramétré s'utilise (feed vs constructor vs etc.)
    - JL > Aucun avis pour le moment, l'un ou l'autre me vont et je m'autorise les deux.
    - DK > Je privilégie le feed qui est explicite pour chaque test. Moins de magie, moins de dinguerie
    - AG > Je préfère le feed
    - FJ > Si l'un ou l'autre va, je propose plutôt de faire un choix pour maintenir une uniformité dans chaque base de code.

- Conventions
    - Nommage
        - Repository / DataSource etc.
            - JL > Je veux ici qu'il n'y ait aucune ambiguité, que l'on ne se pose pas la question. La nature doit être dans le type, pas dans le nom de variable. Avoir une gateway
              in memory, c'est quelque chose qui me perturbe. Donc, je pense que l'interface ne doit pas savoir que c'est une gateway, l'implémentation, oui.
            - DK > Repo c'est un pattern pour save une domain entity. Data source c'est purement de la récupération d'info sans side-effect
            - AG > j'aime bien quand s'est explicite dans le nom de la variable. ça permet de facilement le retrouver avec outils de recherche des IDE.Le mettre dans le noms du
              ficher et un plus mais pas obligatoire, c'est surtout à but de "trier" et regrouper les instances lorsqu'elles sont dans un même folder
            - FJ > En fait, j'pense que c'est surtout côté Ubiquitous Language qu'il faut qu'on travaille ce sujet.

- Architecture
    - Rendre les morceaux de code modulaires (création de librairie)
        - JL > C'est une pratique que j'essaie de mettre en place. C'est un peu tôt pour l'équipe, mais je considère que cela permet de diminuer le couplage, améliorer la
          réutilisabilité, diminuer la charge cognitive, améliorer la rapidité des tests, améliorer le design du code et l'organisation des répertoires.
        - DK > Trop vaste / générique. Si on parle juste de création de lib, je le suis plus souvent moteur pour ce qui a attrait au test tooling
        - AG > ça dépent du context. On ne doit pas créer une lib pour le plaisir alors que j'ai besoin de faire 2 GET sur un adapteur.ça devient de l'overengeniering!
- Méthodologie
    - TDD
        - JL > Je pense qu'on peut encore mieux pratiquer le TDD, mais pas de recommandation particulière pour le moment.
        - AG > c'est outil il faut svoir l'utiliser MAIS surtout savoir quand ne pas l'utiliser. J'entends par là que lorsque son utilisation me demande de repasser 12 fois sur le
          même fichier alors que je savais à l'avance comment j'allais faire l'implémentation, alors ça ne sert à rien. On pourrait débattre sur comment on sait qu'on va faire la
          même chose. Souvent on a une idée ou des prérequis de ce qu'on veut mettre en place, le TDD n'apporte rien là! Autre chose, il a une ENORME plus-value sur des
          algorithmes, quasiment aucune sur comment afficher un composant front.
        - FJ > En phase, mais j'pense pas qu'il y ait d'action spécifique à mettre en place, l'entrainement et l'expérience feront leur office.

    - Avoir le moins de logique possible dans les composants
        - JL > Tester un composant me parait compliqué et lent. Sauf si on change cela, je veux éviter de tester un composant pour des choses qui ne sont pas liées au framework
          front
        - AG > si c'est en mode front, aucun interet. Nos composent doivent être humble et afficher ce qui leur est retourné. Pour ce qui de la logique, tout ne doit pas être
          abstrait !
        - FJ > @JL : Même le testing de page object / View Model ?
    - Des contracts tests
        - JL > J'ai l'impression qu'on applique déjà ça
        - DK > Contract tests côté server c'est de la frappe. Peut-être qu'on pourrait préparer/partager un snippet de structure pour ne changer que l'URL, les dependencies et
          l'assert
        - FJ > Il me faut un court de rattrapage sur ce que c'est
    - Linter/Prettier
        - JL > OK pour en avoir, mais je ne veux pas que cela ait un impact sur mon flow de développement. Je ne veux pas devoir me réaligner chaque fois que je sauvegarde un
          fichier. J'aimerai qu'on les décale au moment du commit, voire du push
        - DK > Avoir du rouge pendant que je dév est une charge cognitive dont je me passerai bien (sauf erreur de compilation OFC). Je suis plutôt contre en l'état
        - AG > 100% pour en avoir un. Et plus précisement lorsque je save mon fichier je veux qu'il format. Je ne dois pas avoir à réfléchir si lorsque je passe la main ou change
          de fichier si j'ai fait la manipulation de format pour que l'autre puisse lire correctement.
        - FJ > J'comprends pas trop ce qui dérange, avec un IDE correctement configuré, c'est transparent. On peut peut-être revoir certaines règles cependant, si elles nous
          gênent.
- Testing
    - Utiliser de l'aléatoire pour faire de la triangulation
        - JL > Totalement en phase. Voir pour l'utilisation de librairie type faker ou le truc qu'on utilisait @Dimitri
        - DK > J'ai rien trouvé en TS malheureusement mais y'a moyen de faire des méthode aTruc() qui font du random sur chaque prop. Je suis pour pousser cette pratique tellement
          ça simplifie la lecture (en plus de la triangulation)
        - AG > J'aime bien l'idée. Est-ce qu'il faut le faire pour chaque "variable" je ne sais pas. Mais si je l'avais je ne serais pas contre.
    - Stratégie de test - Frontend
        - FJ > Je pense qu'il faut limiter les E2E, faire du TDD pour faire émerger les page object / view model
        - AG > composant front NON, logique métier OUI, adapter OUI
        - JL > composant front OUI via contract testing, logique métier OUI, adapter OUI
- A part
    - pour le futur, mettre en place l'event sourcing et devenir expert dessus
        - JL > J'aimerai que ce soit un critère différenciant pour nous et il y a des patterns intéresasnts. Mais c'est peut-être un peu tôt pour l'équipe.
        - DK > Si un domain métier semble le nécessiter, oui. Tant que c'est pas le cas, pas chaud car la courbe d'apprentissage est trop importante
        - AG > si utile pour le contexte oui, sinon non!
        - FJ > C'est bien à connaitre, mais c'est vraiment pas une réponse à tous les problèmes. Ça génère un overhead énorme alors que ça n'a d'intérêt que dans les produits hyper
          coûteux en ressource
    - déterminer des experts sur chaque pratique
        - JL > En fait, je veux avoir du poids dans les parties où je me sens expert et moins de poids dans les parties où je ne le suis pas. Par exemple, je me sens frustré quand
          quelqu'un balaie une de mes propositions quand je parle de TDD (expérience que je ai eu dans une autre équipe).
        - DK > @Johjo je pense que c'est plutôt les rôles de l'holacratie que le fait d'être expert d'une pratique qui soulagerait ça
        - FJ > On sait qui est bon en quoi, j'suis pas sûr de l'intérêt de ça à part transformer certains arguments en arguments d'autorité parce que c'est dit par un "expert"
    - Un référentiel de pratiques générale (puis par langage / stack ?)
        - Avantage : on peut filer ce référentiel aux clients. Ca montre qu'on ne fait pas les choses au hasard et leur permet de reprendre avec le contexte du pourquoi telle ou
          telle pratique
            - JL > Pourquoi pas, mais c'est beaucoup de travail.
            - DK > Générale comme celle-ci pour le moment
            - AG > en interne oui, pour le client non.
    - On peut / on doit / on ne doit pas
        - UL : Principe / Guide line (c'est souple)
        - UL : Règle / loi (c'est dur)
        - JL > Oui, il est important de déterminer dans les pratiques si c'est une règle ou un principe.
        - DK > Plutôt en faveur d'un "on devrait" / "on ne devrait pas". Y'a pas de blame si on n'utilise pas une pratique qu'on aurait pû. Inversement si on utilise une qu'on ne
          devrait pas. Souvent c'est par oubli des practices ou cas particulier qui fait que c'est pas applicable. On en discute quelques minutes et on prend une action (suivre ou
          non la practice)
        - AG > certain cas son à "forcer" je dirais. (ex: bien nommer, faciliter la lecture etc...) La majorité devrait être des conseils d'utilisation


- Collaboration
    - Qui choisi les outils (driver vs navigator)
        - JL > Tout dépend des outils, mais dans l'ensemble, je pense que c'est le driver.
        - DK > Driver. Me demandez pas le watch mode, je souhaite expliciter mes actions.
        - AG > je ne maitrise pas bien ses roles donc difficile de choisir. Par contre je ne supporte pas "être pris pour un enfant". ex: clique ici, d'abord fait ce select, puis
          tel raccourci clavier, etc.

- Parler du mob programming (Dimitri trop rapide)
    - JL > C'est un exemple, désolé de te pointer du doigt Dimitri. Est-ce qu'on pourrait avoir une safe zone pour se faire des feedbacks ? C'est assez risqué, mais de mon côté, je
      me sentirais rassuré. J'ai tellement peur de saouler les gens que j'ai besoin de savoir si c'est le cas ou non afin d'adapter mon comportement.
    - DK > Oui il faut
    - AG > ça dépend ce qu'on entends par parler du mob. Si c'est dans le but de prospecter, l'expérience à montré que ça avait plus de tord que de bien. Si c'est globalement faire
      connaitre cette pratique oui je n'ai pas de soucie avec ça. Pour répondre à JL, il faut pouvoir se donner du feedback c'est hyper important je trouve.

- Méthodologie : Déploiement continu (envisager de déployer toutes les 30 minutes)
    - JL > J'aimerai qu'on ait un principe de déployer toutes les x minutes. Je ne veux surtout pas que ce soit une règle.
    - DK > L'outil mob.sh rend la création de branche facile donc n'aide pas forcément à faire du CD. Je suis pour se fixer un objectif de déploiement régulièrement. Ca permet de
      se focus sur quelque chose qui a de l'impact dans l'idée
    - AG > dans l'idée c'est bien d'essayer de tendre vers ça je pense. L'idée pour moi dérrière est de ce rappelr que ce qui compte c'est la valeur qu'on appporte au client et de
      pouvoir régulièrement /rapidement lui apporter plus de valeur.

- principes d'holacratie dans la rédaction des practices
    - JL > Afin de gagner en efficacité et diminuer les discussions
    - AG > ne maitrisant pas l'holacratie, je dirais non. C'est pas parceque tu es expert dans un domaine, qu'une personne débutante dans ce domaine ne peux pas apporter de super
      pratique de part son expérience dans le reste.
- lorsqu'on parle et que quelqu'un doit partir, comment le dire ?
    - JL > Je n'aime pas partir du mob comme un voleur, mais je n'aime pas non plus couper le flow. Je ne sais pas comment faire.
    - AG > vraiment pas simple ce cas là. Et il y a le même lorsqu'on arrive. Ce que j'applique : si discussion en cours, je ne dis rien lorsque j'arrive et je mets un message
      écris lorsque je pars. Si pas de discussion en cours, je parle.
    - FJ > On a des canaux textuels pour le dire (et je pense qu'il faudrait le dire quand même plutôt que partir sans rien dire), et on sait que les gens avec qui on bosse en ont
      qqch à faire de ce qu'on raconte, donc que le départ n'est pas malveillant

- Lorsqu'on fait un choix différent de l'actuel état de l'art :
    - quel process met-on en œuvre pour l'intégrer dans l'état de l'art ?
        - JL > Lorsqu'on remet en question l'état de l'art, il faudrait le signaler rapidement.
        - DK > Je suis pour garder l'état de l'art même si y'a challenge en cours. Discuter de manière synchrone mais en dehors du contexte client. Trancher et fix ou non sur ce
          qui a été fait avant challenge. A nous de voir si on utilise l'inbox pour challenge la pratique ou si on juge plus pertinent d'en discuter genre en fin de journée et
          d'amend la practice dans la foulée si on est au moins quelques uns
        - AG > je suis mitigé.

- Architecture - Quels raccourcis se permet-on sur une archi ? (définir un raccourci)
    - JL > Je laisse ce raccourci à la responsabilité du mob.
    - AG > l'idée ici est d'en avoir conscience et de le tracer pour que le groupe s'en souvienne.
    - FJ > Je dirais que je prends les raccourcis qui évitent les passe-plat (ex: Un primary peut appeler directement un secondary s'il n'y a aucun traitement fait sur la donnée)

# Objectif du doc

[A préciser ...]

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

