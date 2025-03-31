# SCRIPT-CREATION-GROUPE
SCRIPT CREATION GROUPE

# SCRIPT CREATION GROUPE

---

## CONSIGNE

Écrire un script chargé de créer des groupes en prenant comme arguments au lancement du script les noms de groupes à créer.

- Si aucun argument n'est entré au lancement du script, alors un message invite à relancer le script en donnant des noms de groupes.
- Pour chaque argument, le script doit vérifier si le groupe existe déjà ; auquel cas un message indique l'existence de ce groupe.
- Pour chaque groupe créé, un message doit indiquer si la création a abouti ou non.

---

## CREATION DU SCRIPT

1. **Création et permission du fichier :**
   ```bash
 touch createGroup.sh                          # Création du fichier
   chmod +x createGroup.sh                       # Droits d'exécution au fichier
   export PATH=$PATH:/createGroup.sh             # Permet d'exécuter le script avec PATH
   sudo nano createGroup.sh                      # Édition du script

2 Contenu du script :

#!/bin/bash

# Vérification de la présence d'arguments
if [ $# -eq 0 ]; then
    echo "Relancez le script en rajoutant des arguments."
    exit 1
fi

# Boucle pour vérifier les noms des groupes (arguments)
for group in "$@"; do
    if cat /etc/group | grep -q "$group"; then
        echo "Le groupe $group existe déjà."
    else
        # Création du nouveau groupe
        groupadd "$group"

  # Vérification de la création
  if [ $? -eq 0 ]; then
            echo "La création de $group a réussi."
        else
            echo "La création de $group n'a pas réussi."
        fi
    fi
done

NOTES ET AIDES
$# : Permet de vérifier si des arguments sont passés (exemple : echo $#).

Pour lister les groupes et les utilisateurs :

Groupes : /etc/group (commande cat).

Utilisateurs : /etc/passwd.

Commande groups : Liste les utilisateurs.

Option -q pour la commande grep : Mode silencieux.

Rediriger la sortie de grep vers un fichier sans afficher :

&> /dev/null : Envoie la sortie dans un "Black Hole".

&> : Indique la sortie 1 et 2.

Commandes utiles :
groupadd : Ajoute un groupe (avec répertoire).

useradd : Ajoute un utilisateur (avec répertoire).

adduser : Ajoute un utilisateur (sans répertoire, pour système).

$? : Vérifie si la dernière commande a fonctionné (retourne 0 si OK).
