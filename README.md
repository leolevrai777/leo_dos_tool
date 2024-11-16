tool de DOS :

Pour Linux (Debian, Ubuntu, etc.)

    Mettez à jour votre système :

sudo apt update -y && sudo apt upgrade -y

Installez les outils requis :

sudo apt install git python3 python3-pip tor curl -y

Configurez Tor (facultatif pour anonymisation) :

    Lancez et activez le service Tor :

sudo systemctl start tor
sudo systemctl enable tor

Vérifiez que Tor fonctionne correctement :

        sudo systemctl status tor

Pour Windows

    Téléchargez et installez Python 3 :
        Téléchargez Python ici.
        Lors de l'installation, cochez "Add Python to PATH".

    Téléchargez et installez Git :
        Téléchargez Git ici.

    Téléchargez et installez Tor (facultatif) :
        Téléchargez Tor ici.

    Vérifiez que Python et Git sont correctement installés :
        Ouvrez une invite de commande et exécutez :

        python --version
        git --version

Installation du projet
Étape 1 : Cloner le dépôt GitHub

    Ouvrez un terminal (ou une invite de commande sous Windows).
    Clonez le dépôt :

    git clone https://github.com/ton_utilisateur/leo_dos_tool.git

Étape 2 : Accédez au dossier du projet

    Accédez au répertoire du projet :

    cd leo_dos_tool

Étape 3 : Installer les dépendances

    Installez les dépendances Python listées dans requirements.txt :

    pip install -r requirements.txt

Étape 4 : Préparation pour Tor (facultatif)

    Si vous souhaitez utiliser Tor pour anonymiser les requêtes HTTP/HTTPS, assurez-vous que Tor est actif.
    Sous Linux, lancez Tor :

    sudo systemctl start tor

    Sous Windows, ouvrez le navigateur Tor pour démarrer le service.

Utilisation

    Rendez le script exécutable (Linux uniquement) :

chmod +x leo_dos.py

Lancez le script :

    Sous Linux :

python3 leo_dos.py

Sous Windows :

        python leo_dos.py

Options du menu

    Test UDP :
        Permet d'envoyer des paquets UDP à une adresse IP cible.
        Le script ajuste automatiquement le nombre de threads en fonction de la cible.

    Test HTTP/HTTPS :
        Permet d'envoyer des requêtes HTTP/HTTPS massives à une URL cible.
        Peut utiliser des proxys ou Tor pour anonymiser les requêtes.

    Quitter :
        Quitte le programme.
