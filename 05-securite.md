# 5. Politique de sécurité

## Exigence

Le VLAN Direction (10) ne doit être accessible qu'au service Informatique (VLAN 30). Aucun autre département ne doit pouvoir joindre directement les équipements de la Direction.

## Mise en œuvre

Une ACL étendue est appliquée sur `R-BFS`, en sortie (`out`) de la sous-interface `Gi0/0.10` (VLAN Direction) :

```
access-list 110 permit ip 192.168.10.128 0.0.0.31 192.168.10.160 0.0.0.15
access-list 110 deny ip any 192.168.10.160 0.0.0.15
access-list 110 permit ip any any

interface GigabitEthernet0/0.10
 ip access-group 110 out
```

## Fonctionnement

1. La première ligne autorise uniquement le trafic issu du VLAN Informatique (`192.168.10.128/27`) à destination du VLAN Direction.
2. La deuxième ligne rejette tout autre trafic entrant vers le VLAN Direction (Comptabilité, Commercial, Support Technique, etc.).
3. La troisième ligne autorise le reste du trafic sortant du routeur, afin de ne pas perturber les autres flux.

## Limites connues et recommandations

Cette ACL filtre par sous-réseau source/destination ; elle n'est pas *stateful* (elle ne suit pas l'état des connexions). Pour une politique plus fine et plus robuste, il est recommandé à terme de :

- Migrer vers une liste d'accès **réflexive** (`reflexive access-list`) ou une politique de **zone-based firewall (ZBF)**.
- Activer l'authentification des échanges de routage EIGRP (MD5/SHA).
- Sécuriser l'accès administratif des équipements : mots de passe chiffrés (`service password-encryption`), AAA, SSH plutôt que Telnet.
