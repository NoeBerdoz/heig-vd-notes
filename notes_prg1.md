# Notes
Toolchain -> MinGW
C++20
CMAKE 
-DCMAKE_CXX_FLAGS="-Wall -Wextra -Wconversion -Wsign-conversion -pedantic"

# Générales
Cyberlearn

Possibilité d'accéder aux slides de cours
Mise en place de fichiers/devoirs dans laboratoire

# Cours Prog
## Niveau de langage 
Différence langage bas niveau / haut niveau

*The main difference between high level language and low level language is that,
Programmers can easily understand or interpret or compile the high level language
in comparison of machine. 
On the other hand, Machine can easily understand the low level language in
comparison of human beings.*

C++ est un langage de haut niveau

Le langage haut niveau est équipé d'un compilateur pour que la machine puisse
interpréter le code

Le compilateur est un programme spécial qui traduit la description de haut
niveau (le code C++) en instructions machine pour un processeur particulier

Langage de bas niveau : instructions machine pour un CPU particulier
Le code machine généré par le compilateur sera différent selon le CPU visé,
mais le
programmeur qui utilise un langage de haut niveau ne doit pas s’en inquiéter.

(Différence compilateur / interpréteur)
*Interpreter translates just one statement of the program at a time into machine
code. Compiler scans the entire program and translates the whole of it into machine
code at once.*

# C++

En C++ on peut faire de la programmation procédurale, générique, orienté objet

En C on ne peut que faire de la procédurale

## Variables

Une variable permet d'adresser une valeur

En C++ elle doit être composée d'un type, d'un nom et d'une valeur

Il est important d'initialiser la valeur de la variable

toute instruction se termine par ';', donc à mettre en fin de variable

```C++
int monEntier = 6;

int monEntier; /* Possible mais bad practice*/
```

Le type permet de définir la taille à réserver dans la mémoire
ex: un int prends moins de place qu'un string

Le nom aide à retrouver la valeur de la variable dans la mémoire

On ne peut pas initialiser un int avec une valeur string, cela 
créerai une erreur d'exécution

**En C++ on recommande de déclarer les variables le plus tard possible** à l'inverse de C

Une variable initialisée sans valeurs en mémoire n'est pas vide 
mais est adressée avec une valeur indéterminée


### Initialisation de variable
l'initialisation de la variable est l'attribution de sa valeur de base
Ceci n'est pas obligatoire mais est une bonne pratique à mettre en place

initialisation commune : int age = 6:

initialisation par constructeur : int age(6);

initialisation uniforme depuis C++11 : int age{6};

TODO QUESTION: quand utiliser initialisation uniforme ?


### Opérateur d'affectation

Le contenu d'une variable est géré dynamiquement par 
- l'affectation '='
- l'incrémentation '++', décrémentation '--'
- résultat d'une saisie 'cin >>'

Pour déclarer plusieurs variables sur une ligne :
```C++
int n = 0, m = 0;

// ATTENTION FAUX
int n, m = 0; // ici n n'est pas initialisé et m n'est pas typé
```

### Identificateur / nom de variable
Un identificateur / nom de variable

- Ne pas contenir d'espace
- Ne pas contenir de symbole
- doit commencer par lettre ou '_'
- peut contenir lettres, chiffres et '_'
- est sensible à la casse (maj et min)
- n'a pas de limite de longeur
- ne doit pas être un mot réservé C++

### Constantes
Certaines valeurs ne changent pas au cours de l'exécution du programme
Une telle attribution doit être faite par le biais d'une constante

Les constantes par défaut sont du premier type qui permet de les contenirs
on peut préciser le type en ajoutant des lettres à la fin du nombre
un suffixe (fin) U ou u pour **unisgned**
suffixe L ou l pour **long**
ex: combinaison des deux avec en premier l'attribution de la base: const AHOUAIS = 0x123LU


```C++
const double PRIX_CAFE = 3.90
```

Son initialisation à la déclaration est obligatoire !
Good practice : Une CONSTANTE s'écrit en majuscule

Les constantes évites l'apparition de "*magic number*" (résultat inexpliqué)
Elles améliorent la maintenance du code

Il est possible d'utiliser une constance créer lors de la compilation et non l'exécution
 ```C++
 constexpr int NUMBER = 0 
 ```
Ceci permet au compilateur de réaliser certaines optimisations
Elle peut être utilisé pour des déclarations de fonction
L'avantage de le faire à la compilation et que le processeur
doit réaliser le calcul une seule fois et non à chaque appel de constante comme à l'exécution avec const

````
const int NUMBER_CONST = 5;

constexpr int NUMBER_CONSTEXPR = 5;

magic = 5 + NUMBER_CONST + NUMBER_CONSTEXPR; 
/* 
En exécution -> magic = 5 + NUMBER_CONST + 5
le NUMBER_CONSTEXPR sera déjà attribué et remplacé par la valeur, 
pas besoin d'aller chercher à nouveau la valeur mémoire pour 
NUMBER_CONSTEXPR
*/ 
````

# Types
bool
fait 1 bit, sois 1 sois 0

Pointeurs
Stocke une adresse dans la mémoire
représenté par une étoile
int*
int**
double*

## Nombres :
1 bit est réservé pour le signe du nombre !

Donc sur 32 bits, il il y a 2^31 possibilité et 1 bit réservés pour le moins

¦short¦  16 bits
¦int      ¦  16 bits
¦long(int)    ¦ 32 bits (représente + de 2 milliards)
¦long long(int)   ¦ 64 bits

integer can be positive and negative
integer : 1
````C++
int nombreN = 1 
````

float : 1.1 -> nombre sur 32bit
double : 1.0 -> nombre sur 64bit
longdouble -> plus de valeurs

un nombre informatiquement est structuré ainsi :
1,234 = 12,34 * 10^-1
        
        | mantisse | exposant |
[+ ou -]|   1234   |    -3    |


float sur 32 bits :

        | mantisse | exposant |
[+ ou -]|    32    |    8     |

Donc en gros, 7 décimales après la virgule maximum 
car exemple 2^23 = 8 388 608 -> ,8 ,3,8,8 ,6,0,8 

Donc en gros, un chiffre avec + de 7 chiffres après la virgule 
ne sera plus précis en float

**par défaut C++ prend les float en double**
donc pour réellement mettre un float il faut mettre un f à la fin du nombre
```C++
float b = 1.1234567f;
```
(à utiliser dans le cas où on n'a besoin d'optimiser les performances et la mémoire
au maximum)

le type int est signed par défault (-2 milliards jusqu à +2 milliards)

3 types réels : float, double, long double

(entiers (int), réels (float), chaine de caractère, booléen)

pour déclarer un int:
signed == int == signed int

pour unsigned int:
unsigned == unsigned int

signed = avec signe - ou sans et unsigned = sans signe -

```C++
int valeur = 42; // décimal base 10
int valeur = 0b 101010; // binaire base 2
int valeur = 0 52; // octal base 8
int valeur = 0x 2A; // hexadécimal base 16
```

char permet la définition **d'un seul** caractère selon la table ASCII
pour réaliser un charactère UTF-8 il faudra 2 char, pour UTF-16, 3 char...
char : équivaut à un byte de donnée donc 1 octet, un byte = 8 bit
```C++
char Z = 90
```
char est unsigned ou signed par défaut dépendamment du compilateur
char équivaut à un seul caractère

### Priorité des opérations
Opérateurs multiplicatifs ont la priorité sur les additifs
Pour changer l'ordre des calculs il faut ajouter des paranthèses
2 * (3 + 4) = 14
les opérations sans parantèses et de même niveau se lisent de gauche à droite

Attention, l'ordre des additions et soustractions successives peut avoir un impact
à cause des dépassements ou des arrondis

````C++
float a = 2e38f;
cout << a + a - a << " " << a - a + a << endl; // résultat sera inf 2e+38
// car le a + a au début sort du scope de float, donc résultat infini - a = infini
````

### Conversion nombre réel en nombre entier (Opérations explicites)
La librairie <cmath> fournit les fonctions d'arrondi
  - trunc -> l'entier en tronquant après la virgule 
             (2.3 -> 2.0 | 3.8 -> 3.0 | -5.5 -> -5.0 | -3.8 -> -3.0)
  - round -> l'entier le plus proche
             (2.3 -> 2.0 | 3.8 -> 4.0 | -5.5 -> -5.0 | -3.8 -> -4.0)
  - floor -> l'entier plus petit
             (2.3 -> 2.0 | 3.8 -> 3.0 | -5.5 -> -6.0 | -3.8 -> -4.0)
  - ceil -> l'entier plus grand
            (2.3 -> 3.0 | 3.8 -> 4.0 | ->5.5 -> 5.0 | -3.8 -> 3.0)

    

# Opérations implicites
Lors d'une opération mélangeant des types, 
il se passe une conversion arithmétique entre entiers, 
exemple:
int, long -> long
int, long long -> long long
unsigned int, unsigned long -> unsigned long

Si il y'a des mélanges entre signé et non signé,
on prend unsigned car il permet plus de possibilités
int, unsigned int -> unsigned int
long, long long, unsigned long long -> unsigned long long

Contrairement aux opérations explicites, les opérations implicites
vont automatiquement convertir les types selon les instructions de l'OS
(différences entre Windows et Linux/Mac OS X)
sur Windows : 
unsigned int, long -> unsigned long

sur Linux/Mac OS X :
unsigned int, long -> long

Les conversions implicites peuvent entraîner des pertes de précision 
ou des integer overflow

il est possible de configurer le compilateur pour qu'il flag Warning en 
cas de conversions implicites dangereuses 
Même chose pour les mélanges entre *signed* et *unsigned*

ex: nombre de conversion implicites effectuées ici:
```
char c = 'A';
int n = 7;
long p = 10;

auto r = n + c + p;
```
7int+ 'A'char + 10long
d'abord le char est transformé en int
le résultat de 7 + 'A'(65) va être transformé en long
il y'aura donc deux conversions implicites pour r = 82

ex2:
```
float 1.25
2 int
char 'A'
2 * 1.25 + 'A'
```
3 conversions implicites
d'abord char 'A' à int 65
ensuite 2 int à 2.0 float
ensuite 65 int à 65.0 float

ex3 
char c = 'A';
int n = 7;

auto r = (char) n + c'

2 conversions implicites
char c à int
(char) n à int
résultat 65 + 7 ? 72

ex4:
int n = 7;
double z = 5.5;
auto r = (float)z + n/2

1 conversion implicite
n int / 2 int = 3 int, le 3 int sera converti en float

ex5:
int a = -2;
unsigned b = 1;

auto r = a + b;

1 seule conversion implicite, de int à unsigned int
un int en rapport un un unsigned int est converti implicitement en unsigned int 
car unsigned int prend plus de places mémoires
le résultat sera indéfini, sur windows se sera 4294967295

ex5
Que vaut x ?
int i = 5, j = 11;

double x = j / i + .5
réponse : x = 2.5




## Opérations sur les types

attention sur char, short, int, long, long long
les opérateurs +, -, * se comportent comme pour les réels

L'opérateur */* effectue une division entière, le résultat sera un entier non un réel 
int 5 / int 2 = 2 !!!

% = modulo -> 5%2 = 1

il est possible de faire des opérations d'affectation composée
+=, -=, /=, %=, *=

# Incrémentation
attention au placement de l'incrémentation
```C++
int compteur = 42
compteur++;     // compteur vaut 43
++compteur;     // compteur vaut 44
int pre = compteur ; // compteur vaut 45
                     // et pre vaut 45
int post = compteur ++; // compteur vaut 46
                        // mais post vaut 45
```

# Dépassement d'entier (integer overflow)

```C++
unsigned vMax = numeric_limits unsigned max
unsigned vOver = vMax + 1
cout << vMax << " + 1 = "<< vOver << endl
```
Résultat = 4294967295 + 1 = 0


## Synthaxe

Pour inclure un module
```C++
#include <module>
```

**cout** -> character output
**endl** -> end line

## main
Tout programme C++ contient une fonction main 

## namespace
Espace de nom, zone de déclaration d'identificateur
namespace -> manière d'attribué une valeur sans conflit
permet au compilateur d'attribuer un nom sans conflits

Si, par exemple, deux développeurs définissent des fonctions
avec le même nom, il y aura un conflit lors de l'utilisation
de ces fonctions dans un programme. Les espaces de nommage
permettent de résoudre ce problème en ajoutant un niveau supplémentaire
aux identificateurs.


```C++
#include <iostream>

using namespace std; # déclaration d'identificateur espace de nom

int main() {
    cout << "Hello, World" << endl;
    return 0; /* Veut dire qu'il n'y a pas eu d'erreur */
   }
```

## Erreurs
## Erreurs de syntaxe

Erreur classique - oublier un point virgule
Lors d'une erreur de synthaxe, le programme ne compile pas 

```C++
cout << "Hello World"" << endl
```

## Commentaires
Explications données à la personne qui lit le code
Ignoré par le compilateur 
```C++
/* commentaire multi line */
// commentaire single line
```

### Erreurs execution

Le résultat n'est pas conforme aux attentes, le programme est compilé correctement
```C++
cout << "hollo world" << endl;
```

Certaines erreurs d'exécutions graves génèrent une exception
Une erreur à l'exécution va interrompre le programme

Erreurs qui génèrent une exception : (divide by zero)
```C++
cout << 1/0;

impossible de diviser par 0
```

### Erreur d'édition de liens (link error)
C++ a une seule fonction principale nommée **main**

C++ est case sensitive


# Pseudo Code
-> Compréhension du problème 
-> Description d'un algorithme en pseudo code
-> Tester l'algorithme en pseudo code
-> Écrire l'algorithme en code réel
-> Compiler et tester le programme

Le pseudo code peut aussi servir en équipe
Il permet aux collaborateurs d'avoir une approche simple du code et de la problématique
Il est plus simple de comprendre un pseudo code que du réel code




# Binaire 

Le binaire est en base 2 

(3) base 2 = 00000011
(10) base 2 = 1010


(-(nombres de possibilités que l'on peut représenter
en base 2 = N bits à N puisssances 2)-)

------------------------------------------------------------------------------------------------------------------
------------------------------------------------------------------------------------------------------------------
------------------------------------------------------------------------------------------------------------------
------------------------------------------------------------------------------------------------------------------
# Suite cours
Revoir les types Chapitre 2, slides ~30


# Remarques 
Revoir édition de lien 
Revoir les types d'erreurs


# Tests
Critères :
- Qualités des entêtes de (sous)programmes (pour chaques fichiers)
  - Autheur, date de modif, objectif

pts
-2 Qualités et pertinence des commentaires, seulement quand nécessaire, en anglais si code en anglais
-2 Indentation et lisibilité générale du code
-2 Utilisation correcte des librairies (limiter leur utilisation le plus possible, utiliser seulement quand nécessaire)
-2 Respect du style de programmation : sois camelCase, ou snake_case pas mélange etc
-2 Choix des identificateurs (noms de variables clairs et pertinents, pas trop long, fait pour un néophyte du contexte)
-4 Déclaration et utilisation de constantes ou variables (pas de variables inutiles, utiliser les const quand nécessaire)
-4 Structure et découpe en sous-programmes / fichiers
-4 Qualité des paramètres
-4 Qualité et choix des algorithmes (pas de doublons et optimisations)
-2 Respect de la donnée

Pénalités
- retard (1.0 + 0.5 par jour ouvrable)
- impossibilité de compiler (fichier sources incomplets ou différent) (1pts)
- travail seul (lorsque possible / demandé de travail à deux) (0.5 pts)
- Utilisation d'éléments non vu en théorie (0.5pts)
- nom de fichier mentioné dans l'en-tête ne correspond pas à la réalité (0.3)


