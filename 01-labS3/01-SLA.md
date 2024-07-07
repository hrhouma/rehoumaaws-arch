# README - SLA et Durabilité

## 1. SLA : Qu'est-ce que c'est ? (Disponibilité)

### SLA : Qu'est-ce que c'est ?
SLA signifie "Service Level Agreement" ou "Accord de Niveau de Service" en français. C'est fondamentalement une promesse entre un fournisseur de service et un client, indiquant le niveau de service que le client peut attendre.

### Explication de 99.99999999999% (11 Neuf) SLA
Lorsqu'un fournisseur de services promet un SLA de 99.99999999999%, cela signifie qu'il assure que ses services seront disponibles et opérationnels 99.99999999999% du temps sur une période déterminée (par exemple, une année).

Pour mettre cela en perspective, si nous prenons une année entière (soit 31 536 000 secondes) et si le service n'est pas disponible seulement 0.00000000001% du temps, cela se traduit mathématiquement par :
$ 31 536 000 \text{ secondes/année} \times \frac{0.00000000001}{100} \text{ indisponibilité} = 0.0031536 \text{ secondes/année} $
Cela signifie qu'avec un SLA de 99.99999999999%, le service promet d'être indisponible au maximum pendant environ 0.003 secondes par an.

### Pourquoi est-ce important ?
Pour les entreprises et les individus qui dépendent fortement des services numériques (par exemple, une boutique en ligne, un service bancaire en ligne, etc.), même une petite indisponibilité peut avoir des conséquences graves, telles que la perte de ventes, la perte de données, ou l'insatisfaction des clients.

Plus le pourcentage est élevé, plus le service est fiable, mais aussi plus le coût pour maintenir un tel niveau de service est élevé.

### Un Petit Exemple
Imaginons un service de stockage de données dans le cloud, un peu comme Amazon S3.

- **Sans un SLA fort** : Si le service est down (hors ligne ou inaccessible) même pour une courte durée, les entreprises qui dépendent de ce service pour stocker des données (comme les bases de données de clients, des fichiers importants, etc.) pourraient faire face à des problèmes tels que l'impossibilité d'accéder à des informations cruciales ou de réaliser des ventes.
- **Avec un SLA de 99.99999999999%** : Le service garantit qu'il sera quasiment toujours disponible, avec une très, très courte période d'indisponibilité possible (0.003 secondes par an). Cela rassure les entreprises clientes qu'elles pourront accéder à leurs données presque tout le temps sans interruption.

### Tableau de différents niveaux de SLA et leur équivalent en temps d'indisponibilité
| SLA (%)         | SLA (nombre de neuf) | Indisponibilité annuelle | Indisponibilité mensuelle | Indisponibilité hebdomadaire | Indisponibilité quotidienne |
|-----------------|----------------------|--------------------------|---------------------------|------------------------------|-----------------------------|
| 90%             | 1                    | 36.5 jours               | 3 jours                   | 16.8 heures                  | 2.4 heures                  |
| 99%             | 2                    | 3.65 jours               | 7.2 heures                | 1.68 heures                  | 14.4 minutes                |
| 99.9%           | 3                    | 8.76 heures              | 43.2 minutes              | 10.1 minutes                 | 1.44 minutes                |
| 99.99%          | 4                    | 52.6 minutes             | 4.32 minutes              | 1.01 minutes                 | 8.64 secondes               |
| 99.999%         | 5                    | 5.26 minutes             | 25.9 secondes             | 6.05 secondes                | 0.864 secondes              |
| 99.9999%        | 6                    | 31.5 secondes            | 2.59 secondes             | 0.605 secondes               | 0.0864 secondes             |
| 99.99999%       | 7                    | 3.15 secondes            | 0.259 secondes            | 0.0605 secondes              | 0.00864 secondes            |
| 99.9999999%     | 9                    | 0.315 secondes           | 0.0259 secondes           | 0.00605 secondes             | 0.000864 secondes           |
| 99.999999999%   | 10                   | 0.0315 secondes          | 0.00259 secondes          | 0.000605 secondes            | 0.0000864 secondes          |
| 99.9999999999%  | 11                   | 0.00315 secondes         | 0.000259 secondes         | 0.0000605 secondes           | 0.00000864 secondes         |
| 99.99999999999% | 12                   | 0.000315 secondes        | 0.0000259 secondes        | 0.00000605 secondes          | 0.000000864 secondes        |



# CONCLUSION
- Un SLA (Service Level Agreement), ou Accord de Niveau de Service en français, est une promesse entre un fournisseur de service et un client, définissant le niveau de service attendu. Un SLA de 99.99999999999% (11 neuf) indique que le service promet d'être opérationnel et disponible 99.99999999999% du temps, ce qui équivaut à une potentielle indisponibilité d'environ 0.003 secondes par an.
- Bien que ce niveau de disponibilité exceptionnellement élevé minimise les risques d'interruptions et garantit une fiabilité presque totale, il est également associé à des coûts et une complexité technique importants pour le fournisseur du service. Les entreprises s'appuient sur des SLA robustes pour assurer la continuité de leurs opérations numériques, tout en veillant à équilibrer les coûts et les bénéfices.
- Garantir un SLA avec un aussi haut niveau de disponibilité est complexe et coûteux, et il faut toujours peser le coût par rapport au bénéfice. En général, les exigences du SLA devraient être alignées avec les besoins réels de l'entreprise et le niveau de tolérance au risque.

## 2. Durabilité

### Introduction
Expliquons brièvement la différence entre la disponibilité et la durabilité. Examinons cela avec un exemple basé sur la durabilité.

### 99.999% (cinq 9)
Supposons qu'une entreprise stocke 1 million d'objets de données dans un service de stockage en cloud offrant une durabilité de 99.999% sur une année. Avec une durabilité de 99.999%, la probabilité de perte de données est de 0.001% (0.00001/100 = 0.001%) par objet par an.

Calculons l'attente statistique de la perte de données pour cette entreprise :
\[ 1 000 000 \text{ objets} \times 0.001% \text{ probabilité de perte par objet} = 10 \text{ objets perdus par an} \]

### 99.999999999% (11 neuf) - niveau maximal de durabilité
Imaginons un service de stockage de données en cloud qui offre une durabilité de 99.999999999% (11 neuf) sur une année donnée. Cela signifie qu'il y a une probabilité de 0.000000001% de perdre un objet de données au cours d'une année.

Supposons qu'une entreprise utilise ce service de stockage et qu'elle stocke 1 milliard d'objets dans le cloud. Avec une durabilité de 99.999999999%, ou une probabilité de perte de données de 0.000000001% par objet par an, on peut s'attendre, en moyenne, à perdre :
\[ 1 000 000 000 \text{ objets} \times 0.000000001% \text{ probabilité de perte par objet} = 0.01 \text{ objet perdu par an} \]
Ce qui signifie qu'en moyenne, il faudrait environ 100 ans pour s'attendre à perdre un seul objet, sur la base de cette probabilité.

### Disponibilité vs Durabilité
- **Disponibilité** : Elle concerne le temps d'accès aux données. Un système avec une haute disponibilité est celui qui est opérationnel et accessible lorsque vous en avez besoin. Les SLA de disponibilité sont souvent exprimés en termes de pourcentage de temps opérationnel par rapport à une période donnée, comme nous l'avons vu dans le tableau précédent.
- **Durabilité** : Elle se rapporte à la préservation à long terme des données. Un système offrant une haute durabilité assure que, une fois que les données ont été stockées, elles ne seront pas perdues ou endommagées au fil du temps. La durabilité est souvent exprimée en termes de probabilité de perte de données au cours d'une année donnée.

### Tableau de différents niveaux de durabilité et leur équivalent en probabilité de perte de données
| Durabilité (%) | Durabilité (nombre de neuf) | Probabilité de perte de données par an |
|----------------|-----------------------------|---------------------------------------|
| 99%            | 2                           | 1%                                    |
| 99.9%          | 3                           | 0.1%                                  |
| 99.99%         | 4                           | 0.01%                                 |
| 99.999%        | 5                           | 0.001%                                |
| 99

.9999%       | 6                           | 0.0001%                               |
| 99.99999%      | 7                           | 0.00001%                              |
| 99.999999%     | 8                           | 0.000001%                             |
| 99.9999999%    | 9                           | 0.0000001%                            |
| 99.99999999%   | 10                          | 0.00000001%                           |
| 99.999999999%  | 11                          | 0.000000001%                          |
| 99.9999999999% | 12                          | 0.0000000001%                         |

### Conclusion
Même avec une très haute durabilité, il existe toujours une petite probabilité de perte de données. C'est pourquoi les systèmes de sauvegarde et les stratégies de récupération après incident sont cruciaux même dans les systèmes avec une durabilité très élevée. L'équilibre entre disponibilité, durabilité et coût doit être ajusté en fonction des besoins spécifiques et des exigences de votre application ou entreprise. Chaque ajout de "neuf" dans vos objectifs de durabilité ou de disponibilité peut augmenter considérablement la complexité et le coût de la solution de stockage.

[Retour en haut](#readme---sla-et-durabilit%C3%A9)
