# Labeling System vs. SKOS

Die Modellierung des Labeling system orient sich am Simple Knowledge Organization System, kurz SKOS. SKOS ist eine auf RDF und RDFs basierende formale Sprache zur Kodierung von Dokumentationssprachen wie Thesauri, Klassifikationen oder  kontrollierten Vokabularen. SKOS soll eine einfache Veröffentlichung und Kombination kontrollierter, strukturierter und maschinenlesbarer Vokabulare für das Semantische Web ermöglichen.

## Haupt-Komponenten

Das Datenmodell des Labeling System zeichnet sich inbesondere durch seine zwei Haupt-Komponenten aus: `Vokabular` und `Begriff`.

Ein `Vokabular` ist eindeutig durch eine URI addressiert und definiert durch eine Hauptsprache, einen Titel und eine Beschreibung.

Ein `Vokabular` enthält mehrere `Begriffe`.

Ein `Begriff` ist eindeutig durch eine URI addressiert und definiert durch einen Bezeichner (label) in der Sprache des Vokabulars, eine Beschreibung in der Sprache des Vokabulars, Übersetzungen (je eine pro Sprache) und Assoziationen, Ähnlichkeiten, Übereinstimmungen, Hierarchien und Links zu Referenz-Thesauri, anderen Konzepten bzw. zum Internet Archive.

## Wie unterscheidet sich das Labeling System von SKOS?

SKOS hät eine Reihe von Klassen und Properties bereit. Im folgenden wird aufgezeigt, welche Klassen und Properties unterstützt werden, wie diese im Vergleich zu SKOS im Labeling System definiert werden und welche zusätzlichen Klassen und Properties in der Labeling System Ontologie verwendet werden.

Folgende Aussagen werden im Vergleich zur [SKOS Referenz 18 August 2009 Recommendation Edition](https://www.w3.org/2009/08/skos-reference/skos.html) getätigt mit dem Präfix `skos:http://www.w3.org/2004/02/skos/core#`

**Klassen**

Unterstützt werden (mit spezieller Bedeutung):

`skos:ConceptScheme` `skos:Concept`

Nicht unterstützt werden:

`skos:Collection` `skos:OrderedCollection`

**Properties**

Unterstützt werden (mit spezieller Bedeutung):

*Relationen*

* `skos:broader`
* `skos:broadMatch`
* `skos:narrower`
* `skos:narrowMatch`
* `skos:related`
* `skos:relatedMatch`
* `skos:closeMatch`
* `skos:exactMatch`

*Deskriptive Beschreibungen*

* `skos:prefLabel`
* `skos:scopeNote`

*Zugehörigkeit und Änderungsverfolgung*

* `skos:changeNote`
* `skos:inScheme`

Nicht unterstützt werden:

`skos:altLabel` `skos:broaderTransitive` `skos:definition` `skos:editorialNote` `skos:example` `skos:hasTopConcept` `skos:hiddenLabel` `skos:historyNote` `skos:mappingRelation` `skos:member` `skos:memberList` `skos:narrowerTransitive` `skos:notation` `skos:note` `skos:semanticRelation` `skos:topConceptOf`

Die Struktur im Labeling System und die Haupt-Komponenten `Vokabular` und `Begriff` sind stark an `skos:ConceptScheme` und `skos:Concept` angelehnt. Sie beinhalten allerdings Besonderheiten, die im Folgenden erläutert werden.

## Vokabular vs. skos:ConceptScheme

In der [SKOS Referenz](https://www.w3.org/TR/skos-reference/#schemes) wird ein skos:ConceptScheme definiert:

*"A SKOS concept scheme can be viewed as an aggregation of one or more SKOS concepts. Semantic relationships (links) between those concepts may also be viewed as part of a concept scheme. This definition is, however, meant to be suggestive rather than restrictive, and there is some flexibility in the formal data model stated below. The notion of a concept scheme is useful when dealing with data from an unknown source, and when dealing with data that describes two or more different knowledge organization systems. Thesauri, classification schemes, subject heading lists, taxonomies, 'folksonomies', and other types of controlled vocabulary are all examples of concept schemes. Concept schemes are also embedded in glossaries and terminologies.""*

`ConceptScheme` sind abstrakte Container von `Concepts`. Sie besitzen nativ weder Titel, Beschreibungen, Sprachvorgaben bzw. weitere Metadaten. Einzig mögliche Strukturen sind sogenannte Hierarchien und TopConcepts, welche die höchsten Knotenpunkte in einem Hierarchiebaum darstellen.

Ein `Vokabular` wird eindeutig durch eine Hauptsprache definiert und durch einen Titel und eine Beschreibung inkl. Metadaten wie Kennzeichner, Ersteller, Erstellungs- und Bearbeitungs-, und Veröffentlichungsdatum beschrieben, vgl. [Labeling System Datamodel](http://labeling.link/docs/ls/datamodel/#Vocabulary). Ein `Vokabular` wirkt als Container zur Gruppierung von Begriffen mit kontextgebundener Gültigkeit. Da `Begriffe` nur einem `Vokabular` angehören können, wird diesen somit die Hauptsprache und diverse Metadaten wie die Lizenz vererbt.

## Begriff vs. skos:Concept

In der [SKOS Referenz](https://www.w3.org/TR/skos-reference/#concepts) wird ein skos:Concept definiert:

*"A SKOS concept can be viewed as an idea or notion; a unit of thought. However, what constitutes a unit of thought is subjective, and this definition is meant to be suggestive, rather than restrictive. The notion of a SKOS concept is useful when describing the conceptual or intellectual structure of a knowledge organization system, and when referring to specific ideas or meanings established within a KOS. Note that, because SKOS is designed to be a vehicle for representing semi-formal KOS, such as thesauri and classification schemes, a certain amount of flexibility has been built in to the formal definition of this class.""*

`Concepts` sind als subjektive gedankliche Einheit definiert. Ein Beispiel hierfür ist eine konzeptionelle Struktur eines Wissenssystems wie ein Teil eines Thesaurus. `Concepts` besitzen keine Hauptsprache, als Bezeichner gibt es nur mehrere bevorzugte Bezeichnungen (prefLabel) der gedanklichen Einheit, je Sprache maximal eine ("The preferred lexical label for a resource, in a given language. A resource has no more than one value of skos:prefLabel per language tag, and no more than one value of skos:prefLabel without language tag."). Des Weiteren können auch beliebig viele alternavie Bezeichner (altLabels) verwendet werden ("An alternative lexical label for a resource. Acronyms, abbreviations, spelling variants, and irregular plural/singular forms may be included among the alternative labels for a concept."). Die gedankliche Einheit kann durch Beschreibungen textlich konkretisiert werden. Hier sind Beschreibungen in allen Sprachen möglich. `Concepts` können Relationen zu anderen `Concepts` im gleichen `ConceptsScheme` (auch transitiv) haben oder als Mapping zu `Concepts` in anderen `ConceptSchemes`.

Ein `Begriff` zeichnet sich dadurch aus, dass er einen eindeutigen Bezeichner (label) in der Sprache des `Vokabulars` besitzt. Weitere Bezeichnungen können als Übersetzungen in andere Sprachen modelliert werden. Übersetzungen können nicht direkt addressiert werden. Sie sind nur als Datenprodukt im Begriffscontainer verfügbar. Alternative Bezeichnungen, wie Akronyme, Synonyme, Antonyme, Sprachvarianten etc. können nicht modelliert werden. `Begriffe` können durch eine Beschreibung in der Sprache des `Vokabulars` näher beschrieben werden. Relationen zu anderen `Begriffen` innerhalb eines Vokabulars sind möglich, diese sind jedoch nicht transitiv. Assoziationen, Ähnlichkeiten, Übereinstimmungen und Hierarchien zu `Concepts` / `Begriffen` anderer `ConceptSchemes` bzw. `Vokabulare` sind über Mapping Properties möglich. Darüber hinaus kann ein `Begriff` zu einer Ressource des Internet Archive verlinkt werden, vgl. [Labeling System Datamodel](http://labeling.link/docs/ls/datamodel/#Label).

## Was ist nicht möglich?

* Synonyme
* Antonyme
* Container für Begriffe (vgl. skos:Collection)
* Top Concepts
* SKOS Validierung
* transitive broader / narrower Beziehungen
