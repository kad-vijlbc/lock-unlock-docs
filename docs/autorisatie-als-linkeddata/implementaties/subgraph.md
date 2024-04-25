---
title: Subgraph
---

De subgraph methode werkt door een voorselectie te maken op basis van de regels die van toepassing
zijn voor de betreffende gebruiker. Daarna wordt de query uitgevoerd op deze voorselectie, waardoor
het onmogelijk wordt om ongeauthoriseerde gegevens op te vragen. Net als de rewrite methode kan dit
geïmplementeerd worden als een transparant proxy endpoint.

In theorie is het mogelijk om één endpoint te maken dat data uit verschillende registers combineert,
echter vereist dit ook dat er een centraal autorisatiebeleid wordt geschreven voor deze
gecombineerde data. Om organisatorische en beleidsmatige redenen is het verstandiger om dit niet te
doen, en een endpoint per (basis)registratie te hanteren. Hierdoor houden registereigenaren de
mogelijkheid zelf een autorisatiebeleid op te stellen, terwijl de features van SPARQL het mogelijk
maken deze verschillende endpoints federatief te bevragen,

![Subgraph](../images/Subgraph.png)

Conceptueel werkt de subgraph methode als volgt:

1. De gebruiker stuurt een query en zijn autorisatiegegevens.
2. Het endpoint bepaalt welke autorisatieregels van toepassing zijn voor deze gebruiker.
3. Voor iedere regel wordt bepaald tot welke gegevens deze toegang verleent.
4. De toegankelijke gegevens van alle regels worden samengevoegd tot een subgraaf.
5. De ingestuurde query wordt uitgevoerd op deze subgraph.
6. De resultaten van de query worden teruggestuurd naar de gebruiker.
