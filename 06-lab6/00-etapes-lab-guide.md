# Étapes: 

```plaintext
+--------------------------+
|      Créer un VPC         |
|      CIDR: 10.0.0.0/16    |
+--------------------------+
           |
           |
+--------------------------+       +--------------------------+
|  Créer un sous-réseau     |       |  Créer un sous-réseau     |
|  Public (10.0.0.0/24)     |       |  Privé (10.0.2.0/23)      |
+--------------------------+       +--------------------------+
           |                               |
           |                               |
+--------------------------+       +--------------------------+
|  Créer une passerelle     |       |  Créer une table de       |
|  Internet (IGW)           |       |  routage privée           |
+--------------------------+       |  - Route locale vers      |
           |                      |    le VPC (10.0.0.0/16)    |
           |                      +--------------------------+
+--------------------------+
|  Attacher la passerelle   |
|  au VPC                   |
+--------------------------+
           |
           |
+--------------------------+
|  Créer une table de       |
|  routage publique         |
|  - Route 0.0.0.0/0 vers   |
|    IGW                    |
+--------------------------+
           |
           |
+--------------------------+       +--------------------------+
|  Associer la table de     |       |  Associer la table de     |
|  routage publique         |       |  routage privée           |
|  au sous-réseau public    |       |  au sous-réseau privé     |
+--------------------------+       +--------------------------+
           |
           |
+--------------------------+
|  Lancer une instance      |
|  EC2 dans le sous-réseau  |
|  public                   |
+--------------------------+
```

### Étapes mises à jour :

1. **Créer un VPC** avec une plage CIDR globale (par exemple, `10.0.0.0/16`).
2. **Créer un sous-réseau public** (`10.0.0.0/24`) pour les ressources accessibles depuis Internet.
3. **Créer un sous-réseau privé** (`10.0.2.0/23`) pour les ressources internes non accessibles depuis Internet.
4. **Créer une passerelle Internet** (IGW) pour permettre l'accès Internet.
5. **Attacher la passerelle Internet** au VPC.
6. **Créer une table de routage publique** :
   - Ajouter une route `0.0.0.0/0` pointant vers l'IGW.
   - Associer cette table au sous-réseau public.
7. **Créer une table de routage privée** :
   - Assurer une route locale au sein du VPC (`10.0.0.0/16`).
   - Associer cette table au sous-réseau privé.
8. **Lancer une instance EC2** dans le sous-réseau public pour tester la connectivité.

# Annexe : uniuqment publique simplifié

```plaintext
+--------------------------+
|      Créer un VPC         |
|      CIDR: 10.0.0.0/16    |
+--------------------------+
           |
           |
+--------------------------+
|  Créer un sous-réseau     |
|  Public (10.0.0.0/24)     |
+--------------------------+
           |
           |
+--------------------------+
|  Créer un sous-réseau     |
|  Privé (10.0.2.0/23)      |
+--------------------------+
           |
           |
+--------------------------+
|  Créer une passerelle     |
|  Internet (IGW)           |
+--------------------------+
           |
           |
+--------------------------+
|  Attacher la passerelle   |
|  au VPC                   |
+--------------------------+
           |
           |
+--------------------------+
|  Créer une table de       |
|  routage pour le public   |
|  - Route 0.0.0.0/0 vers   |
|    IGW                    |
+--------------------------+
           |
           |
+--------------------------+
|  Associer la table de     |
|  routage au sous-réseau   |
|  public                   |
+--------------------------+
           |
           |
+--------------------------+
|  Lancer une instance      |
|  EC2 dans le sous-réseau  |
|  public                   |
+--------------------------+
```

### Étapes principales :

1. **Créer un VPC** avec une plage CIDR globale.
2. **Créer un sous-réseau public** pour les ressources accessibles depuis Internet.
3. **Créer un sous-réseau privé** pour les ressources internes non accessibles depuis Internet.
4. **Créer une passerelle Internet** (IGW) pour permettre l'accès Internet.
5. **Attacher la passerelle Internet** au VPC.
6. **Créer une table de routage publique** avec une route 0.0.0.0/0 pointant vers l'IGW.
7. **Associer la table de routage** au sous-réseau public.
8. **Lancer une instance EC2** dans le sous-réseau public pour tester la connectivité.
