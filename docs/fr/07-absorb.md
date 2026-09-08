# Chapitre 7 — absorb : la liquidation par saisie totale et remboursement par les reserves

`absorb`, appelable par n'importe qui pour n'importe quel compte insolvable, opere tres differemment du `liquidationCall` atomique d'Aave ou des encheres hollandaises de MakerDAO. `absorbInternal` saisit d'un coup **tout** le collateral du compte liquide (remise a zero de chaque solde `userCollateral`), calcule sa valeur ponderee par un troisieme facteur (`liquidationFactor`, une remise supplementaire par rapport a `liquidateCollateralFactor`), puis rembourse la dette du compte directement **depuis les reserves du protocole** plutot que depuis les fonds de l'absorbeur.

Le compte liquide voit donc sa dette immediatement remise a zero (ou reduite au minimum) des l'appel a `absorb`, financee par les reserves ; le collateral saisi, lui, reste dans le contrat sous forme de reserves de collateral, sans etre vendu dans la meme transaction. C'est cette separation entre "eponger la dette maintenant" et "revendre le collateral plus tard" (chapitre 8) qui distingue le modele de Comet.

L'absorbeur ne touche aucun fonds directement lors de l'appel : le contrat comptabilise seulement des "points de liquidateur" (`LiquidatorPoints`, nombre d'absorptions, gaz approximatif depense) a titre indicatif pour la gouvernance, qui peut ensuite decider d'un mecanisme d'incitation externe.

[Chapitre suivant : buyCollateral, la revente des reserves saisies](08-buycollateral.md)
