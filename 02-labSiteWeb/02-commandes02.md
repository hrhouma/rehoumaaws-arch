```bash
nano 1-setup_web_server.sh
chmod +x 1-setup_web_server.sh
sh 1-setup_web_server.sh
```
-------

🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇
### Contenu de `1-setup_web_server.sh`
🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇

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

----

```bash
nano 2-setup_database.sh
chmod +x 2-setup_database.sh
sh 2-setup_database.sh
```

🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇
### Contenu de `2-setup_database.sh`
🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇



### Correction de `2-setup_database.sh`

```bash
#!/bin/bash

# Naviguer vers le répertoire de l'environnement
cd ~/environment

# Télécharger et extraire les fichiers nécessaires
wget https://aws-tc-largeobjects.s3-us-west-2.amazonaws.com/ILT-TF-200-ACACAD-20-EN/mod4-challenge/setup.tar.gz
tar -zxvf setup.tar.gz

wget https://aws-tc-largeobjects.s3-us-west-2.amazonaws.com/ILT-TF-200-ACACAD-20-EN/mod4-challenge/db.tar.gz
tar -zxvf db.tar.gz

wget https://aws-tc-largeobjects.s3-us-west-2.amazonaws.com/ILT-TF-200-ACACAD-20-EN/mod4-challenge/cafe.tar.gz
tar -zxvf cafe.tar.gz

# Déplacer les fichiers extraits vers le répertoire web
sudo mv cafe /var/www/html/
cd setup
chmod +x set-app-parameters.sh

# Remplacer les scripts existants avec les nouveaux contenus
echo "
#!/bin/bash
#
# Script to set the MariaDB root user password right after database installation.
# and create an admin user.
#
# Check the set-root-password.log file after running it to verify successful execution.
#

sudo mysql --verbose < sql/set-root-password.sql > set-root-password.log

echo
echo \"Set Root Password script completed.\"
echo \"Please check the set-root-password.log file to verify successful execution.\"
echo
" > ../db/set-root-password.sh

echo "
--
-- Creates a root user that can connect from any host and sets the password for all root users in MariaDB
--
USE mysql;

DROP USER IF EXISTS 'root'@'%';
DROP USER IF EXISTS 'admin'@'%';

CREATE USER 'root'@'%' IDENTIFIED BY 'Re:Start!9';
CREATE USER 'admin'@'%' IDENTIFIED BY 'Re:Start!9';

ALTER USER 'root'@'%' IDENTIFIED BY 'Re:Start!9';
ALTER USER 'admin'@'%' IDENTIFIED BY 'Re:Start!9';

GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' WITH GRANT OPTION;
GRANT ALL PRIVILEGES ON *.* TO 'admin'@'%' WITH GRANT OPTION;

FLUSH PRIVILEGES;
" > ../db/sql/set-root-password.sql

echo "
#!/bin/bash
#
# Script to create and populate the cafe database.
# Check the create-db.log file after running it to verify successful execution.
#
sudo mysql --user=admin --password=\"Re:Start!9\" --verbose < sql/create-db.sql > create-db.log

echo
echo \"Create Database script completed.\"
echo \"Please check the create-db.log file to verify successful execution.\"
echo
" > ../db/create-db.sh

echo "
/*
Database Creation Script for the cafe database
*/
DROP DATABASE IF EXISTS cafe_db;

CREATE DATABASE cafe_db;

USE cafe_db;

/* Create PRODUCT_GROUP table. */

CREATE TABLE product_group (
  product_group_number INT(3) NOT NULL PRIMARY KEY,
  product_group_name VARCHAR(25) NOT NULL DEFAULT ''
  );

/* INSERT initialization data into the PRODUCT_GROUP table. */

INSERT INTO product_group (product_group_number, product_group_name) VALUES
 (1, 'Pastries')
, (2, 'Drinks');

/* Create PRODUCT table. */

CREATE TABLE product (
  id INT(3) NOT NULL AUTO_INCREMENT PRIMARY KEY,
  product_name VARCHAR(40) NOT NULL DEFAULT '',
  description VARCHAR(200) NOT NULL DEFAULT '',
  price DECIMAL(10,2) NOT NULL DEFAULT 0.0,
  product_group INT(2) NOT NULL DEFAULT 1,
  image_url VARCHAR(256) DEFAULT 'images/default-image.jpg',
  FOREIGN KEY (product_group) REFERENCES product_group (product_group_number)
  );

/* INSERT initialization data into the PRODUCT table. */

INSERT INTO product (product_name, description, price, product_group, image_url) VALUES
 ('Croissant', 'Fresh, buttery and fluffy... Simply delicious!', 1.50, 1, 'images/Croissants.jpg')
, ('Donut', 'We have more than half-a-dozen flavors!', 1.00, 1, 'images/Donuts.jpg')
, ('Chocolate Chip Cookie', 'Made with Swiss chocolate with a touch of Madagascar vanilla', 2.50, 1, 'images/Chocolate-Chip-Cookies.jpg')
, ('Muffin', 'Banana bread, blueberry, cranberry or apple', 3.00, 1, 'images/Muffins.jpg')
, ('Strawberry Blueberry Tart', 'Bursting with the taste and aroma of fresh fruit', 3.50, 1, 'images/Strawberry-Blueberry-Tarts.jpg')
, ('Strawberry Tart', 'Made with fresh ripe strawberries and a delicious whipped cream', 3.50, 1, 'images/Strawberry-Tarts.jpg')
, ('Coffee', 'Freshly-ground black or blended Columbian coffee', 3.00, 2, 'images/Coffee.jpg')
, ('Hot Chocolate', 'Rich and creamy, and made with real chocolate', 3.00, 2, 'images/Cup-of-Hot-Chocolate.jpg')
, ('Latte', 'Offered hot or cold and in various delicious flavors', 3.50, 2, 'images/Latte.jpg');

/* Create `order` table. */

CREATE TABLE `order` (
  order_number INT(5) NOT NULL AUTO_INCREMENT PRIMARY KEY,
  order_date_time TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
  amount DECIMAL(10,2) NOT NULL DEFAULT 0.0
  );

/* Create ORDER_ITEM table. */

CREATE TABLE order_item (
  order_number INT(5) NOT NULL,
  order_item_number INT(5) NOT NULL,
  product_id INT(3),
  quantity INT(2),
  amount DECIMAL(10,2) NOT NULL,
  PRIMARY KEY (order_number, order_item_number),
  FOREIGN KEY (order_number) REFERENCES `order` (order_number),
  FOREIGN KEY (product_id) REFERENCES product (id)
  );
" > ../db/sql/create-db.sql

# Exécution des scripts de base de données
cd ../db/
sudo sh set-root-password.sh
sudo sh create-db.sh

# Fin du script
echo "Script de configuration de la base de données terminé."
```

### Mise à jour du script `main_setup.sh` pour inclure le nouvel appel

```bash
#!/bin/bash

# Appel du script de configuration du serveur web
./1-setup_web_server.sh

# Appel du script de configuration de la base de données
./2-setup_database.sh

# Pause finale pour tester les projets
echo "Ajout d'une pause pour tester les projets ==> Adresse IP publique"
echo "Testez et ensuite, Appuyez sur une touche pour terminer..."
read -n 1 -s -r -p " "
echo "Fin du script principal."

# Fin du script principal
echo "Script principal terminé."
```


--------------


### Script de nettoyage : `cleanup.sh`

```bash
#!/bin/bash

# Arrêter les services
sudo systemctl stop httpd
sudo systemctl stop mariadb

# Supprimer les répertoires et fichiers créés
sudo rm -rf /var/www/html/*
sudo rm -rf ~/environment/setup.tar.gz ~/environment/db.tar.gz ~/environment/cafe.tar.gz
sudo rm -rf ~/environment/setup ~/environment/db ~/environment/cafe

# Supprimer les bases de données MariaDB
sudo mysql -u root -pRe:Start!9 -e "DROP DATABASE IF EXISTS cafe_db;"
sudo mysql -u root -pRe:Start!9 -e "DROP USER IF EXISTS 'root'@'%';"
sudo mysql -u root -pRe:Start!9 -e "DROP USER IF EXISTS 'admin'@'%';"

# Démarrer les services pour vérifier que tout a été supprimé
sudo systemctl start httpd
sudo systemctl start mariadb

# Message de fin
echo "Nettoyage terminé. Vous pouvez maintenant réexécuter les scripts."
```

### Exécution du script de nettoyage

1. Enregistrez le script ci-dessus dans un fichier nommé `cleanup.sh`.
2. Rendez le script exécutable et lancez-le :

```bash
chmod +x cleanup.sh
./cleanup.sh
```

### Réexécution des scripts de configuration

Après avoir nettoyé votre environnement, vous pouvez réexécuter les scripts de configuration :

```bash
chmod +x 1-setup_web_server.sh
chmod +x 2-setup_database.sh
./main_setup.sh
```

