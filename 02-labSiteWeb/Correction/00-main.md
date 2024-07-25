# Introduction
- Nous allons créer un script principal `main.sh` qui exécute les deux scripts `1-setup_web_server.sh` et `2-setup_database.sh` dans l'ordre.
- Pour ce faire, voici comment vous pouvez procédé :

1. Créez les deux scripts individuels `1-setup_web_server.sh` et `2-setup_database.sh`.
2. Rendez-les exécutables avec la commande `chmod +x`.
3. Créez un script principal `main.sh` qui appelle les deux scripts dans l'ordre.

- Voici les étapes détaillées :

### Étape 1: Créer et éditer `1-setup_web_server.sh`
Ouvrez le fichier `1-setup_web_server.sh` avec nano :
```sh
nano 1-setup_web_server.sh
```
Ajoutez votre script de configuration du serveur web dans ce fichier.

### Étape 2: Rendre le script exécutable
```sh
chmod +x 1-setup_web_server.sh
```

### Étape 3: Créer et éditer `2-setup_database.sh`
Ouvrez le fichier `2-setup_database.sh` avec nano :
```sh
nano 2-setup_database.sh
```
Ajoutez votre script de configuration de la base de données dans ce fichier.

### Étape 4: Rendre le script exécutable
```sh
chmod +x 2-setup_database.sh
```

### Étape 5: Créer et éditer le script principal `main.sh`
Ouvrez le fichier `main.sh` avec nano :
```sh
nano main.sh
```
Ajoutez les lignes suivantes dans `main.sh` :
```sh
#!/bin/bash
sh 1-setup_web_server.sh
sh 2-setup_database.sh
```

### Étape 6: Rendre le script principal exécutable
```sh
chmod +x main.sh
```

### Étape 7: Exécuter le script principal
```sh
./main.sh
```

Ce script `main.sh` va exécuter `1-setup_web_server.sh` en premier, puis `2-setup_database.sh` ensuite.

# Annexe :

```sh
nano 1-setup_web_server.sh
chmod +x 1-setup_web_server.sh
sh 1-setup_web_server.sh

nano 2-setup_database.sh
chmod +x 2-setup_database.sh
sh 2-setup_database.sh
```
