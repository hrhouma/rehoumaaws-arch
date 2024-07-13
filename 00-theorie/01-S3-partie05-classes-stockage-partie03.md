# Partie (05/10) - Comprendre les Classes de Stockage Amazon S3 : Optimiser la Gestion des Données Cloud

# Références :
- https://www.linkedin.com/pulse/understanding-amazon-s3-storage-classes-making-most-cloud-ajit-pisal
- https://medium.com/@msghodekar/understanding-the-different-storage-types-in-amazon-s3-383d62800700
- https://medium.com/analytics-vidhya/amazon-s3-storage-classes-d77de43df23d

#### Introduction : Le Défi du Stockage des Données

À mesure que les entreprises accumulent de vastes quantités de données, le défi de stocker, d'accéder et de gérer ces données devient de plus en plus complexe. Les solutions de stockage traditionnelles manquent souvent de scalabilité, de rentabilité et d'adaptabilité. C'est ici qu'Amazon S3 excelle, offrant une gamme de classes de stockage répondant à différents besoins.

#### Comprendre les Classes de Stockage Amazon S3

Amazon S3 propose plusieurs classes de stockage, chacune conçue pour optimiser le stockage des données en fonction de facteurs tels que la durabilité, la disponibilité, la latence et le coût. Voici un aperçu des principales classes de stockage :

1. **Amazon S3 Standard**
   - **Usage** : Données fréquemment accédées et actives.
   - **Durabilité et disponibilité** : Haute durabilité et disponibilité.
   - **Latence** : Accès en millisecondes.
   - **Coût** : $0.023/Go.

2. **Amazon S3 Intelligent-Tiering**
   - **Usage** : Données avec des schémas d'accès changeants.
   - **Durabilité et disponibilité** : Haute durabilité et disponibilité.
   - **Latence** : Accès en millisecondes.
   - **Coût** : $0.025 à $0.0125/Go.
   - **Particularités** : Frais de surveillance par objet, durée minimale de stockage.

3. **Amazon S3 Standard-IA (Infrequent Access)**
   - **Usage** : Données accédées de manière peu fréquente.
   - **Durabilité et disponibilité** : Haute durabilité et disponibilité.
   - **Latence** : Accès en millisecondes.
   - **Coût** : $0.0125/Go.
   - **Particularités** : Frais de récupération par Go, durée minimale de stockage.

4. **Amazon S3 One Zone-IA (Infrequent Access)**
   - **Usage** : Données pouvant être recréées, moins critiques.
   - **Durabilité et disponibilité** : Stockées dans une seule zone de disponibilité.
   - **Latence** : Accès en millisecondes.
   - **Coût** : $0.01/Go.
   - **Particularités** : Frais de récupération par Go, durée minimale de stockage.

5. **Amazon S3 Glacier**
   - **Usage** : Archivage et rétention de données à long terme.
   - **Durabilité et disponibilité** : Haute durabilité.
   - **Latence** : Accès en minutes ou heures.
   - **Coût** : $0.004/Go.
   - **Particularités** : Frais de récupération par Go, durée minimale de stockage.

6. **Amazon S3 Glacier Deep Archive**
   - **Usage** : Archivage à très long terme.
   - **Durabilité et disponibilité** : Haute durabilité.
   - **Latence** : Accès en heures.
   - **Coût** : $0.00099/Go.
   - **Particularités** : Frais de récupération par Go, durée minimale de stockage.

#### Optimisation des Coûts et des Performances

Les classes de stockage Amazon S3 permettent aux organisations de trouver un équilibre entre performances et coûts. En choisissant intelligemment la bonne classe de stockage pour chaque jeu de données, vous pouvez optimiser les dépenses de votre infrastructure cloud tout en garantissant que les données restent accessibles quand nécessaire.

#### Conclusion

Les classes de stockage Amazon S3 offrent une boîte à outils complète pour relever divers défis de stockage des données. En alignant les classes de stockage avec les caractéristiques uniques de vos données et vos schémas d'accès, vous pouvez élaborer une stratégie de stockage qui améliore les performances, réduit les coûts et s'aligne sur les objectifs plus larges de votre organisation. À mesure que le paysage du cloud continue d'évoluer, maîtriser les subtilités des classes de stockage S3 est une compétence précieuse pour tout professionnel du cloud.

### Tableau Comparatif des Classes de Stockage S3

| Classe de Stockage                  | Utilisation Fréquente                            | Utilisation Infrequente                                          | Coût                 | Latence          | Durabilité et Disponibilité                          | Particularités                                            |
|-------------------------------------|--------------------------------------------------|-------------------------------------------------------------------|----------------------|------------------|-----------------------------------------------------|----------------------------------------------------------|
| **S3 Standard**                     | Données actives, fréquemment accédées            | -                                                                 | $0.023/Go            | Millisecondes    | ≥ 3 AZ                                              | -                                                        |
| **S3 Intelligent-Tiering**          | Données avec des schémas d'accès changeants       | -                                                                 | $0.025 à $0.0125/Go  | Millisecondes    | ≥ 3 AZ                                              | Frais de surveillance par objet, durée minimale de stockage |
| **S3 Standard-IA**                  | -                                                | Données accédées de manière peu fréquente                         | $0.0125/Go           | Millisecondes    | ≥ 3 AZ                                              | Frais de récupération par Go, durée minimale de stockage  |
| **S3 One Zone-IA**                  | -                                                | Données pouvant être recréées, moins critiques                    | $0.01/Go             | Millisecondes    | 1 AZ                                                | Frais de récupération par Go, durée minimale de stockage  |
| **S3 Glacier**                      | -                                                | Archivage et rétention de données à long terme                    | $0.004/Go            | Minutes ou heures | ≥ 3 AZ                                              | Frais de récupération par Go, durée minimale de stockage  |
| **S3 Glacier Deep Archive**         | -                                                | Archivage à très long terme                                       | $0.00099/Go          | Heures           | ≥ 3 AZ                                              | Frais de récupération par Go, durée minimale de stockage  |


![1693393916325](https://github.com/user-attachments/assets/47f8b861-5022-4da2-be68-2bcb8940d00c)
![image](https://github.com/user-attachments/assets/24c9056e-561e-4a4f-ac68-4f9a88b94f53)
