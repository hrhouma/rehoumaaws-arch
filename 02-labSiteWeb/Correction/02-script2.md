#!/bin/bash

# Naviguer vers le répertoire de l'environnement
cd ~/environment

# Télécharger et extraire les fichiers nécessaires
cd ~/environment
wget https://aws-tc-largeobjects.s3.us-west-2.amazonaws.com/CUR-TF-200-ACACAD-2-91555/04-lab-mod4-challenge-EC2/s3/setup.zip
unzip setup.zip

wget https://aws-tc-largeobjects.s3.us-west-2.amazonaws.com/CUR-TF-200-ACACAD-2-91555/04-lab-mod4-challenge-EC2/s3/db.zip
unzip db.zip

wget https://aws-tc-largeobjects.s3.us-west-2.amazonaws.com/CUR-TF-200-ACACAD-2-91555/04-lab-mod4-challenge-EC2/s3/cafe.zip
unzip cafe.zip -d /var/www/html/



cd setup
chmod +x set-app-parameters.sh
./set-app-parameters.sh


# Remplacer les scripts existants avec les nouveaux contenus
echo "
#!/bin/bash
#
# Script pour définir le mot de passe root de MariaDB juste après l'installation de la base de données.
# et créer un utilisateur admin.
#
# Vérifiez le fichier set-root-password.log après l'exécution pour vérifier l'exécution réussie.
#

sudo mysql --verbose < sql/set-root-password.sql > set-root-password.log

echo
echo \"Le script de définition du mot de passe root est terminé.\"
echo \"Veuillez vérifier le fichier set-root-password.log pour vérifier l'exécution réussie.\"
echo
" > ../db/set-root-password.sh

echo "
--
-- Crée un utilisateur root pouvant se connecter depuis n'importe quel hôte et définit le mot de passe pour tous les utilisateurs root dans MariaDB
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
# Script pour créer et peupler la base de données cafe.
# Vérifiez le fichier create-db.log après l'exécution pour vérifier l'exécution réussie.
#
sudo mysql --user=admin --password=\"Re:Start!9\" --verbose < sql/create-db.sql > create-db.log

echo
echo \"Le script de création de la base de données est terminé.\"
echo \"Veuillez vérifier le fichier create-db.log pour vérifier l'exécution réussie.\"
echo
" > ../db/create-db.sh

# Insérer le script SQL mis à jour
echo "
/*
Script de création de la base de données pour la base de données cafe
*/
DROP DATABASE IF EXISTS cafe_db;

CREATE DATABASE cafe_db;

USE cafe_db;

/* Créer la table PRODUCT_GROUP. */

CREATE TABLE product_group (
  product_group_number INT(3) NOT NULL PRIMARY KEY,
  product_group_name VARCHAR(25) NOT NULL DEFAULT ''
  );

/* Insérer les données d'initialisation dans la table PRODUCT_GROUP. */

INSERT INTO product_group (product_group_number, product_group_name) VALUES
 (1, 'Pastries'),
 (2, 'Drinks');

/* Créer la table PRODUCT. */

CREATE TABLE product (
  id INT(3) NOT NULL AUTO_INCREMENT PRIMARY KEY,
  product_name VARCHAR(40) NOT NULL DEFAULT '',
  description VARCHAR(200) NOT NULL DEFAULT '',
  price DECIMAL(10,2) NOT NULL DEFAULT 0.0,
  product_group INT(2) NOT NULL DEFAULT 1,
  image_url VARCHAR(256) DEFAULT 'images/default-image.jpg',
  FOREIGN KEY (product_group) REFERENCES product_group (product_group_number)
  );
CREATE TABLE orders (
  order_number INT(5) NOT NULL AUTO_INCREMENT PRIMARY KEY,
  order_date_time DATETIME NOT NULL,
  customer_id INT(5),
  amount DECIMAL(10,2)
  );

/* Créer la table ORDER_ITEM. */

CREATE TABLE order_item (
  order_number INT(5) NOT NULL,
  order_item_number INT(5) NOT NULL,
  product_id INT(3),
  quantity INT(2),
  amount DECIMAL(10,2) NOT NULL,
  PRIMARY KEY (order_number, order_item_number),
  FOREIGN KEY (order_number) REFERENCES orders (order_number),
  FOREIGN KEY (product_id) REFERENCES product (id)
  );


/* Insérer les données d'initialisation dans la table PRODUCT. */

INSERT INTO product (product_name, description, price, product_group, image_url) VALUES 
 ('Croissant', 'Fraîche, beurrée et moelleuse... Tout simplement délicieuse!', 1.50, 1, 'images/Croissants.jpg'), 
 ('Donut', 'Nous avons plus d''une demi-douzaine de saveurs!', 1.00, 1, 'images/Donuts.jpg'), 
 ('Cookie aux pépites de chocolat', 'Fait avec du chocolat suisse avec une touche de vanille de Madagascar', 2.50, 1, 'images/Chocolate-Chip-Cookies.jpg'), 
 ('Muffin', 'Banana bread, myrtille, canneberge ou pomme', 3.00, 1, 'images/Muffins.jpg'), 
 ('Tarte fraise-myrtille', 'Pleine du goût et de l''arôme de fruits frais', 3.50, 1, 'images/Strawberry-Blueberry-Tarts.jpg'), 
 ('Tarte aux fraises', 'Fait avec des fraises fraîches mûres et une délicieuse crème fouettée', 3.50, 1, 'images/Strawberry-Tarts.jpg'), 
 ('Café', 'Café noir fraîchement moulu ou café colombien mélangé', 3.00, 2, 'images/Coffee.jpg'), 
 ('Chocolat chaud', '

Riche et crémeux, fait avec du vrai chocolat', 3.00, 2, 'images/Cup-of-Hot-Chocolate.jpg'), 
 ('Latte', 'Proposé chaud ou froid et dans diverses saveurs délicieuses', 3.50, 2, 'images/Latte.jpg');


" > ../db/sql/create-db.sql

# Exécution des scripts de base de données
cd ../db/
sudo sh set-root-password.sh
sudo sh create-db.sh

# Fin du script
echo "Script de configuration de la base de données terminé."



# Annexes : autres commandes utiles

cd ../db/
./set-root-password.sh
./create-db.sh

sudo mysql -u admin -p
Re:Start!9


DANS SQL 

show databases;
use cafe_db;
show tables;
select * from product;
exit;


sudo sed -i "2i date.timezone = \"America/New_York\" " /etc/php.ini
sudo service httpd restart
