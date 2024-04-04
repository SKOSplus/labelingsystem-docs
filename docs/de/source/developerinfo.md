
# Entwickler FAQ

Diese Sektion enthält Informationen für Entwickler.

## Neuer Eintrag im Referenz-Thesaurus-Katalog

### Katalogeintrag hinzufügen

Zunächst muss in `v1.utils.retcat.RetcatItems` der Liste `retcatList` ein neues Item hinzugefügt werden. Dieses muss folgende Struktur und Informationen enthalten:

* name: Name des Thesaurus
* description: Kurzbeschreibung des Thesaurus
* queryURL: Weiterleitung auf /v1/retcat/query/{mustBeImplemented, z.B. RetCat-Typ}
* labelURL: Weiterleitung auf /v1/retcat/info/{mustBeImplemented, z.B. RetCat-Typ}
* prefix: Prefix der URIs, an dem der Thesaurus eindeutig erkennbar ist
* group: RetCat-Gruppe (/api/v1/retcat/info/groups; erweiterbar)
* type: RetCat-Typ (/api/v1/retcat/info/types; erweiterbar)
* language: Hauptsprache des Thesaurus  [/api/v1/languages; value]
* quality: RetCat-Qualität (/api/v1/retcat/info/qualities; erweiterbar)
* defaultValue: [true/false] (wird standardmäßig geladen?)

z.B. Getty AAT

```java
retcatList.add(new RetcatItem(
	"Getty AAT",
	"AAT is a structured vocabulary, [...]",
	"/v1/retcat/query/getty/aat",
	"/v1/retcat/info/getty",
	"//vocab.getty.edu",
	"common reference thesauri (CH)",
	"getty",
	"en",
	"high",
	true
));
```

### Methode zur Info-Anzeige einer URI hinzufügen

In `v1.rest.RetcatResource` muss eine neue GET-Methode mit dem Pfad `/info/{RetCat-Typ}` hinzugefügt werden. Die Methode muss mit der Namenskonvention `getInfo{RetCat-Typ}` benannt werden. Als Query-Parameter enthält diese Methode die URI als String `?uri=`. Rückgabewert dieser Methode ist ein JSON-Objekt mit folgender Struktur:

```json
{
	"uri": "URI der Ressource [erforderlich]",
	"label": "Haupt-Bezeichner der Resource [erforderlich]",
	"lang": "Sprache des Labels [optional]",
	"description": "Kurzbeschreibung [optional]",
	"broaderTerms ": [{
		"label": "Bezeichner des Broader-Terms  [optional]",
		"uri": "URI des Broader-Terms  [optional]"
	}],
	"narrowerTerms": [{
		"label": "Bezeichner des Narrower-Terms  [optional]",
		"uri": "URI des Narrower-Terms  [optional]"
	}],
	"scheme": "Name des Schemes [erforderlich]",
	"type": "RetCat-Typ aus RetCat Item [erforderlich]",
	"quality": "RetCat-Qualität aus RetCat Item [erforderlich]",
	"group": "RetCat-Gruppe aus RetCat Item [erforderlich]"
}
```

z.B. aus `/api/v1/retcat/info/getty?uri=http://vocab.getty.edu/aat/300250186`

```json
{
	"uri": "http://vocab.getty.edu/aat/300250186",
	"label": "Carassius auratus (species)",
	"lang": "en",
	"description": "Members of a species of ornamental [...]",
	"broaderTerms": [{
		"label": "Carassius (genus)",
		"uri": "http://vocab.getty.edu/aat/300310587"
	}],
	"narrowerTerms": [],
	"scheme": "Art and Architecture Thesaurus",
	"type": "getty",
	"quality": "high",
	"group": "common reference thesauri (CH)"
}
```

Gelöst wird dies in der Defaultstruktur über eine eigene Klasse `v1.utils.retcat.Retcat_{Name}` über eine Methode `info(String url)`, welche ein JSONObject der zuvor vorgestellten Struktur zurückgibt. In dieser Methode können HTTP-Requests zur URI oder zu einem SPARQL endpoint erfolgen, jenachdem was der Referenzthesaurus anbietet. Hier sollten implementierte APIs immer genutzt werden.

### Methode zur Suche in einem Thesaurus hinzufügen

In `v1.rest.RetcatResource` muss eine neue GET-Methode mit dem Pfad `/query/{RetCat-Typ}` hinzugefügt werden. Die Methode muss mit der Namenskonvention `getQueryResults{RECTCAT-TYP}` benannt werden. Als Query-Parameter enthält diese Methode den Such-String als `?query=`. Rückgabewert dieser Methode ist ein JSON-Array mit JSON-Objekten folgender Struktur:

```json
{
	"uri": "URI der Ressource [erforderlich]",
	"label": "Haupt-Bezeichner der Resource [erforderlich]",
	"lang": "Sprache des Labels [optional]",
	"description": "Kurzbeschreibung [optional]",
	"broaderTerms ": [{
		"label": "Bezeichner des Broader-Terms  [optional]",
		"uri": "URI des Broader-Terms  [optional]"
	}],
	"narrowerTerms": [{
		"label": "Bezeichner des Narrower-Terms  [optional]",
		"uri": "URI des Narrower-Terms  [optional]"
	}],
	"scheme": "Name des Schemes [erforderlich]",
	"type": "RetCat-Typ aus RetCat Item [erforderlich]",
	"quality": "RetCat-Qualität aus RetCat Item [erforderlich]",
	"group": "RetCat-Gruppe aus RetCat Item [erforderlich]",
	"creator": "Name des Erstellers, hier: Labeling System [optional]",
	"orcid": "ORCID des Erstellers, hier: Labeling System [optional]",
	"similarity": "Levenshtein-Distanz zwischen Suchwort und Label [erforderlich]"
}
```

z.B. aus `/api/v1/retcat/query/getty/aat?query=gold`

```json
[{
	"creator": "",
	"narrowerTerms": [],
	"scheme": "Art and Architecture Thesaurus",
	"description": "Members of a species [...]",
	"broaderTerms": [{
		"label": "Carassius (genus)",
		"uri": "http://vocab.getty.edu/aat/300310587"
	}],
	"orcid": "",
	"label": "Carassius auratus (species)",
	"lang": "en",
	"type": "getty",
	"uri": "http://vocab.getty.edu/aat/300250186",
	"group": "common reference thesauri (CH)",
	"quality": "high"
}, {
	"creator": "",
	"narrowerTerms": [],
	"scheme": "Art and Architecture Thesaurus",
	"description": "Towns where the principal industry [...] ",
	"broaderTerms": [{
		"label": "mining centers (inhabited places)",
		"uri": "http://vocab.getty.edu/aat/300387305"
	}],
	"orcid": "",
	"label": "gold towns",
	"lang": "en",
	"type": "getty",
	"uri": "http://vocab.getty.edu/aat/300387234",
	"group": "common reference thesauri (CH)",
	"quality": "high"
}]
```

Gelöst wird dies in der Defaultstruktur über eine eigene Klasse `v1.utils.retcat.Retcat_{Name}` über eine Methode `query(String searchword)`, welche eine Map<String,SuggestionItem> zurückgibt. In dieser Methode können HTTP-Requests zur einer API oder zu einem SPARQL endpoint erfolgen, jenachdem was der Referenzthesaurus anbietet. Jedes Ergebnis sollte in einem SuggestionItem gespeichert werden. Die Struktur ist gleich der Struktur aus info().

Die Methode `getQueryResults{RECTCAT-TYP}` muss ebenfalls eine Möglichkeit bieten, dass Suchergebnisse nur mittels Eingabe der URI erfolgen kann. Dies wird standardmäßig über den Prefix `uri:` im query-Parameter angekündigt. In diesem Fall wird einfach die info-Methode aufgerufen, z.B.

```java
// Auszug
JSONArray outArray = new JSONArray();
if (searchword.startsWith("uri:")) {
	outArray.add(Retcat_LabelingSystem.info(searchword.replace("uri:", "")));
} else {
	Map<String, SuggestionItem> autosuggests = Retcat_Archwort.query(searchword);
	outArray = fillOutputJSONforQuery(autosuggests);
}
```

### CSS-Klasse für neuen Typ im Client anlegen

Damit die Suchergebnisse richtig im Client angezeigt werden müssen neue CSS-Klassen angelegt werden. Dies passiert in `labelingsystem-client\app\styles\less\labsys.less` ab Zeile 271.
