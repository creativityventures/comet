# Chapitre 11 — AssetList et AssetListFactory : etendre le nombre de collateraux

Le nombre d'actifs de collateral geres directement en stockage par `CometWithExtendedAssetList` est plafonne (`MAX_ASSETS_FOR_ASSET_LIST`). Pour les marches qui ont besoin de plus de collateraux que ce plafond, `AssetListFactory.createAssetList` deploie un contrat `AssetList` dedie, qui porte la liste complete des configurations d'actifs (flux de prix, echelle, facteurs) hors du contrat principal.

Le contrat Comet garde alors seulement l'adresse de cet `AssetList` externe (`assetList`, immuable comme le reste) et delegue les lectures de configuration d'actif a ce contrat separe plutot que de les stocker en interne. C'est le meme principe de deportation de donnees que `CometExt` pour l'enveloppe ERC20 (chapitre 9), applique cette fois a la liste de collateraux plutot qu'a l'interface de jeton.

Cette architecture en couches (stockage interne plafonne + extension externe optionnelle) permet au contrat principal de rester compact pour les marches simples qui n'ont besoin que de quelques collateraux, tout en offrant une echappatoire pour les marches plus riches sans jamais devoir reecrire la logique centrale du protocole.

[Chapitre suivant : CometRewards, la distribution de recompenses](12-rewards.md)
