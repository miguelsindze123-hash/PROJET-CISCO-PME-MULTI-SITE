# 2. Étude VLSM

Méthode : trier les besoins par ordre décroissant, puis allouer à chaque VLAN le plus petit sous-réseau (puissance de 2) couvrant l'effectif annoncé + adresse réseau + adresse de diffusion.

## Site de Bafoussam — `192.168.10.0/24`

Besoins triés : VLAN 20 (125), VLAN 30 (20), VLAN 10 (10).

| Ordre | VLAN / Liaison | Besoin | Bits hôte | Bloc alloué | Masque | Hôtes utilisables |
|---|---|---|---|---|---|---|
| 1 | VLAN 20 — Comptabilité | 125 | 7 (/25) | `192.168.10.0/25` | 255.255.255.128 | .1 – .126 (126) |
| 2 | VLAN 30 — Informatique | 20 | 5 (/27) | `192.168.10.128/27` | 255.255.255.224 | .129 – .158 (30) |
| 3 | VLAN 10 — Direction | 10 | 4 (/28) | `192.168.10.160/28` | 255.255.255.240 | .161 – .174 (14) |
| 4 | Liaison WAN Bafoussam ↔ Douala | 2 | 2 (/30) | `192.168.10.176/30` | 255.255.255.252 | .177 – .178 (2) |

Reliquat libre : `192.168.10.180 – 192.168.10.255` (76 adresses),réservé pour extension future (nouveau VLAN, redondance…) du site de Bafoussam 


## Site de Douala — `192.168.11.0/24`

Besoins triés : VLAN 40 (68), VLAN 50 (10), liaison WAN inter-sites (2).

| Ordre | VLAN | Besoin | Bits hôte | Bloc alloué | Masque | Hôtes utilisables |
|---|---|---|---|---|---|---|
| 1 | VLAN 40 — Commercial | 68 | 7 (/25) | `192.168.11.0/25` | 255.255.255.128 | .1 – .126 (126) |
| 2 | VLAN 50 — Support Technique | 10 | 4 (/28) | `192.168.11.128/28` | 255.255.255.240 | .129 – .142 (14) |

Reliquat libre : `192.168.11.144 – 192.168.11.255` (112 adresses), réservé pour extension future du site de Douala.

## Justification des choix

- **Tri décroissant des besoins** : évite la fragmentation en allouant d'abord les plus gros blocs, qui sont les plus contraints en emplacement.
- **Bloc `/30` pour la liaison WAN** : taille minimale standard pour un lien point-à-point (2 hôtes utiles), prélevée sur le reliquat de Bafoussam plutôt que sur celui de Douala afin de préserver la marge de croissance du VLAN Commercial (le plus grand des deux VLAN de Douala).
- **Reliquats conservés** : les adresses non allouées sur chaque site restent disponibles pour l'ajout futur d'un VLAN ou d'un lien de redondance, sans avoir à renuméroter l'existant.
