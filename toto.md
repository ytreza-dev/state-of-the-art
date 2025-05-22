Reprendre les catégories via le git diff
DK : Remettre ça dans l'état de l'art en async (ce midi genre)

Retourne dans l'inbox
	Définir notre ubiquitous language sur ce que sont les tests (avoir peut-être une section dédiée voire même un fichier à part)

Ca avance
    - Adapter contract testing --> Jonathan documente
      - JL > Peut-être un peu tôt pour l'équipe, mais chaud pour en discuter
      - FJ > Il me faut un court de rattrapage sur ce que c'est
- Comment instancier les sut ? --> Dimitri documente
      - JL > Pas de stratégie à proposer
      - DK > Hexagon : new, Intégration : récupérer via la DI
    Joanthan : documenter le contract testing sur un composant front
Ca avance (1 pers)
	mob.sh
		JL > Cela permet de travailler avec n'importe quel IDE, donc oui pour l'imposer si au moins une personne veut l'utiliser (c'est mon cas). Par contre, si je ne suis pas là, je ne veux pas imposer un outil. --> Jonathan tu documentes
	Lorsqu'on fait un choix différent de l'actuel état de l'art :

Battle ?
	hexagone partout (lecture + écriture)
		AG > ça ne sert à rien de l'avoir partout. Typiquement en lecture, je trouve ça totalement inutile ! Il faut rester au plus proche de la DB dans ce cas précis je pense !
		AT > Ok pour simplifier dans le cadre du read


Proposition: On ne met pas à jour tout de suite l'état de l'art. Chacun met à jour en async.
	Ca avance (personne): c'est celui qui a écrit la practice qui la documente
	Ca avance (1 pers): c'est celui qui a écrit la practice qui la documente + celui qui a réagi si différent (sync ou async peu importe)

