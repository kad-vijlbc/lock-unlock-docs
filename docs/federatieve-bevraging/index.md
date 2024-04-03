---
title: Federatieve Bevraging
---
In een federatief datastelsel wordt data beschikbaar gesteld vanuit diverse en gedistribueerde
bronnen. De toegevoegde waarde volgt wanneer deze bronnen in samenhang bevraagd kunnen worden. En,
sterker nog, wanneer deze geïntegreerde bevraging een eenvoudigere combinatie van gegevens
ondersteunt om voorheen moeilijke of ongrijpbare vragen te beantwoorden. Het opvragen van gegevens
die zijn opgeslagen in gedistribueerde bronnen noemen we 'federatieve bevraging'. 

'Federatieve bevraging' duidt op twee onderdelen, namelijk de _bevraging_ en het feit dat dat
_federatief_ plaatsvindt. We beschouwen dit vanuit een digitaal tijdperk en daarom betekent
'bevraging' een digitale of 'met computer' bevraging. Federatief geeft aan dat de informatie in
verschillende bronnen is opgeslagen en dat de bevraging deze informatie individueel benadert. Er is
geen centrale opslag van informatie. 

### Application Programming Interface 
Door de evolutie van de technologie heen wordt het bevragen van een computer systeem aangeduid met
een 'Application Programming Interface', afgekort een **API** (uitspraak 'ee-pie-ai' of 'aapie').

- In de huidige stand van de techniek wordt met API meestal een **REST API** bedoeld, hoewel er vele
  varianten van API's bestaan. 
- Er zijn echter ook andere API standaarden die gebaseerd zijn op deze internet protocollen en in
  opkomst zijn, zoals **GraphQL** en **SPARQL**. 

Het bestaan en de verschillen zijn relevant voor dit onderzoek en worden daarom beschreven op [API's
| REST vs GraphQL vs SPARQL](apis.md).

### Linked Data

Hoewel in de huidige perceptie van 'een API' een REST API wordt bedoeld, is het _federatief_
bevragen met behulp van REST API's nog niet zo eenvoudig. Daarom is in (de opdracht voor) het
Lock-Unlock project gekozen om uit te gaan van **[Linked Data](linkeddata.md)**. Dit is een
technologie die het koppelen van gegevens tussen gedistribueerde bronnen ondersteunt om een betere
navigatie door de gegevens heen, tussen de nodes in de gegevens, te ondersteunen. De bijbehorende
query taal is **SPARQL**. Daarmee is federatief bevragen inherent mogelijk!

### Leeswijzer
In dit hoofdstuk wordt eerst beschreven hoe de verschillende API's zich tot elkaar verhouden en
waarom we ons beperkt hebben tot de scope van Linked Data. Vervolgens beschrijven we hoe het
informatiemodel in elkaar zit en wat de relatie is tot de informatiekundige kern. Ook wordt
toegelicht hoe de testdata is gegenereerd. Zowel het informatiemodel als de testdata is
randvoorwaardelijk voor een goede testcasus en testopstelling. We sluiten af met conclusies rondom
federatieve bevraging.

- [REST vs GraphQL vs SPARQL](./apis.md)
- [Waarom Linked Data?](./linkeddata.md)
- [Informatiemodel](./informatiemodel.md)
- [Informatiekundigekern](./informatiekundigekern.md)
- [Testopstelling](./testopstelling.md)
- [Demonstrator](./demonstrator.md)
