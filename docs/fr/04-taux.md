# Chapitre 4 — Le modele de taux a double pente (kink)

`getSupplyRate` et `getBorrowRate` calculent un taux par seconde en fonction de l'utilisation courante de l'actif de base (`getUtilization`, le ratio emprunte sur fourni). En dessous d'un seuil `supplyKink`/`borrowKink`, le taux suit une pente basse (`InterestRateSlopeLow`) ; au-dela, une pente haute (`InterestRateSlopeHigh`) prend le relais pour dissuader une utilisation excessive et preserver la liquidite disponible aux preteurs qui souhaitent retirer.

C'est le meme modele a double pente que celui deja documente pour Aave v3 et Compound v2 (compte JulienKervarrec) : la aussi, deux comptes fixes (`InterestRateBase`) et deux pentes forment une fonction affine par morceaux de l'utilisation. La difference tient a l'unite : Comet exprime ses taux par seconde et non par annee, et ces taux sont geles dans l'implementation immuable plutot que modifiables via des parametres de reserve mutables.

`getUtilization` divise la valeur presente totale empruntee par la valeur presente totale fournie ; si personne n'a encore fourni l'actif de base, l'utilisation vaut zero par convention pour eviter une division par zero.

[Chapitre suivant : supply, withdraw et le principal signe](05-supply-withdraw.md)
