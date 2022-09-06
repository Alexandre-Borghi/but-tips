# R3.05 - TP 1

## Pré-requis

Pour ce TP (et très certainement pour les prochains), un environnement Linux semble indispensable. Je conseille :

- Utiliser Linux tout le temps parce que wINdoWs c tRo nuL (le plus simple pour commencer étant Ubuntu ou un dérivé comme Linux Mint, qui est vraiment sympa)
- Ou [faire un dual boot Linux/Windows](https://www.astuces-aide-informatique.info/9490/dual-boot-windows-10-ubuntu-linux)
- Ou [installer WSL](https://docs.microsoft.com/fr-fr/windows/wsl/install) si vous voulez garder seulement Windows, ça a l'air largement suffisant pour le contenu de ce cours. 

_Mais bon ça tout le monde le savait déjà._

## Question 1-6

Chercher sur Internet (perso j'ai jamais trouvé 3 possibilités pour les questions qui les demande, mais bon j'ai sûrement mal cherché `¯\_(ツ)_/¯`)

## Question 7-10

C'est pour celles-là que j'ai surtout écrit ça, parce que c'est clairement pas expliqué.

En fait Merciol a créé des programmes en C qui manipulent eux-mêmes les fameuses ___sémaphores___. Les sémaphores sont gérées par le noyau Linux lui-même. Il faut donc :

  1. Récupérer tous les fichiers sur [r305.merciol.fr](http://r305.merciol.fr), dans le dossier `R305-TP1-Etudiants > semaphore`.
  
     Parmi ceux-ci il y a deux types de fichiers :
     
     1. Les fichiers `.c`, qui sont les fichiers contenant le code des programmes que Merciol à écrit. Ceux-ci seront compilés en programmes exécutables par `compile.sh`. Pour compiler ces fichiers, `compile.sh` utilise `gcc`. C'est un compilateur C disponible (_quasiment_) uniquement sur Linux.
     
        Vous devrez donc avoir `gcc` d'installé sur votre machine. Pour vérifier si `gcc` est installé, faites :
     
        ```bash
        gcc --version
        ```
     
        S'il y a une erreur, il faut installer gcc. Sur une distribution utilisant APT (Debian, Ubuntu, Mint...) :
     
        ```bash
        sudo apt install gcc
        ```
     
     2. Les fichiers `compile.sh` et `wipe.sh` : ce sont des scripts en bash, `compile` va... compiler et `wipe` va effacer tous les fichiers créés par la compilation pour pouvoir retrouver un répertoire propre en cas de problème.
        
        Pour exécuter ces fichiers, placez-vous dans le répertoire ou ils se trouvent à coups de `cd` et faites :
        
        ```bash
        bash compile.sh
        ```
        
        Pour compiler (cela créé les exécutables), ou :
        
        ```bash
        bash wipe.sh
        ```
        
        Pour nettoyer le dossier.

  2. Compiler les programmes en exécutant `compile.sh` comme montré au-dessus. Cela va créer 4 programmes, un par fichier. Il y a :
  
     1. `mkNamedSem` (= "Make named semaphore" = "Créer une sémaphore avec un nom") : Ce programme demande à Linux de créer une sémaphore avec un nom donné en paramètre. Une fois la sémaphore créée, elle sera utilisable par n'importe quel programme sur la machine, dont les autres programmes fournis par Merciol.
        
        La commande s'utilise ainsi (ne pas mettre les `<` et `>`) :
        
        ```bash
        ./mkNamedSem <nom de la sémaphore> <valeur initiale de la sémaphore>
        ```
        
        Le nom est le nom que vous donnez à la sémaphore pour pouvoir la retrouver avec les autres programmes. La valeur initiale est la valeur de départ de la sémaphore, qui est un nombre entier positif (car les sémaphores ne sont en fait que des nombres entiers positifs), le plus souvent 0 (mais pas forcément).
     
     2. `namedSemP` : Exécute P() (= "puis-je" = "wait") sur une sémaphore. On utilise ainsi la commande :
     
        ```bash
        ./namedSemP <nom de la sémaphore>
        ```
     
     3. `namedSemV` : Exécute V() (= "vas-y" = "notify") sur une sémaphore. De la même manière :
     
        ```bash
        ./namedSemV <nom de la sémpahore>
        ```
     
     4. `rmNamedSem` (= "remove" = "supprime") : Supprime une sémaphore. Pareil que le reste :
     
        ```bash
        ./rmNamedSem <nom de la sémaphore>
        ```

   3. Une fois que vous avez vos programmes, vous pouvez maintenant vous en servir pour répondre à :
      
      1. La question 8 où il faut juste utiliser les programmes.
      
      2. La question 9 ou il faut créer un "caroussel", je suppose qu'il parle d'un ordonnanceur, même si là ça me paraît complexe.
      
      3. La question 10 ou il faut créer un script qui "écrit", donc V() (ou notify()) sur une sémaphore, et un script qui "lit", donc P() (ou wait()) sur la sémaphore.
      
      Les réponses à ces questions sont des scripts `bash`, tout se passe soit dans le terminal, soit dans un fichier `.sh` qui sera exécuté par bash avec `bash mon_script.sh`. Ces scripts utilisent les programmes de Merciol de la même manière que montré ci-dessus.

Voilà, n'oubliez pas d'imprimer en deux colonnes recto-verso !
