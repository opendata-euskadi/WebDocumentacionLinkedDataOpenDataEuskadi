Linked Open Data
================

## Introduction

The main idea behind Open Data is to publish government data in the most interoperable and rich way, so that citizens and other institutions can build interesting applications and perform deep analyses. Linked Data offers a suitable technology to do so, through the so called Linked Open Data.

[![Five star Linked Open Data](img/5-star-steps.png)](http://5stardata.info)

The idea behind [Linked Data](https://www.w3.org/standards/semanticweb/data) is to publish data directly on the Web, using current technologies, with standards like RDF, OWL, and SPARQL. In order for such data to be useful, it must be identified with URIs, accesible through HTTP, and most importantly, linked to other Linked Data resources, to be a part of the Linked Open Data Cloud.

[![Linked Open Data cloud](img/lod.png)](http://lod-cloud.net/versions/2017-08-22/lod.png)

By publishing Linked Data, agents (humans or programs) can browser through links, like web browsing, and can perform interesting queries on combined data, since all the data is combined through links on the web.

In Open Data Euskadi, we have chosen data from different sources (Open Data Euskadi catalog, Legegunea, web content, etc.) and we have converted it to Linked Data. This documentation is provided to make the consumption of such data easier to developers, citisens, journalists, etc.

## URI policy

In Linked Data, resources are identified by URIs. This means that URIs should be persistent and well defined (See bellow for the best practices we tried to follow). We have followed the [NTI](https://www.boe.es/diario_boe/txt.php?id=BOE-A-2013-2380) scheme for URIs, with a caveat: instead of using the word "recurso", we are using the word "id" (Yes, we do know that a URI bears no semantics and therefore "recurso" is as good as any word, but we live in a community with two official languages and we think we should not favour one for the URIs). Therefore, you can expect the URIs at Open Data Euskadi to follow the pattern `http://{lang}.euskadi.eus/id/{sector}/{domain}/{ClassName}/{Identifier}`, where:

* `lang`: the language of the resource, one of `eu` (basque) or `es` (spanish). Open Data euskadi follows the architecture of the DBpedia, in which datasets that pertain to different languages are stored in completely different servers.
* `sector`: one of the sectors provided by the NTI (e.g. `environment`).
* `domain`: the realm to which the resource belongs, defined by Open Data Euskadi (e.g. `air-quality`).
* `ClassName`: the name of the class of which this resource is an instance. In other words, the name of the resource at the other end of the `rdf:type` predicate (e.g. ``observation`, from `http://purl.org/linked-data/cube#Observation`).
* `Identifier`: a unique identifier, generated from the original data (e.g. `AV-GASTEIZ-2017-01-26`).

So a real URI, identifying an observation of air quality that follows the [Data Cube](https://www.w3.org/TR/vocab-data-cube/) model, looks like: `<http://es.euskadi.eus/id/environment/air-quality/observation/AV-GASTEIZ-2017-01-26>`.

URIs ELI?

## Content negotiation

An important notion of Linked Data is that a URI identifies a resource (Iñigo Urkullu), but a resource can have different representations of the same content (An HTML page describing Iñigo Urkullu, RDF data describing Iñigo Urkullu, etc.). [Content negotiation](https://tools.ietf.org/html/rfc7231#section-3.4) is the process by which the server provides the appropriate representation for each client, according to the MIME type of the `Accept` header that the client provides (`text/html` for a web browser, `application/rdf+xml` for an RDF agent, etc.). The Content Negotiation at Open Data Euskadi is designed in the same way as in DBPedia. There is a URI with the token `resource` (`id` in our case), and the content negotiation process redirects the client with HTTP 303 codes to the appropriate URLs containing representations (`page` or `data` URLs). In the case of Open Data Euskadi there is an additional consideration since there are two types of pages: pages that represent only data (`doc`) and pages that represent web content that was transposed to RDF (`page`) (See Web content bellow). 

![Content negotiation at Open Data Euskadi](img/content-negotiation.PNG)

The list of supported MIME types can be found at the [Blazegraph REST API documentation](https://wiki.blazegraph.com/wiki/index.php/REST_API#MIME_Types).

## Relation between Open Data Euskadi datasets and Named Graphs in the Triple Store

Datasets: http://es.euskadi.eus/sparql?query=

## Relation between Web content and Named Graphs in the Triple Store
JSON-LD

## To know more

### Specifications, standards, and general purpose vocabularies

* URI (Uniform Resource Identifier): https://tools.ietf.org/html/rfc3986
* RDF (Resource Description Framework): https://www.w3.org/TR/rdf11-primer/
* OWL (Web Ontology Language): https://www.w3.org/TR/owl2-primer/
* SPARQL (SPARQL Protocol and RDF Query Language): https://www.w3.org/TR/sparql11-query/
* SHACL (Shapes Constraint Language): https://www.w3.org/TR/shacl/
* SKOS (Simple Knowledge Organization System): https://www.w3.org/TR/2009/NOTE-skos-primer-20090818/
* DCAT:
* VOID:
* PROV:
* JSON-LD
* Schema:

### Tools

* ELDA
* Yasgui
* Blazegraph
* RDF4J
* Jena
* FAIRifier/OpenRefine
* Silk
* Protégé
* LODE (http://www.essepuntato.it/lode)

### Linked Open Data projects

* [Biblioteca Nacional de España](http://www.bne.es/es/Inicio/Perfiles/Bibliotecarios/DatosEnlazados/index.html)
* [Aragón Open Data](https://opendata.aragon.es/aragopedia/)
* [Ordnance Survey Linked Data Platform](http://data.ordnancesurvey.co.uk/)
* [Scotland statistics](http://statistics.gov.scot/)
* [Office for National Statistics Geography Linked Data](http://statistics.data.gov.uk/)
* [Statistical Linked Open Data of Japan](http://data.e-stat.go.jp/lodw/en)
* [British National Library](http://bnb.data.bl.uk/)
* [Wikidata](https://www.wikidata.org/)
* [DBpedia](http://wiki.dbpedia.org/)
* [GeoNames](http://www.geonames.org/)
* [European Legislation Identifier](http://eur-lex.europa.eu/eli-register/about.html)

### Interesting articles and posts

* [JSON-LD and why I hate the Semantic Web](http://manu.sporny.org/2014/json-ld-origins-2/)
* https://www.w3.org/2001/tag/issues.html#httpRange-14
* http://richard.cyganiak.de/blog/2008/03/what-is-your-rdf-browsers-accept-header/
* https://httpd.apache.org/docs/trunk/content-negotiation.html#better
* http://httpd.apache.org/docs/current/content-negotiation.html
* http://docs.rdf4j.org/rest-api/#_content_types
* https://www.w3.org/TR/webarch/
* https://developer.mozilla.org/en-US/docs/Web/HTTP/Content_negotiation/List_of_default_Accept_values#Values_for_an_image
* https://www.w3.org/Consortium/Persistence
* https://www.w3.org/blog/2006/02/content-negotiation/

### Books

### Linked Data Best Practices

* NTI (https://www.boe.es/diario_boe/txt.php?id=BOE-A-2013-2380)
* Linking Open Government Data (https://logd.tw.rpi.edu/instance-hub-uri-design)
* Designing URI Sets for the UK Public Sector (https://www.gov.uk/government/publications/designing-uri-sets-for-the-uk-public-sector)
* Creating URIs (https://data.gov.uk/resources/uris)
* Data On the Web Best Practices (https://www.w3.org/TR/dwbp/)
* Study on Persistent URIs (http://philarcher.org/diary/2013/uripersistence/)
* Cool URIs for the Semantic Web (https://www.w3.org/TR/cooluris/)
* Cool URIs don’t change (https://www.w3.org/Provider/Style/URI.html)
* Linking Government data (http://www.springer.com/us/book/9781461417668)
* Linked Data – Evolving the Web into a global Data Space (http://linkeddatabook.com/editions/1.0/)
* Linked Data – Structured data on the Web (https://www.amazon.com/Linked-Data-Structured-Web/dp/1617290394)
* Best practices for Publishing Linked Data (https://www.w3.org/TR/ld-bp/)
* Best Practice Recipes for Publishing RDF Vocabularies (https://www.w3.org/TR/swbp-vocab-pub)



