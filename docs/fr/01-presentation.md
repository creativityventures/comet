# Chapitre 1 — Presentation de Compound v3 (Comet)

Compound v3, nomme Comet dans le code, est un marche monetaire mono-actif : chaque deploiement du protocole ne fait tourner qu'un seul actif de base emprunte et fourni (par exemple USDC), entoure de plusieurs actifs de collateral qui ne servent qu'a garantir des emprunts, sans jamais generer de rendement de depot pour leurs deposants. C'est une rupture nette avec Compound v2, qui traitait chaque actif comme a la fois pretable et empruntable dans un pool de cTokens symetrique.

Cette specialisation simplifie radicalement les calculs de risque : il n'y a plus a raisonner sur des dizaines de paires d'actifs pretables entre eux, seulement sur la solvabilite d'un compte vis-a-vis d'un unique actif de base. Le nom "Comet" resume l'intention du protocole : un contrat monolithique et efficace ("efficient monolithic money market protocol", selon le commentaire NatSpec du contrat principal).

Ce parcours s'appuie sur le depot cloné a la date d'ecriture. Fichiers centraux : `contracts/CometWithExtendedAssetList.sol` (logique principale), `contracts/CometCore.sol` et `CometStorage.sol` (etat et calculs partages), `contracts/CometExt.sol` (enveloppe ERC20 du solde de base), `contracts/Configurator.sol` (parametrage), `contracts/CometRewards.sol` (recompenses), `contracts/AssetList.sol` / `AssetListFactory.sol` (liste d'actifs extensible).

Rien n'a ete installe, compile ni execute pour ecrire ces chapitres.

[Chapitre suivant : architecture du protocole](02-architecture.md)
