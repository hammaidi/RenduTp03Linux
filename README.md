# RenduTp03Linux

Hammaidi Karim

EXERCICE 1: parametres::Ecrivez un script analyse.sh qui affiche :Bonjour, vous avez rentre nombre de parametres parametres. Le nom du script est nom du script Le 3eme parametre 


Étape 1 pour exécuter le script :

-Créer le fichier du script avec la comande::nano


` "Bonjour, vous avez rentré $# paramètres."
printf "Le nom du script est $0"

if [ $# -ge 3 ]; then                            
    printf "Le 3ème paramètre est $3"
else
    printf "Il n'y a pas de 3ème paramètre"
fi
printf "Voici la liste des paramètres : $@" `


puis pour sauvegarder le fichier avec le scrypte et quitter nano:: CTRL + X, puis Y pour sauvegarder, et Entrée pour confirmer

j'ai appelé le scrypte "analyse.sh"
pour tester le scrypt:: ./analyse.sh

pb rencontrée: la permission n'est pas accorde

//ls -l:: permet de voir les droits accordés    -> dans mon cas les droits ne sont pas accordés

solution ::chmod +x analyse.sh   -> a présent j'ai les droits et je peux tester mes scripts

résultat de la commande:: ./analyse.sh   :: "il y a moins de 3 parametres"


EXERCICE 2: verification du nombre de parametres

nous créons un nouveau script appellé "concat.sh"


`if [ $# -ne 2 ]; then
    echo "Erreur : Vous devez entrer exactement 2 paramètres."
    exit 1  # Quitter avec un code d'erreur
else

    CONCAT="$1$2"
    echo "La concaténation des deux mots est : $CONCAT"
fi `










EXERCICE 3   Afficher le contenu d’un repertoire


`
if [ $# -ne 1 ]; then
    echo "Erreur : Vous devez passer un fichier en paramètre."
    exit 1
fi

FICHIER=$1

if [ ! -e "$FICHIER" ]; then
    echo "Le fichier $FICHIER n'existe pas."
    exit 1
fi

if [ -d "$FICHIER" ]; then
    echo "Le fichier $FICHIER est un répertoire."
elif [ -f "$FICHIER" ]; then
    # Vérifier si le fichier est un fichier ordinaire
    echo "Le fichier $FICHIER est un fichier ordinaire."
else
    echo "Le fichier $FICHIER est d'un autre type."
fi

USER=$(whoami)

if [ -r "$FICHIER" ]; then
    LECTURE="lecture"
else
    LECTURE="pas de lecture"
fi

if [ -w "$FICHIER" ]; then
    ECRITURE="écriture"
else`   







EXERCICE 4: Afficher le contenu d’un repertoire


objectif:  afficher séparément les fichiers et les répertoires d'un répertoire donné en paramètre.


`if [ $# -ne 1 ]; then
    echo "Erreur : Vous devez spécifier un répertoire."
    exit 1
fi

REP=$1

if [ ! -d "$REP" ]; then
    echo "Erreur : $REP n'est pas valide."
    exit 1
fi


echo "####### fichiers dans $REP/"
for fichier in "$REP"/*; do
    if [ -f "$fichier" ]; then
        echo "$fichier"
    fi


echo "####### répertoires dans $REP/"
for dossier in "$REP"/*; do
    if [ -d "$dossier" ]; then
        echo "$dossier"
    fi `


-On peut executer le script avec le répertoire de son choix
exemple concret :./listedir.sh /boot




EXERCICE : Lister les utilisateurs
objectif: afficher les utilisateurs ayant un UID supérieur à 100.


`awk -F: '$3 > 100 {print $1}' /etc/passwd`




Exercice : Mon utilisateur existe-t-il
Objectif: vérifier si un utilisateur existe en fonction de son login ou de son UID.



`if [ $# -ne 2 ]; then
    echo "Usage: $0 [login|uid] [valeur]"
    exit 1
fi

TYPE=$1
VALEUR=$2

# Vérifier par login
if [ "$TYPE" == "login" ]; then
    UID=$(grep "^$VALEUR:" /etc/passwd | cut -d: -f3)
    if [ -n "$UID" ]; then
        echo "L'utilisateur $VALEUR a pour UID: $UID"
    else
        echo "Utilisateur $VALEUR non trouvé."
    fi

elif [ "$TYPE" == "uid" ]; then
    LOGIN=$(awk -F: -v uid="$VALEUR" '$3 == uid {print $1}' /etc/passwd)
    if [ -n "$LOGIN" ]; alors
        echo "L'UID $VALEUR correspond à l'utilisateur: $LOGIN"
    else
        echo "Aucun utilisateur avec l'UID $VALEUR n'a été trouvé."
    fi
else
    echo "Le premier paramètre doit être 'login' ou 'uid'."
    exit 1
fi`




EXERCICE : Création d’utilisateur

Objectif: créer un utilisateur en recueillant des informations comme son nom, prénom, UID, etc.



`read -p "Nom: " nom
read -p "Prénom: " prenom
read -p "UID: " uid
read -p "GID: " gid
read -p "Commentaires: " commentaires


echo "$nom:x:$uid:$gid:$commentaires:/home/$nom:/bin/bash" >> /etc/passwd_simulé

echo "Utilisateur $nom ajouté avec succès !" `


EXERICE : Lecture au clavier


echo -n "Entrez votre nom: "
read nom
echo "Votre nom est $nom"
Explication : Ce script demande à l'utilisateur de saisir son nom, puis affiche ce nom.

EXERCICE : Appréciation
Objectif:demander à l'utilisateur de saisir une note et affiche une appréciation en fonction de la note.


#tant que cest vrai alors::

`while true; do
    read -p "Entrez une note entre 0 et 20: " note

    if [ "$note" -ge 0 ] && [ "$note" -le 20 ]; then
        if [ "$note" -lt 10 ]; then
            echo "Insuffisant"
        elif [ "$note" -ge 10 ] && [ "$note" -lt 14 ]; then
            echo "Moyen"
        elif [ "$note" -ge 14 ] && [ "$note" -lt 16 ]; then
            echo "Bien"
        elif [ "$note" -ge 16 ] && [ "$note" -lt 20 ]; then
            echo "Très bien"
        else
            echo "Excellent"
        fi
    else
        echo "Note invalide."
    fi `








