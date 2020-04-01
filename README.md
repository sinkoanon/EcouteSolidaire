# EcouteSolidaire

V1.0


Besoin initial : reporter automatiquement les nouvelles demandes arrivées dans l’onglet source (via le formulaire Google attaché) vers le bon onglet cible (ECOUTE, LOGISTIQUE, PARENTALITÉ ou PRATIQUES). 

# Comportement du script :
Il parcourt l'ensemble des prénoms de l'onglet Source/Formulaire,
Pour chaque "oui" détecté il va analyser l'onglet cible concerné (ECOUTE, LOGISTIQUE, PARENTALITÉ ou PRATIQUES),
Il parcourt alors dans l'onglet cible concerné les numéros de téléphone déjà existants,
S'il y détecte que le numéro est absent, il ajoute en fin de tableau une nouvelle ligne en y recopiant les données de la ligne source (date, initiales, prénom, @mail, n° tel, code postal),
Si le numéro de tel est déjà présent, 2 cas : 
Si le prénom est différent (cas très particulier de deux personnes appelant depuis le même numéro), il procède également à la recopie.
Sinon, c'est que le numéro de tel ET le prénom sont identiques, et que la personne existe donc déjà. Le script passe sans rien faire.
Les informations d’exécution sont affichées dans une fenêtre sur la droite et une synthèse est affichée en pop-up en fin d’exécution.  

# Lancement du script :
A l'ouverture du document, le choix est proposé à l'utilisateur de lancer ou non le script de mise à jour automatique.
Il peut aussi être lancée manuellement depuis le menu "Outils \ Macro \ Mise à jour automatique".
Il est nécessaire d’activer les droits sur ton compte Google pour permettre l’exécution du script.


# Note complémentaire :: 
l’onglet source est prépopulé avec des informations pour test (les lignes en orange étant les cas déjà existant/copié dans les onglets cibles, ne devant pas être recopiés par la macro).









V1.1


Nouveau besoin : il est possible qu'une même personne rappelle plusieurs fois ...
par exemple, George a un besoin d'écoute lors de son premier appel et c'est tout, puis il rappelle et indique qu'il a un nouveau besoin d'écoute et en plus de logistique
il faut que ce besoin d'être à nouveau rappelé par l'équipe relais écoute soit pris en compte
 
# Modification : 
la condition de rejet d’une copie devient donc : 
SI le numéro de tel ET le prénom ET la date sont identiques, 
ALORS c’est que la demande existe donc déjà et le script doit passer sans rien faire. 
SINON, il procède à la recopie de cette nouvelle demande.
 
# Notes : 
dans l'onglet source ont été ajoutés trois cas de tests complémentaires (en rouge) :
 > Le cas d'une nouvelle ligne avec même prénom et date => à rejeter
 > Le cas d'une nouvelle ligne avec prénom différent et même date => à reporter 
 > Le cas d'une nouvelle ligne avec même prénom et date différente => à reporter



V1.2

Nouveau besoin : dans un but de confidentialité entre les quatre pôles, il apparaît nécessaire de leur proposer à chacun un fichier séparé sur lequel pourront être contrôlés des droits d’accès différents. 

Modification : la version v1.2 opère à la fin du traitement une recopie des données de chacun des quatre onglets cibles vers un document séparé.

# Il a été ajouté quelques contraintes supplémentaires :
Le script cherche uniquement dans un seul dossier, identifié par son URL, en excluant les dossiers parents et enfants,
De plus l'onglet cible doit porter le même nom que le fichier (ECOUTE, LOGISTIQUE, PARENTALITE,  ou PRATIQUES),
Une erreur est affichée en fin de rapport si une copie n'avait pas pu avoir lieu,
Le script se limite à copier uniquement les données qu'il contrôle (zone  A2:Gn, où n est la dernière ligne non vide de l'onglet source).
 
# Notes :
En conséquence du point 4, il a été nécessaire de reporter à la main la mise en forme (en tête et couleurs) dans chacun des quatre fichiers, puis de figer+protéger les colonnes A à G de chaque fichier afin que les utilisateurs ne puissent pas les modifier.de la ligne “

En conséquence du point 1, une configuration du FOLDER_ID est nécessaire dans la macro si elle est déplacée dans un autre répertoire. Pour cela, 
Copier le document dans sa nouvelle destination
Avant de l’ouvrir, rester dans la vue du dossier et cliquer sur l’URL puis copier l’ID du dossier (partie rouge sur l’exemple suivant : https://drive.google.com/drive/folders/1kH8rUV9E7kMtwwqsyF23kZ8REEtA0JRG
Ouvrir ensuite le document et se rendre dans l’onglet d’édition depuis le menu Outil \ éditeur de script:
Dans le script, rechercher FOLDER_ID et y coller la nouvelle valeur.(vous devez coller en remplacement du précédent, 
            var FOLDER_ID = ”1kH8rUV9E7kMtwwqsyF23kZ8REEtA0JRG“;
Enregistrer, puis fermer l’onglet 
Par sécurité, fermer aussi le document et le rouvrir avant première execution de du script..




