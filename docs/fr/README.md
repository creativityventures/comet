# Parcours francais de Compound v3 (Comet) — Pret et emprunt

Lecture commentee du marche monetaire mono-actif Compound v3 (Comet), en francais, un mecanisme par chapitre.
Aucun code n'a ete installe, compile ni execute : ce parcours est purement documentaire.

1. [Presentation de Compound v3 (Comet)](01-presentation.md)
2. [Architecture : proxy, actif de base unique et collateraux](02-architecture.md)
3. [CometStorage et le systeme d indices de principal](03-stockage.md)
4. [Le modele de taux a double pente (kink)](04-taux.md)
5. [supply, withdraw et le principal signe](05-supply-withdraw.md)
6. [Deux facteurs de risque : isBorrowCollateralized et isLiquidatable](06-collateralisation.md)
7. [absorb : la liquidation par saisie totale et remboursement par les reserves](07-absorb.md)
8. [buyCollateral : la revente a rabais des reserves de collateral](08-buycollateral.md)
9. [CometExt : l enveloppe ERC20 du solde de base et les autorisations par signature](09-cometext.md)
10. [Configurator : reconfigurer un protocole immuable par redeploiement](10-configurator.md)
11. [AssetList et AssetListFactory : etendre le nombre de collateraux](11-assetlist.md)
12. [CometRewards : distribuer des recompenses par indices de suivi](12-rewards.md)
13. [Limites connues et perimetre de ce parcours](13-limites-et-perimetre.md)
