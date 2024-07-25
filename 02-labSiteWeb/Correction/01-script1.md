#!/bin/bash
# Mise à jour du système
sudo yum update -y

# Affichage de la version du noyau
cat /proc/version

# Installation des paquets nécessaires
sudo yum -y install git httpd mariadb-server php-mbstring

# Configuration du serveur Apache
sudo systemctl enable httpd
sudo systemctl start httpd
sudo systemctl status httpd

# Configuration du serveur MariaDB
sudo systemctl enable mariadb
sudo systemctl start mariadb
sudo systemctl status mariadb

# Vérification des versions

sudo httpd -v
sudo mysql --version
sudo mariadb --version
sudo php --version

# Configuration des permissions et des liens symboliques
sudo ln -s /var/www/ /home/ec2-user/environment
sudo chown ec2-user:ec2-user /var/www/html
# Vérifiez le propriétaire du dossier html
ls -la /var/www/
# Exercice 01: Vérifier le propriétaire de /var
# Exercice 02: Vérifier le propriétaire de /www
# Exercice 03: à quoi sert pwd et whoami
pwd
whoami

# Création du fichier index.html initial
cd /var/www/html
echo "<html>Hello from the café web server</html>" > /var/www/html/index.html

# Pause pour vérification du site web
echo "Ajout d'une pause de 1 minute pour consulter le site web ==> Adresse IP publique"
echo "Début de la pause, testez svp"
sleep 60
echo "Pause terminée. Appuyez sur une touche pour continuer..."
read -n 1 -s -r -p " "
echo "Continuer le script"

# Nettoyage et clonage du projet MVC eCommerce
sudo rm -rf index.html /var/www/html/*

echo "Testez svp ==> Adresse IP publique"
echo "Appuyez sur une touche une fois que vous avez vu la nouvelle page"
read -n 1 -s -r -p " "

echo "Nouveau site ecommerce ==> VOTRE-IP-PUBLIQUE/"
sudo git clone https://github.com/devopsgodhrehouma/mvc-ecommerce.git
sudo mv /var/www/html/mvc-ecommerce/* /var/www/html/
sudo rm -rf /var/www/html/mvc-ecommerce
sudo systemctl restart httpd
sudo chown ec2-user:ec2-user /var/www/html
sudo chmod -R 755 /var/www/html

# Pause pour vérification du site web

echo "Appuyez sur une touche une fois que vous avez vu la nouvelle page"
echo "SITE ECOMMERCE"
read -n 1 -s -r -p " "
echo "SITE ECOMMERCE"
echo "Continuer le script"

# Nettoyage et création des répertoires de projets de 3 sites
# Site 1 : Hello from cafe, Site 2 : ecommerce , Site 3 : Netflix, Site 4 : portfolio d'une personne
sudo rm -rf /var/www/html/*
echo "Testez svp ==> Adresse IP publique"
read -n 1 -s -r -p " "

echo "<html>Hello from the café web server</html>" > /var/www/html/index.html
sudo mkdir /var/www/html/mvc-ecommerce
sudo mkdir /var/www/html/netflix
sudo mkdir /var/www/html/vcard

# Clonage des projets depuis GitHub
sudo git clone https://github.com/devopsgodhrehouma/mvc-ecommerce.git /var/www/html/mvc-ecommerce
sudo git clone https://github.com/pro-prodipto/Netflix-Website-Project.git /var/www/html/netflix
sudo git clone https://github.com/codewithsadee/vcard-personal-portfolio.git /var/www/html/vcard

# Testez la commande suivante ls -la


# Configuration des permissions des répertoires
sudo chown -R ec2-user:ec2-user /var/www/html/mvc-ecommerce
sudo chown -R ec2-user:ec2-user /var/www/html/netflix
sudo chown -R ec2-user:ec2-user /var/www/html/vcard
sudo chmod -R 755 /var/www/html/mvc-ecommerce
sudo chmod -R 755 /var/www/html/netflix
sudo chmod -R 755 /var/www/html/vcard
sudo systemctl restart httpd

# Pause à la fin pour tester les projets
# IP/
# IP/mvc-ecommerce/
# IP/netflix
# IP/vcard

echo "Ajout d'une pause pour tester les projets ==> Adresse IP publique"
echo " Testez 1-IP/ ,2-IP/mvc-ecommerce/,3-IP/netflix, 4-IP/vcard "
echo "Testez et ensuite, Appuyez sur une touche pour terminer..."


read -n 1 -s -r -p " "
echo "Fin du script."

# Fin du script
echo "Script terminé."
