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
## Erreurs de compilation

Erreur classique - oublier un point virgule
Erreur de synthaxe 

```C++
cout << "Hello World"" << endl
```

### Erreurs execution

Le résultat n'est pas conforme aux attentes, le programme est compilé correctement
```C++
cout << "hollo world" << endl;
```

### Génération d'exception

Erreurs qui génèrent une exception, 

```C++
cout << 1/0;

impossible de diviser par 0
```

### Erreur d'édition de liens (link error)
C++ a une seule fonction principale nommée **main**

C++ est case sensitive


# Suite cours
Présentation point 6 de 01 Introduction pdf

