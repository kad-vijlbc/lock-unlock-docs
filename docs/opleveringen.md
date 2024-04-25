---
title: Opleveringen
---
In het Lock-Unlock project zijn de volgende zaken ontwikkeld en opgeleverd.

## Autorisatie ontologie

Om het concept te kunnen beproeven hebben we in het Lock-Unlock project een initiële versie van een
_Autorisatie ontologie_ ontwikkeld. Deze is verre van definitief of geschikt voor een standaard ...
en tegelijk wél beproeft! Voor verder onderzoek kan deze als uitgangspunt dienen.

De Autorisatie ontologie is te downloaden uit de GitHub repository:
<br>[lock-unlock-docs/ontologies/Authorisation.ttl](https://github.com/kadaster-labs/lock-unlock-docs/blob/main/ontologies/Authorisation.ttl)
(`.ttl` formaat).

## Authenticatie ontologie

Hoewel authenticatie is uitgesloten van de scope van het Lock-Unlock project, is het wel een
randvoorwaarde voor de [testopstelling](./afscherming/autorisatie.md#subject). Daarom hebben we een
(minimale) _Authenticatie ontologie_ ontwikkeld.

De Authenticatie ontologie is te downloaden uit de GitHub repository:
<br>[lock-unlock-docs/ontologies/Authentication.ttl](https://github.com/kadaster-labs/lock-unlock-docs/blob/main/ontologies/Authentication.ttl)
(`.ttl` formaat).

## Logging ontologie

Ten behoeve van de [Query Auditing](./afscherming/oplossingsrichtingen.md#query-auditing) is er een
eerste begin gemaakt met het vastleggen van een _(Query) Logging ontologie_.

De Logging ontologie is te downloaden uit de GitHub repository:
<br>[lock-unlock-docs/ontologies/Logging.ttl](https://github.com/kadaster-labs/lock-unlock-docs/blob/main/ontologies/Logging.ttl)
(`.ttl` formaat).

## Secured SPARQL Endpoints

Er zijn twee verschillende [implementaties](./autorisatie-als-linkeddata/implementaties/index.md)
gerealiseerd. Beide hebben eigen karakteristieken en voor- en nadelen. Beide implementaties zijn
gepubliceerd onder een open source licentie:

- [Secured SPARQL Endpoint Sub
  Graph](https://github.com/kadaster-labs/secured-sparql-endpoint-subgraph) (based on Apache Jena &
  SpringBoot)
- [Secured SPARQL Endpoint Rewrite (SPARQL
  Query)](https://github.com/kadaster-labs/secured-sparql-endpoint-rewrite) (based on Fuseki)

## Testdata

Voor de [testopstelling](./federatieve-bevraging/testopstelling.md#testdata) is synthetische
testdata gegenereerd. Deze is te vinden onder een open source licentie:

- [Lock-Unlock Testdata](https://github.com/kadaster-labs/lock-unlock-testdata)

## Helm Charts

Tbv de [deployement](./federatieve-bevraging/testopstelling.md#deployment) zijn er Helm Charts
opgeleverd waarmee de implementaties gemakkelijk gedeployed (geïnstalleerd) kunnen worden. Ook deze
zijn onder een open source licentie gepubliceerd:

- [Lock-Unlock Helm Charts](https://github.com/kadaster-labs/lock-unlock-helm-charts)
