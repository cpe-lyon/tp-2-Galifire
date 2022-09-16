*Raphaël DUMAS - 3ICS*

# TP 2 - Bash

## 1 - Variables d'environnement

1. Le bash trouve les commandes entrées par l'utilisateur dans les dossiers "/usr/bin", "/usr/local/bin" et "/bin".

2. La variable d'environnement permettant à la commande "cd" de nous ramener dans notre répertoire personnel lorsqu'aucun argument n'est ajouté est la variable "$HOME".

3. La variable $LANG permet de définir la langue du système. La variable $PWD indique le chemin du dossier courant, et $OLDPWD celui du dossier précédent. La variable $SHELL indique le chemin ou se base l'invite de commandes.

4. Pour créer une variable locale, on entre `MY_VAR="" ; printenv MY_VAR` puis `echo $MY_VAR`.

5. La variable étant locale, il ne se passe rien lorsqu'on exécute `bash`, car la variable locale n'existe pas sur cette session.

6. Cette fois, la variable est détectée puisqu'elle est devenue une variable d'environnement.

7. Pour créer cette variable, on entre la commande `export NOM="Raphaël DUMAS" ; printenv NOM`.

8. Pour afficher un message contenant une variable, la commande à entrer est `echo "Bonjour à vous $NOM"`.

9. Si l'on affecte une valeur vide à une variable d'environnement, celle-ci existe quand même. Si on utilise la commande `unset`, cela transforme la variable en variable locale uniquement.

10. Pour afficher la phrase "$HOME = *chemin*", il faut entrer la commande `echo "\$HOME = $HOME"`.

# PROGRAMMATION Bash

## 2 - Contrôle de mot de passe
```bash
#!/bin/bash

PASSWORD="123+aze"

read -s -p "Mot de passe : " pwd

if [ "$pwd" = "$PASSWORD" ] ; then #On vérifie si le mot de passe entré correspond à la variable définie
    echo "Mot de passe correct"
else
    echo "Mot de passe incorrect"
fi
```
## 3 - Expressions rationnelles

```bash
#!/bin/bash

function is_number() {
    re='^[+-]?[0-9]+([.][0-9]+)?$'
    if ! [[ $1 =~ $re ]] ; then #On vérifie si le paramètre passé est un nombre réel en le comparant au regedit
        return 1
    else
        return 0
    fi
}

is_number $1
if [ $? -eq 0 ] ; then #On a appellé la fonction et on vérifie la valeur selon le code d'erreur retourné par la fonction.
    echo "Réel"
else
    echo "Pas réel"
fi
```

## 4 - Contrôle d'utilisateur

```bash
#!/bin/bash

if [ $# -eq 0 ]
then
    echo "Utilisation : $0 nom_utilisateur"
else 
    if [ -z $(getent passwd$1) ]
    then
        echo "L'utilisateur $1 n'existe pas"
    else
        echo "L'utilisateur $1 existe"
    fi
fi
```

## 5 - Factorielle

```bash
#!/bin/bash

function fact()
{
    FACT=1
    for (( i=1; i<$1+1; i++ )) ; do #On réalise une boucle de 1 qui s'incrémente à chaque tour jusqu'à atteindre le nombre passé en paramètre
        FACT=$(( FACT * i ))
    done
echo "$FACT"
}

fact
```

## 6 - Le juste prix

```bash
#!/bin/bash

prix=$(((RANDOM % 1000 + 1))
echo 'Entrez un nombre'
read reponse

while [ $reponse -ne $prix ] #On fait tourner cette boucle tant que le nombre entré n'est pas égal à la valeur choisie aléatoirement dans les premières lignes du script
do
    if [ $reponse -lt $prix ]; then #On vérifie en fonction de l'entrée si le nombre est supérieur ou inférieur, pour indiquer le joueur.
        echo "C'est plus !"
    else
        echo "C'est plus !"
    fi
    read reponse
done

echo 'Gagné !'
```

## 7 - statistiques
```bash
#!/bin/bash


function is_number() {
    re='^[+-]?[0-9]+([.][0-9]+)?$'
    if ! [[ $1 =~ $re ]] && [ $1 -ge -100 ] && [ $1 -le 100] ; then  #On vérifie si le paramètre passé est un nombre réel, compris en -100 et 100
        return 1
        fi
    else
        return 0
    fi
}

function stats() {

    tab=()
    for (( i=1; i<$1+1; i++ )) ; do
        read -p "Entrez un nombre en -100 et 100 : " nb
        is_number $nb
        if [[ "$?" -eq 0 ]] ; then
            tab+=("$nb")
        else
            echo "Valeur incorrecte"
        fi
    done

    max=${tab[0]}
    min=${tab[0]}
    moy=0
    somme=0

    for number in "${tab[@]}" ; do
        if [[ $number -ge $max ]] ; then
            max=$number
        fi
        if [[ $number -le $min ]] ; then
            min=$number
        fi
        $somme=$(($somme+$number))
    done
    tablength=${#tab[@]}
    $moy=$(($somme/$tablength))

    echo -e "Nombre maximal : $max\nNombre minimal : $min\nMoyenne du tableau : $moy"

}

stats $1
```