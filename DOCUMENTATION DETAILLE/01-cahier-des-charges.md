# 1. Cahier des charges

## Contexte

L'entreprise **CK_237** est une PME en pleine croissance disposant de deux sites :

- **Bafoussam** (Siège social)
- **Douala** (Agence secondaire)

Mission : concevoir, configurer et documenter l'ensemble de l'infrastructure réseau de l'entreprise.

## Site de Bafoussam (siège)

| VLAN | Département | Effectif |
|---|---|---|
| 10 | Direction | 10 postes |
| 20 | Comptabilité | 125 postes |
| 30 | Informatique | 20 postes |

**Exigences :**
- Plan d'adressage VLSM à partir du réseau `192.168.10.0/24`
- Routage inter-VLAN
- Service DHCP pour chaque VLAN
- Serveur DNS interne
- Au minimum un poste client par VLAN
- Vérification de la connectivité et des services réseau

## Site de Douala (agence)

| VLAN | Département | Effectif |
|---|---|---|
| 40 | Commercial | 68 postes |
| 50 | Support Technique | 10 postes |

**Exigences :**
- Plan d'adressage cohérent à partir du réseau `192.168.11.0/24`
- Configuration des VLAN
- Mise en place du DHCP
- Mise en place du DNS
- Déploiement des postes clients
- Vérification des communications internes

## Interconnexion des sites

Les deux sites doivent être reliés par une liaison WAN simulée.

- Mise en place d'un protocole de routage dynamique (OSPF ou EIGRP)
- Les réseaux des deux sites doivent être entièrement joignables
- Les tables de routage doivent être générées automatiquement

## Politique de sécurité

- Le VLAN Direction ne doit être accessible qu'au service Informatique
- Les autres départements ne doivent pas accéder directement aux équipements de la Direction
- Les accès doivent être contrôlés à l'aide d'ACL ou de mécanismes de filtrage appropriés

## Livrables attendus

- **A. Schéma réseau** — topologie complète de l'infrastructure
- **B. Plan d'adressage** — adresse IP, masque, passerelle, VLAN, nom des équipements
- **C. Étude VLSM** — calcul détaillé des sous-réseaux et justification des choix
- **D. Configurations** — routeurs, switches, serveurs
- **E. Rapport technique** — présentation du projet, analyse des besoins, choix techniques, plan d'adressage, configurations réalisées, tests effectués, difficultés rencontrées.
---
*Source : cahier des charges du projet test Cisco, auteur SINDZE WAGNE MIGUEL.*
