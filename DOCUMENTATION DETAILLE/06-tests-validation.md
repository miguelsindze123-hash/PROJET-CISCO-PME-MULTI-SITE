# 6. Tests de validation

| # | Test | Commande | Résultat attendu |
|---|---|---|---|
| 1 | Connectivité intra-VLAN | `ping` entre deux PC du même VLAN | Succès |
| 2 | Routage inter-VLAN (même site) | `ping` PC-INFO → PC-DIRECTION | Succès (autorisé par l'ACL) |
| 3 | Isolation du VLAN Direction | `ping` PC-COMPTA → PC-DIRECTION | Échec (bloqué par l'ACL 110) |
| 4 | Attribution DHCP | `ipconfig /all` sur chaque PC | Adresse, passerelle et DNS corrects pour le VLAN |
| 5 | Résolution DNS | `ping intranet.bafoussam.ck237.local` | Résolution réussie vers 192.168.10.130 |
| 6 | Connectivité inter-sites | `ping` PC-COMPTA → PC-COMMERCIAL | Succès via EIGRP |
| 7 | Table de routage | `show ip route` sur R-BFS et R-DLA | Routes EIGRP vers tous les sous-réseaux distants |
| 8 | Voisinage EIGRP | `show ip EIGRP neighbor` | Voisin à l'état `FULL` entre R-BFS et R-DLA |
| 9 | VLAN et trunk | `show vlan brief` / `show interfaces trunk` | VLAN actifs, trunk correctement formé |
| 10 | Baux DHCP | `show ip dhcp binding` sur les routeurs | Bail actif pour chaque poste client |

## Ordre d'exécution recommandé

1. Mettre les interfaces `no shutdown` sur tous les équipements et vérifier l'état des liens (`show ip interface brief`).
2. Vérifier la formation des VLAN et des trunks (tests 9).
3. Vérifier l'attribution DHCP côté clients (test 4).
4. Vérifier le routage inter-VLAN local (test 2) puis l'isolation du VLAN Direction (test 3).
5. Vérifier la convergence EIGRP (tests 7 et 8) puis la connectivité inter-sites (test 6).
6. Vérifier la résolution DNS (test 5).
