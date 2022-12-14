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

### Variables
Il y'a plusieurs types de variables 

#### extern
Pour déclarer une variable globale, il faut le faire dans un fichier header '.h'
toutefois si la variable est déclarée classiquement, elle sera exécutée à chaque include, 
ce qui créera un conflit de valeurs dupliquées pour une même variable.

Afin de déclarer une variable globale utilisable au-delà du fichier 
de déclaration, il est possible de la déclarer avec **extern**.

#### static
Une variable déclarée **static** permet de créer des variables hybride entre locales
et globales.
Contrairement à une variable locale, une variable static est mémorisée même en sortie de fonction
Cela peut être utile dans le cas par exemple d'un compteur au sein d'une fonction
```C++
f();
void f() {
    static int compteur;
    compteur++
    cout << "appel #"<< compteur << endl;
}

int main() {
    for (int i = 0; i < 5; ++i) {
        f();
    }
```

Une variable **static** et **extern** n'est visible que depuis le fichier cpp où elle est déclarée.
Elle aura un comportement de variable globale, uniquement dans le fichier de déclaration.

#### Méthode d'allocation d'une variable
En C++ il y'a 3 manières d'allouer de la mémoire pour y stocker des données

- Automatique
  - pour lees variables locales
  - existent pendant la durée d'exécution du bloc où elles sont déclarées (aka stack selon Gwenaël)
- Statique
  - pour les variables globales, statiques, et les constantes littérales
  - existent pendant toute la durée du programme 
- Dynamique 
  - créées et effacées explicitement par le programmeur avec les instructions **new** et **delete**

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

```
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
Les entiers peuvent être écrits dans 4 bases mais ils sont toujours stockés en binaire
int decimal = 42;
int binaire =  0b101010;
int octal 042;
int hexadecimal = 0x42


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
int permet à un range dee -2 à 2 milliards pour 4 octets en mémoire

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
(à utiliser dans le cas où on a besoin d'optimiser les performances et la mémoire
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

En ce qui concerne l'évaluation des expressions and et or (&& ||)  
Elle se compile de gauche à droite et s'arrête **dès que possible**

Donc (i++ || j++) si i++ true, j++ ne sera pas exécuté 

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
Les conversions implicites sont gérés par le compilateur
les conversions explicites sont gérés par le programmeur (cast)
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

Par contre si il y'a des opérations entre type signé supérieur au type non signé, 
la conversion dépend des données concernant l'instruction, si les valeurs du unsigned sont représentable en 
type signed, c'est le type signed qui primera
unsigned int, long tel que int est compris dans long, -> long 
unsigned int, double tel que int n'est pas compris dans double -> unsigned int 

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

ex6
cout << 15U / -2LL << endl;
15 unsigned sera mis en 15 long long
15LL / 2LL = -7 LL

## Opérations sur les types

attention sur char, short, int, long, long long
les opérateurs +, -, * se comportent comme pour les réels

L'opérateur */* effectue une division entière, le résultat sera un entier non un réel 
int 5 / int 2 = 2 !!!

% = modulo -> 5%2 = 1

il est possible de faire des opérations d'affectation composée
+=, -=, /=, %=, *=

## Promotion de type vs Ajustement
Promotion entière : char/short -> int
Promotion réelle : float -> double

Les autres conversions sont des ajustements de types qui peuvent potentiellement
influencer la valeur


## Fonctions de manipulation
*fixed* permet d'afficher un chiffre avec 6 chiffres après la virgule
*scientific* affichage scientifique avec les e
*setprecision()* permet de définir le nombre de digits à afficher (après la virgule pour fixed et scientific mais pour tout les digits avec default)

# Incrémentation
attention au placement de l'incrémentation
```C++
int compteur = 42
compteur++;     // compteur vaut 43
++compteur;     // compteur vaut 44
int pre = compteur ; // compteur vaut 45
                     // et pre vaut 45
int post = compteur++; // compteur vaut 46
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


## Condition et comparaison
Attention à l'égalité '==' avec les nombres réels
```
cout << boolalpha;
cout << 1.0 / 3.0 << endl; // 0.333333
cout << (1.0 / 3.0 == 0.333333) << endl; // false

const double EPSILON = 1E-6;
cout << ( abs(1.0 / 3.0 - 0.333333) < EPSILON ) << endl; // true
```

La Loi de Morgane est : 
!(A and B) = (!A or !B)
!(A or B) = (!A and !B)

un entier 1 = true, 
un entier 0 = false

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



# Conditions
```C++
if (condition) {

} else {
  
  }
```
Le else est optionnel 

il est possible mais NON recommandé de faire un if sur une ligne sans accolades
(bad practice)

Pour tester plusieurs conditions, utiliser else if
```C++
if (condition) {

} else if (condition2) {
    
} else {

}
```

# Boucles
while
A une condition d'exécution 
*tant que* selon valeur boolean 

for
When you know exactly how many times you want to loop through a block of code, use the for loop instead of a while loop:
```
const int COLONNES(5), LIGNES(3);
const int LARGEUR(3);
for (int i = 0; i < LIGNES; ++i) {
for (int j = 0; j < COLONNES; ++j) {
int ij = j + COLONNES * i;
cout << setw(LARGEUR) << ij;
}
cout << endl;
}

0 1 2 3 4
5 6 7 8 9
10 11 12 13 14
```

for (initialisation; condition; action) {
    instruction;
}

initialisation;
while (condition) {
    instruction;
    action;
}

for (statement 1; statement 2; statement 3) {
// code block to be executed
}
Statement 1 is executed (one time) before the execution of the code block.

Statement 2 defines the condition for executing the code block.

Statement 3 is executed (every time) after the code block has been executed.


# Switch 
Mettre le default: à la fin, elle peut être mise partout mais good practice de mettre à la fin
le break permet d'arrêter le switch si case true

les cases sont unique, on ne peut pas dire un case, 1, 2, 3...
mais case 1; case 2; case 3;
pas possibilité d'intervalle

si il n'y a pas de break il prend l'information jusquau break même si le case est un default

# Enum
```C++
enum JourDeLaSemaine { DIMANCHE, LUNDI, MARDI, MERCREDI, JEUDI, VENDREDI, SAMEDI, DIMANCHE }
```
convention de nom pour élément énum = TOUT MAJUSCULE

enum Class
le nom de l'enum commence par une MAJUSCULE

on ne peut pas attribué la valeur int directement à un enum
ex jourConge = 1 -> pas possible
mais 
    jourConge = DIMANCHE
    jourConge = joursFerier
    jourConge = JoursDeLaSemaine(1)
    jourConge = (JoursDeLaSemaine)1
    

# Gestion des erreurs d'entrée
**cin.fail()** -> booléen qui indique si il y'a une erreur
**cin.clear** -> réinitialise l'indication d'erreur
**cin.ignore(streamsize n, int delim = EOF)** -> permet de retirer jusqu'à n caractères du flux, ou jusqu
ce qu'on rencontre le caractère *delim* (par défaut la fin du fichier)

*good* -> true -> pas d'erreur 
*eof* -> true -> fin de fichier 
*fail* -> true -> erreur logique sur l'opération entrée/sortie et erreur de lecture/écriture sur opération entrée sortie
*bad* -> true -> erreur de lecture/écriture sur l'opération entrée sortie


# Fonctions
La déclaration d'une fonction en C++ se fait par son prototype, le prototype démontre les paramètres de la fonction.  
La fonction est définie dans un deuxième temps après sa déclaration.

```C++
int f(int val); // déclaration = prototype

int main() {
    int a = f(0);
}

int f(int val) {  // définition
    return val + 42;
}
```
Ce qui est obligatoire pour la déclaration d'une fonction est le type des paramètres et l'ordre de ceux-ci

C'est uniquement dans la déclaration d'une fonction que l'on peut attribuer une valeur par défaut aux paramètre. 

Les paramètres d'une fonction en C++ peuvent se transmettre
- par valeur (valeurs paramètre transitoire)
    Les paramètres doivent être typés la même chose que les types de variable adressés
    on peut faire passer une valeur const typé en paramètre typé sans const, car par valeur
    ne modifie pas la const avec la même adresse mémoire mais modifie une copie non const

- par référence (valeurs paramètre persistent)
    se déclare avec '&' en fin de typage de paramètre
    ```C++
      void testSwitch(int& a, int& b) {}
    ```
    On ne peut pas passer une constante en paramètre par référence
    le type du paramètre doit être le même que le variable adressée
    si le type transmis en paramètre n'est pas le même que le type 
    adressé en référence, il y aura une erreur de compilation, 
    on ne peut pas passer une constante litérale (genre un type non variablé)
    ex: 67, 'A', "HELLO" ne peut pas être passé en paramètre référencé, il 
    faut que ce soit une variable.
  - par référence constante
    se fait lorsque le type du paramètre est const et est référencé avec '&'
    est utile pour les types composés (string, tableaux, classes en paramètres)
    car permet d'économiser une copie en mémoire est et donc moins gourmand en performance
    toutefois on ne peut pas modifier la valeur d'une constante

    
## Surcharge de fonction
Surcharger une fonction est le principe d'utiliser le même nom de celle-ci 
mais en distinguant les paramètres.
Le compilateur choisira la fonction à utiliser.

Toutefois les éléments suivants ne permettent pas de définir une surcharge de fonction :
- Le type de retour
- Les valeurs par défaut des paramètres
- La présence d'un const pour un paramètre passé par valeur
    
On peut surcharger une fonction en faisant varier le type de passage d'un paramètre : 
- Par valeur
- Par référence
- Par référence constante

Attention, il ne faut jamais faire une surcharge par valeur et une autre par référence

# Return

Tout ce qui se trouve après un return ne sera jamais exécuté
Une fonction qui ne retourne pas de valeur n'est pas obligée de contenier le 
terme return, l'accolade de fin '}' permet au compilateur de ne rien retourné 
et de finir l'exécution de la fonction.

Une fonction peut avoir un retour en constexpr pour constexpression
qui sert à évaluer des valeurs au moment de la compilation
ce qui optimisera les performances du code

# Référence

Un élément déclarer avec le caractère '&' en fin de type et traités comme référence
```C++
int
main() {
    int a = 5
    int& b = a
    cout << a << " " << b << endl
    b = 3 
    cout << a << " " << b << endl
}
Va afficher  5 5 puis 3 3 
car b étant une référence à a, si b ou a est changé, la référence est aussi 
modifiée
```

# assert
Lorsque il faut stopper l'exécution d'un code suite à des conditions non remplie, il est possible de déclarer un *assert*

**false** -> écrit un message dans *cerr* et termine le programme avec abort
**true** -> ne fait rien
    
```C++
#include <cassert>
char intToHexa(int value) {
    // arrêt si pas convertible
    assert(value >= 0 and value <= 15);
    
    if (value < 10) // '0' - '9'
        return char('0' + value);
    else // 'a' - 'f'
        return char('a' + value - 10);
}
```

Le assert doit être utilisé en phase de développement, 
Sa déclaration permet de gérer des erreurs de programmation et non d'exécution   
 
Il peut être désactivé avec la macro **NDEBUG**
```C++
#define NDEBUG
...
#include <cassert>
...
```


# Tableaux classiques

les tableaux classique se déclarent s'implement avec []

type nom[capacité]

Les tableaux classiques sont limités,
leur capacité est constante et doit être déclarée
Il faut stocker cette capacité dans une variable annexe
On ne peut pas retourner un tableau classique depuis une fonction 
Il n'y a pas de contrôle sur les bornes d'accès

    
# Function algorithmique
#include <algorithm>
[Documentation en ligne](https://fr.cppreference.com/w/cpp/algorithm)

distance(v.begin, v.end)
retourne le nombre d'élément entre begin et end, end compris

la librairie algorithme n'a pas accès au vecteur mais uniquement a ses éléments par itérations
Si il faut modifier la capacité du vecteur, il faut le faire avec les fonctions prédisposée à modifier le vecteur:
- transform()
- fill() / generate()
- copy()
- remove()
- replace()
- reverse() / rotate() / shuffle()
- sort()
...

<iterator>
pour traiter la valeur d'un iterateur il faut ajouter un '*' au début
par exemple min_element -> *min_element

# Algorithmes de tris

## Bubble sort / Tri à bulles
-> Compare deux éléments et les permutes si ils ne sont pas bien ordonnés
1, 2, 4, 3, 5, 6

1 -> 2 OK, 2 -> 4 pas ok, 2 -> 3 OK, 3 -> 4 OK, 4 -> 5 OK 5 -> 6 OK
output: 1, 2, 3, 4 , 5, 6

Pseudo code :
```C++
Step 1: For i = 0 to N-1 repeat Step 2
Step 2: For J = i + 1 to N – I repeat
              Step 3: if A[J] > A[i]
              Swap A[J] and A[i]
              [End of Inner for loop]
              [End if Outer for loop]
Step 4: Exit
```

si 1, 4, 3, 2, 5, 6
il va falloir plusieurs itérations pour trier

La valeur mathématique d'un bubble sort est O(n^2)

## Insertion Sort
Fonctionne comme le bubble mais au lieu d'effectuer une réitération après contrôle,
on ajout une boucle while qui vient directement placer l'élément à sa place selon l'état

# Fonctions String
#include <string>

initialisation d'un string
```C++
string hello ("Hello, World!"); // contient "Hello, World!"
string world (hello, 7 ); // contient "World!"
string hello2 ("Hello, World!", 7 ); // contient "Hello, "
string world2( string("Hello, World!"), 7 ); // contient "World!"
```

int tolower(int c);
int toupper(int c);
retourne minuscule ou majuscule
si la transformation n'est pas possible retournent le caractère original inchanché

un string peur remplacer un vector<char>
mais un vector<char> n'a pas autant de fonctionnalité qu'un string

```C++
string s1 = "Hello";
string s2(s1); // = "Hello"
string s3("Hello");
string s4{"Hello"};

// Autres constructeurs
string s1 = "Bienvenue";
string s2(s1.begin()+4, s1.begin()+8); // "venu"
string s(6, ' a'); // "aaaaaa"

// pas de valeur par default contrairement à vector
string s(6); // erreur de syntaxe

// Encore un exemple:
string hello("Hello, World!"); // contient "Hello, World!"
string hell  (hello, 0, 4);   // contient la chaîne "Hell" string world (hello, 7, 5);   // 
contient la chaîne "World" string world2(hello, 7);     // contient la chaîne "World!"
string hello2(hello);      // contient la chaîne "Hello, World!"

```

Il y'a des fonctions qui peuvent être utilisé pour travailler sur les strings

```C++
    string s1 = "ABC";
    string s2 = s1[1]; // ERROR, le constructeur string ne peut pas gérer ça
    // il faut le faire comme ça :
    string s2;
    s2 = s1[1]; // ici c'est good car le string a été déclaré avant
    
    // et on ne peut pas faire ça
    string s1 = 'B'; // ERROR car c'est un char
```

## replace(pos, len, str)
```C++
cout <<"my_string before replace() -> " << my_string << endl;

my_string.replace(1, 8, one_string);

cout << my_string << endl;
// là = HPancakeso World! 
// car va ajouter au index 1 Pancakes et va ensuite va remplacer/écraser les 3 lettres après index 1
```

## clear()
Vide la chaîne 

## erase(pos, len)
Va supprimer des éléments selon une position donnée 
```C++
string str("This is an example sentence.");
str.erase(9, 9);  // "This is a sentence." -> supprime 9 élément à partir de l'index 9
str.erase(13);   // "This is a sen" -> supprime tout ce qu'il y'a à partir de l'index 13 jusqu'à la fin
str.erase();    // "" -> revient à faire un clear()

```

## Recherche
- find -> Trouve un sous-chaîne
- rfind -> Idem depuis la fin
- find_first_of(strings à chercher, à partir de l'index dans le string à chercher) -> Trouve le premier caractère parmi une liste
- find_last_of -> Idem depuis la fin
- find_first_not_of -> Trouve le premier caractère hors d'une liste
- find_last_not_of -> idem depuis la fin

Ses méthodes renvoient la position trouvée de type **size_t**
Si la recherche ne trouve rien elles renvoient **-1** en tant que size_t qui est unsigned donc va renvoyer le numeric_limits<size_t>::max
```C++
 
find_first_of("Good Bye!", 0 , 4); // Ici va chercher selon 'Good'
```

# Entrée sortie utilisateur
cin permet de rentrer in string
cout d'afficher
cerr afficher les erreur
clog afficher les logs

getline(flux, str) pour prendre en input une ligne entière, en gros un cin avec les espaces compris

il est possible de convertir des string à des nombres
- stoi() -> string to integer
- stol -> string to long
- stoul -> string to unsigned long
- stoll -> string to long long
- stoull -> string to unsigned long long

Et inversement de nombre à string avec *to_string()*

# Classes et objets

En C++ lorsque l'on déclare une classe ne pas oublier le *;* après le close tag *}*

Pour créer une classe, il faut créer un fichier nom_classe.h
```C++
#ifndef INC_7_4_ROBOT_ROBOT_H
#define INC_7_4_ROBOT_ROBOT_H


class Robot {

};


#endif 
```

Un fichier nom_classe.cpp
```C++
#include "Robot.h"

```

le mot clé *this* permet de faire référence aux éléments de la classe en question
Il faut l'utiliser seulement lorsqu'il permet d'éviter des confusions

une méthode en const ex *double surface() const* indique par son *const* qu'aucune 
donnée de la classe sera modifiée par cette même méthode

``````


# Bad practices but fun to know 
int i = o
int ii = (5, 0)

i -> 0
le 5 sera évalué mais pas attribué

int valeur = (cin << i, i++, i, 9)
et bien valeur est toujours = 9


a = 5, 3
a = 5

car la différence c'est que c++ le comprend comme ça
(a = 5), 3
donc a = 5

alors que a = (5, 3)
a = 3

# Tableaux 
En gros c'est des tableaux array mais sans fonction native, 
ce sont des tableaux comme en C

un tableau en paramètre est nativement passé en référence

# Vectors
Il faut faire un include pour utiliser les vectors
#include <vector>
https://dev-notes.eu/2018/02/introduction-to-vectors-in-c++/


rbegin() rend() = reversebegin reverseend
cbegin() cend() = constbegin constend

le .end() sort du scope du vector, il prend la taille de vecteur + 1, 
donc pour atteindre la dernière valeur du vecteur il faut faire .end() - 1

push_back() -> place un élément à la fin du vecteur
pop_back -> retire un élément à la fin du vecteur
Structure LIFO last in first out (donc pas FIFO first in first out)

erase(parm1, parm2) supprime les positions >= param 1 et  position < param2, mais pas param2 compris
vector.insert(position, nombre de fois, élément) ou vector.insert(position, élément)

On peut créer des vecteurs de plusieurs dimensions
avec des vecteurs dans des vecteurs.

vector<vector<int>> V2D(3, vector<int>(4));

On peut accéder à la size d'un vecteur avec vector_name.size();
la size est le nomre d'éléments (lignes) dans la liste
vector<vector<int>> v2D(4, vector<int>(2,5));
v2D.size() // sera égal à 4
et l'output 
55
55
55
55

# Array
le type Array est un tableau qui se différencie du tableau classic en C 
car un array a des fonctions natives

On passe le type et ensuite le nombre d'éléments
array<array<int, 3>, 2> arrInt2D = {
arrInt2D fait 2 lignes et 3 colonnes

# Using
Keyword qui permet de créer un alias 
using Pomme = int;
Pomme test = 1; // Pomme alias à int

# Type auto
python like
auto blabla:

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


# Révisions
Revoir les cas où c = 0, c-1 = 255 car unsigned char 0 - 1 = 255
Un char/short est TOUJOURS converti en int implicitement si il travail pas 
avec des char/short
si un char travail avec un short, les deux sont converti implicitement en int

Éviter les mêmes noms de variables
```C++
int main() {
    
    a = 0
    {   
        a=0
        {
            a = 0
        }
    } ... etc pas bien

}
```
