# Programmation système - C

##  Sommaire
* Installation
* Compilation
* Commandes utiles
* Cours
* Sources

## Installation
1. gcc `sudo apt-get install gcc`
2. make `sudo apt-get install make`
3. gdb `sudo apt-get install gdb`
4. valgrind `sudo apt-get install valgrind`
5. ar, nm, objdump, readelf `sudo apt-get install binutils`
6. libc `sudo apt-get install libc-dev-bin`

## Compilation
```
$ gcc hello_world.c -o hello_world -Wall -Werror
$ ./hello_world
Hello World!
```

## Commandes utiles

**GDB**

*Charger*  :  `gdb prog` ou `gdb --args prog arg1 arg2 ...` ou `gdb prog core-file`

*Quitter*  :  `q` ou `quit`

----

**Executer**

*Lancer*  :  `r` ou `run' ou 'r arg1 arg2 ...`

*Selectionner args pour prochain run*  :  `set arg1 arg2 ...`

----

**Etat d'un processus**

*Valeur var puis valeur hexa var*  :  `p var` ou `print var`et `p/x var`

*Afficher valeur var après chaque arrêt du prog*  :  `display var`

*Afficher pile d'appel*  :  `bt` ou `back-trace`

*Afficher stack frame courante*  :  `frame`

*Select stack frame*  :  `frame nom`

*Afficher code autour stack frame select*  :  `l` ou `list`

----

**Execution processus**

*Poser breakpoint à position (nom fonction, num ligne, nom_fichier:num_ligne)*  :  `b
position` ou `break position`

*Suppr breakpoint*  :  `clear pos` ou `d num` ou `delete num`

*Etat var*  :  `w var` ou `watch var`

*Avancer d'un pas*  :  `n` ou `next`

*'...' si c'est une fonction ne descend pas dedans*  :  `s` ou `step`

*Executer jusqu'au prochain breakpoint*  :  `c` ou `continue`

----

**Assembleur**

*Afficher code assembleur*  :  `disassemble [function]`

*Afficher valeur registres*  :  `info registers`

*Afficher valeur d'un registre*  :  `p $[register]`

----

**Reverse debugging**

*Début enregistrement comportement du processus*  :  `record`

*Arrete*  :  `record stop `

*Equiv step next continue en arrière*  :  `rs` ou `rn` ou `rc` ou `reverse-step` ou ...

*Utilisation watchpoint*  :  `set can-use-hw-watchpoints 0`

----

**Autres**

*Arret processus à position si condition*  :  `break [pos] if [cond]`

*Remonter ou descendre d'un stackframe dans pile*  :  `up` ou `down`

*Attache GDB au processus de pid et detache*  :  `attach [pid]` ou `detach`

*Affecter value à var*  :  `set env [var]=[value]`


## Cours

Le C est un langage bas niveau (= peu d'abstraction par rapport processeur).

Structure d'un programme:
```
# include < stdio .h >
# include < stdlib .h >



struct nom_de_la_structure {      //sous-types hétérogènes
type1 nom_du_champs1;
type2 nom_du_champs2;
...
};
struct nom_de_la_structure z1, z2, z3;    //z1.nom_du_champs1 pour accéder à ça valeur et nom_du_champs1.z pour accéder à son parent
struct nom_de_la_structure i = { 0, 1 };  //initialisation


//Tableau attention pas accès taille, erreur silencieuse si dépassement taille
//Seul passage par rRéférences
type_des_elements nom_de_la_variable[taille_du_tableau];  //accès el 3 avec x[3]
type_element nom_variable[taille] = { e0, e1, e2, ... };



int main ( int argc , char ** argv ) {
      int entier;
      unsigned int ent;
      short short;
      long long;
      float flottant;   //4octets
      double double;    //8octets
      char chaine;
      char yes[] = "yes";     //char yes[] = { ’y’, ’e’, ’s’, ’\0’ };
      int nb_octet = sizeof(entier);
      
      for(i=0; i<n; i++) { ... }
      while(cond) {...}
      do { ...; } while(cond);
      if (cond) { ... } else { ... }
      
      printf (" Hello World !\ n " );
      printf(”%d exemple de %f format \n”, v1, v2);
      scanf(”exemple de %d format %f”, &v1, &v2);
      
      return EXIT_SUCCESS ;
}
```

## Source

Programmation système en 2A à TSP.

[DocGDB](https://sourceware.org/gdb/current/onlinedocs/gdb/)

[DocGDB Ncurses](https://sourceware.org/gdb/onlinedocs/gdb/TUI-Keys.html)
