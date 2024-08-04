# Quiz : Module 4 - Challenge Lab: Créer un Site Web Dynamique pour le Café

#### Instructions :
- Ce quiz est conçu pour évaluer votre compréhension des étapes nécessaires à la configuration et au déploiement d'un site web dynamique sur AWS, en particulier en utilisant des instances EC2 et des services associés.
- Répondez aux questions suivantes en cochant la bonne réponse. Certaines questions peuvent avoir plus d'une réponse correcte.

---

**Question 1:** Quelles sont les étapes pour configurer une instance EC2 afin qu'elle héberge un site web pour le café ?

1. Analyser l'instance EC2 existante
2. Connecter à l'IDE AWS Cloud9 sur l'instance EC2
3. Installer une application web sur l'instance EC2 en utilisant AWS Systems Manager Parameter Store
4. Tester l'application web
5. Créer une Image Machine Amazon (AMI)
6. Déployer une deuxième copie de l'application web dans une autre région AWS

A. 1, 2, 3, 4  
B. 2, 3, 4, 5  
C. 1, 2, 3, 4, 5, 6  
D. 3, 4, 5, 6  

---

**Question 2:** Quel service AWS est utilisé pour fournir un environnement de développement intégré (IDE) sur l'instance EC2 ?

A. AWS CloudFormation  
B. AWS Cloud9  
C. AWS Lambda  
D. AWS CodeCommit  

---

**Question 3:** Quelle commande permet de vérifier la version du serveur web Apache installé sur l'instance EC2 ?

A. `sudo chkconfig httpd on`  
B. `sudo service httpd status`  
C. `sudo httpd -v`  
D. `sudo yum install -y mariadb-server`  

---

**Question 4:** Que fait la commande `ln -s /var/www/ /home/ec2-user/environment` dans le terminal bash de AWS Cloud9 ?

A. Elle redémarre le serveur web.  
B. Elle change la propriété du répertoire /var/www/html.  
C. Elle crée un lien symbolique du répertoire /var/www vers le répertoire de travail d'AWS Cloud9.  
D. Elle configure la timezone dans PHP.  

---

**Question 5:** Quel est l'objectif de la création d'une Image Machine Amazon (AMI) ?

A. Tester les performances de l'instance EC2.  
B. Créer une copie de l'instance EC2 pour le déploiement dans une autre région AWS.  
C. Augmenter la capacité de stockage de l'instance EC2.  
D. Optimiser la sécurité de l'instance EC2.  

---

**Question 6:** Que fait le script `set-app-parameters.sh` dans le contexte de cette lab ?

A. Il installe l'application web sur l'instance EC2.  
B. Il configure les paramètres de l'application dans AWS Systems Manager Parameter Store.  
C. Il crée une nouvelle instance EC2.  
D. Il redémarre le serveur web Apache.  

---

**Question 7:** Quelle est la commande pour installer le serveur de base de données MariaDB sur l'instance EC2 ?

A. `sudo yum install -y mariadb-server`  
B. `sudo service mariadb start`  
C. `sudo chkconfig mariadb on`  
D. `mysql -u admin -p`  

---

**Question 8:** Quelle est la méthode pour tester si le site web du café est accessible depuis l'internet ?

A. Vérifier la configuration de l'instance EC2 dans la console AWS.  
B. Tenter de charger `http://<public-ip>` dans un nouvel onglet de navigateur.  
C. Configurer les paramètres de sécurité du groupe de sécurité de l'instance EC2.  
D. Redémarrer le serveur web Apache.  

---

**Question 9:** Quelles sont les actions à entreprendre pour rendre le site web accessible sur le port TCP 80 ?

A. Configurer le groupe de sécurité pour permettre le trafic HTTP entrant sur le port 80.  
B. Modifier le fichier de configuration de PHP.  
C. Créer un lien symbolique du répertoire web.  
D. Redémarrer l'instance EC2.  

---

**Question 10:** Quelle est l'utilité de la commande `ssh-keygen -t rsa -f ~/.ssh/id_rsa` lors de la création d'une nouvelle instance EC2 ?

A. Créer une clé publique et privée SSH pour l'authentification sécurisée.  
B. Redémarrer l'instance EC2.  
C. Configurer la timezone dans PHP.  
D. Installer le serveur de base de données MariaDB.  

