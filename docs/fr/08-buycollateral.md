# Chapitre 8 — buyCollateral : la revente a rabais des reserves de collateral

Une fois du collateral saisi par `absorb` (chapitre 7), il reste inerte dans les reserves du protocole jusqu'a ce que quelqu'un appelle `buyCollateral` : n'importe qui peut alors echanger de l'actif de base contre ce collateral, a un prix legerement inferieur au prix de marche (la remise vient du `liquidationFactor` deja applique lors de l'absorption). L'appelant precise un `minAmount` de collateral attendu, une protection contre le glissement de prix si d'autres acheteurs passent avant lui dans le meme bloc.

Cette revente reconstitue les reserves en actif de base (celles-la memes qui ont servi a eponger la dette du compte liquide a l'etape precedente), fermant la boucle economique : les reserves financent l'absorption immediate, puis se reconstituent progressivement via la vente du collateral saisi a des acheteurs opportunistes attires par la remise.

`getReserves` calcule les reserves disponibles comme la difference entre le solde reel d'actif de base detenu par le contrat et le total actuellement du aux preteurs ; `buyCollateral` echoue si l'operation ferait passer les reserves sous zero, une protection qui empeche de vendre plus de collateral que ce que les reserves peuvent justifier.

[Chapitre suivant : CometExt, l enveloppe ERC20 et les signatures](09-cometext.md)
