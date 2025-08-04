# TP12 – Produktkatalog mit der VWS

Im Teilprojekt 12 „Produktkatalog“ wurden auf Basis der in [TP1 „Konzept, Informationsmodelle und Produktbeschreibung„](https://github.com/VWS4LS/vws4ls-subproject-results/tree/main/TP01) erarbeiteten Konzepte rund um das Informationsmodell und die Produktbeschreibung der Leitungssatzherstellung für die Automobilindustrie mittels Verwaltungsschalen (VWS), klare anwendungsorientierte Regeln für das Erzeugen und Verwalten von Typ-Verwaltungsschalen erarbeitet.

Zudem wurde ein Demonstrator erstellt, der einen beispielhaften herstellerübergreifenden Marktplatz basierend auf diesen Typ-Verwaltungsschalen abbildet. In diesem Kontext sollte auch untersucht werden, inwieweit die VWS zur Abwicklung der notwendigen eCommerce-Prozesse anwendbar ist.

Die VWS nach IEC 63278-1 bietet als Schlüsselkonzept der Industrie 4.0 eine standardisierte Struktur für die Beschreibung von Assets (z.B. Maschinen, Komponenten oder Software) in einer digitalen Umgebung. Damit wird ein effizienter Datenaustausch zwischen verschiedenen Systemen und Anbietern ermöglicht.

![image](https://github.com/user-attachments/assets/66a8a6e4-f686-4dac-875a-86e7e18c47e4)       
Abbildung 3-1: VWS im Beschaffungsprozess der Leitungssatz-Wertkette

In TP1 wurde daher basierend auf der VWS ein detailliertes und umfassendes Informationsmodell des Leitungssatzes spezifiziert, welches auch die Produktmodellierung des Leitungssatzes umfasst. Dies beinhaltet die detaillierten Anforderungen, die der Leitungssatz erfüllen muss.

Unverzichtbarer Startpunkt für das Arbeiten mit Verwaltungsschalen ist jedoch die Bereitstellung von Typ-Verwaltungsschalen mit digitalen Modellbeschreibungen für die im Leitungssatzkontext verwendeten Komponenten (siehe Spalte „Tier X“ in Abbildung 1-1). Im bisherigen Projektverlauf wurde dieses Thema nicht ausreichend detailliert behandelt und um die Einführungshürden für die betroffenen Unternehmen zu senken, widmete sich TP12 diesem Thema.

Das Teilprojekt wurde in Arbeitspakete aufgeteilt, die in den folgenden Kapiteln näher erläutert werden.

## AP 1.1 - Anforderungsanalyse

Im AP1.1 „Anforderungsanalyse“ wurden Grundlagen definiert sowie Zielsetzung und Use Cases für das Teilprojekt geklärt. Zusammenfassend geht es darum, eine minimal notwendige Produktdatenqualität für die Datenmodellierung und ein Konzept zur Generierung eines Produktkatalog aus Produktdatenbanken zu definieren und im Demonstrator der AREN2036 sowie möglichst bei den Projektpartnern umzusetzen.

### Ist-Situation

Produktinformationen werden oft ähnlich -aber uneinheitlich- in Online-Produktkatalogen dargestellt, die wesentlichen technischen Daten meist als HTML-Tabellen und zusätzliche Dokumente zum Download angeboten.

![image](https://github.com/user-attachments/assets/5d4a2717-6acf-484f-b368-a106d44bdf75)     
Abbildung 3-2: Typische Online-Produktkataloge

Derartige Bereitstellungen als HTML-Webseiten sowie PDFs sind jedoch nicht standardisiert maschinenlesbar oder -interpretierbar.

Eine semantische Identifizierbarkeit findet in der Regel nur auf Ebene der Produktkategorie statt, nicht auf Merkmalsebene, was unzureichend ist für die angestrebten typischen Anwendungsfälle.

### Anwendungsfälle

Mittels eines VWS-basierten Produktkatalogs und semantischer Klassifizierung bis auf Merkmalsebene sollen die folgenden typischen Anwendungsfälle unterstützt werden:

-   Herstellerübergreifende maschinelle Produktauswahl (Vergleichsportale, Marktplätze)
-   Virtuelles, kollaboratives Engineering (z.B. ECAD, MCAD, VIBN) [^1]
-   Bereitstellung der Datengrundlage des „Product Carbon Footprint“ (PCF)

[^1]: <https://industrialdigitaltwin.org/use-cases/collaborative-engineering-die-technologische-grundlage-zur-digitalisierten-wertschoepfungskette>

![image](https://github.com/user-attachments/assets/d7c1fca2-9e48-4011-8f2a-bcdcb0201d19)     
Abbildung 3-3: Anwendungsfälle des VWS-basierten Produktkatalogs

Das TP12 widmet sich im Besonderen des Anwendungsfalls „Herstellerübergreifende maschinelle Produktauswahl (Vergleichsportale, Marktplätze)“. Angerissen wird dabei auch das Thema e-Commerce unter Anwendung der VWS.

### Typen von Digitalen Zwillingen

Digitale Zwillinge werden üblicherweise in Untertypen unterteilt, zu denen der **Digitale Zwillingsprototyp** (DTP), die **Digitale Zwillingsinstanz** (DTI) und das **Digitale Zwillingsaggregat** (DTA) gehören. Der DTP besteht aus den Entwürfen, Analysen und Prozessen, d.h. Modellen, die ein physisches Produkt abbilden. Der DTP existiert, bevor es ein physisches Produkt gibt. Der DTI ist der digitale Zwilling jeder einzelnen Instanz des Produkts, sobald es hergestellt ist. Der DTI ist mit seinem physischen Gegenstück für die restliche Lebensdauer des physischen Gegenstücks verbunden. Der DTA ist die Zusammenfassung von DTIs, deren Daten und Informationen für Abfragen über das physische Produkt, Prognosen und Lernen verwendet werden können. Die spezifischen Informationen, die in den digitalen Zwillingen enthalten sind, werden durch Anwendungsfälle bestimmt. Der digitale Zwilling ist ein logisches Konstrukt, was bedeutet, dass die tatsächlichen Daten und Informationen in anderen Anwendungen enthalten sein können [1].

Das Konzept des DTP wird im Folgenden durch die Typ-VWS umgesetzt werden. Der DTI beschreibt das Konzept der Instanz-VWS. Der DTA ist nicht im Scope dieses Teilprojekts.

Folgende Klassen von Typ-VWS sind bei der Entstehung von Leitungssätzen relevant:

-   **Einzel-Komponenten-VWS**: Diese modellieren die Einzelkomponenten als Typbeschreibungen, aus denen ein Leitungssatz besteht. Das können auch vorgefertigte zusammengesetzte Komponenten sein.
-   **Halbfabrikat-VWS**: Engineering- und Produktionsmodell für Halb-/Zwischenprodukten, bspw. eine geschnittene & abisolierte Leitung. Enthält das Teilmodell Bill of Material und Bill of Process mit Produktionsanweisungen.
-   **OEM-Leitungsstaz-VWS**: Modell des 150%-Leitungssatz. Enthält Produktspezifikation, Konfiguration, BOM mit Verweisen auf die Typ-VWsen (OEM-Artikelnummer) der beteiligten Komponenten.
-   **Konfektionär-Leitungssatz-VWS**: Modell des 150%-Leitungssatz. Enthält Produktspezifikation, Konfiguration, BOM mit Verweisen auf die Typ-VWsen (Manufacturer-Artikelnummer) der beteiligten Komponenten und die MBOM.
-   **Produktions-VWS**: Modell des Produktionsauftrags für den 100%-LS. Enthält Verweise auf eine definierte LS-Variante aus der LS-Typ-VWS (LS-BoM) sowie Verweise auf die Typ-VWsen der enthaltenen Komponenten und das Teilmodell BoP mit Produktionsanweisungen.

Für diese Typ-VWS sind folgende Lebenszyklusphasen bzw. Anwendungsfälle relevant:

-   **Produktkatalog**: Hier werden die einzelnen Komponenten und Halbprodukt-VWSen, die zur Bildung des Endprodukts verwendet werden sollen, als digitale Produktmodelle bereitgestellt und können bspw. für Angebotsanfrage / Abgabe genutzt und auch im weiteren als Vertragsgrundlage dafür dienen, was der Lieferant eigentlich liefern muss. Diese VWS müssen inhaltlich ausreichend befüllt und über Produktsuchen auffindbar sein. Eine Produktkatalog-VWS kann entweder Hardware, Software oder ein Serviceangebot abbilden. Als Filterregel für die Erkennung einer Produktkatalog-VWS soll die Attributbelegung *assetKind = Type* und das Vorhandensein des *SM TechnicalData* herangezogen werden. Andere VWSen sollten in einem Produktkatalog-Viewer nicht direkt angezeigt werden.
-   **Engineering**: Hier werden mehrere Komponenten- und Halbfabrikat-VWSen virtuell zu einer Leitungssatz-VWS aggregiert. Ausserdem werden auch Halbfabrikat-VWSen erzeugt.
-   **Qualitätssicherung**: Hier kann das Leitungssatz-Modell virtuell auf elektrische, mechanische und andere Eigenschaften geprüft werden, bevor er gefertigt wird.
-   **Produktion:** In der Produktionsphase der Halbprodukte und des Leitungssatzes wird mit produktbezogenen Informationen aus den Typ-VWSen gearbeitet.

Im Folgenden soll die Zusammenstellung von Einzelkomponenten-VWSen zu Hersteller-Produktkatalogen betrachtet werden.

## AP 1.2 - Datenmodellierung

Im AP 1.2 „Entwicklung von Informationsmodellen und Zuweisung der Daten“ wurde basierend auf den folgenden vorhandenen Standards die Datenmodellierung von **Typ-Verwaltungsschalen** für den VWS4LS-Kontext untersucht

Das Ergebnis der Analyse zielte darauf ab, Best-Practice-Ansätze für die Nutzung der Standard-VWS-Metadatenmodelle zu identifizieren und in einem Leitfaden wie folgt zu beschreiben.

### Minimal-Inhalte der Typ-VWS

Die folgenden Submodelle werden als Minimalausstattung für die Typ-VWS von LS-Komponenten empfohlen.

#### SM Technical Data

*IDTA 02003-1-2 TechnicalData* [2] dient dazu, technische Datenblätter in maschinenlesbarer Form und unter Angabe definierte Semantiken zur Verfügung zu stellen. Der beabsichtigte Anwendungsfall ist, dass ein Hersteller sein Produkt, welches er auf den Markt bringt, mittels technischer Daten (Eigenschaften) beschreibt, die idealerweise mit Hilfe von Wörterbüchern wie ECLASS und IEC Common Data Dictionary (IEC CDD) interoperabel sind und von anderen Marktteilnehmern eindeutig verstanden werden.

![image](https://github.com/user-attachments/assets/b5eb17b9-38ff-4c6a-80ac-88fe75a5bbca)     
Abbildung 3-4: IDTA 02003-1-2 TechnicalData

Es wird für Komponenten-VWS im Leitungssatzbereich empfohlen, die Inhalte der SMC *TechnicalProperties* möglichst weitgehend anhand der VEC-Ontologie zu definieren und mit den entsprechenden semantischen Referenzen zu versehen (siehe hierzu Kapitel 3.2.7).

##### Semantische Klassifikation

Für die SMC *ProductClassification* wird die Anwendung von ECLASS, VEC und IEC für die Produktidentifikation empfohlen, bspw. für eine elektrische Leitung wie folgt:

| **ClassificationSystem** | **ClassificationSystemVersion** | **ProductClassId**       |
|--------------------------|---------------------------------|--------------------------|
| VEC                      | 2.1.0                           | PrimaryPartType_Wire     |
| ECLASS                   | 15.0 (BASIC)                    | 44040101 oder 44040201   |
| IEC                      | 2.0018.0002                     | 0112/2///61360_4\#AAA036 |

Tabelle 31: Inhalte für SMC ProductClassification

Komponenten von Leitungssätzen können Steckverbinder, Leitungen, Verbindungen, Isolierungen und vieles mehr sein. Diese Produktidentifikation muss eindeutig semantisch klassifiziert werden.

ECLASS [3] als weit verbreitetes Klassifikationssystem für Produkte und Dienstleistungen bietet einige Klassifizierungs-Kategorien für den Kfz-Leitungssatz:

-   [44 Fahrzeugtechnik, Fahrzeugkomponente](https://eclass.eu/eclass-standard/content-suche/show?tx_eclasssearch_ecsearch%5Bdischarge%5D=0&tx_eclasssearch_ecsearch%5Bid%5D=44000000&tx_eclasssearch_ecsearch%5Blanguage%5D=0&tx_eclasssearch_ecsearch%5Bversion%5D=15.0&cHash=3973328aec14b612ae68a7aa42ca7e01)
-   [44-04 Elektrik, Elektronik (KFZ)](https://eclass.eu/eclass-standard/content-suche/show?tx_eclasssearch_ecsearch%5Bdischarge%5D=0&tx_eclasssearch_ecsearch%5Bid%5D=44040000&tx_eclasssearch_ecsearch%5Blanguage%5D=0&tx_eclasssearch_ecsearch%5Bversion%5D=15.0&cHash=4e4393873cb61f025a8cb093900ab8da)
-   [44-04-01 Bordnetz (KFZ, low voltage)](https://eclass.eu/eclass-standard/content-suche/show?tx_eclasssearch_ecsearch%5Bdischarge%5D=0&tx_eclasssearch_ecsearch%5Bid%5D=44040100&tx_eclasssearch_ecsearch%5Blanguage%5D=0&tx_eclasssearch_ecsearch%5Bversion%5D=15.0&cHash=e06daf8652ff1e09a7d3f2cdd31cccb8)
-   [44-04-01-01 Leitung (KFZ, low voltage)](https://eclass.eu/eclass-standard/content-suche/show?tx_eclasssearch_ecsearch%5Bdischarge%5D=0&tx_eclasssearch_ecsearch%5Bid%5D=44040101&tx_eclasssearch_ecsearch%5Blanguage%5D=0&tx_eclasssearch_ecsearch%5Bversion%5D=15.0&cHash=9eabf6364b06709c477c23a0ab151064)
-   [44-04-01-02 Leitungsstrang (KFZ, low voltage)](https://eclass.eu/eclass-standard/content-suche/show?tx_eclasssearch_ecsearch%5Bdischarge%5D=0&tx_eclasssearch_ecsearch%5Bid%5D=44040102&tx_eclasssearch_ecsearch%5Blanguage%5D=0&tx_eclasssearch_ecsearch%5Bversion%5D=15.0&cHash=bc422c52b259e112d116077a8b0d31f2)
-   [44-04-01-03 Leitungsstrang, Ladekabel (KFZ, low voltage)](https://eclass.eu/eclass-standard/content-suche/show?tx_eclasssearch_ecsearch%5Bdischarge%5D=0&tx_eclasssearch_ecsearch%5Bid%5D=44040103&tx_eclasssearch_ecsearch%5Blanguage%5D=0&tx_eclasssearch_ecsearch%5Bversion%5D=15.0&cHash=0f995e839d5d25fcaf50c3356a984d7b)
-   [44-04-01-05 Masseband, Batterieleitung (KFZ, low voltage)](https://eclass.eu/eclass-standard/content-suche/show?tx_eclasssearch_ecsearch%5Bdischarge%5D=0&tx_eclasssearch_ecsearch%5Bid%5D=44040105&tx_eclasssearch_ecsearch%5Blanguage%5D=0&tx_eclasssearch_ecsearch%5Bversion%5D=15.0&cHash=e0cc371bcbb7dbf5d1cbe968351f5273)
-   [44-04-01-90 Bordnetz (KFZ, low voltage, nicht spezifiziert)](https://eclass.eu/eclass-standard/content-suche/show?tx_eclasssearch_ecsearch%5Bdischarge%5D=0&tx_eclasssearch_ecsearch%5Bid%5D=44040190&tx_eclasssearch_ecsearch%5Blanguage%5D=0&tx_eclasssearch_ecsearch%5Bversion%5D=15.0&cHash=89dcde265e9a3d42a63f5dc645cba130)
-   [44-04-01-91 Bordnetz (KFZ, low voltage, Teile)](https://eclass.eu/eclass-standard/content-suche/show?tx_eclasssearch_ecsearch%5Bdischarge%5D=0&tx_eclasssearch_ecsearch%5Bid%5D=44040191&tx_eclasssearch_ecsearch%5Blanguage%5D=0&tx_eclasssearch_ecsearch%5Bversion%5D=15.0&cHash=d84f0afb5aa00e09f36373b9efcf1cb5)
-   [44-04-01-92 Bordnetz (KFZ, low voltage, Zubehör)](https://eclass.eu/eclass-standard/content-suche/show?tx_eclasssearch_ecsearch%5Bdischarge%5D=0&tx_eclasssearch_ecsearch%5Bid%5D=44040192&tx_eclasssearch_ecsearch%5Blanguage%5D=0&tx_eclasssearch_ecsearch%5Bversion%5D=15.0&cHash=440bfd1a1c63483399f60c482eab7857)
-   [44 Fahrzeugtechnik, Fahrzeugkomponente](https://eclass.eu/eclass-standard/content-suche/show?tx_eclasssearch_ecsearch%5Bdischarge%5D=0&tx_eclasssearch_ecsearch%5Bid%5D=44000000&tx_eclasssearch_ecsearch%5Blanguage%5D=0&tx_eclasssearch_ecsearch%5Bversion%5D=15.0&cHash=3973328aec14b612ae68a7aa42ca7e01)
-   [44-04 Elektrik, Elektronik (KFZ)](https://eclass.eu/eclass-standard/content-suche/show?tx_eclasssearch_ecsearch%5Bdischarge%5D=0&tx_eclasssearch_ecsearch%5Bid%5D=44040000&tx_eclasssearch_ecsearch%5Blanguage%5D=0&tx_eclasssearch_ecsearch%5Bversion%5D=15.0&cHash=4e4393873cb61f025a8cb093900ab8da)
-   [44-04-02 Bordnetz (KFZ, high voltage)](https://eclass.eu/eclass-standard/content-suche/show?tx_eclasssearch_ecsearch%5Bdischarge%5D=0&tx_eclasssearch_ecsearch%5Bid%5D=44040200&tx_eclasssearch_ecsearch%5Blanguage%5D=0&tx_eclasssearch_ecsearch%5Bversion%5D=15.0&cHash=db74a23fdd1513282d73c02d39dcc400)
-   [44-04-02-01 Leitung (KFZ, high voltage)](https://eclass.eu/eclass-standard/content-suche/show?tx_eclasssearch_ecsearch%5Bdischarge%5D=0&tx_eclasssearch_ecsearch%5Bid%5D=44040201&tx_eclasssearch_ecsearch%5Blanguage%5D=0&tx_eclasssearch_ecsearch%5Bversion%5D=15.0&cHash=313695c3aff99b1a5c90b347e3090ad7)
-   [44-04-02-02 Leitungsstrang (KFZ, high voltage)](https://eclass.eu/eclass-standard/content-suche/show?tx_eclasssearch_ecsearch%5Bdischarge%5D=0&tx_eclasssearch_ecsearch%5Bid%5D=44040202&tx_eclasssearch_ecsearch%5Blanguage%5D=0&tx_eclasssearch_ecsearch%5Bversion%5D=15.0&cHash=c54f0f26eed2ae904cc30cca3ec41151)
-   [44-04-02-03 Leitungsstrang, Ladekabel (KFZ, high voltage)](https://eclass.eu/eclass-standard/content-suche/show?tx_eclasssearch_ecsearch%5Bdischarge%5D=0&tx_eclasssearch_ecsearch%5Bid%5D=44040203&tx_eclasssearch_ecsearch%5Blanguage%5D=0&tx_eclasssearch_ecsearch%5Bversion%5D=15.0&cHash=fb3895890e5595b6481e5d62b3be2185)
-   [44-04-02-05 Masseband, Batterieleitung (KFZ, high voltage)](https://eclass.eu/eclass-standard/content-suche/show?tx_eclasssearch_ecsearch%5Bdischarge%5D=0&tx_eclasssearch_ecsearch%5Bid%5D=44040205&tx_eclasssearch_ecsearch%5Blanguage%5D=0&tx_eclasssearch_ecsearch%5Bversion%5D=15.0&cHash=e1a4c0c50201d58a159150794c7bcbe8)
-   [44-04-02-06 Leistungselektronik E-Motor (KFZ, high voltage)](https://eclass.eu/eclass-standard/content-suche/show?tx_eclasssearch_ecsearch%5Bdischarge%5D=0&tx_eclasssearch_ecsearch%5Bid%5D=44040206&tx_eclasssearch_ecsearch%5Blanguage%5D=0&tx_eclasssearch_ecsearch%5Bversion%5D=15.0&cHash=562fe179f4648dc256fddbaa305f3223)
-   [44-04-02-90 Bordnetz (KFZ, high voltage, nicht spezifiziert)](https://eclass.eu/eclass-standard/content-suche/show?tx_eclasssearch_ecsearch%5Bdischarge%5D=0&tx_eclasssearch_ecsearch%5Bid%5D=44040290&tx_eclasssearch_ecsearch%5Blanguage%5D=0&tx_eclasssearch_ecsearch%5Bversion%5D=15.0&cHash=431e6ede6f50fd722860f8d1f4db4fd8)
-   [44-04-02-91 Bordnetz (KFZ, high voltage, Teile)](https://eclass.eu/eclass-standard/content-suche/show?tx_eclasssearch_ecsearch%5Bdischarge%5D=0&tx_eclasssearch_ecsearch%5Bid%5D=44040291&tx_eclasssearch_ecsearch%5Blanguage%5D=0&tx_eclasssearch_ecsearch%5Bversion%5D=15.0&cHash=9f70cb7d39dd326349824012f3d59e06)
-   [44-04-02-92 Bordnetz (KFZ, high voltage, Zubehör)](https://eclass.eu/eclass-standard/content-suche/show?tx_eclasssearch_ecsearch%5Bdischarge%5D=0&tx_eclasssearch_ecsearch%5Bid%5D=44040292&tx_eclasssearch_ecsearch%5Blanguage%5D=0&tx_eclasssearch_ecsearch%5Bversion%5D=15.0&cHash=dbdba9a3bd7aa1bccd3bfd0503ee5170)
-   [19-21-20-90 Testing software (client, server operating system, unspecified)](https://eclass.eu/eclass-standard/content-suche/show?tx_eclasssearch_ecsearch%5Bdischarge%5D=0&tx_eclasssearch_ecsearch%5Bid%5D=19212090&tx_eclasssearch_ecsearch%5Blanguage%5D=1&tx_eclasssearch_ecsearch%5Bversion%5D=15.0&cHash=c27bb5f0da1c8491ccd0b67e47456e38)
-   [36-64-02-91 Mach. a. appliance f. nondestructive testing of materials, components (parts)](https://eclass.eu/eclass-standard/content-suche/show?tx_eclasssearch_ecsearch%5Bdischarge%5D=0&tx_eclasssearch_ecsearch%5Bid%5D=36640291&tx_eclasssearch_ecsearch%5Blanguage%5D=1&tx_eclasssearch_ecsearch%5Bversion%5D=15.0&cHash=d7c46716161181c9668a4326da30f694)

Das „Common Data Dictionary“ der IEC [4] bietet ebenfalls tendenziell für den Leitungssatz verwendbare Klassifizierungen, z.B.

-   [0112/2///61360_4\#AAA548 - car plug](https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/TU0/0112-2---61360_4%23AAA548)[^2]
-   [0112/2///61360_4\#AAA032 - conductor](https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/classesblocks/0112-2---61360_4%23AAA032?opendocument)
-   [0112/2///61360_4\#AAA034 - insulated conductor](https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/classes/0112-2---61360_4%23AAA034?opendocument)
-   [0112/2///61360_4\#AAA035 - cable](https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/classesblocks/0112-2---61360_4%23AAA035)
-   [0112/2///61360_4\#AAA036 - electric power cable](https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/classes/0112-2---61360_4%23AAA036)[^3]
-   [0112/2///61360_4\#AAA148 - connector](https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/classesblocks/0112-2---61360_4%23AAA148?opendocument)
-   [0112/2///61360_4\#AAA612 - connector shell](https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/classesblocks/0112-2---61360_4%23AAA612?opendocument)
-   [0112/2///61360_4\#AAA524 - connector contact](https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/classesblocks/0112-2---61360_4%23AAA524?opendocument)
-   [0112/2///61360_4\#AAA611 - connector tool](https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/TU0/0112-2---61360_4%23AAA611)[^4]
-   [0112/2///61360_4\#AAF249 - cable/wire](https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/PropertiesAllVersions/0112-2---61360_4%23AAF249?opendocument)
-   [0112/2///61360_4\#AUA478 - cable (multi-conductor)](https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/TerminologiesAllVersions/0112-2---61360_4%23AUA478?opendocument)
-   [0112/2///61360_4\#AUA479 - insulated wire (single conductor)](https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/TerminologiesAllVersions/0112-2---61360_4%23AUA479?opendocument)
-   …

[^2]: <https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/TU0/0112-2---61360_4%23AAA548>

[^3]: <https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/classes/0112-2---61360_4%23AAA036>

[^4]: <https://cdd.iec.ch/cdd/iec61360/iec61360.nsf/TU0/0112-2---61360_4%23AAA611>

Um eine gezielte Produktsuche zu vereinfachen, wird empfohlen, Leitungssatzkomponenten in Produktkatalogen mit den oben aufgeführten Bezeichnern zu klassifizieren.

#### SM Handover Documentation

*IDTA 02004-1-2 HandoverDocumentation* [5] definiert ein standardisiertes Austauschformat für Dokumentationsartefakte zu einem bestimmten Asset. Die übergebenen Dokumente können Informationen enthalten, die z.B. für die korrekte Konstruktion, Installation, Inbetriebnahme, Ersatzteilbevorratung, Bedienung, Reinigung, Inspektion, Wartung und Reparatur erforderlich sind. Darüber hinaus gibt es gesetzliche Regelungen, die das Vorhandensein bestimmter Herstellerdokumente vorschreiben können, wie z.B. Konformitätserklärungen der Communauté Européenne (CE), Atmosphères Explosives (ATEX) Zertifikate oder Materialzertifikate.

![Ein Bild, das Text, Screenshot, Schrift, parallel enthält. KI-generierte Inhalte können fehlerhaft sein.](media/7303e3860eef8a5a98f90be3ea1c2572.png)

Abbildung 3-6: SM HandoverDocumentation

Im Teilmodell *HandoverDocumentation* müssen relativ wenige relevante Properties beachtet werden, insbesondere die SMC *DocumentVersion und DocumentClassification*. Da *DocumentId* als mandatory deklariert ist, kann es nicht weggelassen werden.

##### Klassifizierungssysteme für Dokumente

Das SM *HandoverDocumentation* erlaubt die Klassifizierung von Dokumenten unter Verwendung von Referenzsystemen, siehe hierzu auch „4.7.6 Klassifizierungssysteme für “.

Soweit vorhanden, wird empfohlen, die im folgenden aufgeführten Dokumenttypen in der VWS aufzuführen. Weiter wird empfohlen, die Dokumente nicht direkt in der VWS als Datei, sondern besser als Link auf einen Dokumentenserver bereitzustellen. Für die Preview-Files wird die Erstellung geeigneter Thumbnail-Bilddateien empfohlen, die für ganze Produktgruppen einheitlich genutzt werden können.

Als Mindestanforderung muss im SM *HandoverDocumentation* jedes Dokument nach VDI 2770 Blatt 1:2020-04 klassifiziert werden. Ergänzend kann nach „*IEC 61355-1:2008*“ klassifiziert werden.

Der Wert von „*ClassificationSystem*“ ist dazu auf „*VDI2770 Blatt 1:2020*“ oder „*IEC 61355-1:2008*“ zu setzen und der Wert von „*ClassId*“ auf den entsprechenden Code aus den nachstehenden Tabellen:

##### Datenblatt: Technische Beschreibung (TB)

| **ClassificationSystem** | **ClassID**  | **ClassName (DE)**        | **ClassName (EN)**      |
|--------------------------|--------------|---------------------------|-------------------------|
| VDI2770 Blatt 1:2020     | 02-01        | Technische Spezifikation  | Technical specification |
| IEC 61355-1:2008         | DA           | Datenblätter              | Data sheets             |

Tabelle 32: Datenblatt: Inhalte für SMC DocumentClassification

##### VEC: Technische Beschreibung (TB)

| **ClassificationSystem** | **ClassID**  | **ClassName (DE)**                                 | **ClassName (EN)**                               |
|--------------------------|--------------|----------------------------------------------------|--------------------------------------------------|
| VDI2770 Blatt 1:2020     | 02-01        | Technische Spezifikation                           | Technical specification                          |
| IEC 61355-1:2008         | EC           | Technische Spezifikations- / Anforderungsdokumente | Technical specification /  requirement documents |

Tabelle 33: Technische Spezifikation: Inhalte für SMC DocumentClassification

##### Technische Zeichnung (TZ)

| **ClassificationSystem** | **ClassID**  | **ClassName (DE)**         | **ClassName (EN)**     |
|--------------------------|--------------|----------------------------|------------------------|
| VDI2770 Blatt 1:2020     | 02-02        | Zeichnungen, Pläne         | Drawings, plans        |
| IEC 61355-1:2008         | ED           | Dimensionierungsdokumente  | Dimensioning documents |

Tabelle 34: Technische Zeichnung: Inhalte für SMC DocumentClassification

##### Betriebsanleitung (BA)

| **ClassificationSystem** | **ClassID**  | **ClassName (DE)**          | **ClassName (EN)**       |
|--------------------------|--------------|-----------------------------|--------------------------|
| VDI2770 Blatt 1:2020     | 03-02        | Bedienung                   | Operation                |
| IEC 61355-1:2008         | DC           | Anleitungen und Handbücher  | Instructions and manuals |

Tabelle 35: Betriebsanleitung: Inhalte für SMC DocumentClassification

##### Konformitätserklärung (KE)

| **ClassificationSystem** | **ClassID**  | **ClassName (DE)**        | **ClassName (EN)**        |
|--------------------------|--------------|---------------------------|---------------------------|
| VDI2770 Blatt 1:2020     | 02-04        | Zertifikate, Deklaration  | Certificates, Declaration |
| IEC 61355-1:2008         | EB           | Normen und Richtlinien    | Standards and regulations |

Tabelle 36: Konformitätserklärung: Inhalte für SMC DocumentClassification

#### SM Digital Nameplate

*IDTA 02006-2-0 Digital Nameplate for Industrial Equipment* [6] zielt darauf ab, den jeweiligen Verwaltungsschalen interoperable Informationen über Anlagenkennzeichen zur Verfügung zu stellen.

![Ein Bild, das Text, Screenshot, Schrift, Reihe enthält. KI-generierte Inhalte können fehlerhaft sein.](media/e80c07c676e4e87f24d01d68b6b30ea1.png)

Abbildung 3-7: SM DigitalNameplate

Das SM DigitalNameplate enthält einige instanzbezogene Properties. Diese und sonstige Nicht-sinnvolle Properties dürfen für die Anwendung in der Typ-VWS nicht befüllt oder sollten entfernt werden. Das betrifft vor allem SerialNumber, DateOfManufacture sowie FirmwareVersion, SoftwareVersion. Eine Ausnahme wird vorgeschlagen für URIOfTheProduct, wo der Link auf eine ausserhalb des VWS-Ökosystems vorhandenen Online-Produktkatalogseite eingebracht werden kann, um hierüber eine sinnvolle Informationsverlinkung herzustellen.

Bei einigen Properties im SM DigitalNameplate gibt es Redundanzen zum SM TechnicalData, die beachtet und konsistent gehalten werden müssen, bei ManufacturerName besteht eine gewisse Typinkonsistenz:

| **SM „Digital Nameplate“**                  | **SM „Technical Data“**                | **Inhalt**                                               |
|---------------------------------------------|----------------------------------------|----------------------------------------------------------|
| *ManufacturerName [MLP]*                    | *ManufacturerName [Prop]*              | Textueller Bezeichner ohne Sonderzeichen                 |
| *ManufacturerProductDesignation [MLP]*      | *ManufacturerProductDesignation [MLP]* | Beschreibender Kurztext, sprachabhängig                  |
| *ProductArticleNumberOfManufacturer [Prop]* | *ManufacturerArticleNumber [Prop]*     | Textueller Bezeichner ohne Sonderzeichen                 |
| *OrderCodeOfManufacturer [Prop]*            | *ManufacturerOrderCode [Prop]*         | Textueller Bezeichner ohne Sonderzeichen                 |
| *CompanyLogo [File]*                        | *ManufacturerLogo [File]*              |  Langzeitstabile URL auf Bilddatei oder angehängte Datei |

Tabelle 37: Redundante Properties in SM DigitalNameplate und SM TechnicalData

##### Produkthierarchie

Das SM DigitalNameplate enthält als wesentliche Informationsbestandteile für den Produktkatalog die Produkthierarchie, welche über die folgenden Properties abgebildet wird:

| ManufacturerProductRoot         | top level of a 3-level manufacturer specific product hierarchy                                     |
|---------------------------------|----------------------------------------------------------------------------------------------------|
| ManufacturerProductFamily       | second level of a 3-level manufacturer specific product hierarchy                                  |
| ManufacturerProductDesignation  | third or lowest level of a 3-level manufacturer specific product hierarchy                         |
| ManufacturerProductType         | characteristic to differentiate between different products of a product family or special variants |

Tabelle 38: Properties für Produkthierarchie

Es wird empfohlen, dass jede Organisation für sich ein klar definiertes Konzept entwirft, wie diese Properties in der VWS konkret befüllt werden sollen. Siehe dazu auch Kapitel 3.3 „AP 1.3 - Extraktionslogik (ETL) entwickeln“.

##### Kennzeichen

Die SMC *Markings* soll Verweise auf relevante Conformance-Standards und -Organisationen enthalten, idealerweise mit einem geeigneten Logo zur grafischen Darstellung. In *DesignationOfCertificateOrApproval* sollte der jeweilige exakte Spezifikationsname verwendet werden, für *MarkingName* eine gängige Abkürzung.

Spezifikationen für Produktkonformität im Automotive-Umfeld sind bspw.:

| LV216-2 Tabelle A.2       | VDA-Standard für geschirmte Hochspannungsmantelleitungen für Kraftfahrzeuge und deren elektrische Antriebe |
|---------------------------|------------------------------------------------------------------------------------------------------------|
| NaBMW GS 95007-6-2        |                                                                                                            |
| BMW 9 327 162.9           |                                                                                                            |
| Mercedes C51 / 12.14      |                                                                                                            |
| Daimler Truck A0025460501 |                                                                                                            |
| VW N 107 777              |                                                                                                            |
| VW N 108 888              |                                                                                                            |

Tabelle 39: Automotive-Spezifikationen

Wenn kein zugehöriges Logo in Form einer Bilddatei vorhanden ist, wird aus Darstellungsgründen empfohlen, ein Logo generativ mit dem Text des Dokuments zu erzeugen, z.B.

![](media/6f3760e0d46f19c15293db39265c9441.png)![Ein Bild, das Text, Schrift, Screenshot, Grafiken enthält. KI-generierte Inhalte können fehlerhaft sein.](media/77375f4e8a6c7e12968640b58a16ab25.jpeg)![Ein Bild, das Kreis, Oval, Logo enthält. KI-generierte Inhalte können fehlerhaft sein.](media/edd0cc6492b364b3484e3b8b00dde5ba.jpeg)![Ein Bild, das Text, Schrift, Screenshot, Design enthält. KI-generierte Inhalte können fehlerhaft sein.](media/52fcb9bd25b45acb86365f70d6687394.jpeg)

![](media/9f13c45d628751558cc243314a2f3922.png)![Ein Bild, das Schwarz, Dunkelheit enthält. KI-generierte Inhalte können fehlerhaft sein.](media/8f7c74a302db50411fcea9e03763d3af.png)![](media/191cdd4bb57861b36f57a60432051a0e.png)

Abbildung 3-8: SM Marking Logos

### Benennung der VWS

Prägendes Element für die Benennung einer VWS ist die *idShort*. Es wird empfohlen, diese inhaltlich sprechend zu gestalten, dass der Herstellername, die Produktfamilie und die Artikelnummer enthalten ist. Bei AASX-Dateiausleitungen sollte die *idShort* die Basis für den Dateinamen bilden.

Im Folgenden ist detaillierter erklärt, welche Aspekte bei der ID-Bildung beachtet werden sollten.

#### ID-Bildung

Eine systematische ID-Definition ist relevant für die langfristige Wartbarkeit des VWS-Systems. Es wird eine methodische Vorgehensweise empfohlen, nach der VWS-Veröffentlicher bei der ID-Bildung vorgehen können.

Es gibt folgende Arten von Identifizierern:

-   Semantic-IDs, um Konzepte zu referenzieren
-   IDs für Artefakte, d.h. Assets, VWS, Submodelle, Properties

| **VWS-Metadaten** | **Inhalt**                                                                                                                                                        |
|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| *idShort*         | Textueller Bezeichner ohne Leer- und Sonderzeichen, idealerweise identisch oder ähnlich der *ProductArticleNumberOfManufacturer* bzw*. ManufacturerArticleNumber* |
| *VWSId*           | URI/IRI                                                                                                                                                           |
| *globalAssetId*   | URI/IRI nach IEC 61406 (Identification Link), wird als QR-Code aufgebracht und fungiert als Digitales Typenschild.                                                |
| *semanticId*      | GUID, IRDI, URI/IRI als Referenz auf einen semantischen Datensatz, z.B. im Concept Description Repository, der ECLASS-Datenbank oder dem IEC-CDD.                 |

Tabelle 310: VWS Metadaten

Die Anwendung von Uniform Resource Identifier (URI)/ Internationalized Resource Identifier (IRIs) wird als bevorzugte Methode (vor IRDIs, GUIDs ) zur Bildung von global unverwechselbaren IDs empfohlen. Die VWS-Metamodell-Spezifikation [7] beschreibt dazu eine „Best Practice for Creating URI Identifiers“, basierend auf folgendem Grammatik-Schema:

![Ein Bild, das Text, Screenshot, Schrift, Algebra enthält. Automatisch generierte Beschreibung](media/cc42c6b4a10e526e5a13f62934be136f.png)

Abbildung 3-9: Grammatik für URI Identifier

Es wird empfohlen, diesen generischen Strukturvorschlag wie im Folgenden beschrieben in vereinfachter Form anzuwenden, ggf. im **\<path\>** auf die Elemente **\<domain\>** und **\<release\>** zu verzichten. Insbesondere **\<release\>** als Bestandteil der ID kann langfristig problematisch werden, sollte sich diese ändern. Im Falle der von Notwendigkeit von geänderten Versionsständen (die aus Wartbarkeitsgründen generell vermieden werden sollten) könnten diese besser per Query-Parameter abgefragt werden.

Die „**aasId***“* der VWS ist die global eineindeutige Identifikations-Zeichenketten zur Kennung der VWS in Form eines URI/IRI nach [RFC 3987](https://tools.ietf.org/html/rfc3987), wobei darauf zu achten, dass der verwendete Zeichensatz des Kennzeichnungssystems kompatibel zu RFC 3986 ist, d.h. aus sog. „unreserved characters“ besteht und prozentcodierte Bestandteile konsequent vermeidet.

Die „**idShort**“ ist ein optionaler kurzer textueller Bezeichner, der nur in diesem Kontext eindeutig sein muss. Die *idShort* darf keine Leerzeichen oder Sonderzeichen enthalten und nur Ziffern, Buchstaben und das „_“-Symbol enthalten ([a-zA-Z][a-zA-Z0-9_]). Zudem muss die erste Ziffer ein Buchstabe sein.

Sobald eine Asset Administration Shell für die Produktion oder den Betrieb "freigegeben" ist, sollte eine „**globalAssetId***“* als Zugriffslink zugewiesen werden. Diese Asset-ID kann z.B. über einen QR-Code auf dem Asset, über ein RFID für das Asset, aus der Firmware des Assets oder aus einer Asset-Datenbank abgerufen werden. Die IEC 61406 (früher DIN SPEC 91406) definiert das Format solcher Asset-IDs und es wird empfohlen den *IdentificationLink* nach IEC 61406-1 [8] als Basis sowohl für die **id** als auch für die **globalAssetId** zu verwenden. Die URI/IRI kann systematisch so aufgebaut werden, dass Sie gleichzeitig zur produktbezogenen Referenzierung und Verlinkung in den Digitale Produkttyp (DTP) und die Digitale Produktinstanz (DPI) definiert werden kann:

Der *IdentificationLink* könnte sich demnach nach einem der folgenden Beispiele systematisch zusammensetzen:

-   https://{ManufacturerDomain}/{ManufacturerArticleNumber}
-   https://{ManufacturerDomain}/{ManufacturerOrderCode}
-   https://{ManufacturerDomain}/{ManufacturerArticleNumber}/{ManufacturerOrderCode}

Würde man diese Typ-URI/IRI dann um bspw. die *serialNumber* erweitern, könnte man damit die URI/IRI für die Produktinstanz erzielen:

-   https://{ManufacturerDomain}/{ManufacturerArticleNumber}/{ManufacturerOrderCode}/{SerialNumber}

Alternativ kann auch eine Linkbildung nach IEC61406-2 [9] erfolgen, wobei dann die Identifikationsparameter nicht im URL-Pfad codiert sind, sondern als Query-Parameter mitgegeben werden.

-   https://{manufacturerDomain}?1P={ManufacturerArticleNumber} S={ManufacturerOrderCode}

Dieser *Identification Link* nach IEC 61406 [8] [9] verbindet ein Produkt nahtlos mit seinen Informationen im Internet – dem Digitalen Typenschild (Digital Nameplate, DNP) als Schlüsseltechnik für Industrie 4.0 -Anwendungen, wie bspw. den Digital Product Passport (DPP).

#### [8] [9]Best-Practice-Kochrezept

Hier eine zusammenfassende Übersicht der Empfehlungen zur ID-Definition:​

![Ein Bild, das Text, Screenshot, Schrift, Diagramm enthält. KI-generierte Inhalte können fehlerhaft sein.](media/7c42a44264591fbb4235848366e4493d.jpeg)

Abbildung 3-10: Basic URL Structure

1.  Protocol (scheme) „https://“ (nicht „http://“) verwenden wegen Linkfähigkeit
2.  Domain-Name (authority) des Komponentenherstellers verwenden
3.  Möglichst kurze Root Domain
4.  Subdomain oder Subdirectory „**VWS**“ wird empfohlen für **ID**
5.  Subdomain oder Subdirectory „**asset**“ wird empfohlen für **globalAssetId**
6.  Im Pfad Sonderzeichen und Leerzeichen vermeiden (RFC 3986)
7.  Keine Sprachabhängigkeiten im Pfad (z.B. „/en/“, „/de/“)
8.  Zufallsstrings (z.B. UUIDs) als ID-Bestandteil vermeiden!
9.  Pfadbestandteile ohne semantischen Informationsgehalt vermeiden
10. Auf bestehendem ID-System aufsetzen, bspw. Artikelnummern (z.B. „https://aas.kostal.com/**10142491**“)
11. Passendes gleichförmiges Schema für Submodell-IDs verwenden (z.B. „https://aas.kostal.com/**sm/nameplate**/10142491“)
12. **IdShort***:* menschenlesbarer kurzer String, ohne Sonderzeichen, ggf. nach dem Schema „{M*anufacturerName*}_{M*anufacturerProductFamily*}_{*ManufacturerArticleNumber*}“ aufbauen, (z.B. **KOSTAL_PLK14_10142491**)
13. Ggf. **IdShort** als ID-Bestandteil im URI/IRI-Pfad verwenden (z.B. „https://VWS.kostal.com/**KOSTAL_PLK14_10142491**“)
14. Analog gleichförmiges Schema für Dateinamen anwenden, z.B. „**KOSTAL_PLK14_10142491_v10.aasx**“

### Benennung der Submodelle

Es wird empfohlen, die Benennung der IDTA-Submodelle möglichst nicht zu verändern. In untergeordneten Strukturen werden bspw. für SMC-Listenelemente menschenlesbare Benennungen empfohlen, anstelle der in den SMT-Spezifikationen manchmal empfohlenen fortlaufenden Nummerierungen (siehe Abbildung 3-11).

![](media/55d2a2e5f234912bceb4e93f42f28035.png)

Abbildung 3-11: Benennung der Submodell-Elemente

### Versionierung

Die Versionierung einer VWS erfolgt über die administrativen Metadaten (Version, Revision, Creator) und sollte entsprechend der unternehmensinternen Prozesse gepflegt werden.

![Ein Bild, das Text, Screenshot, Schrift, Zahl enthält. KI-generierte Inhalte können fehlerhaft sein.](media/c86a91ee4908773cc182b672726c4cec.png)

Abbildung 3-12: Versionierung

Es muss darauf hingewiesen werden, dass im VWS-Metamodell derzeit immer noch keine Metadaten für die Historieninformation verfügbar sind, was die praktische Nutzbarkeit der VWS-Technologie stark einschränkt. Siehe dazu auch [AdministrativeInformation: New properties "createdAt" and "lastModified" · Issue \#520 · admin-shell-io/aas-specs-metamodel](https://github.com/admin-shell-io/aas-specs-metamodel/issues/520)[^5].

[^5]: <https://github.com/admin-shell-io/aas-specs-metamodel/issues/520>

### Semantische Referenzierung in der VWS

Semantische Referenzierung stellt sicher, dass Daten in der Verwaltungsschale nicht nur Werte enthalten, sondern auch deren Bedeutung klar definiert ist. Dies ermöglicht Interoperabilität zwischen Systemen, da die Daten kontextbezogen interpretiert werden können. Beispielsweise wird eine Eigenschaft wie "Temperatur" nicht nur als Zahl (z. B. 25) dargestellt, sondern mit einer eindeutigen Definition verknüpft (z. B. "Temperatur in Grad Celsius").

Dies geschieht hauptsächlich durch die *semanticId* und die *Concept Description*. Die *semanticId* verweist auf eine Definition (extern oder intern), während die *ConceptDescription* als eigenständiges Element in der Verwaltungsschale eine detaillierte semantische Beschreibung eines Konzepts (z. B. einer Eigenschaft, Einheit oder eines Objekts) bereitstellt.

Andere Systeme können die *semanticId* auswerten, die referenzierte Definition nachschlagen (entweder direkt oder über die *ConceptDescription*) und die Bedeutung der Daten verstehen. Diese grundsätzlichen Arten der Referenzierung werden unterschieden:

-   **Direkte Referenzierung**: Die *semanticId* einer Property kann direkt auf eine externe Definition (z. B. ECLASS, IEC 61360 oder VEC) verweisen (via *ExternalReference*). In diesem Fall ist **keine** *ConceptDescription* notwendig.
````
{
  "idShort": "Temperature",
  "modelType": "Property",
  "valueType": "xs:double",
  "value": "25.0",
  "semanticId": {
    "type": "ExternalReference",
    "keys": [
      {
        "type": "GlobalReference",
        "value": "0112/2///61360_4#AAE685"
      }
    ]
  }
}
````

-   **Indirekte Referenzierung**: Die *semanticId* einer Property verweist auf eine *ConceptDescription* innerhalb der Verwaltungsschale (via *ModelReference*). Die *ConceptDescription* selbst kann über ihre *dataSpecifications* auf externe Standards verweisen. **Beispiel**: Diese *ConceptDescription* beschreibt das Konzept von „Durchmesser“ mit der Einheit „Millimeter“ und kann von mehreren Elementen in der Verwaltungsschale referenziert werden, was die Wiederverwendbarkeit fördert. Intern verweist Sie über *dataSpecification* auf externe Definitionen (z. B. in VEC, ECLASS und IEC).
````
{
  "idShort": "Diameter",
  "modelType": "Property",
  "valueType": "xs:double",
  "value": "21.2",
  "semanticId": {
    "type": "ModelReference",
    "keys": [
      {
        "type": "ConceptDescription",
        "value": "http://example.com/concept/diameter"
      }
    ]
  }
}
````

````
{
  "modelType": "ConceptDescription",
  "id": "http://example.com/concept/diameter",
  "idShort": "diameter",
  "displayName": [
    {
      "language": "en",
      "text": "diameter"
    }
  ],
  "embeddedDataSpecifications": [
    {
      "dataSpecification": {
        "type": "ExternalReference",
        "keys": [
          {
            "type": "GlobalReference",
            "value": "http://admin-shell.io/DataSpecificationTemplates/DataSpecificationIEC61360/3/0"
          }
        ]
      },
      "dataSpecificationContent": {
        "preferredName": [
          {
            "language": "en",
            "text": "diameter"
          },
          {
            "language": "de",
            "text": "Durchmesser"
          }
        ],
        "unit": "mm",
        "unitId": {
          "type": "ExternalReference",
          "keys": [
            {
              "type": "GlobalReference",
              "value": "0173-1#05-AAA480#004"
            }
          ]
        },
        "dataType": "REAL_MEASURE",
        "definition": [
          {
            "language": "en",
            "text": "extension, measured as spacing..."
          },
          {
            "language": "de",
            "text": "Ausdehnung, gemessen als Abstand..."
          }
        ],
        "modelType": "DataSpecificationIec61360"
      }
    }
  ]
}
````

Eine *ConceptDescription* fungiert als Metadaten-Container und enthält Informationen wie:

-   Eindeutige Identifikation (*id*).
-   Kurzbezeichnung (*idShort*).
-   Beschreibungen in mehreren Sprachen (*preferredName, shortName, definition*).
-   Verweise auf standardisierte Datenformate oder Ontologien (*dataSpecifications*).
-   Optional: Zusätzliche Attribute wie Synonyme, Formeln oder physikalische Definitionen.

Die *semanticId* und die *ConceptDescription* zusammen ermöglichen eine vollständige semantische Referenzierung innerhalb des VWS-Ökosystems.

#### Data Specification IEC 61360

Eine *Concept Description* ist anhand des Templates „*DataSpecificationIec61360*“ aufgebaut *(*Abbildung 3-13*),* welches spezifische Attribute wie *preferredName, unit, dataType* und *definition* enthält*.* Siehe hierzu auch [IDTA-01003-3-0: Specification Asset Administration Shell – Part 3a: Data Specification IEC 61360](https://industrialdigitaltwin.io/aas-specifications/IDTA-01003-a/v3.1/index.html)[^6] und [IDTA_Tutorial_VWS-Specification_Part3a_DataSpec_IEC61360.pdf](https://www.industrialdigitaltwin.org/en/wp-content/uploads/sites/2/2023/09/2023-09-28_IDTA_Tutorial_AAS-Specification_Part3a_DataSpec_IEC61360.pdf)[^7].

[^6]: <https://industrialdigitaltwin.io/aas-specifications/IDTA-01003-a/v3.1/index.html>

[^7]: <https://www.industrialdigitaltwin.org/en/wp-content/uploads/sites/2/2023/09/2023-09-28_IDTA_Tutorial_VWS-Specification_Part3a_DataSpec_IEC61360.pdf>

![Ein Bild, das Text, Screenshot, Schrift, Dokument enthält. KI-generierte Inhalte können fehlerhaft sein.](media/1a49dc7089666dfa0b18e168afc146a5.png)

Abbildung 3-13: DataSpecification nach IEC61360

![Ein Bild, das Text, Screenshot, Software, Zahl enthält. KI-generierte Inhalte können fehlerhaft sein.](media/71a4344d7e45b50207b026c9a502c1e5.png)

Abbildung 3-14: AASPE Beispiel DataSpecification nach IEC61360

### Einheitendeklaration in der Concept Description

Die [*IDTA GUIDELINE: How to transport ECLASS in the Asset Administration Shell*](https://industrialdigitaltwin.org/wp-content/uploads/2024/10/2024-10_IDTA_ECLASS_Semantic_Transport_ECLASS_in_AAS_1.0.pdf) [10] beschreibt die Anwendung von ECLASS und Einheitendefinitionen über *ConceptDescriptions*. Es wird allerdings empfohlen, auch die in dem Dokument nicht berücksichtigte property *symbol* zu belegen, damit Viewer Tools sicher anzeigen können.

![Ein Bild, das Text, Screenshot, Schrift, Reihe enthält. KI-generierte Inhalte können fehlerhaft sein.](media/cd9d4726c5103de687e027d8c9871a56.png)

Abbildung 3-15: Beispiel zur Einheitendefinition mittels einer Concept Description

Alternativ zu ECLASS (welches ohnehin auf IEC 62720 referenziert) wird empfohlen, direkt auf Einheitendefinitionen in IEC 62720 zu verweisen, und zwar mittels URI-Referenzen über <http://qudt.orq>, da diese Lösung gleichzeitig eine attraktive Onlinedarstellung bereitstellt (siehe z.B. <https://qudt.org/vocab/unit/MilliM>):

![Ein Bild, das Text, Screenshot, Software, Display enthält. KI-generierte Inhalte können fehlerhaft sein.](media/281732ea3bd94c1591b92828b5d7c79d.png)

Abbildung 3-16: QUDT-Onlinedarstellung

Siehe zu diesem Thema auch Kapitel „4.7.6 Klassifizierungssysteme für Einheiten“.

### Anwendung des VEC

VEC [11] ist das führende Modellierungssystem der Leitungssatzbranche und stellt präzise semantische Definitionen für Komponentenmerkmale und Datentypen bereit. Um Inkonsistenzen im Produktlebenszyklus zu vermeiden, wird empfohlen, in Produktkatalogen und Datenblättern nur Merkmale aufzuführen, die auch im VEC-Standard definiert sind. In der VWS sind diese mit einer mit einer entsprechenden semantischen Referenz auf die VEC-Definition zu versehen, um die maschinelle Interpretierbarkeit sicherzustellen. Im Idealfall erstellt bereits der Komponentenhersteller ergänzend eine komplette VEC-Spezifikation für seine jeweilige Komponente und fügt diese der VWS als Dateianhang hinzu.

![Ein Bild, das Text, Screenshot, Software, Design enthält. Automatisch generierte Beschreibung](media/f2657ffc8a79cab6382a2d457d066ae0.png)

Abbildung 3-17: Vehicle Electric Container (VEC)

Für die Produktklassifizierung über den VEC eignet sich die Klasse [PrimaryPartType](http://www.prostep.org/ontologies/ecad/2024/03/vec#PrimaryPartType)[^8].

[^8]: [http://www.prostep.org/ontologies/ecad/2024/03/vec\#PrimaryPartType](http://www.prostep.org/ontologies/ecad/2024/03/vec#PrimaryPartType)

![Ein Bild, das Text, Screenshot, Schrift, Diagramm enthält. Automatisch generierte Beschreibung](media/73389a40795cf6dde6e6586a6b1f1643.png)

Abbildung 3-18: VEC-Datenmodell: Description of Parts

Es liegt nahe, für leitungssatzspezifische Properties in Produktkatalogen auf die [Definitionen des VEC](https://ecad-wiki.prostep.org/specifications/vec/v210/general-component-data/description-of-parts/) zurückzugreifen und entsprechend im Submodel „TechnicalData“ [2] in der SMC *TechnicalProperties* darauf zu verweisen.

Unter <https://ecad.prostep.org/ontologies/2024/03/vec> wird eine Ontologie in „[RDF 1.1 Turtle](https://www.w3.org/TR/turtle/#sec-iri-references)“-Syntax bereitgestellt. Deren Anwendung ist in Kapitel 4.7.5.3 VEC erläutert.

![A diagram of a machine Description automatically generated](media/cf0e1134a604f6b8902c082dc0b2720c.png)

Abbildung 3-19: Beispiel VEC Terminal Datamodell (Quelle: VEC Recommendation V2.1)

Sowohl in der OPC UA Companion Spec. „OPC 40570: OPC UA for the Wire Harness Manufacturing Industry“ [12] als auch der [DIN 72036](https://dx.doi.org/10.31030/3521962) [13] wird als semantische Referenzierung auf die [Ontologie des VEC](https://ecad-wiki.prostep.org/specifications/vec/v210/vec-2.1.0-ontology.ttl) verwiesen.

**Als bevorzugte Lösung wäre es daher wünschenswert, dass Komponentenlieferanten grundsätzlich ein vollständiges VEC-Modell als Handover-Dokumentation zu Ihrer Komponente bereitstellen. Unabhängig davon wird der im Folgenden beschriebene Ansatz als Migrationspfad empfohlen, um eine Angleichung der Datenmodelle zwischen Produktkatalog und VEC zu erreichen:**

Im Sinne konsistenter Datendefinitionen über den Produktlebenszyklus hinweg wurde versucht, auch die im Online-Katalog dargestellten Produktdaten (im Submodell *TechnicalData* enthalten) auf dem VEC-Datenmodell basierend zu definieren, um eine semantische Kompatibilität der im klassischen Produktdatenblatt eines Online-Katalog dargestellten Informationen zur VEC-Ontologie zu erreichen.

In Kapitel 4.7.5.3 ist das Prinzip der Referenzenbildung zur VEC-Ontologie erläutert.

#### NumericalValue (VEC) als Property (VWS) modellieren

Modellierung eines VEC-NumericalValue durch verschiedene VWS-Konzepte und deren Bewertung

**Variante 1**: Definition der Einheit in der Konzeptbeschreibung

{

"idShort": "vec_terminalTypeNominalSize",

"description": [

{

"language": "en",

"text": "Specifies the nominal size of terminals that fit into the cavity. (e.g. 2x4)."

}

],

"id": "http://www.prostep.org/ontologies/ecad/2024/03/vec\#terminalTypeNominalSize",

"embeddedDataSpecifications": [

{

"dataSpecificationContent": {

"preferredName": [

{

"language": "en",

"text": " Terminal Size"

}

],

"unit": "Millimeter",

"sourceOfDefinition": "http://qudt.org/vocab/unit/MilliM",

"symbol": "mm",

"dataType": "REAL_MEASURE",

"definition": [

{

"language": "en",

"text": "Specifies the nominal size of terminals that fit into the cavity. (e.g. 2x4)."

},

{

"language": "de",

"text": "Gibt die Nenngröße der Klemmen an, die in den Hohlraum passen. (z. B. 2x4)."

}

],

"modelType": "DataSpecificationIec61360"

},

"dataSpecification": {

"type": "ExternalReference",

"keys": [

{

"type": "GlobalReference",

"value": "http://admin-shell.io/DataSpecificationTemplates/DataSpecificationIEC61360/3/0"

}

]

}

}

],

"modelType": "ConceptDescription"

}

![Ein Bild, das Text, Screenshot, Schrift, Reihe enthält. KI-generierte Inhalte können fehlerhaft sein.](media/cd9d4726c5103de687e027d8c9871a56.png)

Abbildung 3-20: Einheitendefinition in der Concept Description für ein VEC NumericalValue

Problem:

\- Die Einheit (z.B. in m, mm, Zoll) ist damit global für die referenzierte VEC-Eigenschaft für alle VWS auf dem VWS-Server definiert.

\- Bei Einheitenwechsel aus einer nativen Quelle kann eine Konvertierung mit Rundungsfehlern auftreten, da es im Kontext Einheiten gibt, die nicht direkt umrechenbar sind (z.B. Leitungsquerschnitte in mm² vs. AWG analog wie zöllige und metrische Gewinde). Die meisten CAD-Formate (bspw. STEP oder JT sind Einheiten agnostisch).

Betrachtung des folgenden Szenarios: Hersteller X gibt seine Daten frei (in Inches) und will seine Daten in einem zentralen VWS Marketplace einstellen. Dort werden jetzt die Inches in Meter umgerechnet. Falls nun diese digitalen Daten auch für digitale Verhandlungsprozesse genutzt werden und dann auch Vertragsgrundlage sind, wer verantwortet es, wenn die Daten aufgrund von Rundungsfehlern bei der Umrechnung nicht stimmen? Der Hoster des Marketplace? Der Einsteller der Daten, weil er das, was umgerechnet wurde, nicht nochmal geprüft hat, der Datenempfänger, weil er sich auf die Daten verlassen hat, oder der Hersteller der VWS-Repository Service?

**Variante 2**: Erstellen einer Konzeptbeschreibung für jede Einheit-Eigenschafts-Kombination, z. B.

-   vec\#thickness_m
-   vec\#thickness_mm
-   vec\#thickness_inches

Problem: Der semantische Bezug zwischen den Konzeptbeschreibung und der VEC-Spezifikation würde verloren gehen.


**Variante 3**: Definition der Einheit in der eingebetteten Datenspezifikation jedes VEC Properties

![Ein Bild, das Text, Screenshot, Software, Zahl enthält. KI-generierte Inhalte können fehlerhaft sein.](media/0ef177855be010ece7bfcc794fd575b1.png)

Abbildung 3-21: Definition der Einheit in der eingebetteten Datenspezifikation der Property

Problem: Erzeugt potentielle Redundanz.

Basierend auf der dargestellten Analyse wird für metrische Einheiten die Anwendung der Variante 1 als Standard empfohlen, für andere Einheitensysteme die Anwendung der Variante 3, um das Risiko von Rundungsfehlern bei der Einheitenkonvertierung in der Verantwortung des Datenempfängers zu belassen.

#### VEC als VWS-Submodell

Für die [OSS Harness Lib](https://github.com/4Soft-de/harness-model) wurde seitens 4Soft ein „experimental“ Modul „[vec-VWS-conversion](https://github.com/4Soft-de/harness-model/pull/313/files)“[^9] erstellt, um einen VEC verlustfrei in ein VWS-Submodell konvertieren zu können. Dabei wurden Modellierungsschwächen im Bereich der VWS-Properties offenbart, insbesondere zur Definition von Bereichswerten und Toleranzen.

[^9]: <https://github.com/4Soft-de/harness-model/pull/313>

Die Behebung dieser Modellierungsschwächen wurde daraufhin bei der IDTA in die Wege geleitet.

Den Ansatz der verlustlosen Transformation des VEC in ein VWS-Submodell wurde daraufhin nicht weiterverfolgt, da der VEC als formal definierte Spezifikation vorliegt und als solcher im Originalformat an die VWS angehängt werden kann.

#### VEC als HandoverDocumentation

Als praktikabelste Lösung wurde schließlich die Einbindung der VEC-Datei als *HandoverDocument* angesehen und auch zur Anwendung empfohlen.
