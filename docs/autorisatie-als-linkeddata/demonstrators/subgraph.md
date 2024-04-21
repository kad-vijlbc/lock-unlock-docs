---
title: Subgraph
---
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

Als deze query wordt uitgevoerd als ongeauthoriseerde gebruiker, zal het resultaat er als volgt uit zien.

| naam                     | rechtsvoorm | kvkNr     | ubo  |
| ------------------------ | ----------- | --------- | ---- |
| Noten Eenmanszaak        | Eenmanszaak | 44812469  |      |
| Duijndam VOF             | VOF         | 9945351   |      |
| Welten BV                | BV          | 100498427 |      |
| Langeveld BV             | BV          | 123274139 |      |
| Bouthoorn VOF            | VOF         | 112709985 |      |
| Schellekens NV           | NV          | 10272019  |      |
| Wessels VOF              | VOF         | 71071932  |      |
| Roeterdink Eenmanszaak   | Eenmanszaak | 13673037  |      |
| van Cruchten Eenmanszaak | Eenmanszaak | 53937500  |      |
| Alberti BV               | BV          | 42847358  |      |

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

| naam           | inwonersAantal |
| -------------- | -------------- |
| 's-Graveland   | 92             |
| 's-Gravendeel  | 103            |
| 's-Gravenhage  | 100            |
| 's-Gravenmoer  | 100            |
| 's-Gravenzande | 108            |
| ...                             |

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

| persoon                                                      | naam                     |
| ------------------------------------------------------------ | ------------------------ |
| `brp:geregistreerd-persoon/1d29a2b2-84fe-438e-8f62-64ac38a275e1` | Nathan Roersma           |
| `brp:geregistreerd-persoon/122d863a-2cc4-4596-b4ce-4ecb59fb511f` | Ellen Campfens           |
| `brp:geregistreerd-persoon/060fccb4-855d-4676-aa4d-59ac3f726b4e` | Dana Reuvekamp           |
| `brp:geregistreerd-persoon/e14ab059-00f2-472e-8d1e-8a0a9fc2b7ca` | Marijn Bakels            |
| `brp:geregistreerd-persoon/44ed4149-d41d-49ca-9740-a09b4137b9f7` | Alicia van Groeningen    |
| `brp:geregistreerd-persoon/2a31221d-3ae5-4e63-8584-ccd005232489` | Vincent van Melis        |
| `brp:geregistreerd-persoon/d4a3acdf-2513-41cd-aa80-6e07d8cb64af` | Franciscus van der Aalst |
| `brp:geregistreerd-persoon/a96cb8ce-911d-4553-95a5-e809ede262f9` | Cynthia Buitelaar        |
| `brp:geregistreerd-persoon/20dc12af-69be-46d8-9a59-405d3c6d2404` | Maaike Jellema           |
| `brp:geregistreerd-persoon/bca7aa84-9de4-4a35-adad-c413d867e8ef` | Daisy Reitsma            |



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

| bedrijf                                                 | ubo                                                          | naam                | geboortedatum |
| ------------------------------------------------------- | ------------------------------------------------------------ | ------------------- | ------------- |
| `nhr:inschrijving/35af1729-bb46-4394-b3a0-e2b8e8103f4e` | `brp:geregistreerd-persoon/9b335fdf-8197-4c32-873b-9390038f20e0` | Kevin Jordens       | 1967-06-25    |
| `nhr:inschrijving/ae17ce08-f7c8-4389-bc3e-1c9153d1aa1c` | `brp:geregistreerd-persoon/13de1f66-dce3-4bbf-b600-e3500d555474` | Jules van Gorkom    | 1984-08-19    |
| `nhr:inschrijving/3b41d2f1-11bf-4479-b374-679750425073` | `brp:geregistreerd-persoon/0c8f8ea5-0cb1-4bba-8ace-6079ccc57faa` | Marinus Zwiggelaar  | 1965-06-13    |
| `nhr:inschrijving/ff2776ca-af9d-4f1b-8a9c-5a2dfa84ed3b` | `brp:geregistreerd-persoon/b5c10e6e-9c06-4072-9d4e-78f2f603ad6f` | Julius van Gijzen   | 1987-11-01    |
| `nhr:inschrijving/41fa977a-0276-4c0b-a66e-22b27020d5a9` | `brp:geregistreerd-persoon/49e3bc54-f47a-499b-87af-663fb6863ba7` | Alexandra Giesberts | 1966-01-27    |
| `nhr:inschrijving/3235c199-abd3-46d4-a658-227c339712ac` | `brp:geregistreerd-persoon/d4ed5e54-d7a3-44cf-b7a0-a20fb98ec909` | Pepijn Mager        | 2002-09-12    |
| `nhr:inschrijving/08731853-fd78-4b41-b4a3-d9328d2c2aac` | `brp:geregistreerd-persoon/c4e4ccb1-2390-4005-9cc0-8a280973ce15` | Barbara Landkroon   | 1989-10-16    |
| `nhr:inschrijving/795b39a8-09d0-433d-8d18-765f8bf832cc` | `brp:geregistreerd-persoon/b632fa65-0708-40ea-b5d9-57b577b3a7d5` | Gerard van Casteren | 1961-10-12    |
| `nhr:inschrijving/dacb3a70-f9a0-4512-8b1b-f4f42d7631ba` | `brp:geregistreerd-persoon/921ad989-c2d7-4a4e-aaca-1b19c1141f8e` | Jos Engel           | 1993-03-04    |
| `nhr:inschrijving/e72ea78f-6eaa-4db6-84c9-71aa740d1f96` | `brp:geregistreerd-persoon/e27ce142-3aed-468d-96cf-60325a8ba757` | Roel Kloos          | 1963-06-20    |



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

| personas                                                     | rule                             | subject                                     | condition                                                    |
| ------------------------------------------------------------ | -------------------------------- | ------------------------------------------- | ------------------------------------------------------------ |
| Ferdinand van As                                             | `brp-auth:alle_gegevens`         | `?s ?p ?o`                                  |                                                              |
| Ferdinand van As, Henk de Vries, Marjolein Groen, Jessica Jansen, Jeroen Peerenboom | `brp-auth:gemeenteaanduidingen`  | `?node rdfs:label ?name`                    | `FILTER (strstarts(str(?node), 'https://brk.basisregistraties.overheid.nl/brk2/id/kadastraleGemeente/'))` |
| Jeroen Peerenboom                                            | `brp-auth:inwoners_almere`       | `?persoon ?predicate ?value.`               | `?persoon brp:heeftVerblijfsplaats brk:kadastraleGemeente/25.` |
| Marjolein Groen                                              | `brp-auth:inwoners_zeewolde`     | `?persoon ?predicate ?value.`               | `?persoon brp:heeftVerblijfsplaats brk:kadastraleGemeente/1156.` |
| Ferdinand van As, Henk de Vries, Marjolein Groen, Jessica Jansen, Jeroen Peerenboom | `brp-auth:statistische_gegevens` | `?persoon brp:heeftVerblijfsplaats ?plaats` |                                                              |


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

| timestamp         | user       | endpoint | duration | query                                                        |
| ----------------- | ---------- | -------- | -------- | ------------------------------------------------------------ |
| 2024-04-21T10:01Z | h_de_vries | brp      | 476      | `PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> [...]` |