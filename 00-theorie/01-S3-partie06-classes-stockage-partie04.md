# Partie (06/10) - Comprendre les Classes de Stockage Amazon S3 : Optimiser la Gestion des Données Cloud

# Références: 
- https://medium.com/analytics-vidhya/amazon-s3-storage-classes-d77de43df23d

## Types de Classes de Stockage S3

Amazon S3 propose une gamme de classes de stockage conçues pour différents cas d'utilisation. Elles offrent des options de stockage pour des données rarement utilisées, ne nécessitant pas un accès instantané, pour des archives à long terme, la préservation numérique, et bien plus encore. Toutes les classes de stockage Amazon S3 garantissent un haut niveau de fiabilité et prennent en charge le chiffrement SSL des données lors de la transmission, mais diffèrent par leurs coûts. S3 vérifie régulièrement l'intégrité de vos données grâce à des sommes de contrôle et propose une capacité d'auto-guérison. Les classes de stockage S3 permettent également une gestion des cycles de vie/politique pour la migration automatique des objets afin de réaliser des économies de coûts.

Les différentes classes de stockage proposées sont :

- **S3 Standard**
- **S3 Standard-IA**
- **S3 Intelligent-Tiering**
- **S3 One Zone-IA**
- **S3 Glacier**
- **S3 Glacier Deep Archive**
- **S3 Outposts**

### S3 Standard (Usage général)

- S3 Standard est la classe de stockage par défaut, si rien n'est spécifié lors du téléchargement.
- S3 Standard offre un stockage d'objets avec une haute durabilité, disponibilité et performance pour les données fréquemment accédées.
- S3 Standard propose une faible latence et un débit élevé.
- S3 Standard a une large gamme de cas d'utilisation, des applications cloud aux sites web dynamiques, services web, hébergement de sites web, analyses de big data, jeux mobiles, et distribution de contenu.
- C'est la classe de stockage la plus chère parmi toutes les autres.
- Conçu pour une durabilité de 99,999999999% des objets à travers plusieurs Zones de Disponibilité.
- Les données sont stockées dans plusieurs emplacements. S3 Standard est résistant aux événements affectant une zone de disponibilité entière et est conçu pour supporter la perte de données dans deux installations.
- Conçu pour une disponibilité de 99,99% sur une année donnée.
- Prend en charge le chiffrement SSL pour les données en transit et le chiffrement des données au repos.

### S3 Intelligent-Tiering (Accès inconnu ou changeant)

- S3 Intelligent-Tiering est conçu pour optimiser les coûts de stockage en déplaçant automatiquement les données vers le niveau d'accès le plus rentable, sans impact sur les performances ni surcharge opérationnelle.
- Il offre des économies automatiques en déplaçant les données à un niveau granulaire entre deux niveaux d'accès.

  - Un niveau optimisé pour l'accès fréquent.
  - Un autre niveau à moindre coût optimisé pour les données peu fréquemment accédées.

- Idéal pour optimiser les coûts de stockage automatiquement pour les données à long terme lorsque les modèles d'accès sont inconnus ou imprévisibles.
- Pour un petit frais mensuel de surveillance et d'automatisation par objet, S3 déplace les objets non accédés pendant 30 jours consécutifs vers le niveau d'accès peu fréquent. Si l'objet est accédé, il est automatiquement déplacé vers le niveau d'accès fréquent.
- Pas de frais de récupération ou de frais de nivellement supplémentaires.
- Conçu pour les objets de plus de 128 KB (les plus petits objets sont facturés pour 128 KB) conservés pendant au moins 30 jours (facturés pour un minimum de 30 jours).
- Faible latence et haute performance de débit.
- Durabilité de 99,999999999% et disponibilité de 99,99% sur une année donnée des objets à travers les zones de disponibilité.
- Déplacement automatique des données entre les deux niveaux d'accès (Accès Fréquent et Accès Peu Fréquent).
- Soutenu par l'Accord de Niveau de Service (SLA) d'Amazon S3 pour la disponibilité.
- Pas de durée minimale de stockage.
- Petite charge mensuelle de surveillance et d'auto-nivellement.

### S3 Standard-IA (Accès peu fréquent)

- S3 Standard-Infrequent Access est optimisé pour les données à long terme et moins fréquemment accédées, par exemple pour les sauvegardes et les anciennes données où l'accès est limité, mais l'utilisation exige toujours une haute performance.
- Idéal pour une copie primaire ou unique de données qui ne peuvent être recréées.
- Haute durabilité, faible latence et performance de débit élevée de S3 Standard mais avec un prix de stockage par Go inférieur et des frais de récupération par Go.
- Conçu pour une durabilité de 99,999999999% des objets à travers plusieurs Zones de Disponibilité.
- S3 Standard-IA est idéal pour les sauvegardes, le stockage à long terme et comme stockage de données pour la récupération après sinistre.
- Les données sont stockées de manière redondante à travers plusieurs zones de disponibilité géographiquement séparées et sont résistantes à la perte d'une zone de disponibilité.
- Offre une plus grande disponibilité et résilience que la classe ONEZONE_IA.
- Les objets sont disponibles pour un accès en temps réel.
- Conçu pour les objets de plus de 128 KB (les plus petits objets sont facturés pour 128 KB) conservés pendant au moins 30 jours (facturés pour un minimum de 30 jours).
- Conçu pour une durabilité de 99,999999999% des objets à travers les zones de disponibilité.
- Conçu pour une disponibilité de 99,9% sur une année donnée.
- Moins cher que le stockage S3 Standard.

### S3 One Zone-IA (Accès peu fréquent)

- S3 One Zone-IA est conçu pour les données à long terme et peu fréquemment accédées, mais disponibles pour un accès en millisecondes (similaire aux classes de stockage STANDARD et STANDARD_IA).
- Idéal lorsque les données peuvent être recréées si la zone de disponibilité échoue, et pour les répliques d'objets lors de la configuration de la réplication entre régions (CRR).
- Les objets sont disponibles pour un accès en temps réel.
- Conçu pour les objets de plus de 128 KB (les plus petits objets sont facturés pour 128 KB) conservés pendant au moins 30 jours (facturés pour un minimum de 30 jours).
- Contrairement aux autres classes de stockage S3 qui stockent les données dans un minimum de 3 zones de disponibilité (AZ), S3 One Zone-IA stocke les données des objets dans une seule AZ, ce qui le rend moins cher et coûte 20% moins cher que le Standard-Infrequent Access.
- Les données ne sont pas résistantes à la perte physique de l'AZ résultant de catastrophes, telles que les tremblements de terre et les inondations.
- S3 One Zone-IA est aussi durable que Standard-Infrequent Access, mais il est moins disponible et moins résilient.
- Conçu pour une durabilité de 99,999999999% des objets dans une seule AZ.
- Conçu pour une disponibilité de 99,5% sur une année donnée.
- S3 facture des frais de récupération pour ces objets, ils sont donc les plus appropriés pour les données peu fréquemment accédées.

### S3 Glacier (Archive)

- La classe de stockage GLACIER est adaptée à l'archivage des données à faible coût où l'accès aux données est peu fréquent et le temps de récupération de minutes à heures est acceptable.
- Période minimale de stockage de 90 jours.
- Offre des temps de récupération configurables, de quelques minutes à plusieurs heures.
- Pour accéder aux objets GLACIER :

  - L'objet doit être restauré, ce qui peut prendre entre quelques minutes et plusieurs heures.
  - Les objets ne sont disponibles que pour la période spécifiée lors de la demande de restauration.
  - La classe de stockage de l'objet reste GLACIER.
  - Des frais sont facturés à la fois pour l'archive (tarif GLACIER) et pour la copie restaurée temporairement.

- La fonctionnalité Vault Lock impose la conformité via une politique verrouillable.
- Offre la même durabilité et résilience que la classe de stockage STANDARD.
- Conçu pour une durabilité de 99,999999999% des objets à travers les zones de disponibilité.
- Conçu pour une disponibilité de 99,9% sur une année donnée.

### S3 Glacier Deep Archive

- La classe de stockage Glacier Deep Archive offre le coût le plus bas pour l'archivage des données où l'accès aux données est peu fréquent et un temps de récupération de plusieurs heures est acceptable.
- Période minimale de stockage de 180 jours et peut être accédée avec un temps de récupération par défaut de 12 heures.
- Prend en charge la rétention à long terme et la préservation numérique pour les données qui peuvent être accédées une ou deux fois par an.
- Conçu pour une durabilité de 99,999999999% des objets à travers les zones de disponibilité.
- Conçu pour une disponibilité de 99,9% sur une année donnée.
- Les coûts de récupération DEEP_ARCHIVE peuvent être réduits en utilisant la récupération en vrac, qui renvoie les données sous 48 heures.
- Alternative idéale aux bibliothèques de bandes magnétiques.
- Idéal pour les industries qui stockent des données pendant 5 à 10 ans ou plus, comme la santé, la finance, etc. Peut également être utilisé pour la sauvegarde et la récupération après sinistre

---
# Table comparative des différentes classes de stockage Amazon S3 :

| Classe de Stockage         | Description | Utilisation Idéale | Durabilité | Disponibilité | Latence et Débit | Frais de Stockage | Frais de Récupération | Durée Minimale de Stockage | 
|----------------------------|-------------|---------------------|------------|----------------|-------------------|-------------------|-----------------------|----------------------------|
| **S3 Standard**            | Stockage d'objets à haute durabilité, disponibilité et performance pour les données fréquemment accédées | Applications cloud, sites web dynamiques, analyses de big data, distribution de contenu | 99.999999999% | 99.99% | Faible latence, haut débit | Élevé | Aucun | Aucun |
| **S3 Intelligent-Tiering** | Optimisation automatique des coûts de stockage en déplaçant les données entre niveaux d'accès fréquent et peu fréquent | Données à long terme avec modèles d'accès inconnus ou imprévisibles | 99.999999999% | 99.99% | Faible latence, haut débit | Faible + frais de surveillance | Aucun | Aucun |
| **S3 Standard-IA**         | Stockage d'objets à haute durabilité et performance pour les données peu fréquemment accédées | Sauvegardes, stockage à long terme, récupération après sinistre | 99.999999999% | 99.9% | Faible latence, haut débit | Modéré | Frais par Go récupéré | 30 jours |
| **S3 One Zone-IA**         | Stockage d'objets pour les données peu fréquemment accédées dans une seule zone de disponibilité | Données pouvant être recréées en cas de perte de la zone de disponibilité, répliques d'objets | 99.999999999% | 99.5% | Faible latence, haut débit | Moindre que Standard-IA | Frais par Go récupéré | 30 jours |
| **S3 Glacier**             | Archivage à faible coût avec temps de récupération de minutes à heures | Archivage de données à accès peu fréquent avec temps de récupération acceptable | 99.999999999% | 99.9% | Latence élevée | Très faible | Frais de récupération | 90 jours |
| **S3 Glacier Deep Archive**| Archivage à coût minimal avec temps de récupération de plusieurs heures | Archivage de données à long terme, accès peu fréquent (ex : santé, finance) | 99.999999999% | 99.9% | Latence élevée | Très faible | Frais de récupération réduits (récupération en vrac) | 180 jours |
| **S3 Outposts**            | Stockage d'objets dans un environnement AWS on-premises | Charges de travail avec exigences locales de résidence des données, performances élevées requises | Conçu pour une durabilité et une redondance élevées | Selon l'environnement Outposts | Faible latence, haut débit | Variable selon l'utilisation | Aucun | Aucun |

Cette table fournit une vue d'ensemble rapide des principales caractéristiques et utilisations de chaque classe de stockage S3 d'Amazon.

