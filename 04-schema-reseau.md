# 4. Schéma réseau

![Topologie réseau CK_237](../DIAGRAMME/Architecture.PNG)

## Description de la topologie

Chaque site est structuré autour d'un routeur assurant le routage inter-VLAN par la méthode *router-on-a-stick* (sous-interfaces 802.1Q), relié par un lien trunk à un commutateur d'accès. Les postes clients et les serveurs sont raccordés en accès sur le VLAN correspondant.

- **R-BFS** (Bafoussam) porte trois sous-interfaces : `Gi0/0/0.10` (Direction), `Gi0/0/0.20` (Comptabilité), `Gi0/0/0.30` (Informatique), et une interface série `Se0/1/0` vers Douala.
- **R-DLA** (Douala) porte deux sous-interfaces : `Gi0/0/1.40` (Commercial), `Gi0/0/1.50` (Support Technique), et une interface série `Se0/1/1` vers Bafoussam.
- **SW-BFS** et **SW-DLA** relient les postes clients et serveurs de chaque site à leur routeur respectif via un lien trunk (`802.1Q`).
- La liaison **WAN** entre `R-BFS` et `R-DLA` (`192.168.10.176/30`) est simulée par une liaison série ; le routage entre les deux sites est assuré par **EIGRP** .
- Les serveurs **SRV-BFS** et **SRV-DLA** (DHCP + DNS) sont rattachés respectivement au VLAN Informatique (Bafoussam) et au VLAN Support Technique (Douala).

## Équipements

| Rôle | Bafoussam | Douala |
|---|---|---|
| Routeur | R-BFS | R-DLA |
| Commutateur | SW-BFS | SW-DLA |
| Serveur DHCP/DNS | SRV-BFS | SRV-DLA |
| Postes clients | PC-DIRECTION, PC-COMPTA, PC-INFO | PC-COMMERCIAL, PC-SUPPORT |
