---
title: Glossary
---

### Authenticatie

Om de gebruiker te herkennen is een authenticatie proces nodig. In dit project is de gehele
authenticatie overgeslagen en dus buiten scope. 

### Autorisatie

Autorisatie is het proces waarbij een gebruiker rechten (of privileges) verkrijgt. In dit project is
er afgeschermde data. Per gebruiker of rol kan de afscherming verschillen. Oftewel per rol of
gebruiker zijn de privileges tot data verschillend.

### Axioma

Een axioma is in (de wiskunde en) de logica een niet bewezen, maar als grondslag aanvaarde bewering
- bron <a href="https://nl.wikipedia.org/wiki/Axioma" target="_blank">wikipedia</a>.

### Dataset

Een collectie van bij elkaar horende gegevens. Dat kan bestaan uit een enkele tabel, maar ook uit
een verzameling tabellen uit een database.

Als een deel van een dataset geduid wordt, dan wordt vaak gesproken over een **subset**.

Dit is vooral jargon wanneer over databases gesproken wordt. In geval van [Linked
Data](#linked-data) wordt er meer gesproken over een [graph](#graph) of subgraph.

### Graph

In geval van [Linked Data](#linked-data) wordt data gezien als nodes met relaties. Het totaal aan
nodes en relaties vormen samen een graaf of graph (Engels). In de techniek wordt vooral de Engels
notatie gebruikt.

Je zou kunnen stellen dat een collectie van data voor een bepaalde context bij elkaar horend één
graph vormen. Dit lijkt op zoals er over [dataset](#dataset)s gesproken wordt. En vergelijkbaar met
een deel van een dataset, kan ook een deel van een graph aangeduid worden met **subgraph**.

Dit is vooral jargon wanneer de data [Linked Data](#linked-data) betreft. In geval van meer
traditionele vormen als REST API's en databases wordt over [dataset](#dataset)s gesproken.

### Inferentie

Inferentie gaat over het afleiden of gevolgtrekking van nieuwe kennis uit bestaande kennis en
[axioma](#axioma)'s. In Linked Data is dit een bekend begrip.

> Inference is the derivation of new knowledge from existing knowledge and axioms. In an RDF
> database, inference is used for deducing further knowledge based on existing RDF data and a formal
> set of inference rules. - bron: <a
> href="https://www.ontotext.com/knowledgehub/fundamentals/what-is-inference/"
> target="_blank">ontotext</a>.

### Linked Data

Linked data is manier om data te structureren en te verbinden over het web en maakt gebruik van
stanfaarden zoals URI's, RDF en ontologieen gedefinieerd in [RDF](#rdf) zoals RDFS, [OWL](#owl) en
[SHACL](#shacl). 

### Open Policy Agent

Open Policy Agent (OPA) is een open-source beleidsmotor voor toegangscontrole en beleidsautomatisering in softwaretoepassingen. Het maakt gebruik van de beleidstaal genaamd Rego om beleidsregels te definiëren en uit te voeren. Rego is ontworpen om leesbare en krachtige beleidsregels te maken. OPA integreert met verschillende services en applicaties en kan complexe beveiligings- en autorisatievereisten implementeren door Rego-beleidsregels te evalueren op basis van inputgegevens, waardoor wordt beslist of een actie al dan niet wordt toegestaan. Dit wordt vaak gebruikt in moderne IT-omgevingen voor flexibele en geautomatiseerde beleidsafdwinging.

- [Documentatie](https://www.openpolicyagent.org/)
- Policies in [Rego lang](https://www.openpolicyagent.org/docs/latest/policy-language/)

### OWL

OWL staat voor de Web Ontology Language en is een gestandardiseerde taal voor formaliseren van
ontologieen op basis van Linked Data.

### Privacy Enhancing Technologies (PETs)

PET is een verzamelnaam voor verschillende technieken die de afscherming van (persoons-)gegevens ondersteunen
PETs faciliteren dat analyses kunnen worden uitgevoerd zonder de onderliggende data in te zien, zo worden toepassingen mogelijk die anders onmogelijk zouden zijn. PETs zien wij dan ook niet als technieken die autorisaties inregelen voor het bevragen van specifieke data maar faciliteren voornamelijk analyses waarbij toegang tot de onderliggende data niet toegestaan/gewenst is.

| Voorbeelden: | |
|----|----|
|<ul><li>Zero knowledge proofs</li><li>Bloom filters</li><li>Differential Privacy</li><li>Synthetische data</li></ul> |<ul><li>Federated Learning</li><li>Multi Party Computation</li><li>Homomorphic Encryption</li></ul> |

**Zie ook:**

- [Wegzwijzer PETs van IBDS](https://realisatieibds.pleio.nl/groups/view/c23ab74c-adb4-424e-917d-773a37968efe/kenniscentrum-van-de-ibds/wiki/view/a2d325d4-0047-4967-8200-c4a29e392060/privacy-enhancing-technologies-pet)
- [PETs in de praktijk - VKA](https://www.vka.nl/wp-content/uploads/2023/04/VKA_whitepaper-PETs-in-de-praktijk.pdf)
- [TNO over PETs](https://www.tno.nl/en/digital/digital-innovations/data-sharing/privacy-enhancing-technologies/) 

### RDF

RDF staat voor Resource Description Framework. Het is een gestandardiseerd model voor het opslaan
van verwerkbare gegevens en biedt een zeer veel flexibiliteit mbt het structureren en beschrijven
van gegevens.

### SHACL

SHACL staat voor Shapes Constraint Language. Het is een W3C stdnaard voor het valideren van RDF data
volgens een Shacl model. Via Shacl kun je zogenaamde Shapes definieren die structuren beschrijven
van RDF data. Vervolgens kan RDF data getest worden of ze voldoen aan deze shapes. 

### SPARQL

Sparql is een querytaal voor het bevragen en manipuleren van [Linked Data](#linked-data) op basis
van de RDF standaard. Sparql biedt o.a. de mogelijkheid om complexe vragen te stellen aan Linked
Data waarbij er op zoek gegaan wordt naar 'oplossingen' die voldoen aan de vraag.

### SPARQL Endpoint

Een SPARQL endpoint is een REST API die [SPARQL](#sparql) queries kan uitvoeren. Het betreft hier
een W3C standaard. 

### Triplestore

Een triplestore is een database voor het opslaan en bevragen van [Linked Data](#linked-data) op
basis van de [RDF](#rdf) standaard. Vaak biedt een triplestore een [SPARQL
endpoint](#sparql-endpoint) aan.

### Uniform Resource Identifier 

Een reeks tekens die wordt gebruikt om een bron op een computernetwerk te identificeren, waarvan het bekendste type het webadres of een URL is.

### Upperontologie

Een upperontologie, of upper ontology (EN), is een ontologie welke algemene termen bevat of termen
die over meerdere domeinen bestaan. Andere woorden voor upperontologie zijn top-level ontologie,
uppermodel of foundation ontology.

> _In information science, an **upper ontology** (also known as a top-level ontology, upper model,
> or foundation ontology) is an ontology (in the sense used in information science) that consists of
> very general terms (such as "object", "property", "relation") that are common across all domains.
> An important function of an upper ontology is to support broad semantic interoperability among a
> large number of domain-specific ontologies by providing a common starting point for the
> formulation of definitions. Terms in the domain ontology are ranked under the terms in the upper
> ontology, e.g., the upper ontology classes are superclasses or supersets of all the classes in the
> domain ontologies._
> <br>
> bron: [wikipedia](https://en.wikipedia.org/wiki/Upper_ontology)
