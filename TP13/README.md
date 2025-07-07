# **TP13 – Standards und Middleware**

Im [Teilprojekt 13 „Standards und Middleware“](https://github.com/VWS4LS/vws4ls-subproject-results/tree/main/TP13) des Projekts VWS4LS wurden Lösungsansätze für die Anwendung von Branchenstandards und Normen zur Beschreibung von Informationsfragmenten in der Verwaltungsschale erarbeitet.

So wurde untersucht, inwieweit Aspektmodelle und VWS-Submodelle für verschiedene Technologien – wie EDC und VWS – geeignet sind und ob beide Ansätze parallel oder jeweils nur einer davon eingesetzt werden kann.

Weiterhin wurde der aktuelle Entwicklungsstand der OPC-UA Companion Specification für die Wiring Harness Industrie dargestellt, um einen umfassenden Überblick über den Stand der Standardisierung und Interoperabilität in diesem Bereich zu geben.

Darüber hinaus werden vorhandene semantische Beschreibungen, wie beispielsweise der VEC (Vehicle Electric Container), ECLASS und IEC, auf ihre Kompatibilität und ihren Mehrwert für die Verwaltungsschale geprüft.

Ein weiterer Fokus lag auf der Analyse und dem Vergleich von bereits etablierten Lösungen wie Eclipse BaSyx (siehe Abbildung 4-1), dem AAS-Designer sowie MNESTIX, um die Einsatzmöglichkeiten der Verwaltungsschale (VWS) in der industriellen Praxis zu bewerten. 

![image](https://github.com/user-attachments/assets/670adad0-3c1a-447e-a295-740e8bb07c4d)     
Abbildung 4 1: BaSyx: Neue AAS Editor Funktionalitäten

## AP 13.1 – Abgleich von Aspekt- und Teilmodellen

Eine wesentliche Herausforderung für den interoperablen Datentransfer im Catena-X Automotive Network (Catena-X) ist die Bereitstellung von Informationen in Form von Aspektmodellen.

Im Projektverlauf wurden zwei wesentliche Erkenntnisse gewonnen:

1.  Für den Zugriff auf Verwaltungsschalen über Catena-X ist es nicht zwangsweise notwendig die Teilmodelle der Verwaltungsschale in Aspektmodelle für Catena-X zu transformieren. Stattdessen kann über die Control Plane des EDC die Zugriffskontrolle zum Verwaltungsschalenserver geregelt werden. Anschließend kann ein direkter Zugriff auf die Teilmodelle erfolgen.
2.  Im Februar 2025 wurde zwischen IDTA und Catena-X eine gemeinsame Arbeitsgruppe «Guideline: How to use SAMM as semantic definition for Asset Administration Shell» geformt, um ein ganzheitliches Regelwerk zu erarbeiten, mit dem Interoperabilität zwischen Aspekt- und Teilmodellen hergestellt werden soll.

Aus diesen Gründen hat das Konsortium entschieden keine parallelen Forschungsaktivitäten hinsichtlich des Abgleichs von Aspekt- und Teilmodellen zu starten.

## AP 13.2 – Freigabe der Teilmodelle „Process Parameters“

Im Rahmen von AP 13.2 wurde das Teilmodell «Bill of Process» (IDTA 02031) zu «Process Parameters» umbenannt, in zwei Teile aufgegliedert, inhaltlich klarer formuliert und im Kontext einer umfassenden Prozessbeschreibung - in Form eines Prozess-Teilmodells - eingeordnet.

Die ursprüngliche Bezeichnung «Bill of Process» war missverständlich und legte eine thematische Nähe zum Teilmodell «Hierarchical Structures enabling Bills of Material» (IDTA 02011) nahe. Diese thematische Nähe ist jedoch nicht vorhanden, weshalb das Teilmodell für ein besseres Verständnis umbenannt wurde.

Im weiteren Verlauf wurde deutlich, dass das Teilmodell in zwei Teilen veröffentlicht werden muss. Dieser Schritt ist notwendig, weil die Parameter auf Typ- und Instanz-Ebene beschrieben werden. Da die Verwaltungsschalen für Typen und Instanzen eigene Teilmodelle benötigen, sind hierfür entsprechend zwei Teilmodelle notwendig. Diese wurden entsprechend als Teil 1 für Typen und Teil 2 für Instanzen aufgegliedert:

-   IDTA 02031-1 Process Parameters, Part 1: Type
-   IDTA 02031-1 Process Parameters, Part 2: Instance

Die Teilmodelle wurden am 24.04.2025 in den IDTA-Freigabeprozess gegeben, mit dem Ziel einer Freigabe innerhalb der Laufzeit des Forschungsprojektes am 08.06.2025 zu erreichen.

## AP 13.3 – OPC UA Begleitstandard "Wire Harness Manufacturing"

Der im Rahmen von TP1 erarbeitete OPC UA Begleitstandard «Wire Harness Manufacturing» (OPC 40570) wurde am 24.02.2025 in der Version 1.0 veröffentlicht und umfasst zunächst Prozesse im Schneidraum. Um einen ganzheitlichen Begleitstandard zu erreichen, wurden Prozesse für Prüfmaschinen beschrieben.

Hierfür wurde ein mehrstufiges Vorgehen gewählt:

1.  Prüfprozesse identifizieren
2.  Use Cases und Prozessparameter definieren
3.  Abgleich mit Domänenexperten
4.  Parameterabgleich mit VEC
5.  Übergabe an VDMA-Arbeitsgruppe

### Prüfprozesse identifizieren

Auf Basis der Prozessliste aus TP3 wurde zunächst die Liste der Prüfprozesse extrahiert und Kernprozesse für den Begleitstandard ausgewählt. In Tabelle 4-1 sind die Prüfprozesse mit Erläuterungen aufgeführt. Es handelt sich hierbei um eine unvollständige Liste der Prüfprozesse, die für die Leitungssatzherstellung üblich sind.

| Prüfprozess          | Beschreibung                                                                                                                                                                                                                                                                                                                                                                                           |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Kapazitätsmessung    | Bei der Kapazitätsmessung werden die im Leitungssatz verbauten Kondensatoren auf Vorhandensein und Größe überprüft.                                                                                                                                                                                                                                                                                    |
| Farberkennung        | Die Farberkennung dient im Wesentlichen der Erkennung von Leitungsfarben oder farblich Kodierten Anbauteilen.                                                                                                                                                                                                                                                                                          |
| Durchmesser          | Durchmesserprüfungen werden in der Regel durch geometrische Formen realisiert und dienen beispielsweise der Überprüfung von Ringkabelschuhen.                                                                                                                                                                                                                                                          |
| Dioden               | Bei der Dioden-Prüfung werden im Leitungssatz verbaute Dioden in Durchgangs- und Sperr-Richtung überprüft.                                                                                                                                                                                                                                                                                             |
| Lichtleiter          | Die Lichtleiter-Prüfung dient der Bewertung der Dämpfung des Lichtsignals im Leitungssatz, um schwache Lichtsignale zu erkennen.                                                                                                                                                                                                                                                                       |
| Verbindungstest      | Beim Verbindungstest werden alle elektrischen Verbindungen im Leitungssatz überprüft, um Kurzschlüsse, Unterbrechungen und vertauschte Leitungen zu erkennen.                                                                                                                                                                                                                                          |
| Pin-Position         | Bei der Pin-Positions-Prüfung werden die Stecktiefen der Terminals im Steckergehäuse überprüft, um unzureichende oder zu weit herausstehende Kontakte zu erkennen.                                                                                                                                                                                                                                     |
| Präsenz              | Die Präsenzerkennung wird eingesetzt, um Anbauteile und Kodierungen von Leitungssatzkomponenten zu erkennen.                                                                                                                                                                                                                                                                                           |
| Relais               | Bei der Relaisprüfung werden im Leitungssatz verbaute Relais auf Funktion und Schaltverhalten überprüft.                                                                                                                                                                                                                                                                                               |
| Airbag-Brücke        | Airbag-Brücken sind elektrische Brücken im Stecker der Airbag-Zündpille, die ein versehentliches Auslösen durch statische Entladungen verhindern sollen. Bei der Prüfung wird die Brücke im geschlossenen und geöffneten Zustand überprüft.                                                                                                                                                            |
| Thermistor           | Die Thermistor-Prüfung wird für temperaturveränderliche Widerstände eingesetzt. Hierbei wird der Temperaturkennwert des Widerstands mit einem Vergleichswert verglichen.                                                                                                                                                                                                                               |
| Leckage-Test         | Der Leckage-Test findet Anwendung bei Steckergehäusen, für die besondere Anforderungen an Dichtungen und Wasser- bzw. Luftdurchlässigkeit gelten. Hierbei wir die Dichtheit mittels Über- oder Unterdruckkontrolle nachgewiesen.                                                                                                                                                                       |
| Bestückungskontrolle | Die Bestückungskontrolle findet Anwendung bei der Montage von Sicherungsboxen. Hierbei werden die bestückten Sicherungen, Relais und andere Anbauteile auf Vorhandensein, Steckrichtung und Lesbarkeit der Beschriftung überprüft.                                                                                                                                                                     |
| Höhenkontrolle       | Die Höhenkontrolle wird in Kombination mit der Bestückungskontrolle durchgeführt und überprüft ob die bestückten Sicherungen, Relais und andere Anbauteile vollständig gesteckt wurden.                                                                                                                                                                                                                |
| Schraubmontage       | Der Schraubprozess ist sowohl ein Montage- als auch ein Prüfprozess. Hierbei werden kritische Verschraubungen nach der Richtlinie VDI/VDE 2862 «*Mindestanforderungen zum Einsatz von Schraubsystemen und -Werkzeugen - Anwendungen in der Automobilindustrie*» durchgeführt und protokolliert. Zusätzlich werden die Schraubpositionen, Schraubparameter und ggf. elektrische Verbindungen überwacht. |

Tabelle 4-1: Liste von Prüfprozessen mit Erläuterungen

Da eine realistische Standardisierung für alle Prüfprozesse innerhalb der Projektlaufzeit nicht möglich ist, wurden für die weiteren Arbeiten am Begleitstandard die folgenden Prüfprozesse ausgewählt:

-   Verbindungstest
-   Bestückungskontrolle
-   Höhenkontrolle
-   Höhenkontrolle

Es handelt sich hierbei um elementare Prüfprozesse, für die erhebliche Informationsbedarfe bestehen und somit wesentliche Anforderungen an den OPC UA Begleitstandard stellen.

### Use Cases und Prozessparameter definieren

Für die ausgewählten Prüfprozesse wurden im nächsten Schritt die Use Cases und die wichtigsten Prozessparameter definiert. Hierbei sind zunächst nur diejenigen Use Cases und Parameter betrachtet worden, die für die jeweiligen Prozesse unerlässlich sind und somit den größten Nutzen erzeugen. Weitere Parameter werden für zukünftige Versionen des Begleitstandards vorbehalten. Die vollständige Liste der Use Cases und Parameter ist dem Anhang zu entnehmen.

Abbildung 4-1 gibt einen Überblick über die allgemeine Struktur der Prüfprozesse, wie sie als erster Entwurf definiert wurden. Die Details sind in den folgenden Kapiteln näher beschrieben.

![image](https://github.com/user-attachments/assets/738664b7-6289-4470-9089-e2ea695b757b)     
Abbildung 4-1: Struktur der Prüfprozesse für den OPC UA Begleitstandard

#### Prüfprozesse

Der allgemeine Teil bezieht sich auf Parameter und Use Cases, die für alle Prüfprozesse gleichermaßen gültig sind. Hierbei geht es in erster Linie um Parameter bezüglich der zu prüfenden Komponenten, sowie des Gesamtergebnisses. Die Anforderungen sind in Tabelle 4-2 dargestellt.

| Prüfprozesse |                                                                                                                                                                                              |
|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Name         | Prüfprozesse                                                                                                                                                                                 |
| Ziel         | Kontrolle und Rückverfolgbarkeit von Prüfprozessen sicherstellen.                                                                                                                            |
| Beschreibung | Der Client möchte… die zu prüfenden Komponenten festlegen wissen, welcher Benutzer und in welcher Schicht eine Prüfung durchgeführt wurde. wissen, wie häufig eine Prüfung wiederholt wurde. |

Tabelle 4-2: Use Cases für Prüfprozesse

#### Verbindungstest

Beim Verbindungstest werden alle elektrischen Verbindungen im Leitungssatz überprüft, um Kurzschlüsse, Unterbrechungen und vertauschte Leitungen zu erkennen. In Tabelle 4-3 sind die Use Cases für den Prozess aufgeführt und beschrieben.

| Elektrische Verbindung |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Name                   | Elektrische Verbindung                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| Ziel                   | Kontrolle und Überprüfung des elektrischen Durchgangs, der ordnungsgemäßen Installation und der Eigenschaften von Kabelbäumen.                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Beschreibung           | Der Client möchte… die elektrische Durchgängigkeit und weitere Eigenschaften des Leitungssatzes überprüfen. steuern, ob eine Kurzschlussprüfung erfolgen soll. den Grenzwert für die Kurzschlussprüfung festlegen. wissen, ob eine Komponente im Leitungssatz vorhanden ist. wissen, ob eine Komponente bestimmte Eigenschaften aufweist. wissen, ob eine Leitung fehlt. wissen, ob eine Leitung am falschen Terminal angeschlossen ist. wissen, ob zwei Leitungen kurzgeschlossen sind. wissen, ob zwei Leitungen vertauscht wurden. wissen, was der genaue Grund für eine Fehler ist. |

Tabelle 4-3: Verbindungstest Use Cases

#### Bestückungskontrolle

Die Bestückungskontrolle findet Anwendung bei der Montage von Sicherungsboxen. Hierbei werden die bestückten Sicherungen, Relais und andere Anbauteile auf Vorhandensein, Steckrichtung und Lesbarkeit der Beschriftung überprüft. In Tabelle 4-4 sind die Use Cases für den Prozess aufgeführt und beschrieben.

| Bestückungskontrolle |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Name                 | Bestückungskontrolle                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| Ziel                 | Kontrolle und Überprüfung der korrekten Bestückung einer Sicherungsbox                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Beschreibung         | Der Client möchte… eine Sicherungsbox bestücken steuern, ob eine leere Position überprüft werden soll. steuern, ab welchem Schwellenwert eine Komponente als bestückt erkannt wird. wissen, ob die korrekte Komponente in einer Position bestückt wurde. wissen, welche Komponente in einer Position bestückt ist. wissen, mit welcher Konfidenz eine Komponente erkannt wurde. wissen, ob eine Komponente fehlt. wissen, ob eine Komponente an der falschen Position bestückt wurde. wissen, ob eine Komponente in der falschen Drehrichtung bestückt wurde. wissen, ob eine Komponente auf einer Position bestückt wurde, die leer sein sollte. wissen, ob eine Beschilderung fehlt. |

Tabelle 4-4: Bestückungskontrolle Use Cases

#### Höhenkontrolle

Die Höhenkontrolle wird in Kombination mit der Bestückungskontrolle durchgeführt und überprüft ob die bestückten Sicherungen, Relais und andere Anbauteile vollständig gesteckt wurden. In Tabelle 4-5 sind die Use Cases für den Prozess aufgeführt und beschrieben.

| Höhenkontrolle |                                                                                                                                                                                                                                                                   |
|----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Name           | Höhenkontrolle                                                                                                                                                                                                                                                    |
| Ziel           | Kontrolle und Überprüfung der korrekten Einbauposition von Komponenten einer Sicherungsbox                                                                                                                                                                        |
| Beschreibung   | Der Client möchte… die Einbauposition von Komponenten einer Sicherungsbox überprüfen. steuern, ob leere Positionen überprüft werden sollen. wissen, ob eine Komponente nicht vollständig gesteckt wurde. wissen, ob eine Komponente ungleichmäßig gesteckt wurde. |

Tabelle 4-5: Höhenkontrolle Use Cases

#### Schraubmontage

Der Schraubprozess ist sowohl ein Montage- als auch ein Prüfprozess. Hierbei werden kritische Verschraubungen nach der Richtlinie VDI/VDE 2862 «*Mindestanforderungen zum Einsatz von Schraubsystemen und -Werkzeugen - Anwendungen in der Automobilindustrie*» durchgeführt und protokolliert. Zusätzlich werden die Schraubpositionen, Schraubparameter und ggf. elektrische Verbindungen überwacht. In Tabelle 4-6 sind die Use Cases für den Prozess aufgeführt und beschrieben.

| Schraubmontage |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Name           | Schraubmontage                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Ziel           | Kontrolle und Überprüfung der korrekten Verschraubung von sicherheitsrelevanten Schraubverbindungen.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| Beschreibung   | Der Client möchte… Schraubvorgänge an sicherheitsrelevanten Schraubverbindungen durchführen. die Anzahl der Wiederholungen mit einer Schraube oder Mutter begrenzen. wissen, ob ein Schraubvorgang mit den richtigen Einstellungen durchgeführt wurde. wissen, welches Schraubwerkzeug für den Schraubvorgang verwendet wurde. wissen, welche ID zum Schraubvorgang gehört. wissen, wie häufig eine Schraube oder Mutter verschraubt wurde. die Ergebnisse jeder Schraubstufe wissen. wissen, an welcher Position die Verschraubung durchgeführt wurde. die Schraubprogramme für eine Position festlegen. die Losschraubprogramme für eine Position festlegen. |

Tabelle 4-6: Schraubmontage Use Cases

### Abgleich mit Domänenexperten

Die erarbeiteten Use Cases und Prozessparameter wurden im nächsten Schritt weiteren Domänenexperten zur Kommentierung und Ergänzung zur Verfügung gestellt. Hierzu haben die Unternehmen Adaptronic und Cirris der Komax Gruppe in Zusammenarbeit mit dem Konsortialpartner Komax Testing den Abgleich durchgeführt.

Das Ergebnis des Abgleichs ist eine Liste der Use Cases und Prozessparameter, die aus Sicht der Domänenexperten notwendig sind.

### Abgleich mit VEC

Nach dem Abgleich mit den Domänenexperten wurden die Prozessparameter mit dem VEC-Standard abgeglichen, wie es auch für die vorhandenen Prozesse des Begleitstandards erfolgt ist. Hierfür wurden die Parameter zunächst auf relevante Klassen und Eigenschaften des VEC-Standards eingegrenzt, um anschließend die benötigten Strukturen zu extrahieren.

Eine wesentliche Erkenntnis bei der Anwendung des VEC-Standards ist die Möglichkeit Prüfprozesse auf der Grundlage von unterschiedlichen Merkmalen abzubilden. Beispielsweise können einfache elektrische Prüfprozesse, die lediglich die Verbindung zwischen zwei Komponenten erfassen, bereits auf Grundlage des logischen Modells des Leitungssatzes durchgeführt werden. Komplexere Anforderungen, hingegen, erfordern detailliertere Informationen aus dem physischen Modell. Das stellt besondere Herausforderungen an Maschinenhersteller und VEC-Datenquellen, die im Rahmen der Projektlaufzeit dieses Forschungsprojektes nicht weiter betrachtet werden konnten.

Auch die Zuordnung von VEC-Merkmalen zu den Prozessparametern stellte eine besondere Herausforderung dar, die nicht abschließend gelöst wurde. Beispielsweise lassen sich Merkmale aus dem VEC nicht immer eindeutig auf die heute üblichen Prozessmerkmale übertragen. Mögliche Ansätze für die Auflösung dieser Herausforderungen sind Änderungen an den heute üblichen Prozessparametern, sowie die Erweiterung des VEC-Standards, um Spezifikationslücken zu schließen.

### Übergabe an die VDMA-Arbeitsgruppe «Wire Harness Manufacturing»

Die mit den Domänenexperten und VEC abgeglichenen Prüfprozesse wurden an die VDMA-Arbeitsgruppe «Wire Harness Manufacturing» für die weitere Standardisierung im Begleitstandard übergeben.

## AP 13.4 – Semantische Durchgängigkeit

Eine elementare Voraussetzung für digitale Interoperabilität ist die Nutzung von semantischen Identifikationsmerkmalen und eindeutigen Bezeichnern über die gesamte digitale Wertkette.

Eindeutige Bezeichner sind erforderlich, um auf eine Verwaltungsschale und ihre Teilmodelle zu verweisen. Eindeutige Bezeichner werden zudem für den Verweis auf externe semantische Informationen verwendet. Die im Folgenden beschriebenen Kennzeichnungsschemata sind für die Verwendung in der Verwaltungsschale von entscheidender Bedeutung.

### Modellierung von Bereichswerten

Die [„Range“-Definition der VWS](https://admin-shell-io.github.io/aas-specs-antora/IDTA-01001/v3.1/spec-metamodel/submodel-elements.html#range-attributes) ist ähnlich wie die Property aufgebaut und als „experimental“ klassifiziert. Problematisch ist, dass damit kein Ist- / bzw. Sollwert abgebildet werden können, sondern lediglich eine Ober- und Untergrenze. Semantische Referenzierbarkeit über *valueId* wird im „Range“-Konstrukt ebenfalls nicht unterstützt.

Siehe dazu auch die Diskussion hier: [https://github.com/admin-shell-io/VWS-specs/issues/450](https://github.com/admin-shell-io/aas-specs/issues/450)

Um für eine Property Bereichswerte zu modellieren, sollen geeignete „[Qualifier](https://industrialdigitaltwin.io/aas-specifications/IDTA-01001/v3.2/spec-metamodel/common.html#qualifiable-attributes)“ definiert und in einen geeigneten VWS-Standard überführt werden.

Dazu wurde im Rahmen einer adHoc-„Qualifier-Initiative“ bei der IDTA mit F. Scherenschlich, M. Hoffmeister und C. Bornträger eine Vorschlagsliste zur Ergänzung der *IDTA GUIDELINE: How to create a Submodel Template Specification* [22] erarbeitet. Im Wesentlichen geht es dabei um diese vier „TOLERANCE_...“-Definitionen:

````
{
    "name": "Predicate relation | negative tolerance %",
    "qualifier": {
      "kind": "ConceptQualifier",
      "semanticId": {
        "type": "ExternalReference",
        "keys": [
          {
            "type": "GlobalReference",
            "value": "0112/2///61360_4#AAF444"
          }
        ]
      },
      "type": "PredicateRelation",
      "value": "TOLERANCE_REL_NEG_10",
      "valueId": null
    }
  },
  {
    "name": "Predicate relation | positive tolerance %",
    "qualifier": {
      "kind": "ConceptQualifier",
      "semanticId": {
        "type": "ExternalReference",
        "keys": [
          {
            "type": "GlobalReference",
            "value": "0112/2///61360_4#AAF445"
          }
        ]
      },
      "type": "PredicateRelation",
      "value": "TOLERANCE_REL_POS_11",
      "valueId": null
    }
  },
  },
    "name": "Predicate relation | negative tolerance abs",
    "qualifier": {
      "kind": "ConceptQualifier",
      "semanticId": {
        "type": "ExternalReference",
        "keys": [
          {
            "type": "GlobalReference",
            "value": "http://www.prostep.org/ontologies/ecad/2024/03/vec#toleranceLowerBoundary"
          }
        ]
      },
      "type": "PredicateRelation",
      "value": "TOLERANCE_ABS_NEG_12",
      "valueId": null
    }
  },
  {
    "name": "Predicate relation | positive tolerance abs",
    "qualifier": {
      "kind": "ConceptQualifier",
      "semanticId": {
        "type": "ExternalReference",
        "keys": [
          {
            "type": "GlobalReference",
            "value": "http://www.prostep.org/ontologies/ecad/2024/03/vec#toleranceUpperBoundary"
          }
        ]
      },
      "type": "PredicateRelation",
      "value": "TOLERANCE_ABS_POS_13",
      "valueId": null
    }
  },
}

````
Listing 4-1: Vorschlag für die Definition von Qualifiern

Die Qualifier-Definitionen in dieser Datei des VWSXPE sollen konsolidiert werden in der *IDTA GUIDELINE: How to create a Submodel Template Specification* [22]:

[https://github.com/eclipse-VWSpe/package-explorer/blob/main/src/VWSxPackageExplorer/qualifier-presets.json](https://github.com/eclipse-aaspe/package-explorer/blob/main/src/AasxPackageExplorer/qualifier-presets.json)

Die [DIN SPEC 92000](https://www.dinmedia.de/de/technische-regel/din-spec-92000/320981982) und bestehende IEC-Definitionen soll dabei beachtet werden.sollen dabei beachtet werden, z.B.

<https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/PropertiesAllVersions/0112-2---61360_4%23AAF445>

<https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/PropertiesAllVersions/0112-2---61360_4%23AAF575>

### UUID / GUID

**UUID** (Universally Unique Identifier[^1]) ist eine 128-Bit-Kennung (16 Byte), die vom Open Systems Interconnection (OSI)-Framework standardisiert und in der RFC 4122 spezifiziert ist. UUIDs sind immer einzigartig, ohne dass eine zentrale Behörde zur Koordination notwendig wäre. Die Einzigartigkeit beruht auf Wahrscheinlichkeit (für V4) oder sorgfältigem Design (für V1, V3, V5), wodurch die Wahrscheinlichkeit von Kollisionen mathematisch ausgeschlossen werden kann.

[^1]: <https://de.wikipedia.org/wiki/Universally_Unique_Identifier>

**GUID** (Globally Unique Identifier) ist eine spezielle Form von UUID, die von Microsoft gestaltet wurde. Im Kontext der Verwaltungsschale können UUID und GUID als austauschbar betrachtet werden.

**Format:** Eine UUID wird in der Regel als 32-stellige Hexadezimalzahl dargestellt, die durch Bindestriche in fünf Gruppen unterteilt ist: 8-4-4-4-12.

**Beispiel:** 550e8400-e29b-41d4-a716-446655440000

**Varianten:** RFC 4122 definiert eine bestimmte „Variante“ (Bits 64-65 auf 10 gesetzt), um sie von anderen 128-Bit-ID-Schemata zu unterscheiden. Die meisten UUIDs folgen dieser Variante.

UUIDs werden oft von VWS-Tools generiert, um sie als VWS- und Teilmodell-IDs zu verwenden. Dies mag in vielen Fällen als schnelle Lösung angemessen sein, kann aber langfristig problematisch werden, da UUIDs nicht *systematisch* und *sprechend* und somit schwierig zu verwalten sind. Insbesondere für die Verwendung in logisch aufgebauten ID-Strukturen sind UUIDs eher nicht geeignet. Daher sollten VWS-Ersteller eine sorgfältige Entscheidung über die Verwendung von UUIDs treffen.

***

### IRDI (ISO 29005-5)

Der *International Registration Data Identifier* (IRDI) ist ein globales Identifikationssystem für Eigenschaften, Werte und Konzepte, siehe Tabelle 4-2. Es ist in ISO 29005-5 und ISO/IEC 11179-6 als ein bewährtes Mittel zur Schaffung handhabbarer eindeutiger Identifikatoren definiert, die über verschiedene Sprachen und IT-Systeme hinweg konsistent bleiben. IRDIs werden in ECLASS-, IEC- und ISO-Normen verwendet.

![A diagram of a data identifier AI-generated content may be incorrect.](media/8568e76ca295b13ecbbc2a2e9dbec07b.png)

Abbildung 4-2: IRDI-Schema nach ISO 29005-5[^2][^3]

[^2]: <https://eclass.eu/fileadmin/Redaktion/pdf-Dateien/Wiki/ECLASS-BMEcat-Guideline-2005_1_v2_1.pdf>

[^3]: <https://reference.opcfoundation.org/Core/Part19/v105/docs/5.3>

IRDIs sind ein historisch etablierter Referenzier-Mechanismus, mit dem in der VWS umgegangen werden muss. Da sie aber eine externe Verwaltung benötigen, wird davon abgeraten, neue IRDIs für Elemente in der VWS zu erzeugen.

***

#### IEC IRDI-Struktur

Eine IEC-CDD folgt dem allgemeinen Format: **ICD**/**OI**/**AI**\#**IC**\#**VI**

-   **International Code Designator** (**ICD**): Identifiziert die Registrierungsbehörde (z. B. „0112“ für IEC).
-   **Organization Identifier** (OI): Gibt die Organisation innerhalb der Behörde an (z. B. „2“ für IEC).
-   Application Identifier (AI): Gibt die spezifische Norm an (z. B. „61360_4“ für IEC 61360-4 DB).
-   **Internal Code** (IC): Eindeutiger Code für das Element innerhalb des Wörterbuchs (z. B. „AAA612“).
-   **Version Indicator** (VI): Bezeichnet die Version des Eintrags (z. B. „001“).

**Beispiel**: [0112/2///61360_4\#AAA612\#001](https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/TU0/0112-2---61360_4%23AAA612), siehe Tabelle 4-7

| 0112/2///61360_4\#AAA612 |                                        |
|--------------------------|----------------------------------------|
| Code:                    | description                            |
| 0112/2/                  | Issuing Agency Code (IEC)              |
| 61360_4                  | IEC 61360 Standard Reference           |
| \#AAA612                 | Unique identifier for a property/class |

Tabelle 4-7: Breakdown of IRDI Example (0112/2///61360_4\#AAA612)

#### ECLASS IRDI-Struktur

Eine ECLASS IRDI hat in der Regel das Format: **ICD**/**OI**/**CSI**\#**Code**\#**Version**, siehe Tabelle 4-8 und Tabelle 4-9

-   **ICD (International Code Designator):** Code für die Registrierungsbehörde, z. B. „0173“ für ECLASS.
-   **OI (Organization Identifier):** Identifiziert die Organisation
-   **CSI (Code Space Identifier):** Gibt die Art des Strukturelements an (z. B. „01“ für Klassifizierungsklasse, „02“ für Eigenschaft, „07“ für Wert):

| Code Space Identifier  |                     |
|------------------------|---------------------|
| 01                     | Class               |
| 02                     | Property            |
| 05                     | unit of measurement |
| 07                     | property value      |

Tabelle 4-8: Excerpt of Code Space Identifiers (CSI) according to ISO 290ß05-527

-   **Code:** Eindeutiger Bezeichner für das spezifische Element (z. B. „27-22-01-01“ für eine Klasse oder „AAB123“ für eine Eigenschaft).
-   **Version:** Eine Versionsnummer (z. B. „001“).

| 0173-1\#01-AAA123\#001 |                     |
|------------------------|---------------------|
| Code:                  | description         |
| 0173                   | ICD code for eCl@ss |
| 1                      | eCl@ss Office       |
| 02                     | property            |
| ABH173                 | identifier of class |
| 003                    | version of class    |

Tabelle 4-9: Breakdown of IRDI Example (0173-1\#02-ABH173\#003)

**Classification classes**

**Beispiel**: 0173-1\#01-27-22-01-01\#001 entspricht 0173-1\#01-AAC098\#020

Informative Links zu online Elementbeschreibungen können so zusammengesetzt werden:

<https://eclass.eu/eclass-standard/content-suche/show?tx_eclasssearch_ecsearch%5Bid%5D=27220101>

### URI / IRI

Eine **URI** (Uniform Resource Identifier) ist eine Zeichenkette zur Identifizierung einer Ressource und ist durch RFC 3986 standardisiert. Es handelt sich um ein Konzept, das alles umfasst, was benannt oder lokalisiert werden kann, sei es eine Webseite, eine Datei oder eine abstrakte Einheit.

**Beispiel**

http://example.com/resource/123

**Bestandteile**

-   **Schema (**http**),**
-   **Autorität** (example.com),
-   **Pfad** (/resource/123)
-   **Abfragen** (?key=value) und/oder Fragmente (\#section1).

**Untertypen**

-   URL (Uniform Resource Locator)
-   URN (Uniform Resource Name)

Eine **IRI** (Internationalized Resource Identifier) ist eine durch RFC 3987 definierte Erweiterung des URI, die durch Umkodierung auch Nicht-ASCII-Zeichen (z.B. Akzente, chinesische Zeichen) unterstützt. IRIs sind technisch gesehen eine Obermenge von URIs, d.h. jeder URI ist ein IRI, aber nicht andersherum.

**Beispiel  
***http://exâmple.com/资源/123*

wird codiert als

*https://xn--exmple-xta.com/%E8%B5%84%E6%BA%90/123*

Die VWS benötigt weltweit eindeutige, maschinenlesbare und interoperable Identifikatoren. IRIs erfüllen diese Aufgabe, da sie die URIs (Uniform Resource Identifiers) um internationale Zeichen erweitern und sich durch die folgenden Merkmale an den globalen Geltungsbereich von Industrie 4.0 anpassen:

-   **Globale Einzigartigkeit**: IRIs nutzen Namensräume (z. B. Domänennamen), um sicherzustellen, dass sich zwei Assets nicht überschneiden, auch nicht in verschiedenen Organisationen.
-   **Internationalisierung**: IRIs erlauben Nicht-ASCII-Zeichen (z. B. http://工厂.cn/设备/123 für eine chinesische Fabrik), was für multinationale Lieferketten entscheidend ist.
-   **Auflösbarkeit**: HTTP-basierte IRIs können auf eine Ressource (z.B. einen VWS-Server) verweisen, was den direkten Abruf von Daten ermöglicht.
-   **Standardisierung**: IRIs entsprechen den Webstandards (RFC 3987) und den Praktiken des sog. „Semantic Web“[^4],, wodurch VWS mit breiteren Ökosystemen wie OPC UA oder Linked Data kompatibel ist.

[^4]: <https://de.wikipedia.org/wiki/Semantic_Web>

In der VWS-Metamodellspezifikation [13] werden IRIs ausdrücklich als primärer Bezeichnertyp sowohl für das Asset als auch für die VWS selbst empfohlen und bieten wesentliche administrative Vorteile:

***

**Namensraum-Kontrolle**: Das Schema und die Domäne fungieren als Namensraum, sodass Organisationen oder Systeme ihre eigenen Bezeichner ohne zentrale Koordinierungsstelle definieren können.

***

**Erweiterbarkeit**: URIs sind flexibel, man kann einen Pfad, eine Abfrage oder ein Fragment hinzufügen, um die Identität zu verfeinern.

***

Für die Anwendung in der VWS wird empfohlen, die Verwendung von Nicht-ASCII-Sonderzeichen in URIs/IRIs zu vermeiden.

***

### Semantische Datenbanken

Eine semantische Referenz ist ein Link zu einem externen Standard oder einer Ontologie, die die Bedeutung eines Datenelements innerhalb einer VWS definiert. Diese Referenzen gewährleisten Interoperabilität, Konsistenz und Automatisierbarkeit zwischen Industrie 4.0 Komponenten.

Für technische Daten in Industrieanlagen ist ein generischer Rahmen zur Strukturierung der Informationen erforderlich, um standardisierte Vokabulare und Industriestandards zur Definition und Verknüpfung von Komponentenattributen bereitzustellen. Es gibt eine Reihe von Industriestandards für semantische Referenzen:

-   **ECLASS**: Ein branchenübergreifender Standard mit Schwerpunkt auf Produktidentifikation mit detaillierten technischen Eigenschaften, der in Europa weit verbreitet ist. Er ist sehr granular und unterstützt mehrere Domänen.

    <https://eclass.eu/en/eclass-standard/search-content/search>

-   **ETIM** (Elektrotechnisches Informationsmodell): Ein standardisiertes Klassifizierungssystem hauptsächlich für Elektro- und HLK-Produkte. Konzentriert sich auf technische Produktdaten für die Elektro-, Gebäude- und Installationsbranche. Beliebt in Europa, insbesondere bei Herstellern, Großhändlern und Auftragnehmern für den Austausch von Produktdaten. Ähnlich wie ECLASS bietet es Klassen, Merkmale und Werte, ist aber stärker auf die elektrotechnischen und verwandten Branchen spezialisiert. Es wird von der Organisation ETIM International verwaltet.

    <https://prod.etim-international.com/class>,  
    <https://etimapi.etim-international.com/>

-   **GPC** (Globale Produktklassifikation): Ein Produktklassifizierungssystem, das von GS1 für den globalen Handel entwickelt wurde. Es deckt Konsumgüter, Industrieprodukte und Dienstleistungen ab, wobei der Schwerpunkt auf dem Einzelhandel und dem Handel liegt. Wird in Verbindung mit GS1-Standards (z. B. Barcodes) für die Effizienz der Lieferkette verwendet.

    <https://gpc-browser.gs1.org/>

-   **Electropedia**: Von der IEC herausgegebene Online-Terminologiedatenbank, enthält alle Begriffe und Definitionen des Internationalen Elektrotechnischen Vokabulars (IEV), das in den IEC 60050-Schriften veröffentlicht ist. Sie enthält mehr als 22 000 terminologische Einträge in englischer und französischer Sprache, gegliedert nach Themenbereichen, mit entsprechenden Begriffen in verschiedenen anderen Sprachen: Arabisch, Chinesisch, Dänisch, Deutsch, Finnisch, Italienisch, Japanisch, Koreanisch, Kroatisch, Mongolisch, Niederländisch, Norwegisch, Polnisch, Portugiesisch, Russisch, Schwedisch, Serbisch, Slowakisch, Slowenisch, Spanisch, Tschechisch, Türkisch und Ukrainisch (die Abdeckung variiert je nach Fachgebiet).

    <https://electropedia.org/>

-   **IEC-CDD**: Konzentriert sich auf elektrotechnische und industrielle Bereiche, basiert auf IEC 61360-Normen und legt den Schwerpunkt auf die technische Merkmalsbeschreibung.

    <https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/SearchFrameset>,  
    <https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/TreeFrameset>

-   **VEC** (Vehicle Electric Container) ist ein offener Standard, der im Rahmen von prostep ivip und VDA entwickelt wurde, um elektrische und elektronische Systeme in Fahrzeugen zu beschreiben, z. B. Kabelbäume, Komponenten und Anschlussmöglichkeiten. Es ist ein XML-basiertes Datenmodell, stellt aber auch eine Ontologie bereit, d.h. ein formalisiertes Vokabular mit Klassen, Eigenschaften und Beziehungen. Seine Elemente können unter Anwendung der Prinzipien des semantischen Webs über URIs referenziert werden.

    <https://ecad.prostep.org/ontologies/2024/03/vec>

Einzelne Referenzsysteme bieten meist nur spezialisierte semantische Definitionen. Es kann daher auch sinnvoll sein, mehrere Referenzsysteme in Kombination zu verwenden.

#### ECLASS

ECLASS ist ein international anerkanntes Klassifizierungssystem, welches einen standardisierten Rahmen für die Beschreibung von Produkten und Dienstleistungen in allen Branchen bietet. Es ermöglicht Unternehmen, Herstellern und Lieferanten eine konsistente Identifizierung von Produktklassen und -eigenschaften über verschiedene Länder, Sprachen und Geschäftssysteme hinweg.

Der ECLASS-Standard wird kontinuierlich erweitert, wobei neue IRDIs über eine Content-Development-Plattform vorgeschlagen und geprüft werden.

Der Datenbestand kann über eine native Webseite eingesehen werden, siehe Abbildung 4-3: <https://eclass.eu/en/eclass-standard/search-content>:

![A screenshot of a web page AI-generated content may be incorrect.](media/e48ca18b6b1f9894b6fc1ee2395f90f8.png)

Abbildung 4-3: ECLASS - Webbasierte Contentsuche und -anzeige

Die Nutzung von ECLASS-Daten unterliegt den Vertragsbedingungen des ECLASS e.V. Mitglieder zahlen Beiträge, die je nach Unternehmensgröße variieren, und erhalten Zugang zu den Daten, auch über eine webbasierte REST-API. Nicht-Mitglieder müssen ebenfalls Lizenzen erwerben, um IRDIs rechtmäßig zu nutzen. Eine unbefugte Nutzung ohne Lizenz verstößt gegen die Nutzungsbedingungen und kann rechtliche Konsequenzen nach sich ziehen. Es gibt auch die Möglichkeit, ECLASS IRDIs über ein Pay-per-IRDI-Modell zu lizenzieren.

Die IDTA hat eine Best-Practice-Guideline zur Anwendung von ECLASS im VWS-Kontext veröffentlicht [16].

#### IEC-CDD

Das *Common Data Dictionary* (CDD) der Internationalen Elektrotechnischen Kommission (IEC) verwendet den International Registration Data Identifier (IRDI) zum Referenzieren von Eigenschaften, Klassen und Werten und gewährleistet so die Interoperabilität über Branchen, digitale Zwillinge und Lieferketten hinweg. IEC-Normen sind in der Industrieautomation, in Energiesystemen, in der Elektronik und in der Fertigung weit verbreitet.

Die Nutzung von IEC CDD IRDIs ist grundsätzlich kostenfrei, Nutzer müssen jedoch die IEC-Nutzungsbedingungen und die zugrunde liegenden Standards einhalten, insbesondere bei kommerziellen Anwendungen oder Integrationen in Systeme. Die Datenbank ist über eine Weboberfläche öffentlich zugänglich, eine netzwerkbasierte Schnittstelle über eine REST-API wurde bislang jedoch noch nicht realisiert.

Der Zugang über die native Weboberfläche ist im Folgenden kurz beschrieben:

**Schritt 1**: Aufruf der Webseite: <https://cdd.iec.ch/cdd/common/iec61360-7.nsf/TreeFrameset>

**Schritt 2**: Auswahl eines geeigneten IEC-Standards, z.B. „IEC61360-4“ (siehe Abbildung 4-4):

![Ein Bild, das Text, Screenshot, Software, Zahl enthält. KI-generierte Inhalte können fehlerhaft sein.](media/29952ab47cef7d6a056b07ca53cd83a7.png)

Abbildung 4-4: IEC CDD: Auswahl des Standards

**Schritt 3**: Durchsuchen des ausgewählten Baums manuell über <https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/TreeFrameset> und nach der passenden Klasse und/oder dem passenden Attribut suchen, siehe Abbildung 4-5. Alternativ kann eine Textsuche über <https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/SearchFrameset> durchgeführt werden. Wenn Sie z. B. die IEC-ID für „Temperaturtyp“ (<https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/PropertiesAllVersions/0112-2---61360_4%23AAE683>) finden möchten, scrollen Sie entweder auf der Website nach unten oder führen Sie eine Textsuche über das entsprechende Suchwort durch. Klicken Sie auf das Suchergebnis, das Ihrer Meinung nach am besten zu Ihrer Suche passt.

![A screenshot of a computer AI-generated content may be incorrect.](media/f1ee0f14a968f40345a4f1dff1f47c8e.png)

Abbildung 4-5: Suche nach IEC-IRDIs

**Schritt 4**: Auswahl des IEC IRDI für die gewählte Property, siehe Abbildung 4-6

![A screenshot of a computer AI-generated content may be incorrect.](media/881dfae4b52f621e84bb05ffdaf53076.png)

Abbildung 4-6: IEC-IRDI für eine Property

**Schritt 5**: Das ausgewählte IRDI kann nun als semantische Referenz an entsprechender Stelle (z.B. als *semanticId*, *referredSemanticId, valueId*) in der VWS eingefügt werden. Siehe Abbildung 4-7 als Beispiel die Verwendung für ProductClassId

![Ein Bild, das Text, Zahl, Schrift, Reihe enthält. KI-generierte Inhalte können fehlerhaft sein.](media/b003751559f0f01404e7e64540b09ece.png)

Abbildung 4-7: ProductClassId mit IEC-IRDI Referenz

##### Vordefinierte Daten aus dem IEC-CDD

Typisch anwendbare Attribute für spezielle Themen wie Farben, Materialien, Schutzklassen, etc. finden sich im IEC-CDD in gut ausdefinierter Form. Im Folgenden eine auszugsweise Auflistung.

Colour properties

| Applicable properties:                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Enumeration code list:                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [0112/2///61360_4\#AAF250 - insulation colour code](https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/PropertiesAllVersions/0112-2---61360_4%23AAF250?opendocument) [0112/2///61360_4\#AAH065 - housing colour code](https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/PropertiesAllVersions/0112-2---61360_4%23AAH065?opendocument) [0112/2///61360_7\#CBA018 - IEC colour code of item](https://cdd.iec.ch/cdd/common/iec61360-7.nsf/PropertiesAllVersions/0112-2---61360_7%23CBA018?opendocument)  | [0112/2///61360_7\#CEA012 - IEC colour codes:](https://cdd.iec.ch/cdd/common/iec61360-7.nsf/EnumerationsAllVersions/0112-2---61360_7%23CEA012)  N.A., BK, BN, RD, OG, GN, YE, BU, VT, GY, WH, PK, GD, TQ, SR, GNYE, BKBN, BKRD, BKOG, BKGN, BKVT, BKGY, BKWH, BKPK, BKGD, BKTQ, BKSR, BRRD, BROG, BRBU, BRVT, BRGY, BRWH, BRPK, BRGD, BRTK, BRSR, RDOG, RDBU, RDVT, RDGY, RDWH, RDPK, RDGD, RDTQ, RDSR, OGBU, OGVT, OGGY, OGWH, OGPK, OGGD, OGTQ, OGSR, BUVT, BUGY, BUWH, BUPK, BUGD, BUTQ, BUSR, VTGY, VTWH, VTPK, VTGD, VTTQ, VTSR, GYWH, GYPK, GYGD, GYTQ, GYSR, WHPK, WHGD, WHTQ, WHSR, PKGD, PKTQ, PKSR, GDTQ, GDSR, TQSR, OTHERS |
| [0112/2///61360_4\#AAF128 - package colour](https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/PropertiesAllVersions/0112-2---61360_4%23AAF128?opendocument)                                                                                                                                                                                                                                                                                                                                      | BG, BK, BL, BN, BZ, GN, GY, IV, NC, OR, PK, RD, TN, VT, WT, YL                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |

Tabelle 4-10: IEC Colour properties

Conductor properties

| Applicable properties:                                                                                                                                                                                          | Enumeration code list:                                                                                           |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------|
| [0112/2///61360_4\#AAF243 - conductor configuration](https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/PropertiesAllVersions/0112-2---61360_4%23AAF243?opendocument)                                                 | BRAID, BUNCH, LITZ, SOLID, STRAND, TINSEL                                                                        |
| [0112/2///61360_4\#AAJ018 - sealing class](https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/PropertiesAllVersions/0112-2---61360_4%23AAJ018?opendocument)                                                           | DUSTP, OPEN, SEAL                                                                                                |
| ![](media/09cb0048f6a36c977c45fbf1f8a75e76.gif)[0112/2///61360_4\#AAH056 - body insulation material](https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/PropertiesAllVersions/0112-2---61360_4%23AAH056?opendocument) | CER, GLS, PLA                                                                                                    |
| [0112/2///61360_4\#AAF248 - insulating material](https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/PropertiesAllVersions/0112-2---61360_4%23AAF248?opendocument)                                                     | ECTFE, ENAM, E/TFE, FEP, PA, PAPER, PE, PFA, POLY, PP, PTFE, PUR, PVC, RUBBER, TEXTILE, UP                       |
| ![](media/09cb0048f6a36c977c45fbf1f8a75e76.gif)[0112/2///61360_4\#AAF241 - conductive material](https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/PropertiesAllVersions/0112-2---61360_4%23AAF241?opendocument)      | Al, Cu, CuCd, CuCdCr, CuCr, CuNi, CuSn, CuZn, Fe/Cu                                                              |
| ![](media/09cb0048f6a36c977c45fbf1f8a75e76.gif)[0112/2///61360_4\#AAF240 - conductor finish](https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/PropertiesAllVersions/0112-2---61360_4%23AAF240?opendocument)         | Ag, Ni, Sn                                                                                                       |
| [0112/2///61360_4\#AAR025 - contact material](https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/PropertiesAllVersions/0112-2---61360_4%23AAR025?opendocument)                                                        | Ag, AgCdO, AgCdO/Au, AgNi, AgNi/Au, AgPd, AgPd/Au, AgSnO2, AgSnO2/Au, AgW, Ag/Au, AuAg, PdCu, PdNi, Rh, Rh/Au, W |
| ![](media/09cb0048f6a36c977c45fbf1f8a75e76.gif)[0112/2///61360_4\#AAE355 - contact body material](https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/PropertiesAllVersions/0112-2---61360_4%23AAE355?opendocument)    | BeCu, Cu, CuSn, CuZn, Ni, PCuSn                                                                                  |
| ![](media/09cb0048f6a36c977c45fbf1f8a75e76.gif)[0112/2///61360_4\#AAE350 - contact finish](https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/PropertiesAllVersions/0112-2---61360_4%23AAE350?opendocument)           | Ag, Au, CuZn, Ni, PCuSn, Pd, Sn, Zn                                                                              |
| ![](media/09cb0048f6a36c977c45fbf1f8a75e76.gif)[0112/2///61360_4\#AAE351 - housing material](https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/PropertiesAllVersions/0112-2---61360_4%23AAE351?opendocument)         | CER, DAP, MET, PA, PC, PLA, PPOX, PTFE                                                                           |
| [0112/2///61360_4\#AAH005 - housing finish](https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/PropertiesAllVersions/0112-2---61360_4%23AAH005?opendocument)                                                          | Ag, Au, Cr, ELOX, LAC, Ni, PLA, RAW, RUB, Sn, Zn                                                                 |
| ![](media/09cb0048f6a36c977c45fbf1f8a75e76.gif)[0112/2///61360_4\#AAE634 - terminal material](https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/PropertiesAllVersions/0112-2---61360_4%23AAE634?opendocument)        | AgPd, NiSn                                                                                                       |
| [0112/2///61360_4\#AAH028 - terminal finish](https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/PropertiesAllVersions/0112-2---61360_4%23AAH028?opendocument)                                                         | Ag, Au, Cr, Ni, Pd, RAW, Sn                                                                                      |

Tabelle 4-11: IEC Conductor properties

Mechanical properties

| Applicable properties:                                                                                                                                                                                                                                                                                                                                                                                                                                                             | Enumeration code list:                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [0112/2///61360_4\#AAH011 - designation of IP protection](https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/PropertiesAllVersions/0112-2---61360_4%23AAH011?opendocument) [0112/2///61360_7\#CBA025 - IP code](https://cdd.iec.ch/cdd/common/iec61360-7.nsf/PropertiesAllVersions/0112-2---61360_7%23CBA025?opendocument) [0112/2///61987\#ABA558 - degree of protection (IP)](https://cdd.iec.ch/cdd/iec61987/iec61987.nsf/PropertiesAllVersions/0112-2---61987%23ABA558?opendocument) | [0112/2///61360_7\#CEA015](https://cdd.iec.ch/cdd/common/iec61360-7.nsf/EnumerationsAllVersions/0112-2---61360_7%23CEA015?opendocument)  IP00, IP01, IP02, IP03, IP04, IP05, IP06, IP07, IP08, IP10, IP11, IP12, IP13, IP14, IP15, IP16, IP17, IP18, IP20, IP21, IP22, IP23, IP24, IP25, IP26, IP27, IP28, IP30, IP31, IP32, IP33, IP34, IP35, IP36, IP37, IP38, IP40, IP41, IP42, IP43, IP44, IP45, IP46, IP47, IP48, IP50, IP51, IP52, IP53, IP54, IP55, IP56, IP57, IP58, IP60, IP61, IP62, IP63, IP64, IP65, IP66, IP67, IP68, IP69, IPX1, IPX2, IPX3, IPX4, IPX5, IPX6, IPX7, IPX8, IP1X, IP2X, IP3X, IP4X, IP5X, IP6X |

Tabelle 4-12: IEC Mechanical Properties

![](media/1f71b021e061a4948d69adc4ff10ccad.gif)[0112/2///62683\#ACC066 - Installation, mounting and dimensions](https://cdd.iec.ch/cdd/iec62683/iec62683.nsf/classesblocks/0112-2---62683%23ACC066)

[0112/2///63213\#KEA336 - max. height of the device](https://cdd.iec.ch/cdd/IECTC85/iec63213.nsf/PropertiesAllVersions/0112-2---63213%23KEA336?opendocument)

[0112/2///63213\#KEA337 - max. width of the device](https://cdd.iec.ch/cdd/IECTC85/iec63213.nsf/PropertiesAllVersions/0112-2---63213%23KEA337?opendocument)

[0112/2///63213\#KEA337 - max. width of the device](https://cdd.iec.ch/cdd/IECTC85/iec63213.nsf/PropertiesAllVersions/0112-2---63213%23KEA337?opendocument)

[0112/2///63213\#KEA321 - portable device](https://cdd.iec.ch/cdd/IECTC85/iec63213.nsf/PropertiesAllVersions/0112-2---63213%23KEA321?opendocument)

[0112/2///63213\#KEA322 - dimension of panel mounted device](https://cdd.iec.ch/cdd/IECTC85/iec63213.nsf/PropertiesAllVersions/0112-2---63213%23KEA322?opendocument)

[0112/2///63213\#KEA323 - number of modular spacings](https://cdd.iec.ch/cdd/IECTC85/iec63213.nsf/PropertiesAllVersions/0112-2---63213%23KEA323?opendocument)

[0112/2///63213\#KEA324 - housing device for DIN rail mounting](https://cdd.iec.ch/cdd/IECTC85/iec63213.nsf/PropertiesAllVersions/0112-2---63213%23KEA324?opendocument)

[0112/2///62683\#ACE801 - height of the device](https://cdd.iec.ch/cdd/iec62683/iec62683.nsf/PropertiesAllVersions/0112-2---62683%23ACE801?opendocument)

[0112/2///62683\#ACE802 - width of the device](https://cdd.iec.ch/cdd/iec62683/iec62683.nsf/PropertiesAllVersions/0112-2---62683%23ACE802?opendocument)

[0112/2///62683\#ACE803 - length of the device](https://cdd.iec.ch/cdd/iec62683/iec62683.nsf/PropertiesAllVersions/0112-2---62683%23ACE803?opendocument)

[0112/2///62683\#ACE804 - mounting onto standard rail](https://cdd.iec.ch/cdd/iec62683/iec62683.nsf/PropertiesAllVersions/0112-2---62683%23ACE804?opendocument)

[0112/2///62683\#ACE808 - product mass](https://cdd.iec.ch/cdd/iec62683/iec62683.nsf/PropertiesAllVersions/0112-2---62683%23ACE808?opendocument)

Power supply properties

[0112/2///62683\#AC531 - supply voltage limit](https://cdd.iec.ch/cdd/iec62683/iec62683.nsf/e0e56d2682a34311c12575560058dc1c/f9ac42311a67c29bc12584ec0072daba)

Identification properties

![](media/1f71b021e061a4948d69adc4ff10ccad.gif)[0112/2///61987\#ABC269 - Identification](https://cdd.iec.ch/cdd/iec61987/iec61987.nsf/classes/0112-2---61987%23ABC269)

[0112/2///61987\#ABA565 - name of manufacturer](https://cdd.iec.ch/cdd/iec61987/iec61987.nsf/PropertiesAllVersions/0112-2---61987%23ABA565?opendocument)

[0112/2///61987\#ABP463 - URI of company logo](https://cdd.iec.ch/cdd/iec61987/iec61987.nsf/PropertiesAllVersions/0112-2---61987%23ABP463?opendocument)

[0112/2///61987\#ABP462 - country of origin](https://cdd.iec.ch/cdd/iec61987/iec61987.nsf/PropertiesAllVersions/0112-2---61987%23ABP462?opendocument)

[0112/2///61987\#ABB064 - name of supplier](https://cdd.iec.ch/cdd/iec61987/iec61987.nsf/PropertiesAllVersions/0112-2---61987%23ABB064?opendocument)

[0112/2///61987\#ABA566 - type name of product](https://cdd.iec.ch/cdd/iec61987/iec61987.nsf/PropertiesAllVersions/0112-2---61987%23ABA566?opendocument)

[0112/2///61987\#ABP464 - family name of product](https://cdd.iec.ch/cdd/iec61987/iec61987.nsf/PropertiesAllVersions/0112-2---61987%23ABP464?opendocument)

[0112/2///61987\#ABA567 - model name of product](https://cdd.iec.ch/cdd/iec61987/iec61987.nsf/PropertiesAllVersions/0112-2---61987%23ABA567?opendocument)

[0112/2///61987\#ABA300 - code of product](https://cdd.iec.ch/cdd/iec61987/iec61987.nsf/PropertiesAllVersions/0112-2---61987%23ABA300?opendocument)

[0112/2///61987\#ABA950 - order code of product](https://cdd.iec.ch/cdd/iec61987/iec61987.nsf/PropertiesAllVersions/0112-2---61987%23ABA950?opendocument)

[0112/2///61987\#ABA581 - article number](https://cdd.iec.ch/cdd/iec61987/iec61987.nsf/PropertiesAllVersions/0112-2---61987%23ABA581?opendocument)

[0112/2///61987\#ABA587 - GTIN code](https://cdd.iec.ch/cdd/iec61987/iec61987.nsf/PropertiesAllVersions/0112-2---61987%23ABA587?opendocument)

[0112/2///61987\#ABA301 - national stock number](https://cdd.iec.ch/cdd/iec61987/iec61987.nsf/PropertiesAllVersions/0112-2---61987%23ABA301?opendocument)

[0112/2///61987\#ABP643 - device version](https://cdd.iec.ch/cdd/iec61987/iec61987.nsf/PropertiesAllVersions/0112-2---61987%23ABP643?opendocument)

[0112/2///61987\#ABA601 - software version](https://cdd.iec.ch/cdd/iec61987/iec61987.nsf/PropertiesAllVersions/0112-2---61987%23ABA601?opendocument)

[0112/2///61987\#ABA601 - software version](https://cdd.iec.ch/cdd/iec61987/iec61987.nsf/PropertiesAllVersions/0112-2---61987%23ABA601?opendocument)

[0112/2///61987\#ABA926 - hardware version](https://cdd.iec.ch/cdd/iec61987/iec61987.nsf/PropertiesAllVersions/0112-2---61987%23ABA926?opendocument)

[0112/2///61987\#ABB062 - fabrication number](https://cdd.iec.ch/cdd/iec61987/iec61987.nsf/PropertiesAllVersions/0112-2---61987%23ABB062?opendocument)

[0112/2///61987\#ABA951 - serial number](https://cdd.iec.ch/cdd/iec61987/iec61987.nsf/PropertiesAllVersions/0112-2---61987%23ABA951?opendocument)

[0112/2///61987\#ABN590 - URI of product instance](https://cdd.iec.ch/cdd/iec61987/iec61987.nsf/PropertiesAllVersions/0112-2---61987%23ABN590?opendocument)

[0112/2///61987\#ABN591 - URI of manufacturer](https://cdd.iec.ch/cdd/iec61987/iec61987.nsf/PropertiesAllVersions/0112-2---61987%23ABN591?opendocument)

[0112/2///61987\#ABP465 - URI of supplier](https://cdd.iec.ch/cdd/iec61987/iec61987.nsf/PropertiesAllVersions/0112-2---61987%23ABP465?opendocument)

[0112/2///61987\#ABB757 - date of manufacture](https://cdd.iec.ch/cdd/iec61987/iec61987.nsf/PropertiesAllVersions/0112-2---61987%23ABB757?opendocument)

[0112/2///61987\#ABB757 - date of manufacture](https://cdd.iec.ch/cdd/iec61987/iec61987.nsf/PropertiesAllVersions/0112-2---61987%23ABB757?opendocument)

#### VEC

Der Vehicle Electric Container (VEC)[^5] ist ein Beispiel für ein Industriestandard-Datenmodell, das für den Austausch von elektrischen Systeminformationen in der Automobil- und Transportbranche entwickelt wurde. Er wird von ProSTEP iViP entwickelt und gepflegt, einem Konsortium, das sich auf die Interoperabilität im technischen Datenaustausch konzentriert. Die Verwendung von VEC-Definitionen ist grundsätzlich kostenfrei, erfordert jedoch die Einhaltung der VDA- und prostep ivip-Nutzungsbedingungen sowie der technischen Spezifikationen.

[^5]: <https://ecad.prostep.org/ontologies/2024/03/vec>

VEC bietet ein strukturiertes Format für die Darstellung und den Austausch von elektrischen Kabelbaumdaten, einschließlich Komponenten, Verbindungen, Signalen, Geometrien und Metadaten. Seine Aufgabe ist es, die nahtlose Kommunikation zwischen verschiedenen CAD- und PLM-Systemen (Product Lifecycle Management) zu ermöglichen. VEC ist in der VDA-Empfehlung 4968 und der ProSTEP iViP-Empfehlung PSI21 definiert, in Form eines standardisierten Informationsmodells, eines Datenverzeichnisses, sowie eines XML-Schemas und einer Ontologie in “RDF 1.1 Turtle”-Syntax, die im VWS wie folgt genutzt werden kann:

**Schritt 1**: Öffnen der Datei: <https://ecad-wiki.prostep.org/specifications/vec/v210/vec-2.1.0-ontology.ttl>

**Schritt 2**: Drücken Sie Strg+F und suchen Sie nach dem gewünschten Begriff. Wenn z. B. nach Definitionen zur Temperatur gesucht wird, einfach nach „Temperatur“ suchen und die Trefferliste auf Eignung analysieren.

**![A yellow text on a black background AI-generated content may be incorrect.](media/72ab6f2582b1ae537198b8818a6de4ef.png)Schritt 3**: eines der Ergebnisse ist unten dargestellt. Die relevante VEC-Definition für die Suche wäre vec:TemperatureInformation, siehe Abbildung 4-8.

Abbildung 4-8: Suche nach Temperaturinformationen im VEC-Modell

Für die Verwendung innerhalb der VWS muss eine VWS-taugliche ID-Bildung definiert werden, z. B. in Form von IRIs (Internationalized Resource Identifier):

http://www.prostep.org/ontologies/ecad/2024/03/vec\#TemperatureType

http://www.prostep.org/ontologies/ecad/2024/03/vec\#InsulationSpecification

Listing 4-2: Referenzbeispiele zur Klassendefinitionen

http://www.prostep.org/ontologies/ecad/2024/03/vec\#PrimaryPartType_Wire

http://www.prostep.org/ontologies/ecad/2024/03/vec\#PrimaryPartType_PluggableTerminal

http://www.prostep.org/ontologies/ecad/2024/03/vec\#TemperatureType_AmbientTemperature

Listing 4-3: Referenzbeispieel für Enumerationswerte

http://www.prostep.org/ontologies/ecad/2024/03/vec\#itemVersionCompanyName

http://www.prostep.org/ontologies/ecad/2024/03/vec\#partVersionPrimaryPartType

http://www.prostep.org/ontologies/ecad/2024/03/vec\#partVersionPartNumber

http://www.prostep.org/ontologies/ecad/2024/03/vec\#partVersionPreferredUseCase

http://www.prostep.org/ontologies/ecad/2024/03/vec\#insulationSpecificationBaseColor

http://www.prostep.org/ontologies/ecad/2024/03/vec\#insulationSpecificationMaterial

http://www.prostep.org/ontologies/ecad/2024/03/vec\#conductorSpecificationCrossSectionArea

Listing 4-4: Referenzbeispiele für Properties

### Klassifizierungssysteme für Einheiten

**IEC 62720** bietet Definitionen für physikalische Einheiten, die auf den SI-Einheiten basieren und für den Datenaustausch in Lieferketten oder IoT-Systemen geeignet sind. Die IRDI-Referenzierungscodes können in der VWS über *semanticId* für einfache Einheitenreferenzierung verwendet werden. Die IEC 62720 ist auch in der IEC-CDD repräsentiert, und die Definitionen damit indirekt über URI-Verknüpfungen zugreifbar.

**ECLASS** bietet IRDI-Referenzcodes für physikalische SI-Einheiten an, verweist dabei aber grundsätzlich auf IEC 62720 als Definitionsquelle (siehe Abbildung 4-9).

![Ein Bild, das Text, Screenshot, Schrift, Zahl enthält. KI-generierte Inhalte können fehlerhaft sein.](media/8e5f9edc61f3a79ac687277576002856.png)

Abbildung 4-9: Datensatz zu einer Einheitendefinition in ECLASS

Zur Anwendung von ECLASS und Einheitendefinitionen in *Concept Descriptions* hat die IDTA eine Best-Practice-Guideline[^6] veröffentlicht [16] und dort die folgenden wesentlichen Zuordnungen festgelegt:

[^6]: [https://industrialdigitaltwin.org/wp-content/uploads/2024/10/2024-10_IDTA_ECLASS_Semantic_Transport_ECLASS_in_VWS_1.0.pdf](https://industrialdigitaltwin.org/wp-content/uploads/2024/10/2024-10_IDTA_ECLASS_Semantic_Transport_ECLASS_in_AAS_1.0.pdf)

-   \<*id*\> soll mit der IRDI der Property befüllt werden. Die Referenz auf die ConceptDescription wird dann im Submodel oder der Property über *semanticId* gesetzt.
-   \<*definition*\> soll mit dem Text aus der ECLASS-Definition der Property befüllt werden
-   \<*unit*\> soll den Namen der Einheit aus der ECLASS-Definition enthalten (z.B. „mm“)
-   \<*unitId*\> soll mit der IRDI der Einheit befüllt werden (z.B. „0173-1\#05-AAA480“)

Da es sich bei ECLASS ein proprietäres kostenpflichtiges Referenzsystem handelt und keine Verlinkung auf eine frei im Internet verfügbare Definitionsquelle möglich ist, wird empfohlen, eine frei verfügbare und kostenlose Alternative zu verwenden, die diese Einschränkungen nicht hat.

**QUDT** (Quantities, Units, Dimensions, and Types)[^7] ist ein weit verbreitetes und kostenfrei verfügbares Open-Source-Referenzierungssystem für physikalische Einheiten, Größen und Datentypen, das speziell für die semantische Modellierung und den Einsatz in digitalen Systemen entwickelt wurde. QUDT bietet eine detaillierte Ontologie für physikalische Größen, Einheiten, Dimensionen und Datentypen, die auf Standards wie dem SI-System, IEC 62720, ISO 80000 und anderen basiert. QUDT ist als RDF/OWL-Ontologie (Resource Description Framework / Web Ontology Language) implementiert, was es ideal für semantische Web-Anwendungen und digitale Zwillinge basierend auf der VWS macht. Ergänzend zu den IRDIs der IEC 62720 sind mit QUDT präzise, maschinenlesbare Verknüpfungen über URIs möglich (z. B. <http://qudt.org/vocab/unit/W> für Watt), sowie in die zugrundeliegende RDF-Ontologie (z. B. [http://qudt.org/vocab/unit\#W](http://qudt.org/vocab/unit#W) für Watt). In der folgenden Tabelle 4-13 findet sich eine Gegenüberstellung von Referenz-IDs für ausgewählte Einheiten.

[^7]: [https://qudt.org](https://qudt.org/2.1/vocab/unit)

| Physikalische Einheit   | ECLASS-Referenz   | IEC-Referenz                                                                                                      | QUDT-Referenz                                |
|-------------------------|-------------------|-------------------------------------------------------------------------------------------------------------------|----------------------------------------------|
| Spannung (Volt)         | 0173-1\#05-AAA153 | [0112/2///62720\#UAA296](https://cdd.iec.ch/cdd/iec62720/iec62720.nsf/Units/0112-2---62720%23UAA296)              | <http://qudt.org/vocab/unit/V>               |
| Stromstärke (Ampere)    | 0173-1\#05-AAA220 | [0112/2///62720\#UAA101](https://cdd.iec.ch/cdd/iec62720/iec62720.nsf/Units/0112-2---62720%23UAA101)              | <http://qudt.org/vocab/unit/A>               |
| Leistung (Watt)         | 0173-1\#05-AAA282 | [0112/2///62720\#UAA306](https://cdd.iec.ch/cdd/iec62720/iec62720.nsf/Units/0112-2---62720%23UAA306)              | <http://qudt.org/vocab/unit/W>               |
| Temperatur (Kelvin)     | 0173-1\#05-AAA064 | [0112/2///62720\#UAA185](https://cdd.iec.ch/cdd/iec62720/iec62720.nsf/Units/0112-2---62720%23UAA185)              | <http://qudt.org/vocab/unit/K>               |
| Temperatur (Celsius)    | 0173-1\#05-AAA567 | [0112/2///62720\#UAA033](https://cdd.iec.ch/cdd/iec62720/iec62720.nsf/Units/0112-2---62720%23UAA033)              | <http://qudt.org/vocab/unit/DEG_C>           |
| Temperatur (Fahrenheit) | 0173-1\#05-AAA739 | [0112/2///62720\#UAA039](https://cdd.iec.ch/cdd/iec62720/iec62720.nsf/Units/0112-2---62720%23UAA039)              | <http://qudt.org/vocab/unit/DEG_F>           |
| Distanz (Millimeter)    | 0173-1\#05-AAA480 | [0112/2///62720\#UAA862](https://cdd.iec.ch/cdd/iec62720/iec62720.nsf/Units/0112-2---62720%23UAA862?opendocument) | <http://qudt.org/vocab/unit/MilliM>          |
| Distanz (Meter)         | 0173-1\#05-AAA551 | [0112/2///62720\#UAA726](https://cdd.iec.ch/cdd/iec62720/iec62720.nsf/Units/0112-2---62720%23UAA726?opendocument) | <http://qudt.org/vocab/unit/M>               |
| Kraft (Newton)          | 0173-1\#05-AAA561 | [0112/2///62720\#UAA235](https://cdd.iec.ch/cdd/iec62720/iec62720.nsf/Units/0112-2---62720%23UAA235)              | <http://qudt.org/vocab/unit/N>               |
| Masse (Kilogramm)       | 0173-1\#05-AAA731 | [0112/2///62720\#UAA594](https://cdd.iec.ch/cdd/iec62720/iec62720.nsf/Units/0112-2---62720%23UAA594)              | http://qudt.org/vocab/unit/KiloGM            |
| Masse (Gramm)           | 0173-1\#05-AAA728 | [0112/2///62720\#UAA465](https://cdd.iec.ch/cdd/iec62720/iec62720.nsf/Units/0112-2---62720%23UAA465)              | <http://qudt.org/vocab/unit/GM>              |
| Fläche (mm²)            | 0173-1\#05-AAA295 | [0112/2///62720\#UAA871](https://cdd.iec.ch/cdd/iec62720/iec62720.nsf/Units/0112-2---62720%23UAA871)              | <https://qudt.org/vocab/unit/MilliM2>        |
| Stücke (Pieces)         | unknown           | [0112/2///62720\#UAD146](https://cdd.iec.ch/cdd/iec62720/iec62720.nsf/Units/0112-2---62720%23UAD146)              | <https://qudt.org/vocab/quantitykind/Count>  |

Tabelle 4-13: Referenzbeispiele für physikalische Einheiten mit ECLASS, IEC und QUDT

Wie im Best-Practice-Guideline der IDTA [16] beschrieben, muss in der VWS der Umweg über die *IEC61360 Data Descriptions* bzw. *Concept Descriptions* gegangen werden, um einem Property eine Einheit zuweisen zu können. Dort müssen zusätzlich zur *referenceId* mindestens die Einheitenbezeichner oder -symbole hinterlegt werden, damit die Viewer-Tools diese anzeigen können, siehe Abbildung 4-10.

![Ein Bild, das Text, Screenshot, Zahl, Software enthält. KI-generierte Inhalte können fehlerhaft sein.](media/d1479eeca3bfec077c51026f9f17dc8d.png)

Abbildung 4-10: Beispiel zur Einheiten-Referenzierung in einer Concept Description

### Klassifizierungssysteme für Dokumente

Das SM *HandoverDocumentation* nutzt die im Folgenden kurz beschriebenen Klassifizierungssysteme für Dokumente, siehe Abbildung 4-11.

![Ein Bild, das Text, Screenshot, Schrift, Zahl enthält. KI-generierte Inhalte können fehlerhaft sein.](media/e395550ee9808e20e63fa5931cf530fa.png)

Abbildung 4-11: Klassifizierung des Dokuments „Drawing“ im SM HandoverDocumentation

#### VDI 2770

VDI 2770 Blatt 1:2020-04 definiert Mindestanforderungen an digitale Herstellerinformationen für die Prozessindustrie, ist jedoch branchenübergreifend anwendbar. Der Zweck ist, die digitale Dokumentation von Maschinen und Anlagen zu standardisieren, insbesondere für die Übergabe von Herstellerinformationen an Betreiber.

In der SMC „*DocumentClassificationItem*“ ist der Wert von „*ClassificationSystem*“ auf „*VDI2770 Blatt 1:2020*“ zu setzen und der Wert von „*ClassId*“ auf einen der Zahlencodes aus der nachstehenden Tabelle 4-14 einzustellen:

| ClassID  | ClassName (EN)                    | ClassName (DE)                          |
|----------|-----------------------------------|-----------------------------------------|
| 01-01    | Identification                    | Identifikation                          |
| 02-01    | Technical specification           | Technische Spezifikation                |
| 02-02    | Drawings, plans                   | Zeichnungen, Pläne                      |
| 02-03    | Assemblies                        | Bauteile                                |
| 02-04    | Certificates, declarations        | Zeugnisse, Zertifikate, Bescheinigungen |
| 03-01    | Commissioning, de-commissioning   | Montage, Demontage                      |
| 03-02    | Operation                         | Bedienung                               |
| 03-03    | General safety                    | Allgemeine Sicherheit                   |
| 03-04    | Inspection, maintenance, testing  | Inspektion, Wartung, Prüfung            |
| 03-05    | Repair                            | Instandsetzung                          |
| 03-06    | Spare parts                       | Ersatzteile                             |
| 04-01    | Contract documents                | Vertragsunterlagen                      |

Tabelle 4-14: DocumentClassification according to VDI 2770 Blatt 1: 2020

#### IEC 61355

Die IEC 61355-1:2008 befasst sich mit der Klassifikation und Kennzeichnung von Dokumenten für Anlagen, Systeme und Ausrüstungen. Sie bietet ein standardisiertes System zur Strukturierung und Kategorisierung technischer Dokumentationen, um deren Verwaltung, Auffindbarkeit und Austausch zu erleichtern. Der Fokus liegt auf Dokumenten in der Industrie, insbesondere in der Elektrotechnik, Anlagenbau und Prozessindustrie.

Die IEC 61355-Datenbank[^8] kann als direkte Referenz für die Klassifikation von Dokumentenarten (DCC-Codes) und Metadaten dienen, um eine einheitliche Dokumentenverwaltung zu gewährleisten, z.B.

[^8]: <https://std.iec.ch/iec61355/iec61355.nsf>

-   Data sheet (DA): <https://std.iec.ch/iec61355/iec61355.nsf/(SysSymbolEN)/D00178>
-   Operating manual (DC): <https://std.iec.ch/iec61355/iec61355.nsf/(SysSymbolEN)/D00034>
-   Requirement specification (EC): <https://std.iec.ch/iec61355/iec61355.nsf/(SysSymbolEN)/D00035>
-   Technical Drawing (ED): <https://std.iec.ch/IEC61355/iec61355.nsf/(sysSymbolEn)/D00032>

Im Folgenden eine tabellarische Zusammenstellung der in der IEC 61355 definierten Codes[^9]. Der Wert von „*ClassificationSystem*“ ist auf „*IEC 61355-1:2008*“ zu setzen und der Wert von „*ClassId*“ auf einen der Buchstabencodes aus der nachstehenden Tabelle 4-14 einzustellen:

[^9]: <https://en.wikipedia.org/wiki/IEC_61355>

| ClassID  | ClassName (DE)                                                        | ClassName (EN)                                                          |
|----------|-----------------------------------------------------------------------|-------------------------------------------------------------------------|
| A        | Dokumentationsbeschreibende Dokumente                                 | Documentation describing documents                                      |
| AA       | Verwaltungstechnische Dokumente                                       | Administrative documents                                                |
| AB       | Listen (Dokumente betreffend)                                         | Lists (regarding documents)                                             |
| AC       | Erläuternde Dokumente (Dokument betreffend)                           | Explanatory documents (regarding documents)                             |
| B        | Managementdokumente                                                   | Management documents                                                    |
| BB       | Berichte                                                              | Reports                                                                 |
| BC       | Schriftwechsel                                                        | Correspondence                                                          |
| BD       | Projektleitungsdokumente                                              | Project control documents                                               |
| BE       | Ressourcenplanungsdokumente                                           | Resource planning documents                                             |
| BF       | Versand-, Lager- und Transportdokumente                               | Dispatch, storage and transport documents                               |
| BG       | Standortplanungs- und Standortorganisationsdokumente                  | Site planning and site organization documents                           |
| BH       | Dokumente zum Änderungswesen                                          | Documents regarding changes                                             |
| BS       | Objektschutzdokumente                                                 | Security documents                                                      |
| BT       | Schulungsdokumente                                                    | Training specific documents                                             |
| C        | Vertragliche und nicht-technische Dokumente                           | Contractual and non-technical documents                                 |
| CA       | Anfrage-, Kalkulations- und Angebotsdokumente                         | Inquiry, calculation and offer documents                                |
| CB       | Genehmigungsdokumente                                                 | Approval documents                                                      |
| CC       | Vertragliche Dokumente                                                | Contractual documents                                                   |
| CD       | Bestell- und Lieferdokumente                                          | Order and delivery documents                                            |
| CE       | Rechnungsdokumente                                                    | Invoice documents                                                       |
| CF       | Versicherungsdokumente                                                | Insurance documents                                                     |
| CG       | Gewährleistungsdokumente                                              | Warranty documents                                                      |
| CH       | Gutachten                                                             | Expertises                                                              |
| D        | Dokumente mit allgemeiner technischer Information                     | General technical information documents                                 |
| DA       | Datenblätter                                                          | Data sheets                                                             |
| DB       | Erläuternde Dokumente                                                 | Explanatory documents                                                   |
| DC       | Anleitungen und Handbücher                                            | Instructions and manuals                                                |
| DD       | Technische Berichte                                                   | Technical reports                                                       |
| DE       | Kataloge, Werbeschriften                                              | Catalogues Advertising documents                                        |
| DF       | Technische Veröffentlichungen                                         | Technical publications                                                  |
| E        | Dokumente für technische Anforderungen und Auslegung                  | Technical requirement and dimensioning documents                        |
| EA       | Dokumente über gesetzliche Anforderungen                              | Legal requirement documents                                             |
| EB       | Normen und Richtlinien                                                | Standards and regulations                                               |
| EC       | Technische Spezifikations- / Anforderungsdokumente                    | Technical specification / requirement documents                         |
| ED       | Dimensionierungsdokumente                                             | Dimensioning documents                                                  |
| F        | Funktionsbeschreibende Dokumente                                      | Function describing documents                                           |
| FA       | Funktionsübersichtsdokumente                                          | Functional overview documents                                           |
| FB       | Fließschemata                                                         | Flow diagrams                                                           |
| FC       | Dokumente der MMS-Gestaltung (Mensch-Machine-Schnittstelle)           | MMI layout documents (MMI = man-machine interface)                      |
| FE       | Funktionsbeschreibungen                                               | Function descriptions                                                   |
| FF       | Funktionsschaltpläne                                                  | Function diagrams                                                       |
| FP       | Signalbeschreibungen                                                  | Signal descriptions                                                     |
| FQ       | Einstellwertdokumente                                                 | Setting value documents                                                 |
| FS       | Schaltkreisdokumente                                                  | Circuitry documents                                                     |
| FT       | Softwarespezifische Dokumente                                         | Software specific documents                                             |
| L        | Ortsbeschreibende Dokumente                                           | Location documents                                                      |
| LA       | Erschließungs- und Vermessungsdokumente                               | Exploitation and survey documents                                       |
| LB       | Erdbau- und Fundamentbaudokumente                                     | Earthwork and foundation work documents                                 |
| LC       | Rohbaudokumente                                                       | Building carcass documents                                              |
| LD       | Dokumente, die Orte an Standorten beschreiben                         | On-site location documents                                              |
| LH       | Orte in Gebäuden (Schiffen, Flugzeugen, etc.) beschreibende Dokumente | In-building location documents (also applied for ships, aircraft, etc.) |
| LU       | Orte in/auf Einrichtungen beschreibende Dokumente                     | In/on-equipment location documents                                      |
| M        | Verbindungsbeschreibende Dokumente                                    | Connection describing documents                                         |
| MA       | Verbindungsbezogene Dokumente                                         | Connection documents                                                    |
| MB       | Verkabelungs- und Rohrleitungsdokumente                               | Cabling or piping documents                                             |
| P        | Objektlisten                                                          | Object listings                                                         |
| PA       | Materiallisten                                                        | Material lists                                                          |
| PB       | Teilelisten                                                           | Parts lists                                                             |
| PC       | Stücklisten                                                           | Item lists                                                              |
| PD       | Produktlisten und Produkttypenlisten                                  | Product lists and product type lists                                    |
| PF       | Funktionslisten                                                       | Function lists                                                          |
| PL       | Ortslisten                                                            | Location lists                                                          |
| Q        | Qualitätsmanagementdokumente und sicherheitsbeschreibende Dokumente   | Quality management documents; safety-describing documents               |
| QA       | Qualitätsmanagementdokumente                                          | Quality management documents                                            |
| QB       | Sicherheitsbeschreibende Dokumente                                    | Safety-describing documents                                             |
| QC       | Qualitätsnachweisdokumente                                            | Quality verifying documents                                             |
| T        | Dokumente zur Beschreibung geometrischer Formen                       | Geometry-related documents                                              |
| TA       | Entwurfszeichnung                                                     | Planning drawings                                                       |
| TB       | Konstruktionszeichnungen                                              | Construction drawings                                                   |
| TC       | Fertigungs- und Errichtungszeichnungen                                | Manufacturing and erection drawings                                     |
| TL       | Anordnungszeichnung                                                   | Arrangement documents                                                   |
| W        | Betriebliche Protokolle und Aufzeichnungen                            | Operation records                                                       |
| WA       | Einstellwertdokumente                                                 | Set point documents                                                     |
| WT       | Logbücher                                                             | Logbooks                                                                |

Tabelle 4-15: Document classification according to IEC 61355

## AP 13.5 – Meta-Level AAS Designer

Im Zuge des Teilprojekts 12 erfolgte die begleitende Weiterentwicklung des AAS-Designers der Fa. Meta-level, um Komponenten-VWS anwenderfreundlicher anlegen, editieren und validieren zu können. Dabei wurde auch ein erstes Anwenderhandbuch für den AAS-Designer erstellt[^10].

[^10]: <https://github.com/VWS4LS/vws4ls-subproject-results/tree/main/TP12/VWS4LS_AAS_Designer_Manual.pdf>

Die im Folgenden beschriebenen Features wurden im Kontext des TP12 angeregt und implementiert.

### Import von semantischen IDs aus Referenzkatalogen

Zur Sicherstellung der semantischen Interoperabilität sind die Verwendungen von allgemein bekannten semantischen IDs aus Referenzkatalogen wie ECLASS von entscheidender Bedeutung. Um die Zuweisung von solchen IDs für den Anwender so einfach wie möglich zu gestalten, wurde die Möglichkeit geschaffen, IDs direkt bei der Erstellung aus einer Auswahlliste zu wählen und zu filtern. Spezifisch für den Einsatz in der Leitungssatzfertigung wurde zudem die Ontologie vom VEC als Referenzsystem hinzugefügt.

Für die folgenden Elemente können Semantische IDs nun direkt ausgewählt werden:

**Properties**

Für *Properties (Eigenschaft: valueId)* können Wertereferenzen aus Referenzkatalogen importiert werden, siehe Abbildung 4-12. Abbildung 4-13 zeigt den Auswahldialog für mögliche Wertereferenzen aus dem VEC-Katalog.

![Ein Bild, das Text, Screenshot, Reihe, Schrift enthält. KI-generierte Inhalte können fehlerhaft sein.](media/ca8cfead8f4aee03ee6847cb5c79cf88.png)

Abbildung 4-12: Suche nach Wertereferenzen in Referenzkatalogen

![Ein Bild, das Text, Screenshot, Software, Zahl enthält. KI-generierte Inhalte können fehlerhaft sein.](media/c92d689d554f923d55f9e0217b8f1be1.png)

Abbildung 4-13: Import von Wertereferenzen aus der VEC-Ontologie

**Concept Descriptions**

In *ConceptDescriptions* (Eigenschaft: *unitId*) können Einheitenreferenzen aus Referenzkatalogen zugewiesen und Inhalte daraus importiert werden (ECLASS, QUDT, SI-Units). In Abbildung 4-14 ff. werden die unterschiedlichen Auswahlmöglichkeiten für Einheiten aus den Referenzkatalogen dargestellt.

![Ein Bild, das Text, Screenshot, Zahl, Schrift enthält. KI-generierte Inhalte können fehlerhaft sein.](media/3ab9ca500d59756d147dc35828fbba9c.png)

Abbildung 4-14: Suche nach Einheitenreferenzen in Referenzkatalogen

![Ein Bild, das Text, Screenshot, Software, Zahl enthält. KI-generierte Inhalte können fehlerhaft sein.](media/337cbfd5e9800d2a3753fc7b40a048a0.png)

Abbildung 4-15: Import von Einheiten aus QUDT.org

![Ein Bild, das Text, Screenshot, Zahl, Schrift enthält. KI-generierte Inhalte können fehlerhaft sein.](media/08c1af26a2dde427e3e10eafcfbddeb9.png)

Abbildung 4-16: Import von Einheiten aus SI-Units

![Ein Bild, das Text, Screenshot, Software, Zahl enthält. KI-generierte Inhalte können fehlerhaft sein.](media/b4d81d142d78ea24b1d344fd5242586b.png)

Abbildung 4-17: Verweise auf weitere Referenzkataloge

### Handover Documentation-Wizard

Die Bereitstellung von Übergabedokumentationen in Verwaltungsschalen ist einer der grundlegendsten Funktionen, die durch Anwender auf verständliche Weise genutzt werden. Um den Einstieg so einfach wie möglich zu gestalten, bietet es sich an, die Dokumentenbereitstellung direkt über die Weboberfläche zu ermöglichen.

Hierfür wurde die vereinfachte Anlage von Elementen im Teilmodell *HandoverDocumentation hinzugefügt.* So ist es jetzt möglich Dokumente direkt über die Weboberfläche hochzuladen und mit semantischen Informationen anzureichern. Abbildung 4-18 zeigt exemplarisch die Eingabemaske für die Neuanlage von Dokumenten.

![Ein Bild, das Text, Screenshot, Software, Computersymbol enthält. KI-generierte Inhalte können fehlerhaft sein.](media/87b9bb14575ca5264405002f425b6e30.png)

Abbildung 4-18: Wizard HandoverDocumentation im AAS-Designer

### Auswahl des ContentType

Bei angehängten oder verlinkten Dateireferenzen ist es wichtig, den korrekten Dateityp (mime type) anzugeben, siehe Abbildung 4-19. Deshalb wurde ein Feature implementiert, welches anhand der Dateinamenserweiterung einen passenden [MimeType](https://www.iana.org/assignments/media-types/media-types.xhtml)[^11] vorauswählt, z.B.:

[^11]: <https://www.iana.org/assignments/media-types/media-types.xhtml>

![Ein Bild, das Text, Screenshot, Schrift, Reihe enthält. KI-generierte Inhalte können fehlerhaft sein.](media/d1de3b957afe9349703ce488ed169795.png)

Abbildung 4-19: ContentType

### ID-Validation

Die konsistente Befüllung und Pflege von IDs in einer Verwaltungsschale ist ein fehlerträchtiger Prozess, insbesondere wenn dieser manuell ausgeführt wird und keine geeignete Toolunterstützung vorhanden ist. Für den AAS-Designer wurde deswegen eine Konsistenzprüfung mit dem Feature “Validate IDs” ergänzt. Abbildung 4-20 zeigt exemplarisch die Ergebnisse eines solchen Prüfvorgangs.

![Ein Bild, das Text, Screenshot, Software, Computersymbol enthält. KI-generierte Inhalte können fehlerhaft sein.](media/82d88497cb4ebbb7f38e3ae92e54d1e0.png)![Ein Bild, das Text, Screenshot, Schrift, Zahl enthält. KI-generierte Inhalte können fehlerhaft sein.](media/2265155704fbcbe9c61d84ec39f59442.png)

Abbildung 4-20: Ergebnis einer ID-Validierung im AAS-Designer

### Auswahllisten für Produkthierarchien

Produkthierarchien sind per Definition mehrstufig und insbesondere bei umfangreichen Verwaltungsschalen-Repositories ohne Hilfsmittel nur schwer zu verwalten. Um die Handhabung zu vereinfachen, wurde der AAS-Designer um die Möglichkeit zum Verwalten von Eigenschaften der Produkthierarchie im *DigitalNameplate* (*ManufacturerProductRoot*, *ManufacturerProductFamily, ManufacturerProductDesignation*) ergänzt. Die folgende Abbildung 4-21 zeigt exemplarisch eine Definition der Produktfamilien.

![Ein Bild, das Text, Screenshot, Zahl, Software enthält. KI-generierte Inhalte können fehlerhaft sein.](media/2d31b90d413589a1dcc704cc7cf47048.png)

Abbildung 4-21: Vorauswahllisten Produkthierarchie im AAS-Designer

### ConceptDescription-Management

Um die semantische Eindeutigkeit zu gewährleisten, werden eine Reihe von *ConceptDescriptions* verwendet. Um die Einrichtung neuer Werte und den damit verbundenen Suchaufwand für *ConceptDescriptions* zu minimieren, muss die Auffindbarkeit sichergestellt werden.

Hierfür wurde die Verwaltung von *ConceptDescriptions* im AAS-Designer deutlich verbessert, indem diese im ausgewählte AAS-Repository über eine such- und sortierbare Tabelle bearbeitet und verwaltet werden können. Abbildung 4-22 zeigt exemplarisch eine Liste von *Concept Descriptions* mit den entsprechenden Suchschaltflächen und Sortieroptionen im AAS-Designer.

![Ein Bild, das Text, Screenshot, Software, Zahl enthält. KI-generierte Inhalte können fehlerhaft sein.](media/4a254693c7d4019f5920197fdb64d7c8.png)

Abbildung 4-22: ConceptDescriptions im AAS-Designer

## AP 13.6 – XITASO Mnestix Viewer

Im Zuge des Teilprojekts 12 erfolgte die begleitende Weiterentwicklung des Eclipse-basierten OpenSource-VWS-Viewers „[Mnestix](https://github.com/eclipse-mnestix/mnestix-browser)“[^12] um für Produktkataloge üblichen Such- und Filterfunktionen – insbesondere die Weiterentwicklung einzelner Viewer-Features zur optimalen Darstellung der Submodelle „*TechnicalData*“, „*HandoverDocumentation*“ und „*DigitalNameplate*“ in einem ansprechenden Produktkatalog-Erscheinungsbild. Der Mnestix-Viewer wurde daher auf vereinfachte Darstellung für den Anwendungsfall „Produktkatalog“ optimiert (siehe auch Kapitel 0).

[^12]: <https://github.com/eclipse-mnestix/mnestix-browser>

Die komplette Dokumentation, wie beispielsweise die Konfiguration eines sicheren Logins und eines Rollen-basierten Zugriffssystem[^13], findet sich [im respektiven GitHub Repository](https://github.com/eclipse-mnestix/mnestix-browser/blob/1.5.0-product-catalog/wiki/product-catalog.md)[^14]. Der Quellcode für das in TP12 entstandene Artefakt findet sich auf dem „Branch“ „1.5.0-product-catalog“ des GitHub Repositories[^15].

[^13]: <https://github.com/eclipse-mnestix/mnestix-browser/wiki/Role-Based-Access-Control>

[^14]: <https://github.com/eclipse-mnestix/mnestix-browser/blob/1.5.0-product-catalog/wiki/product-catalog.md>

[^15]: <https://github.com/eclipse-mnestix/mnestix-browser/tree/1.5.0-product-catalog>

### Funktionsweise

Technologisch gesehen ist der Mnestix AAS Viewer kein ausschließlich browserbasierter AAS-Client, d.h. der Webbrowser kommuniziert nicht direkt über die REST-API mit dem AAS-Server, sondern indirekt über das sog. Backend-for-Frontend. Dies schränkt potenziell die Anwendungsfreiheit ein, da nicht ohne Vorkonfiguration des Backends auf beliebige AAS-Server zugegriffen werden kann.

Dieser Ansatz ermöglicht es Unternehmen zu spezifizieren, auf welche Verwaltungsschalen die Nutzer am Ende Zugriff haben sollen. So können bspw. auch VWS Repositories angebunden werden, welche nur im internen Firmennetz erreichbar sind und ohne direkt die API zur Verfügung zu stellen. Zudem werden so Probleme mit „Cross-Origin Resource Sharing (CORS)“ umgangen, um den Nutzern einen möglichst einfachen Umgang mit der Software zu ermöglichen.

Produkte haben eine weltweit eindeutige **assetId**, die einer oder mehreren Anlagenverwaltungsschalen zugeordnet werden kann. Für viele Anwendungsszenarien ist es sinnvoll, zusätzlich einen DNS-Zugang über die **assetId** einzurichten und damit die Datenabfrage aus herkömmlichen Browseranwendungen zu ermöglichen, siehe Abbildung 4-23.

![Ein Bild, das Text, Screenshot, Schrift, Zahl enthält. KI-generierte Inhalte können fehlerhaft sein.](media/6a2e64284f81d174ff1639d76af3d754.png)

Abbildung 4-23: VWS Repository, Asset ID und DNS

Zum Beispiel wird d**ie assetId** <https://asset.coroplast.de/9-2611-35> **umgeleitet nach** <https://vws4ls.dev.mnestix.xitaso.net/asset/http%3A%2F%2Fasset.coroplast.de%2F9-2611-35>*.*

*Dort* wird die **aasId** <https://aas.coroplast.de/COROFLEX_9_2611_FHLR2GCB2G_35> ermittelt und im **Viewer-Link** Base64-codiert übergeben: [*https://vws4ls.dev.mnestix.xitaso.net/en/product/aHR0cHM6Ly9hYXMuY29yb3BsYXN0LmRlL0NPUk9GTEVYXzlfMjYxMV9GSExSMkdDQjJHXzM1*](https://vws4ls.dev.mnestix.xitaso.net/en/product/aHR0cHM6Ly9hYXMuY29yb3BsYXN0LmRlL0NPUk9GTEVYXzlfMjYxMV9GSExSMkdDQjJHXzM1)

### Bedienung

Die Bedienung des Mnestix-Produktkatalog-Viewers ist im Folgenden erläutert, wobei die folgenden grundsätzlichen Bedienelemente im Mnestix-Viewer zur Verfügung stehen (siehe Abbildung 4-24):

1.  Hamburger-Menu: Auswahl zwischen **Dashboard**, **AAS-Liste**, **Templates** und **Einstellungen**
2.  Breadcrumb mit Produkthierarchie und anwählbaren Bestandteilen
3.  Sprachauswahl
4.  Umschaltung zwischen **AAS View** und **Product View**.
5.  AASX-Datei herunterladen

![](media/259c7f71ea344f9d4eefc7bf42f40b78.png)

Abbildung 4-24: Mnestix Bedienelemente

Eine [openapi-Spezifikation](https://github.com/VWS4LS/vws4ls-subproject-results/blob/main/TP12/mnestix-openapi.yaml)[^16] wurde für Mnestix erstellt, siehe [im Swagger-Editor](https://editor.swagger.io/?url=https://raw.githubusercontent.com/VWS4LS/vws4ls-subproject-results/refs/heads/main/TP12/mnestix-openapi.yaml)[^17] in Abbildung 4-25: Mnestix API

[^16]: <https://github.com/VWS4LS/vws4ls-subproject-results/blob/main/TP12/mnestix-openapi.yaml>

[^17]: <https://editor.swagger.io/?url=https://raw.githubusercontent.com/VWS4LS/vws4ls-subproject-results/refs/heads/main/TP12/mnestix-openapi.yaml>

![Ein Bild, das Text, Screenshot, Zahl, parallel enthält. KI-generierte Inhalte können fehlerhaft sein.](media/d9129dc6aa9182d681cc9dc22faf9289.png)

Abbildung 4-25: Mnestix API

### Einstellungen

Die Einstellungen für Mnestix werden im Bereich Settings (Abbildung 4-26) vorgenommen. Hier lassen sich unter anderem Vorgaben für die Bildung von global eindeutigen IDs festlegen, sodass diese automatisch erzeugt werden. Diese Einstellungen werden in dem, beim Start von Mnestix hinterlegten Repository gespeichert, weswegen andere Tools u.U. diese VWSn anzeigen. Sie sind an dem Prefix „https://mnestix.com/aas/“ zu erkennen. Bei Änderungen kann es zu Problemen in Mnestix kommen.

![Ein Bild, das Text, Screenshot, Software, Webseite enthält. KI-generierte Inhalte können fehlerhaft sein.](media/107abd358f59aea4f5326a79f1981d53.png)

Abbildung 4-26: Mnestix Konfiguration Überblick

Nach betätigen von „EDIT ALL“ werden die Felder editierbar, Einstellungen werden nach betätigen von „SAVE ALL“ gespeichert, siehe Abbildung 4-27.

![Ein Bild, das Text, Screenshot, Software, Zahl enthält. KI-generierte Inhalte können fehlerhaft sein.](media/ba54f5a1e2516f591e5ea5ac36c11e3e.jpeg)

Abbildung 4-27: Mnestix Konfiguration Edit Mode

#### Datenquellen

Im Konfigurationsdialog „Data sources“ lassen sich die AAS-Repositories konfigurieren, die im Dashboard und der AAS-Liste zur Auswahl stehen sollen, siehe Abbildung 4-28.

![Ein Bild, das Text, Screenshot, Software, Computersymbol enthält. KI-generierte Inhalte können fehlerhaft sein.](media/2cf02b624fc32a98ea59d188ae81ee93.png)

Abbildung 4-28: Mnestix Konfiguration für “Data Sources”

### Dashboard

Dies ist der einstiegsdialog für den normalen Anwender, in dem entweder direkt ein Herstellerkatalog ausgewählt oder per Chatbot-Funktion eine katalogübergreifende Produktsuche durchgeführt werden kann, siehe Abbildung 4-29.

![Ein Bild, das Text, Screenshot, Software, Computersymbol enthält. KI-generierte Inhalte können fehlerhaft sein.](media/f4646715505d8f8085c61c31b0170491.jpeg)

Abbildung 4-29: Mnestix Dashboard

### Produktfilterung

Nach Auswahl eines Herstellerkatalogs kann in diesem Dialog innerhalb des ausgewählten Katalogs mit detaillierten Filtern sowie Tabellensortierung die Produktsuche gezielt verfeinert werden, siehe Abbildung 4-30.

![Ein Bild, das Text, Screenshot, Software, Computersymbol enthält. KI-generierte Inhalte können fehlerhaft sein.](media/94d5128795d4366be297401367e857b0.png)

Abbildung 4-30: Mnestix Produktfilterung

### Produktanzeige

In diesem Dialog wird das final ausgewählte Produkt angezeigt und ggf. die Interaktionselemente zu einem e-Shop bereitgestellt, siehe Abbildung 4-31.

![Ein Bild, das Text, Screenshot, Software enthält. KI-generierte Inhalte können fehlerhaft sein.](media/81e43fd1c62f8852af9c87b9df05d5cc.jpeg)

Abbildung 4-31: Mnestix Produktanzeige

## AP 13.7 – BaSyx

Eclipse BaSyx™ ist eine Middleware für Verwaltungsschalen und stellt neben Verwaltungsschalen-Repositories weitere Funktionalitäten für den Zugriff und Integration von Verwaltungsschalen in die Systemlandschaften zur Verfügung. Beispielsweise ein Web-Frontend für die Visualisierung von Verwaltungsschalen und eine REST API für den Datenzugriff auf die Verwaltungsschalen.

### Anpassungen in Eclipse BaSyx

Im Rahmen des Forschungsvorhabens wurden Anpassungen an der BaSyx Plattform vorgenommen, die im Folgenden kurz erläutert werden.

#### Basic Authentication für das BaSyx Web UI

Zur Verbesserung der Sicherheit wurde im Web UI von Eclipse BaSyx eine Basic Authentication[^18] eingeführt. Nutzername und Passwort können nun als Konfigurationsparameter direkt im UI konfiguriert werden, was die Handhabung im Betrieb vereinfacht, und eine einheitliche Zugangskontrolle ermöglicht.

[^18]: <https://en.wikipedia.org/wiki/Basic_access_authentication>

#### Query Language

Die Funktionalität des Systems wurde durch die Implementierung der Query-Endpunkte erweitert. Diese basieren auf Elasticsearch[^19] und erlauben eine performante und flexible Abfrage von Daten. Dadurch wird insbesondere die Suche innerhalb großer Datenmengen deutlich effizienter.

[^19]: <https://www.elastic.co/>

#### Design-Anpassungen im Web UI

Nach Rückmeldung von Projektmitgliedern wurde das Design des Web UIs überarbeitet. Es wurde ein neues, übersichtlicheres Hauptmenü eingeführt, welches das einfache Einbinden von Modulen ermöglicht hat. Ebenso wurden die Einstellungsseiten verbessert und Konfigurationen, etwa der verlinkten Repository- und Registry-URLs, in eigene Menüs zusammengefasst. Hilfestellungen wurden verbessert und klarer strukturiert, um die Nutzbarkeit des Web UI zu verbessern. Zudem wurden die Kontextmenüs vereinfacht, was die Bedienbarkeit insgesamt erhöht.

#### RBAC-Verbesserungen

Zur Optimierung der rollenbasierten Zugriffskontrolle (RBAC – Role-Based Access Control) wurde ein Update der eingesetzten Keycloak[^20]-Version durchgeführt. Zusätzlich wurde die teilmodellbasierte RBAC-Konfiguration verbessert, um eine präzisere und flexiblere Rechtevergabe zu ermöglichen. Dies trägt wesentlich zur Sicherheit und Skalierbarkeit der Anwendung bei.

[^20]: <https://www.keycloak.org/>

### BaSyx UI – Modul-Feature

Das Eclipse BaSyx™ Web UI ist eines der gängigen Werkzeuge zur Interaktion mit Verwaltungsschalen. Es bieten neben der Darstellung der Rohdaten aus der Verwaltungsschale auch die Möglichkeit eigene Visualisierungen für Teilmodelle modular anzudocken. Es ist somit eine geeignete Anwendung für verschiedene Nutzergruppen, die dedizierte Oberflächen für ihre jeweiligen Anwendungsfälle benötigen.

Für die Umsetzung anwendungsfallbezogener Applikationen müssen aktuell jedoch neue Applikationen entwickelt werden. Dies resultiert in einem hohen zeitlichen und finanziellen Aufwand. Grundfunktionen wie das Abfragen von Verwaltungsschalen und Teilmodellen sowie zugehörige Methoden müssen für jede Anwendung neu implementiert werden. Außerdem steigt die Komplexität für den Endnutzer, da dieser potenziell mit einer Vielzahl heterogener Anwendungen konfrontiert wird.

Um den Prozess der Erstellung und Nutzung von AAS-Applikationen zu homogenisieren, wurde im Rahmen von Teilprojekt 14 das sogenannte Modul-Feature konzipiert und umgesetzt. Module erlauben es eigene Anwendungen als Teil des BaSyx Web UIs zu realisieren. Diese können dynamisch dem Modul-Ordner hinzugefügt werden und sind anschließend im Hauptmenü des BaSyx UIs verfügbar (vgl. Abbildung 4-32). Eine vollständige Dokumentation für die Entwicklung eigener Module ist im BaSyx Wiki[^21] zu finden.

[^21]: <https://wiki.basyx.org/>

![Ein Bild, das Text, Schrift, Webseite, Website enthält. KI-generierte Inhalte können fehlerhaft sein.](media/6d58eab8adea00ff35d3ec0b1070fd71.png)

Abbildung 4-32 Hauptmenü zur Auswahl verfügbarer Module

Module werden wie das Web UI selbst in Vue.js[^22] entwickelt und können somit auf sämtliche Hilfsfunktionen und Composables (reaktive Methoden) aus der Kernanwendung zugreifen. Das bedeutet, dass Funktionalitäten - wie das Abfragen von Verwaltungsschalen oder die Anzeige von Teilmodellen wie „Hierarchical Structures enabling Bills of Materials“ - nicht neu implementiert werden müssen, sondern einfach wiederverwendet werden können. Das reduziert den Entwicklungsaufwand und führt zu einheitlichen Darstellungen für dieselben Konzepte. Auch für den Endnutzer des Moduls führt dies zu einer homogeneren Darstellung und bekannte Interaktionsmuster.

[^22]: <https://vuejs.org/>

Als Teil des Projektes wurden mehrere Module mit dem Modul-Feature umgesetzt. Diese werden in den Kapiteln „4.7.3 AAS-Editor „5.1.1 BaSyx UI – Leitungssatzherstellung (Demonstrator UI)“ und „0 Modul für Änderungsmanagement“ im Detail beschrieben.

### BaSyx UI – AAS Editor

Die Eclipse BaSyx™ Web UI ist eines der gängigen Werkzeuge zur Darstellung von Verwaltungsschalen. Es bietet neben der reinen Betrachtung von Verwaltungsschalen auch die Möglichkeit Werte einzelner Teilmodell-Elemente zu ändern. Es ist somit ein geeignetes Werkzeug, um Verwaltungsschalen zu sichten und Einsteiger an das Thema Verwaltungsschale heranzuführen.

Zum Erstellen neuer Verwaltungsschalen muss heute jedoch häufig auf Expertenwerkzeuge wie der Eclipse AASX Package Explorer™ oder Entwickler-Bibliotheken wie aas-core-works[^23] zurückgegriffen werden. Diese Werkzeuge und Bibliotheken erfordern jedoch ein relativ gutes Vorwissen und Erfahrung und sind für Neueinsteiger weniger geeignet.

[^23]: <https://github.com/aas-core-works>

Um der Übergang vom reinen Sichten zum Erstellen von Verwaltungsschalen für Neueinsteiger einfacher zu gestalten, wurden im Rahmen von TP12 und TP13 neue Anforderung an das Eclipse BaSyx™ Web UI gestellt, siehe Abbildung 333.

Als Kernanforderung soll es möglich sein, ohne tiefere Kenntnisse, eine neue Verwaltungsschale zu erstellen und mit neuen Teilmodellen anzureichern. Hierfür muss es auch möglich sein neue Teilmodell-Elemente zu erstellen. Mittels geführter Dialoge sollen die wesentlichen Eigenschaften vom Benutzer eingefordert werden.

Das Team vom Fraunhofer IESE hat diese Anforderungen aufgenommen und eine erste Version mit dem Eclipse BaSyx™ Web UI v2-250305 veröffentlicht. Weitere Ergänzungen sind in der Version v2-250417 hinzugekommen. Eine vollständige Dokumentation ist im BaSyx Wiki[^24] zu finden.

[^24]: <https://wiki.basyx.org/>

Der AAS-Editor ist nun Teil des Eclipse BaSyx™ Web UI und kann über den Ansichtsmodus "AAS-Editor" aktiviert werden. Wenn der Modus aktiviert wurde, sind eine Reihe von neuen Funktionen über die Benutzeroberfläche verfügbar.

![A screenshot of a computer AI-generated content may be incorrect.](media/1d649a68db7b63502cd97f3bb6e0dd30.png)

Abbildung 4-33: Umschalten zum AAS-Editor

#### Verwaltungsschale erstellen

Über das Kontextmenü neben der Suchschaltfläche kann eine neue Verwaltungsschale erstellt werden, siehe in Abbildung 4-34.

![A screenshot of a computer AI-generated content may be incorrect.](media/0df266d87513b68811610fe9377af7f9.png)

Abbildung 4-34: Neue Verwaltungsschale erstellen

Es erscheint ein Dialog, über den die wichtigsten Parameter für die Verwaltungsschale eingegeben bzw. ausgewählt werden können. Einige Inhalte werden automatisch erzeugt und vorbelegt, sodass die Anwender sich auf die inhaltlichen Werte konzentrieren können.

Der Dialog ist in mehrere Kategorien aufgegliedert:

**Details**

Im Detailbereich (vgl. Abbildung 4-35) werden zunächst die Kopfdaten der Verwaltungsschale festgelegt. Hierzu gehören die global eindeutige Verwaltungsschalen ID, sowie die menschenlesbare *idShort*, womit die Verwaltungsschale in der Auswahlliste erscheint. Die Verwaltungsschalen ID kann über die Schaltfläche **Generate IRI** neu erzeugt werden.

Der Anzeigename (engl. Display Name) und die Beschreibung (engl. Description) mitsamt Kategorie sind optional und können nach Bedarf hinzugefügt werden.

![A screenshot of a computer AI-generated content may be incorrect.](media/c8fd7c38b1771528d904a97060cb101d.png)

Abbildung 4-35: Anreicherung mit Informationen im Bereich „Details“

**Administrative Information**

Im Bereich *Administrative Information* (vgl. Abbildung 4-36) werden Informationen über die Version und den Ersteller hinterlegt. Diese Eingaben sind optional und können für den einfachen Einstieg vernachlässigt werden.

![A screenshot of a computer AI-generated content may be incorrect.](media/fdc854cabeb93deba47eac6d6e69881c.png)

Abbildung 4-36: Administrative Information

**Derivation**

Der Bereich *Derivation* (vgl. Abbildung 4-37) ist aktuell noch nicht implementiert und wird in einer zukünftigen Version unterstützt. In diesem Bereich wird es möglich sein eine Ableitungsbeziehung (derivedFrom) zu einer anderen Verwaltungsschale herzustellen. Diese Funktionalität ist u.a. für die Verwendung in Typ-Instanz-Beziehungen notwendig.

![A screenshot of a computer AI-generated content may be incorrect.](media/55d2d26f330c913e91d4587d299781f9.png)

Abbildung 4-37: Derivation

**Asset**

Im Bereich *Asset* (vgl. Abbildung 4-38) werden Informationen zum (physikalischen) Asset hergestellt. Hierfür ist zunächst die Angabe der Art des Assets (engl. Asset Kind) notwendig. Also, ob es sich um eine Instanz oder einen Typ handelt.

Zudem die Angabe einer global eindeutigen Asset ID, die auch über die Schaltfläche **Generate IRI** erzeugt werden kann und den Asset Typ (engl. Asset Type).

Optional kann hier auch noch eine Asset-Abbildung in Form einer angehängten Bilddatei (FILE) oder URL auf eine Bilddatei hinterlegt werden.

![A screenshot of a computer AI-generated content may be incorrect.](media/ed591d164dfb1c3f2c7401c6f3e42135.png)

Abbildung 4-38: Asset

Wenn alle Angaben vollständig sind, kann die Verwaltungsschale über die Schaltfläche **Save** gespeichert werden und erscheint in der Liste der Verwaltungsschalen. Abbildung 4-39 zeigt exemplarisch die Details einer erzeugte Verwaltungsschale.

![A screenshot of a phone AI-generated content may be incorrect.](media/1dcb75677984dd7376bc872d5a5d1519.png)

Abbildung 4-39: VWS4LS Demo VWS

Die Verwaltungsschale ist somit vollständig erstellt. Über das Kontextmenü (vgl. Abbildung 4-40) kann eine Verwaltungsschale bearbeitet oder ergänzt werden.

![A screenshot of a computer AI-generated content may be incorrect.](media/162bcf892f6a168d923d5877540b19f9.png)

Abbildung 4-40: Kontextmenü zum Bearbeiten einer Verwaltungsschale

#### Teilmodell erstellen

Um eine Verwaltungsschale mit Inhalten zu füllen, sind Teilmodelle erforderlich. Diese können nach der Auswahl der Verwaltungsschale über das Kontextmenü im Inhaltsbereich erstellt werden (vgl. Abbildung 4-41).

![A screenshot of a computer AI-generated content may be incorrect.](media/3c4282c00b29e412af15f3ed59ba9318.png)

Abbildung 4-41: Neues Teilmodell erstellen

Ähnlich wie beim Erstellen neuer Verwaltungsschalen erscheint ein Dialog, in dem diverse Parameter eingegeben werden können. Einige Inhalte werden automatisch erzeugt und vorbelegt, sodass die Anwender sich auf die inhaltlichen Werte konzentrieren können.

Der Dialog ist in mehrere Kategorien aufgegliedert:

**Details**

Im Detailbereich (vgl. Abbildung 4-42) werden zunächst die Kopfdaten des Teilmodells festgelegt. Hierzu gehören die global eindeutige Teilmodell ID, sowie die menschenlesbare *IdShort*, womit das Teilmodell in der Auswahlliste erscheint. Die Teilmodell ID kann über die Schaltfläche **Generate IRI** neu erzeugt werden.

Der Anzeigename (engl. Display Name) und die Beschreibung (engl. Description) mitsamt Kategorie sind optional und können nach Bedarf hinzugefügt werden.

![A screenshot of a computer AI-generated content may be incorrect.](media/9c7cbc176f8dd15fa4a9ff1a5c632458.png)

Abbildung 4-42: Submodel Editor - Details

**Administrative Information**

Im Bereich *Administrative Information* (vgl. Abbildung 4-43 werden Informationen über die Version und den Ersteller hinterlegt. Diese Eingaben sind optional und können für den einfachen Einstieg vernachlässigt werden.

![A screenshot of a computer AI-generated content may be incorrect.](media/51c65d16483e011a8315823fc590e6c2.png)

Abbildung 4-43: Submodel Editor - Administrative Information

**Semantic ID**

Der Bereich Semantic ID (vgl. Abbildung 4-44) definiert den semantischen Identifier für das Teilmodell. Entsprechende Identifier sind in den Teilmodell-Vorlagen der IDTA[^25] zu finden.

[^25]: <https://industrialdigitaltwin.org/content-hub/teilmodelle>

![A screenshot of a computer AI-generated content may be incorrect.](media/75b36f5027e7c65f269e71ec631905f7.png)

Abbildung 4-44: Submodel Editor - Semantic ID

**Data Specification**

Der Bereich *Data Specification* (vgl. Abbildung 4-45) ist aktuell noch nicht implementiert und wird in einer zukünftigen Version unterstützt.

![A screenshot of a computer AI-generated content may be incorrect.](media/7516bf3ab7fbd21625c92dac67ba4e3e.png)

Abbildung 4-45: Submodel Editor - Data Specification

Wenn alle Angaben vollständig sind, kann das Teilmodell über die Schaltfläche **Save** gespeichert werden und erscheint in der Liste der Teilmodelle. Abbildung 4-46 zeigt exemplarisch die Details eines erstellten Teilmodells.

![Ein Bild, das Text, Screenshot, Software, Webseite enthält. KI-generierte Inhalte können fehlerhaft sein.](media/24de8649e999c75629aee5e2b567abfc.png)

Abbildung 4-46: Erstelltes Teilmodell

Neben dem Erstellen von Teilmodellen ermöglicht der AAS Editor auch das Bearbeiten existierender Teilmodelle. Hierfür kann über das Teilmodell über das Kontextmenü (Abbildung 4-47) bearbeitet bzw. ergänzt werden.

![A phone with a message AI-generated content may be incorrect.](media/d30a7d49bd5d116962b42cdbdcb9611c.png)

Abbildung 4-47: Teilmodell Kontextmenü

Die erstellten Teilmodelle sind zunächst ohne Inhalt und müssen im Weiteren mit Teilmodellelementen angereichert werden.

#### Teilmodell-Element erstellen

Die Inhalte von Teilmodellen werden mittels Teilmodell-Elementen dargestellt. Diese können im AAS Editor über das Kontextmenü des Teilmodells (siehe Abbildung 4-48) hinzugefügt werden.

![A screen shot of a phone AI-generated content may be incorrect.](media/19bd48a88ff81f467467e624153cd1bf.png)

Abbildung 4-48: Teilmodell-Element zu einem Teilmodell hinzufügen

Dafür muss zunächst der Datentyp des Elements ausgewählt werden (Abbildung 4-49)

![A screenshot of a computer AI-generated content may be incorrect.](media/9042fae483be6d8456a17a79c72ac390.png)

Abbildung 4-49: Submodel Element - Type

In der aktuellen Version werden die folgenden Datentypen unterstützt:

-   Property
-   SubmodelElementCollection
-   SubmodelElementList
-   MultiLanguageProperty
-   Range
-   File

Mit diesen Optionen können bereits viele Teilmodelle vollständig mit Inhalten gefüllt werden. Im Weiteren wird der Ablauf anhand einer *MultiLanguageProperty* beschrieben.

Nachdem der Datentyp mit der Schaltfläche **Next** bestätigt wurde, erscheint die Eingabemaske für die Inhalte. Abhängig vom gewählten Datentyp können sich die angezeigten Inhalte unterscheiden.

**Details**

Im Bereich *Details* (vgl. Abbildung 4-50) werden die allgemeinen Informationen des Elements festgelegt. Dazu gehören die *IdShort*, welche im jeweiligen Kontext eindeutig sein muss, sowie optional der Anzeigename (engl. Display Name) und die Beschreibung (engl. Description).

![A screenshot of a computer AI-generated content may be incorrect.](media/29f3aa2ab34d6201b5ffa229922bd316.png)

Abbildung 4-50: Submodel Element – Details

**Value**

Im Bereich *Value* (vgl. Abbildung 4-51) wird der Merkmalswert des Elements eingetragen. Je nach gewähltem Datentyp können sich die Inhalte stark unterscheiden.

![A screenshot of a computer AI-generated content may be incorrect.](media/6a01f72535ad18c1e1f3b2458e68ff3b.png)

Abbildung 4-51: Submodel Element – Value

**Semantic ID**

Im Bereich *Semantic ID* (vgl. Abbildung 4-52) wird der semantische Identifier für das Merkmal festgelegt. Dieser Wert ist essenziell für den interoperablen Datenaustausch mit dritten.

![A screenshot of a computer AI-generated content may be incorrect.](media/f04c812192a4b1d6b69b717885817958.png)

Abbildung 4-52: Submodel Element - Semantic ID

**Data Specification**

Der Bereich *Data Specification* (vgl. Abbildung 4-53) ist aktuell noch nicht implementiert und wird in einer zukünftigen Version unterstützt.

![Ein Bild, das Text, Screenshot, Zahl enthält. KI-generierte Inhalte können fehlerhaft sein.](media/ce35b58599f3d9ad53f81435fecc1f01.png)

Abbildung 4-53: Submodel Element - Data Specification

Wenn alle Angaben vollständig sind, kann das Element über die Schaltfläche **Save** gespeichert werden und erscheint in der Liste der Teilmodell-Elemente. Abbildung 4-54 zeigt exemplarisch die Details eines erstellten Elements.

![A screenshot of a computer AI-generated content may be incorrect.](media/39fa78025f31417d014c67116b79d648.png)

Abbildung 4-54: Erstelltes Submodel Element

Neben dem Erstellen von Teilmodell-Elementen ermöglicht der AAS-Editor auch das Bearbeiten existierender Elemente. Hierfür kann das jeweilige Element über das Kontextmenü (siehe Abbildung 4-55) bearbeitet, gelöscht oder kopiert.

![A screenshot of a computer AI-generated content may be incorrect.](media/e8e58f9681a155c2975d1e1ca51e4913.png)

Abbildung 4-55: Submodel Element Kontextmenü
