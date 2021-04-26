# Programmation système - C

##  Sommaire
* Installation
* Compilation
* Commandes utiles
* Cours
  * Système d'exploitation
  * Structure
  * Pointeur
  * Bibliothèque
  * Makefile
  * Fichiers
  * Processus
  * Signal
  * String
  * Autre
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

Phase 1 : **Préprocesseur** prépare code source (inclue fichiers, interprète #). `gcc -E mem_alloc.c`

Phase 2 : **Compilateur**  C->binaire dependante processeur (.c -> .o).  `gcc -c mem_alloc.c`

Phase 3 : **Editeur de liens** regroupe fichiers objects et crée un exécutable.  `gcc -o executable mem_alloc.o module2.o [...] moduleN.o `

*-DN=7 change valeur N DEFINE

nm nom.o permet d'afficher variable,l'état B globale non ini (b sinon), U undefined

-I../tab definir lieu fichier h   et  -ltab/-lplop -L../tab pour definir lieu bibliothèque*

## Commandes utiles

GDB permet le debugging, seul pre-requis compiler avec -g

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

> L'interface (truc.h) accessible à d'autres modules pour les prototypes, constantes et types.

> L'implémentation (truc.c) est privé pour les variables et fonctions.

> Le module truc regroupe précédent.

### Système d'exploitation

Permet cacher complexité matériel, interface virtuelle, protège droit d'accès/mémoire/.../matériel, partage ressources CPU/périphériques


Mode utilisateur: certaines instructions interdites, pas accès periphériques, accès mémoire virtuelle processus *bibliothèques (libc, etc.),shell et commandes systèmes*

Mode Kernel/Noyau: accès periph, accès mémoie physique *ordonnanceur, gestion mémoire virtuelle, système de fichiers, drivers périphériques*

Pour y accéder :

1. interruption (processeur, division 0, accès mémoire illicite, carte réseau recoit message, moteur DMA)
2. appel système (user demande OS un service)

Gestion des différents processus accède mémoire etc --> utilisation sémaphore (=jetons)

1. P (puis-je prendre un jeton / l'attendre)
2. V (vas-y ajouter un jeton et débloquer processus)

Création  :  `sem_open(”/CLE”, O_CREAT, S_IRWXU, nb_jetons);      //return sem_t* et CLE chaine débute par /`

Ouverture  :  `sem_open(”/CLE”, 0);       //return sem_t`

Destruction  :  `sem_unlink(sem_t* sem)`

Opération P  :  `sem_wait(sem_t* sem)`

Opération V  :  `sem_post(sem_t* sem)`


### Structure d'un programme:
```
# include < stdio .h >        //biliothèque
# include < stdlib .h >

#ifndef N
#define N 13
#endif


static int var = 0;     //statique = globale ds fichier
int var;                //globale
extern int var;         //externe (globale ailleurs)

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
      int entier;             //locale
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
      printf("adresse de var: %p\n", &var);                 //adresse var
      scanf(”exemple de %d format %f”, &v1, &v2);
      sprintf(s,message,arg);
      
      return EXIT_SUCCESS ;
}
```

### Pointeur

**Espace mémoire processus**

1. pile (stack) --> var locale + para fonction
2. tas (heap)   --> var globale
3. segment code --> code binaire du programme

**Adresse**

1octet d'espace mémoire = 1 adresse

Adresse mémoire totale = 2^k octets accessible (k=64)

Adresse d'une var = `&var` (type p pointer) donne l'emplacement

Modifer emplacement mémoire var --> `*var='B'` donc var pointera sur B

Acceder valeur stocké à son adresse --> `*var`

char a = crée var a type char

char* a = crée pointeur sur donnée type var


### Biliothèque

Statique : créée édition lien **libmemory.a** 

```
ar rcs libmemory.a mem_alloc.o mem_plip.o mem_plop.o
```

Dynamique : créée exécution **libmemory.so** 

```
gcc -shared -o libmemory.so mem_alloc.o mem_plip.o
mem_plop.o [...]

gcc -c mem_alloc.c -fPIC      //objets
```

### Makefile

```
cible : dependance1 dependance2 ... dependanceN
<TAB>commande
```

On lance avec `make`

A adapter selon besoin:

```
# In order to reuse this Makefile
#    Modify the project name => modify the binary name
#    Add all the .o dependencies in OBJ
#    That's all folk :)

PROJECT=main

BIN=$(PROJECT)
OBJ=main.o

# compilation flags
CFLAGS=-Wall -Werror -g
# link flags
LDFLAGS=
CC=gcc

Echo=@echo [$(PROJECT)]:

ifndef VERBOSE
  Verb := @
endif

# Tells make that 'all' and 'clean' are "virtual" targets (that does not generate a file)
.PHONY: all clean

all: $(BIN)

$(BIN): $(OBJ)
	$(Echo) Linking $@
	$(Verb) $(CC) $(LDFLAGS) -o $@ $^

# generic rule: to generate foo.o, we need foo.c
%.o: %.c
	$(Echo) Compiling $<
	$(Verb) $(CC) $(CFLAGS) -c "$<" -o "$@"

# you can add specific compilation rules here


# you can invoke "make clean" to delete all the generated files
clean:
	$(Echo) Cleaning compilation files
	$(Verb) rm -f $(OBJ) $(BIN)
```

```
CC=gcc
CFLAGS=-Wall -Werror

all:main

main:main.o foo.o LIBTAB
	$(CC) -o main main.o foo.o -L../libtab -ltab

clean:
	rm -f main *.o
```

### Fichiers

Primitves d'entrées/sorties bufférisées(=E/S groupés mémoire puis exec perif) (accès contenu fichiers, améliore perf)

```
FILE*                                                             // type “opaque” désignant un fichier ouvert
FILE* fopen(char* fichier, char* mode);                           //mode (r=lecture,w=ecriture, r+ ou w+ les2, a ecriture seule (ajout), a+ les 2(ajout)
int fclose(FILE* f);                                              //termine opé et ferme
int fprintf(FILE* f, char* format, ...);                          //ecrit ds fichier une char
size_t fwrite(void* ptr, size_t size, size_t nmemb, FILE* f);     //sizexnmemb octet à l'adresse ptr ds f
int fscanf(FILE* f, char* format, ...);                           //scanf depuis fichier
size_t fread(void* ptr, size_t size, size_t nmemb, FILE* f);      //stocke nmembxxsize octet à l'adresse ptr, return nb item lu, si fin fichier atteinte fread<nmemb
char* fgets(char* s, int size, FILE* f);                           //lit max size carac stocke ds s, s'arrete avant /n ou fin fichier
```

Le curseur debute à 0 (mode a à la fin fichier), désigne lieu prochaine opé, ++

```
long ftell(FILE *stream);                                         //position actu, nb octets depuis début du fichier
int fseek(FILE *f, long offset, int whence);                      //déplace curseur de offset octets depuis whence (début si=SEEK_SET, position actu=SEEK_CUR, fin=SEEK_END)
```

### Processus

PID courant  :  `pid_t getpid();`

PID père  :  `pid_t getppid();`

Création processus shell exe cmd et retourne 0 si ok  :  `int system(const char* cmd);`

Dupliquer courant  :  `pid_t fork();` Créé est le fils, copie sauf PID et PPID, fork retourne PID fils au père et 0 au fils.

Executer une commande  :  `execlp, execvp, execve, execle, execlp, etc.` (famille exec)

Terminaison processus fils :  `pid_t wait(int *status);`  //status=cause décès ou `pid_t waitpid(pid_t pid, int *wstatus, int options);`


### Signal

1. Com inter-processus
2. 1<=entier<=31
3. Recep aléatoire
4. Routine de reception auto

Envoyer sig à pid  :   `int kill(pid_t pid, int sig); `

Attender  :  `int pause( );`

Programmer alarme (envoir SIGALRM après s sec)  :  `■ int alarm(unsigned int s);`

Recevoir :   `int sigaction(int signum, const struct sigaction *act, struct sigaction *oldact); ` 

* Avec signum spécifie comportement reception
* sigaction sous forme
```
struct sigaction {
void (* sa_handler )( int );
void (* sa_sigaction )( int , siginfo_t *, void *);
sigset_t sa_mask ;
int sa_flags ;
void (* sa_restorer )( void );
};
```
* sa_handler pointeur sur fonction à appeler

## String

**strsep:  strsep - Extraction de mots d'une chaîne**

Si stringp est NULL, la fonction strsep() renvoie NULL et ne fait rien d'autre.  Dans  le
       cas  contraire,  cette  fonction recherche le premier élément lexical (token) de la chaîne
       *stringp qui est délimité par l'un des octets de la  chaîne  delim.  Le  mot  renvoyé  est
       terminé  en  écrasant  le séparateur avec un octet nul (« \0 ») et *stringp est mis à jour
       pour pointer après le mot. Dans le cas où aucun séparateur n'est trouvé, l'élément extrait
       est constitué de toute la chaîne *stringp, et *stringp vaut NULL.

**strcmp**

Trois cas distincts doivent être considérés. Soit les deux chaînes sont égales : dans ce cas, une valeur nulle sera retournée. Soit la première chaîne est plus petite que la seconde (dans l'ordre lexicographique) : dans ce cas, une valeur négative sera retournée. Soit la première chaîne est plus grande que la seconde : dans ce dernier cas, une valeur positive sera renvoyée. Dans tous les cas, la valeur absolue indiquera la position du premier caractères permettant de produire le résultat.

**strcpy**

Cette fonction permet de copier le contenu d'une chaîne de caractères dans une autre. Bien entendu, la chaîne de caractère devant recevoir le contenu de l'autre doit être allouée de manière à être suffisament grande pour contenir tout le texte.


## Autre

Lock=Semaphore

void * malloc( size_t memorySize );

Cette fonction permet d'allouer un bloc de mémoire dans le tas (le heap en anglais). Attention : la mémoire allouée dynamiquement n'est pas automatiquement relachée. Il faudra donc, après utilisation, libérer ce bloc de mémoire via un appel à la fonction free.

avoir la langue : getenv("LANG")

## Source

Programmation système en 2A à TSP.

[DocGDB](https://sourceware.org/gdb/current/onlinedocs/gdb/)

[DocGDB Ncurses](https://sourceware.org/gdb/onlinedocs/gdb/TUI-Keys.html)
