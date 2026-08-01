# 3. Plan d'adressage

## Site de Bafoussam

| Équipement | Interface | VLAN | Adresse IP | Masque | Passerelle |
|---|---|---|---|---|---|
| R-BFS | Gi0/0/0.10 | 10 — Direction | 192.168.10.161 | /28 | — |
| R-BFS | Gi0/0/0.20 | 20 — Comptabilité | 192.168.10.1 | /25 | — |
| R-BFS | Gi0/0/0.30 | 30 — Informatique | 192.168.10.129 | /27 | — |
| R-BFS | Se0/1/0 (WAN) | — | 192.168.10.177 | /30 | — |
| SW-BFS | SVI VLAN 30 (gestion) | 30 | 192.168.10.158 | /27 | 192.168.10.129 |
| SRV-BFS (DHCP) | Fa0 | 30 — Informatique | 192.168.10.130 | /27 | 192.168.10.129 |
| SRV-BFS (DNS) | Fa0 | 10 — Direction | 192.168.10.174 | /28 | 192.168.10.161 |
| PC-DIRECTION | Fa0 | 10 — Direction | attribuée par DHCP | /28 | 192.168.10.161 |
| PC-COMPTA | Fa0 | 20 — Comptabilité | attribuée par DHCP | /25 | 192.168.10.1 |
| PC-INFO | Fa0 | 30 — Informatique | attribuée par DHCP | /27 | 192.168.10.129 |

## Site de Douala

| Équipement | Interface | VLAN | Adresse IP | Masque | Passerelle |
|---|---|---|---|---|---|
| R-DLA | Gi0/0/1.40 | 40 — Commercial | 192.168.11.1 | /25 | — |
| R-DLA | Gi0/0/1.50 | 50 — Support Technique | 192.168.11.129 | /28 | — |
| R-DLA | Se0/1/1 (WAN) | — | 192.168.10.178 | /30 | — |
| SW-DLA | SVI VLAN 50 (gestion) | 50 | 192.168.11.140 | /28 | 192.168.11.129 |
| SRV-DLA (DHCP) | Fa0 | 50 — Support Technique | 192.168.11.130 | /28 | 192.168.11.129 |
| SRV-DLA (DNS) | Fa0 | 40 — Commercial | 192.168.11.126 | /25 | 192.168.11.1 |
| PC-COMMERCIAL | Fa0 | 40 — Commercial | attribuée par DHCP | /25 | 192.168.11.1 |
| PC-SUPPORT | Fa0 | 50 — Support Technique | attribuée par DHCP | /28 | 192.168.11.129 |

## Exclusions DHCP

| Routeur | Adresses exclues |
|---|---|
| R-BFS | 192.168.10.161 ; 192.168.10.1 – .2 ; 192.168.10.129 – .130 |
| R-DLA | 192.168.11.1  ; 192.168.11.129 – .130 |

Les adresses de passerelle et celle du serveur DHCP/DNS de chaque VLAN sont exclues du pool afin d'éviter tout conflit d'adressage.
