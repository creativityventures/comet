# Chapitre 5 — supply, withdraw et le principal signe

`supply`/`supplyTo`/`supplyFrom` acheminent tous vers `supplyInternal`, qui distingue en interne `supplyBase` (l'actif de base, qui modifie le principal et peut faire passer un compte d'emprunteur a preteur) de `supplyCollateral` (un actif de collateral, qui incremente simplement `userCollateral[account][asset].balance` et active le bit correspondant dans `assetsIn`).

`withdraw`/`withdrawTo`/`withdrawFrom` suivent le meme schema cote retrait, avec une verification cle : apres un retrait qui ferait passer le principal en base au-dessous de zero (donc un emprunt), `withdrawBase` exige que le compte reste `isBorrowCollateralized` (chapitre 6) avant de laisser l'operation aboutir.

`repayAndSupplyAmount` et `withdrawAndBorrowAmount` sont des fonctions utilitaires pures qui decomposent le changement de principal signe en montants distincts (rembourse/fourni, ou retire/emprunte) : comme un seul champ `principal` porte les deux etats, ces fonctions traduisent une variation de ce champ en operations comptables lisibles pour les evenements et les indices globaux `totalSupplyBase`/`totalBorrowBase`.

[Chapitre suivant : isBorrowCollateralized et isLiquidatable](06-collateralisation.md)
