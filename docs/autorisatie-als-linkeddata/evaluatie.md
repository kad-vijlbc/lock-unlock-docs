---
title: Evaluatie
---
Beide besproken methodes hebben natuurlijk sterke en zwakke punten. In dit hoofdstuk proberen we
hier een overzicht van te geven. Er was te weinig tijd beschikbaar om uitgebreide vergelijkingen te
doen tussen beide implementatie strategieën en dat verdient dan ook meer aandacht in
vervolgonderzoeken; zie [aanbevelingen: implementaties
doorontwikkelen](../conclusies.md#implementaties-doorontwikkelen).

Zie verder ook de [conclusies van de beproevingen](../conclusies.md#conclusies-van-beproevingen).

### Subgraph

- Een autorisatiebeleid is eenvoudig te valideren met de subgraaf methode. Doordat er een complete
  subgraaf gemaakt wordt van de toegankelijke informatie, is deze ook te exporteren en analyseren.

- Om optimaal gebruik te maken van de subgraaf-methode, moeten de subgraven gecached worden. Dit kan
  significante hoeveelheden RAM of schijfruimte kosten. Een alternatief is om de subgraven pas te
  bepalen zodra een query wordt geëvalueerd, maar hierdoor wordt juist het query-process significant
  langzamer.

- Bij iedere verandering van de onderliggende data moeten de _cached_ subgraven opnieuw gegenereerd
  worden. Bij frequent veranderende data kan dit te veel tijd gaan kosten

- Met de subgraaf-methode is het niet mogelijk om bewerkingen aan de onderliggende graaf te
  ondersteunen.

### Rewrite

- Het rewriten van een query is een complex process waarbij makkelijk een fout gemaakt kan worden,
  waardoor mogelijk meer gegevens beschikbaar worden gesteld dan bedoeld.

- De rewrite methode kan toegepast worden voor het autoriseren van bewerkingen op de onderliggende
  graaf.
