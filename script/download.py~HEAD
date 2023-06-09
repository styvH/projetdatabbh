import requests
from bs4 import BeautifulSoup
import os

# URL du site contenant les fichiers CSV
base_url = "https://files.data.gouv.fr/lcsqa/concentrations-de-polluants-atmospheriques-reglementes/temps-reel/2023"

# Répertoire de destination pour enregistrer les fichiers CSV
destination_folder = "./data-pre-traitement/2023"
 
# Créer le répertoire de destination s'il n'existe pas
if not os.path.exists(destination_folder):
    os.makedirs(destination_folder)

# Envoyer une requête GET à l'URL de base
response = requests.get(base_url)

# Vérifier si la requête a réussi
if response.status_code == 200:
    # Analyser le contenu HTML de la page
    soup = BeautifulSoup(response.content, "html.parser")

    # Rechercher tous les liens avec l'extension .csv
    links = soup.find_all("a", href=lambda href: href and href.endswith(".csv"))

    # Parcourir tous les liens et télécharger les fichiers CSV
    for link in links:
        file_url = base_url + link["href"]
        file_name = link["href"].split("/")[-1]
        file_path = os.path.join(destination_folder, file_name)

        print("Téléchargement du fichier :", file_name)

        # Envoyer une requête GET pour télécharger le fichier CSV
        file_response = requests.get(file_url)

        # Enregistrer le fichier sur le disque
        with open(file_path, "wb") as file:
            file.write(file_response.content)

        print("Fichier téléchargé :", file_name)
else:
    print("La requête a échoué avec le code d'état :", response.status_code)
