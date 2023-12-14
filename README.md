# Workshop Listes Chainées

Aujourd'hui nous allons nous intéresser aux listes chainées en C.

Afin de faciliter la mise en place de workshop, vous trouverez dans ce repository une structure de projet déjà mise en place. Vous n'avez plus qu'à coder !

Fonctions autorisées: **write, malloc, free, printf**

Pour la validation de chaque exercice, vous ne devez pas avoir de memory leak. \
Pour le vérifier, essayez valgrind.

## Ex 0: Votre première liste

Pour commencer, on va devoir s'intéresser à la structure d'une liste chainée, une liste chainée dispose de deux parties, une qui servira de stockage principal de la liste, qu'on appellera `list_t` qui contiendra le premier élément nommé `node_t` et au besoin le nombre d'éléments dans la liste

Tout d'abord créer un fichier dans le dossier include nommé `list.h`

Créer donc une structure `node_s` que vous allez typedef en `node_t` pour faciliter son utilisation qui doit contenir:
- Un `int value` -> une valeur en entier
- Un `struct node_s *next` -> représente l'élément suivant dans notre liste

Pour pouvoir utiliser efficacement cette node nous allons avoir besoin de la liste principal qui va nous permettre de toujours avoir le premier élément de cette liste, nous allons donc créer une structure `list_s` que vous allez typedef en `list_t`:
- Un `int nb_nodes` -> représente le nombre d'éléments de notre liste
- Un `node_t *first` -> représente le premier élément de notre liste


### Initialisation de la liste

Créez une fonction `list_t *init_list();`
Cette fonction doit créer la liste et initialiser ses valeurs. Pour cet exercice, `first = NULL` et `nb_nodes = 0`.

### Initialisation de la node

Faites de même pour les nodes avec une fonction `node_t *init_node(int new_value);` 
Cette fonction doit créer la liste et initialiser ses valeurs. Pour cet exercice, `next = NULL` et `value = new_value`.

### Ajouter un élément dans la liste

Par la suite il va nous falloir une fonction permettant d'ajouter une node prenant en parametre la liste et une node, la fonction devrait avoir comme prototype: `void add_node(list_t *list, node_t *node);`

N'oubliez pas que vous devez ajouter la node à la fin de la liste, il va surement falloir modifier la derniere node existante dans la liste (si elle existe).

*Pensez à incrémenter dans la liste* ;)

### Afficher la liste

Pour tester le bon fonctionnement de votre liste chainée la fonction suivante devra avoir comme résultat: `{value} -> {value} -> NULL`.
Vous devez partir du premier élément de votre liste et arriver jusqu'au dernier en affichant leur valeur et un NULL pour montrer la fin de votre liste.
Prenez comme prototype: `void show_list(list_t *list);`
Libre à vous de choisir quelle fonction utiliser pour afficher ce résultat.

### Supprimer un élément de la liste

Nous voulons enlever des éléments de notre liste. Il faut donc créer une fonction pour s'occuper de ça !
Créez une fonction `void delete_node(list_t *list, int value);`
Cette fonction doit s'occuper de free l'ensemble des élements pouvant être free dans la node, pour l'instant nous disposont que d'un `int` donc rien besoin de free.

(Peut-être que vous devriez vérifier que l'élément que vous supprimer n'est pas le dernier élément de la liste, il pourrait y avoir des problèmes si la `list_t *list` n'est pas modifiée :))

*Faites attention peut-etre qu'il va falloir garder la node précédente pour pouvoir la relier avec la node qui suit celle que nous voulons supprimer*

## Ex 1: Manipulation de votre liste

Pour vous montrer les limites des listes simplement chainées nous allons faire quelques petits exercice.
Reprenez la liste de l'exercice précedent.

### Echanger des valeurs

Créez une fonction `void swap_first_and_last(list_t *list);`
Cette fonction doit échanger les valeurs de la première et de la dernière node, affichez `Nothing to do` si il y a un nombre de nodes inférieur à 2 dans la liste.

*Afficher votre liste pour etre sûr que vos éléments ont bien été échangés.*

### Ajouter une node à un Index

Créez une fonction `void add_node_index(list_t *list node_t *node, size_t index);`
Cette fonction doit ajouter la node à un index précis, plusieurs cas sont possibles:
- cas 1 (index == 0) : Ajouter en premier élément de la liste.
- cas 2 (index > 0 && index < max de la liste) : Ajouter l'élément à l'index requis.
- cas 3 (index >= max de la liste) : Ajouter a la fin (Cela me rappelle un éxercice précédent, pas vous ?)

### Et si on veut changer nos nodes de places ?

Créez une fonction `void swap_node_index(list_t *list, size_t index_one, size_t index_two);`
Cette fonction doit échanger les pointeurs de la node à l'index one et de la node a l'index two (Pensez à bien modifier vos next dans vos nodes ;)), affichez `Nothing to do` si il y a un nombre de nodes inférieur à 2 dans la liste.

*Affichez votre liste pour etre sûr que vos éléments ont bien été échangés.*

## Ex 2: Les listes doublement chainées ?

Maintenant, il suffit de s'embêter à parcourir notre liste, on a compris, on veut du concret.
C'est ce que vous allez apprendre, les listes doublement chainées, permettant plus de manipulations.
Nous allons commencer par modifier l'existant.

### Modifications

Pour commencer, on va devoir s'intéresser à la structure d'une liste doublement chainée, ces listes permettent de naviguer dans les deux sens, c'est à dire du début vers la fin de la liste, mais aussi de la fin vers le début !

Tout d'abord reprenez le fichier dans le dossier include nommé `list.h`

Dans notre structure `node_s` nous allons y ajouter un élément qui nous permettra de bouger dans les deux sens, auparavant nous avions:
- Un `int value` -> une valeur en entier.
- Un `struct node_s *next` -> représente l'élément suivant dans notre liste.
Et nous allons donc ajouter:
- Un `struct node_s *previous` -> représente l'élément précédent dans notre liste.

Pour pouvoir utiliser notre liste de manière optimale nous allons aussi la modifier en y ajoutant le dernier élément de notre liste, nous avions donc:
- Un `int nb_nodes` -> représente le nombre d'éléments de notre liste.
- Un `node_t *first` -> représente le premier élément de notre liste.
Et nous allons donc ajouter:
- Un `node_t *last` -> représente le dernier élément de notre liste.

### Initialisation de la liste

Modifiez la fonction `list_t *init_list();`, pour que toutes ses valeurs soient initialisées.

### Initialisation de la node

Faites de même pour les nodes en modifiant la fonction `node_t *init_node(int new_value);`
Cette fonction doit donc initialisé un nouvel élément le `node_t *previous`.

### Ajouter un élément dans la liste

Par la suite il va nous falloir modifier la fonction: `void add_node(list_t *list, node_t *node);`
Quand nous ajoutons à la fin, il va falloir modifier le previous de notre node.

N'oubliez pas que vous devez ajouter la node à la fin de la liste, il va surement falloir modifier une valeur dans la `list_t *list`.

### Afficher la liste en reverse !

Pour tester le bon fonctionnement de votre liste doublement chainée la fonction suivante devra avoir comme résultat: `NULL -> {value} -> {value}`.
Vous devez partir du dernier élément de votre liste et arriver jusqu'au premier en affichant leur valeur et un NULL pour montrer le début de notre fonction.
Prenez comme prototype: `void show_list_reverse(list_t *list);`
Libre à vous de choisir quelle fonction utiliser pour afficher ce résultat.

### Supprimer un élément de la liste

Pour supprimer un élément de notre liste, nous allons devoir modifier deux trois choses
Modifiez la fonction `void delete_node(list_t *list, int value);`
Maintenant elle va devoir relier l'élément précédent et l'élément suivant, et après delete notre élément actuel.

*Vous n'aurez plus besoin de garder l'élément précédent car il est maintenant stocké dans notre node actuel* :)


## Ex 3: Manipulation de votre liste chainée

Pour vous montrer que les listes chainées c'est super cool, nous allons faire des exercices :D.
Reprenez la liste de l'exercice précedent.

### Echanger des valeurs

Modifier votre fonction: `void swap_first_and_last(list_t *list);`
Maintenant que vous avez directement accès aux deux éléments grâce à votre liste, ça devrait être sympa non ?

*Affichez votre liste pour etre sûr que vos éléments ont bien été échangés.*

### Ajouter une node à un Index

Modifiez votre fonction: `void add_node_index(list_t *list node_t *node, size_t index);`
Même fonctionnement que tout à l'heure mais pensez à bien relier vos nodes entre elles ;)
Je vous remets les cas:
- cas 1 (index == 0) : Ajouter en premier élément de la liste.
- cas 2 (index > 0 && index < max de la liste) : Ajouter l'élément à l'index requis.
- cas 3 (index >= max de la liste) : Ajouter a la fin (Cela me rappelle un éxercice précédent, pas vous ?)

*Affichez votre list en reverse pour être sur que vous avez tout bien relié.*

### Et si on veut changer nos nodes de places ?

Modifiez votre fonction: `void swap_node_index(list_t *list, size_t index_one, size_t index_two);`
Pareil que tout à l'heure, mais comme les exos d'avant pensez à bien relier vos previous entre eux.

(Normalement en ayant accès aux previous ça devrait etre plus simple)

*Affichez votre liste en reverse pour etre sûr que vos éléments ont bien été échangés.*

### Allons nous amusez un peu

Créez une fonction qui tri par ordre croissant notre liste chainée,
prenez ce prototype: `void sort_list(list_t *list)`

(Je n'ai plus besoin de vous guider n'est ce pas ?)

### Bon ça ne devrait pas être bien compliqué

A l'inverse de l'exercice d'avant.
Créez une fonction qui tri par ordre décroissant notre liste chainée,
prenez ce prototype: `void sort_list_reverse(list_t *list)`
