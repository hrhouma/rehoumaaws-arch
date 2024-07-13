## Cours sur les Stratégies (Policies) et les Rôles (Roles) dans AWS

### Introduction

Dans AWS (Amazon Web Services), la gestion des accès et des permissions est cruciale pour la sécurité et l'efficacité de votre infrastructure. Les principaux composants de cette gestion sont les utilisateurs (users), les groupes (groups), les rôles (roles), les stratégies (policies), et les permissions (permissions).

### Concepts Clés

1. **Utilisateurs (Users)**:
   - Représentent des individus ou des services nécessitant un accès à AWS.

2. **Groupes (Groups)**:
   - Collections d'utilisateurs partageant des permissions similaires.

3. **Rôles (Roles)**:
   - Entités qui définissent un ensemble de permissions pour effectuer des actions spécifiques dans AWS.
   - Souvent utilisés pour accorder des permissions aux services AWS ou aux applications.

4. **Stratégies (Policies)**:
   - Documents JSON qui définissent les permissions.
   - Peuvent être attachées à des utilisateurs, des groupes, ou des rôles.

5. **Permissions (Permissions)**:
   - Définissent les actions qu'une entité (utilisateur, groupe, ou rôle) peut effectuer sur des ressources spécifiques.

### Relations entre les Concepts

- Les utilisateurs et les groupes peuvent avoir des stratégies (policies) directement attachées.
- Les rôles contiennent des stratégies (policies) qui définissent les permissions.
- Les stratégies (policies) définissent les permissions qui spécifient quelles actions sont autorisées sur quelles ressources.

### Exemple de Stratégie (Policy)

Voici un exemple simple de stratégie (policy) JSON qui accorde des permissions de lecture sur un bucket S3 :

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

### Schéma de Relations

Voici un schéma illustrant les relations entre utilisateurs, groupes, rôles, stratégies (policies), et permissions :

```plaintext
Utilisateur (User)  -> Stratégie (Policy) -> Permissions
                 \
                  -> Groupe (Group) -> Stratégie (Policy) -> Permissions
                 /
Rôle (Role)      -> Stratégie (Policy) -> Permissions
```

- Les **utilisateurs** peuvent avoir des stratégies (policies) directement attachées.
- Les **groupes** peuvent avoir des stratégies (policies) attachées, et les utilisateurs membres de ces groupes héritent de ces stratégies.
- Les **rôles** contiennent des stratégies (policies) qui définissent leurs permissions.

### Conclusion

En résumé, la gestion des accès et des permissions dans AWS repose sur des stratégies (policies) qui définissent les permissions. Ces stratégies peuvent être attachées à des utilisateurs, des groupes, ou des rôles, permettant ainsi une gestion flexible et sécurisée des accès.
