# **TP14 – Demonstrator**

Im Teilprojekt 14 „Demonstrator“ des Projekts VWS4LS steht die praktische Validierung und Erprobung der im Projekt entwickelten Lösungen im Mittelpunkt. Ziel ist es, die verschiedenen Ansätze und Konzepte, die in den vorangegangenen Teilprojekten erarbeitet wurden, in einer realitätsnahen Umgebung umzusetzen und auf ihre Praxistauglichkeit zu überprüfen. Der Aufbau des Demonstrators orientiert sich dabei im Wesentlichen an der in der Ergebnisdokumentation 1 beschriebenen Architektur, mit einigen Anpassungen: So kommen unter anderem eine Crimp-Maschine, eine BaSyx-Umgebung mit einem neu entwickelten Frontend sowie eine Komax Alpha-Simulation zum Einsatz.

Die Schwerpunkte des TPs liegen darauf, die Usability des BaSyx-Frameworks für den potenziellen Nutzer entlang des Produktionsprozesses Anwenderfreundlicher zu gestalten. Die einzelnen Handlungsschritte sollen dargestellt, nachvollziehbarer und die notwendigen Informationen pro Prozessschritt aggregiert werden. Darüber hinaus, wurde ein Proof of Concept entwickelt, welches sich dem Änderungsmanagement und wie dieses umgesetzt werden kann widmet. Hierbei wird demonstriert, wie Änderungen im System effizient erkannt, verwaltet und nachvollzogen werden können. Durch die Integration dieser Komponenten wird sichergestellt, dass alle relevanten Lösungsansätze des Projekts in einem umfassenden Demonstrator abgebildet und getestet werden können.

![VWS4LS_TP14_Events_1](https://github.com/user-attachments/assets/10889e10-082d-45ad-bc96-59f8f046058a)     
Abbildung 5-0: VWS und Events

Damit leistet das Teilprojekt einen entscheidenden Beitrag zur Überführung der theoretischen Konzepte in die industrielle Anwendung und schafft die Grundlage für eine spätere Implementierung im realen Produktionsumfeld.

## Workflow-gesteuerte Auftragsabwicklung

Der Demonstrator bildet einen kompletten Fertigungsauftrag in Form eines digital vernetzten Ablaufes nach. Im Kern handelt es sich um eine Javabasierte Anwendung, die auf dem SpringBootFramework aufsetzt. Über eine schlanke RESTSchnittstelle können externe Akteure Aufträge anlegen, verhandeln, bestätigen und schließlich abwickeln. Die Geschäftslogik jedes Auftrags wird dabei durch ein BPMNProzessmodell beschrieben, das zur Laufzeit von einer WorkflowEngine ausgeführt und von speziell zugeschnittenen WorkerModulen unterstützt wird.

Der Ablauf beginnt typischerweise damit, dass ein Client einen neuen Produktionsauftrag initiiert. Dazu übergibt er lediglich die ProduktID an das System. Daraufhin lädt die Anwendung die passende VWS des Produkttyps, generiert individuelle Identifikatoren für Auftrag, Charge und Lot und legt diese VWSen in der BaSyxUmgebung an. Anschließend startet ein Verhandlungsprozess: Das System nimmt die gewünschte Stückzahl entgegen, schreibt sie in das Submodell des Auftrags und leitet über einen kurzen Aufruf an einen NodeREDFlow einen Verhandlungsdialog zwischen den verfügbaren Maschinen ein. In diesem Verhandlungsszenario werden die offered- mit den required-Capabilities abgeglichen. Ziel ist es ein Match zwischen den produktseitigen required-Capabilities und der Maschinen seitigen offered-Capabilities zu ermöglichen.

Sobald eine Maschine ausgewählt wurde, spielt die Anwendung nun das zugehörige BPMNModell in die WorkflowEngine ein und startet eine frische Prozessinstanz. Zu diesem Zeitpunkt wechselt das System in die Phase der AssetBestätigung. Schritt für Schritt werden Maschine, Werkzeug, Terminal und Kabel geprüft, indem der Client jeweils die gescannte Kennung einsendet. Die Kennung ist in diesem Fall ein QR-Code, der die jeweilige Asset-ID des zu verwendenden Produktes beinhaltet. Das System vergleicht die Werte mit denen im AuftragsSubmodell und bestätigt oder verwirft die Eingabe.

Sind alle Prüfungen erfolgreich, geht der Auftrag in die Ausführung über. Die WorkerModule greifen einzelne Aufgaben aus dem BPMNModell ab, setzen Werte in Submodellen oder publizieren Statusmeldungen auf einen internen Nachrichtendienst. Gleichzeitig aktualisieren sie den Fortschritt in einer eigenen StatusVWS, sodass Bedienende und externe Systeme den Prozess in nahezu Echtzeit verfolgen können.

Wenn während der Ausführung ein Fehler auftritt oder ein Testlauf erneut gestartet werden soll, steht ein ResetEndpoint zur Verfügung. Dieser beendet alle untergeordneten Prozesse, stoppt die Worker und setzt das System in einen definierten Ausgangszustand zurück. Dadurch lässt sich schnell wieder ein neues Szenario beginnen, ohne manuell aufräumen zu müssen.

Für jede Entität, seien es Maschinen, Materialien oder der Produktionsauftrag selbst, existiert eine Shell, in der statische Informationen und aktuelle Mess oder Statuswerte gleichermaßen abgelegt sind. Ein eigenes Submodell dient als zentrale Drehscheibe für Laufzeitdaten wie den internen Systemstatus oder den Schlüssel der gerade laufenden Prozessinstanz. Dank der semantischen Kennzeichnungen können externe Anwendungen gezielt auf einzelne Elemente zugreifen, ohne den vollständigen Pfad kennen zu müssen.

Ein RESTController bündelt alle Schnittstellen, ein Handler verwaltet Zustände und verteilt sie auf die entsprechenden Submodelle, während Hilfsklassen das Anlegen und Aktualisieren von ShellElementen übernehmen. WorkerModule stellen die Verbindung zur WorkflowEngine her; jede WorkerKlasse ist für einen klar umrissenen Aufgabentyp verantwortlich.

Externe Dienste ergänzen die Laufzeitumgebung. Eine BaSyxInstanz beherbergt die Verwaltungsschalen, eine WorkflowEngine führt die BPMNModelle aus, ein Nachrichtendienst transportiert Prozess und Prüfereignisse, und ein NodeREDFlow vereinfacht die Kopplung einzelner Schritte. All diese Dienste laufen eigenständig, werden aber über Adressen konfiguriert, die die Anwendung beim Start einliest.

Die Anwendung wird in der Regel containerisiert betrieben. Ein typischer Aufbau umfasst die BaSyxUmgebung, die WorkflowEngine und das Backend selbst in separaten Containern, optional ergänzt durch einen Nachrichtendienst. Dadurch lässt sich das System leicht auf einem Entwicklungsrechner, in einer Laborumgebung oder in der Cloud starten.

Wer das System in eine bestehende ITLandschaft integrieren möchte, geht im Wesentlichen wie folgt vor: Zunächst werden die in den VWSen vergebenen Identifikatoren in das eigene Stammdaten oder MasterDataSystem übernommen. Anschließend wird ein Gateway eingerichtet, das den Verkehr zu den RESTEndpunkten und zum Nachrichtendienst lenkt. Schließlich werden betriebliche Auftragsnummern auf die IDs des Demonstrators gemappt, sodass vorhandene Tools die Abläufe auswerten können. Sobald dieser Rahmen steht, kann die Produktion in kleinen Schritten auf die VWSbasierte Steuerung umgestellt oder in einer Sandbox für Schulungen und Demonstrationen genutzt werden.

Damit bietet der Demonstrator eine praxisnahe, zugleich überschaubare Grundlage, um digitale Zwillinge in der Fertigung kennenzulernen und eigene Erweiterungen auszuprobieren – ohne sich sofort in Details wie Portnummern, Pfadstrukturen oder Konfigurationsdateien vertiefen zu müssen.

### BaSyx UI – Leitungssatzherstellung (Demonstrator UI)

Im Rahmen von TP14 wurde ein Modul entwickelt, das die Abbildung und Nachverfolgung eines Produktionsprozesses für ein Halbfabrikat, konkret ein Kabel mit gecrimptem Terminal, ermöglicht. Ziel war es, den gesamten Ablauf von der Produktauswahl bis zur Qualitätskontrolle digital abzubilden und über die VWS-gestützte Infrastruktur steuerbar zu machen.

Das Modul wurde als eigenständiges BaSyx UI-Modul umgesetzt und nutzt das zuvor beschriebene Modul-Feature. Verwendet werden Insbesondere bereits bestehende Funktionen des Web UIs wie die Abfrage von Verwaltungsschalen und Teilmodellen, sowie die Filterung nach spezifischen Semantischen IDs und Short-IDs. In der visuellen Umsetzung werden insbesondere die Plugins für „Bills of Materials“ und „Time Series Data“ des BaSyx UIs wiederverwendet. Im Folgenden sind die einzelnen Prozessschritte als Teil des Moduls beschrieben.

**Schritt 1: Produktauswahl**

Der Benutzer wählt ein konkretes Produkt aus, das produziert werden soll. In unserem Anwendungsfall handelt es sich um ein Kabel mit definiertem Querschnitt, das als Halbfabrikat klassifiziert ist, siehe Abbildung 5-1.

![image](https://github.com/user-attachments/assets/aff67ae1-14eb-4955-9677-5786564e688a)   
Abbildung 5-1: BaSyx-Modul VWS4LS Demonstrator - Produktauswahl

**Schritt 2: Auftragsbestätigung**

Im nächsten Schritt, siehe Abbildung 5-2 wird die Auftragsgröße festgelegt. Für Demonstrationszwecke wird ein einfacher Auftrag mit einer Charge (engl. Batch), einem Los (engl. Lot) und einem Produkt abgebildet.

![image](https://github.com/user-attachments/assets/35ddcdcb-0e1f-41cd-a4f9-93fb83ba12e5)    
Abbildung 5-2: BaSyx-Modul VWS4LS Demonstrator - Auftragsdaten

**Schritt 3: Maschinenverhandlung**

Auf Basis der Produktspezifikation wird ein Produktionsprozess abgeleitet. Eine Flowable-Engine wird genutzt, um eine Verhandlung über mögliche Produktionsressourcen (Maschinen) anzustoßen, siehe Abbildung 5-3. In dieser Phase geben verschiedene virtuelle Produktionssysteme Gebote ab.

![image](https://github.com/user-attachments/assets/3340a490-9bd6-452e-9343-dbd919a4330f)    
Abbildung 5-3: BaSyx-Modul VWS4LS Demonstrator – Verhandlungsprozess

**Schritt 4: Maschinenauswahl**

Die Ergebnisse der Verhandlung werden dem Nutzer präsentiert. Er kann nun eine geeignete Maschine auswählen, auf der der Produktionsprozess durchgeführt werden soll, siehe Abbildung 5-4.

![image](https://github.com/user-attachments/assets/46b3151e-f0e1-4d5f-8e8e-e11be4a56130)    
Abbildung 5-4: BaSyx-Modul VWS4LS Demonstrator - Maschinenauswahl

**Schritt 5: Asset-Bestätigung per Scan**

Vor dem Produktionsstart werden alle relevanten Assets durch QR-Code-Scans bestätigt, siehe Abbildung 5-5. Dazu zählen:

-   Die reale Produktionsmaschine
-   Das gewählte Kabel (Rohmaterial)
-   Das passende Terminal
-   Das eingesetzte Werkzeug (z. B. Crimpwerkzeug)

Die Validierung dient der Sicherstellung, dass alle für die Produktion benötigten Komponenten korrekt bereitgestellt wurden.

![image](https://github.com/user-attachments/assets/07f844df-d505-4254-94c6-c2d63f2fd280)    
Abbildung 5-5: BaSyx-Modul VWS4LS Demonstrator - Asset Identifikation (Spezifische Asset ID)

**Schritt 6: Prozessdurchführung**

Der Produktionsprozess wird auf Basis eines BPMN-Diagramms visualisiert, siehe Abbildung 5-6. Das Diagramm wird mit *bpmn.io* eingebettet und zeigt stets den aktuellen Zustand des Prozesses an, z. B. „Schneiden“, „Abisolieren“ oder „Crimpen“.

![image](https://github.com/user-attachments/assets/7995db3c-e46e-40aa-85aa-4e011e252c61)
Abbildung 5-6: BaSyx-Modul VWS4LS Demonstrator - Prozessdurchführung

**Schritt 7: Qualitätsprüfung der Crimpung**

Nach dem Crimpvorgang wird die sogenannte Crimpkurve als Qualitätsmerkmal ausgewertet. Die Kurve wird in einem Diagramm visualisiert und mit definierten Grenzwerten verglichen, siehe Abbildung 5-7. Der Benutzer erhält eine Rückmeldung darüber, ob der Produktionsschritt innerhalb der Qualitätsparameter liegt.

![image](https://github.com/user-attachments/assets/ec5f3ece-f304-4d72-a8dc-553995c0b3ff)    
Abbildung 5-7: BaSyx-Modul VWS4LS Demonstrator – Qualitätsprüfung der Crimpung

## Änderungsmanagement Einleitung

Ziel des VWS4LS-Demonstrators ist es, verschiedene Anwendungsfälle und Einsatzmöglichkeiten der Verwaltungsschale (VWS) zu veranschaulichen. Einer dieser Anwendungsfälle ist das Änderungsmanagement.

*Hinweis:* Das Änderungsmanagement bezieht sich in diesem Fall auf die Benachrichtigung, wenn Änderungen in einer VWS und deren Infrastruktur vorgenommen werden. Die entsprechenden VWS-Elemente müssen durch das Event-Element der VWS explizit abonniert werden.

Als mögliche Events werden

-   die Erstellung neuer,
-   das Update – also die Änderung der Werte der Attribute bereits existierender
-   oder das Löschen von

Teilmodellen, Teilmodellelementen, Verwaltungsschalen und Concept Descriptions betrachtet. Diese möglichen Events werden im Dokument als **Create, Update und Delete** bezeichnet. Hierbei sind *create* und *delete* dem Strukturevent zuzuweisen. Weiterhin gibt es noch andere Arten von Events, wie Security- und Runtime-Events als auch Alarme, die jedoch in dem VWS4LS-Demonstrator nicht näher betrachtet werden. Abbildung 5-8 stellt einen Baum von VWS-Entitäten dar, von der VWS-Umgebung bis hin zu einem Teilmodellelement, und zeigt die ihnen zugeordneten Eventtypen mit Beispielen. Innerhalb einer einzelnen VWS können strukturelle Änderungen (z. B. Erstellung und Löschung) oder die Aktualisierung von VWS-Entitäten wie Teilmodellen, Teilmodellelementen, VWS-Metadaten und Teilmodell-Metadaten abonniert werden. Die Spezifikation ​[1]​ erwähnt auch die Benachrichtigung über die Erstellung und Löschung einer gesamten VWS sowie über infrastrukturbezogene Ereignisse, die außerhalb einer bestimmten VWS auftreten, wie z. B. Alarme, Sicherheitsvorfälle (z. B. Logging-Ereignisse, Zugriffsverletzungen, Unstimmigkeiten zwischen Rollen und Rechten, Denial-of-Service-Versuche) und Lebenszyklus-Ereignisse von Infrastrukturkomponenten (z. B. Booten, Herunterfahren, Out-of-Memory-Zustände).

Das derzeitige Metamodell definiert das Event Element als Teilmodellelement, wodurch dessen Implementierung implizit auf das Innere einer VWS, genauer gesagt auf ein Teilmodell, beschränkt ist. Es kann rein logisch gesehen daher nur Ereignisse beobachten, die innerhalb dieser bestimmten VWS auftreten. Die Beobachtung der Erstellung einer VWS-Instanz ist logisch gesehen nicht möglich: In welchem Teilmodell würde man ein Event-Element platzieren, das die Existenz einer VWS überwacht, die entweder noch nicht existiert? Das gleiche Problem gilt für die in Abbildung 5-8 gezeigte Sicherheits-, Alarm- und Infrastruktur, da solche Event Elemente typischerweise nicht dem durch eine einzelne VWS repräsentierten Asset zuzuordnen sind. Diese Einschränkung könnte nur durch die Instanziierung einer VWS überwunden werden, die die VWS-Umgebung selbst repräsentiert. Eine Entscheidung, die diskutiert werden muss. Diese Probleme motivieren eine Neupositionierung des Event Elements innerhalb des VWS-Metamodells. Da die Abbildung auf Englisch ist, wurde für den Begriff VWS die englische Abkürzung AAS (Asset Administration Shell) genutzt.

![image](https://github.com/user-attachments/assets/b3eb40e3-664b-476f-9ce1-be981546c96d)    
Abbildung 5-8: VWS-Entitäten und ihre Eventtypen

Das entwickelte technische Konzept wurde im VWS4LS-Demonstrator prototypisch umgesetzt und evaluiert. Über die entwickelte Weboberfläche (siehe Kapitel 5.1.1) können VWS-Entitäten, im folgenden „Element“ genannt, abonniert und über Änderungen der abonnierten Elemente informiert werden. Je nach Szenario, sollen diese Änderungen vom Nutzer angenommen oder abgelehnt werden dürfen. Das allgemeine Anwendungsfalldiagramm dazu ist in Abbildung 5-9 zu sehen.

![image](https://github.com/user-attachments/assets/c096e8ea-8923-4efa-8a16-28b9ba80751a)    
Abbildung 5-9: Anwendungsfalldiagramm Änderungsmanagement

Ziel dieses Anwendungsfalls ist es nicht nachgeschaltete Automatismen, nach einer Änderung auszuführen, sondern lediglich über eine erfolgte Änderung zu informieren. Solche Automatismen beziehen sich im Änderungsmanagement der Leitungssatzentwicklung beispielsweise auf Entscheidungs- und Anpassungsvorgänge, wenn z. B. die Länge einer Leitung geändert werden muss. Das ist nicht Teil des hier definierten Änderungsmanagements.

Aus dem allgemeinen Anwendungsfall und den zuvor in Abbildung 5-8 definierten VWS-Eventtypen „Structure“ (*create*, *delete*) und „Update“, wurden drei Szenarien entwickelt, die im Folgenden beschrieben sind.

### Szenario 1: Abonnieren eines Teilmodellelements (update)

In diesem Szenario wird sich auf das Abonnieren einer Änderung eines Teilmodellelements fokussiert. D.h. der Abonnent möchte informiert werden, sobald sich der Wert eines Teilmodellelements verändert. Dies kann die Metainformation des Teilmodellelements betreffen oder aber den Wert des Elements selbst. Das Szenario ist in Abbildung 5-10 dargestellt. Als Voraussetzung wird angenommen, dass der VWS-Designer bereits eine VWS mit ihren Teilmodellen erstellt hat (1). Über einen Event-Broker abonniert der VWS-Designer anschließend ein Teilmodellelement (2). Sobald eine Applikation den Wert dieses Teilmodellelements ändert (3), wird der VWS-Designer durch den Broker über diese Änderung informiert (4).

![image](https://github.com/user-attachments/assets/23633b0e-9999-4f31-8c28-7cad182b950a)    
Abbildung 5-10: allgemeines Szenario - Abonnieren eines Teilmodellelements (update)

Bezug zu dem VWS4LS-Demonstrator

Bezogen auf den VWS4LS-Demonstrator nimmt der Produktionsleiter die Rolle des VWS-Designers ein und die externe Applikation wird von einem Manufacturing Execution System (MES) eingenommen, siehe Abbildung 5-11. Der Produktionsleiter legt eine Auftrags-VWS an (1) und abonniert den Auftragsstatus (2). Ein Mitarbeiter führt die notwendigen Produktionsschritte aus und trägt deren Ergebnisse in das MES ein. Dieses wiederum aktualisiert die Auftrags-VWS und ändert unter anderem auch das Teilmodellelement „Produktionsstatus“. Sobald eine Änderung vorgenommen wird, informiert der Broker den Produktionsleiter über die aktuelle Änderung mit Hilfe einer Pop-Up Benachrichtigung.

![image](https://github.com/user-attachments/assets/08c7d0d5-1db4-4fa7-a532-48dda1107153)    
Abbildung 5-11: VWS4LS Szenario - Abonnieren eines Teilmodellelements (update)

### Szenario 2: Abonnieren eines neuen Teilmodells in einer VWS (create)

Dieses Szenario behandelt die Nachverfolgung von neu hinzugefügten Teilmodellen zu einer bekannten VWS (s. Abbildung 5-12). Es wird vorausgesetzt, dass bereits sowohl eine originale als auch eine Kopie der originalen VWS vorliegen. Die originale VWS wird vom VWS-Designer erzeugt und die Kopie vom VWS-Nutzer verwendet.

Um über ein neu hinzugekommenes Teilmodell informiert zu werden, wählt der VWS-Abonnent zuerst den Eventtyp *create* und danach die VWS, in der die Teilmodelle beobachtet werden sollen aus (1). Dies erledigt er mit Hilfe einer Weboberfläche, die in der Abbildung nicht dargestellt ist. Danach wird im Broker ein Event angelegt, das auslöst, sobald ein neues Teilmodell in der originalen VWS erstellt wurde (2). Sobald ein neues Teilmodell durch den VWS-Designer in der originalen VWS hinzugefügt wird, sendet der Event Broker eine Benachrichtigung an den VWS-Nutzer.

![image](https://github.com/user-attachments/assets/8d4f3ac2-c294-4103-a774-366730fd61f3)    
Abbildung 5-12: allgemeines Szenario - Abonnieren eines neuen Teilmodell in einer VWS (create)

Bezug zu dem VWS4LS-Demonstrator

Bezogen auf den VWS4LS-Demonstrator kann in diesem Szenario der Komponentenkatalog eines Konfektionärs herangezogen werden. Die originalen VWS der Komponentenhersteller (VWS-Designer) liegen in diesem Katalog als Kopien und haben aber noch eine Referenz zu der originalen VWS. Der Konfektionär kann bei Durchsicht der Komponenten die VWS auswählen, zu denen er benachrichtigt werden möchte, sobald ein neues Teilmodell hinzugefügt wird (2). Sobald dann die abonnierte Änderung eintritt (3), wird der Konfektionär mittels einer Pop-Up Benachrichtigung über die Änderung informiert (4). Danach kann der Konfektionär entscheiden, ob er dieses neue Teilmodell in seine VWS-Kopie übernehmen möchte oder nicht. Das angewandte Szenario ist mit Ausnahme des letzten Schritts, der Änderungsübernahme, in Abbildung 5-13 dargestellt.

![image](https://github.com/user-attachments/assets/2e5c2468-a085-4700-b686-e052d9115ba5)     
Abbildung 5-13: VWS4LS Szenario - Abonnieren eines neuen Teilmodell in einer VWS (create)

### Szenario 3: Abonnieren einer neuen VWS (create)

In diesem Szenario (siehe Abbildung 5-14) soll der Abonnent über das Hinzufügen einer neuen VWS informiert werden. Dazu abonniert der Abonnent über den Broker ein Event, dass mit dem Hinzufügen einer neuen VWS in einem Repository auslöst (1). Sobald der VWS-Designer eine neue VWS in das Repository hochlädt (2), informiert der Broker den Abonnenten über die Änderung (3).

![image](https://github.com/user-attachments/assets/81b68379-ccc6-45fd-95d4-55fe479283aa)    
Abbildung 5-14: allgemeines Szenario - Abonnieren einer neuen VWS (create)

Bezug zu dem VWS4LS-Demonstrator

Bezogen auf den VWS4LS-Demonstrator könnte es ein Repository mit Leitungssatz-VWS für einen definierten OEM geben, siehe Abbildung 5-15. Der OEM kann dann die Benachrichtigung über neu hinzugefügte VWS mit Hilfe des Eventtyps „create“ und dem zu beobachtenden Repository abonnieren (1). Sobald ein Leitungssatz hergestellt wurde, lädt der Konfektionär die zugehörige VWS in das Repository des OEM (2) und der Broker sendet dem OEM eine Pop-Up Benachrichtigung (3).

![image](https://github.com/user-attachments/assets/2adfb7e6-3474-48d7-bb52-c666b6bd27c3)    
Abbildung 5-15: VWS4LS Szenario - Abonnieren einer neuen VWS (create)

Das Ziel der Arbeit ist es zu beschreiben, wie diese Änderungsarten mithilfe des Event-Elements aus der Metamodell-Spezifikation übertragen werden können. Dazu gehören unter anderem folgende Fragen:

-   Wie wird das "Abonnieren" mithilfe des Event-Elements modelliert?
-   Wie werden diese Änderungen technisch übertragen?
-   Welche Infrastrukturkomponenten sind dafür notwendig?
-   Wie spielen diese Infrastrukturkomponenten und Rollen (VWS-Nutzer, VWS-Owner, VWS-Designer) zusammen, also wie sieht die Systemarchitektur aus?
-   Wie ist der Inhalt der mithilfe des Event-Elements übertragenen Informationen abgebildet?

### Rollen und ihre Interaktionen

Die hier dargestellten Abläufe und Rollen fokussieren sich auf die Modellierung und Abbildung der oben eingeführten Szenarien mithilfe der VWS.

Um ein Asset in seiner VWS zu beschreiben, ist die Rolle des VWS-Designers erforderlich. Dieser ist dafür verantwortlich, Änderungen im Lebenszyklus eines Assets in entsprechende Änderungen der zugehörigen VWS bzw. Teilmodelle (TM) zu überführen. Die Änderungen können dabei durch eine Person oder eine Software durchgeführt werden.

Der Ablauf für das Änderungsmanagement ist in Abbildung 5-16 schematisch für das Abonnieren einer einzelnen Verwaltungsschale dargestellt und erfolgt für alle anderen VWS-Elemente in gleicher Weise.

![image](https://github.com/user-attachments/assets/e8d4fd4c-a604-420c-94cb-125b6ed380b0)    
Abbildung 5-16: Sequenzdiagramm des allgemeinen Änderungsmanagements

## Anforderungsanalyse

Zu Beginn wurde eine Anforderungsanalyse durchgeführt, um die Ziele für die zu entwickelnden Konzepte und die darauffolgende Implementierung festzulegen.

Wie im vorherigen Abschnitt beschrieben werden vier Aspekte betrachtet:

1.  VWS-Elemente, die abonniert werden können,
2.  VWS-Elemente, die abonniert werden können,
3.  Architektur, in der das Event umgesetzt wird und
4.  Technologie, mit der Events versendet werden.

### Die Arten der zu abonnierenden VWS-Elemente

Aus dem Anwendungsfall und den abgeleiteten Szenarien ergeben sich die in Abbildung 5-17 dargestellten Elemente der VWS, die der Nutzer bezüglich des Änderungsmanagements abonnieren kann. Dies ist eine Untermenge der in Abbildung 5-8 dargestellten VWS-Elemente und Eventtypen, da nicht alle Möglichkeiten im Projekt aufgrund der zeitlichen Begrenzung umgesetzt werden konnten. Tabelle 51 schlüsselt hierbei die einzelnen Eventtypen, die abonniert werden können (*create*, *update*, *delete*) mit ihren Anforderungen (Tabelle 54) für die gezeigten Elemente auf. Hierbei wurde der Eventtyp „Structure“ in die zwei Subtypen *create* und *delete* aufgeschlüsselt.

![image](https://github.com/user-attachments/assets/8b4585d0-ba85-4a7e-8c18-1361d4be15e2)    
Abbildung 5-17: Varianten der zu abonnierenden VWS-Elemente mit ausgewählten Eventtypen

Die konkrete Anwendung des Event-Elements auf die in Abbildung 5-17 gezeigten VWS-Elemente erfolgt in Kapitel 5.3.4.

| Lfd. Nr. | Element                     | Eventtyp                | Beschreibung                                                                                                                                                                                              | Bezug zu Anforderungsnummer (Tabelle 4)                                            |
|----------|-----------------------------|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------|
| 1        | VWS                         | create                  | Benachrichtigung über das Hinzufügen einer neuen VWS.                                                                                                                                                     | [\#AF_1](bookmark://AF_1), [\#AF_15](bookmark://AF_15)                             |
| 2        | VWS                         | delete                  | Benachrichtigung über das Löschen einer bestehenden VWS.                                                                                                                                                  | [\#AF_2](bookmark://AF_2), [\#AF_3](bookmark://AF_3)                               |
| 3        | VWS                         | update                  | Benachrichtigung über ein geändertes Element in der VWS (z.B. Metainformation, Teilmodell, Concept Description)                                                                                           | [\#AF_2](bookmark://AF_2), [\#AF_4](bookmark://AF_4), [\#AF_5](bookmark://AF_5)    |
| 4        | VWS Metainformation         | update, create, delete  | Benachrichtigung über eine geänderte Metainformation.  Eingrenzung: Wird eine einzelne Metainformation geändert, werden alle Metainformatiionen der VWS als update gesendet.                              | [\#AF_2](bookmark://AF_2), [\#AF_6](bookmark://AF_6), [\#AF_7](bookmark://AF_7)    |
| 5        | Concept Description         | create                  | Benachrichtigung über das Hinzufügen einer neuen Concept Description **in einer VWS**.                                                                                                                    | [\#AF_1](bookmark://AF_1), [\#AF_8](bookmark://AF_8), [\#AF_15](bookmark://AF_15)  |
| 7        | Concept Description         | delete                  | Benachrichtigung über das Löschen einer Concept Description **aus einer VWS**.                                                                                                                            | [\#AF_3](bookmark://AF_3), [\#AF_8](bookmark://AF_8)                               |
| 9        | Concept Description         | update                  | Benachrichtigung über die Aktualisierung einer Concept Description.  Eingrenzung: Wenn ein Element in einer Concept Description geändert wird, erfolgt immer ein update der gesamten Concept Description. | [\#AF_2](bookmark://AF_2), [\#AF_8](bookmark://AF_8), [\#AF_9](bookmark://AF_9)    |
| 10       | Teilmodell                  | create                  | Benachrichtigung über das Hinzufügen eines neuen Teilmodells **in einer VWS**.                                                                                                                            | [\#AF_1](bookmark://AF_1), [\#AF_8](bookmark://AF_8), [\#AF_15](bookmark://AF_15)  |
| 12       | Teilmodell                  | delete                  | Benachrichtigung über das Löschen eines Teilmodells **aus einer VWS**.                                                                                                                                    | [\#AF_3](bookmark://AF_3), [\#AF_8](bookmark://AF_8)                               |
| 14       | Teilmodell                  | update                  | Benachrichtigung über ein geändertes Element in einem Teilmodell (z.B. Metainformation, Teilmodellinhalt).                                                                                                | [\#AF_2](bookmark://AF_2), [\#AF_5](bookmark://AF_5)                               |
| 15       | Teilmodell Metainformation  | update, create, delete  | Benachrichtigung über eine geänderte Metainformation.  Eingrenzung: Wird eine einzelne Metainformation geändert, werden alle Metainformatiionen dem Teilmodell als update gesendet.                       | [\#AF_2](bookmark://AF_2), [\#AF_6](bookmark://AF_6), [\#AF_7](bookmark://AF_7)    |
| 16       | Teilmodell-element          | create                  | Benachrichtigung über das Hinzufügen eines neuen Teilmodellelements in einem Teilmodell.                                                                                                                  | [\#AF_1](bookmark://AF_1), [\#AF_15](bookmark://AF_15)                             |
| 17       | Teilmodell-element          | delete                  | Benachrichtigung über das Löschen eines Teilmodellelements in einem Teilmodell.                                                                                                                           | [\#AF_3](bookmark://AF_3)                                                          |
| 18       | Teilmodell-element          | update                  | Benachrichtigung über ein geändertes Teilmodellelement in einem Teilmodell. Das können sowohl geänderte Metainformationen (z. B. idShort) als auch der geänderte Wert des Elements selbst sein.           | [\#AF_2](bookmark://AF_2), [\#AF_5](bookmark://AF_5)                               |

Tabelle 51: VWS-Elemente und ihre zu abonnierenden Operationen

### Spezifizierung des Event-Elements

In Abschnitt 5.2 wurde beschrieben, welche Änderungen abonniert werden können, sowie welche Anforderungen sich daraus ergeben. In diesem Abschnitt wird analysiert, welche Anforderungen an das Event-Element zum Abonnieren von Änderungen vorliegen. Zur Einführung wird das im Metamodell der VWS ​[1]​ als experimentell gekennzeichnete *BasicEventElement* und der *EventPayload* erklärt.

Das Event-Element kann sich in seinem Typ unterscheiden. In ​[1]​ sind bereits erste Eventtypen aufgeführt. Die für das Änderungsmanagement verwendeten sind:

-   Strukturelle Änderungen von Verwaltungsschalen
-   Aktualisierungen von Teilmodellelementen und deren Attribute

Mit den strukturellen Änderungen können die Eventtypen *create* und *delete* in Verbindung gebracht werden. Für die Aktualisierungen von VWS-Elementen (s. Abbildung 5-17) bietet sich die Änderungsart *update* an. Zusätzlich zu diesen und den anderen definierten Events können laut ​[1]​ benutzerdefinierte Events spezifiziert werden. Diese müssen jedoch mit einer global eindeutigen semantischen ID versehen werden. Dies gilt ebenso für die bereits aufgezählten Eventtypen aus ​[1]​. Sie haben ebenfalls noch keine definierte semantische ID [(\#AF_12)](bookmark://AF_12)

Elemente, die durch ein Event abonniert werden können, sind wie in der Abbildung 5-17 dargestellt, Verwaltungsschalen, Concept Descriptions, Teilmodelle und alle Teilmodellelemente sowie die Metainformationen von Verwaltungsschalen und Teilmodellen.

*Hinweis:* Concept Descriptions werden in der Spezifikation ​[1]​ nicht als zu abonnierendes Element genannt ([\#AF_11](bookmark://AF_11)).

#### Spezifikation BasicEventElement

Das Event-Element selbst ist, wie in Abbildung 5-18 zu sehen, spezifiziert.

![image](https://github.com/user-attachments/assets/9ad83b32-38ee-47b9-adcf-2a5014557cd9)    
Abbildung 5-18: Spezifikation Event-Element [1]

Die aufgeführten Attribute des Event-Element haben folgende Bedeutung:

-   **observed**: Referenz auf ein referenzierbares Element.
-   **direction**: Definition der Richtung des Events (eingehend oder ausgehend).
-   **state**: Status des Events (An und Aus).
-   **messageTopic**: Eindeutige Bezeichnung des Events für die Nachrichtenübertragung mit maximal 255 Zeichen.
-   **messageBroker**: Referenz auf eine Applikation, die die Eventnachrichten entgegennimmt und verteilt.
-   **lastUpdate**: Letzter Zeitstempel an dem das letzte Event gesendet bzw. empfangen wurde.
-   **minInterval**: Minimale Dauer zwischen dem Senden bzw. Empfangen von Events.
-   **maxInterval**: Maximale Dauer zwischen dem Senden von Events, wenn kein anderer Trigger eingegangen ist. Dies gilt nur für ausgehende Events.

Es ist zu sehen, dass die Beschreibung des Events technologieunabhängig ist.

Durch die Verwendung typischer MQTT-Begriffe in der Spezifikation des *BasicEventElement* entsteht der Eindruck, dass die Nutzung von MQTT mit einem MQTT-Broker und MQTT-Topics für die Übertragung von Events in der Spezifikation der VWS implizit vorausgesetzt wird. Dies ist jedoch nicht korrekt, da dies in der Spezifikation nicht eindeutig festgelegt ist. Andere Technologien sind somit nicht ausgeschlossen. Allerdings verwenden alternative Technologien oft Konzepte, die dem MQTT-Broker und den Topics ähneln. Ein Beispiel hierfür ist eine HTTP/REST-Schnittstelle, bei der öffentliche Server als Analogie zu einem Broker fungieren und Endpunkte als Entsprechung zu den Topics dienen, an die Events gesendet werden. ([\#AF_13](bookmark://AF_13))

#### Spezifikation EventPayload

Der Inhalt des Events ist durch den *EventPayload* in Abbildung 5-19 definiert. Die Attribute haben die folgende Bedeutung:

-   **source**: Referenz auf das zugehörige Event-Element
-   **sourceSemanticId**: Semantische ID des Event-Elements, bevorzugt als externe Referenz. ([\#AF_12](bookmark://AF_12))
-   **observableReference**: Referenz auf das zu beobachtende Element, welches das Attribut *observed* in der Beschreibung des *BasicEventElement* ist.
-   **observableSemanticId**: Semantische ID des zu beobachtenden Elements.
-   **topic**: Deckungsgleich mit dem *messageTopic* des *BasicEventElement*.
-   **subjectId**: Externe Reference auf das Subjekt, dass die Erzeugung des Events bzw. Payloads vorgenommen hat.
-   **timestamp**: Zeitstempel, an dem das Event ausgelöst wurde.
-   **payload**: Spezifisch auf das Event angepasster Inhalt als Blob Element. ([\#AF_10](bookmark://AF_10))

![image](https://github.com/user-attachments/assets/d9a9a51f-097a-4631-8fbd-c8f9f923dd53)    
Abbildung 5-19: Spezifikation EventPayload [1]

Die ausführliche Spezifikation des Event-Elements, angepasst auf den Anwendungsfall des Änderungsmanagements, erfolgt in Kapitel 5.3.2.

### Integration des Events in einen Systementwurf

In diesem Abschnitt wird betrachtet, wie das Event-Element im Kontext der VWS implementiert werden kann. In der aktuellen Spezifikation des VWS-Metamodells ​[1]​ ist es als Teilmodellelement gekennzeichnet. Damit ist es laut Spezifikation nur in Teilmodellen nutzbar. Deshalb wird zu Beginn die Datenarchitektur eines Teilmodells betrachtet, in dem Event-Elemente gespeichert werden (siehe Abschnitt 5.3.3.1) können. Eine ausführliche Beschreibung der Integration des derzeitig spezifizierten Event-Elements ist in dem gemeinsam veröffentlichten Whitepaper ​[2]​ des Projekts DAVID nachzulesen.

Ein anderes Konzept, das in diesem Projekt entwickelt werden soll, sieht die Abwandlung der Metamodell-Spezifikation ​[1]​ vor. Hierbei wird das Event-Element nicht als Teilmodellelement definiert. Vielmehr wird es wie eine VWS oder ein Teilmodell mit deren Repository und Registry als eigenständiges Element betrachtet. Hierbei wird in Abschnitt 5.3.3.2 der Fokus auf die Systemarchitektur gelegt. Die Ausarbeitung des zweiten Konzepts erfolgt in Kapitel 5.4.

In beiden Konzepten ist zu beachten, dass ein Event-Element laut den Anforderungen aus Tabelle 4 die Benachrichtigung über Änderungen von Verwaltungsschalen über Concept Descriptions bis hin zu einzelnen Teilmodellelementen ermöglichen soll.

#### Datenarchitektur

Wird das Event-Element der Spezifikation [1] folgend als Teilmodellelement betrachtet, ergeben sich zwei Optionen für dessen Integration [2].

##### Option 1: Event im zugehörigen Teilmodell

Bei dieser Option wird das zu einem Teilmodellelement zugehörige Event-Element im gleichen Teilmodell gespeichert, in dem auch das zu abonnierende Teilmodellelement liegt. Abbildung 5-20 zeigt schematisch das Konzept.

Hinweis: Bei Befolgung dieses Schemas wird das Abonnieren von Änderungen an Verwaltungsschalen, deren Metainformationen und Concept Descriptions ausgeschlossen.

![image](https://github.com/user-attachments/assets/8434388b-9862-4a7f-98c2-b95c45251f27)    
Abbildung 5-20: Abonnieren durch Hinzufügen des BasicEventElement zu einem Teilmodell

##### Option 2: Ein Teilmodell nur für Events

In dieser Option ist es vorgesehen, dass ein Teilmodell zur Sammlung aller Events für eine VWS genutzt wird, siehe Abbildung 5-21. Hier können Events für die Änderungsnachverfolgung sowohl an der VWS selbst, in der das Teilmodell liegt, Concept Descriptions sowie Teilmodellen und ihren Teilmodellelementen der spezifischen VWS definiert werden. Auch das Abonnieren von Metainformationen ist mit dieser Option möglich.

Hinweis: Bei Befolgung dieses Schemas wird das Abonnieren von Informationen über das Hinzufügen bzw. Löschen einer Verwaltungsschale ausgeschlossen.

![image](https://github.com/user-attachments/assets/73f69ad8-68c8-4376-ad08-da08262809ed)    
Abbildung 5-21: Abonnieren durch Sammlung von EventElements in spezifischem Teilmodell

Die Vor- und Nachteile beider Optionen sind in Tabelle 52 zusammengefasst.

| Vorteile                                                                                                                                                             | Nachteile                                                                                                                                                                                                              |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Durch die Nutzung von Sicherheitsmechanismen wie RBAC oder ABAC sind nur die Event-Elemente zum Abonnieren sichtbar, die für den Benutzer der VWS freigegeben sind.  | Es können nur die Elemente als Events abonniert werden, die in einer VWS modelliert sind. Dadurch kann [\#AF_2](bookmark://AF_2), die Benachrichtigung z. B. über eine neu hinzugefügte VWS, nicht realisiert werden.  |
|                                                                                                                                                                      | Schlecht skalierbar mit steigender Anzahl an Verwaltungsschalen                                                                                                                                                        |

Tabelle 52: Vor- und Nachteile der Integration des Event-Elements als Teilmodellelement

#### Systemarchitektur

Nachdem das Event-Element im vorhergehenden Abschnitt als Teilmodellelement betrachtet wurde, sieht das folgende Konzept vor, das Event-Element wie eine VWS oder ein Teilmodell gemäß Abbildung 5-22 zu spezifizieren.

![image](https://github.com/user-attachments/assets/28386146-6f5a-4c85-845c-e93a89b63595)    
Abbildung 5-22: Neue Spezifizierung des Event-Elements in der VWS-Umgebung

Dieses Konzept bedingt die Definition neuer Infrastrukturkomponenten (Repository und Registry), wie sie es auch bereits für VWS, Teilmodelle und Concept Descriptions gibt. Das bedeutet, dass die aktuelle Spezifikation des VWS-Metamodells [1] geändert und für die Event-Registry, die die Endpunkte zu den Event-Elementen beinhaltet, ein Descriptor mit Metainformationen spezifiziert werden muss. Die Events selbst werden in einem bzw. mehreren separaten Repositories gehostet. Über ein Eventing Feature, das das Repository nutzt, können die Nachrichten des Events, der sogenannte Event Payload, zwischen Teilnehmern versendet werden. Das allgemeine Konzept ist in Abbildung 5-23 zu sehen. Die genaue Spezifizierung erfolgt in Kapitel 5.5. Notwendige Anpassungen am definierten Event-Element ([\#AF_17](bookmark://AF_17)) und die Definition der Schnittstellen der Infrastrukturkomponeten ([\#AF_18](bookmark://AF_18)) sind weitere Anforderungen.

![image](https://github.com/user-attachments/assets/4ec58617-59d5-4ea6-9a47-c5e54e83d57c)    
Abbildung 5-23: Infrastrukturkomponenten für das Event

Die Vor- und Nachteile des Konzepts sind in Tabelle 53 aufgeführt.

| Vorteile                                                                                | Nachteile                                                                                | Vorteile                                                                                | Nachteile                                                                                |
|-----------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------|
| Vereinfachtes Logging von Events in einem separat dafür erschaffenen Eventing Feature.  | Zunehmende Komplexität des Environments und der Interaktionen zwischen den Komponenten.  | Vereinfachtes Logging von Events in einem separat dafür erschaffenen Eventing Feature.  | Zunehmende Komplexität des Environments und der Interaktionen zwischen den Komponenten.  |
| Anwendung des Discovery-Service für vorhandene Events.                                  | Die Spezifizierung neuer Schnittstellen wird notwendig.                                  | Anwendung des Discovery-Service für vorhandene Events.                                  | Die Spezifizierung neuer Schnittstellen wird notwendig.                                  |
| Zentrale Verwaltung aller Events in einer geschlossenen Umgebung.                       |                                                                                          | Zentrale Verwaltung aller Events in einer geschlossenen Umgebung.                       |                                                                                          |

Tabelle 53: Vor- und Nachteile der Integration des Event-Elements als eigenständiges Element

### Übertragungstechnologie

Für die Übertragung der Events wird sich im Rahmen dieses Projekts auf die Nutzung von MQTT und HTTP/REST fokussiert. Aus dem Aufbau des Event-Elements aus Abschnitt 5.3.2 ist durch die Benennung der Attribute bereits ersichtlich, dass MQTT als ein Protokoll in Betracht zu ziehen ist.

Soll HTTP/REST für die Übertragung genutzt werden, müssen keine Änderungen an der Spezifikation des Event-Elements vorgenommen werden. Die Attributnamen sind in diesem Fall so zu verstehen, dass das Attribut *messageBroker* die http-Adresse der Applikation enthält, die die Events entgegennimmt und weiterleitet. Das *messageTopic* ist immer noch die eindeutige Bezeichnung für das Event selbst.

### Anforderungsliste

In Tabelle 54 sind aus Sicht des Demonstrators die Anforderungen an das Event-Element selbst, die Systemarchitektur und die Benutzerschnittstelle aufgelistet, die sich aus den vier zuvor betrachteten Aspekten ergeben haben.

| AF. Nr. | Kategorie              | Anforderung                                                                                                                                                                                                                                                                                                                                           |
|---------|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1       | Event                  | Definition von Events ohne Kenntnis von dem referenzierten Element.                                                                                                                                                                                                                                                                                   |
| 2       | Event                  | Definition von Events abhängig von einem vorher bekannten VWS-Element.                                                                                                                                                                                                                                                                                |
| 3       | Systemarchitektur      | Events, die direkt einem Element zugeordnet sind, müssen nach dem Löschen des Elements ebenfalls gelöscht werden.                                                                                                                                                                                                                                     |
| 4       | Benutzerschnittstelle  | In der Nutzeroberfläche muss das Abonnieren von Concept  Descriptions und Teilmodellen mit ihren unterlagerten Elementen durch  eine Anwahl der gewünschten Elemente möglich sein. Grund dafür ist, dass die eben genannten Elemente unabhängig von der VWS in eigenen Repositories gespeichert werden. Zusammenhang zu [\#AF_14](bookmark://AF_14).  |
| 5       | Systemarchitektur      | Werden Events zu Elementen abonniert, die noch unterlagerte Elemente beinhalten können (z.B. abonnieren eines Teilmodells mit seinen Inhalten), dann müssen automatisch die Events der unterlagerten Elemente abonniert werden.                                                                                                                       |
| 6       | Benutzerschnittstelle  | In der Nutzeroberfläche muss die Anwahl von Metainformationen für ein Abo möglich sein.                                                                                                                                                                                                                                                               |
| 7       | Systemarchitektur      | Metainformationen werden nur im gesamten aktualisiert.                                                                                                                                                                                                                                                                                                |
| 8       | Systemarchitektur      | Das Nutzertool muss die Verlinkung von Teilmodellen und Concept Descriptions zu VWS kennen, um Events korrekt an die Nutzeroberfläche weiterleiten zu können.                                                                                                                                                                                         |
| 9       | Systemarchitektur      | Concept Descriptions werden nur im gesamten aktualisiert.                                                                                                                                                                                                                                                                                             |
| 10      | Event                  | Der Inhalt einer Änderung eines Elements muss als Nachrichteninhalt im Event übersendet werden. Dies erfolgt in dem spezifizierten JSON-Datenmodell des VWS-Metamodells entsprechend dem abonnierten Element.                                                                                                                                         |
| 11      | Event                  | Der Umfang von Events soll auch die Concept Descriptions enthalten.                                                                                                                                                                                                                                                                                   |
| 12      | Event                  | Die Eventtypen *create*, *update* und delete benötigen für das jeweilige VWS-Element eine eindeutige semantische ID.                                                                                                                                                                                                                                  |
| 13      | Event                  | Event muss für MQTT und HTTP/REST anwendbar sein.                                                                                                                                                                                                                                                                                                     |
| 14      | Benutzerschnittstelle  | In der Nutzeroberfläche soll nach bestimmten verfügbaren Eventtypen gefiltert werden können. Zusammenhang mit [\#AF_12](bookmark://AF_12).                                                                                                                                                                                                            |
| 15      | Systemarchitektur      | In der Nutzeroberfläche muss angewählt werden können, welche Elemente (VWS, Teilmodell, Teilmodellelement) von dem Event-Typ *create* immer automatisch abonniert werden sollen. Zusammenhang zu [\#AF_16](bookmark://AF_16).                                                                                                                         |
| 16      | Systemarchitektur      | Events vom Typ *create* müssen nach Anwahl in der Nutzeroberfläche automatisch vom Empfänger abonniert werden.                                                                                                                                                                                                                                        |
| 17      | Systemarchitektur      | VWS4J muss um Event-Element erweitert werden, wenn eine Anpassung des bereits spezifizierten Event-Elements erfolgt.                                                                                                                                                                                                                                  |
| 18      | Systemarchitektur      | Die REST-API muss um Operationen zum Auslösen des Events erweitert werden.                                                                                                                                                                                                                                                                            |

Tabelle 54: Anforderungsliste

## Konzept

In den folgenden Abschnitten werden die erarbeiteten Lösungen für die zuvor genannten Konzeptideen und deren Anforderungen vorgestellt. Der Fokus wird daraufgelegt, das Event-Element als eigenständiges Element im Metamodell der VWS zu betrachten (s. Abschnitt 5.3.3.1.2). Das hat zur Folge, dass die Spezifikation des Event-Elements angepasst und entsprechende Infrastrukturkomponenten für die Verwaltung und Bereitstellung der Event-Elemente definiert werden müssen.

Der erste Abschnitt beschäftigt sich mit der Systemarchitektur für das Event-Element. Daran anschließend erfolgt die Definition des neu hinzugekommenen Event Descriptors sowie die Beschreibung über notwendige Anpassungen des *BasicEventElements*. Danach werden in Abschnitt 5.5 die semantischen IDs für die verwendeten Eventtypen definiert. Mit diesen grundlegenden Voraussetzungen wird die Anwendung, d.h. die Beschreibung des Events mit seinem Descriptor und dem *EventPayload* auf einzelne VWS-Elemente gezeigt. In Abschnitt 5.5.3 erfolgt die Spezifikation der Schnittstellen für die neu definierten Infrastrukturkomponenten.

### Systemarchitektur

In Abbildung 5-24 ist die technologieneutrale Systemarchitektur für das Event als eigenständiges Element des VWS-Metamodells zu sehen. Zentrales Element bildet das Eventing-Feature, dass die Verteilung der *EventPayloads* ermöglicht, während das Event Repository und die Event Registry die Event-Elemente und -Descriptoren speichern. Das Eventing-Feature selbst besteht aus einem Orchestration-Layer, dass die Kommunikation zwischen den Subkomponenten orchestriert. Dazu zählt die Konfiguration des Event Payload Transformers und des Event Routers durch die Events im Event Repository. Der Event Payload Transformer empfängt über einen externen Observer die stattfindenden Änderungen in einem VWS Repository. Diese Nachrichten werden noch nicht im spezifizierten *EventPayload* übertragen, sodass der Event Payload Transformer für verschiedene Observer die Umwandlung in den *EventPayload* vornimmt. Diese *EventPayloads* werden anschließend an den Event Router weitergeleitet. Der Event Router erzeugt mit seiner eigenen Konfiguration die Message Broker, die in den Event-Elementen spezifiziert sind. Mit dem Empfang des *EventPayloads*, verteilt der Event Router den Payload auf den richtigen Message Broker. Von außen kann nun ein Subscriber ein Event-Element aus dem Event-Repository lesen und mit Hilfe des darin beschriebenen Endpunktes des Message Brokers sich direkt mit dem jeweiligen Broker verbinden und die *EventPayloads* direkt empfangen. Die Schnittstellenspezifikation der Event-Registry und des Event-Repository erfolgt in Abschnitt 5.5.3.

![image](https://github.com/user-attachments/assets/ba0ff595-7e1a-4845-8006-bbb22fb66220)    
Abbildung 5-24: Systemarchitektur für das Event

## Definition der Event-Metamodellelemente

In der allgemeinen Systemarchitektur aus Abbildung 5-22 sind die drei wichtigen Elemente zur Realisierung des Events ersichtlich. Der *EventPayload* beinhaltet die Nachricht, die über das *BasicEventElement* gesendet werden soll. Der *EventDescriptor* wiederum enthält Metainformationen und den Endpunkt des *BasicEventElements*. Alle drei Modellelemente werden im Folgenden detailliert betrachtet und wenn notwendig neu definiert.

Begonnen wird mit dem *EventDescriptor* (s. Abbildung 5-25). Er soll unter anderem semantische Informationen über die Art des Event-Elements beinhalten. Dies geschieht über die *semanticId* und *supplementalSemanticId*. (Die genaue Definition der semanticId erfolgt in Abschnitt 5.3.3) Des Weiteren muss der Endpunkt, administrative Informationen und Benennungen des *BasicEventElements* erfolgen. Die genannten Punkte sind bereits alle im *SubmodelDescriptor* aus ​[3]​ spezifiziert, weshalb diese Struktur für den *EventDescriptor* übernommen wurde.

![image](https://github.com/user-attachments/assets/63c23df1-7042-4a61-85e2-f04324b4344d)    
Abbildung 5-25: VWS4LS Definition EventDescriptor

In Abbildung 5-26 erfolgt die neue Definition des *BasicEventElement*. Da es in dieser Lösung nicht als Teilmodellelement betrachtet wird, sind Anpassungen notwendig. Das *EventElement* muss die gleichen Metainformationen erhalten, wie ein Teilmodell, da es nun als eigenständiges Element neben dem Teilmodell betrachtet wird. Das heißt, das *EventElement* erbt von den Klassen *Identifiable*, *HasSemantics*, *Qualifiable* und *HasDataSpecification*. Die Elemente im abgeleiteten *BasicEventElement* bleiben bis auf eine Änderung der Attribute „observed“ und „messageBroker“ von „Referable“ auf „Reference“ gleich. Der Grund für die Änderung liegt darin, dass im Falle des Eventtyps „create“ für eine neue VWS, das zu beobachtende Environment verlinkt werden muss. Dies geht nicht über das Element „Referable“.

![image](https://github.com/user-attachments/assets/2551688b-f920-4e51-a004-2b353ff58cf7)    
Abbildung 5-26: a) derzeitige EventElement Spezifikation und b) VWS4LS Spezifikation

Der *EventPayload* wird ebenfalls einer kleinen Veränderung unterzogen. Der Typ der „observableReference“ wird von „Referable“ zu „Reference“ geändert, siehe Abbildung 5-27.

![image](https://github.com/user-attachments/assets/c4829b37-0760-4ed4-b6f9-67c6eaeaffbc)    
Abbildung 5-27: VWS4LS Definition EventPayload

### Festlegung der Eventtypen

Für die Definition der semantischen ID von Eventtypen, wurde ein Schema entwickelt, das die Eventtypen, die in diesem Dokument spezifizierten Änderungsarten und die zu abonnierenden VWS-Elemente einfließen lässt. Zur Erläuterung des Schemas werden zuerst die Kategorien der drei genannten Informationen eingeführt.

Erste Eventtypen sind, wie bereits erwähnt, in der Spezifikation des VWS-Metamodells [1] aufgelistet. Diese Auflistung ist in Abbildung 5-28 zu sehen, wobei die für den Anwendungsfall relevanten Eventtypen rot eingerahmt sind. Im Projekt werden für die strukturellen Änderungen Structural Change (SC) verwendet und für die Updates von bestehenden Elementen das Kürzel „**UEE**“ (Update Existing Element). Die Definition der Kürzel für die anderen Eventtypen wird hier nicht vorgenommen.

![image](https://github.com/user-attachments/assets/3d9beab5-0b34-4fcd-b05f-40df2777e25a)    
Abbildung 5-28: Kategorisierung von Eventtypen nach [1]

Die Änderungsarten wurden bereits mehrfach erwähnt und umfassen **Create, Update und Delete**.

Die VWS-Elemente, deren Änderungen abonniert werden können, wurden ebenfalls zuvor definiert (s. Abbildung 5-8).

Aus den Kategorien der drei Informationen, ergibt sich die folgende Tabelle 55 an Kombinationsmöglichkeiten für die semantische ID. Es werden einheitlich englische Begriffe verwendet

| Eventtyp                | Änderungsart    | VWS-Element                     |
|-------------------------|-----------------|---------------------------------|
| Structural Change)      | Create          | VWS                             |
|                         |                 | Submodel                        |
|                         |                 | ConceptDescription              |
| Update Existing Element | Delete  Update  | VWS                             |
|                         |                 | VWSMetainformation              |
|                         |                 | ConceptDescription              |
|                         |                 | Submodel                        |
|                         |                 | SubmodelMetainformation         |
|                         |                 | SubmodelElement                 |
|                         |                 | SubmodelElementMetainformation  |

Tabelle 55: Kategorisierung für die semantische ID eines Events

Kombiniert man die Zeilen der drei Spalten nachfolgendem Schema, ergibt sich daraus die jeweilige semantische ID.

\<Identifier\> ::= \<Namespace\>” /Event/” \<Eventtyp\>”/”\<Änderungsart\>”/”\<VWS-Element\>

\<Namespace\> ::= https://www.arena2036.de

\<Eventtyp\> ::= “SC” \| “UEE”

\<Änderungsart\> ::= “Create” \| “Update” \| “Delete”

VWS-Element ::= “VWS” \| “VWSMetainformation“ \| … (siehe Tabelle 5)

Listing 51: Darstellung der Semantischen ID

Als ein Beispiel lautet die semantische ID des Events für den Update eines bestehenden Teilmodellelements wie folgt:

„https://www.arena2036.de/Event/UEE/Update/SubmodelElement”

Listing 52: Beispielhafte Darstellung der Semantischen ID

### Modellierung des Event-Elements

Am Beispiel der Szenarien aus Kapitel 5.2 wird in den folgenden Abschnitten die zugehörige Umsetzung des Events beispielhaft gezeigt. Davor wird jedoch die allgemeine Anwendung der einzelnen Attribute des *BasicEventElements* und des *EventPayloads* nach den entwickelten Konzepten definiert.

Das Event-Element selbst ist, wie in Abbildung 5-29 zu sehen, erweitert worden.

![image](https://github.com/user-attachments/assets/b632fe51-a98d-479f-8786-c381e4b9e371)    
Abbildung 5-29: VWS4LS Definition EventElement und BasicEventElement

Die aufgeführten Attribute des Event-Element haben folgende Bedeutung:

-   **observed**: Referenz auf ein Element des VWS-Metamodells. Sollen alle Änderungen innerhalb einer VWS beobachtet werden, wird in diesem Fall eine Referenz auf eine VWS gelegt. Sollen alle Änderungen innerhalb eines Teilmodells beobachtet werden, wird das entsprechende Teilmodell referenziert. Damit wird die Erzeugung eines EventElements für jedes zu beobachtende Element, wie z.B. einer Property, vermieden. Für die Entscheidung kann der Baum mit den Eventtypen aus Kapitel 5.3 herangezogen werden. Alles, was in diesem Baum z. B. unter dem update einer VWS definiert ist, wird in dem Event berücksichtigt. Damit kann die Detailtiefe des *EventElements* vom Nutzer bestimmt werden.
-   **direction**: Definition der Richtung des Events (eingehend oder ausgehend) gemäß ​[2]​.
-   **state**: Status des Events (An und Aus).
-   **messageTopic**: Eindeutige Bezeichnung des Events für die Nachrichtenübertragung mit maximal 255 Zeichen.
-   **messageBroker**: Referenz auf eine den Endpunkt einer Applikation, die die Eventnachrichten entgegennimmt und verteilt. Hier wird vorgeschlagen, auf ein „standalone“ Teilmodell zu verweisen, dass keiner VWS zugeordnet ist. Die Beschreibung des messageBrokers kann über das bereits veröffentlichte Teilmodell „Asset Interfaces Description“, im speziellen über „EndpointMetadata“ erfolgen. Dies bietet sich an, da das Teilmodell die Beschreibung der Endpunkte sowohl für http/REST als auch für MQTT anbietet.
-   **lastUpdate**: Letzter Zeitstempel an dem das letzte Event gesendet bzw. empfangen wurde.
-   **minInterval**: Minimale Dauer zwischen dem Senden bzw. Empfangen von Events.
-   **maxInterval**: Maximale Dauer zwischen dem Senden von Events, wenn kein anderer Trigger eingegangen ist. Dies gilt nur für ausgehende Events.

Der Inhalt des Events ist durch den *EventPayload* in Abbildung 5-30 definiert und wurde nicht abgeändert. Lediglich die Nutzung der Attribute geschieht im Konzept anhand folgender Definitionen:

-   **source**: Referenz auf die eindeutige ID des zugehörigen Event-Elements. Im Gegensatz zur bisherigen Spezifikation wird hier das Element „Reference“ anstatt „Referable“ genutzt. Das erlaubt auch im Fall der Benachrichtigung über neue VWS in einem Repository, das Repository zu verlinken.
-   **sourceSemanticId**: Semantische ID des Event-Elements, definiert durch Kapitel 5.3.2.
-   **observableReference**: Referenz auf das sich geänderte Element. Im Fall, dass im *BasicEventElement* eine ganze VWS beobachtet werden soll und sich nun eine einzelne Property geändert hat, wird hier durch den Publisher die Referenz auf die Property gelegt. Somit wird im „payload“ Attribut nicht die gesamte VWS übertragen, sondern nur das geänderte Element.
-   **observableSemanticId**: Semantische ID des geänderten Elements.
-   **topic**: Deckungsgleich mit dem *messageTopic* des *BasicEventElement*.
-   **subjectId**: Externe Reference auf das Subjekt, dass die Erzeugung des Events bzw. Payloads vorgenommen hat. Hier wird vorgeschlagen, den Aktor mit einer eindeutigen IRI anzugeben, der das Element geändert hat. Beispielsweise kann dies die IRI eines Unternehmens, wie in den Beispielen der Komponentenhersteller, oder einer Applikation, wie einem MES, sein.
-   **timestamp**: Zeitstempel, an dem das Event ausgelöst wurde.
-   **payload**: Spezifisch auf das geänderte Element angepasster Inhalt als serialisierter JSON-String. Im Falle einer strukturellen Änderung in einem Teilmodell, wird das gesamte Teilmodell übergeben. Sollte kein Payload angegeben werden, kann der Inhalt des Elements über die observaleReference und einem Zugriff auf den Server, der das Element hostet, abgerufen werden. Das ist vor allem sinnvoll, wenn Files in einem Teilmodellelement gespeichert werden, die nicht als JSON-String übertragen werden können.

![image](https://github.com/user-attachments/assets/4f2ef267-b5a6-4fed-bea3-7adf0bf30f7d)    
Abbildung 5-30: VWS4LS Definition EventPayload

#### Update von Teilmodellelementen

Abbildung 5-31 zeigt eine exemplarische Modellierung für das 3. Szenario aus Kapitel 5.2, dass im VWS4LS-Demonstrator umgesetzt wurde. In diesem Fall soll eine Benachrichtigung erfolgen, sobald der Wert eines bestimmten Teilmodellelements verändert wurde.

Das Attribut „observed“ des BasicEventElements verweist auf das Referable des abonnierten Teilmodellelements, zum Beispiel eine Property. Das Attribut „HasSemantics“ des BasicEventElements gibt an, über welche Art von Änderung benachrichtigt werden soll. Hierbei wird die definierte semantische ID aus Kapitel 5.3.2 verwendet und ist im Fall des Updates eines Teilmodellelements folgende:

„https://www.arena2036.de/Event/UEE/Update/SubmodelElement”

Listing 53: Beispielhafte Umsetzung

Als „source“ des *EventPayload* wird das *Identifiable* des zugehörigen *BasicEventElement* definiert. Das Attribut „sourceSemanticId“ entspricht dabei exakt dem Attribut „HasSemantics“ des *BasicEventElements*. Das Attribut „observableReference“ enthält in diesem Beispiel analog zum „observed“ des *BasicEventElements* das *Referable* der überwachten Property. Im Falle, dass im „observed“ des *BasicEventElements* die Updates einer VWS beobachtet werden sollen, kann im Attribut „observableReference“ die Referenz auf das Teilmodellelement erfolgen, wenn sich nur dies geändert hat. Die „observableSemanticID“ enthält die semantische ID der beobachteten Property. Das Attribut „Topic“ übernimmt denselben Wert wie das Attribut „messageTopic“ des *BasicEventElement*.

![image](https://github.com/user-attachments/assets/c40d304f-6dd0-4391-b3b9-f2aa887a8627)     
Abbildung 5-31: Modellierung update-Event für ein Teilmodellelement (Szenario 1)

#### Create von Teilmodellen

Abbildung 5-32: Modellierung create-Event für neue Teilmodelle in einer VWS (Szenario 2) zeigt die exemplarische Modellierung des 2. Szenarios aus Kapitel 5.2, und zwar dem Abonnieren neu zu einer VWS hinzugefügten Teilmodellen.

Das Attribut „observed“ des *BasicEventElement* verweist auf die aasId der überwachten VWS, die auf ein neues Teilmodell hin beobachtet werden soll. Das Attribut „HasSemantics“ hat den Wert:

„https://www.arena2036.de/Event/SC/Create/Submodel”

Als „source“ des *EventPayload* wird das *Identifiable* des zugehörigen *BasicEventElements* definiert. Das Attribut „sourceSemantic“ entspricht dabei exakt dem Attribut „HasSemantics“ des *BasicEventElements*. Das Attribut „observableReference“ im *EventPayload* verweist in diesem Fall auf das neu hinzugefügte Teilmodell. Die „observableSemanticID“ des „EventPayload“ enthält die semantische ID des neuen Teilmodells. Das Attribut „topic“ übernimmt denselben Wert wie das Attribut „messageTopic“ des *BasicEventElements*. Der „payload“ des Events ist das neu hinzugefügte Teilmodell.

![image](https://github.com/user-attachments/assets/b7bf3adc-93c9-46d0-9f57-ecaba4584cc0)     
Abbildung 5-32: Modellierung create-Event für neue Teilmodelle in einer VWS (Szenario 2)

#### Create von VWS

Abbildung 5-33 zeigt eine exemplarische Modellierung eines Events für die Erstellung (create) einer VWS aus dem 3. Szenario (s. Kapitel 5.2). Das Attribut „observed“ des *BasicEventElement* verweist auf das zu beobachtende VWS-Environment. Das Attribut „HasSemantics“ gibt an, über welche Art von Änderung das jeweilige *BasicEventElement* benachrichtigen soll, in diesem Fall:

„https://www.arena2036.de/Event/SC/Create/VWS”

Listing 54: Beispielhafte Umsetzung

Als Quelle im *EventPayload* wird das *Identifiable* des *BasicEventElements* angegeben und die „sourceSemanticId“ enthält den gleichen Wert wie die semanticID des *BasicEventElements*. Das Attribut „observableReference“ enthält die Referenz (*Identifiable*) auf die neue VWS. Die „observableSemanticID“ ist in diesem Fall leer, da eine VWS keine semanticID besitzt. Als „payload“ wird die neue VWS in JSON-Serialisierung übergeben. Ist kein Payload angefügt, kann über die „observableReference“ die VWS mittels eines Zugriffs auf das Environment vollständig heruntergeladen werden.

![image](https://github.com/user-attachments/assets/12f13fb3-78b9-4126-ab30-e735ca326050)     
Abbildung 5-33: Modellierung creat-Events für neue VWS in definiertem Environment (Szenario 3)

### Spezifikation der Infrastrukturkomponenten-Schnittstellen

In Abschnitt 5.4.1 wurde die technologieneutrale Systemarchitektur für das Event-Element als eigenständige Komponente vorgestellt. Zur Umsetzung der vorgestellten Anwendungsfälle erfolgt die Spezifikation der Schnittstellen von Event-Registry und -Repository in Anlehnung an die API-Spezifikation der VWS​ [3]​ in englischer Sprache. Die zur Verfügung stehenden Operationen orientieren sich dabei an den Operationen des VWS- und Teilmodell-Registries, bzw. -Repositories.

#### Event-Registry-Interface

Die Event-Registry bietet über die in Tabelle 56 angegebenen Operationen einen zur VWS- oder Teilmodell-Registry vergleichbaren Funktionsumfang. Die enthaltenen Deskriptoren können in ihrer Gesamtheit oder einzeln per Event ID (siehe Definition von *EventElement* in Abschnitt 5.3.2) aufgerufen werden. Neue Deskriptoren können durch eine zusätzliche Operation angelegt werden, bereits vorhandene ersetzt oder gelöscht werden.

| Operation Name             | Description                                                                     |
|----------------------------|---------------------------------------------------------------------------------|
| GetAllEventDescriptors     | Returns all Event Descriptors                                                   |
| GetEventDescriptorById     | Returns a specific Event Descriptor                                             |
| PostEventDescriptor        | Creates a new Event Descriptor, i.e., registers an Event                        |
| PutEventDescriptorById     | Replaces an existing Event Descriptor, i.e., replaces registration information  |
| DeleteEventDescriptorById  | Deletes an Event Descriptor, i.e., deregisters an Event                         |

Tabelle 56: Event-Registry-Interface

Für den Zugriff per HTTP/REST ergeben sich entsprechend unterschiedliche URIs, um die Operationen umzusetzen. Diese Anfragen können durch GET, POST, PUT und DELETE umgesetzt werden und sind in Tabelle 57 angegeben.

| Operation Name             | URI                                                                                   |
|----------------------------|---------------------------------------------------------------------------------------|
| GetAllEventDescriptors     | GET http://\<host\>:\<port\>/event-descriptors                                        |
| GetEventDescriptorById     | GET http://\<host\>:\<port\>/event-descriptors/\<descriptor-id\>                      |
| PostEventDescriptor        | POST http://\<host\>:\<port\>/event-descriptors \<EventDescriptor\>                   |
| PutEventDescriptorById     | PUT http://\<host\>:\<port\>/event-descriptors/\<descriptor-id\> \<EventDescriptor\>  |
| DeleteEventDescriptorById  | DELETE http://\<host\>:\<port\>/event-descriptors/\<descriptor-id\>                   |

Tabelle 57: Event-Registry-HTTP-REST-URIs

Die Ein- und Ausgabeparameter der Operationen werden in Tabelle 58 bis Tabelle 512 angegeben.

| semanticId        | https://arena2036.de/event/API/GetAllEventDescriptors  |        |                     |              |
|-------------------|--------------------------------------------------------|--------|---------------------|--------------|
| Name              | Description                                            | Mand.  | Type                | Cardinality  |
| Input Parameters  |                                                        |        |                     |              |
| limit             | Maximum size of result set                             | no     | nonNegativeInteger  | 1            |
| cursor            | Position from which to resume the result listing       | no     | string              | 1            |
| Output Parameters |                                                        |        |                     |              |
| statusCode        | Status Code                                            | yes    | StatusCode          | 1            |
| payload           | List of Event Descriptors                              | no     | EventDescriptor     | 1..\*        |

Tabelle 58: Parameter GetAllEventDescriptors

| semanticId        | https://arena2036.de/event/API/GetEventDescriptorById  |        |                  |              |
|-------------------|--------------------------------------------------------|--------|------------------|--------------|
| Name              | Description                                            | Mand.  | Type             | Cardinality  |
| Input Parameters  |                                                        |        |                  |              |
| identifier        | The descriptors unique id (Base64)                     | yes    | Identifier       | 1            |
| Output Parameters |                                                        |        |                  |              |
| statusCode        | Status Code                                            | yes    | StatusCode       | 1            |
| payload           | Requested Event Descriptor                             | no     | EventDescriptor  | 1            |

Tabelle 59: Parameter GetEventDescriptorById

| semanticId        | https://arena2036.de/event/API/PostEventDescriptor  |        |                  |              |
|-------------------|-----------------------------------------------------|--------|------------------|--------------|
| Name              | Description                                         | Mand.  | Type             | Cardinality  |
| Input Parameters  |                                                     |        |                  |              |
| eventDescriptor   | Object containing the events id and endpoint        | yes    | EventDescriptor  | 1            |
| Output Parameters |                                                     |        |                  |              |
| statusCode        | Status Code                                         | yes    | StatusCode       | 1            |
| payload           | Created Event Descriptor                            | yes    | EventDescriptor  | 1            |

Tabelle 510: Parameter PostEventDescriptor

| semanticId        | https://arena2036.de/event/API/PutEventDescriptorById  |        |                  |              |
|-------------------|--------------------------------------------------------|--------|------------------|--------------|
| Name              | Description                                            | Mand.  | Type             | Cardinality  |
| Input Parameters  |                                                        |        |                  |              |
| eventDescriptor   | Object containing the events id and endpoint           | yes    | EventDescriptor  | 1            |
| Output Parameters |                                                        |        |                  |              |
| statusCode        | Status Code                                            | yes    | StatusCode       | 1            |
| payload           | Replaced Event Descriptor                              | no     | EventDescriptor  | 1            |

Tabelle 511: Parameter PutEventDescriptorById

| semanticId        | https://arena2036.de/event/API/DeleteEventDescriptorById  |        |             |              |
|-------------------|-----------------------------------------------------------|--------|-------------|--------------|
| Name              | Description                                               | Mand.  | Type        | Cardinality  |
| Input Parameters  |                                                           |        |             |              |
| eventIdentifier   | The descriptors unique id (Base64 encoded)                | yes    | Identifier  | 1            |
| Output Parameters |                                                           |        |             |              |
| statusCode        | Status Code                                               | yes    | StatusCode  | 1            |

Tabelle 512: Parameter DeleteEventDescriptorById

#### Event-Repository-Interface

Der Funktionsumfang des Event-Repositories orientiert sich an den Operationen von VWS- und Teilmmodell-Repository. Die zur Verfügung stehenden Interfaces werden in Tabelle 513 angegeben. Die hinterlegten Events können gruppenweise nach IdShort, bzw. SemanticId oder SupplementalSemanticId, oder einzeln per ID ausgelesen werden. Neue Events können angelegt, vorhandene ersetzt oder gelöscht werden.

| Operation Name            | Description                                                               |
|---------------------------|---------------------------------------------------------------------------|
| GetAllEvents              | Returns all Events                                                        |
| GetEventById              | Returns a specific Event                                                  |
| GetAllEventsBySemanticId  | Returns all Events with a specific SemanticId                             |
| GetAllEventsByIdShort     | Returns all Events with a specific idShort                                |
| PostEvent                 | Creates a new Event. The id of the new Event must be set in the payload.  |
| PutEventById              | Replaces an existing Event                                                |
| DeleteEventById           | Deletes an Event                                                          |

Tabelle 513: Event-Repository-Interface

Für den Zugriff per HTTP/REST ergeben sich entsprechend unterschiedliche URIs, um die Operationen umzusetzen. Diese Anfragen können durch GET, POST, PUT und DELETE umgesetzt werden und sind in Tabelle 514 bis Tabelle 521 angegeben.

| Operation Name                          | URI                                                               |
|-----------------------------------------|-------------------------------------------------------------------|
| GetAllEvents                            | GET http://\<host\>:\<port\>/event                                |
| GetEventById                            | GET http://\<host\>:\<port\>/event/\<event-id\>                   |
| GetAllEventsBySemanticId                | GET http://\<host\>:\<port\>/event?semanticId=\<semanticId\>      |
| GetAllEventsByIdShort (*experimental*)  | GET http://\<host\>:\<port\>/event?idShort=\<idShort\>            |
| PostEvent                               | POST http://\<host\>:\<port\>/event \<EventElement\>              |
| PutEventById                            | PUT http://\<host\>:\<port\>/event/\<event-id\> \<EventElement\>  |
| DeleteEventById                         | DELETE http://\<host\>:\<port\>/event/\<event-id\>                |

Tabelle 514: Event-Repository-HTTP-REST-URIs

| semanticId             | https://arena2036.de/event/API/GetAllEvents      |        |                        |              |
|------------------------|--------------------------------------------------|--------|------------------------|--------------|
| Name                   | Description                                      | Mand.  | Type                   | Cardinality  |
| Input Parameters       |                                                  |        |                        |              |
| serializationModifier  | Format of the response                           | yes    | SerializationModifier  | 1            |
| limit                  | Maximum size of result set                       | no     | nonNegativeInteger     | 1            |
| cursor                 | Position from which to resume the result listing | no     | string                 | 1            |
| Output Parameters      |                                                  |        |                        |              |
| statusCode             | Status Code                                      | yes    | StatusCode             | 1            |
| payload                | List of Events                                   | no     | EventElement           | 1..\*        |

Tabelle 515: Parameter GetAllEvents

| semanticId             | https://arena2036.de/event/API/GetEventById  |        |                        |              |
|------------------------|----------------------------------------------|--------|------------------------|--------------|
| Name                   | Description                                  | Mand.  | Type                   | Cardinality  |
| Input Parameters       |                                              |        |                        |              |
| id                     | The events unique id (Base64)                | yes    | Identifier             | 1            |
| serializationModifier  | Format of the response                       | yes    | SerializationModifier  | 1            |
| Output Parameters      |                                              |        |                        |              |
| statusCode             | Status Code                                  | yes    | StatusCode             | 1            |
| payload                | Requested Event Element                      | yes    | EventElement           | 1            |

Tabelle 516: Parameter GetEventById

| semanticId             | https://arena2036.de/event/API/GetAllEventsBySemanticId |        |                        |              |
|------------------------|---------------------------------------------------------|--------|------------------------|--------------|
| Name                   | Description                                             | Mand.  | Type                   | Cardinality  |
| Input Parameters       |                                                         |        |                        |              |
| semanticId             | Id of the semantic definition (Base64 encoded)          | yes    | Reference              | 1            |
| serializationModifier  | Format of the response                                  | yes    | SerializationModifier  | 1            |
| limit                  | Maximum size of result set                              | no     | nonNegativeInteger     | 1            |
| cursor                 | Position from which to resume the result listing        | no     | string                 | 1            |
| Output Parameters      |                                                         |        |                        |              |
| statusCode             | Status Code                                             | yes    | StatusCode             | 1            |
| payload                | Requested Event Elements                                | no     | EventElement           | 1..\*        |

Tabelle 517: Parameter GetAllEventsBySemanticId

| semanticId             | https://arena2036.de/event/API/GetAllEventsByIdShort  |        |                        |              |
|------------------------|-------------------------------------------------------|--------|------------------------|--------------|
| Name                   | Description                                           | Mand.  | Type                   | Cardinality  |
| Input Parameters       |                                                       |        |                        |              |
| idShort                | IdShort of the event (Base64)                         | yes    | NameType               | 1            |
| serializationModifier  | Format of the response                                | yes    | SerializationModifier  | 1            |
| limit                  | Maximum size of result set                            | no     | nonNegativeInteger     | 1            |
| cursor                 | Position from which to resume the result listing      | no     | string                 | 1            |
| Output Parameters      |                                                       |        |                        |              |
| statusCode             | Status Code                                           | yes    | StatusCode             | 1            |
| payload                | Requested Event Elements                              | no     | EventElement           | 1..\*        |

Tabelle 518: Parameter GetAllEventsByIdShort (experimental)

| semanticId        | https://arena2036.de/event/API/PostEvent  |        |               |              |
|-------------------|-------------------------------------------|--------|---------------|--------------|
| Name              | Description                               | Mand.  | Type          | Cardinality  |
| Input Parameters  |                                           |        |               |              |
| event             | Event Element Object                      | yes    | EventElement  | 1            |
| Output Parameters |                                           |        |               |              |
| statusCode        | Status Code                               | yes    | StatusCode    | 1            |
| payload           | The created Event Element                 | yes    | EventElement  | 1            |

Tabelle 519: Parameter PostEvent

| semanticId        | https://arena2036.de/event/API/PutEventById  |       |              |             |
|-------------------|----------------------------------------------|-------|--------------|-------------|
| Name              | Description                                  | Mand. | Type         | Cardinality |
| Input Parameters  |                                              |       |              |             |
| event             | Event Element Object                         | yes   | EventElement | 1           |
| Output Parameters |                                              |       |              |             |
| statusCode        | Status Code                                  | yes   | StatusCode   | 1           |
| payload           | The replaced Event Element                   | no    | EventElement | 1           |

Tabelle 520: Parameter PutEventById

| semanticId        | https://arena2036.de/event/API/DeleteEventById  |        |             |              |
|-------------------|-------------------------------------------------|--------|-------------|--------------|
| Name              | Description                                     | Mand.  | Type        | Cardinality  |
| Input Parameters  |                                                 |        |             |              |
| id                | The events unique id (Base64)                   | yes    | Identifier  | 1            |
| Output Parameters |                                                 |        |             |              |
| statusCode        | Status Code                                     | yes    | StatusCode  | 1            |

Tabelle 521: Parameter DeleteEventById

## BaSyx UI – Änderungsmanagement

Ein weiteres Eclipse BaSyx™ Web UI Modul, welches im Rahmen von TP14 entstanden ist, dient der Abbildung des Änderungsmanagements. Ziel ist die Benachrichtigung von Nutzern über Änderungen in Verwaltungsschalen. Das können beispielsweise Auftragsverwaltungsschalen oder Produktverwaltungsschalen sein. Produkt meint dabei den Leitungssatz. Im Anwendungsfall wird beispielhaft die Änderung des Produktionsstatus betrachtet.

Anforderung an das Modul ist die Möglichkeit einzelne Datenpunkte und zusammenhängende Datenobjekte (Teilmodelle) zu Abonnieren. Abonnierte Elemente werden dann auf Änderungen überwacht. Erfolgt eine Änderung in einem abonnierten Element, wird dies dem Abonnenten über das Änderungsmanagement-Modul mitgeteilt.

Das Modul selbst ist in zwei Hauptfunktionalitäten unterteilt. Es kann zum einen über den „Abonnieren“ Reiter auf die Oberfläche gewechselt werden, um neue Elemente (*Properties*, *SubmodelElementCollections*, …) zu abonnieren. Zum anderen kann per Click auf den Reiter „Änderungen“ eine Liste aller Änderungsbenachrichtigungen angezeigt werden. Hier werden chronologisch alle Nachrichten gezeigt, die nicht bereits als gelesen bestätigt wurden.

Zunächst wird der Prozess des Abonnierens von Elementen detailliert (siehe Abbildung 5-34). Das Modul zeigt zunächst eine Liste aller registrierten Verwaltungsschalen des Systems (linke Spalte). Der Anwender kann aus der Liste eine Verwaltungsschale nach Belieben auswählen. Erfolgt eine Auswahl, zeigt das Modul dem Nutzer alle enthaltenen Teilmodelle (mittlere Spalte). Aus den Teilmodellen können Properties aber auch ganze *SubmodelElementCollections* (verschachtelte Properties) angehakt werden (rechte Spalte).

Nach dem Anhaken aller für den Anwender relevanten Elemente kann dieser über die Schaltfläche „Abonnements aktualisieren“ eine Anfrage der Abonnements an das Event-Feature versenden. Das Event-Feature speichert die angefragten Abonnements in einem Event-Repository, welches ein HTTP/REST Server ist und der ähnlich wie ein Verwaltungsschalenserver Event Elemente als Datenobjekte speichert. In diesem Fall werden Abonnements persistiert. Die Anfrage erfolgt an den /subscribe-Endpunkt des Event-Features. Als Anfrageinhalt werden „Subscription-Objekte“ mitgegeben. Diese enthalten jeweils vier wesentliche Eigenschaften:

1.  Eine „*EventID*“ als eindeutige Identifizierung eines Event-Elements,
2.  Eine „*ElementID*“ für die Zuordnung zu einem Datenpunkt in einer Verwaltungsschale,
3.  Eine „*SemanticID*“, welche angibt, um welchen Typ von Element es sich handelt und
4.  Eine “SubmodelID”, für das Teilmodell mit dem zu beobachtenden Element.

Bei Erfolgreicher Erstellung eines Abonnements von Elementen einer Verwaltungsschale, werden die angelegten „Subscription-Objekte“ zurückgegeben. Somit hat der Anwender Einblick, welche Elemente er bereits abonniert hat. Diese Information kann jederzeit ebenfalls eingesehen werden, wenn auf den „Abonnieren“-Reiter auf der Hauptseite des Moduls navigiert wird. Dort wird zu Beginn eine Anfrage an das Event-Feature gesendet, welche Elemente abonniert wurden. Ein Löschen von Abonnements ist ebenfalls möglich durch das Entfernen des Hakens neben dem betreffenden Element der ausgewählten Verwaltungsschale.

![image](https://github.com/user-attachments/assets/fd3c1a28-bdf8-4937-8568-4c8dd5fefc95)    
Abbildung 5-34: BaSyx UI - Änderungsmanagement abonnieren

Im Weiteren werden die Änderungsbenachrichtigungen betrachtet (siehe Abbildung 5-35). Auch hier wird zunächst eine Anfrage an das Event-Feature gesendet, auf die es mit einer Liste aller ungelesenen Event Payloads antwortet. Diese werden grafisch im Modul unterteilt nach ungelesenen, also neuen Event Payloads bzw. Nachrichten und bereits gelesenen Nachrichten (vgl. Abbildung 3-3). Nachrichten können durch den Nutzer angewählt werden. Erfolgt dies, wird im Zentrum der Oberfläche die neue Änderung dargestellt. Dies erfolgt bisher prototypisch im JSON-Format. Angewählte und damit auch angesehene Nachrichten werden automatisch als gelesen markiert. Im Hintergrund erfolgt eine Anfrage an den Server, die den Status des Event Elements auf „gelesen“ aktualisiert. Ein neu Laden der Seite führt dazu, dass bereits gelesene Nachrichten ausgeblendet werden. Als Nachrichtentitel in der linken Spalte wird bisher die ID des Event Payloads angezeigt. Dies kann jedoch abgeändert werden und Informationen aus dem verlinkten Event Element können hier eingesetzt werden. Im Event Payload ist die Referenz auf das zu beobachtende Element zu sehen. Im Beispiel aus Abbildung 5-35 ist dies die URI des Produkts, die zuvor in Abbildung 5-34 abonniert wurde. Der Payload wird als byte[] übertragen und kann entsprechend decodiert werden.

![image](https://github.com/user-attachments/assets/2fd7d5c1-d38d-4024-ad9b-9e32c39e3b7d)     
Abbildung 5-35: BaSyx UI - Änderungsmanagement Nachrichten

## Zusammenfassung

Ein Ziel in VWS4LS war die nähere Untersuchung und Anwendung des als experimentell gekennzeichneten Event-Elements der VWS. Dafür wurden drei Anwendungsszenarien definiert, anhand derer die Nutzung des Event-Elements gezeigt werden sollten. Anhand der Szenarien wurden Anforderungen an das Event-Element selbst, der Systemarchitektur, in der es integriert ist und dessen Nutzung durch einen Weboberfläche definiert. Diese Anforderungen wurden in einem Konzept umgesetzt, dass das Event-Element nicht mehr als Teilmodellelement sieht, sondern als eigenständiges Element neben der VWS und den Teilmodellen. In Folge dieses Konzepts wurde die Definition neuer Infrastrukturkomponenten notwendig, die ähnliche Funktionen wie die bereits existierenden Infrastrukturkomponenten (z. B. VWS-Repository und -Registry) bereitstellen. Als Grundlage für die Implementierung wurde das Eclipse BaSyx Framework genutzt und um eine Event-Registry und ein Event-Repository erweitert. Der Code hierfür ist im [VWS4LS GitHub](VWS4LS/vws4ls-event-infrastructure:%20Contains%20the%20implementation%20of%20the%20Eventing%20Feature)[^1] zu finden. Für die Implementierung des *EventPayload* Transfers wurde ein Eventing Feature definiert, dass die Sammlung und Verteilung gemäß der neu spezifizierten Event-Elemente der VWS ermöglicht. Aufgrund der kurzen Zeitspanne zur Untersuchung dieses Themas, wurde nur ein Anwendungsszenario, das Abonnieren eines Updates von Teilmodellelementen, prototypisch umgesetzt.

[^1]: <https://github.com/VWS4LS/vws4ls-event-infrastructure>

Ergebnisse dieses Projekts sind zum einen in das Whitepaper des Projekts DAVID mit eingeflossen. Zum anderen wurde vor Abschluss des Projekts ein Beitrag „[*Towards an AAS Event Mechanism: A proposal to extend the AAS specification*](https://github.com/VWS4LS/vws4ls-subproject-results/upload/main/TP14)“[^2] bei der „*30th IEEE International Conference on Emerging Technologies and Factory Automation (ETFA)“* eingereicht. Die Annahme oder Ablehnung war zum Zeitpunkt der Beendigung des Projekts noch nicht bekannt.

[^2]: <https://github.com/VWS4LS/vws4ls-subproject-results/upload/main/TP14>

