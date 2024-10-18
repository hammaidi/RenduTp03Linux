# RenduTp03Linux

Hammaidi Karim

Exercice : parametres::Ecrivez un script analyse.sh qui affiche :Bonjour, vous avez rentre nombre de parametres parametres. Le nom du script est nom du script Le 3eme parametre 


Étape 1 pour exécuter le script :

-Créer le fichier du script avec la comande::nano analyse.sh


on utilise 'printf' a la place de echo

` "Bonjour, vous avez rentré $# paramètres."
printf "Le nom du script est $0"

if [ $# -ge 3 ]; then                            
    printf "Le 3ème paramètre est $3"
else
    printf "Il n'y a pas de 3ème paramètre"
fi
printf "Voici la liste des paramètres : $@" `





puis pour sauvegarder le fichier avec le scrypte et quitter nano:: CTRL + X, puis Y pour sauvegarder, et Entrée pour confirmer

pour tester le scrypt:: ./analyse.sh

pb rencontrée: la permission n'est pas accorde


