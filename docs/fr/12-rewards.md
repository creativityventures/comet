# Chapitre 12 — CometRewards : distribuer des recompenses par indices de suivi

`CometRewards` est un contrat de recompenses separe du coeur du protocole : chaque deploiement Comet accumule en interne des indices de suivi (`trackingSupplyIndex`, `trackingBorrowIndex`, mis a jour dans `accrueInternal`, chapitre 3) qui representent des points accumules par les preteurs et emprunteurs au fil du temps, sans jamais transferer de jeton directement depuis le contrat principal.

`setRewardConfig`/`setRewardConfigWithMultiplier` associent un marche Comet donne a un jeton de recompense (typiquement COMP) et un multiplicateur de conversion entre l'echelle interne des indices de suivi et l'echelle du jeton distribue. `getRewardOwed` calcule, pour un compte, la difference entre son index de suivi personnel enregistre lors de sa derniere interaction et l'index global courant, convertie en montant de jeton du.

`claim`/`claimTo` accrue d'abord l'etat du compte sur le contrat Comet cible (pour que les indices de suivi soient a jour), puis transferent le montant du calcule depuis les reserves de `CometRewards` — un contrat que la gouvernance approvisionne separement (`withdrawToken` en sens inverse permet aussi de recuperer un exces). Ce decouplage total entre calcul des droits (dans Comet) et distribution effective (dans CometRewards) permet de changer le jeton de recompense ou son taux sans jamais toucher au contrat de marche lui-meme.

[Chapitre suivant : limites et perimetre](13-limites-et-perimetre.md)
