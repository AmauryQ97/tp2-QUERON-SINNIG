**Amaury QUERON et Solène SINNIG**

#TP2- Bash

## Exercice 1 - Variables d'environnement

1/ On trouves les commandes **Bash** tapées par l'utilisateur grâce à la commande *printenv PATH* :

/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/usr/local/cpe/bin:/softwares/bin:/softs/bin

2/ La commande *cd ~* permet de revenir dans le répertoire personnel.

3/**LANG** détermine la langue utilisées dans les logiciels. 
**PWD** nous renvoie le chemin du répertoire courant.
**OLDPWD** renvoie le dernier répertoire visité par l'utilisateur.
**SHELL** renvoie le chemin "préféré" du shell de l'utilisateur.
**_** contient le nom de fichier absolu du shell ou du script en cours d'exécution.

4/ On crée une variable locale: *MY_VAR="coucou"* et on vérifie son existance avec *echo $MY_VAR* qui nous renvoie son contenu.

5/ On rentre ensuite dans le mode **bash**, la variable n'existe pas car c'est une variable locale et non une variable d'environnement.

6/ On transforme MY_VAR en variable d'environnement *export MY_VAR*, elle apparaît maintenant dans le mode bash.

7/ On utilise la commande *export NOMS="Solene Amaury"*

8/ On écrit la commande *echo "Bonjour à vous deux, $NOMS"* où $NOMS est remplacé par le contenu de la variable.

9/ La valeur vide remplace la valeur actuelle de la variable, elle est donc vide mais elle existe alors qu'*unset* supprime la variable et son contneu.

10/Pour écrire la phrase $HOME = chemin on tape *echo '$HOME = '$HOME

## Exercice 2 - Contrôle de mot de passe

#!/bin/bash

PASSWORD="blop"
echo 'Mot de passe : '
read -s mdp

if [ $mdp == $PASSWORD ]
then
    echo "Mot de passe valide"
else
    echo "Mot de passe invalide"
fi

##Exercice 3 - Expressions rationnelles

#!/bin/bash

function is_number()
{
    re='^[+-]?[0-9]+([.][0-9]+)?$'
    if ! [[ $1 =~ $re ]] ; then
	echo 1
    else
	echo 0
    fi
}
is_number $1

##Exercice 4 - Ctrl d'utilisateur

#!/bin/bash

user1="sosory"

function verification(){
    if [ $1 == $user1 ]
    then
	echo "utilisateur valide"
    else
	echo "Utilisation: $0 $1"
    fi
}
verification $1

##Exercice 5 - Factorielle

#!/bin/bash

function factor() {
    n=$1
    if [ $n -eq 0 ]
    then 
	echo 1
    else 
	echo $(( n * $(factor $(( n - 1 )) ) ))
    fi
}

factor $1

##Exercice 6 - Le juste prix

#!/bin/bash

val=$RANDOM

if [ $(( val % 1000 + 1)) -lt 1000 ]
then 

    echo $val
    n=$1
    finish=0
    while [ $finish -eq 0 ]
    do
	read -p "Tapez un nombre : " n
	if [ $val -eq $n ]
	then 
	    echo "You WINNNNN!"
	    finish=1
	elif [ $val -gt $n ]
	then
	    echo "C'est plus!"
	    echo "Essayez encore:"
	    read n
	else
	    echo "C'est moins!"
	    echo "Essayez encore:"
	    read n
	fi
    done
else 
    echo 'mauvais random'
fi






















