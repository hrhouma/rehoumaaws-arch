### Tâche 1 : Analyse de l'instance EC2 existante

```sh
sudo yum update -y
cat /proc/version
sudo yum install -y httpd mysql-server php
sudo systemctl enable httpd
sudo systemctl start httpd
sudo systemctl status httpd
sudo systemctl enable mysqld
sudo systemctl start mysqld
sudo systemctl status mysqld
sudo httpd -v
mysql --version
php --version
ln -s /var/www/ /home/ec2-user/environment
sudo chown ec2-user:ec2-user /var/www/html
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
