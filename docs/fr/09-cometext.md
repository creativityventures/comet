# Chapitre 9 — CometExt : l enveloppe ERC20 du solde de base et les autorisations par signature

Le solde fourni en actif de base par un compte se comporte comme un jeton ERC20 (transferable, avec `name`/`symbol`/`decimals`/`balanceOf`/`allowance`), mais cette logique est deleguee a un contrat separe, `CometExt`, plutot qu'integree directement dans le contrat principal. `CometMainInterface` route les appels correspondants vers `extensionDelegate` par un `delegatecall`, une facon de garder le contrat principal sous la limite de taille de bytecode d'Ethereum tout en presentant une interface ERC20 complete a l'exterieur.

`CometExt` implemente egalement `allowBySig`, une autorisation hors chaine au format EIP-712 (domaine avec `name`, `version`, `chainId`, `verifyingContract`) qui permet a un compte de deleguer sa gestion (`allow`) a un gestionnaire sans transaction prealable, en fournissant simplement une signature ECDSA. La constante `MAX_VALID_ECDSA_S` impose la forme canonique de la signature (moitie basse de l'ordre de la courbe), une protection standard contre la malleabilite des signatures secp256k1.

Cette separation en deux contrats (logique principale immuable + extension ERC20 deleguee) permet aussi de faire evoluer l'enveloppe ERC20 independamment du coeur du protocole, tant que l'adresse `extensionDelegate` reste configurable par la gouvernance via `Configurator.setExtensionDelegate` (chapitre 10) — mais seulement lors d'un redeploiement complet, puisque `extensionDelegate` est lui aussi `immutable`.

[Chapitre suivant : Configurator et le redeploiement comme mecanisme de mise a jour](10-configurator.md)
