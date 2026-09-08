# Chapitre 10 — Configurator : reconfigurer un protocole immuable par redeploiement

Puisque tous les parametres economiques de `CometWithExtendedAssetList` sont figes dans son constructeur, Comet ne peut pas les modifier en place comme le ferait Aave sur son `ReserveConfiguration`. A la place, `Configurator.sol` maintient en stockage mutable une copie **en attente** de la configuration courante (taux, facteurs de collateral, actif ajoute...), a travers des dizaines de fonctions setter (`setSupplyKink`, `updateAssetBorrowCollateralFactor`, `addAsset`...), chacune protegee par le gouverneur ou un "market admin" delegue.

Quand la gouvernance est prete a appliquer ces changements, une fabrique (`CometFactory` / `CometFactoryWithExtendedAssetList`) deploie une toute nouvelle instance de `CometWithExtendedAssetList` a partir de cette configuration en attente, puis `CometProxyAdmin` repointe le proxy public vers cette nouvelle implementation. Le contrat precedent devient obsolete ; son adresse ne sert plus jamais.

Ce cycle "modifier la configuration en attente -> redeployer -> repointer le proxy" est plus lourd qu'une simple ecriture de stockage, mais garantit qu'aucun parametre economique actif ne peut etre modifie autrement que par un remplacement complet et audite de l'implementation — une discipline de gouvernance imposee par la structure du code plutot que par une simple convention.

[Chapitre suivant : AssetList, etendre le nombre de collateraux](11-assetlist.md)
