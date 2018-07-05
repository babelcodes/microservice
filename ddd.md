# Domain Driven Design - DDD

> DDD est l’acronyme de Domain Driven Design. Ce n’est ni un framework, ni une méthodologie, mais plutôt une approche décrite dans l’ouvrage du même nom d’Eric Evans. Un de ses objectifs est de définir une vision et un langage partagés par toutes les personnes impliquées dans la construction d’une application, afin de mieux en appréhender la complexité.

# Modélisation du domaine

Cette activité doit nous permettre de nous attaquer à la complexité du problème/métier à résoudre:
- Quels sont les « objets » mis en jeu ? 
- Quels sont les comportements, les règles qui régissent les interactions ? 
Le modèle du domaine doit être "ubiquitous", c’est-à-dire partagé par l’ensemble des acteurs contribuant à la construction du produit. Les noms et les verbes utilisés font partie de l’ubiquitous language. L’architecture logicielle qui va porter notre application devra être au service de notre domaine.

# Qui modélise ? Quand ?

En début d’itération, l’équipe définit et échange sur les User Stories à traiter et s’accorde un temps de réflexion pour partager sa vision du modèle du domaine. Utilisateurs et experts métiers apportent leur connaissance du problème à résoudre ; développeurs et architectes fournissent leur point de vue d’experts techniques. L’équipe doit garder en tête que le modèle retenu a une limite de validité (modèle valide sous contraintes), puisqu’il est conçu pour :

- Modéliser une problématique bien précise et uniquement celle-ci : celle du __Bounded Context__ en question
- Répondre au problème qui se pose __aujourd’hui__ : demain, nous pourrons raffiner le modèle
- Être implémentable techniquement : si les composants et mécanismes purement techniques (relatifs à l’implémentation logicielle) ne font pas partie du domaine et ne doivent pas le polluer, la modélisation ne doit pas non plus ignorer ce qui effectivement réalisable et ce qui ne l’est pas !

> La représentation que l’on donne n’est qu’un moyen d’échange, de partage de la compréhension par l’ensemble des acteurs. 


# Que mettre dans un modèle ?

On peut notamment citer :

- Les _Aggregate Roots_ : des objets ayant une identité et représentant chacun une unité de cohérence (ex: un agriculteur, une commande)
- Les _services du domaine_, représentant des opérations agissant sur plusieurs objets (ex: une opération bancaire)
- Les _repositories_, abstraction du moyen de stockage des _Aggregate Roots_
- Les _specifications_, qui représentent des ensembles de critères et permettent d’exprimer des règles métier (cf. design pattern du même nom ?)
- Les _évènements du domaine_, qui matérialisent des évènements importants survenus dans le domaine

# Architecture

## Services applicatifs

- Cette couche a pour responsabilité de coordonner les activités de l’application
- Elle ne contient pas de logique métier
- récupérer les objets du domaine via le repository pour “injecter” la dynamique dans le domaine

## Domaine 

- Les classes du domaine
- couplé à aucun mécanisme technique
- Elle utilise une __spécification__ afin de savoir si l’action de mise en vente est valide ou pas
- Une fois le traitement métier de mise en vente réalisé, un __évènement du domaine__ est produit pour notifier tous les composants intéressés
- Cette gestion reposant sur des domain events permet donc de mieux séparer les responsabilités des différents objets

## Infrastructure

- l’anti-corruption
- l’isolation de la complexité technique de l’application
- la persistance des données du modèle
- la communication entre les différentes couches


# Points positifs de l’architecture

- La modélisation du domaine est au plus proche de la problématique des utilisateurs, et on a réussi à construire un code très expressif dans lequel il est aisé d’identifier une règle, un comportement. La __plasticité__ du système facilite les __changements__ fréquents dont ont besoin les utilisateurs.
- Puisque la modélisation du domaine met l’accent sur l’identification des interactions dans le système, il devient plus naturel de mettre en oeuvre __une interface utilisateur orientée tâches/activités__
- Les __échanges__ sont facilités entre profils fonctionnels et techniques sur les fonctionnalités offertes par l’application, et les règles (les comportements) qu’elle implémente
- Les développeurs bénéficient d’une __meilleure compréhension du métier__ à la lecture du code du domaine : un nouveau développeur peut plus facilement appréhender le code et le fonctionnel de l’application
- La __testabilité fonctionnelle__ est facilitée : les règles métier sont explicitées, concentrées dans une couche bien définie de l’application, et donc plus facilement testables par un outil de tests fonctionnels automatisés
- La __robustesse vis-à-vis des changements dans le SI__ et de l’architecture technique est améliorée, grâce à la couche d’infrastructure / anti-corruption


# Resources

- https://blog.octo.com/domain-driven-design-des-armes-pour-affronter-la-complexite/
- https://msdn.microsoft.com/en-us/magazine/dd419654.aspx