---
title: Informatiemodel
---
Om een federatieve bevraging te kunnen laten zien, is een testopstelling nodig en dus een
informatiemodel. Voor dit project hebben we gekozen voor een reële situatie maar wel in
vereenvoudigde vorm en, zoals al eerder benoemd, gebaseerd op [Linked Data](./linkeddata.md) en
Linked Data gedachte. Hiermee is het mogelijk om een realistische situatie na te bootsen waarin
informatie afgeschermd dient te worden. Aangezien het heel handig is om data in een context te
plaatsen (denk aan data schema's) is er binnen dit project een set van schema's ontwikkeld die de
registers nabootsen (versimpeld en fictief) en natuurlijk bijbehorende datasets. Deze pagina
beschrijft het maken van de schema's die relevant zijn voor dit project en de pagina [testopstelling
](./testopstelling.md) beschrijft het maken van de bijbehorende datasets. 

Onderdeel van de ontwikkeling van het informatiemodel en de testdata was het formaliseren van
relaties tussen databronnen. Deze formalisering van relaties is een voorbeeld van een implementatie
van een [informatiekundige kern](./informatiekundigekern.md). Omdat deze relaties worden
gedefinieerd tussen fictieve, vereenvoudigde databronnen die voor dit project zijn ontwikkeld,
kunnen er geen conclusies worden getrokken over de geschiktheid van dit informatiemodel voor het
Federatief Datastelsel en de informatiekundige kern in het algemeen. Dit informatiemodel laat alleen
zien hoe relaties in Linked Data geformaliseerd kunnen worden en hoe federatieve bevraging mogelijk
wordt gemaakt.

### Vereenvoudigd Conceptueel Model 

De eerste stap hiervoor is het maken van een conceptueel model om de benodigde gegevens voor ons
doel te modelleren. Om een logisch begin te maken, hebben we gekozen voor een situatie 'dicht bij
huis', bij het Kadaster: De Basisregistratie Kadaster, afgekort de **BRK**. 

Dit begint met het opnemen van percelen als object binnen een conceptueel model en vervolgens is het
eigendom vastgesteld via `Tenaamstellingen` aan personen. Met personen worden
`Rechtspersonen` bedoeld, wat een echt of 'natuurlijk' persoon kan zijn, maar ook een bedrijf. De
juridische term is `Natuurlijk Persoon` voor echte mensen, welke geregistreerd zijn in de
Basisregistratie Personen, afgekort met de **BRP**. Bedrijven zijn juridisch `Niet Natuurlijke
Personen` en deze zijn geregistreerd in het Nationaal Handelsregister, afgekort met **NHR**. Om de
casus nog wat breder te maken hebben we ook nog het **ANBI** register toegevoegd; het register van
de Belastingdienst waarin goede doelen staan die aangemerkt zijn als Algemeen Nut Beogende
Instellingen.

| ![Vereenvoudigd concetpueel model](images/vereenvoudigd-informatiemodel.png) |
| :--------------------------------------------------------------------------: |
|                  *Informatie Model IMX-Geo als Linked Data*                  |

Het vereenvoudigd conceptueel model zoals getoond in bovenstaande afbeelding is verder uitgewerkt in
Linked Data als een ontologie voor een Lock-Unlock informatiemodel gebaseerd op losstaande schema's.
Om de schema's en ontologie te modelleren is er gebruik gemaakt van de RDF/RDFS/OWL en SHACL
standaarden. 

### Losstaande schema's per silo

Voor elke silo is een schema gemaakt. Het betreft hier een (over)versimpeld schema dat grofweg de
kern van het register bevat met als doel Research & Development voor dit project te ondersteunen en
tevens demonstratie mogelijkheden. Het schema voor elke silo heeft een eigen namespace en is
relatief onafhankelijk gemodelleerd. Zo is voor Kadaster de <a
href="https://www.geonovum.nl/geo-standaarden/nen-3610-basismodel-voor-informatiemodellen"
target="_blank">NEN3610</a> een belangrijke
[upperontologie](../achtergrond/glossary.md#upperontologie) terwijl dit wellicht voor de BRP niet zo
hoeft te zijn. Op deze manier onstaat er een situatie dat elk register een eigen ontologie heeft op
basis van verschillende upperontologieën.

#### IMX-Geo Schema

Een openbare basis dataset is de Kadaster Knowledge Graph (KKG) welke gebruik maakt van het <a
href="https://www.geonovum.nl/geo-standaarden/imx-geo-semantisch-model-basis-en-kernregistraties"
target="_blank">IMX-Geo</a> schema. De KKG bevat data van gebouwen en percelen liggende in
registratieve ruimtes als Linked Data. Bijna alle gegevens zijn openbaar. De 'laatste koopsom' is
een uitzondering hierop. Het deel van het informatiemodel dat nodig is voor Lock-Unlock wordt
gevisualiseerd in de volgende afbeelding en is ook in <a
href="https://data.labs.kadaster.nl/lock-unlock/informatie-model/schema?f=http%3A%2F%2Fmodellen.geostandaarden.nl%2Fdef%2Fimx-geo%23"
target="_blank">dynamische viewer</a> te vinden.

| ![linked registers](images/schema-imx.png) |
| :----------------------------------------: |
| *Informatie Model IMX-Geo als Linked Data* |

IMX-Geo is vanuit Kadaster beschikbaargesteld in Linked Data en is grofweg voor het 'Kadaster
gedeelte' helemaal compleet aanwezig. Deze dataset is gebruikt in dit project.

#### BRK (Gesloten Deel) Schema

Een versimpeld model van de BRK is ontwikkeld in Linked Data voor dit project. Hieronder is een
screenshot van het model zichtbaar en het schema is ook in <a
href="https://data.labs.kadaster.nl/lock-unlock/informatie-model/schema?f=https%3A%2F%2Fdata.labs.kadaster.nl%2Flock-unlock%2Fbrk%2Fdef%2F"
target="_blank">dynamische viewer</a>.

| ![linked registers BRK](images/schema-brk2.png) |
| :---------------------------------------------: |
|          *BRK Schema als Linked Data*           |

#### NHR Schema

Een versimpeld model van de NHR is gemaakt. Inschrijvingen bevatten wat basisgegevens en zijn
gekoppeld aan de openbare Registratieve Ruimtes. Hieronder is een diagram van het NHR schema te zien
en deze is beschikbaar in een <a
href="https://data.labs.kadaster.nl/lock-unlock/informatie-model/schema?f=https%3A%2F%2Fdata.federatief.datastelsel.nl%2Flock-unlock%2Fnhr%2Fdef%2F"
target="_blank">dynamische viewer</a>.

| ![linked registers NHR](images/schema-nhr2.png) |
| :---------------------------------------------: |
|          *NHR Schema als Linked Data*           |

#### BRP Schema

Een versimpelde versie van het BRP register is gemodelleerd. Hieronder is een diagram van het BRP
schema te zien en deze is beschikbaar in een <a
href="https://data.labs.kadaster.nl/lock-unlock/informatie-model/schema?f=https%3A%2F%2Fdata.federatief.datastelsel.nl%2Flock-unlock%2Fbrp%2Fdef%2F"
target="_blank">dynaminsche viewer</a>.

| ![linked registers](images/schema-brp.png) |
| :----------------------------------------: |
|        *BRP Schema als Linked Data*        |

#### ANBI Schema

Hieronder is een diagram van het ANBI schema te zien. Deze sluit niet precies op het ANBI informatie
model zelf aan en is alleen voor dit project gemodelleerd. Een live versie van de schema is ook
beschikbaar in een <a
href="https://data.labs.kadaster.nl/lock-unlock/informatie-model/schema?f=https%3A%2F%2Fdata.federatief.datastelsel.nl%2Flock-unlock%2Fanbi%2Fdef%2F"
target="_blank">dynamische viewer</a>.


| ![linked registers](images/schema-anbi.png) |
| :-----------------------------------------: |
|        *BRP Schema als Linked Data*         |

### Samenhang creëren

De schema's en de data van de schema's zijn als silo's opgezet. Elk register publiceert zijn data en
de bijbehorende context (schema's) op een eigen triplestore. Om de verschillende schema's met elkaar
te verbinden worden twee relaties gedefinieerd tussen klassen die in de schema's zijn gedefinieerd,
`owl:sameAs` en een `ik:heeftUBO` relatie. In beide gevallen worden deze relaties gedefinieerd
tussen klassen die aanwezig zijn in de schema's en gematerialiseerd als relaties die
instantiegegevens met elkaar verbinden. Zie [optie 2 in informatiekundige
kern](informatiekundigekern.md#optie-2-gematerialiseerde-relaties) voor meer informatie over
gematerialiseerde relaties. 

#### `owl:sameAs`

Door middel van `owl:sameAs` relaties kunnen individuele nodes (_individual_) in Linked Data gelijk verklaard
worden over verschillende silo's heen. Oftewel een Linked Data resource (element) welke leeft in één
register wordt gelijk verklaard aan een andere resource dat zich bevindt in een ander register (zie
hieronder).

| ![linked registers](images/relatiesV1.png) |
| :----------------------------------------: |
|           *Netwerk van schemas*            |

Dit betekent dat alle gegevens van de twee gelijkgestelde resources gekopieerd kunnen worden. Stel
individual 'A' is gelijk (`owl:sameAs`) aan individual 'B' dan kunnen alle relaties en kenmerken
gekopieerd worden van 'A' naar 'B' en andersom. Hierdoor ontstaan netwerken van Linked Data over de
registers heen en kan er daadwerkelijk genavigeerd worden van het ene register naar het andere. Ook
SPARQL queries kunnen hier gebruik van maken om zoekopdrachten over meerdere registers  uit te
voeren. Ook in onze testopstelling maken we gebruik van `owl:sameAs` om relaties te leggen naar
andere registers zonder volledig afhankelijk te worden van deze registers. Dit is een natuurlijke
manier om de relaties te leggen. Er zijn meerdere manieren om registerdata te koppelen via Linked
Data.

**Voorbeeld: BRK naar BRP en NHR**

'Personen' uit de BRK kunnen gelijk verklaard worden met 'geregistreerde personen' uit de BRK of
'Inschrijvingen' uit de NHR (Zie diagram hieronder).

| ![linked registers](images/schema-brk.png) |
| :----------------------------------------: |
| *Relatie tussen BRK, BRP en NHR registers* |

Een `owl:sameAs` relatie kan gelegd worden wanneer je weet dat deze 2 individuals ook daadwerkelijk
gelijk zijn (refereert naar dezelfde persoon in de werkelijkheid). Vanuit Kadaster zal er
waarschijnlijk akte informatie gebruikt worden zoals voornamen, achternaam, geboortedatum,
geboorteplaats, etc. om de juiste persoon in de BRP te vinden. De eigen adminstratie (`BRK:Persoon`)
wordt dan gelijk verklaard met de gevonden (`BRP:GeregistreerdPersoon`). Ook voor relaties met de
NHR werkt dit vergelijkbaar. Akte informatie zal gebruikt worden om de juiste inschrijving te vinden
in de NHR om vervolgens weer de `owl:sameAs` relatie te leggen.

**Voorbeeld: ANBI naar NHR**

De ANBI dataset kan direct gekoppeld worden aan NHR Inschrijvingen (zie diagram hieronder).

| ![linked registers](images/schema-nhr-anbi.png) |
| :---------------------------------------------: |
|     *Relatie tussen ANBI en NHR registers*      |

#### `ik:heeftUBO`

De `ik:heeftUBO` relatie [(Ultimate Beneficial Owner)](https://www.kvk.nl/veilig-zakendoen/wat-is-een-ubo/) is specifiek gedefinieerd om de relatie tussen individuen in de NHR en de
BRP te ondersteunen. In dit geval was het niet voldoende om een `owl:sameAs` relatie in te voeren,
omdat er geen gedeelde identifier (zoals een BSN-nummer) aanwezig was en er dus op basis van deze
nieuwe relatie twee verschillende identificerende attributen aan elkaar gerelateerd moesten worden.
In de context van dit project werden geen [axioma](../achtergrond/glossary.md#axioma)'s
gedefinieerd, dus er is geen gevolgtrekking mogelijk op basis van de aanwezigheid van deze relatie,
maar dit zou indien nodig in toekomstige iteraties van het model kunnen worden geïntroduceerd.

**Voorbeeld: NHR naar BRP**

Net zoals de BRK linkt naar personen in de BRP kan ook de NHR direct verbonden worden met BRP
(Geregistreerde)Personen (zie diagram hieronder).

| ![linked registers](images/schema-nhr-brp.png) |
| :--------------------------------------------: |
|     *Relatie tussen NHR en BRP registers*      |

## Hét Informatiemodel voor Lock-Unlock

Door de `owl:sameAs` relatie (en bijbehorende [inferentie](../achtergrond/glossary.md#inferentie))
en `ik:heeftUBO` relatie ontstaat er een netwerk van samenhangende schema's. Dit kan als één schema
gepresenteerd worden. Op basis van de implementatie van dit model als Linked Data kunnen een aantal
conclusies en aanbeveilingen worden getrokken met betrekking tot de mogelijkheden om federatief
bevragingen te ondersteunen. Zie [conclusies en aanbeveilingen](../conclusies.md). 

Hieronder een screenshot van de visualisatie direct uit de data van de schema's. Deze visualisatie
is ook te bekijken via een <a
href="https://data.labs.kadaster.nl/lock-unlock/informatie-model/schema" target="_blank">dynamische
viewer</a>. In dit samengesteld model zijn verschillende kleuren gebruikt om de individuele silo's
(weer) te onderscheiden.

| ![linked registers](images/InformatieModel.png) |
| :---------------------------------------------: |
|     *Hèt Informatie Model voor Lock-Unlock*     |

Onze ervaring met het koppelen van deze schema's en de onderliggende gegevens bood ons de
mogelijkheden het ontwerp en de implementatie van een informatiekundige kern te verkennen op basis
van Linked Data technologieën. Dit onderzoeken we in de [volgende sectie
](./informatiekundigekern.md), waarbij we slechts één optie voor implementatie bieden. Er zou verder
onderzoek gedaan moeten worden naar andere methoden voor de introductie van de informatiekundige
kern.
