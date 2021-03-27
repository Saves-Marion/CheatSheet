# Programmation système - C

##  Sommaire
* Installation
* Commandes utiles
* Sources

## Installation
1. gcc `sudo apt-get install gcc`
2. make `sudo apt-get install make`
3. gdb `sudo apt-get install gdb`
4. valgrind `sudo apt-get install valgrind`
5. ar, nm, objdump, readelf `sudo apt-get install binutils`
6. libc `sudo apt-get install libc-dev-bin`

## Commandes utiles

**GDB**

*Charger*  :  `gdb prog` ou `gdb --args prog arg1 arg2 ...` ou `gdb prog core-file`

*Quitter*  :  `q` ou `quit`

**Executer**

*Lancer*  :  `r` ou `run' ou 'r arg1 arg2 ...`

*Selectionner args pour prochain run*  :  `set arg1 arg2 ...`

**Etat d'un processus**

*Valeur var puis valeur hexa var*  :  `p var` ou `print var`et `p/x var`

*Afficher valeur var après chaque arrêt du prog*  :  `display var`

*Afficher pile d'appel*  :  `bt` ou `back-trace`

*Afficher stack frame courante*  :  `frame`

*Select stack frame*  :  `frame nom`

*Afficher code autour stack frame select*  :  `l` ou `list`

**Execution processus**

*Poser breakpoint à position (nom fonction, num ligne, nom_fichier:num_ligne)*  :  `b
position` ou `break position`

*Suppr breakpoint*  :  `clear pos` ou `d num` ou `delete num`

*Etat var*  :  `w var` ou `watch var`

*Avancer d'un pas*  :  `n` ou `next`

*'...' si c'est une fonction ne descend pas dedans*  :  `s` ou `step`

*Executer jusqu'au prochain breakpoint*  :  `c` ou `continue`

**Assembleur**

*Afficher code assembleur*  :  `disassemble [function]`

*Afficher valeur registres*  :  `info registers`

*Afficher valeur d'un registre*  :  `p $[register]`

**Reverse debugging**

*Début enregistrement comportement du processus*  :  `record`

*Arrete*  :  `record stop `

*Equiv step next continue en arrière*  :  `rs` ou `rn` ou `rc` ou `reverse-step` ou ...

*Utilisation watchpoint*  :  `set can-use-hw-watchpoints 0`

**Autres**

*Arret processus à position si condition*  :  `break [pos] if [cond]`

*Remonter ou descendre d'un stackframe dans pile*  :  `up` ou `down`

*Attache GDB au processus de pid et detache*  :  `attach [pid]` ou `detach`

*Affecter value à var*  :  `set env [var]=[value]`

## Source

Programmation système en 2A à TSP.

[DocGDB](https://sourceware.org/gdb/current/onlinedocs/gdb/)

[DocGDB Ncurses](https://sourceware.org/gdb/onlinedocs/gdb/TUI-Keys.html)
