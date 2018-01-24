+++
title = "Les motivations de la conception de l'algorithme de consensus Obelisk"
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

>>>>Pour créer un noeud, vous devez prouver que vous possédez des pièces. Disons 10 pièces. Vous envoyez 10
>>>>pièces à l'adresse A, puis vous envoyez 10 pièces de l'adresse A vers l'adresse B.
>>>>Vous ajoutez ensuite une signature en utilisant la clé public de l'adresse A pour signer le message
>>>>dans votre blockchain Obelisk.

>>>>Alternativement, vous pourriez aussi publier la clé publique de l'adresse A puis
>>>>signer un message avec cette clé public. Le noeud doit publier une
>>>>signature à un certain interval de temps, ou à un certain nombre de blocs de la réserve de
>>>>pièces déplacées, afin de maintenir une relation de confiance valide avec les autres pairs.

>>>>De façon alternative également, une preuve de brûlure pourrait être exigée, quand les pièces sont envoyées
>>>>de l'adresse A vers une adresse B qui n'a pas de clé privée. La preuve de brûlure, entrant en conflit
>>>>avec l'exigence que personne ne devrait télécharger la blockchain entière
>>>>depuis le début pour faire fonctionner un noeud complet, est donc improbable.

>>>> Ce système limite le nombre de nœuds Obelisk maximum et limite la
>>>> capacité à faire fonctionner des nœuds Obelisk aux seuls détenteurs de pièces.
>>>> La limite supérieure du nombre de nœuds et le besoin de pièces ajoutent
>>>> une autre couche de protection contre l'attaque dite "Sybil".

>>>Je ne suis pas sur de comment ceci empêche une attaque de type "Sybil".
>>>Est-ce que vous ajoutez simplement un coût au fait d'ajouter un noeud au réseau et par conséquence
>>>une attaque de type "Sybil" nécessiterait un coût financier pour la mettre en oeuvre ?

>>Il s'agit uniquement d'une idée à ce stade. Une amélioration a été trouvée. Chaque noeud Obelisk possède
>>une clé publique. La clé publique est hashé en une adresse, puis 10 pièces sont stockées à un endroit
>>détenu par cette adresse.

>> Cela n'ajoute pas de coût. Vous prouvez simplement que vous possédez 10 pièces et
>> que vous connaissez la clé privée, pour une clé publique dont l'adresse associée contient 10 pièces. Vous
>> pouvez toujours utiliser les pièces.

>> L'idée est que cela définit une limite maximale sur le nombre de nœuds. Si 10 pièces doivent être
>> retenues et qu'il y a 100 millions de pièces, alors cela limite le réseau à 10
>> millions de nœuds. La limite supérieure ne semble pas être mathématiquement utile
>> pour l'instant, mais c'est quelque chose que nous devrions garder à l'esprit.

>> Lorsqu'un nouveau nœud Obelisk est executé, il fera "confiance" à des pairs aléatoires. L'utilisateur
>> peut également ajouter manuellement quelques nœuds qu'il approuve (bourses ou 
>> membres de confiance de la communauté). Un noeud est identifié par son hash de clé publique et trouvé par
>> DHT (table de hachage distribuée). Ce n'est pas comme avec Bitcoin où les nœuds sont des paires IP:port.
>> Vous pouvez déplacer votre ordinateur, l'identité du nœud ne dépend pas de son adresse IP.

>> Nous voulons que le réseau soit sécurisé avec des nœuds aléatoirement choisis. Nous ne voulons pas
>> une situation comme Ripple, où les trois nœuds des développeurs contrôlent le
>> réseau. Cependant, nous voulions éviter une situation dans laquelle quelqu'un gère
>> 200 000 nœuds et tente de collecter les relations de confiance auprès des nouveaux utilisateurs.
>> Ces nœuds d'attaque de type "Sybil" ne peuvent toujours pas faire une attaque des 51% en général, mais tout
>> ce qui augmente le coût d'une attaque est toujours utile.

>> Peut-être que nous le restreindrons afin qu'un nouvel utilisateur ne puisse faire confiance, de manière aléatoire, qu'à un noeud
>> qui possède un solde de pièces. Les relations de confiance existantes ne seront pas rompues si le noeud n'a
>> plus de solde de pièces, mais il n'obtiendra pas de nouveaux utilisateurs aléatoires.

>> Le graphe de connectivité pour les relations de confiance est censé être un
>> graphe connecté de manière entièrement aléatoire. Quelques nœuds (membres de confiance de la communauté, bourses,
>> sites Web, organisations) auront plus de relations de confiance et cela aidera
>> un peu au moment de la convergence pour le consensus sur un bloc. Cela réduit un peu le périmètre
>> du réseau. Certains nœuds seront utilisés pour vérifier le consensus (vous choisissez un
>> lot de bourses ou de clés publiques différentes), ces nœuds n'influencent pas
>> les décisions de consensus, mais sont des "oracles du consensus" pour vérifier si votre noeud
>> converge avec le réseau.

>> Si deux grandes bourses ont un consensus différent pour un bloc particulier, il s'agit
>> d'un problème. Cela pourrait indiquer une déconnexion du réseau ou une attaque sur le réseau.
>> Les bourses peuvent vouloir suspendre la négociation jusqu'à ce que le problème soit résolu.
> Obelisk est le nœud de consensus distribué de skycoin? Je pensais que skycoind était
> le noeud ...

Oui.

Skycoin a une blockchain. La blockchain se trouve ici:
https://github.com/skycoin/skycoin/tree/develop/src/coin. Cela analyse les
blocs et traite les résultats et les transactions non dépensés.

Skywire est le daemon, et a une "architecture de service". Il peut exécuter des services,
comme le service de synchronisation de la blockchain et plus encore. Le meshnet est actuellement
mis en œuvre comme un service Skywire (même si cela pourrait
changer).

Le mécanisme de consensus est en dehors de la blockchain. Les noeuds Obelisk (qui
seront probablement mis en œuvre en tant que service Skywire) ont une blockchain.
Chaque noeud possède une clé publique et celle-ci publique identifie le nœud Obelisk.
Chaque nœud Obelisk a sa propre blockchain (il n'y a pas de pièces dans cette chaîne).
Le noeud crée un nouveau bloc et le signe avec sa clé privée.
Les blockchains Obelisk sont utilisées pour négocier un consensus (déterminer le bloc de tête 
dans la blockchain Skycoin). Obelisk utilise Ben-Or pour un consensus aléatoire. 
Chaque nœud Obelisk possède une liste des autres nœuds auxquels il est abonné.
Ces nœuds influencent les décisions de consensus et de vote pour le nœud local.
Pour les topologies de réseau non pathologiques, le consensus local converge
en permanence vers un consensus global.

Chaque noeud vote sur le bloc suivant de la chaîne. Un noeud propose le bloc suivant
et les nœuds votent sur le successeur. Les votes sont publiés dans les
blocs dans la blockchain Obelisk pour chaque nœud. Votre noeud vote aléatoirement
entre temps et change son vote de temps en temps. Une fois que 40% de
vos pairs ont atteint un consensus (les nœuds auxquels vous êtes abonnés), vous
passez à ce candidat. Le réseau peut voter sur plusieurs branches à la fois, il
ne ralentit pas dans l'attente d'un consensus. Les branches sont réduites à une seule
chaîne au fil du temps. Les divisions de deux ou trois blocs sont normales, mais après quelques
confirmations, la probabilité de l'annulation du bloc diminue
exponentiellement vers zéro. Si une transaction a été exécutée sur toutes les
chaînes candidates, alors elle est exécutée, même si le consensus sur la chaîne particulière
n'a pas encore été décidé.
C'est ainsi que le binaire Ben-Or et Skycoin utiliseront quelque chose de légèrement plus avancé,
et qui est plus rapide lorsqu'il y faut choisir le bloc qui suit parmi plusieurs dans le groupe de consensus. 
Le choix aléatoire est important pour empêcher leblocage des sous-graphes du réseau.
Le processus de vote est une forme de "recuit" où chaque
noeud arrivera au consensus global indépendamment, seulement à partir de ses informations locales.

Le processus de consensus se déroule en public. Un noeud publie des blocs, les signe
avec leur clé privée et les blocs sont répliqués de pair à pair parmi les
abonnés de la chaîne. Ensuite, il y a des "oracles du consensus" qui sont les nœuds
utilisés pour vérifier le consensus mais sans l'influencer. Vous pourriez donc
choisir les clés publiques de certaines bourses et certains membres de confiance de la communauté
et votre noeud les utilisera pour détecter si quelque chose ne va pas. Ceci est utilisé pour
détecter les déconnexions. Cela protège également contre une attaque, dans laquelle un pirate
contrôle votre routeur et peut contrôler les pairs auxquels vous pouvez vous connecter.

Si un nœud se présente sur le réseau et tente de faire accepter une chaîne différente par le réseau
(attaque des 51%, annulation des transactions), il est généralement ignoré.
La plupart des attaques des 51% nécessitent un comportement malveillant d'un nœud, ce qui est automatiquement
détecté et résulte à la suppression de celui-ci par un noeud de
la liste de confiance. La plus simple des stratégies d'attaque des 51% est facile à détecter et à prouver
avec une certitude mathématique comme étant une tentative d'annuler des
transactions, car elle exige des décisions consensuelles suu le bloc précédent.
Elle nécessite la publication de deux blocs signés avec le même numéro de séquence,
donc nous en avons fait une infraction automatiquement bannie pour un noeud.

Nous essayons d'éliminer la dernière attaque des 51% possible, qui survient lorsqu'un
sous-réseau de noeuds se déconnecte (attaque de déconnexion), puis rejoint le
réseau avec un consensus de blockchain différent et tente de le forcer sur le
réseau pour annuler les transactions. La plupart de ces attaques échoueront, car le
sous-réseau n'aura pas assez d'influence.

Cette attaque est encore très difficile à réaliser. Dans le cas où 
une attaque des 51% se produit, une solution consiste à bloquer le réseau et permettre à chaque nœud / utilisateur
de choisir individuellement la chaîne qui est valide, et permettre aux gens d'exclure manuellement les noeuds 
d'attaque. L'oracle de consensus permet à chaque nœud de
savoir, avec une forte probabilité, si l'état est synchronisé et si un consensus global a été atteint ou
s'ils font partie d'un sous-graphe déconnecté. Nous pensons qu'il est possible pour chaque noeud de
savoir avec une forte probabilité d'exactitude, à partir des informations locales, si un
nœud était hors ligne lors d'une décision de consensus, et d'ignorer les nœuds
déconnectés qui apparaissent soudainement et qui tentent de forcer une chaîne sur le réseau.

Avec Bitcoin, si vous avez la plus grande puissance de hachage, vous pouvez annuler les transactions quand vous le souhaitez.

Avec Skycoin, pour annuler les transactions:

- Il est nécessaire de contrôler un grand nombre de nœuds;
- Les nœuds que vous contrôlez doivent être "influents" et fiables dans la topologie du réseau;
- Vos noeuds doivent présenter un comportement d'attaque pathologique extrêmement évident,
  sans que cela ne soit détecté, car la détection entraînerait la perte
  des relations de confiance dont vous avez besoin pour attaquer le réseau;
- Vos nœuds doivent être dans une topologie d'attaque pathologique, sans être
  détectés (la plupart des noeuds robots auront la confiance de très peu d'humains et seront très facilement repérables).
- Vous devez amener les nœuds que vous contrôlez à s'entendre de manière à aboutir
  à une attaque réussie (ce qui n'est pas simple).
- Si l'attaque réussit, vous devez empêcher le réseau d'annuler l'attaque manuellement (très difficile si les gens ont perdu des pièces ou de l'argent en raison de l'attaque).

Pour démontrer une résistance à l'attaque des 51%, vous devez écrire les hypothèses
et créer un modèle mathématique simple pour tester les
conditions dans lesquelles les choses peuvent et ne peuvent pas arriver dans le modèle. Une fois que vous
connaissez les conditions dans lesquelles une attaque est possible, vous essayez de les éliminer,
et si vous ne le pouvez pas, vous les rendez aussi difficile que possible.
Vous augmentez le coût d'une attaque et vous réduisez la probabilité qu'une
attaque spécifique réussira. Vous réduisez ainsi les gains et l'incitation à attaquer.

Le processus de consensus est simple et facile à modéliser, mais non intuitif sans
le voir. Il y aura dans la finalité un site javascript avec une animation du
processus de consensus avec lequel vous pourrez jouer.