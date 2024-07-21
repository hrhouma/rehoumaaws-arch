```bash
nano 1-setup_web_server.sh
chmod +x 1-setup_web_server.sh
sh 1-setup_web_server.sh
```

### Contenu de `1-setup_web_server.sh`

```bash
#!/bin/bash

# Mise à jour du système
sudo yum update -y

# Affichage de la version du noyau
cat /proc/version

# Installation des paquets nécessaires
sudo yum install -y git httpd mariadb-server php

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
sudo php --version

# Configuration des permissions et des liens symboliques
sudo ln -s /var/www/ /home/ec2-user/environment
sudo chown ec2-user:ec2-user /var/www/html

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
sudo git clone https://github.com/devopsgodhrehouma/mvc-ecommerce.git
sudo mv /var/www/html/mvc-ecommerce/* /var/www/html/
sudo rm -rf /var/www/html/mvc-ecommerce
sudo systemctl restart httpd
sudo chown ec2-user:ec2-user /var/www/html
sudo chmod -R 755 /var/www/html

# Pause pour vérification du site web
echo "Ajout d'une pause pour consulter le site web ==> Adresse IP publique"
echo "Testez et ensuite, Appuyez sur une touche pour continuer..."
read -n 1 -s -r -p " "
echo "Continuer le script"

# Nettoyage et création des répertoires de projets
sudo rm -rf /var/www/html/*
echo "<html>Hello from the café web server</html>" > /var/www/html/index.html

sudo mkdir /var/www/html/mvc-ecommerce
sudo mkdir /var/www/html/netflix
sudo mkdir /var/www/html/vcard

# Clonage des projets depuis GitHub
sudo git clone https://github.com/devopsgodhrehouma/mvc-ecommerce.git /var/www/html/mvc-ecommerce
sudo git clone https://github.com/pro-prodipto/Netflix-Website-Project.git /var/www/html/netflix
sudo git clone https://github.com/codewithsadee/vcard-personal-portfolio.git /var/www/html/vcard

# Configuration des permissions des répertoires
sudo chown -R ec2-user:ec2-user /var/www/html/mvc-ecommerce
sudo chown -R ec2-user:ec2-user /var/www/html/netflix
sudo chown -R ec2-user:ec2-user /var/www/html/vcard
sudo chmod -R 755 /var/www/html/mvc-ecommerce
sudo chmod -R 755 /var/www/html/netflix
sudo chmod -R 755 /var/www/html/vcard
sudo systemctl restart httpd

# Pause à la fin pour tester les projets
echo "Ajout d'une pause pour tester les projets ==> Adresse IP publique"
echo "Testez et ensuite, Appuyez sur une touche pour terminer..."
read -n 1 -s -r -p " "
echo "Fin du script."

# Fin du script
echo "Script terminé."
```

### Script principal pour appeler `1-setup_web_server.sh`

Créez un autre script, par exemple `main_setup.sh`, qui appellera le script `1-setup_web_server.sh`.

```bash
#!/bin/bash

# Appel du script de configuration
./1-setup_web_server.sh
```

Pour exécuter le script principal, rendez-le exécutable et lancez-le :

```bash
nano main_setup.sh
chmod +x main_setup.sh
./main_setup.sh
```

Ainsi, `main_setup.sh` appelle `1-setup_web_server.sh`, et à la fin de ce dernier, une pause est incluse pour vous permettre de tester les différents projets avant de terminer le script.
