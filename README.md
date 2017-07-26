# Experiments/thoughts for bibliotek-o/BIBFRAME to schema.org conversion

## Existing work

[Osma Suominen](https://github.com/osma) at the National Library of Finland has implemented a SPARQL `CONSTRUCT` to convert from BIBFRAME to schema.org as part of the [`bib-rdf-pipeline`](https://github.com/NatLibFi/bib-rdf-pipeline). See [`bf-to-schema.rq`](https://github.com/NatLibFi/bib-rdf-pipeline/blob/master/sparql/bf-to-schema.rq).

We can easily run this on our sample minimal record:

```
> sparql --data=data/102063-bf.ttl --query=vendor/bib-rdf-pipeline/bf-to-schema.rq 
@prefix schema: <http://schema.org/> .
@prefix rdau:  <http://rdaregistry.info/Elements/u/> .
@prefix bf:    <http://id.loc.gov/ontologies/bibframe/> .
@prefix madsrdf: <http://www.loc.gov/mads/rdf/v1#> .
@prefix bflc:  <http://id.loc.gov/ontologies/bflc/> .
@prefix rdf:   <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs:  <http://www.w3.org/2000/01/rdf-schema#> .

<http://example.org/102063#Instance>
        a                     bf:Instance , schema:CreativeWork ;
        schema:datePublished  "1957" ;
        schema:exampleOfWork  <http://example.org/102063#Work> ;
        schema:name           "Clinical cardiopulmonary physiology" .

<http://example.org/102063#Work>
        a                   bf:Work , schema:CreativeWork ;
        schema:inLanguage   "eng" ;
        schema:name         "Clinical cardiopulmonary physiology" ;
        schema:workExample  <http://example.org/102063#Instance> .
```

## Setup

### Apache Jena for command line SPARQL

On MacOSX

```
> brew install jena
```

which should then make `sparql` available (referred to as `arq.sparql` accessed via [`arq.query`](http://jena.apache.org/documentation/query/cmds.html#arqquery) in the Jena docs).

```
> sparql --version
Jena:       VERSION: 3.1.0
Jena:       BUILD_DATE: 2016-05-10T11:59:39+0000
ARQ:        VERSION: 3.1.0
ARQ:        BUILD_DATE: 2016-05-10T11:59:39+0000
RIOT:       VERSION: 3.1.0
RIOT:       BUILD_DATE: 2016-05-10T11:59:39+0000
```
