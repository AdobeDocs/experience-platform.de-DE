---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Produktdokumentation zu Adobe Experience Platform
topic: getting started
translation-type: tm+mt
source-git-commit: a5268c2d31d356ce479bdcc143050cd513259235
workflow-type: tm+mt
source-wordcount: '6973'
ht-degree: 0%

---


# Adobe Experience Platform Glossar {#adobe-experience-platform-glossary}

## A

**Zugriffskontrolle:** {#access-control} Zugriffskontrolle für Experience Platform verknüpft Benutzer mit Zugriffsberechtigungen und Sandbox-Umgebung über Produkt-Profil in der Adobe Admin-Konsole.

**Zugriffsschlüssel-ID:** Die Zugriffsschlüssel-ID ist eine eindeutige Kennung, die mit einem geheimen Zugriffsschlüssel für Amazon S3 verknüpft ist. Die Zugriffsschlüssel-ID und der geheime Zugriffsschlüssel werden zusammen verwendet, um AWS-Anforderungen zu signieren.

**Aktion:** Beim Start der Erlebnisplattform handelt es sich bei einer Aktion um einen bestimmten Typ von Regelkomponente, mit der festgelegt wird, was nach dem Eintreten eines Ereignisses geschehen soll und welche Bedingungen ausgewertet und weitergereicht werden.

**Aktivieren:** In der Echtzeit-Kundendatenplattform ist &quot;Aktivieren&quot;die Aktion, die ein Benutzer zur Zuordnung eines Segments oder von Profilen zu einem Ziel wie Oracle Eloqua, Google oder Salesforce Marketing Cloud durchführt.

**Aktivität:** Im Entscheidungsdienst ist eine Aktivität eine Reihe von Angeboten, aus denen der Marketingspezialist das beste Angebot auswählen möchte.

**Adobe Admin Console:** Die Adobe Admin-Konsole bietet eine zentrale Stelle für die Verwaltung der Zugriff- und Funktionsberechtigungen für Ihr Unternehmen.

**Adobe Experience Platform:** Die Adobe Experience Platform standardisiert Daten und Inhalte im gesamten Unternehmen und ermöglicht so Echtzeit-Profile für Konsumenten, Datenerhebung und schnellere Inhaltsgeschwindigkeit, um die Personalisierung von Erlebnissen während der gesamten Customer Journey zu fördern.

**Adobe Connectors:** Adobe Connectors sind vorkonfigurierte Verbindungen, die von Adobe erstellt wurden, um Daten in die und aus der Experience Platform zu übertragen. Dazu gehören Microsoft Dynamics, Salesforce, Amazon S3 und Azurblut.

**Adobe Intelligent Services:** Adobe Sensei ist der intelligente Rahmen für Experience Platform. Es bietet außerdem eine Reihe von AI-Diensten, die Marken in die Lage versetzen, ihre Fähigkeit zur Bereitstellung personalisierter Echtzeit-Kundenerlebnisse zu verbessern.

**Adobe-E/A:** Adobe I/O ist Teil der Experience Platform und bietet Zugriff auf alles, was Entwickler zur Integration, Erweiterung und Anpassung der Adobe Experience Platform benötigen, einschließlich APIs, Ereignis, Entwicklerkonsole und hilfreicher Werkzeuge.

**Adobe Sensei:** Adobe Sensei ist der intelligente Rahmen für Experience Platform. Es bietet außerdem eine Reihe von AI-Diensten, die Marken in die Lage versetzen, ihre Fähigkeit zur Bereitstellung personalisierter Echtzeit-Kundenerlebnisse zu verbessern.

**Amazon S3-Behälter:** Amazon S3-Behälter sind die grundlegenden Container für im Amazon-Ökosystem gespeicherte Daten. Behälter enthalten Objekte, die Objekte werden mit einem eindeutigen Schlüssel gespeichert und abgerufen, der dem Entwickler zugewiesen wurde.

**Amazon S3 Connector:** Mit dem Amazon S3 Connector können Kunden von Experience Platform ihre Amazon S3-Daten sicher verbinden und darauf zugreifen.

**Speicherstrategie anhängen:** Die `Append` Speicherstrategie ist eine Option, die verwendet wird, wenn Daten von Drittanbietern angegeben werden, die über eine Verbindung aufgenommen werden sollen, und neue Daten oder Zeilen am Ende des Datensatzes angehängt werden. Die zuvor erfassten Zeilen bleiben unberührt und nur die seit der letzten geplanten Ausführung erstellten Zeilen werden in Experience Platform aufgenommen. Alle Zeilen, die im Quellsystem geändert wurden, bleiben auf Experience Platform unverändert.

**Anwendungslebenszyklusmanagement:** Das Application Lifecycle Management ermöglicht die Erstellung separater virtueller Umgebung zur Entwicklung und Weiterentwicklung digitaler Erlebnisanwendungen.

**Array:** Arrays werden für geordnete Elemente mit demselben Datentyp verwendet.

**Künstliche Intelligenz:** Künstliche Intelligenz ist eine Theorie und Entwicklung von Computersystemen, die in der Lage sind, Aufgaben auszuführen, die normalerweise menschliche Intelligenz erfordern, wie visuelle Wahrnehmung, Spracherkennung, Entscheidungsfindung und Übersetzung zwischen Sprachen.

**Attribute:** Attribute sind bestimmte Eigenschaften, die ein Profil darstellen.

**Attributzusammenführung:** Die Attributzusammenführung definiert, wie eine Richtlinie zum Zusammenführen den Attributwert des Profils bei Datenkonflikten priorisiert.

**Zuordnung AI:** Attribution AI ist ein Adobe Sensei Service, der algorithmische Funktionen zur Zuordnung mehrerer Kanal über den gesamten Kundenlebenszyklus hinweg bereitstellt.

**Audience**: Eine Audience ist der resultierende Satz von Profilen, die die Kriterien einer Segmentdefinition erfüllen.

**Audience Snapshot**: Ein Audience-Schnappschuss erfasst alle Profil, die zum Zeitpunkt der Segmentierung für die Segmentkriterien infrage kommen.

[Zurück zum Anfang](#adobe-experience-platform-glossary)

## B

**Aufstockung:** In der Echtzeit-Kundendatenplattform ermöglicht die Aufstockung in geplanten Quellverbindungen die Erfassung historischer Daten.

**Aufstockungszeitraum:** `Backfill period` ist eine Option, um die Dauer für die Erfassung von Verlaufsdaten von Drittanbietern über eine Verbindung festzulegen. Wenn Sie einen Aufstockungszeitraum für immer wählen, wird der gesamte Verlauf der Quelldaten an die Experience Platform übertragen.

**Stapel:** Der Stapel ist ein Datensatz, der über einen bestimmten Zeitraum erfasst und als eine Einheit verarbeitet wird.

**Stapel-ID:** Stapel-ID ist ein von Adobe generierter Bezeichner für einen Stapel von Daten.

**Batch Ingestion:** Die Stapelverarbeitung ermöglicht es Benutzern, Petabyte von Daten zu erfassen und sie in Unternehmenssystemen verfügbar zu machen. Mit den neuesten Technologien können Benutzer jetzt jedes beliebige Schema XDM und Nicht-XDM in Experience Platform aufnehmen.

**Stapelsegmentierung:** Die Stapelsegmentierung ist eine Alternative zu einem laufenden Datenauswahlprozess und verschiebt alle Profil-Daten gleichzeitig durch Segmentdefinitionen, um entsprechende Audiencen zu erstellen. Nach der Erstellung wird dieses Segment gespeichert und gespeichert, damit es zur Verwendung exportiert werden kann.

**Erstellen:** Beim Start der Experience Platform handelt es sich bei einem Build um eine bereitgestellte Bibliothek. Der Build ist eine Datei oder ein Satz von Dateien, die alle Konfigurationen und den Code enthalten, die zum Ausführen der Geschäftslogik in dieser Bibliothek erforderlich sind.

**Business Intelligence-Tools:** Business Intelligence, auch &quot;BI&quot;-Tools genannt, sind in erster Linie in den Experience Platform Abfrage Service integriert. BI-Tools sind Typen von Anwendungssoftware, die große Mengen unstrukturierter Daten von internen und externen Systemen erfassen und verarbeiten.

[Zurück zum Anfang](#adobe-experience-platform-glossary)

## C

**Deckelung:** Im Entscheidungsdienst wird die Begrenzung verwendet, um festzulegen, wie oft ein Angebot präsentiert wird. Es gibt zwei Arten von Obergrenzen: Wie oft ein Angebot in der kombinierten Audience vorgeschlagen werden kann, auch als &quot;globale Obergrenze&quot;bezeichnet, und wie oft ein Angebot für denselben Endbenutzer vorgeschlagen werden kann, auch als &quot;Profil Cap&quot;bezeichnet.

**Katalog:** In der Echtzeit-Plattform für Kundendaten in Quellen und Zielen ist ein Katalog eine Galerie mit verfügbaren Verbindungen zu Adobe-Anwendungen und Drittanbieter-Technologien.

**Klasse:** Eine Klasse definiert den kleinsten Feldsatz, der zum Erstellen eines Schemas verwendet wird, und ist das Basisverhalten, das das Geschäftsobjekt beschreibt.

**Client:** Ein Client ist ein externes Tool oder eine externe Anwendung, das bzw. die über das Postgres-Protokoll oder die HTTP-API eine Verbindung zum Abfrage Service herstellt.

**Sammlung:** Im Entscheidungsdienst sind Sammlungen Untergruppen von Angeboten, die auf vordefinierten, von einem Marketingspezialisten definierten Bedingungen basieren, z. B. der Kategorie des Angebots.

**Befehlszeilenschnittstelle:** Die Befehlszeilenschnittstelle ist ein Befehlszeilenwerkzeug, mit dem Sie eine Verbindung zum Abfrage-Dienst zur Ausführung von Rohdaten herstellen können.

**Zusammensetzung**: Eine Komposition ist eine Gruppierung von Komponenten, die sich zu dem Schema zusammensetzen.

**Verbindung:** Eine Verbindung ist eine virtuelle Pipeline, die den Datenfluss in und aus der Experience Platform ermöglicht. Verbindungen werden jetzt durch Quellen ersetzt.

**Anschluss:** Adobe Experience Platform Source Connectors unterstützen Benutzer bei der einfachen Erfassung von Daten aus mehreren Quellen und ermöglichen so die Strukturierung, Kennzeichnung und Verbesserung von Daten mithilfe von Experience Platform Services. Daten können aus verschiedenen Quellen wie Cloud-basierte Datenspeicherung, Drittanbieter-Software und CRM-Systeme erfasst werden.

**Bedingung:** Beim Start der Erlebnisplattform ist eine Bedingung eine Regelkomponente, die eine logische Anweisung auswertet, die zurückgegeben `true` oder `false`zurückgegeben werden muss. Alle Bedingungen müssen ausgewertet werden `true` und alle Ausnahmebedingungen müssen ausgewertet werden, `false` bevor Aktionen für die Regel ausgeführt werden.

**Konsole:** Im Abfrage-Dienst stellt die Konsole Informationen zum Status und zum Betrieb einer Abfrage bereit. Die Konsole zeigt den Verbindungsstatus zum Abfrage-Dienst, die ausgeführten Abfragen und alle Fehlermeldungen an, die sich aus diesen Abfragen ergeben.

**Vertragsdaten &quot;C&quot;-Beschriftungen:** Vertragsbezeichnungen `C` werden verwendet, um Daten zu kategorisieren, die vertragliche Verpflichtungen haben oder mit den Datenschutzrichtlinien eines Kunden in Zusammenhang stehen.

**C1 Vertragssiegel:** `C1` Die Beschriftung zur Verwaltung von Vertragsdaten gibt an, dass Daten nur in aggregierter Form aus Adobe Experience Cloud exportiert werden können, ohne dass dabei einzelne IDs oder Gerätekennungen einbezogen werden. Zum Beispiel Daten, die aus sozialen Netzwerken stammen.

**C2 Vertragsbezeichnung:** `C2` Die Beschriftung zur Verwaltung von Vertragsdaten gibt Daten an, die nicht in eine dritte Partei exportiert werden können. Einige Datenanbieter haben in ihren Verträgen Bedingungen, die den Export von Daten, von denen sie ursprünglich erfasst wurden, verbieten.  So wird beispielsweise die Übertragung von Daten, die Sie von sozialen Netzwerken erhalten, oft durch Verträge eingeschränkt. C2 ist restriktiver als C1, was nur Aggregation und anonyme Daten erfordert.

**C3 Vertragssiegel:** `C3` Die Beschriftung zur Verwaltung von Vertragsdaten gibt Daten an, die nicht mit direkt identifizierbaren Informationen kombiniert oder anderweitig verwendet werden können. Einige Datenanbieter haben Vertragsbedingungen, die die Kombination oder Verwendung dieser Daten mit direkt identifizierbaren Informationen verbieten.  Verträge für Daten, die aus Werbenetzwerken, Werbeservern und Drittanbietern von Daten bezogen werden, enthalten beispielsweise oft spezifische vertragliche Verbote für die Verwendung direkt identifizierbarer Daten.

**C4 Vertragssiegel:** `C4` Die Beschriftung zur Verwaltung von Vertragsdaten gibt an, dass Daten nicht für das Targeting von Anzeigen oder Inhalten verwendet werden können, weder auf der Site noch auf der Site. C4 ist die restriktivste Bezeichnung, da sie C5-, C6- und C7-Etiketten umfasst.

**C5-Vertragssiegel:** `C5` Die Beschriftung zur Verwaltung von Vertragsdaten gibt an, dass Daten nicht für interessensbasiertes, Site-übergreifendes Targeting von Inhalten oder Anzeigen verwendet werden können. Interessensbasiertes Targeting oder Personalisierung tritt auf, wenn die folgenden drei Bedingungen erfüllt sind:  Die auf der Site erfassten Daten werden verwendet, um Rückschlüsse auf das Interesse eines Benutzers zu ziehen, in einem anderen Kontext, z. B. auf einer anderen Site oder App, verwendet und um festzulegen, welche Inhalte oder Anzeigen auf der Grundlage dieser Schlussfolgerungen bereitgestellt werden.

**C6 Vertragssiegel:** `C6` Die Beschriftung zur Verwaltung von Vertragsdaten gibt an, dass Daten nicht für das Targeting von Onsite-Anzeigen verwendet werden können. Daten können nicht für das Targeting von Anzeigen auf der Site verwendet werden, einschließlich der Auswahl und des Versands von Anzeigen auf den Websites oder Apps Ihres Unternehmens oder zur Messung des Versands und der Effektivität solcher Anzeigen.  Dazu gehören die Verwendung von zuvor erfassten Onsite-Daten über das Interesse der Benutzer, um Anzeigen auszuwählen, Prozessdaten darüber, wann und wo Werbung angezeigt wurde und ob die Benutzer irgendwelche Aktionen im Zusammenhang mit der Werbung ergriffen haben, z. B. das Klicken auf eine Anzeige oder einen Kauf.

**C7-Vertragsbezeichnung:** `C7` &quot;Contract Data Governance&quot;-Bezeichnung gibt an, dass Daten nicht für das Targeting von Inhalten auf der Site verwendet werden können.  Daten können nicht für das Targeting von Inhalten auf der Site verwendet werden, einschließlich der Auswahl und des Versands von Inhalten auf den Websites oder Apps Ihres Unternehmens oder zur Messung des Versands und der Effektivität solcher Inhalte.  Dazu gehören zuvor erfasste Informationen über das Interesse der Benutzer an der Auswahl von Inhalten, die Verarbeitung von Daten darüber, welche Inhalte angezeigt wurden, wie oft und wie lange sie angezeigt wurden, wann und wo sie angezeigt wurden und ob die Verwendungszwecke irgendwelche Aktionen im Zusammenhang mit dem Inhalt durchgeführt haben, z. B. das Klicken auf Inhalte.

**C8 Vertragssiegel:** `C8` &quot;Contract Data Governance&quot;-Bezeichnung gibt an, dass Daten nicht zur Messung der Websites oder Apps Ihres Unternehmens verwendet werden können. Daten können nicht verwendet werden, um die Nutzung der Sites oder Apps Ihres Unternehmens durch Benutzer zu messen, zu verstehen und Berichte darüber zu erstellen. Dies umfasst nicht das interessensbasierte Targeting, d. h. die Erfassung von Informationen über Ihre Nutzung dieses Dienstes zur späteren Personalisierung von Inhalten und/oder Werbung in anderen Kontexten.

**C9-Vertragssiegel:** `C9` &quot;Contract Data Governance&quot;-Etikett gibt an, dass Daten in Data Science-Workflows nicht verwendet werden können. Einige Verträge beinhalten explizite Verbote von Daten, die für die Datenwissenschaft verwendet werden.  Manchmal werden diese Begriffe in Begriffen ausgedrückt, die die Verwendung von Daten für künstliche Intelligenz (KI), maschinelles Lernen (ML) oder Modellierung verbieten.

**Spalte &quot;Erstellungsdatum&quot;:** Die Auswahl einer `Created Date` Spalte ist eine Option, wenn Daten von Drittanbietern über eine Verbindung angegeben werden. Wenn die Speicherstrategie zum Anhängen ausgewählt ist und der Datensatz ein Schema mit mehreren Daten enthält, muss der Benutzer aus dem verfügbaren Datums-/Uhrzeitfeld wählen, um eine `Created Date` Schlüsselspalte anzugeben. `Created Date` nicht verfügbar ist, wenn die Speicherstrategie überschreiben ausgewählt ist.

**Tabelle als Auswahl erstellen:** &quot;Tabelle als Auswahl erstellen&quot;ist ein SQL-Befehl, der, wenn er als Teil einer vollständigen und gültigen SQL-Abfrage ausgeführt wird, den Abfrage Service anweist, die Ergebnisse der Abfrage in einem Datensatz auf dem Data Lake beizubehalten. Zu den Optionen gehören: Neu erstellen, Alle vorherigen überschreiben und An Vorherige anhängen.

**Site-übergreifende Daten:** Site-übergreifende Daten sind die Kombination von Daten aus verschiedenen Sites, einschließlich einer Kombination aus Vor-Ort- und Offsite-Daten oder einer Kombination von Daten aus verschiedenen Offsite-Quellen.

**Benutzerdefinierter Identitäts-Namensraum:** Benutzerdefinierte Identitätskennungen sind vom Namensraum erstellte IDs, die zur Darstellung von Identitäten für ein bestimmtes Unternehmen oder eine bestimmte Geschäftsbeziehung verwendet werden.

**Kunden-AI:** Customer AI ist ein Adobe Sensei Service, der Profil mit AI-basierten Eigenschaften bereichert und die Segmentierung und das Targeting von Kunden stärkt.

[Zurück zum Anfang](#adobe-experience-platform-glossary)

## D

**Datenwörterbuch:** Bei Experience Platform Launch ist ein Datenwörterbuch ein Satz von Datenelementen, die innerhalb einer Eigenschaft definiert werden.

**Datenelement:** Beim Start der Experience Platform ist ein Datenelement ein Zeiger, der in Regeln und Erweiterungen verwendet wird, um auf ein bestimmtes Datenelement zu verweisen, das auf dem Client-Gerät vorhanden ist.

**Datenschicht:** Beim Start der Experience Platform handelt es sich bei einer Datenschicht um eine Datenstruktur, die auf dem Client-Gerät vorhanden ist und Metadaten zum Kontext enthält, in dem eine Seite oder ein Bildschirm angezeigt wird.

**Datenzuordnung:** Bei der Datenzuordnung werden Quelldatenfelder zielbezogenen Zielgruppen zugeordnet.

**Datenstream:** Ein Datenstrom ist ein Satz oder eine Sammlung von Nachrichten, die dasselbe Schema teilen und von derselben Quelle gesendet werden.

**Datenverwaltung:** Die Datenverwaltung umfasst die Strategien und Technologien, mit denen sichergestellt werden soll, dass die Daten im Einklang mit Vorschriften und organisatorischen Richtlinien zur Datenverwendung stehen.

**Bezeichnungen für Datenverwaltung:** Datenverwaltungs-Etiketten bieten Benutzern die Möglichkeit, Daten zu klassifizieren, die datenschutzbezogene Erwägungen und Vertragsbedingungen widerspiegeln, damit sie mit Vorschriften und Unternehmensrichtlinien in Einklang stehen. Zu einem Datensatz hinzugefügte Datenverwaltungs-Beschriftungen werden vererbt oder auf alle Felder in diesem Datensatz angewendet.  Datenverwaltungs-Beschriftungen können auch direkt auf Felder angewendet werden.

**Data Integration Partner:** Data-Integrationspartner vereinfachen und automatisieren das Laden und Umwandeln massiver Datenmengen von über 200 Quellen in Experience Platform, ohne Code zu schreiben.

**Datensatzbeschriftungen:** Datennutzungsbeschriftungen können zu Datasets hinzugefügt werden. Alle Felder in diesem Datensatz übernehmen die Beschriftungen des Datensatzes.

**Data Science Workspace** Mit Data Science Workspace innerhalb der Experience Platform können Kunden Modelle für maschinelles Lernen erstellen, die Daten über Experience Platform- und Adobe-Anwendungen hinweg nutzen, um intelligente Einblicke und Prognosen zu generieren, um ansprechende digitale Erfahrungen für Endbenutzer zu entwickeln.

**Datenquelle:** Eine Datenquelle ist eine vom Benutzer festgelegte Herkunft von Daten. Beispiele für eine Datenquelle sind mobile App, Profil- und/oder Erlebnis-Ereignis, Website-Profil-Ereignis oder CRM.

**Datenverlauf:** Ein Datenverwalter ist die Person, die für die Verwaltung, Überwachung und Durchsetzung der Datenbestände einer Organisation verantwortlich ist. Ein Datenmanager stellt außerdem sicher, dass die Datenschutzrichtlinien geschützt und so aufrechterhalten werden, dass sie mit den Regierungs- und Organisationspolitiken im Einklang stehen.

**Datentyp:** Der Datentyp ist ein wiederverwendbares Objekt mit Eigenschaften in einer hierarchischen Darstellung.

**Beschriftungen für die Datenverwendung:** Datenverwendungsbeschriftungen bieten Benutzern die Möglichkeit, Daten zu kategorisieren, die datenschutzbezogene Erwägungen und Vertragsbedingungen widerspiegeln, damit sie mit Vorschriften und Unternehmensrichtlinien übereinstimmen.

**Datenflug:** In der Echtzeit-Kundendatenplattform ist ein Datenflug eine virtuelle Datenpipeline, die von einer Quelle bis zu Zielen in die Plattform fließt.

**Datensatz:** Ein Datensatz ist ein Datenspeicherung- und Verwaltungskonstrukt für eine Datenerfassung, normalerweise eine Tabelle, die Schema (Spalten) und Felder (Zeilen) enthält.

**Datenbestand-ID:** Eine von Adobe generierte ID für einen erfassten Datensatz.

**Datensatzausgabe:** Die Datensatzausgabe bietet einen Mechanismus, mit dem bestimmt wird, welche Option &quot;Tabelle als Auswahl *erstellen* &quot;für eine bestimmte Ausführung des Abfrage-Dienstes verwendet wird.

**Ereignis der Entscheidung:** Ein Ereignis dient der Erfassung von Bemerkungen zum Ergebnis und zum Kontext einer Aktivität. Das Ereignis &quot;Decision&quot;erfasst Informationen darüber, wie die Entscheidung erfolgte, wann sie erfolgte, welche Optionen vorgeschlagen (gewählt) wurden und welcher kontextuelle Zustand existierte, der die Entscheidung beeinflusste oder während des Entscheidungsprozesses beobachtet werden konnte. Das Ereignis &quot;Decision&quot;erfasst auch die Proposition-ID, eine weltweit eindeutige Kennung, mit der die Entscheidung mit anderen Ereignissen korreliert werden kann.

**Entscheidungsregel:** Im Entscheidungsdienst ist eine Entscheidungsregel die Logik, die definiert und steuert, was, wann, wo und wie ein Angebot Endbenutzern präsentiert wird.

**Entscheidungsdienst:** Der Entscheidungsdienst umfasst eine Reihe von Diensten und Benutzeroberflächen, mit denen Marketingexperten personalisierte Angebot-Erlebnisse für Endbenutzer erstellen und bereitstellen können, und zwar über Kanal und Anwendungen, die Geschäftslogik und Entscheidungsregeln nutzen.

**Delta-Spalte:** In der Echtzeit-Kundendatenplattform aktiviert die Delta-Spalte die Auswahl des Quelldatenfelds für einen Zeitstempel zur inkrementellen Erfassung

**Delta-Speicherstrategie:** `Delta save strategy` ist eine Option zum Erfassen von Drittanbieterdaten über eine Verbindung. Mit dieser Option kann der Benutzer festlegen, dass neue oder geänderte Zeilen mit Quelldaten in Experience Platform aufgenommen werden. Neue Zeilen werden am Ende des Datensatzes hinzugefügt und geänderte Zeilen werden im Datensatz auf Experience Platform aktualisiert.

**Ziel:** In der Echtzeit-Kundendatenplattform ist ein Ziel ein allgemeiner Begriff für jedes System, z. B. eine Adobe-Anwendung, ein Werbeserver oder ein Werbenetzwerk, in dem eine Audience aktiviert und bereitgestellt wird.

**Ziel-Kategorie:** Eine Ziel-Kategorie ist eine Gruppierung von Zielen der Echtzeit-Kundendatenplattform, die ähnliche Merkmale aufweisen.

**Zielkatalog:** Ein Zielkatalog ist eine Liste der verfügbaren Ziele in der Echtzeit-Kundendatenplattform.

**Anzeigename:** Der Anzeigename ist ein benutzerfreundlicher Name eines Felds, der in der Benutzeroberfläche angezeigt wird.

**DULE:** DULE ist ein Akronym für die *Datenverwendung, die Kennzeichnung und Durchsetzung*. DULE ist ein wichtiger Bestandteil der Datenverwaltung und eine Sammlung von Schlüsselfunktionen, die eine Datenverwendungskennzeichnung und die Anwendung von Datenzugriffsrichtlinien für Governance-Anforderungen in einem Unternehmen ermöglichen.

[Zurück zum Anfang](#adobe-experience-platform-glossary)

## E

**Fehlerdiagnose:** Die Fehlerdiagnose ermöglicht die Generierung detaillierter Fehlermeldungen für erfasste Stapel. Der Fehlerschwellenwert ermöglicht die Konfiguration des Prozentsatzes der zulässigen Fehler, bevor der gesamte Stapel fehlschlägt.

**Förderfähiges Angebot:** Im Entscheidungsdienst erfüllt ein förderfähiges Angebot die im Upstream definierten Einschränkungen, die einem Profil konsistent angeboten werden können.

**Förderfähige Regeln:** Im Entscheidungsdienst werden Eignungsregeln auf ein Profil im Zusammenhang mit Kalender-, Zeitplan- und Deckelungsbeschränkungen angewendet.

**Einbettungscode:** Beim Start der Experience Platform handelt es sich bei dem Einbettungscode um ein Skript-Tag, das auf einer Site oder Umgebung in den HTML-Code eingefügt wird. Der Einbettungscode weist den Browser an, wo der Build abgerufen werden soll.

**Auflistung:** Ein Enum ist eine Liste von Werten, die die gültigen Daten für ein Feld darstellen.

**Umgebung:** Beim Start der Experience Platform handelt es sich bei einer Umgebung um einen Satz von Bereitstellungsanweisungen, die den Host-Versand und das Dateiformat eines Builds angeben. Eine Bibliothek muss mit einer Umgebung gepaart werden, bevor sie erstellt werden kann.

**Ereignis** Beim Start der Erlebnisplattform ist ein Ereignis ein bestimmter Regeltyp, ein Auslöser, der auf einem Client-Gerät auftritt, um die Ausführung einer Regel zu beginnen.

**Ereignisse:** Ereignis sind die mit einem Profil verknüpften Verhaltensdaten.

**Erlebnisdatenmodell (XDM):** Erlebnis-Datenmodell (XDM) ist das Konzept der Verwendung von Standard-Schemas zur Vereinheitlichung von Daten für die Verwendung mit Experience Platform- und Adobe Experience Cloud-Anwendungen. XDM standardisiert die Strukturierung von Daten und beschleunigt und vereinfacht den Prozess der Gewinnung von Erkenntnissen aus enormen Datenmengen.

**Erlebnisplattform-Start:** Launch ist ein Tag- und SDK-Management-Ökosystem, das in Experience Platform- und Experience Cloud-Anwendungen integriert ist. Launch bietet Tools zur Bereitstellung, Vereinheitlichung und Verwaltung von Analyse-, Marketing- und Werbeintegrationen, die erforderlich sind, um relevante Kundenerlebnisse auf allen Client-Geräten zu ermöglichen.

**Erlebnis-Plattform-Starterweiterungen:** Mit Experience Platform Launch-Erweiterungen können Rohdaten aus Ereignissen direkt an Zielorte der Echtzeit-Datenplattform des Kunden Versand werden. Für die Installation von Starterweiterungen ist der Zugriff auf die Eigenschaften von &quot;Start&quot;erforderlich.

**Experiment:** Bei einem Experiment wird ein trainiertes Modell erstellt, indem die Instanz mit einem Beispielteil der Live-Produktionsdaten trainiert wird.

**Experimente:** Experimente sind der Prozess, bei dem ein trainiertes Modell auf einen kleinen Teil der Live-Produktionsdaten angewendet wird, um seine Leistung zu überprüfen. Dies unterscheidet sich von einem trainierten Modell, das mit einem Holdout-Testdatensatz getestet wird. Dies unterscheidet sich auch vom Konzept eines Experiments in einigen ML-Frameworks, bei dem es sich tatsächlich um ein Beispielmodellierungsprojekt handelt.

**ExperienceEvent:** ExperienceEvent ist ein Standard-Schema der Experience Platform, das Beobachtungen einschließlich des Zeitpunkts und der Identität des jeweiligen Objekts erfasst. Experience Ereignisses sind Faktenaufzeichnungen dessen, was passiert ist, und die das darstellen, was ohne Aggregation oder Interpretation passiert ist.

**Erweiterung:** Bei Experience Platform Launch ist eine Erweiterung ein Funktionspaket, das einer Launch-Eigenschaft hinzugefügt wird.  Eine Erweiterung konzentriert sich in der Regel auf eine bestimmte Marketing- oder Analyselösung und stellt die Werkzeuge bereit, die zur Bereitstellung dieser Technologie in einer Client-Umgebung erforderlich sind.

**Erweiterungspaket:** Bei Experience Platform Launch handelt es sich bei einem Erweiterungspaket um eine ZIP-Datei, die von einem Entwickler der Erweiterung erstellt und hochgeladen wurde und die alle erforderlichen Informationen enthält, damit Launch-Benutzer die Erweiterung in ihrer Eigenschaft installieren können.  Ein Erweiterungspaket enthält ein Manifest, das Informationen über die Erweiterung, HTML und JavaScript angibt, die Endbenutzer zum Konfigurieren des Verhaltens der Launch-Erweiterung und der ausführbaren JavaScript-Datei, die an die Client-Umgebung geliefert wird, benötigen, falls erforderlich.

[Zurück zum Anfang](#adobe-experience-platform-glossary)

## F

**Fallback-Angebot:** Im Entscheidungsdienst ist ein Ausweichmanöver-Angebot das standardmäßige Angebot, das angezeigt wird, wenn ein Endbenutzer für keines der Angebot in der verwendeten Sammlung berechtigt ist.

**Funktionszuordnung:** &quot;Funktionszuordnung&quot;bezeichnet den Vorgang der Zuordnung von Funktionen aus Daten zu Eingabe- und Zielgruppe-Funktionen, die für ein maschinelles Lernmodell erforderlich sind.

**Feld:** Ein Feld ist das Element der untersten Ebene eines Datensatzes. Jedes Feld hat einen Namen zum Referenzieren und einen Typ zum Identifizieren des darin enthaltenen Datentyps. Zu den Feldtypen können &quot;integer&quot;, &quot;number&quot;, &quot;string&quot;, &quot;Boolean&quot;und &quot;Schema&quot;gehören.

**Feldbezeichnungen:** Feldbezeichnungen sind Bezeichnungen zur Datenverwaltung, die entweder von einem Datensatz übernommen oder direkt auf ein Feld angewendet werden.

**Feldname:** &quot;Feld&quot;ist ein Name, der auf das Feld in Abfragen und Diensten verweist.

**Häufigkeit:** Die Häufigkeit legt fest, wie oft eine wiederkehrende geplante Abfrage-Dienst-Abfrage ausgeführt wird.

[Zurück zum Anfang](#adobe-experience-platform-glossary)

## G

**Quelle:** Eine Geofence ist eine virtuelle geografische Grenze, die durch GPS- oder RFID-Technologie definiert wird und die Software in die Lage versetzt, eine Antwort auszulösen, wenn ein Mobilgerät ein bestimmtes Gebiet betritt oder verlässt.

**GDPR:** Die Allgemeine Datenschutzverordnung (GDPR) ist ein Rechtsrahmen, der Leitlinien für die Erhebung und Verarbeitung personenbezogener Daten innerhalb der Europäischen Vereinigung (EU) festlegt. Der GDPR legt die Grundsätze für das Data Management und die Rechte des Einzelnen fest und deckt alle Firmen ab, die sich mit den Daten der Unionsbürger befassen.

**GDPR-Datenbeschriftung:** Das GDPR-Governance-Etikett dient zur Definition der Felder, die persönliche IDs für den Zugriff auf GDPR und/oder das Löschen von Anforderungen enthalten können.

[Zurück zum Anfang](#adobe-experience-platform-glossary)

## H

**Host:** In Experience Platform Launch gibt ein Host den Speicherort, die Domäne und die Benutzerberechtigungen an, die erforderlich sind, damit Launch einen Build bereitstellt.

[Zurück zum Anfang](#adobe-experience-platform-glossary)

## I

**Identität:** Identity ist ein Bezeichner wie eine Cookie-ID, Geräte-ID oder E-Mail-ID, die einen Endkunden eindeutig repräsentiert.

**Identitäts-&quot;I&quot;-Datenbezeichnungen:** `Identity I` werden zur Kategorisierung von Daten verwendet, die eine bestimmte Person identifizieren oder kontaktieren können.

**Identitätsdiagramm:** Das Identitätsdiagramm ist eine Zusammenstellung der Beziehungen zwischen verbundenen und gehefteten Identitäten, die mit der Aktivität von Kunden nahezu in Echtzeit aktualisiert wird.

**Identitäts-Namensraum:** Ein Identitäts-Namensraum ist ein Bezeichner wie Cookie-ID, Geräte-ID oder E-Mail-ID, der den Kontext angibt, aus dem Daten stammen und zur Erkennung und Verknüpfung von Identitäten in der Experience Cloud verwendet werden.

**Identitätsdienst:** Die Benutzeroberfläche des Experience Platform-Identitätsdienstes ermöglicht die Erstellung und Verwaltung von Identitätstypen, um die Verknüpfung von Identitäten zwischen Geräten und Kanälen zu ermöglichen und eine vollständige Ansicht des Kunden-Profils in Echtzeit zu ermöglichen.

**Identitätsfixierung:** Identitätszuordnung ist der Prozess der Identifizierung von Datenfragmenten und deren Zusammenführung, um einen vollständigen Datensatz eines Profils zu bilden.

**Identitätssymbol:** Identitätssymbol ist eine Abkürzung eines Identitäts-Namensraums, der als Referenz in APIs verwendet werden kann.

**Identitätswert:** Identitätswert sind Daten, die mit einer zugeordneten Identität im Schema verknüpft sind. Bei der Zuordnung von Datensatzdaten zu Profil-Fragmenten müssen sowohl der Identitätswert als auch der Namensraum übereinstimmen.

**I1-Datenbeschriftung:** Die `I1` Datenbeschriftung dient zur Klassifizierung direkt identifizierbarer Daten, die eine bestimmte Person anstatt eines Geräts identifizieren oder kontaktieren können.

**I2 Datenbeschriftung:** Die `I2` Datenbeschriftung dient zur Klassifizierung indirekt identifizierbarer Daten, die in Verbindung mit anderen Daten zur Identifizierung oder zum Kontakt mit einer bestimmten Person verwendet werden können.

**Zusammenfassung:** Bei der Integration werden Daten aus einer Quelle zur Experience Platform hinzugefügt. Daten können auf verschiedene Weise in die Experience Platform aufgenommen werden, z. B. über Streaming, Batch oder Connector.

**Einstiegsplan:** Der Einstiegsplan bietet zeitbasierte Optionen, wenn Sie von einer Quelle zu einer Erlebnisplattform wechseln.

**Eingabefunktion:** Die Eingabefunktion ist in der Funktionszuordnung angegeben und wird von einem maschinellen Lernmodell verwendet, um Vorhersagen zu treffen.

**Intelligente Dienste:** Intelligente Dienste wie Attribution.ai und Customer.ai sind maschinelles Lernen, bedarfsbasierte Modelle mit künstlicher Intelligenz, für die die Experience Platform ausgeführt und betrieben werden muss.

**Interessensbasiertes Targeting oder Personalisierung:** Interessensbasiertes Targeting, auch Personalisierung genannt, tritt auf, wenn die folgenden drei Bedingungen erfüllt sind: Daten, die vor Ort gesammelt werden, werden verwendet, um Rückschlüsse auf das Interesse eines Benutzers zu ziehen, Daten werden in einem anderen Kontext verwendet, z. B. auf einer anderen Site oder App (außerhalb der Site), und wenn Daten verwendet werden, um auszuwählen, welche Inhalte oder Anzeigen auf der Grundlage dieser Schlussfolgerungen bereitgestellt werden.

[Zurück zum Anfang](#adobe-experience-platform-glossary)

## J

**JupyterLab:** Eine Open-Source-webbasierte Schnittstelle für Project Jupyter und ist eng in Experience Platform integriert.

**Jupyter-Notebook:** Eine Open-Source-Webanwendung, mit der Benutzer Dokumente erstellen und freigeben können, die Live-Code, Gleichungen, Visualisierungen und Erzählungstext enthalten.

## K

[Zurück zum Anfang](#adobe-experience-platform-glossary)

## L

**Bibliothek:** In Experience Platform Launch ist eine Bibliothek ein Satz von Geschäftslogik, die Anweisungen enthält, wie sich die Launch-Bibliothek auf dem Client-Gerät verhalten sollte.

[Zurück zum Anfang](#adobe-experience-platform-glossary)

## M

**Maschinelles Lernen (ML):** Maschinelles Lernen ist der Studienbereich, der es Computern ermöglicht, zu lernen, ohne explizit programmiert zu werden.

**Modell für maschinelles Lernen:** Ein maschinelles Lernmodell ist ein Beispiel für ein maschinelles Lernrezept, das mithilfe historischer Daten und Konfigurationen für die Lösung eines Geschäftsfalls trainiert wird. In Adobe Data Science Workspace werden Modelle für maschinelles Lernen als Rezepte bezeichnet.

**Zuordnung:** In der Echtzeit-Kundendatenplattform wird bei der Datenzuordnung die Zuordnung von Quelldatenfeldern zu zielbezogenen Zielgruppen durchgeführt.

**Marketingaktion:** Eine Marketingaktion im Kontext des Data Governance-Rahmens ist eine Aktion, die ein Datenerfassungsbenutzer von Experience Platform durchführt und bei der überprüft werden muss, ob die Datenverwendungsrichtlinien verletzt wurden.

**Zusammenführungsmethode:** Eine `merge method` Option der Richtlinie zum Zusammenführen ermöglicht die Priorisierung der Zusammenführung von Datenfragmenten. Die Optionen für die Zusammenführungsmethode werden nach der Priorität des Datensatzes oder nach dem Zeitstempel des Datensatzes zusammengeführt.

**Richtlinie zusammenführen:** Eine Zusammenführungsrichtlinie ist ein Satz von Regeln, die von Profil verwendet werden, um zu bestimmen, wie Daten priorisiert und unter bestimmten Bedingungen zu einer einheitlichen Ansicht kombiniert werden.

**Mixin:** Mit einem Mixin können Benutzer wiederverwendbare Felder mit Variablen erweitern, die ein oder mehrere Attribute definieren, die in ein Schema eingeschlossen oder einer Klasse hinzugefügt werden sollen.

**Spalte &quot;Geändertes Datum&quot;:** Die Auswahl einer `Modified Date` Spalte ist eine Option, wenn Daten von Drittanbietern über eine Verbindung angegeben werden. Wenn die `Delta` Speicherstrategie ausgewählt ist und der Datensatz mehrere datumsbezogene Schema enthält, muss der Benutzer aus dem verfügbaren Datums-/Uhrzeittyp-Schema wählen, um die Spalte mit dem geänderten Datumsschlüssel anzugeben. `Modified Date` nicht verfügbar ist, wenn die `Overwrite` Speicherstrategie ausgewählt ist.

**Modul:** Bei Experience Platform Launch handelt es sich bei einem Modul um einen Snippet ausführbaren JavaScript, das von einer Erweiterung bereitgestellt wird, die Aktionen in einer Client-Umgebung ausführt, ohne dass der Launch-Benutzer eine Regel erstellen muss.

[Zurück zum Anfang](#adobe-experience-platform-glossary)

## N

**Sandbox ohne Produktion:** Nicht-Produktions-Sandboxes sind eine Form der Datenvirtualisierung, mit der Sie Daten von anderen Sandboxen isolieren können und die üblicherweise für Entwicklungsversuche, Tests oder Tests verwendet werden. Nicht-Produktions-Sandboxen können zurückgesetzt und gelöscht werden.

**Notebooks:** Notebooks werden mit *Jupyter-Notebook* erstellt und enthalten Beschreibungen der Analyse, Ergebnisse und können zur Analyse von Daten ausgeführt werden.

[Zurück zum Anfang](#adobe-experience-platform-glossary)

## O

**Angebot:** Im Entscheidungsdienst ist ein Angebot eine Marketingmeldung, der möglicherweise Regeln zugeordnet sind, die angeben, wer zum Anzeigen des Angebots berechtigt ist.

**Angebot-Entscheidungsfindung:** Im Entscheidungsdienst ermöglicht die Angebot-Entscheidungsfindung einem Marketingspezialisten die Verwaltung der Regeln und geschulten Modelle von Angebotsvorschlägen, wenn er mit einem Endbenutzer auf der Grundlage von Daten interagiert, die über Kanal und Anwendungen hinweg gesammelt wurden.

**Angebot-Bibliothek:** Im Entscheidungsdienst ist die Angebot-Bibliothek eine zentrale Bibliothek, die zum Verwalten personalisierter und Ausweichfunktionen, von Entscheidungsregeln und Aktivitäten verwendet wird.

**Einrichtung:** Eine Organisation ist der Name, der zur Identifizierung einer Firma oder einer bestimmten Gruppe innerhalb einer Firma in allen Adobe-Produkten verwendet wird. Administratoren können den Zugriff und die Berechtigungen von Funktionen für Benutzer einer Organisation konfigurieren und verwalten.

**Speicherstrategie überschreiben:** `Overwrite` Speicherstrategie ist eine Option zum Erfassen von Daten von Drittanbietern über eine Verbindung, bei der der Benutzer angibt, ob die erfassten Daten nach einem bestimmten Zeitplan überschrieben werden. Experience Platform erfasst den angegebenen Datensatz aus der Drittanbieter-Quelle und überschreibt den Datensatz auf Experience Platform.

[Zurück zum Anfang](#adobe-experience-platform-glossary)

## P

**Partielle Aufnahme:** Die teilweise Erfassung ermöglicht die Erfassung gültiger Datensätze von Stapeldaten innerhalb eines festgelegten Fehlerschwellenwerts. Die Fehlerdiagnose für fehlgeschlagene Datensätze kann unter Überwachung heruntergeladen oder aufgerufen werden.

**Parkettdateien:** Bei einer Parkettdatei handelt es sich um ein Spaltenformat mit Datenspeicherung und komplexen verschachtelten Datenstrukturen. Zum Hinzufügen von Daten zum Ausfüllen eines Schema-Datensatzes sind Parkettdateien erforderlich.

**Personalisierte Angebot:** Im Entscheidungsdienst ist ein personalisiertes Angebot eine benutzerspezifische Marketingbotschaft, die auf Eignungsregeln und Einschränkungen basiert.

**Praktika:** Im Entscheidungsdienst ist eine Platzierung der Ort und der Kontext, in dem ein Angebot für einen Endbenutzer angezeigt wird.

**Richtlinie:** Eine Datenverwendungsrichtlinie ist eine Regel, die Marketingaktionen angibt, die auf der Grundlage der Anwendung von Datenverwendungsbeschriftungen auf Daten in Experience Platform eingeschränkt sind.

**Primärschlüssel:** Primärschlüssel ist eine Bezeichnung in einem Schema zur eindeutigen Identifizierung aller Datensätze.

**Priorität:** Im Entscheidungsdienst wird die Priorität verwendet, um Angebot zu sortieren, die alle Einschränkungen erfüllen, wie z. B. Förderfähigkeit, Kalender und Deckelung.

**Diagramm zur privaten Identität:** Private Identitätsdiagramm ist eine private Zuordnung von Beziehungen zwischen verbundenen und verknüpften Identitäten, die nur von Ihrer Organisation sichtbar sind und auf Ihren Erstanbieterdaten basieren.

**Produkt-Profil:** Mithilfe von Produkt-Profilen können Administratoren allen oder einer Untergruppe von Diensten, die mit Experience Platform verknüpft sind, Benutzerzugriff gewähren.

**Produktions-Sandbox:** Eine Produktions-Sandbox zur Isolierung virtueller Daten auf der Plattform, die nicht zurückgesetzt oder gelöscht werden können.

**Profil:** Profil ist ein Experience Platform-Standarddatenmodell, mit dem Verbraucherattribute definiert werden. Ein Profil kann auch ein Aggregat von Ereignisdaten und -attributen sein, das sich auf eine Person oder ein Gerät bezieht.

**Profil-Export:** Der Export von Profilen ist einer der beiden Zieltypen in der Echtzeit-Kundendatenplattform. Beim Profil-Export wird eine Datei mit Profilen und Attributen erstellt, PII-Rohdaten mit E-Mail verwendet und in Marketing- und E-Mail-Automatisierungsplattformen integriert.

**Profil FProfile Fragment:** Ein Profil-Fragment ist das Profil für nur eine Identität aus der Liste der Identitäten, die für einen bestimmten Benutzer vorhanden sind.

**Profil-ID:** Eine Profil-ID ist eine automatisch generierte ID, die einem Identitätstyp zugeordnet ist und ein Profil darstellt.

**Eigenschaft:** In Experience Platform Launch ist eine Eigenschaft ein Container für alles, was zum Bereitstellen eines Satzes von Tags erforderlich ist.

[Zurück zum Anfang](#adobe-experience-platform-glossary)

## Q

**Abfragen:** Eine Abfrage ist eine Anforderung von Daten aus Datenbanktabellen.

**Abfragen-Editor:** Abfrage Editor ist ein Tool zum Schreiben, Prüfen und Senden von SQL-Anweisungen im Abfrage Service.

**Abfrage Service for Adobe Experience Platform:** *Der Experience Platform Abfrage Service* ermöglicht Datenanalysten die Verwendung von Abfrage ExperienceEvents und XDMs für die Analyse und das maschinelle Lernen. Mit dem Abfrage Service können Datenwissenschaftler und Analysten alle in Experience Platform gespeicherten Datensätze abrufen - einschließlich Verhaltensdaten sowie POS (Point-of-Sale), CRM (Customer Relationship Management) und mehr - und diese Datensätze zur Beantwortung spezifischer Fragen zu den Daten Abfrage.

[Zurück zum Anfang](#adobe-experience-platform-glossary)

## R

**Echtzeit-Kundendatenplattform:** Die Echtzeit-Kundendatenplattform von Adobe vereint bekannte und unbekannte Kundendaten, um vertrauenswürdige Profil mit vereinfachter Integration, intelligenter Segmentierung und Echtzeit-Aktivierung während der gesamten Customer Journey zu erstellen.

**Echtzeit-Profil des Kunden:** Echtzeit-Customer-Profil ist ein zentralisiertes Profil für zielgerichtetes und personalisiertes Erlebnis-Management.

**Rezept:** Ein Rezept ist der von Adobe verwendete Begriff für eine Modellspezifikation. Es handelt sich dabei um einen Container auf oberster Ebene, der ein bestimmtes maschinelles Lernen, einen AI-Algorithmus oder ein Ensemble von Algorithmen, eine Verarbeitungslogik und eine Konfiguration darstellt, die erforderlich sind, um ein geschultes Modell zu erstellen und auszuführen und damit zur Lösung spezifischer Geschäftsprobleme beizutragen.

**Datensatz:** Ein Datensatz sind Daten, die als Zeilen in einem Datensatz beibehalten werden.

**Wiederholung:** Eine Wiederholung definiert, ob eine Abfrage Service-Abfrage nur einmal oder wiederholt ausgeführt werden soll.

**Vertretung:** Im Entscheidungsdienst ist eine Darstellung die von einem Kanal verwendeten Informationen, z. B. Ort oder Sprache zur Anzeige eines Angebots.

**Ressource:** Beim Start der Experience Platform ist resource ein allgemeiner Begriff, der auf Optionen verweist, die der Startbenutzer innerhalb der Client-Umgebung konfigurieren kann, einschließlich Erweiterungen, Datenelemente und Regeln.

**Rollenbasierte Zugriffskontrolle:** Rollenbasierte Zugriffskontrolle ermöglicht Administratoren die Zuweisung von Zugriff und Berechtigungen an Benutzer von Experience Platform. Zu den Berechtigungen gehören die Möglichkeit zur Ansicht und/oder Verwendung von Experience Platform-Funktionen wie das Erstellen von Sandboxen, das Definieren von Schemas und das Verwalten von Datensätzen.

**Regel:** Beim Start der Erlebnisplattform handelt es sich bei einer Regel um eine Sammlung von Regelkomponenten, die einen bestimmten Satz von Ereignissen, Bedingungen und Aktionen definieren, die logisch gruppiert werden sollen.

**Regelkomponente:** Beim Start der Erlebnisplattform sind Regelkomponenten die Ereignis, Bedingungen und Aktionen, aus denen eine Regel besteht.

**Laufzeit:** Laufzeitumgebung gibt eine Laufzeitumgebung für ein maschinelles Lernrezept an. Spark- und PySpark-Laufzeitumgebungen ermöglichen das direkte Hochladen einer binären Rezeptquellendatei (.jar). Python-, R- und Tensorflow-Laufzeitumgebungen ermöglichen die Eingabe einer URL in ein Dockerbild für eine Rezept-Quelle.

[Zurück zum Anfang](#adobe-experience-platform-glossary)

## S

**Beispieldaten:** Musterdaten sind eine Vorschau einer Datendatei, in der Regel die ersten 100 Zeilen, um einem Datenwissenschaftler oder -ingenieur eine Vorstellung davon zu vermitteln, welches Schema oder welche Daten in der Datendatei enthalten sind.

**Sandbox:** Eine Sandbox ist eine Form der Isolierung virtueller Daten innerhalb eines Benutzerorgs auf Experience Platform.

**Sandbox-Reset:** Sandbox-Zurücksetzung löscht alle Daten, einschließlich Daten, Profilen und Segmenten innerhalb einer Sandbox. Das Zurücksetzen der Sandbox könnte sich auf Daten auswirken, die mit internen oder externen Zielen verbunden sind.

**Sandbox-Switcher:** Mit dem Sandbox-Umschalter in Experience Platform können Benutzer zwischen Sandboxen navigieren, auf die sie Zugriff haben. Durch das Umschalten einer Sandbox werden alle Inhalte geändert und der Funktionszugriff kann je nach Berechtigungen geändert werden.

**Plan:** Plan ist eine benutzerdefinierte Spezifikation zur Häufigkeit oder Häufigkeit der Datenerfassung von einer Datenquelle eines Drittanbieters zu Adobe Experience Platform.

**Bewertung:** Die Auswertung ist der Prozess, bei dem mithilfe eines geschulten Modells Erkenntnisse aus Daten generiert werden.

**Schema:** Schema besteht aus einer Klasse und einem optionalen Mixin und wird zum Erstellen von Datensätzen und Datenströmen verwendet. Ein Schema umfasst Verhaltensattribute, Zeitstempel, Identitäten, Attributdefinitionen und Beziehungen.

**Schema-Deskriptor:** Schema-Deskriptor sind zusätzliche Metadaten zum Schema, die Verhaltensweisen beschreiben, die von Experience Platform verwendet werden können, um das beabsichtigte Verhalten von Schemas zu verstehen, z. B. die Beziehung zwischen zwei Schemas.

**Schlüssel für geheimen Zugriff:** Ein geheimer Zugriffsschlüssel ist ein Amazon S3-Schlüssel, der zusammen mit der Zugriffsschlüssel-ID zum Signieren von AWS-Anforderungen verwendet wird.

**Segment:** Ein Segment ist ein Regelsatz, der Attribute und Ereignis-Daten enthält, die eine Reihe von Profilen zu einer Audience machen.

**Segmentaufbau:** Der Segmentaufbau ist die visuelle Umgebung zur Entwicklung von Segmentdefinitionen und dient als gemeinsame Komponente aller Anwendungen unter Verwendung der Segmentierung von Kundendaten in Echtzeit auf Experience Platform.

**Segmentdefinition:** Die Segmentdefinition ist der Regelsatz, der zur Beschreibung der Hauptmerkmale oder des Verhaltens einer Zielgruppe-Audience verwendet wird. Nach der Konzeption werden die in einer Segmentdefinition beschriebenen Regeln verwendet, um qualifizierte Segmentmitglieder für eine Audience zu bestimmen.

**Methode zur Segmentbewertung:** Die geplante Segmentauswertung ermöglicht einen regelmäßigen Zeitplan für die Ausführung eines Exportauftrags zu einem bestimmten Zeitpunkt, während die On-Demand-Auswertung die Erstellung eines Segmentauftrags zur sofortigen Erstellung der Audience umfasst.

**Segmentexport:** Der Segmentexport ist einer der beiden Zieltypen und sendet die Profil, die qualifiziert sind und dem Ziel zugeordnet wurden. Verwendet Segment- und Benutzer-IDs und pseudonyme Daten und integriert sich in der Regel in soziale Netzwerke und andere Plattformen zur Zielgruppe digitaler Medien.

**Segment-ID:** Segment-ID ist eine automatisch generierte ID, die mit einem Segment verknüpft ist.

**Segmentmitgliedschaft:** Die Segmentmitgliedschaft zeigt an, zu welchem Segment ein Profil derzeit gehört.

**Segmentregeln:** Segmentregeln geben an, wo und wie der Benutzer definiert, welche Profil für das Segment qualifiziert sind.

**Segmenttyp:** Es gibt zwei Arten von Segmenten: Eines ist ein Segment, das dynamisch mit Änderungen an Experience Platform-Daten aktualisiert wird, und das andere ein Snapshot der Audience, der alle Profil erfasst, die Segmentregeln erfüllen, und diese Änderungen bleiben unverändert.

**Segmentierung:** Bei der Segmentierung wird eine große Gruppe von Kunden, Potenzieller Kunden oder Verbrauchern in kleinere Gruppen unterteilt, die ähnliche Attribute aufweisen und ähnlich wie Marketingstrategien reagieren.

**Sensei-ML-Framework:** Sensei ML Framework ist ein einheitliches Framework für maschinelles Lernen in Adobe, das Daten über Experience Platform nutzt, um Datenwissenschaftler bei der Entwicklung von intelligenten Diensten mit maschinellem Lernen schneller, skalierbar und wiederverwendbar zu unterstützen.

**Sensible Datenbezeichnungen:** Sensible &quot;S&quot;-Beschriftungen werden verwendet, um Daten zu kategorisieren, die als sensibel gelten, z. B. verschiedene Arten von Verhaltens- oder geografischen Daten, die als sensibel gekennzeichnet werden sollen.

**Dienste:** Ein leistungsstarkes Framework zur Operationalisierung von AI- und ML-Diensten mithilfe von Adobe Intelligent Services. Services liefern personalisierte Kundenerlebnisse in Echtzeit oder operalisieren benutzerdefinierte intelligente Dienste.

**S1-Datenbeschriftung:** `S1` Datenbeschriftung wird verwendet, um Daten zu klassifizieren, die Breiten- und Längengrad angeben, die zur Bestimmung der genauen Position eines Geräts verwendet werden können.

**S2-Datenbeschriftung:** `S2` Datenbeschriftung wird verwendet, um Daten zu klassifizieren, die zur Bestimmung eines breit definierten Geo-Zaun-Bereichs verwendet werden können.

**Quelle:** Source ist ein allgemeiner Begriff für jeden Input Connector in der Echtzeit-Kundendatenplattform.

**Quellenattribut:** Ein Quellattribut ist ein Feld im Quelldataset.  Quellattribute werden den Feldern des Schemas Zielgruppe zugeordnet.

**Source Connector:** Adobe Experience Platform Source Connectors unterstützen Benutzer bei der einfachen Erfassung von Daten aus mehreren Quellen und ermöglichen so die Strukturierung, Kennzeichnung und Verbesserung von Daten mithilfe von Experience Platform Services. Daten können aus verschiedenen Quellen wie Cloud-basierte Datenspeicherung, Drittanbieter-Software und CRM-Systeme erfasst werden.

**Quell-Kategorie:** Eine Quell-Kategorie ist eine Gruppierung von Echtzeit-Kundendatenplattformquellen mit ähnlichen Eigenschaften.

**Quellkatalog:** Ein Quellkatalog ist eine Liste der verfügbaren Quellen in der Echtzeit-Kundendatenplattform.

**Standard-Identitäts-Namensraum:** Standard-Identitäts-Namensraum sind von Adobe vordefinierte Identifikatoren, einschließlich Adobe- und Branchenstandards zur Identifizierung von Benutzern.

**Standard-Schema:** Standardmäßige Schema bestehen aus Klassen und Mixins und sind zur Wiederverwendung bestimmt.

**Streaming-Ingestion:** Die Streaming-Erfassung bietet Benutzern eine Methode, Daten von client- und serverseitigen Geräten in Echtzeit an Experience Platform zu senden.

**Streaming-Endpunkt-URL:** Eine Streaming-Endpunkt-URL ist ein eindeutiger Endpunkt, der von Adobe bereitgestellt wird und an das IMS-Format eines Kunden gebunden ist, um Daten in die Experience Platform zu streamen.

**Streaming-Segmentierung:** Die Streaming-Segmentierung ist ein fortlaufender Datenauswahlprozess, der Segmente entsprechend der Aktivität des Benutzers aktualisiert. Nachdem ein Segment erstellt und gespeichert wurde, wird die Segmentdefinition auf eingehende Daten im Echtzeit-Kundensegment angewendet. Segmentzufügungen und -entfernungen werden regelmäßig verarbeitet, um sicherzustellen, dass Ihre Audience der Zielgruppe relevant bleibt.

**Symbol:** Symbol ist eine Abkürzung eines Identitäts-Namensraums, der als Referenz in APIs verwendet werden kann.

**System-Ansicht:** Die Ansicht des Systems ist eine visuelle Darstellung der Quelldatasets, die durch Echtzeit-Kundendaten-Profile zu Zielen fließen.

[Zurück zum Anfang](#adobe-experience-platform-glossary)

## T

**Funktionen der Zielgruppe:** Die Funktion Zielgruppe ist in der Funktionszuordnung angegeben und wird von einem Modell vorhergesagt.

**Praktisches Modell:** Ein trainiertes Modell stellt die ausführbare Ausgabe eines Modellschulungsprozesses dar, bei dem eine Reihe von Schulungsdaten auf die Modellinstanz angewendet wurde. Ein ausgebildetes Modell behält einen Verweis auf alle intelligenten Webdienste bei, die daraus erstellt werden. Das geschulte Modell eignet sich für die Bewertung und Erstellung eines intelligenten Webdiensts. Änderungen an einem geschulten Modell können als neue Version nachverfolgt werden.

**Token:** Ein Token ist eine Art zweifakultativer Authentifizierungssicherheit, mit der die Verwendung von Computerdiensten mit Abfrage Service autorisiert werden kann.

**Typ:** Typ ist die Klasse des maschinellen Lernproblems, für das ein Rezept entworfen wurde und nach dem Training verwendet wird, um die Auswertung der Ausbildung zu erleichtern.

[Zurück zum Anfang](#adobe-experience-platform-glossary)

## U

**Vereinigung Schema:** Vereinigung Schema ist eine Konsolidierung von Schemas, die für Echtzeit-Kundendaten-Profil aktiviert wurden.

[Zurück zum Anfang](#adobe-experience-platform-glossary)

## V

[Zurück zum Anfang](#adobe-experience-platform-glossary)

## W

[Zurück zum Anfang](#adobe-experience-platform-glossary)

## X

**XDM (Experience Data Model):** XDM (Experience Data Model) ist das Konzept der Verwendung von Standard-Schemas zur Vereinheitlichung von Daten für die Verwendung mit Experience Platform- und Adobe Experience Cloud-Anwendungen. XDM ist eine formale Spezifikation, mit der alle Kundenerlebnisdaten in einer Sprache oder einem Standard-Datenmodell dargestellt werden. Mit XDM wird die Struktur von Daten standardisiert und der Prozess der Erlangung von Erkenntnissen aus enormen Datenmengen beschleunigt und vereinfacht.

**XDM DecisionEvent:** Ein DecisionEvent wird dazu verwendet, Beobachtungen über das Ergebnis und den Kontext einer Entscheidungs-Aktivität zu erfassen, einschließlich Informationen darüber, wie die Entscheidung getroffen wurde, wann sie stattfand, welche Optionen vorgeschlagen (und gewählt) wurden und welcher kontextuelle Zustand bestand, der die Entscheidung beeinflusste oder während des Entscheidungsprozesses beobachtet werden konnte. DecisionEvents erfasst auch die Proposition-ID, eine weltweit eindeutige ID, mit der die Entscheidung mit anderen Ereignissen korreliert werden kann. DecisionEvents sind nicht nur mit Experience Ereignisses verknüpft, die eine Entscheidung beeinflussten, sondern auch mit ExperienceEvents, die eine direkte Antwort auf einen Vorschlag sind. Es ist die Erwartung, dass Anwendungen in jedem ExperienceEvent auf die Proposition-ID verweisen, die von den Vorschlägen beeinflusst wurde. Der Proposition-Response-Verlauf in einem einzelnen Profil wird mithilfe von Proposition-IDs beibehalten.

**XDM ExperienceEvent:** Ein ExperienceEvent ist ein Faktendatensatz zu dem, was geschehen ist, einschließlich des Zeitpunkts und der Identität der beteiligten Person. ExperienceEvents können explizit (direkt erkennbare menschliche Aktionen) oder implizit (ohne direkte menschliche Aktion ausgelöst) sein und ohne Aggregation oder Interpretation aufgezeichnet werden. Sie sind für die Analyse von Zeitdomänen von entscheidender Bedeutung, da sie die Beobachtung und Analyse von Änderungen ermöglichen, die in einem bestimmten Zeitfenster auftreten, und den Vergleich zwischen mehreren Zeitfenstern, um Trends zu verfolgen.

**XDM Individuelles Profil:** Ein XDM Individual Profil bildet eine einzigartige Darstellung der Attribute und Interessen sowohl identifizierter als auch nur teilweise identifizierter Personen. Weniger identifizierte Profil können nur anonyme Verhaltenssignale wie Browser-Cookies enthalten, während hoch identifizierte Profil detaillierte persönliche Informationen wie Name, Geburtsdatum, Ort und E-Mail-Adresse enthalten können. Mit zunehmendem Profil wird es zu einem robusten Archiv mit persönlichen Informationen, Identifizierungsinformationen, Kontaktdaten und Kommunikationsvorlieben für eine Einzelperson.

**XDM-System:** XDM System ist die Infrastruktur, die Datensemantik und der Arbeitsablauf in Experience Platform, die auf Standard-Schemas basiert.

[Zurück zum Anfang](#adobe-experience-platform-glossary)

## Y

[Zurück zum Anfang](#adobe-experience-platform-glossary)

## Z

[Zurück zum Anfang](#adobe-experience-platform-glossary)
