# Tâche 1 : Analyse de l'instance EC2 existante

```sh
sudo yum update -y
cat /proc/version

# Installation de la pile LAMP - Linux - Apache - MYSQL - PHP 
sudo yum install -y httpd mariadb-server php

# Installation du serveur web APACHE
sudo yum install -y httpd 
sudo systemctl enable httpd
sudo systemctl start httpd
sudo systemctl status httpd

# Installation de la base de données mariadb (MYSQL)
sudo yum install -y mariadb-server
sudo systemctl enable mariadb
sudo systemctl start mariadb
sudo systemctl status mariadb

# Installation de la base de données mysql
# sudo yum install -y mysql-server
# sudo systemctl enable mysqld
# sudo systemctl start mysqld
# sudo systemctl status mysqld
# Installation de PHP
# sudo yum install -y php

# Vérification des états des services
sudo systemctl status httpd
sudo systemctl status mariadb

# Vérification des services
sudo httpd -v
sudo mysql --version
sudo php --version

sudo ln -s /var/www/ /home/ec2-user/environment
sudo chown ec2-user:ec2-user /var/www/html


# Ajouter la page web de test simple
echo '<html>Hello from the café web server!</html>' > /var/www/html/index.html

# TESTEZ @IP publique - TEST 1

# Téléchargement du premier dépôt GitHub
sudo yum install -y git
cd /var/www/html
sudo rm -rf index.html
sudo rm -rf /var/www/html/*
sudo git clone https://github.com/andrewtch88/mvc-ecommerce.git


# Configurer Apache pour utiliser le répertoire cloné
sudo mv /var/www/html/mvc-ecommerce/* /var/www/html/
sudo rm -rf /var/www/html/mvc-ecommerce
# Redémarrer Apache pour appliquer les changements
sudo systemctl restart httpd

# TESTEZ @IP publique - TEST 2


# Donner les permissions appropriées
# sudo chown -R apache:apache /var/www/html
# apache ne fonctionne pas , mais plutôt ec2-user
sudo chown ec2-user:ec2-user /var/www/html
sudo chmod -R 755 /var/www/html

# Redémarrer Apache pour appliquer les changements
sudo systemctl restart httpd

# Suppression de l'ancien site web
sudo rm -rf /var/www/html/*


# TESTEZ @IP publique - TEST 3

# Ajouter de nouveau la page web de test simple
echo "<html>Hello from the café web server</html>" > /var/www/html/index.html

# Création de dossiers pour les nouveaux sites web
sudo mkdir /var/www/html/netflix
sudo mkdir /var/www/html/vcard

# Téléchargement des nouveaux dépôts GitHub dans des dossiers distincts
sudo git clone https://github.com/pro-prodipto/Netflix-Website-Project.git /var/www/html/netflix
sudo git clone https://github.com/codewithsadee/vcard-personal-portfolio.git /var/www/html/vcard

# Donner les permissions appropriées
sudo chown -R apache:apache /var/www/html/netflix
sudo chown -R apache:apache /var/www/html/vcard
sudo chown -R ec2-user:ec2-user /var/www/html/netflix
sudo chown -R ec2-user:ec2-user /var/www/html/vcard
sudo chmod -R 755 /var/www/html/netflix
sudo chmod -R 755 /var/www/html/vcard

# Redémarrer Apache pour appliquer les changements
sudo systemctl restart httpd

# TESTEZ @IP publique - TEST 4
```

# Tâche 3 : Création d'une page web de test simple

```sh
sudo chown ec2-user:ec2-user /var/www/html
sudo rm -rf /var/www/html/*
echo "<html>Hello from the café web server!</html>" > /var/www/html/index.html
```

# Tâche 4 : Installation de l'application du café

```sh
cd ~/environment
wget https://aws-tc-largeobjects.s3-us-west-2.amazonaws.com/ILT-TF-200-ACACAD-20-EN/mod4-challenge/setup.tar.gz
tar -zxvf setup.tar.gz
wget https://aws-tc-largeobjects.s3-us-west-2.amazonaws.com/ILT-TF-200-ACACAD-20-EN/mod4-challenge/db.tar.gz
tar -zxvf db.tar.gz
wget https://aws-tc-largeobjects.s3-us-west-2.amazonaws.com/ILT-TF-200-ACACAD-20-EN/mod4-challenge/cafe.tar.gz
tar -zxvf cafe.tar.gz
mv cafe /var/www/html/
cd setup
./set-app-parameters.sh
cd ../db/
./set-root-password.sh
./create-db.sh
mysql -u root -p

# Commands inside MySQL
show databases;
use cafe_db;
show tables;
select * from product;
exit;

sudo sed -i "2i date.timezone = \"America/New_York\" " /etc/php.ini
sudo systemctl restart httpd
```

# Tâche 6 : Création d'une AMI et lancement d'une autre instance EC2

```sh
sudo hostname cafeserver
ssh-keygen -t rsa -f ~/.ssh/id_rsa
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
```

### Création d'une instance EC2 à partir de l'AMI dans une autre région AWS (Oregon)

```sh
cd setup
sed -i 's/region="us-east-1"/region="us-west-2"/' set-app-parameters.sh
sed -i 's/publicDNS=".*"/publicDNS="<public-dns-of-ProdCafeServer-instance>"/' set-app-parameters.sh
./set-app-parameters.sh
```

### Connexion SSH à la nouvelle instance (si nécessaire)

```sh
ssh -i ~/.ssh/id_rsa ec2-user@<public-ip-of-ProdCafeServer>
```


🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇
# Annexe 0 : Exécution
🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇

```sh
cd ../db/
chmod +x set-root-password.sh
chmod +x create-db.sh
./set-root-password.sh
./create-db.sh
sudo mysql -u admin -p
ou
sudo mysql -u root -p
ou
sudo mysql -u eleve -p
(en cas ou vous avez un autre utilisateur de la base de données eleve)
mot de passe : Re:Start!9
```

---
🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇
# Annexe 1 : Explication de quelques commandes
🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇

```sh
sudo mysql -u admin -p
OU
sudo mysql -u root -p
mot de passe : Re:Start!9
```

### 1. `sudo ln -s /var/www/ /home/ec2-user/environment`

- `sudo`: Ce préfixe exécute la commande avec des privilèges administratifs (super utilisateur).
- `ln -s`: Cette commande crée un lien symbolique. Un lien symbolique est comme un raccourci qui pointe vers un autre fichier ou répertoire.
- `/var/www/`: C'est la cible du lien symbolique. Il s'agit généralement du répertoire racine où les fichiers web sont stockés sur un serveur.
- `/home/ec2-user/environment`: C'est l'endroit où le lien symbolique sera créé.

**Explication complète**: Cette commande crée un lien symbolique nommé `environment` dans le répertoire `/home/ec2-user/`, qui pointe vers le répertoire `/var/www/`. Ainsi, lorsque vous accédez à `/home/ec2-user/environment`, vous accédez en réalité à `/var/www/`.

### 2. `sudo chown ec2-user:ec2-user /var/www/html`

- `sudo`: Encore une fois, cela exécute la commande avec des privilèges administratifs.
- `chown`: Cette commande change le propriétaire d'un fichier ou d'un répertoire.
- `ec2-user:ec2-user`: Cela spécifie le nouvel utilisateur et le nouveau groupe propriétaire. Dans ce cas, `ec2-user` est à la fois l'utilisateur et le groupe.
- `/var/www/html`: C'est le fichier ou le répertoire dont la propriété va être modifiée.

**Explication complète**: Cette commande change le propriétaire du répertoire `/var/www/html` pour qu'il soit `ec2-user`, et que le groupe propriétaire soit aussi `ec2-user`. Cela signifie que l'utilisateur `ec2-user` aura les permissions nécessaires pour lire, écrire et exécuter des actions sur ce répertoire.

En résumé :

- La première commande crée un lien symbolique pour accéder facilement au répertoire `/var/www/` à partir de l'environnement de l'utilisateur `ec2-user`.
- La deuxième commande change les permissions de façon à ce que l'utilisateur `ec2-user` puisse contrôler le répertoire `/var/www/html`.

# Annexe 2 :

```sh
nano script1.sh
chmod +x script1.sh
./script1.sh
```

```sh
#!/bin/bash

# Mise à jour du système
sudo yum update -y

# Vérification de la version du noyau
cat /proc/version

# Installation de la pile LAMP
sudo yum install -y httpd mariadb-server php git

# Configuration et démarrage d'Apache
sudo systemctl enable httpd
sudo systemctl start httpd
sudo systemctl status httpd

# Configuration et démarrage de MariaDB
sudo systemctl enable mariadb
sudo systemctl start mariadb
sudo systemctl status mariadb

# Vérification des versions des services installés
sudo httpd -v
sudo mysql --version
sudo php --version

# Création d'un lien symbolique vers le répertoire web et modification des permissions
sudo ln -s /var/www/ /home/ec2-user/environment
sudo chown ec2-user:ec2-user /var/www/html

# Ajout d'une page de test
echo '<html>Hello from the café web server!</html>' | sudo tee /var/www/html/index.html

# Téléchargement et déploiement du dépôt GitHub
cd /var/www/html
sudo rm -rf /var/www/html/*
sudo git clone https://github.com/andrewtch88/mvc-ecommerce.git
sudo mv mvc-ecommerce/* .
sudo rm -rf mvc-ecommerce
sudo chown ec2-user:ec2-user /var/www/html
sudo chmod -R 755 /var/www/html
sudo systemctl restart httpd

# Ajout de nouveau la page de test simple
sudo rm -rf /var/www/html/*
echo '<html>Hello from the café web server!</html>' | sudo tee /var/www/html/index.html

# Création de dossiers pour les nouveaux sites web
sudo mkdir /var/www/html/netflix /var/www/html/vcard

# Téléchargement des nouveaux dépôts GitHub
sudo git clone https://github.com/pro-prodipto/Netflix-Website-Project.git /var/www/html/netflix
sudo git clone https://github.com/codewithsadee/vcard-personal-portfolio.git /var/www/html/vcard

# Modification des permissions
sudo chown -R ec2-user:ec2-user /var/www/html/netflix /var/www/html/vcard
sudo chmod -R 755 /var/www/html/netflix /var/www/html/vcard

# Redémarrage d'Apache pour appliquer les changements
sudo systemctl restart httpd
```

Ce script exécute les étapes de mise à jour du système, d'installation des composants LAMP, de configuration et démarrage des services, de téléchargement et déploiement des sites web à partir de dépôts GitHub, et de modification des permissions nécessaires.

----
🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇
# Annexe 2 
🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇

J'ai crée deux fichiers, un pour l'utilisateur root et un pour l'utilisateur admin.

---
🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈
# Utilisateur root
🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈


Ce projet contient des scripts pour configurer et initialiser une base de données MariaDB. Les scripts permettent de définir le mot de passe de l'utilisateur root et de créer et peupler une base de données appelée `cafe_db`.

## Prérequis

Assurez-vous d'avoir MariaDB installé et accessible depuis la ligne de commande.

## Scripts

1. **set-root-password.sh**
2. **set-root-password.sql**
3. **create-db.sh**
4. **create-db.sql**

### Instructions

1. **Définir le mot de passe root**

   Le script `set-root-password.sh` définit le mot de passe pour l'utilisateur root de MariaDB.

   ```bash
   cd ../db/
   sudo ./set-root-password.sh
   ```

   Vérifiez le fichier `set-root-password.log` pour vous assurer de la bonne exécution du script.

2. **Exécuter le script SQL pour définir le mot de passe root**

   Le fichier `set-root-password.sql` contient les commandes SQL nécessaires pour définir le mot de passe root.

   ```bash
   sudo mysql --verbose < sql/set-root-password.sql
   ```

3. **Créer et peupler la base de données**

   Le script `create-db.sh` crée et peuple la base de données `cafe_db`.

   ```bash
   sudo ./create-db.sh
   ```

   Vérifiez le fichier `create-db.log` pour vous assurer de la bonne exécution du script.

4. **Exécuter le script SQL pour créer et peupler la base de données**

   Le fichier `create-db.sql` contient les commandes SQL nécessaires pour créer et peupler la base de données.

   ```bash
   sudo mysql --user=root --password="Re:Start!9" --verbose < sql/create-db.sql
   ```

### Contenu des Scripts

#### set-root-password.sh

```bash
#!/bin/bash
#
# Script to set the MariaDB root user password right after database installation.
#
# Check the set-root-password.log file after running it to verify successful execution.
#
sudo mysql --verbose < sql/set-root-password.sql > set-root-password.log

echo
echo "Set Root Password script completed."
echo "Please check the set-root-password.log file to verify successful execution."
echo
```

#### set-root-password.sql

```sql
--
-- Sets the password for the root user in MariaDB
--
USE mysql;
ALTER USER 'root'@'%' IDENTIFIED BY 'Re:Start!9';
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```

#### create-db.sh

```bash
#!/bin/bash
#
# Script to create and populate the cafe database.
# Check the create-db.log file after running it to verify successful execution.
#
mysql --user=root --password="Re:Start!9" --verbose < sql/create-db.sql > create-db.log

echo
echo "Create Database script completed."
echo "Please check the create-db.log file to verify successful execution."
echo
```

#### create-db.sql

```sql
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

/* Create ORDER table. */

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
```

## Notes

- Les fichiers SQL doivent être placés dans un répertoire `sql` situé dans le même répertoire que les scripts `.sh`.
- Assurez-vous que les permissions d'exécution sont définies sur les scripts `.sh` avant de les exécuter.

```bash
chmod +x set-root-password.sh
chmod +x create-db.sh
```

----
🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈
# Utilisateur admin
🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈🥈

Ce projet contient des scripts pour configurer et initialiser une base de données MariaDB. Les scripts permettent de définir le mot de passe de l'utilisateur root, de créer un utilisateur admin et de créer et peupler une base de données appelée `cafe_db`.

## Prérequis

Assurez-vous d'avoir MariaDB installé et accessible depuis la ligne de commande.

## Scripts

1. **set-root-password.sh**
2. **set-root-password.sql**
3. **create-db.sh**
4. **create-db.sql**

### Instructions

1. **Définir le mot de passe root et créer l'utilisateur admin**

   Le script `set-root-password.sh` définit le mot de passe pour l'utilisateur root de MariaDB et crée l'utilisateur admin.

   ```bash
   cd ../db/
   sudo ./set-root-password.sh
   ```

   Vérifiez le fichier `set-root-password.log` pour vous assurer de la bonne exécution du script.

2. **Exécuter le script SQL pour définir le mot de passe root et créer l'utilisateur admin**

   Le fichier `set-root-password.sql` contient les commandes SQL nécessaires pour définir le mot de passe root et créer l'utilisateur admin.

   ```bash
   sudo mysql --verbose < sql/set-root-password.sql
   ```

3. **Créer et peupler la base de données**

   Le script `create-db.sh` crée et peuple la base de données `cafe_db` en utilisant l'utilisateur admin.

   ```bash
   sudo ./create-db.sh
   ```

   Vérifiez le fichier `create-db.log` pour vous assurer de la bonne exécution du script.

4. **Exécuter le script SQL pour créer et peupler la base de données**

   Le fichier `create-db.sql` contient les commandes SQL nécessaires pour créer et peupler la base de données.

   ```bash
   sudo mysql --user=admin --password="Re:Start!9" --verbose < sql/create-db.sql
   ```

### Contenu des Scripts

#### set-root-password.sh

```bash
#!/bin/bash
#
# Script to set the MariaDB root user password right after database installation.
# and create an admin user.
#
# Check the set-root-password.log file after running it to verify successful execution.
#
sudo mysql --verbose < sql/set-root-password.sql > set-root-password.log

echo
echo "Set Root Password script completed."
echo "Please check the set-root-password.log file to verify successful execution."
echo
```

#### set-root-password.sql

```sql
--
-- Creates a root user that can connect from any host and sets the password for all root users in MariaDB
--
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
```

#### create-db.sh

```bash
#!/bin/bash
#
# Script to create and populate the cafe database.
# Check the create-db.log file after running it to verify successful execution.
#
mysql --user=admin --password="Re:Start!9" --verbose < sql/create-db.sql > create-db.log

echo
echo "Create Database script completed."
echo "Please check the create-db.log file to verify successful execution."
echo
```

#### create-db.sql

```sql
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

/* Create ORDER table. */

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
```

```sql
sudo mysql -u admin -p
select * from `product`;
```
![image](https://github.com/user-attachments/assets/d077a7b8-71cd-4b17-8600-1176ae986a46)


## Notes

- Les fichiers SQL doivent être placés dans un répertoire `sql` situé dans le même répertoire que les scripts `.sh`.
- Assurez-vous que les permissions d'exécution sont définies sur les scripts `.sh` avant de les exécuter.

```bash
chmod +x set-root-password.sh
chmod +x create-db.sh
```




🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇
# Annexe1 - Configuration MySQL sur Ubuntu
🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇

```bash
# Installation de MySQL Server
sudo apt-get install mysql-server

# Connexion à MySQL
sudo mysql

# Configuration des utilisateurs MySQL
CREATE USER 'eleve'@'localhost' IDENTIFIED BY 'eleve';
GRANT ALL PRIVILEGES ON *.* TO 'eleve'@'localhost' WITH GRANT OPTION;
ALTER USER 'root'@'localhost' IDENTIFIED WITH 'mysql_native_password' BY 'eleve';
FLUSH PRIVILEGES;
DESCRIBE mysql.user;
SELECT User, Host FROM mysql.user;
SELECT user, authentication_string, plugin, host FROM mysql.user;
FLUSH PRIVILEGES;
exit;

# Connexion avec l'utilisateur root
sudo mysql -u root -p
```
🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇
# Annexe4 - Configuration MariaDB sur Amazon Linux 2023
🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇🥇

```bash
# Connexion à MariaDB
sudo mysql

# Configuration des utilisateurs MariaDB
CREATE USER 'eleve'@'localhost' IDENTIFIED BY 'eleve';
GRANT ALL PRIVILEGES ON *.* TO 'eleve'@'localhost' WITH GRANT OPTION;
ALTER USER 'root'@'localhost' IDENTIFIED BY 'eleve';
FLUSH PRIVILEGES;
DESCRIBE mysql.user;
SELECT User, Host FROM mysql.user;
SELECT user, authentication_string, plugin, host FROM mysql.user;
FLUSH PRIVILEGES;
SHOW DATABASES;
CREATE DATABASE employee;
USE employee;
CREATE TABLE emp_info(
    emp_id INT(11),
    emp_name VARCHAR(50),
    emp_username VARCHAR(50),
    emp_password VARCHAR(50),
    emp_email VARCHAR(50),
    emp_phone BIGINT(20)
);
SHOW TABLES;
exit;

# Connexion avec l'utilisateur root
sudo mysql -u root -p

# Gestion de la base de données 'employee'
SHOW DATABASES;
USE employee;
SHOW TABLES;
SELECT * FROM emp_info;
```


