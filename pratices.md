# Nouvel inbox - à discuter

- Pas de it.only en prod
  DK > Quand on en vient à jouer avec du only, focus, skip & cie, ça smell grave. Ca veut dire qu'on a un test flaky, trop long ou un découpage des suites de tests beaucoup trop large (genre on veut pas tout lancer car ça prendrait des plombes même si notre test qui nous intéresse est rapide)

- création sut & collab en beforeEach, verify(expected) généralisé. C'est tellement plus simple à la lecture (ça enlève le bruit de comment on assert, comment on appelle notre sut, etc.)
- mettre les collab.feed dans des méthodes feed -> ca enlève le bruit technique

# A discuter (inbox)

- Tests
    - Définir notre ubiquitous language sur ce que sont les tests (avoir peut-être une section dédiée voire même un fichier à part)
    - Minimiser les tests e2e et les tests d'intégration
      JL > Je veux que la suite de test soit rapide à lancer. Si les tests e2e et intégration respecte cette contrainte, il peut y en avoir beaucoup.
      DK > Pas d'envie de minimiser les tests d'intégration. Quand ce sont des adapters ciblant des collaborateurs qu'on ne maîtrise pas, la logique est distante donc c'est souvent juste le happy path + un cas d'erreur qui est testé. Quand ce sont des adapters ciblant des collaborateurs qu'on maîtrise (data source, repository, file storage), je couvre chaque WHERE, ORDER BY, etc. surtout pour les repos (si tu te foires sur ton repo autant dire que toutes tes règles de gestion ne servent à rien car tu pourrais persister le mauvais état -> critique pour moi ce type d'adapter)

  - On entend quoi par test "rapide"
      JL > Je considère qu'un test (ou surtout une suite de tests) est lent lorsque je n'ai plus envie de le lancer entre l'écriture de deux lignes de code.
      DK > Hexagon: 3sec max pour 1000 tests (pour y mettre du mutation test les yeux fermés). intégration: même idée que celle de JL, faut pas que la lenteur by design m'encourage à prendre des raccourcis

  - Préciser comment un stub paramétré s'utilise (feed vs constructor vs etc.)
      JL > Aucun avis pour le moment, l'un ou l'autre me vont et je m'autorise les deux.
      DK > Je privilégie le feed qui est explicite pour chaque test. Moins de magie, moins de dinguerie

- Conventions
    - Nommage
        - Repository / DataSource etc.
          JL > Je veux ici qu'il n'y ait aucune ambiguité, que l'on ne se pose pas la question. La nature doit être dans le type, pas dans le nom de variable. Avoir une gateway in memory, c'est quelque chose qui me perturbe. Donc, je pense que l'interface ne doit pas savoir que c'est une gateway, l'implémentation, oui.
          DK > Repo c'est un pattern pour save une domain entity. Data source c'est purement de la récupération d'info sans side-effect
      
        - organisation des dossiers :
          - `image` ou `images` ? 

- Architecture
    - Définir un ensemble d'architectures permettant de répondre avec un minimum de code au besoin
    - Rendre les morceaux de code modulaires (création de librairie)
        JL > C'est une pratique que j'essaie de mettre en place. C'est un peu tôt pour l'équipe, mais je considère que cela permet de diminuer le couplage, améliorer la réutilisabilité, diminuer la charge cognitive, améliorer la rapidité des tests, améliorer le design du code et l'organisation des répertoires.
        DK > Trop vaste / générique. Si on parle juste de création de lib, je le suis plus souvent moteur pour ce qui a attrait au test tooling
    - Choisir une manière de représenter l'organisation des répertoires (vertical architecture, etc...)
      DK > Je serais d'avis de faire au plus simple tant que y'a peu de chose dans le répertoire. Si on juge ensemble que split primary/hexagon/secondary est pertinent, on le fait. Pareil pour port/use cases/domain model
- Outillage
    - Définir, par stack, les outils qu'on préfère utiliser
        - ex : Front : Angular, un outil de state, un outil de gestion event driven, un outil d'injection de dépendances
    - De l'injection de dépendances
- Méthodologie
    - TDD
      JL > Je pense qu'on peut encore mieux pratiquer le TDD, mais pas de recommandation particulière pour le moment.
    - Adapter contract testing
      JL > Peut-être un peu tôt pour l'équipe, mais chaud pour en discuter
    - Avoir le moins de logique possible dans les composants
      JL > Tester un composant me parait compliqué et lent. Sauf si on change cela, je veux éviter de tester un composant pour des choses qui ne sont pas liées au framework front
    - Des contracts tests
      JL > J'ai l'impression qu'on applique déjà ça
      DK > Contract tests côté server c'est de la frappe. Peut-être qu'on pourrait préparer/partager un snippet de structure pour ne changer que l'URL, les dependencies et l'assert
    - Avoir un watch mode par type de test (local vs acceptance)
      JL > C'est une pratique du driver. De mon point de vue, la watcher n'est pas assez rapide. Mais je ne veux pas interdire l'utilisation
    - Quand tester quoi
      JL > Je ne comprend pas ce point
    - Linter/Prettier 
      JL > OK pour en avoir, mais je ne veux pas que cela ait un impact sur mon flow de développement. Je ne veux pas devoir me réaligner chaque fois que je sauvegarde un fichier. J'aimerai qu'on les décale au moment du commit, voire du push
      DK > Avoir du rouge pendant que je dév est une charge cognitive dont je me passerai bien (sauf erreur de compilation OFC). Je suis plutôt contre en l'état
- Testing
    - Utiliser de l'aléatoire pour faire de la triangulation
      JL > Totalement en phase. Voir pour l'utilisation de librairie type faker ou le truc qu'on utilisait @Dimitri 
      DK > J'ai rien trouvé en TS malheureusement mais y'a moyen de faire des méthode aTruc() qui font du random sur chaque prop. Je suis pour pousser cette pratique tellement ça simplifie la lecture (en plus de la triangulation)
    - Commenter instancier les sut ?
      JL > Pas de stratégie à proposer
      DK > Hexagon : new, Intégration : récupérer via la DI
    - Stratégie de test - Frontend
- A part
    - pour le futur, mettre en place l'event sourcing et devenir expert dessus
      JL > J'aimerai que ce soit un critère différenciant pour nous et il y a des patterns intéresasnts. Mais c'est peut-être un peu tôt pour l'équipe.
      DK > Si un domain métier semble le nécessiter, oui. Tant que c'est pas le cas, pas chaud car la courbe d'apprentissage est trop importante
    - déterminer des experts sur chaque pratique
      JL > En fait, je veux avoir du poids dans les parties où je me sens expert et moins de poids dans les parties où je ne le suis pas. Par exemple, je me sens frustré quand quelqu'un balaie une de mes propositions quand je parle de TDD (expérience que je ai eu dans une autre équipe).
      DK > @Johjo je pense que c'est plutôt les rôles de l'holacratie que le fait d'être expert d'une pratique qui soulagerait ça
    - Un référentiel de pratiques générale (puis par langage / stack ?)
        - Avantage : on peut filer ce référentiel aux clients. Ca montre qu'on ne fait pas les choses au hasard et leur permet de reprendre avec le contexte du pourquoi telle ou telle pratique
        JL > Pourquoi pas, mais c'est beaucoup de travail.
        DK > Générale comme celle-ci pour le moment
    - On peut / on doit / on ne doit pas
        JL > Oui, il est important de déterminer dans les pratiques si c'est une règle ou un principe.
        DK > Plutôt en faveur d'un "on devrait" / "on ne devrait pas". Y'a pas de blame si on n'utilise pas une pratique qu'on aurait pû. Inversement si on utilise une qu'on ne devrait pas. Souvent c'est par oubli des practices ou cas particulier qui fait que c'est pas applicable. On en discute quelques minutes et on prend une action (suivre ou non la practice) 
    - Voir via git blame le mob complet qui a participé à la modification (Jonathan)
        JL > Je pense qu'on peut oublier pour le moment.
- Management
    - Demander en permanence où en sont les membres vis-à-vis du collectif
        JL > Faire du ménage récurrent, mais est-ce que ça a sa place ici ? même si c'est moi qui l'ai proposé :p  


- Collaboration
    - Qui choisi les outils (driver vs navigator)
      JL > Tout dépend des outils, mais dans l'ensemble, je pense que c'est le driver.
      DK > Driver. Me demandez pas le watch mode, je souhaite expliciter mes actions.
- Outils imposés
    - mob.sh
      JL > Cela permet de travailler avec n'importe quel IDE, donc oui pour l'imposer si au moins une personne veut l'utiliser (c'est mon cas). Par contre, si je ne suis pas là, je ne veux pas imposer un outil.

- Parler du mob programming (Dimitri trop rapide)
    JL > C'est un exemple, désolé de te pointer du doigt Dimitri. Est-ce qu'on pourrait avoir une safe zone pour se faire des feedbacks ? C'est assez risqué, mais de mon côté, je me sentirait rassuré. J'ai tellement peur de saouler les gens que j'ai besoin de savoir si c'est le cas ou non afin d'adapter mon comportement.
    DK > Oui il faut

- Méthodologie : Déploiement continu (envisager de déployer toutes les 30 minutes)
    JL > J'aimerai qu'on ait un principe de déployer toutes les x minutes. Je ne veux surtout pas que ce soit une règle.
    DK > L'outil mob.sh rend la création de branche facile donc n'aide pas forcément à faire du CD. Je suis pour se fixer un objectif de déploiement régulièrement. Ca permet de se focus sur quelque chose qui a de l'impact dans l'idée

- Définir nos différentes boucles de feedback
    JL > Il faudrait les définir dans UL
- UL : Principe / Guide line (c'est souple)
- UL : Règle / loi (c'est dur)
- principes d'holacratie dans la rédaction des practices
    JL > Afin de gagner en efficacité et diminuer les discussions
- lorsqu'on parle et que quelqu'un doit partir, comment le dire ?
    JL > Je n'aime pas partir du mob comme un voleur, mais je n'aime pas non plus couper le flow. Je ne sais pas comment faire.

- Lorsqu'on fait un choix différent de l'actuel état de l'art : 
  - dans quelle mesure réapplique-t-on ce nouveau choix sur le code existant ?
  - quel process met-on en œuvre pour l'intégrer dans l'état de l'art ?
    JL > Lorsqu'on remet en question l'état de l'art, il faudrait le signaler rapidement.
    DK > Je suis pour garder l'état de l'art même si y'a challenge en cours. Discuter de manière synchrone mais en dehors du contexte client. Trancher et fix ou non sur ce qui a été fait avant challenge. A nous de voir si on utilise l'inbox pour challenge la pratique ou si on juge plus pertinent d'en discuter genre en fin de journée et d'amend la practice dans la foulée si on est au moins quelques uns

- Architecture - Quels raccourcis se permet-on sur une archi ? (définir un raccourci)
    JL > Je laisse ce raccourci à la responsabilité du mob. 
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
- couche de présentation (primary) (react  / tsx, html, css) : dedans très peu de logique, pour une entrée on doit avoir une sortie, on peut appeler les uses cases dedans (tester via cypress ou testing library)  

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



## Minimiser l'utilisation des librairies de mock

Nous savons faire sans et de manière efficace. Nous préférons éviter l'implicite et créons nos propres test doubles réutilisables.

## Maintenir ce référentiel en français

Le français étant notre langue maternelle, lire et écrire dans cette langue n'ajoute pas de charge mentale.

## On timebox

Nous avons choisi de time-box nos discussions à 10 minutes par pratique. Si besoin de plus de temps, nous pouvons nous caler un point/atelier dédié.

## Stratégie de test

### Backend

#### Controllers

Nous utilisons du contract testing pour nous assurer du bon comportement de nos controllers.
- Une vraie requête HTTP est réalisée sur un serveur lancé par la suite de test.
- Dans le monde du write, nous utilisons un Spy de notre use case.
- Dans le monde du read, nous utilisons un Stub parametré de notre use case. Nous dissocions la valeur retournée attendue de la valeur retournée parametrée dans le Stub. Le changement de l'un n'entraîne pas le changement de l'autre. Cela permet de garantir le contrat même en cas de renommage

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

