# Chapitre 2 — Architecture : proxy, actif de base unique et collateraux

Un deploiement Comet est un contrat de proxy (`CometProxyAdmin`, motif transparent proxy standard) qui delegue tous ses appels vers une implementation `CometWithExtendedAssetList`. Cette implementation est **immuable** : tous ses parametres economiques (taux d'interet, facteurs de collateral, actif de base...) sont fixes une seule fois dans le constructeur, sous forme de variables `immutable`, et ne peuvent plus changer sans deployer une toute nouvelle implementation et repointer le proxy dessus. Ce choix de conception est aux antipodes du Pool unique et mutable d'Aave v3 : Comet echange de la flexibilite de configuration contre des lectures de stockage moins chere et une surface d'attaque reduite.

Chaque compte utilisateur a une position resumee par un seul `UserBasic.principal` (entier signe : positif si le compte prete l'actif de base, negatif s'il l'emprunte) et un bitmap `assetsIn` qui indique quels collateraux il detient, permettant de parcourir uniquement les actifs effectivement utilises plutot que la liste complete a chaque calcul de solvabilite.

Le nombre d'actifs de collateral geres directement dans le stockage du contrat est plafonne (`MAX_ASSETS_FOR_ASSET_LIST`, 24 dans cette version) ; au-dela, un contrat externe `AssetList` (chapitre 11) prend le relais. Chaque actif de collateral porte ses propres parametres : flux de prix, echelle, facteur d'emprunt, facteur de liquidation, facteur de liquidation-remise et plafond de detention.

[Chapitre suivant : stockage et indices de principal](03-stockage.md)
