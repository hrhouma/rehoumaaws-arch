# Relations entre les Utilisateurs, Groupes, Rôles, Stratégies et Permissions dans AWS

Voici une représentation textuelle des relations entre les différents concepts :

## Schéma des Relations

```
Utilisateur (User)
     |
     V
Stratégie (Policy) -------> Permissions
     ^
     |
     |
Groupe (Group)
     |
     V
Stratégie (Policy) -------> Permissions
     ^
     |
     |
Rôle (Role)
     |
     V
Stratégie (Policy) -------> Permissions
```

## Explications

- **Utilisateur (User)** : Représente des individus ou des services nécessitant un accès à AWS.
  - Peut avoir des stratégies (Policies) directement attachées.
  - Peut appartenir à des groupes (Groups) et hériter des stratégies de ces groupes.

- **Groupe (Group)** : Collection d'utilisateurs partageant des permissions similaires.
  - Peut avoir des stratégies (Policies) attachées.
  - Les utilisateurs membres héritent des stratégies de leurs groupes.

- **Rôle (Role)** : Entité qui définit un ensemble de permissions pour effectuer des actions spécifiques dans AWS.
  - Contient des stratégies (Policies) qui définissent les permissions.
  - Souvent utilisé pour accorder des permissions aux services AWS ou aux applications.

- **Stratégie (Policy)** : Document JSON qui définit les permissions.
  - Spécifie les actions autorisées sur des ressources spécifiques.

- **Permissions (Permissions)** : Définissent les actions qu'une entité (utilisateur, groupe ou rôle) peut effectuer sur des ressources spécifiques.

## Exemple de Stratégie (Policy)

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::example-bucket/*"
        }
    ]
}
```

Dans cet exemple :

- `Version` : spécifie la version du langage de stratégie.
- `Statement` : contient les éléments de la stratégie.
  - `Effect` : spécifie si la stratégie permet (`Allow`) ou refuse (`Deny`) l'accès.
  - `Action` : liste les actions que la stratégie permet ou refuse.
  - `Resource` : spécifie les ressources sur lesquelles les actions sont autorisées ou refusées.
