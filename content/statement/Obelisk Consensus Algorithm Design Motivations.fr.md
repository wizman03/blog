+++
title = "Les motivations de la comception de l'algorithme de consensus Obelisk"
tags = [
    "Obelisk",
    "Consensus",
    "Skywire",
]
date = "2017-10-26"
categories = [
    "Statement",
]
bounty = 20
+++

*Voici un message archivé du fil de discussion de bitcointalks en date du 19 juin 2014*

>Citation de: yxxyun le 19 juin 2014, 02:52:38 AM

>>Citation de: skycoin le 19 juin 2014, 02:31:59 AM

>>>Citation de: FrictionlessCoin le 18 juin 2014, 09:15:07 PM

>>>>Citation de: skycoin le 18 juin 2014, 09:08:56 PM

>>>>Mise à jour concernant le développement:

>>>>Nous avons trouvé un moyen d'empêcher l'attaque dite "Sybil" en utilisant un système hybride
>>>>de preuve d'enjeu (Proof of Stake).

>>>>Pour créer un noeud, il vous faut prouver que vous possèdez des pièces. Disons 10 pièces. Vous envoyez 10
>>>>pièces à l'adresse A. Puis vous envoyez 10 pièces de l'adresse A vers l'adresse B.
>>>>Puis vous ajoutez une signature en utilisant la clé public de l'adresse A pour signer le message
>>>>dans votre blockchain Obelisk.

>>>>D'une autre façon, vous pourriez publiez la clé publique de l'adresse A puis
>>>>signer un message avec cette clé public. Le noeud aurait besoin de publier une
>>>>signature à un certain interval de temps, ou à un certain nombre de blocs de la réserve de
>>>>pièces en train d'être déplacées, dans le but de maintenir une relation de confiance valide avec les autres.

>>>>De façon alternative, la preuve de brûlure pourrait être nécessaire, quand les pièces sont envoyées
>>>>de l'adresse A à une adresse B qui n'a pas de clé privée. La preuve de brûlure entrant en conflit
>>>>avec le besoin que personne ne devrait télécharger le blockchain en entier
>>>>depuis le début pour opérer un noeud complet, est donc peu probable

>>>> Ce système limite le nombre de nœuds Obelisk et limite la
>>>> possibilité de faire fonctionner des nœuds Obelisk aux seuls détenteurs de pièces.
>>>> La limite supérieure du nombre de nœuds et le besoin de pièces ajoutent
>>>> une autre couche de protection contre l'attaque dite "Sybil".

>>>Je ne suis pas certain de comment ceci empêche une attaque de type "Sybil".
>>>Est-ce que vous ajoutez simplement un coût au fait d'ajouter un noeud au réseau et en conséquence
>>>une attaque de type "Sybil" nécessiterait un coût financier pour l'exécuter ?

>>Il s'agit uniquement d'une idée à ce stade. Une amélioration a été trouvée. Chaque noeud Obelisk possède
>>une clé publique. La clé publique est hashé en une adresse puis 10 pièces sont stockées dans un endroit
>>détenu par cette adresse.

>> Cela n'ajoute pas de coût. Cela prouve simplement que vous possédez 10 pièces. Cela prouve
>> que vous connaissez la clé privée, pour une clé publique, dont l'adresse contient 10 pièces. Vous
>> pouvez encore utiliser les pièces.

>> L'idée est que cela limite le nombre de nœuds. Si 10 pièces doivent être
>> retenues et qu'il y a 100 millions de pièces, alors cela limite le réseau à 10
>> millions de nœuds. La limite supérieure ne semble pas être mathématiquement utile
>> maintenant, mais c'est quelque chose que nous devrions garder à l'esprit.

>> Lorsqu'un nouveau nœud Obelisk est lancé, il fera "confiance" à des pairs aléatoires. L'utilisateur
>> peut également ajouter quelques nœuds qu'il approuve à la main (bourses ou 
>> membres de confiance de la communauté). Un noeud est identifié par son hash de clé publique et trouvé par
>> DHT (table de hachage distribuée). Ce n'est pas comme Bitcoin où les nœuds sont des paires IP:port.
>> Vous pouvez déplacer votre ordinateur, l'identité du nœud ne dépend pas de son adresse IP.

>> Nous voulons que le réseau soit sécurisé avec une sélection de nœuds aléatoires. Nous ne voulons pas
>> une situation comme Ripple, où les trois nœuds des développeurs contrôlent le
>> réseau. Cependant, nous voulions éviter une situation où quelqu'un lance
>> 200 000 nœuds et tente de collecter les approbations auprès des nouveaux utilisateurs.
>> Ces nœuds d'attaque de type "Sybil", ne peuvent toujours pas faire une attaque des 51% en général, mais tout
>> ce qui augmente le coût de l'attaque est toujours utile.
>> Peut-être que nous le restreindrons afin qu'un nouvel utilisateur ne fasse confiance uniquement de manière aléatoire qu'à un noeud
>> qui possède une balance de pièces. Les relations de confiance ne seront pas rompues si le noeud n'a
>> pas une balance de pièces, mais il ne recevra pas de nouveaux utilisateurs aléatoires.

>> Le graphe de connectivité pour les relations de confiance, est censé être un
>> graphe aléatoire entièrement connecté. Quelques nœuds (membres de confiance de la communauté, bourses,
>> sites Web, organisations) auront plus de relations de confiance et cela aide
>> un peu le temps de convergence pour un consensus sur un bloc. Cela réduit un peu le périmètre
>> du réseau. Certains nœuds seront utilisés pour vérifier le consensus (vous choisissez un
>> lot de bourses ou de clés publiques différentes), ces nœuds n'affectent pas
>> les décisions de consensus, mais sont des "oracles du consensus" pour vérifier si votre noeud a
>> convergé avec le réseau.

>> Si deux grandes bourses ont un consensus différent pour un bloc particulier, ceci
>> est un problème. Cela pourrait indiquer une déconnexion du réseau ou une attaque sur le réseau.
>> Les bourses peuvent vouloir suspendre la négociation jusqu'à ce que le problème soit résolu.

> Obelisk est le nœud de consensus de skycoin? Je pensais que le skycoind était le
> le noeud ...

Oui.

Skycoin a une blockchain. La blockchain est sur
https://github.com/skycoin/skycoin/tree/develop/src/coin. Cela analyse les
blocs et gère les résultats et les transactions non dépensés.

Skywire est le daemon et a une "architecture de service". Il peut exécuter des services,
comme le service de synchronisation de la blockchain et d'autres choses. Le meshnet est actuellement
mis en œuvre comme un service sur Skywire (même si cela peut avoir besoin de
changer).

Le mécanisme de consensus est en dehors de la blockchain. Les noeuds Obelisk (qui
seront probablement mis en œuvre comme un service Skywire) ont une blockchain.
Chaque noeud a une clé publique. La clé publique identifie le nœud Obelisk.
Chaque nœud Obelisk a sa propre blockchain (il n'y a pas de pièces dans cette chaîne).
Le noeud crée un nouveau bloc et le signe avec sa clé privée.
Les blockchains Obelisk sont utilisées pour négocier un consensus (déterminer le bloc de tête 
dans la blockchain Skycoin). Obelisk utilise Ben-Or pour un consensus aléatoire. 
Chaque nœud Obelisk possède une liste des autres nœuds auxquels il est abonné.
Ces nœuds influencent les décisions de consensus et de vote pour le nœud local.
Pour les topologies de réseau non pathologiques, le consensus local converge
vers un consensus global.

Chaque noeud vote sur le bloc suivant de la chaîne. Un noeud propose le prochain
bloc et les nœuds votent sur le successeur. Les votes sont publiés dans les
blocs dans la blockchain Obelisk pour chaque nœud. Votre noeud vote au hasard
entre temps et retourne son vote de temps en temps. Une fois 40% de
vos pairs (les nœuds auxquels vous êtes abonné) ont atteint un consensus, vous
passer à ce candidat. Le réseau peut voter sur plusieurs branches à la fois, il
ne ralentit pas dans l'attente d'un consensus. Les branches sont réduits à une seul
chaîne au fil du temps. Les divisions de deux ou trois blocs sont normales, mais après quelques
confirmations la probabilité de l'annulation du bloc diminue
exponentiellement vers zéro. Si une transaction a été exécutée sur toutes les
chaînes candidates, alors elle est exécuté, même si le consensus sur la chaîne particulière
n'a pas encore été décidé.
C'est ainsi que le binaire Ben-Or et Skycoin va utiliser quelque chose de légèrement plus avancé,
qui est plus rapide quand il y a plusieurs blocs successeurs à choisir dans le
set de consensus. Le choix aléatoire est important pour empêcher les sous-graphiques du réseau
de rester bloqués. Le processus de vote est une forme de "cuisson" où chaque
noeud arrivera au consensus global indépendamment, seulement à partir de ses informations locales.

Le processus de consensus se passe en public. Un noeud publie des blocs, les signe
avec leur clé privée et les blocs sont répliqués de pair à pair entre les
abonnés de la chaîne. Puis, il y a des "oracles du consensus" qui sont des nœuds
qui sont utilisés pour vérifier le consensus mais qui n'influencent pas le consensus. Donc vous pourriez
choisir les clés publiques de quelques bourses et quelques membres de confiance de la communauté
et votre noeud les utilisera pour détecter si quelque chose ne va pas. Ceci est utilisé pour
détecter les déconnexions. Cela protège également contre une attaque, où un pirate
contrôle votre routeur et peut contrôler les pairs auxquels vous pouvez vous connecter.

Si un nœud s'affiche sur le réseau et tente de pousser le réseau à accepter une
chaîne différente (attaque des 51%, annulation des transactions), il est généralement ignorée.
La plupart des attaques des 51% nécessitent un comportement malicieux du nœud qui est automatiquement
détecté et résulte à la suppression du noeud malicieux par un noeud abonné de
sa liste de confiance. La stratégie d'attaque des 51% la plus facile est simple à détecter et à prouver
avec une certitude mathématique qu'elle était prévu comme une tentative d'annuler des
transactions, car elle nécessite des décisions consensuelles de blocage de bloc.
Il nécessite la publication de deux blocs signés avec le même numéro de séquence,
donc nous en avons juste fait une infraction automatiquement bannisable pour un noeud.

Nous essayons d'éliminer la dernière attaque des 51% possible, qui est lorsquun
sous-réseau de noeuds se déconnecte (attaque de déconnexion), puis rejoint le
réseau avec un consensus de blockchain différent et tente de forcer cela sur le
réseau pour annuler les transactions. La plupart de ces attaques échoueront, car le
sous-réseau n'aura pas assez d'influence.

Cette attaque est toujours très difficile à enlever. Dans le cas où il y a
une attaque des 51% réussie, une solution consiste à geler le réseau et laisser chaque nœud / utilisateur
choisir individuellement la chaîne qui est valide et laisser les gens interdire noeuds attaquant manuellement. L'oracle de consensus permet à chaque nœud de
savoir, avec une forte probabilité, si l'état est synchronisé et si un consensus global a été atteint ou si
ils font partie d'un sous-graphique déconnecté. Nous pensons qu'il est possible pour chaque noeud de
savoir avec une forte probabilité d'exactitude à partir des informations locales, si un
nœud était hors ligne lors d'une décision de consensus, puis d'ignorer les nœuds
qui étaient déconnectés qui apparaissent soudainement et tentent de forcer une chaîne sur le réseau.

Dans Bitcoin, si vous avez le plus de pouvoir de hachage, vous pouvez annuler les transactions quand vous le souhaitez.

Dans Skycoin, pour inverser les transactions:

- Vous devez controller un grand nombre de nœuds
- Les nœuds que vous contrôlez doivent être "influents" et fiables dans la topologie du réseau
- Vos noeuds doivent présenter un comportement d'attaque pathologique extrêmement flagrant
  sans que le comportement ne soit détecté, car la détection entraînerait la perte
  des relations de confiance dont vous avez besoin pour attaquer le réseau.
- Vos nœuds doivent être dans une topologie d'attaque pathologique, sans être
  détecté (la plupart des noeuds robots auront la confiance de très peu d'humains et seront très évidents)
- Vous devez être en mesure de faire en sorte que les nœuds que vous contrôlez parviennent à s'entendre de manière à aboutir
  dans une attaque réussie (ce n'est pas très simple)
- Si l'attaque réussit, vous devez empêcher le réseau d'annuler l'attaque manuellement (très difficile si les gens ont perdu des pièces ou de l'argent en raison de l'attaque)

Pour prouver qu'il est n'est résistant à l'attaque des 51%, vous devez écrire les hypothèses que vous formulez, puis créer un modèle mathématique simple et ensuite prouver les
conditions dans lesquelles les choses peuvent et ne peuvent pas arriver dans le modèle. Une fois que vous
connaissez les conditions dans lesquelles une attaque est possible, vous essayez de les éliminer et si vous ne pouvez pas les éliminer, vous les rendez aussi difficile que possible.
Vous augmentez le coût d'une attaque et vous réduisez la probabilité qu'un
attaque spécifique réussira. Ensuite, vous réduisez les gains et les incitations pour
l'attaque.

Le processus de consensus est simple et facile à modéliser, mais non intuitif sans
le voir. Il y aura dans la finalité un site javascript avec une animation du
processus de consensus avec lequel vous pourrez jouer.
