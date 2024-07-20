### Tâche 1 : Analyse de l'instance EC2 existante

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
sudo git clone https://github.com/andrewtch88/mvc-ecommerce.git


# Configurer Apache pour utiliser le répertoire cloné
sudo mv /var/www/html/mvc-ecommerce/* /var/www/html/
sudo rm -rf /var/www/html/mvc-ecommerce
# Redémarrer Apache pour appliquer les changements
sudo systemctl restart httpd

# TESTEZ @IP publique - TEST 2


# Donner les permissions appropriées
# sudo chown -R apache:apache /var/www/html
# sudo chmod -R 755 /var/www/html

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
sudo chmod -R 755 /var/www/html/netflix
sudo chmod -R 755 /var/www/html/vcard

# Redémarrer Apache pour appliquer les changements
sudo systemctl restart httpd

```

### Tâche 3 : Création d'une page web de test simple

```sh
echo "<html>Hello from the café web server!</html>" > /var/www/html/index.html
```

### Tâche 4 : Installation de l'application du café

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

### Tâche 6 : Création d'une AMI et lancement d'une autre instance EC2

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


# Annexe 1

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
