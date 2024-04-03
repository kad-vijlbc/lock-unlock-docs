---
title: Conclusies en aanbevelingen
---
Lock-Unlock richt zich op [Linked Data](./federatieve-bevraging/linkeddata.md), voortbouwend op de
<a href="https://labs.kadaster.nl/cases/integralegebruiksoplossing" target="_blank">Integrale
Gebruiksoplossing (IGO)</a> en de <a href="https://labs.kadaster.nl/thema/Knowledge_graph"
target="_blank">Kadaster Knowledge Graph (KKG)</a> ontwikkeld door het Kadaster. Er zijn weinig
gestandaardiseerde mogelijkheden voor autorisatie van data in het Linked Data domein. Dit project is
een verkenning om de (on)mogelijkheden te onderzoeken en te testen.

## Conclusies

Hoewel het doel van dit project vooral lag op [autorisatie als Linked
Data](./autorisatie-als-linkeddata/index.md), is een deel van de aandacht ook gegaan naar
[federatieve bevraging](./federatieve-bevraging/index.md). Dat schetst namelijk de context waarin
[afscherming](./afscherming/index.md) zou moeten plaatsvinden. Uiteraard hebben we ook beproefd in
hoeverre autorisatie als Linked Data mogelijk en haalbaar is via prototype implementaties met 2 verschillende aanpakken. Over de voor- en na-delen van de 2 aanpkken hebben we apart een korte
[evaluatie](./autorisatie-als-linkeddata/evaluatie.md) geschreven. De conclusies volgen hier:

:warning: Zie ook [disclaimer](#disclaimer).

### Autorisatie als Linked Data

**<a id="afscherming-van-linked-data-is-mogelijk"
href="#afscherming-van-linked-data-is-mogelijk">Afschermen van Linked Data is mogelijk</a>**

Het is mogelijk om fijnmazig autorisatieregels declaratief te modelleren op basis van een
autorisatie ontologie voor federatieve bevragingen op basis van Linked Data. We hebben dit aan
kunnen tonen in onze [demonstrators](./autorisatie-als-linkeddata/demonstrators/index.md), waarin we
een eerste toepassing van een door ons ontwikkelde autorisatie ontologie hebben uitgewerkt. Hieruit blijkt dat het mogelijk is om een sparql-endpoint op te zetten die alleen informatie teruggeeft waarvoor je de benodigde rechten hebt.

**<a id="declaratieve-autorisatieregels-als-linked-data"
href="#declaratieve-autorisatieregels-als-linked-data">Declaratieve autorisatieregels als Linked
Data</a>**

Met _autorisatieregels_ doelen we op toegangsregels die gelden voor een specifieke situatie. Voor
een bepaalde gebruikersgroep wordt toegang verleend voor een specifiek data-schema, een specifieke
ontologie. De regels die gelden kunnen zeer fijnmazig zijn en de verschillende
[afschermingspatronen](./afscherming/afschermingspatronen.md) bevatten. We hebben in onze
demonstrators aangetoond dat [verticale en horizontale
subsets](./afscherming/afschermingspatronen.md#toegang-tot-een-subset) mogelijk zijn. Afscherming van een zoek [richting](./afscherming/afschermingspatronen.md#toegang-tot-data-in-een-bepaalde-richting) is helaas niet beproefd. Is het mogelijk? Wij denken van wel.

De autorisatieregels zijn _declaratief_. Dat betekent dat de gewenste toegang of juist afscherming
gespecificeerd kan worden. Onderliggende uitvoering en zelfs uitwerking wordt overgelaten aan een
'engine' die zorgdraagt voor de afscherming.

Dit houdt ook in dat autorisatieregels data is `#data-gedreven`. Dit betekent:

- dat de autorisatieregels kunnen worden bevraagd (wie heeft toegang tot wat en eventueel zelfs
  waarom (niet)). Wellicht is het mogelijk om te verwijzen t/m de wettelijke grondslag?
- dat de autorisatieregels kunnen worden opgesteld en gedefinieerd onafhankelijk van de software
  (engine) waarin de regels worden afgedwongen
- dat de autorisatieregels als _knowledge graph_ toegankelijk zijn
- dat de autorisatieregels opgesteld kunnen worden gebruikmakende van de Linked Data schema's

**<a id="autorisatie-ontologie-voor-standaardisatie"
href="#autorisatie-ontologie-voor-standaardisatie">Autorisatie ontologie voor standaardisatie</a>**

De autorisatieregels kunnen worden gestandaardiseerd in een _autorisatie ontologie_. Dat betekent
dat een software implementatie van deze ontologie als engine gebruikt kan worden om de data van de
autorisatieregels uit te voeren. Doordat een ontologie programeertaal onafhankelijk is, kunnen er
meerdere implementaties gemaakt worden voor de autorisatie ontologie.

**<a id="declaratieve-autorisatieregels-gekoppeld-aan-bestaande-ontologieen"
href="#declaratieve-autorisatieregels-gekoppeld-aan-bestaande-ontologieen">Declaratieve
autorisatieregels gekoppeld aan bestaande ontologieën</a>**

Het is mogelijk om in de declaratie van de autorisatieregels volgens de autorisatie ontologie, een
relatie te maken naar al bestaande ontologieën. Dat wil zeggen dat de toegang (of juist ontzegging
daarvan) gedeclareerd kan worden volgens de autorisatie ontologie en daarbij kan gedeclareerd worden
_over welke_ andere ontologie die regels gelden. In ons voorbeeld zijn dat de registratie
ontologieën van de BRK, BRP en NHR. De autorisatieregels zijn daarmee direct gekoppeld aan de
schema-elementen van deze register ontologieën.

Deze vorm biedt inzicht in wie waar toegang toe heeft of juist niet. Daarmee biedt het mogelijkheden
tot verificatie van de autorisaties (eventueel aan andere partijen, zoals een toezichtshouder).

### Conclusies van beproevingen

- het is mogelijk om gebruik te maken van de data om autorisatieregels op te stellen. Zo kan er
  bijvoorbeeld toegangsregels opgesteld worden voor een bepaalde gemeente. De daadwerkelijke
  gemeente wordt uit de dataset opgehaald.

- De ge-identificeerde afschermings patronen zijn generiek en bieden veel mogelijkheden tot
  afscherming via configuratie van deze patronen

- De PoC implementaties laten zien dat veel autorisatie patronen makkelijk implementeerbaar en
  haalbaar zijn. (Deze implementaties zijn niet bruikbaar voor productie en evt problemen mbt
  veiligheid en schaalbaarheid zijn niet onderzocht. Zie ook [disclaimer](#disclaimer).)

- Fictieve data van gekoppelde registers in Linked Data is makkelijk te realiseren. 

- Rewritten queries uit de [implementatie
  rewrite](./autorisatie-als-linkeddata/implementaties/rewrite.md) zijn complexer dan de orginele
  queries. Dat geeft extra belasting bij de uitvoering van de query. Daarom zijn optimale
  queryplannen noodzakelijk zijn om prestatie (performance) redenenen. Alleen triplestores met goede
  optimalisatie van queryplannen kunnen deze queries performant uitvoeren.

- Het afschermen van gegevens zo dicht mogelijk bij de triplestore biedt grotere zekerheid dan
  afscherming van gegevens door applicaties

- Bewijs dat de queries 'waterdicht' zijn is niet aanwezig in dit project noch was dit de
  doelstelling van de PoC implementaties. Zie ook aanbeveling [Volledigheid en effectiviteit
  meetbaar maken](#volledigheid-en-effectiviteit-meetbaar-maken)

### Federatieve bevraging

**<a id="linked-data-maakt-federatieve-bevraging-gemakkelijk"
href="#linked-data-maakt-federatieve-bevraging-gemakkelijk">Linked Data maakt federatieve bevraging
gemakkelijk</a>**

Een federatieve bevraging is op meerdere manier mogelijk. Een omgeving met REST API's biedt ook wel
de mogelijkheid voor federatieve bevragingen, maar dit legt een grote beheerlast bij de 'vrager'.
Met GraphQL zijn daar stappen in gemaakt, maar daarin is nog steeds behoefte aan gateway
oplossingen.

Linked Data is _ontworpen_ met federatie in de basis. Vanuit het ontwerp is federatieve bevraging
daarom al beschikbaar. In de Linked Data Query Language, SPARQL, is dit gespecificeerd met de
`service` clause. Daarmee is het relatief eenvoudig om een federatieve bevraging, een SPARQL query,
te schrijven die uitvoerbaar is. Daarmee is Linked Data van nature geschikt voor federatief
bevragen. In applicaties die ondersteuning hebben voor Linked Data en SPARQL is het eenvoudig om
rijke en federatieve functionaliteit te ontwikkelen.

**<a id="open-source-triples-stores-maken-testopstelling-gemakkelijk"
href="#open-source-triples-stores-maken-testopstelling-gemakkelijk">Open Source triplestores maken
testopstelling gemakkelijk</a>**

Door gebruik te maken van Open Source producten voor Linked Data databases, zogenaamde triplestores, is het opbouwen van een testopstelling relatief gemakkelijk. In onze cloud omgeving wordt
gebruik gemaakt van Cloud Native tools en daarvoor was nog geen standaard deployment script
beschikbaar. Tegelijk was het niet extreem moeilijk om, met kennis van zaken natuurlijk, deze te
ontwikkelen en gebruiken voor de testopstelling.

Open Source maakte het ook mogelijk om eigen implementaties te ontwikkelen tbv van [autorisatie als
Linked Data](#autorisatie-als-linked-data). Ons eigen werk is ook openbaar beschikbaar tbv verdere
ontwikkelingen, zie [opleveringen](./opleveringen.md).


**<a id="performance-van-federatieve-bevraging-varieert"
href="#performance-van-federatieve-bevraging-varieert">Performance van federatieve bevraging
varieert</a>**

Dat federatieve bevraging standaard in de Query Language zit en in de basis van Linked Data wil dat
niet zeggen dat er geen 'problemen' zijn. In concept is het al ingewikkeld om een generieke
werkwijze te bedenken die een query snel uitvoert. Daar is vrijwel altijd een analyse van de query
voor benodigd om uit te werken wat de snelste manier is om de vraag (query) te beantwoorden. Deze
analyse en uitwerking naar snelle uitvoering van federatieve vragen, is niet gestandaardiseerd in
SPARQL of Linked Data. In de verschillende implementaties van triplestores zijn hier grote
verschillen. In dit project is er gebruik gemaakt van een open-source triplestore waarbij query
performance achterloopt t.o.v. de commerciele toppers.

Er zijn wel ontwikkelingen rondom federatieve bevraging in het Linked Data domein. Zie ook
aanbeveling [Meer onderzoek naar performance federatieve bevragingen](#aanbevelingen)

**<a id="duurzame-koppeling-van-silos-vraagt-om-expliciet-ontwerp"
href="#duurzame-koppeling-van-silos-vraagt-om-expliciet-ontwerp">Duurzame koppeling van silo's
vraagt om een expliciet ontwerp</a>**

Impliciet zijn registers koppelbaar vanwege (impliciet) aanwezige koppelsleutels. In alle gevallen zullen sleutels tussen registers / silo's op
elkaar moeten passen. Linked Data biedt daar standaard al enige constructen voor om in een query
transformaties of iets dergelijks te doen. Dit is echter een punt oplossing en moet voor elke query
opnieuw toegepast worden.

Om duurzaam over silo's van data heen goed te kunnen navigeren en federatieve bevragingen te vergemakkelijken, dient minimaal dee data gekoppeld te zijn. Linked
Data biedt hiervoor verschillende mogelijkheden. Een mogelijkheid is bijvoorbeeld om een _upper ontology_ voor de
registers af te spreken. Door adoptie van deze upper-ontologie kunnen relaties tussen de informatie
modellen maar ook relaties tussen de datasets toe gevoegd worden. 

Zie ook [informatiekundige kern](./federatieve-bevraging/informatiekundigekern.md).

## Aanbevelingen

**<a id="linked-data-adoptie-vergroten" href="#linked-data-adoptie-vergroten">Linked Data adoptie
vergroten</a>**

Linked Data biedt veel mogelijkheden voor federatieve bevragingen, expliciete verplichting voor
semantiek, informatiemodellen en begrippen. En met de autorisatie ontologie komt ook afscherming in
de mogelijkheden van Linked Data. Het succes en toepassen van deze technieken staat of valt echter
met de adoptiegraad van Linked Data in het algemeen. Het vergroten van deze adoptie is daarom van
belang. Hierbij Kun je vragen stellen zoals wat is het minimum noodzakelijke voor een registerhouder
om data als Linked data te publiceren. Wat is de minimale infrastructuur hiervoor en hoe kan er snel
en robuust Linked Data gecreëerd worden.   

**<a id="autorisatie-ontologie-verder-uitwerken"
href="#autorisatie-ontologie-verder-uitwerken">Autorisatie ontologie verder uitwerken</a>**

De [Authorisation Ontology](./opleveringen.md#authorisation-ontology) waar in dit project in eerste
opzet van is gedaan, dient verder te worden uitgewerkt. Idealiter ontstaat er een geadopteerde standaard autorisatie ontologie. Dat betekent ook dat vendors van triple stores deze standaard
kunnen implementeren zodat het écht gaat werken. Federatief!

Het is daarin van belang dat ook [alternatieven](./achtergrond/auth-alternatieven.md) goed
geanalyseerd en overwogen worden. In dit onderzoek hebben we daar wel kennis van genomen, maar zijn
we te weinig toegekomen aan een 'in depth' vergelijking.

Voor de ontwikkeling zou een W3C Working Group uiteraard een mooi middel zijn!

**<a id="beperking-van-richting-uitwerken" href="#beperking-van-richting-uitwerken">Beperking van
richting uitwerken</a>**

In dit project hebben we uitgewerkt en beproefd hoe [verticale en horizontale
subsets](./afscherming/afschermingspatronen.md#toegang-tot-een-subset) afgeschermd of juist onsloten
kunnen worden. We hebben geen aandacht kunnen besteden aan het beperken van de
[richting](./afscherming/afschermingspatronen.md#toegang-tot-data-in-een-bepaalde-richting). Hier
dient extra (vervolg)onderzoek op gedaan te worden.

**<a id="volledigheid-en-effectiviteit-meetbaar-maken"
href="#volledigheid-en-effectiviteit-meetbaar-maken">Volledigheid en effectiviteit meetbaar
maken</a>**

In dit onderzoek is aangetoond dat het mogelijk is om mbv een autorisatie ontologie een 'secured
SPARQL endpoint' te ontwikkelen (twee zelfs! :grin:). We hebben echter niet aangetoond dat dit
volledig waterdichte toegangscontrole biedt. Sterker nog, we zijn niet eens toegekomen aan de
[richting](./afscherming/afschermingspatronen.md#richting) beperken.

Om (later) aan te tonen dat de autorisatie ontologie volledig is en effectief wordt toegepast voor
een 'secured SPARQL endpoint' is het noodzakelijk om een betrouwbare en herhaalbare meetmethode te
hebben. Hierin zullen de verschillende [afschermingspatronen](./afscherming/afschermingspatronen.md)
opgenomen moeten zijn en allerlei variaties en combinaties hierin.

**<a id="opvolging-organiseren-tbv-volledigheid-en-effectiviteit"
href="#opvolging-organiseren-tbv-volledigheid-en-effectiviteit">Opvolging organiseren tbv
volledigheid en effectiviteit</a>**

Verdere R&D bewijsvoering dat de implementatie waterdicht is. Eventueel in samenwerking met
academici voor wetenschappelijk fundament.

**<a id="meer-onderzoek-naar-performance-federatieve-bevraging"
href="#meer-onderzoek-naar-performance-federatieve-bevraging">Meer onderzoek naar performance
federatieve bevragingen</a>**

De performance van federatieve bevragingen is nog weinig onderzocht en er is waarschijnlijk veel
ruimte om dit te verbeteren. De voornaamste aspecten hierin zijn de schaalbaarheid en de
optimalisatie van de queries. Het gebruiken van [HDT-bestanden](https://www.rdfhdt.org/), en
specifiek de header-sectie, kan interessante mogelijkheden bieden hierin.

**<a id="informatiekundige-kern" href="#informatiekundige-kern">Informatiekundige kern</a>**

Relaties tussen registers en silo's zijn geen eenvoudig probleem. Daar zijn oplossingen voor nodig
en dienen expliciet ontworpen te worden. Daar horen afspraken bij om deze relatie te onthouden en
wie deze verantwoordelijkheid krijgt.

In technische zin is het mogelijk om de relaties meer nadruk en belang te geven. Een oplossing die
Linked Data daarvoor kan bieden is een _upper ontology_. Daarmee zouden relaties gestandaardiseerd
en geformaliseerd kunnen worden. Daarna zouden (gelijke) functionele zaken gestandardiseerd kunnen
worden. Denk aan "ID"'s en versie beheer en meta-data van registers in Linked Data.

**<a id="meer-onderzoek-naar-performance-van-de-afscherming"
href="#meer-onderzoek-naar-performance-van-de-afscherming">Meer onderzoek naar performance van de
afscherming</a>**

Naast de performance van Linked Data oplossing in het geheel, stelt de afscherming nieuwe en extra
complexiteit verhogende eisen en karakteristieken. Het verdient meer onderzoek naar de performance
van specifiek dit onderdeel.

**<a id="implementatie-doorontwikkelen" href="#implementatie-doorontwikkelen">Implementatie
doorontwikkelen</a>**

Een eerste aanzet en prototyping rondom
[implementaties](./autorisatie-als-linkeddata/implementaties/index.md) is gedaan, maar verdient meer
opvolging. Hierbij kan gedacht worden aan vervolgonderzoeken in samenwerking met vendors van
triplestores en/of academici.

## Disclaimer

Dit project is een onderzoeksproject. De [opleveringen](./opleveringen.md) die ontstaan zijn, zijn
van het niveau Research & Development. Goed ter inspiratie en vervolgonderzoek zeer geschikt. Voor
productie ... ongeschikt! :warning:

- :warning: [Authenticatie](./afscherming/autorisatie.md#subject) is uitgesloten van dit project en
  als gegeven beschouwd. Hier is echter ook nog veel in te kiezen en te onderzoeken!

- :warning: De [autorisatie ontologie](./opleveringen.md#autorisatie-ontologie) die opgeleverd is in
  dit project, is slechts een eerste prototype en voorbeeld! Dit is uitsluitend voor Research &
  Development doeleinden. Zie ook aanbeveling [autorisatie ontologie verder
  uitwerken](#autorisatie-ontologie-verder-uitwerken)

- :warning: De [implementaties](./autorisatie-als-linkeddata/implementaties/index.md) zijn nog niet
  bruikbaar voor productie en eventuele problemen mbt veiligheid en schaalbaarheid zijn niet
  onderzocht
