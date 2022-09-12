*Raphaël DUMAS - 3ICS*

# TP 2 - Bash

## 1 - Variables d'environnement

1. Le bash trouve les commandes entrées par l'utilisateur dans les dossiers "/usr/bin", "/usr/local/bin" et "/bin".

2. La variable d'environnement permettant à la commande "cd" de nous ramener dans notre répertoire personnel lorsqu'aucun argument n'est ajouté est la variable "$HOME".

3. La variable $LANG permet de définir la langue du système. La variable $PWD indique le chemin du dossier courant, et $OLDPWD celui du dossier précédent. La variable $SHELL indique le chemin ou se base l'invite de commandes.

4. On entre `MY_VAR="" ; printenv MY_VAR` puis `echo $MY_VAR`.

5. La variable étant locale, il ne se passe rien lorsqu'on exécute `bash`, car la variable locale n'existe pas sur cette session.

6. Cette fois, la variable est détectée puisqu'elle est devenue une variable d'environnement.

7. Pour créer cette variable, on entre la commande `export NOM="Raphaël DUMAS" ; printenv NOM`.

8. La commande à entrer est `echo "Bonjour à vous $NOM"`.

9. Si l'on affecte une valeur vide à une variable d'environnement, celle-ci existe quand même. Si on utilise la commande `unset`, cela transforme la variable en variable locale uniquement.

10. Pour afficher la phrase "$HOME = *chemin*", il faut entrer la commande `echo "\$HOME = $HOME"`.

# PROGRAMMATION Bash

## 2 - Contrôle de mot de passe
```bash
#!/bin/bash

PASSWORD="123+aze"

read -s -p "Mot de passe : " pwd

if [ "$pwd" = "$PASSWORD" ] ; then
    echo "Mot de passe correct"
else
    echo "Mot de passe incorrect"
fi
```
## 3 - Expressions rationnelles

```bash
#!/bin/bash

read -p 'Entrez un nombre :' nb

function is_number() {
    re='^[+-]?[0-9]+([.][0-9]+)?$'
    if [[ $nb =~ $re ]] ; then
        echo 'Réel'
        return 1
    else
        echo 'Irréel'
        return 0
    fi
}

is_number
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
    for (( i=1; i<n+1; i++ )) ; do
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

while [ $reponse -ne $prix ]
do
    if [ $reponse -lt $prix ]; then
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

read "Entrez un premier nombre" n1
read "Entrez un deuxième nombre" n2
read "Entrez un troisième nombre" n3

if [ n1 >= n2 ] ; then
    if [ n1 >= n3 ] ; then
        max=$n1
    fi
fi

if [ n2 >= n1 ] ; then
    if [ n2 >= n3 ] ; then
        max=$n2
    fi
fi

if [ n3 >= n2 ] ; then
    if [ n3 >= n1 ] ; then
        max=$n3
    fi
fi

if [ n1 <= n2 ] ; then
    if [ n1 <= n3 ] ; then
        min=$n1
    fi
fi

if [ n2 <= n1 ] ; then
    if [ n2 <= n3 ] ; then
        min=$n2
    fi
fi

if [ n3 <= n2 ] ; then
    if [ n3 <= n1 ] ; then
        min=$n3
    fi
fi

moy=$( ( n1 + n2 + n3 ) / 3 )

echo "Nombre minimal : $min"
echo "Nombre maximal : $max"
echo "Moyenne : $moy"