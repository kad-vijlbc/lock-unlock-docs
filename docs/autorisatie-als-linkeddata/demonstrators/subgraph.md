---
title: Subgraph
---
> TO DO: 
> 
> - gebruikers kunnen dit nu nog niet (volgens mij) testen omdat de demo niet live staat. Is het een
>   idee om dan ook output te laten zien in de screenshots?

Voor het Lock-Unlock project is ook een simpele demonstrator ontwikkeld voor de [Subgraph
implementatie](../implementaties/subgraph.md). Deze toont aan dat een autorisatie-beleid afgedwongen
kan worden op een SPARQL-endpoint zonder dat queries hier uitzonderlijk traag van worden. De
ervaringen die hiermee zijn opgedaan zijn deels verder geïntegreerd in de demonstrator. Verdere
conclusies en aanbevelingen worden besproken in het hoofdstuk [evaluatie](../evaluatie.md).

Hieronder worden een aantal voorbeelden gegeven van queries die wel/niet zijn toegestaan voor
specifieke gebruikers. Al deze queries kunnen uitgevoerd worden in de demonstrator op
<a href="https://subgraph.dst.test.cloud.kadaster.nl/" target="_blank">subgraph.dst.test.cloud.kadaster.nl</a>.
Verschillende registers kunnen aangeroepen worden door het endpoint als volgt aan te passen:

- ANBI: `https://subgraph.dst.test.cloud.kadaster.nl/anbi/sparql?persona=h_de_vries`
- BRK: `https://subgraph.dst.test.cloud.kadaster.nl/brk/sparql?persona=h_de_vries`
- BRP: `https://subgraph.dst.test.cloud.kadaster.nl/brp/sparql?persona=h_de_vries`
- NHR: `https://subgraph.dst.test.cloud.kadaster.nl/nhr/sparql?persona=h_de_vries`

## Algemene Bedrijfsgegevens

De algemene bedrijfsgegevens uit het NHR zijn openbaar beschikbaar, dus ook niet-geautoriseerde
gebruikers kunnen deze opvragen. Deze query zal dus resultaten geven ongeacht welke gebruiker deze
uitvoert. Echter is toegang tot de UBO-gegevens beperkt zodat deze enkel toegankelijk zijn in de
context van een politieonderzoek. De kolom `?ubo` zal dus leeg blijven tenzij de query wordt
uitgevoerd door _Ferdinand van As (een politiemedewerker)_.

```sparql
PREFIX nhr: <https://data.federatief.datastelsel.nl/lock-unlock/nhr/def/>

SELECT ?naam ?rechtsvorm ?kvkNr ?ubo WHERE {
  ?inschrijving a nhr:Inschrijving.
  OPTIONAL { ?inschrijving nhr:bedrijfsnaam ?naam. }
  OPTIONAL { ?inschrijving nhr:rechtsvorm ?rechtsvorm. }
  OPTIONAL { ?inschrijving nhr:kvkNummer ?kvkNr. }
  OPTIONAL { ?inschrijving nhr:heeftUBO ?ubo. }
} LIMIT 10
```

## Inwonersaantallen per Gemeente

Een van de doelen van Lock-Unlock is het ondersteunen van statistische queries waar de onderliggende
data afgeschermd moet blijven. Denk hierbij bijvoorbeeld aan het inwonersaantal van een of meerdere
gemeentes. Dit wordt met de onderstaande query gedemonstreerd. Om dit mogelijk te maken, zijn de
verblijfplaatsen van personen openbaar toegankelijk. Dit lijkt in eerste instantie misschien op
ongeautoriseerde datatoegang, maar gezien enkel de verblijfsplaats wordt ontsloten, is het niet
mogelijk de ideniteit van een individueel persoon te achterhalen. Dit blijft natuurlijk wel een punt
van aandacht wanneer een systeem als hier gedemonstreerd in productie wordt gebracht. Door
overlappende beveiligingsregels kan het onbedoeld toch mogelijk worden om de identiteit van personen
te achterhalen.

```sparql
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX brp: <https://data.federatief.datastelsel.nl/lock-unlock/brp/def/>

SELECT ?naam ?inwonersAantal WHERE {
  ?gemeente rdfs:label ?naam.
  {
    SELECT ?gemeente (COUNT(*) AS ?inwonersAantal) WHERE {
      ?persoon brp:heeftVerblijfsplaats ?gemeente.
    } GROUP BY ?gemeente
  }
} ORDER BY ?naam
```

## Inwoners van Zeewolde

Deze query lijkt heel erg op de vorige, en vraagt specifiek de inwoners van Zeewolde op. Echter
vraagt deze query ook wat de namen van de inwoners zijn, er is dus een zekere mate van autorisatie
nodig. In de demonstrator zijn er twee scenario's waarin de naam van een gebruiker mag worden
opgehaald. Dit mag gebeuren in de context van een politieonderzoek, via onze fictieve gebruiker
_Ferdinand van As_. Ook is het mogelijk voor ambtenaren om de inwoners van hun gemeente te bekijken.
Alleen _Marjolein van Groen (medewerker Gemeente Zeewolde)_ mag dit dus doen. Wanneer _Jeroen
Peerenboom (medewerker Gemeente Almere)_ dit zou proberen, krijgt hij geen resultaten. Zou de
gemeente-URI worden aangepast naar `brk-gem:25`, dan krijgt _Jeroen Peerenboom_ juist resultaten en
heeft _Marjolein van Groen_ geen toegang.

```sparql
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX brk-gem: <https://brk.basisregistraties.overheid.nl/brk2/id/kadastraleGemeente/>
PREFIX brp: <https://data.federatief.datastelsel.nl/lock-unlock/brp/def/>

SELECT * WHERE {
  ?persoon brp:heeftVerblijfsplaats brk-gem:1156;
           rdfs:label ?naam.
} LIMIT 10
```

## UBOs van Bedrijven

Een van de krachtigste mogelijkheden van SPARQL is het federatief bevragen van datasets. In de
onderstaande query koppelen we het NHR en de BRP om de naam en geboortedatum van de UBO van een
bedrijf te bepalen. Het gedeelte van de query wat uitgevoerd wordt aan de BRP-kant staat in het
`SERVICE`-blok, waar het persoons-URI wordt gebruikt om de naam en geboortedatum te bepalen.

```sparql
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX brp: <https://data.federatief.datastelsel.nl/lock-unlock/brp/def/>
PREFIX nhr: <https://data.federatief.datastelsel.nl/lock-unlock/nhr/def/>

SELECT * WHERE {
  ?bedrijf nhr:heeftUBO ?ubo.
  SERVICE <http://localhost:8080/brp/sparql?persona=f_van_as> {
      ?ubo rdfs:label ?naam;
           brp:geboortedatum ?geboortedatum.
	}
} LIMIT 10
```

## Autorisatie-beleid

Gezien het autorisatie-beleid ook wordt uitgedrukt als Linked Data, is het mogelijk deze te bevragen
via SPARQL. Met deze query worden alle beveiligingsregels getoond en voor welke gebruikers deze van
toepassing zijn.

```sparql
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX sse: <https://data.federatief.datastelsel.nl/lock-unlock/authorisation/model/def/>

SELECT (GROUP_CONCAT(?name; SEPARATOR=", ") AS ?personas) ?rule ?subject ?condition WHERE {
  ?rule a sse:AccessRule;
        sse:subject ?subject;
  	    sse:condition ?condition.
  ?persona sse:extends*/sse:has_rule ?rule;
  		   rdfs:label ?name.
} GROUP BY ?rule ?subject ?condition
```

## Logging

Om achteraf te inzage te hebben in wat gebruikers hebben opgevraagd, worden alle queries gelogd in
de triplestore. Deze data kan ook weer als linked data worden bevraagd. De onderstaande query geeft
een kleine inzage in de gelogde gegevens. In de demonstrator zijn deze gegevens openbaar
toegankelijk, maar in een productie-versie is het waarschijnlijk wenselijk om ook een
autorisatie-beleid af te dwingen op deze data.

```sparql
PREFIX log: <https://data.federatief.datastelsel.nl/lock-unlock/logging/model/def/>

SELECT ?timestamp ?user ?endpoint ?duration ?query WHERE {
  ?event log:startDate ?timestamp;
         log:by_user ?user;
         log:endpoint ?endpoint;
         log:processingtime ?duration;
         log:sparqlquery ?query.
} ORDER BY DESC(?timestamp) LIMIT 25
```
