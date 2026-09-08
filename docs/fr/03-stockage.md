# Chapitre 3 — CometStorage et le systeme d indices de principal

Comet ne stocke pas directement le solde en actif de base de chaque compte : il stocke un `principal`, une valeur figee au moment du dernier mouvement, et deux indices globaux (`baseSupplyIndex`, `baseBorrowIndex`) qui croissent avec le temps pour representer l'interet accumule — exactement le meme principe que les indices normalise d'Aave v3 (chapitre deja documente pour ce compte), mais applique a un unique actif plutot qu'a chaque reserve.

`presentValueSupply` et `presentValueBorrow` (dans `CometCore.sol`) convertissent un principal en solde reel courant en le multipliant par l'indice correspondant ; `principalValue` fait l'inverse. Comme le principal est signe, un meme champ `UserBasic.principal` represente indifferemment un solde prete (positif) ou emprunte (negatif), ce qui evite de dupliquer la comptabilite entre les deux etats.

`accrueInternal`, appelee au debut de chaque fonction qui modifie l'etat, met a jour les deux indices en fonction du temps ecoule et des taux courants (chapitre 4), avant que la fonction n'agisse sur les soldes. Elle met egalement a jour des indices de suivi separes (`trackingSupplyIndex`, `trackingBorrowIndex`) utilises uniquement pour le calcul des recompenses (chapitre 12), decouples de l'accumulation d'interet elle-meme.

[Chapitre suivant : le modele de taux a double pente](04-taux.md)
