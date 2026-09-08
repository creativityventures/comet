# Chapitre 6 — Deux facteurs de risque : isBorrowCollateralized et isLiquidatable

Comet distingue deux seuils de solvabilite par actif de collateral, exactement comme la paire LTV / seuil de liquidation d'Aave v3 : `borrowCollateralFactor`, plus strict, verifie par `isBorrowCollateralized` avant d'autoriser un nouvel emprunt ou un retrait qui en creerait un ; et `liquidateCollateralFactor`, plus permissif, verifie par `isLiquidatable` pour declencher une liquidation. L'ecart entre les deux constitue la marge de securite du compte.

Les deux fonctions partagent la meme structure : partir de la valeur en actif de base du principal (negative si emprunt), puis, pour chaque collateral effectivement detenu (via le bitmap `assetsIn`, sans boucler sur les actifs non utilises), ajouter sa valeur ponderee par le facteur pertinent. Des que la liquidite cumulee redevient positive, `isBorrowCollateralized` peut retourner vrai immediatement sans terminer la boucle — une optimisation de gaz qui exploite le fait qu'un compte tres sur-collateralise n'a pas besoin d'evaluer tous ses actifs pour prouver sa solvabilite.

Un compte dont le principal est positif ou nul (il ne doit rien) est toujours collateralise et jamais liquidable, quel que soit son collateral : ces deux fonctions retournent immediatement dans ce cas.

[Chapitre suivant : absorb, la liquidation par saisie totale](07-absorb.md)
