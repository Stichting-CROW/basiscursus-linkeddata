# CROW-Basiscursus Linked data: spiekbriefje

## Termen

<!-- Vergeet niet: Sort lines ascending -->

- **Blank node**: `[]` een node zonder URI-identifier
- **Literal**: een string, met een datatype. Standaarddatatype: `xsd:string`.
- **Namespace**: een gemeenschappelijke (gebruikelijk http-adres) prefix van een aantal URI’s.
- **Object**: derde positie in een Triple; een URI, een _Blank node_ of een _Literal_.
- **Predicaat**: tweede positie in een Triple; een URI.
- **Subject**: eerste positie in een Triple; een URI of een _Blank node_.
- **Triple**: de drieslag van Subject, Predicaat, Object.
- **Turtle**: serialisatie
- **URL, URI, IRI, URN**: Universal Resource Locator, ~ Identifier, International ~, Uniform Re-source Name.
- **LOD (Linked Open Data)**: een methode om gestructureerde data te publiceren zodat deze eenvoudig gekoppeld en hergebruikt kan worden.
- **KG (Knowledge Graph)**: een netwerk van entiteiten (objecten, gebeurtenissen, concepten) en hun onderlinge relaties, vaak gemodelleerd als RDF-triples.
- **RDF (Resource Description Framework)**: een standaardmodel voor datarepresentatie gebaseerd op triples (subject, predicaat, object).
- **RDF-schema (RDFS)**: een vocabulaire voor het definiëren van klassen, eigenschappen en hiërarchieën binnen RDF-data.
- **SPARQL**: een querytaal voor het opvragen en manipuleren van RDF-data.
- **Vocabulaire/Ontologie**: een formele beschrijving van klassen, eigenschappen en relaties binnen een bepaald domein.
- **Graph**: een verzameling van triples die samen een netwerk van verbonden data vormen.
- **IRI (Internationalized Resource Identifier)**: een algemene vorm van URI die ook niet-ASCII-tekens ondersteunt.
- **Predicate**: een eigenschap of relatie die het subject en object verbindt in een triple.
- **Resource**: elk ding dat kan worden geïdentificeerd met een URI of IRI.
- **Statement**: een enkele triple die een feit uitdrukt in RDF.
- **Class**: een categorie of type waar resources toe kunnen behoren, bijvoorbeeld `schema:Person`.
- **Datatype**: het type van een literal, zoals `xsd:string` of `xsd:date`.
- **Graph database**: een database die is geoptimaliseerd voor het opslaan en bevragen van grafen, zoals RDF-data.
- **Instance**: een individueel object dat behoort tot een bepaalde klasse.
- **Prefix**: een korte aanduiding voor een namespace, gebruikt om URI’s leesbaarder te maken.
- **Property**: een eigenschap of relatie die wordt gebruikt als predicaat in een triple.
- **Query**: een vraag aan een dataset, bijvoorbeeld met SPARQL.
- **Serialization**: de manier waarop RDF-data wordt opgeslagen of uitgewisseld, zoals Turtle of JSON-LD.
- **Shape**: een beschrijving van de structuur en validatie van RDF-data, bijvoorbeeld met SHACL.
- **SHACL (Shapes Constraint Language)**: een taal om regels en validaties op RDF-data te definiëren.

## Standaardvocabularia

Een selectie van veelgebruikte namespaces en de meest belangrijke definities uit die vocabularia.

- [`rdf:` RDF voor de basis](https://www.w3.org/TR/rdf-concepts/)
  - `rdf:type`,
    `rdf:value`,
    `rdf:Property`,
    `rdf:HTML`,
    `rdf:JSON`,
    `rdf:XMLLiteral`
- [`rdfs:` RDFS voor schema's](https://www.w3.org/TR/rdf-schema/)
  - `rdfs:domain`,
    `rdfs:range`,
    `rdfs:label`,
    `rdfs:subClassOf`,
    `rdfs:subPropertyOf`,
    `rdfs:Class`
- [`owl:` OWL voor geavanceerde ontologieën](https://www.w3.org/TR/owl-ref/)
  - `owl:Restriction`,
    `owl:allValuesOf`,
    `owl:someValuesOf`,
    `owl:ObjectProperty`,
    `owl:DatatypeProperty`,
    `owl:AnnotationProperty`
- [`sh:` SHACL voor validatie van gegevenssets](https://www.w3.org/TR/shacl/)
  - `sh:PropertyShape`,
    `sh:NodeShape`,
    `sh:minCount`
- [`dct:` DublinCore voor bibliotheekachtige metadatabeschrijvingen](http://purl.org/dc/terms/)
  - `dct:created`,
    `dct:author`
- [`sdo:` of `schema:` Schema.org voor een zeer uitgebreide basisontologie](https://schema.org/)
  - `sdo:Person`,
    `sdo:Car`,
    `sdo:hasPart`,
    `sdo:mainPageOf`
- [`skos:` SKOS voor vocabulaires](https://www.w3.org/TR/skos-reference/)
  - `skos:prefLabel`,
    `skos:Concept`,
    `skos:narrower`,
    `skos:broader`
- [`nen2660:` Gebouwde omgeving](https://w3id.org/nen2660/def)

## Syntax

Alle tripleserialisatieformaten drukken dezelfde triples uit, maar zijn handiger voor bijv. menselijke of computerverwerking of passen juist beter bij bestaande computersystemen.
De meest belangrijke serialisatieformaten zijn:

- **Turtle** (`.ttl`) of _Terse Triple Language_ is de meest menselijk-leesbare variant:

  ```ttl
  @prefix schema: <https://schema.org/> .

  <http://example.org#jdj> a schema:Person ;
    schema:name "Jan de Jong" .
  ```

- **N-Triples** (`.nt`) is de voor lineaire computerverwerking het eenvoudigst:

  ```nt
  <http://example.org#jdj> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <https://schema.org/Person> .
  <http://example.org#jdj> <https://schema.org/name> "Jan de Jong" .
  ```

- **JSON-LD** (`.json` of `.jsonld`) is handig voor systemen die al met JSON om kunnen gaan:

  ```json-ld
  [
    {
      "@id": "http://example.org#jdj",
      "@type": [
        "https://schema.org/Person"
      ],
      "https://schema.org/name": [
        {
          "@value": "Jan de Jong"
        }
      ]
    }
  ]
  ```

- **RDF/XML** (`.rdf`) is vooral handig voor systemen die al met XML om kunnen gaan; anders af te raden:
  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <rdf:RDF xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#" xmlns:schema="https://schema.org/">
    <rdf:Description rdf:about="http://example.org#jdj">
      <rdf:type rdf:resource="https://schema.org/Person"/>
      <schema:name>Jan de Jong</schema:name>
    </rdf:Description>
  </rdf:RDF>
  ```

Er zijn ook serialisatieformaten die quads uitdrukken:

| Triple      | Quad      | Opmerking                      |
|-------------|-----------|--------------------------------|
| [Turtle]    | [TriG]    | Menselijk leesbaar             |
| [N-Triples] | [N-Quads] | Uitgeschreven triples of quads |
| [JSON-LD]   | [JSON-LD] | JSON-gebaseerd                 |
| [RDF/XML]   | TriX      | XML-gebaseerd                  |

[RDF/XML]: https://www.w3.org/TR/rdf-syntax-grammar/
[TriG]: https://www.w3.org/TR/trig/
[Turtle]: https://www.w3.org/TR/turtle/
[JSON-LD]: https://www.w3.org/TR/json-ld/
[N-Quads]: https://www.w3.org/TR/n-quads/
[N-Triples]: https://www.w3.org/TR/n-triples/
