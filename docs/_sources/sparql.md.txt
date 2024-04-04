# Suche und SPARQL

## Volltextsuche

Eine Volltextsuche ist mit einer [grafischen Oberfläche](http://labeling.link/search) möglich.

Diese Oberfläche greift auf die API zurück, welche mit den Parametern Suchwort, Vokabular ID, lookup Feld prefLabel oder scopeNote und maximale Anzahl der Ergebnisse angesprochen werden kann:

`/api/v1/search/query=&vocab=&lookup=&maxhits=`

Die API gibt ein JSON zurück, das wie folgt aufgebaut ist:

```json
[{
	"id": "<itemid>",
	"uri": "<uri>",
	"prefLabels": [{
		"label": "<value>",
		"lang": "<languagecode>"
	}],
	"scopeNote": {
		"note": "<note>",
		"lang": "<languagecode>"
	},
	"vocab": {
		"label": "<title>",
		"lang": "<languagecode>",
		"uri": "<uri>"
	},
	"broaderTerms": [{
		"label": "<label>@<languagecode>",
		"uri": "<uri>"
	}],
	"narrrowerTerms": [{
		"label": "<label>@<languagecode>",
		"uri": "<uri>"
	}],
	"similarityNormalizedLevenshtein": {
		"label": "<double>",
		"scopeNote": "<double>"
	}
}]
```

## Autovervollständigung

In der API ist eine Autovervollständigung integrtiert die auf [jQuery-Autocomplete](https://github.com/devbridge/jQuery-Autocomplete) abgestimmt ist.

Diese ermöglicht eine realtime Suche für Begriffe, Vokabulare und Erstellern.

Das Ergebnis wird als JSON ausgegeben:

```json
{
	"query": "<querystring>",
	"suggestions": [{
		"data": "<uri>",
		"lang": "<languagecode> (optional)",
		"value": "<value>"
	}]
}
```

## SPARQL

### Namespaces

```sparql
PREFIX ls: <http://labeling.link/docs/ls/core#>
PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
PREFIX ls_lab: <http://labeling.link/item/concept/>
PREFIX ls_voc: <http://labeling.link/item/vocab/>
PREFIX ls_rev: <http://labeling.link/item/revision/>
PREFIX ls_age: <http://labeling.link/item/agent/>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX dc: <http://purl.org/dc/elements/1.1/>
PREFIX dct: <http://purl.org/dc/terms/>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX prov: <http://www.w3.org/ns/prov#>
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
```

### Beispiele

#### Veröffentlichte Begriffe, deren Ersteller, Vokabular und Vokabulartitel

```sparql
SELECT ?concept ?label ?creator ?vocab ?vocabtitle WHERE {
  ?concept a ls:Label.
  ?concept dct:creator ?creator.
  ?concept ls:thumbnail ?label .
  ?concept skos:inScheme ?vocab.
  ?vocab ls:hasReleaseType ls:Public.
  ?vocab dc:title ?vocabtitle.
} ORDER BY ASC(?label)
LIMIT 50
```
