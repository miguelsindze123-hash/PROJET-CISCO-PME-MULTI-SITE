# Infrastructure réseau multi-sites — Entreprise CK_237

> Projet test Cisco : conception, configuration et documentation de l'infrastructure réseau d'une PME disposant de deux sites — **Bafoussam** (siège social) et **Douala** (agence secondaire).

![Statut](https://img.shields.io/badge/statut-terminé-brightgreen) ![VLSM](https://img.shields.io/badge/adressage-VLSM-blue) ![Routage](https://img.shields.io/badge/routage-OSPF-informational) ![Simulateur](https://img.shields.io/badge/testé%20sur-Cisco%20Packet%20Tracer-lightgrey)

**Auteur :** SINDZE WAGNE MIGUEL — Etudiant réseau & Securite

**Date : 01/08/2026** 

---

## Sommaire

- [Contexte](#contexte)
- [Architecture](#architecture)
- [Plan d'adressage (résumé)](#plan-dadressage-résumé)
- [Politique de sécurité](#politique-de-sécurité)
- [Comment utiliser ce dépôt](#comment-utiliser-ce-dépôt)
- [Documentation complète](#documentation-complète)

## Contexte

L'entreprise **CK_237** est une PME en croissance disposant de deux sites : Bafoussam (siège social) et Douala (agence secondaire). Ce dépôt regroupe l'ensemble des livrables du projet : étude d'adressage VLSM, plan d'adressage, schéma réseau, configurations Cisco IOS et rapport technique complet.

**Objectifs du projet :**
- Segmenter chaque site par VLAN (Direction, Comptabilité, Informatique à Bafoussam ; Commercial, Support Technique à Douala).
- Construire un plan d'adressage VLSM à partir de `192.168.10.0/24` (Bafoussam) et `192.168.11.0/24` (Douala).
- Mettre en place le routage inter-VLAN sur chaque site et une interconnexion WAN inter-sites en routage dynamique (OSPF).
- Déployer les services DHCP (par VLAN) et DNS interne (par site).
- Restreindre l'accès au VLAN Direction au seul service Informatique (ACL).

## Architecture

![Topologie réseau CK_237](diagramme/Architecture.PNG)
Chaque site repose sur un routeur assurant le routage inter-VLAN (sous-interfaces 802.1Q, *router-on-a-stick*) relié en trunk à un commutateur d'accès. Les deux routeurs de site sont interconnectés par une liaison WAN série sur laquelle tourne OSPF (zone 0).

| Site | Routeur | Commutateur | VLAN | Serveur |
|---|---|---|---|---|
| Bafoussam (siège) | R-BFS | SW-BFS | 10 (Direction), 20 (Comptabilité), 30 (Informatique) | SRV-BFS (DHCP + DNS) |
| Douala (agence) | R-DLA | SW-DLA | 40 (Commercial), 50 (Support Technique) | SRV-DLA (DHCP + DNS) |



## Plan d'adressage (résumé)

**Bafoussam — `192.168.10.0/24`**

| VLAN | Désignation | Réseau | Masque | Passerelle |
|---|---|---|---|---|
| 10 | Direction | 192.168.10.160/28 | 255.255.255.240 | 192.168.10.161 |
| 20 | Comptabilité | 192.168.10.0/25 | 255.255.255.128 | 192.168.10.1 |
| 30 | Informatique | 192.168.10.128/27 | 255.255.255.224 | 192.168.10.129 |


**Douala — `192.168.11.0/24`**

| VLAN | Désignation | Réseau | Masque | Passerelle |
|---|---|---|---|---|
| 40 | Commercial | 192.168.11.0/25 | 255.255.255.128 | 192.168.11.1 |
| 50 | Support Technique | 192.168.11.128/28 | 255.255.255.240 | 192.168.11.129 |
| — | Liaison WAN vers Douala | 192.168.10.176/30 | 255.255.255.252 | — |

Détail complet du calcul VLSM : [`DOCUMENTATION DETAILLE/02-etude-vlsm.md`](docs/02-etude-vlsm.md). Table d'adressage complète (équipements, serveurs, postes) : [`DOCUMENTATION DETAILLE/03-plan-adressage.md`](docs/03-plan-adressage.md).

## Politique de sécurité

Le VLAN Direction (10) n'est accessible qu'au service Informatique (VLAN 30) via une ACL étendue appliquée sur R-BFS. Détails et commandes : [`DOCUMENTATION DETAILLE/05-securite.md`](docs/05-securite.md).

## Comment utiliser ce dépôt

1. Ouvrir un simulateur compatible IOS (Cisco Packet Tracer ou GNS3) et construire la topologie décrite dans [`diagramme/Architecture.PNG`](diagramme/Architecture.PNG).
2. Copier-coller le contenu de chaque fichier `.cfg` du dossier [`configuration/`](configuration/) dans le mode de configuration globale (`configure terminal`) de l'équipement correspondant.
3. Vérifier la connectivité et les services à l'aide du protocole de tests décrit dans [`DOCUMENTATION DETAILLE/06-tests-validation.md`](docs/06-tests-validation.md).

## Documentation complète

Le rapport technique complet (présentation, analyse des besoins, choix techniques, VLSM, plan d'adressage, configurations, tests, difficultés rencontrées, recommandations) est disponible dans [`Rapport_Technique_CK237`](Rapport_Technique_CK237.docx), [`Rapport_Technique_CK237.docx`](Rapport_Technique_CK237.docx).
