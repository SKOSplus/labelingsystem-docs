# Handbuch Viewer

*Stand: 02.05.2017*

## Landing Page & Suche

Auf der Landing Page befindet sich in der oberen Hälfte ein Suchschlitz, indem nach `labels` gesucht werden kann.

[![](_images/ug_viewer/ug_v_landingpage.png)](_images/ug_v_landingpage.png)

Die Seite zeigt dann eine Ergebnisliste an.

[![](_images/ug_viewer/ug_v_labelsearch1.png)](_images/ug_v_labelsearch1.png)

Die Liste kann durch Klick auf `extend/collapse boxes` komplett aufgeklappt, bzw. verkleinert werden oder auch durch den Breadcrumb einzeln geöffnet werden. Hierbei werden die Beschreibung und Verlinkungen angezeigt.

[![](_images/ug_viewer/ug_v_labelsearch2.png)](_images/ug_v_labelsearch2.png)

Ergibt eine Suche kein Ergebnis, kann zur [Vokabularübersicht](#vokabularubersicht) gesprungen werden.

[![](_images/ug_viewer/ug_v_labelsearch3.png)](_images/ug_v_labelsearch3.png)

Ein Klick auf ein Suchergebnis zeigt die [Concept-Details](#concept-details).

## Vokabularübersicht

Veröffentlichte Vokabulare sind über `[host]/#/vocabularies` erreichbar.

[![](_images/ug_viewer/ug_v_vocabsoverview.png)](_images/ug_v_vocabsoverview.png)

Hier können die Vokabulare über den `filter` nach dem jeweiligen Titel gefiltert werden. Die Vokabularkacheln zeigen den Titel, die Anzahl der Konzepte, den Ersteller, die Kurzbeschreibung, wie auch die Hauptsprache an. Ein Klick auf die Kachel führt weiter zu den [Vokabular-Details](#vokabular-details). Durch Klick auf das `Suchen` Symbol kann zurück zur label-Suche gelangt werden.

## Vokabular-Details

Die Vokabular-Detail-Ansicht zeigt im oberen Bereich die Metadaten des Vokabulars an, wie Titel, Hauptsprache, URI, Ersteller, Beschreibung, Lizenz, sowie allgemeine Informationen zum Labeling System. Zudem kann über den Link `SKOS` das Vokabular als SKOS-RDF-File heruntergeladen werden. Das Suchen-Symbol leitet zurück zur allgemeinen label-Suche. Im unteren Bereich ist eine Liste aller Begriffe des Vokabulars verfügbar. Diese kann wie gewohnt extended oder sortiert werden. Zudem ist eine Filterung nach dem label-Namen möglich. Ein Klick auf einen Begriff öffnet diesen in den Concept-Details.

[![](_images/ug_viewer/ug_v_vocabdetail1.png)](_images/ug_v_vocabdetail1.png)

[![](_images/ug_viewer/ug_v_vocabdetail2.png)](_images/ug_v_vocabdetail2.png)

## Concept-Details

Die Concept-Detail-Ansicht zeigt im oberen Bereich die Metadatend des Begriffs an, wie Vokabular, Bezeichner, Sprache, URI, Ersteller, Historie (mit Klick auf `history` können Änderungen nach der Veröffentlichung nachvollzogen werden), Lizenz, sowie allgemeine Informationen zum Labeling System. Über die Links im Bereich Download kann der Begriff in diversen RDF-Foramten maschinenlesbar heruntergeladen werden. Dies ist auch mit der API über diverse Accept-Header möglich. Das Suchen-Symbol leitet zurück zur allgemeinen label-Suche.

Im unteren Bereich können die Details des Begriffs angesehen werden. Links, bzw. rechts stehen die broader, bzw. narrower Begriffe, mittig können Übersetzungen inkl. Sprache, die Beschreibung, sowie Mappings und Links (inkl. Typ und Sprache) eingesehen werden. Ein Klcik auf ein "graues" Label öffnet die Concept-Detail-Ansicht des jeweiligen Begriffs, so dass hiermit durch den "Baum" gebrowsed werden kann. Ein Klick auf ein externes Konzept öffnet die Original-Ressource in einem neuen Fenster.

[![](_images/ug_viewer/ug_v_conceptdetail1.png)](_images/ug_v_conceptdetail1.png)

[![](_images/ug_viewer/ug_v_conceptdetail2.png)](_images/ug_v_conceptdetail2.png)
