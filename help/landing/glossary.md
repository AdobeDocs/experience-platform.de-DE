---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Adobe Experience Platform Glossar
topic-legacy: getting started
description: Ein Glossar wichtiger Experience Platform-Terminologie.
exl-id: 00eae5f5-7dfa-45ac-aff9-9e1769a3a53a
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '7137'
ht-degree: 1%

---

# Glossar zu Adobe Experience Platform {#adobe-experience-platform-glossary}

## A

**Zugriffskontrolle**: Durch rollenbasierte Zugriffskontrolle können Administratoren Benutzern von Experience Platformen Zugriff und Berechtigungen zuweisen. Zu den Berechtigungen gehören die Möglichkeit zur Ansicht und/oder Verwendung von Experience Platform-Funktionen wie das Erstellen von Sandboxen, das Definieren von Schemas und das Verwalten von Datensätzen.

**Zugriffsschlüssel-ID**: Eine Zugriffsschlüssel-ID ist eine eindeutige Kennung, die mit einem  [!DNL Amazon] S3-geheimen Zugriffsschlüssel verknüpft ist. Die Zugriffsschlüssel-ID und der geheime Zugriffsschlüssel werden zusammen verwendet, um AWS-Anforderungen zu signieren.[!DNL Amazon Web Services]

**Aktion**: Bei einer Aktion handelt es sich  [!DNL Platform Launch]um einen bestimmten Typ von Regelkomponente, mit der festgelegt wird, was nach dem Eintreten eines Ereignisses geschehen soll und welche Bedingungen ausgewertet und weitergereicht werden.

**Aktivieren**: &quot;Aktivieren&quot;ist die Aktion, die ein Benutzer zum Zuordnen eines Segments oder von Profilen zu einem Ziel wie  [!DNL Oracle Eloqua],  [!DNL Google]oder  [!DNL Salesforce Marketing Cloud] ausgeführt hat.

**Aktivität**: In  [!DNL Offer Decisioning]einer Aktivität ist die Logik enthalten, die die Auswahl eines Angebots informiert.

**Administrator**: Eine oder mehrere Personen in Ihrem Unternehmen, die Berechtigungen für die Experience Platform in Adobe Admin Console konfigurieren und anpassen können.

**Adobe Admin Console**: Adobe Admin Console bietet eine zentrale Stelle für die Verwaltung der Produktberechtigungen und den Zugriff auf Adoben für Ihr Unternehmen. Über die Konsole können Administratoren Benutzergruppen Zugriffsberechtigungen für verschiedene Plattformfunktionen erteilen, z. B. &quot;Ansichten-Datensätze verwalten&quot;, &quot;Datasets&quot;oder &quot;Profil verwalten&quot;.

**Adobe Experience Platform**: Adobe Experience Platform standardisiert Daten und Inhalte im gesamten Unternehmen und ermöglicht so Echtzeit-Profile für Verbraucher, Datenerhebung und beschleunigte Inhaltsgeschwindigkeit, um die Personalisierung von Erlebnissen über die Journey zu fördern.

**Adobe Experience Platform Launch**:  [!DNL Platform Launch] ist ein Tag- und SDK-Management-Ökosystem, das in Experience Platform und  [!DNL Experience Cloud] Anwendungen integriert ist. [!DNL Platform Launch] bietet Tools zur Bereitstellung, Vereinheitlichung und Verwaltung von Analyse-, Marketing- und Werbeintegrationen, die erforderlich sind, um relevante Kundenerlebnisse auf allen Client-Geräten zu ermöglichen.

**Adobe Experience Platform Abfrage Service**: Ermöglicht es Datenanalysten, Ereignis und Profil für die Abfrage in Analytics und maschinellem Lernen zu verwenden. Mit dem Abfrage Service können Datenwissenschaftler und Analysten alle in der Experience Platform gespeicherten Datensätze abrufen (einschließlich Verhaltensdaten sowie POS (Point-of-Sale), CRM (Customer Relationship Management) usw.) und diese Datensätze zur Beantwortung spezifischer Fragen zu den Daten Abfrage geben.

**Adobe Experience Platform-Segmentierungsdienst**: Ermöglicht das Erstellen von Segmenten und das Generieren von Audiencen aus Ihren Echtzeit-Daten zum Profil von Kunden. Diese Audiencen können dann in ihre eigenen Datensätze innerhalb des Data Lake exportiert werden.

**Adobe Intelligent Services**: Intelligente Dienste wie Attribution AI und Customer AI sind auf maschinellem Lernen basierende, auf künstlichen Erkenntnissen basierende Modelle, die zielgerichtet konzipiert sind und Experience Platform erfordern, damit sie ausgeführt und betrieben werden können.

**Adobe I/O**: Adobe I/O ist Teil der Experience Platform und bietet Zugriff auf alles, was Entwickler zur Integration, Erweiterung und Anpassung von Plattformen benötigen, einschließlich APIs, Ereignisse, Entwicklerkonsole und hilfreicher Werkzeuge.

**Adobe Sensei**: Adobe Sensei ist der Geheimdienstrahmen, der die Experience Platform beherrscht. Es bietet außerdem eine Reihe von AI-Diensten, die Marken in die Lage versetzen, ihre Fähigkeit zur Bereitstellung personalisierter Echtzeit-Kundenerlebnisse zu verbessern.

**Amazon S3-Behälter**:  [!DNL Amazon S3] Behälter sind die grundlegenden Container für im  [!DNL Amazon] Ökosystem gespeicherte Daten. Behälter enthalten Objekte, die Objekte werden mit einem eindeutigen Schlüssel gespeichert und abgerufen, der dem Entwickler zugewiesen wurde.

**Amazon S3-Anschluss**: Der  [!DNL Amazon] S3-Anschluss ermöglicht es Kunden von Experience Platform, ihre  [!DNL Amazon] S3-Daten sicher zu verbinden und darauf zuzugreifen.

**Speicherstrategie** anhängen: Die Speicherstrategie &quot;anhängen&quot;ist eine Option, die verwendet wird, wenn Daten von Drittanbietern angegeben werden, die über eine Verbindung aufgenommen werden sollen, und neue Daten oder Zeilen am Ende des Datensatzes angehängt werden. Die zuvor erfassten Zeilen bleiben unberührt und nur die seit der letzten geplanten Ausführung erstellten Zeilen werden in die Experience Platform aufgenommen. Alle Zeilen, die im Quellsystem geändert wurden, bleiben bei der Experience Platform unverändert.

**Array**: Arrays werden für geordnete Elemente mit demselben Datentyp verwendet.

**Künstliche Intelligenz**: Künstliche Intelligenz ist eine Theorie und Entwicklung von Computersystemen, die in der Lage sind, Aufgaben auszuführen, die normalerweise menschliche Intelligenz erfordern, wie visuelle Wahrnehmung, Spracherkennung, Entscheidungsfindung und Übersetzung zwischen Sprachen.

**Attribute**: Attribute sind bestimmte Eigenschaften, die ein Profil darstellen.

**Attributzusammenführung**: Beim Definieren einer Richtlinie zum Zusammenführen mit der Echtzeit-Client-Profil-API gibt das  `attributeMerge` Objekt an, wie die Richtlinie zum Zusammenführen bei Datenkonflikten Profil-Attribute priorisiert. Es entspricht der Auswahl einer [!UICONTROL Merge-Methode], wenn eine Zusammenführungsrichtlinie in der Plattform-Benutzeroberfläche definiert wird.

**Attribution AI**:  [!DNL Attribution AI] ist ein auf Adobe Sensei basierender intelligenter Dienst, der algorithmische Funktionen zur Zuordnung mehrerer Kanal über den gesamten Kundenlebenszyklus hinweg bereitstellt.

**Audience**: Eine Audience ist der resultierende Satz von Profilen, die die Kriterien einer Segmentdefinition erfüllen.

**Audience**: Eine Segmentgröße ist die Gesamtanzahl der Profil, die die Kriterien einer Segmentdefinition erfüllen und für eine Mitgliedschaft in der Audience infrage kommen.

**Schnappschuss** der Audience: Ein Audience-Schnappschuss erfasst alle Profil, die zum Zeitpunkt der Segmentierung für die Segmentkriterien infrage kommen.

## B

**Aufstockung**: Bei geplanten Quellen ermöglicht die Option &quot;Aufstocken&quot;die Erfassung von Verlaufsdaten.

**Aufstockungszeitraum**: Der Aufstockungszeitraum bietet die Möglichkeit, die Zeitdauer für die Erfassung von Verlaufsdaten von Drittanbietern über eine Quellverbindung festzulegen. Wenn Sie einen Aufstockungszeitraum von &quot;ewig&quot;wählen, wird der gesamte Verlauf der Quelldaten in die Experience Platform aufgenommen.

**Stapel**: Ein Stapel ist ein Datensatz, der über einen bestimmten Zeitraum erfasst und als eine Einheit verarbeitet wird. Datensätze bestehen aus mehreren Stapeln.

**Stapel-ID**: Eine Stapel-ID ist eine von der Adobe erzeugte ID für einen Datenstapel.

**Stapelverarbeitung**: Mit der Stapelverarbeitung können Sie Daten als Stapeldateien in die Experience Platform aufnehmen. Batches sind Dateneinheiten aus einer oder mehreren Dateien, die als Ganzes aufgenommen werden.

**Stapelsegmentierung**: Die Stapelsegmentierung ist eine Alternative zu einem laufenden Datenauswahlprozess und verschiebt alle Profil-Daten gleichzeitig durch Segmentdefinitionen, um entsprechende Audiencen zu erstellen. Nach der Erstellung wird dieses Segment gespeichert und gespeichert, damit es zur Verwendung exportiert werden kann.

**Erstellen**: Bei  [!DNL Platform Launch]einem Build handelt es sich um eine Datei oder einen Satz von Dateien, die alle Konfigurationen und den Code enthalten, die zum Ausführen der Geschäftslogik in einer Bibliothek erforderlich sind, sodass Sie diese Bibliothek auf Ihrer Website oder mobilen App bereitstellen können.

**Business Intelligence-Tools**: Business Intelligence (BI) Tools sind in erster Linie in  [!DNL Experience Platform Query Service]integriert. BI-Tools sind Typen von Anwendungssoftware, die große Mengen unstrukturierter Daten von internen und externen Systemen erfassen und verarbeiten.

## C

**Deckelung**: In  [!DNL Offer Decisioning]den Entscheidungsregeln wird durch die Deckelung (auch als Frequenzzuordnung bezeichnet) festgelegt, wie oft ein Angebot präsentiert wird. Es gibt zwei Arten von Großbuchstaben: wie oft ein Angebot in der kombinierten Zielgruppe-Audience (als &quot;globale Obergrenze&quot;bezeichnet) vorgeschlagen werden kann und wie oft ein Angebot demselben Endbenutzer vorgeschlagen werden kann (als &quot;Profil-Cap&quot;bezeichnet).

**Katalog**: Im Zusammenhang mit Quellen und Zielen ist ein Katalog eine Galerie mit verfügbaren Verbindungen zu Adoben- und Drittanbietertechnologien. Nicht zu verwechseln mit [!DNL Catalog Service].

**[!DNL Catalog Service]**:  [!DNL Catalog Service] (manchmal auch als  [!DNL Catalog]) bezeichnet, ist das Datensatzsystem für den Speicherort und die Datenlinie innerhalb von Adobe Experience Platform. Während alle Daten, die in die Experience Platform aufgenommen werden, als Dateien und Verzeichnisse im Datensee gespeichert werden, enthält [!DNL Catalog] die Metadaten und Beschreibungen dieser Dateien und Ordner zum Nachschlagen, Überwachen und Verwalten von Daten.

**Klasse**: Im Experience Data Model (XDM) definiert eine Klasse den kleinsten Feldsatz, der zum Erstellen eines Schemas verwendet wird, und definiert das Basisverhalten des Geschäftsobjekts, das das Schema darstellt.

**Client**: Ein Client ist ein externes Tool oder eine Anwendung, die eine Verbindung  [!DNL Query Service] über das PostgreSQL-Protokoll oder die HTTP-API herstellt.

**Sammlung**: Sammlungen sind  [!DNL Offer Decisioning]Untergruppen von Angeboten, die auf vordefinierten, von einem Marketingspezialisten definierten Bedingungen basieren, wie z. B. der Kategorie des Angebots.

**Kombinieren mit PII-Marketingmaßnahmen**: Eine Marketingaktion, die alle persönlichen identifizierbaren Informationen (PII) mit anonymen Daten kombiniert. Verträge über Daten, die aus Werbenetzwerken, Werbeservern und Drittanbietern von Daten bezogen werden, beinhalten häufig spezifische vertragliche Verbote der Verwendung solcher Daten mit direkt identifizierbaren Daten.

**Befehlszeilenschnittstelle**: Eine Befehlszeilenschnittstelle ist ein textbasiertes Tool, mit dem eine Verbindung  [!DNL Query Service] zur Ausführung von Rohdaten hergestellt werden kann.

**Zusammensetzung**: Eine Komposition ist eine Gruppierung von Komponenten, die sich zu dem Schema zusammensetzen.

**Bedingung**: In  [!DNL Platform Launch]einer Bedingung ist eine Regelkomponente, die eine logische Anweisung auswertet, die zurückgegeben  `true` oder  `false`zurückgegeben werden muss. Alle Bedingungen müssen mit `true` ausgewertet werden und alle Ausnahmebedingungen müssen mit `false` ausgewertet werden, bevor Aktionen für die Regel ausgeführt werden.

**Konsole**: In  [!DNL Query Service]der Konsole finden Sie Informationen zum Status und zum Betrieb einer Abfrage. Die Konsole zeigt den Verbindungsstatus zu [!DNL Query Service], ausgeführte Abfragen-Vorgänge und alle Fehlermeldungen an, die sich aus diesen Abfragen ergeben.

**Beschriftungen** des Vertrags (&quot;C&quot;): Die Datenverwendungsbeschriftungen (&quot;C&quot;) werden zur Kategorisierung von Daten verwendet, die vertragliche Verpflichtungen haben oder mit den Datenverwaltungs-Richtlinien eines Kunden in Zusammenhang stehen.

**Vertragsbezeichnung** C1: Eine Beschriftung zur  `C1` Vertragsdatenverwendung gibt an, dass Daten nur in aggregierter Form aus Adobe Experience Cloud exportiert werden können, ohne dass dabei einzelne IDs oder Gerätekennungen einbezogen werden. Zum Beispiel Daten, die aus sozialen Netzwerken stammen.

**C2-Vertragsbezeichnung**: Eine  `C2` Vertragsdatenverwendungsbeschriftung gibt Daten an, die nicht in einen Drittanbieter exportiert werden können. Einige Datenanbieter haben in ihren Verträgen Bedingungen, die den Export von Daten, von denen sie ursprünglich erfasst wurden, verbieten. So wird beispielsweise die Übertragung von Daten, die Sie von sozialen Netzwerken erhalten, oft durch Verträge eingeschränkt. C2 ist restriktiver als C1, was nur Aggregation und anonyme Daten erfordert.

**Vertragsbezeichnung** C3: Eine Beschriftung für die  `C3` Vertragsdatennutzung gibt Daten an, die nicht mit direkt identifizierbaren Informationen kombiniert oder anderweitig verwendet werden können. Einige Datenanbieter haben Vertragsbedingungen, die die Kombination oder Verwendung dieser Daten mit direkt identifizierbaren Informationen verbieten. Verträge für Daten, die aus Werbenetzwerken, Werbeservern und Drittanbietern von Daten bezogen werden, enthalten beispielsweise oft spezifische vertragliche Verbote für die Verwendung direkt identifizierbarer Daten.

**Vertragsbezeichnung** C4: Eine Beschriftung für die  `C4` Vertragsdatennutzung gibt an, dass Daten nicht für das Targeting von Anzeigen oder Inhalten auf der Site oder über die Site hinweg verwendet werden können. C4 ist die restriktivste Bezeichnung, da sie C5-, C6- und C7-Etiketten umfasst.

**C5-Vertragsbezeichnung**: Eine Beschriftung für die  `C5` Vertragsdatennutzung gibt an, dass Daten nicht für das Site-übergreifende Targeting von interessenbasierten Inhalten oder Anzeigen verwendet werden können. Interessensbasiertes Targeting oder Personalisierung tritt auf, wenn die folgenden drei Bedingungen erfüllt sind: Die vor Ort erfassten Daten werden verwendet, um Rückschlüsse auf das Interesse eines Benutzers zu ziehen; in einem anderen Kontext verwendet wird, z. B. auf einer anderen Site oder App; und wird verwendet, um festzulegen, welche Inhalte oder Anzeigen auf der Grundlage dieser Schlussfolgerungen bereitgestellt werden.

**C6-Vertragsbezeichnung**: Eine Beschriftung zur  `C6` Vertragsdatennutzung gibt an, dass Daten nicht für das Targeting von Onsite-Anzeigen verwendet werden können. Das Targeting von Anzeigen auf der Site umfasst die Auswahl und den Versand von Anzeigen auf Websites oder Apps Ihrer Organisation oder zur Messung des Versands und der Effektivität solcher Anzeigen. Dazu gehören die Verwendung von zuvor erfassten Onsite-Daten über das Interesse der Benutzer bei der Auswahl von Anzeigen, Prozessdaten darüber, wann und wo die Anzeigen angezeigt wurden und ob die Benutzer irgendwelche Aktionen im Zusammenhang mit der Werbung ergriffen haben, wie z. B. die Auswahl einer Anzeige oder den Kauf einer Anzeige.

**C7-Vertragsbezeichnung**: Eine Beschriftung für die  `C7` Vertragsdatennutzung gibt an, dass Daten nicht für das Targeting von Inhalten auf der Site verwendet werden können. Das Targeting von Inhalten auf der Site umfasst die Auswahl und den Versand von Inhalten auf den Websites oder Apps Ihres Unternehmens oder die Messung des Versands und der Effektivität solcher Inhalte. Dazu gehören zuvor erfasste Informationen über das Interesse der Benutzer an der Auswahl von Inhalten, die Verarbeitung von Daten darüber, welche Inhalte angezeigt wurden, wie oft und wie lange sie angezeigt wurden, wann und wo sie angezeigt wurden und ob die Verwendungszwecke irgendwelche Aktionen im Zusammenhang mit dem Inhalt durchgeführt haben, einschließlich der Auswahl von Inhalten.

**Vertragsbezeichnung** C8: Eine Beschriftung für die  `C8` Vertragsdatennutzung gibt an, dass Daten nicht zur Messung der Websites oder Apps Ihres Unternehmens verwendet werden können. Dies umfasst nicht das interessensbasierte Targeting, d. h. die Erfassung von Informationen über Ihre Nutzung dieses Dienstes zur späteren Personalisierung von Inhalten und/oder Werbung in anderen Kontexten.

**Vertragsbezeichnung** C9: Eine  `C9` Beschriftung für die Verwendung von Vertragsdaten gibt an, dass Daten nicht in datenwissenschaftlichen Workflows verwendet werden können. Einige Verträge beinhalten explizite Verbote von Daten, die für die Datenwissenschaft verwendet werden. Manchmal werden diese Begriffe in Begriffen ausgedrückt, die die Verwendung von Daten für künstliche Intelligenz (KI), maschinelles Lernen (ML) oder Modellierung verbieten.

**C10-Kontraktbeschriftung**: Eine Beschriftung für die  `C10` Vertragsdatennutzung gibt an, dass Daten nicht für die Aktivierung von zusammengenähten Identitäten verwendet werden können. Einige Datenverwendungsrichtlinien beschränken die Verwendung von gehefteten Identitätsdaten für die Personalisierung. Die Beschriftung `C10` wird automatisch auf Segmente angewendet, wenn deren Zusammenführungsrichtlinien die Option &quot;Privates Diagramm&quot;verwenden.

**Spalte** Erstellungsdatum: Die Auswahl der Spalte &quot;Erstellungsdatum&quot;ist eine Option, wenn Sie Daten von Drittanbietern über eine Quellverbindung angeben. Wenn die Option zum Anhängen einer Speicherstrategie ausgewählt ist und das DataSet-Schema mehrere Datumsfelder enthält, müssen Sie aus dem verfügbaren Schema eine Schlüsselspalte für das Erstellungsdatum angeben. Die Option &quot;Erstellungsdatum&quot;steht nicht zur Verfügung, wenn die Speicherstrategie zum Überschreiben ausgewählt wurde.

**Tabelle als Auswahl** erstellen: &quot;Tabelle als Auswahl erstellen&quot;(CTAS) ist ein SQL-Befehl, der bei Ausführung im Rahmen einer vollständigen und gültigen SQL-Abfrage anweist, die Ergebnisse der Abfrage in einem Datensatz  [!DNL Query Service] zu behalten. Sie können einen neuen Ergebnissatz erstellen, vorherige Ergebnisse überschreiben oder an vorherige Ergebnisse anhängen.

**Site-übergreifende Daten**: Site-übergreifende Daten sind die Kombination von Daten aus verschiedenen Sites, einschließlich einer Kombination aus Vor-Ort- und Offsite-Daten oder einer Kombination von Daten aus verschiedenen Offsite-Quellen.

**Site-übergreifende Targeting-Marketingaktion**: Eine Marketingaktion, die Daten für das Site-übergreifende Anzeigen-Targeting verwendet. Die Kombination von Daten aus verschiedenen Sites, einschließlich einer Kombination aus Vor-Ort-Daten und Offsite-Daten oder einer Kombination von Daten aus verschiedenen Offsite-Quellen, wird als Site-übergreifende Daten bezeichnet. Site-übergreifende Daten werden in der Regel gesammelt und verarbeitet, um Rückschlüsse auf die Interessen der Kunden zu ziehen.

**Benutzerdefinierter Identitäts-Namensraum**: Benutzerspezifische Identitätskennungen können von Ihrem Unternehmen erstellt werden, um Identitäten für eine bestimmte Organisation oder einen bestimmten Geschäftsfall darzustellen.

**Benutzerdefinierte Beschriftungen**: Mit benutzerdefinierten Datenverwendungsbeschriftungen können Sie spezifische Beschriftungen erstellen und auf Datenfelder anwenden, die bestimmten Geschäftsanforderungen entsprechen.

**Kunden-API**: Customer AI ist ein Intelligent Service auf der Basis von Adobe Sensei, der die Profil mit AI-basierten Eigenschaften bereichert und die Segmentierung und das Targeting von Kunden ermöglicht.

## D

**Datenwörterbuch**: Bei  [!DNL Platform Launch]einem Datenwörterbuch (auch als Datenzuordnung bezeichnet) handelt es sich um einen Satz von Datenelementen, die innerhalb einer Eigenschaft definiert werden.

**Datenelement**: Ein Datenelement ist  [!DNL Platform Launch]ein Zeiger, der in Regeln und Erweiterungen verwendet wird, um auf ein bestimmtes Datenelement zu verweisen, das auf dem Client-Gerät vorhanden ist.

**Datenerfassung**: Die Datenerfassung ist der Vorgang, bei dem Daten aus einer Quelle zur Experience Platform hinzugefügt werden. Daten können auf verschiedene Weise in die Plattform aufgenommen werden, einschließlich Streaming, Batches oder Hinzufügen über Quell-Connectors.

**Datenschicht**: Bei  [!DNL Platform Launch]einer Datenschicht handelt es sich um eine Datenstruktur, die auf dem Client-Gerät vorhanden ist und Metadaten zum Kontext enthält, in dem eine Seite oder ein Bildschirm angezeigt wird.

**Datenverwaltung**: Die Datenverwaltung umfasst die Strategien und Technologien, mit denen sichergestellt werden soll, dass die Daten im Einklang mit Vorschriften und organisatorischen Richtlinien zur Datenverwendung stehen.

**Datenintegrationspartner**: Die Data-Integration-Partner vereinfachen und automatisieren das Laden und Umwandeln enormer Datenmengen von über 200 Quellen in die Experience Platform, ohne dass Code geschrieben werden muss.

**Datenbeschriftungen**: Datennutzungsbeschriftungen können zu Datasets hinzugefügt werden. Alle Felder in diesem Datensatz übernehmen die Beschriftungen des Datensatzes.

**Data Science Workspace**:  [!DNL Data Science Workspace] Mit Experience Platform können Kunden maschinelle Lernmodelle erstellen, die Daten aus Plattform- und Adobe-Anwendungen verwenden, um intelligente Segmente zu erstellen, Erkenntnisse zu generieren und Prognosen zu erstellen, sodass Sie digitale Endbenutzererlebnisse deutlich verbessern können.

**Datenquelle**: Eine Datenquelle ist eine vom Benutzer festgelegte Herkunft von Daten. Beispiele für eine Datenquelle sind eine mobile App, Profil- und/oder Erlebnis-Ereignis, Website-Profil-Ereignis oder ein CRM.

**Datenstatus**: Ein Datenverwalter ist die Person, die für die Verwaltung, Überwachung und Durchsetzung der Datenbestände einer Organisation verantwortlich ist. Ein Datenmanager stellt außerdem sicher, dass die Datenschutzrichtlinien geschützt und so aufrechterhalten werden, dass sie mit den Regierungs- und Organisationsvorschriften im Einklang stehen.

**Datenstrom**: Ein Datenstrom ist ein Satz oder eine Sammlung von Nachrichten, die dasselbe Schema teilen und von derselben Quelle gesendet werden.

**Datentyp**: Ein Datentyp ist eine wiederverwendbare XDM-Ressource, die ein Objekt-Typ-Feld mit mehreren Eigenschaften in einer hierarchischen Darstellung definiert.

**Datenverwendungsbeschriftungen**: Datenverwendungsbeschriftungen ermöglichen es Ihnen, Daten zu kategorisieren, die datenschutzbezogene Erwägungen und Vertragsbedingungen widerspiegeln, damit sie mit Vorschriften und Unternehmensrichtlinien übereinstimmen. Zu einem Datensatz hinzugefügte Datenverwendungsbeschriftungen werden vererbt oder auf alle Felder in diesem Datensatz angewendet. Datenverwendungsbeschriftungen können auch direkt auf Felder angewendet werden.

**Datenflug**: Ein Datenflug ist eine virtuelle Datenpipeline, die von einer Quelle bis zu Zielen in die Plattform fließt.

**Datenfluss**: Ein Datenflug-Ausführung ist ein Datendurchlauf, der auf der Grundlage eines vom Benutzer festgelegten Zeitplans in die Experience Platform gelangt.

**Datensatz**: Ein Datensatz ist ein Datenspeicherung- und Verwaltungskonstrukt für eine Datenerfassung, normalerweise eine Tabelle, die ein Schema (Spalten) und Felder (Zeilen) enthält.

**Datenbestand-ID**: Ein von der Adobe generierter Bezeichner für einen erfassten Datensatz.

**Datensatzausgabe**: Die Datensatzausgabe bietet einen Mechanismus, um zu bestimmen, welche Option &quot;Tabelle als Auswahl erstellen&quot;für eine bestimmte  [!DNL Query Service] Ausführung verwendet wird.

**Delta-Spalte**: In einer Delta-Spalte können Sie ein Quelldatenfeld auswählen, das einen Zeitstempel für die inkrementelle Erfassung darstellt.

**Delta-Speicherstrategie**: Die Delta-Speicherstrategie ist eine Option zum Erfassen von Daten von Drittanbietern über eine Quellverbindung. Mit dieser Option kann der Benutzer festlegen, dass neue oder geänderte Zeilen mit Quelldaten in die Experience Platform aufgenommen werden. Neue Zeilen werden am Ende des Datensatzes hinzugefügt und geänderte Zeilen werden im Datensatz bei der Experience Platform aktualisiert.

**Deskriptor**: Im Experience Data Model (XDM) ist ein Deskriptor ein zusätzlicher Satz von Schema-bezogenen Metadaten, der ein bestimmtes Verhalten für ein Feld beschreibt. Deskriptoren können von der Experience Platform verwendet werden, um das beabsichtigte Verhalten von Schemas zu verstehen, z. B. die Beziehung zwischen zwei Schemas.

**Ziel**: Ein Ziel ist ein allgemeiner Begriff für einen Endpunkt, z. B. eine Adobe, eine Werbungsplattform, einen Cloud-Datenspeicherung-Dienst oder einen Marketingdienst, bei dem eine Audience aktiviert und bereitgestellt wird.

**Ziel-Kategorie**: Eine Ziel-Kategorie ist eine Gruppe von Zielen mit ähnlichen Merkmalen.

**Zielkatalog**: Ein Zielkatalog ist eine Liste der verfügbaren Ziele in der Experience Platform.

**Direktaufrufregeln**: Bei  [!DNL Platform Launch]einer Direktaufrufregel handelt es sich um eine Regel, die ausgeführt wird, wenn sie direkt von der Seite aus aufgerufen wird, wobei Ereignis- und Suchsysteme umgangen werden.

**Anzeigename**: Im Experience Data Model (XDM) ist ein Anzeigename ein benutzerfreundlicher Name für ein Feld, das in der Benutzeroberfläche angezeigt wird.

## E

**Förderfähiges Angebot**: Ein förderfähiges Angebot kann einem Profil konsistent angeboten werden, da es die im Upstream definierten Einschränkungen erfüllt.

**Eignungsregeln**: In  [!DNL Offer Decisioning]diesem Fall werden Eignungsregeln auf ein Profil angewendet, das sich auf Kalender-, Zeitplan- und Deckelungsbeschränkungen bezieht.

**E-Mail-Targeting-Marketingaktion**: Eine Marketingaktion, die Daten in E-Mail-Targeting-Kampagnen verwendet.

**Einbettungscode**: Bei  [!DNL Platform Launch]dem Einbettungscode handelt es sich um ein Skript-Tag, das auf einer Site oder Umgebung in den HTML-Code eingefügt wird. Der Einbettungscode weist den Browser an, wo der Build abgerufen werden soll.

**Auflistung**: Eine Auflistung (enum) ist ein XDM-Feld, das auf einen Satz vordefinierter Werte beschränkt ist.

**Umgebung**: Bei einer Umgebung handelt es sich  [!DNL Platform Launch]um einen Satz von Bereitstellungsanweisungen, die den Host-Versand und das Dateiformat eines Builds angeben. Eine Bibliothek muss mit einer Umgebung gepaart werden, bevor sie erstellt werden kann.

**Fehlerdiagnose**: Die Fehlerdiagnose ermöglicht die Generierung detaillierter Fehlermeldungen für erfasste Stapel. Mit dem Fehlerschwellenwert können Sie den Prozentsatz der zulässigen Fehler konfigurieren, bevor ein Stapel fehlschlägt.

**Ereignis**: Bei  [!DNL Platform Launch]einem Ereignis handelt es sich um einen bestimmten Typ von Regelkomponente, bei dem es sich um einen Trigger handelt, der auf einem Client-Gerät auftritt, um die Ausführung einer Regel zu beginnen.

**Ereignis-Entitäten**: Im Rahmen der Datenmodellierung stellen Ereignis-Entitäten Konzepte dar, die mit Aktionen zusammenhängen, die ein Kunde ausführen kann, Systemkonzepte oder andere Ereignisse, bei denen Sie Änderungen im Laufe der Zeit nachverfolgen möchten. Entitäten, die unter diese Kategorie fallen, sollten durch Schema dargestellt werden, die auf der [!DNL XDM ExperienceEvent]-Klasse basieren.

**Ereignisse**: Ereignis sind die mit einem Profil verknüpften Verhaltensdaten.

**Experience Data Model (XDM)** [!DNL Experience Data Model]  (XDM) ist ein Open-Source-Framework, das Standarddaten mithilfe von Schemas für die Verwendung mit Experience Platform- und Adobe Experience Cloud-Anwendungen vereinheitlicht. XDM standardisiert die Strukturierung von Daten und beschleunigt und vereinfacht den Prozess der Gewinnung von Erkenntnissen aus enormen Datenmengen.

**Experiment**: Bei einem Experiment wird ein trainiertes Modell erstellt, indem die Instanz mit einem Beispielteil der Live-Produktionsdaten trainiert wird. Dies unterscheidet sich von einem trainierten Modell, das mit einem Holdout-Testdatensatz getestet wird. Das unterscheidet sich auch vom Konzept eines Experiments in einigen maschinellen Lernstrukturen, bei dem es tatsächlich ein Beispielmodellierungsprojekt bedeutet.

**Experience Ereignis**: Ein Experience Ereignis stellt eine Momentaufnahme des Systems dar, wenn eine Interaktion oder ein Ereignis im Zusammenhang mit einem Kundenerlebnis stattfindet. Erlebnis-Ereignis sind unveränderliche Faktenaufzeichnungen über das, was geschehen ist, und stellen dar, was ohne Aggregation oder Interpretation passiert ist. In Experience Data Model (XDM) wird dieses Konzept von der [!DNL XDM ExperienceEvent]-Klasse erfasst.

**Erweiterung**: Eine Erweiterung  [!DNL Platform Launch]ist ein Funktionspaket, das einer  [!DNL Platform Launch] Eigenschaft hinzugefügt wird. Eine Erweiterung konzentriert sich in der Regel auf eine bestimmte Marketing- oder Analyselösung und stellt die Werkzeuge bereit, die zur Bereitstellung dieser Technologie in einer Client-Umgebung erforderlich sind.

**Erweiterungspaket**: Ein Erweiterungspaket  [!DNL Platform Launch]ist eine ZIP-Datei, die von einem Erweiterungs-Entwickler erstellt und hochgeladen wird und die  [!DNL Platform Launch] Benutzern alle erforderlichen Informationen zum Installieren der Erweiterung in ihrer Eigenschaft liefert. Ein Erweiterungspaket enthält ein Manifest, das Informationen über die Erweiterung, das HTML/JavaScript, das zum Konfigurieren des Verhaltens der [!DNL Platform Launch]-Erweiterung erforderlich ist, und das ausführbare JavaScript, das an die Client-Umgebung geliefert wird (falls erforderlich), angibt.

## F

**Fallback-Angebot**: Ein Ausweichmanöver-Angebot ist das Standard-Angebot, das angezeigt wird, wenn ein Endbenutzer für keines der Angebot in der verwendeten Sammlung berechtigt ist.

**Funktionszuordnung**: Die Funktionszuordnung bezieht sich auf den Prozess der Zuordnung von Funktionen aus Daten zu Eingabe- und Zielgruppe-Funktionen, die für ein maschinelles Lernmodell erforderlich sind.

**Feld**: Ein Feld ist das Element der untersten Ebene eines Datensatzes, wie es vom XDM-Schema des Datensatzes definiert wird. Jedes Feld hat einen Namen für Verweiszwecke und einen Typ, der den Typ der darin enthaltenen Daten angibt. Zu den Feldtypen können Ganzzahl, Zahl, Zeichenfolge, boolescher Wert und Objekt gehören.

**Feldbeschriftungen**: Feldbezeichnungen sind Bezeichnungen zur Datenverwaltung, die entweder von einem Datensatz übernommen oder direkt auf ein Feld angewendet werden.

**Feldname**: Ein Feldname wird verwendet, um auf den Feldwert in Abfragen und nachgeschalteten Diensten zu verweisen.

**Häufigkeit**: In  [!DNL Query Service]der Häufigkeit wird bestimmt, wie oft eine wiederkehrende geplante Abfrage ausgeführt wird.

## G

**Kompetenz**: Eine Geofence ist eine durch GPS- oder RFID-Technik definierte geographische Grenze, die es der Software ermöglicht, eine Antwort zu Triggern, wenn ein Mobilgerät in ein bestimmtes Gebiet einsteigt oder es verlässt.

**GDPR (Allgemeine Datenschutzverordnung)**: Die Allgemeine Datenschutzverordnung (GDPR) ist ein Rechtsrahmen, der Leitlinien für die Erhebung und Verarbeitung personenbezogener Daten innerhalb der Europäischen Vereinigung (EU) festlegt. Der GDPR legt die Grundsätze für das Data Management und die Rechte des Einzelnen fest und deckt alle Firmen ab, die sich mit den Daten der Unionsbürger befassen.

## H

**Host**: In  [!DNL Platform Launch]einem Host werden der Speicherort, die Domäne und die Benutzerberechtigungen angegeben, die für die Bereitstellung  [!DNL Platform Launch] des Builds erforderlich sind.

## I

**Identität**: Eine Identität ist ein Bezeichner, der einen einzelnen Kunden eindeutig darstellt, z. B. eine Cookie-ID, Geräte-ID oder E-Mail-ID.

**Identitätsfelder**: Identitätsfelder sind XDM-Felder, mit denen Informationen über einzelne Kunden aus mehreren Datenquellen zusammengeführt werden. Eine einzige primäre Identität muss definiert werden, damit das Schema für die Verwendung im Echtzeit-Profil aktiviert werden kann.

**Identitätsbezeichnungen**: Identitätskennzeichen (&quot;I&quot;) dienen zur Kategorisierung von Daten, die eine bestimmte Person identifizieren oder kontaktieren können.

**Identitätsdiagramm**: Ein Identitätsdiagramm ist eine Zuordnung der Beziehungen zwischen zusammengesetzten und verknüpften Identitäten, die für einen einzelnen Kunden bestehen. Jedes Identitätsdiagramm wird mit der Aktivität der Kunden in Echtzeit aktualisiert. Die gemeinsame Struktur der Identitätsbeziehungen in Ihren Daten wird durch das [!UICONTROL Private Diagramm] dargestellt, das als struktureller Entwurf für jedes einzelne Identitätsdiagramm dient.

**Identitäts-Namensraum**: Ein Identitäts-Namensraum definiert den Kontext einer ID, z. B. eine E-Mail-Adresse oder eine CRM-ID.

**Identitätsdienst**:  [!DNL Experience Platform Identity Service] ermöglicht die Erstellung und Verwaltung von Identitätstypen, sodass Sie die Kundenidentitäten geräteübergreifend und geräteübergreifend verknüpfen können. Die Fähigkeit des Dienstes, Identitäten miteinander zu verknüpfen, ermöglicht es dem Echtzeit-Profil, eine vollständige Darstellung der einzelnen Kunden zu liefern.

**Identitätszuordnung**: Identitätszuordnung ist der Prozess der Identifizierung von Datenfragmenten und deren Zusammenführung zu einem vollständigen Profil-Datensatz.

**Identitätssymbol**: Ein Identitätssymbol ist eine Abkürzung eines Identitäts-Namensraums, der als Referenz in APIs verwendet werden kann.

**Identitätswert**: Ein Identitätswert in Verbindung mit einem Identitäts-Namensraum ist ein Bezeichner, der eine eindeutige Einzelperson, Organisation oder ein Asset darstellt. Bei der Zuordnung von Datensatzdaten zu Profil-Fragmenten müssen Namensraum und Identitätswert übereinstimmen.

**i1-Datenverwendungsbeschriftung**: Die  `I1` Datenverwendungsbeschriftung wird verwendet, um Daten zu klassifizieren, die eine bestimmte Person direkt identifizieren oder kontaktieren können und nicht ein Gerät.

**I2-Datenverwendungsbeschriftung**: Die  `I2` Datenverwendungsbeschriftung wird verwendet, um Daten zu klassifizieren, die in Verbindung mit anderen Daten zur indirekten Identifizierung oder Kontaktaufnahme mit einer bestimmten Person verwendet werden können.

**IMS-Organisation**: Eine IMS-Organisation (manchmal auch als IMS-Org bezeichnet) ist der Name, mit dem eine Firma oder eine bestimmte Gruppe innerhalb einer Firma über verschiedene Adoben hinweg identifiziert wird. Administratoren können den Zugriff und die Berechtigungen von Funktionen für Benutzer einer Organisation konfigurieren und verwalten.

**Ingestion**: Siehe Datenerfassung.

**Ingestion Plan**: Ein Erfassungszeitplan bietet zeitbasierte Optionen, wenn Sie von einer Quelle zur Experience Platform wechseln.

**Eingabefunktion**: Eine Eingabefunktion ist in der Funktionszuordnung angegeben und wird von einem Modell für maschinelles Lernen verwendet, um Prognosen zu erstellen.

**[!DNL Intelligent Services]**:  [!DNL Intelligent Services] zum Beispiel  [!DNL Attribution AI] und  [!DNL Customer AI] sind auf maschinellem Lernen basierende Modelle mit künstlicher Intelligenz, bei denen Experience Platform (oder auf Plattform aufbauende Anwendungen wie Echtzeit-Kundendatenplattform) erforderlich sind, um ausgeführt und betrieben zu werden.

**Interessensbasiertes Targeting oder Personalisierung**: Interessensbasiertes Targeting, auch Personalisierung genannt, tritt auf, wenn die folgenden drei Bedingungen erfüllt sind:

1. Daten, die vor Ort gesammelt werden, dienen dazu, Rückschlüsse auf das Interesse eines Benutzers zu ziehen.
1. Daten werden in einem anderen Kontext verwendet, z. B. auf einer anderen Site oder App (außerhalb der Site).
1. Mithilfe von Daten wird festgelegt, welche Inhalte oder Anzeigen auf der Grundlage dieser Schlussfolgerungen bereitgestellt werden.

## J

**[!DNL JupyterLab]**: Eine Open-Source-webbasierte Schnittstelle für das Projekt,  [!DNL Jupyter] die in die Plattform-Benutzeroberfläche integriert ist.

**[!DNL Jupyter Notebook]**: Dank der Integration mit JupyterLab können Sie mit Jupyter-Notebooks Datenbereinigung und -umwandlung, numerische Simulation, statistische Modellierung, Datenvisualisierung, maschinelles Lernen und vieles mehr in verschiedenen Sprachen wie Python, Scala und PySpark durchführen.

## K

## L

**Bibliothek**: Eine Bibliothek ist  [!DNL Platform Launch]ein Satz von Geschäftslogik, die Anweisungen zum Verhalten der  [!DNL Platform Launch] Bibliothek auf dem Client-Gerät enthält.

**Suchentitäten**: Im Zusammenhang mit der Datenmodellierung stellen Suchentitäten Konzepte dar, die sich auf eine einzelne Person beziehen können, aber nicht direkt zur Identifizierung der Person verwendet werden können. Entitäten, die unter diese Kategorie fallen, sollten durch Schema dargestellt werden, die auf benutzerdefinierten Experience Data Model-Klassen (XDM) basieren.

## M

**Maschinelles Lernen (ML)**: Maschinelles Lernen ist der Studienbereich, in dem Computer lernen können, ohne explizit programmiert zu werden.

**Modell** für maschinelles Lernen: Ein Modell für maschinelles Lernen ist ein Beispiel für ein Rezept für maschinelles Lernen, das mithilfe historischer Daten und Konfigurationen für die Lösung eines Geschäftsfalls trainiert wird. In Adobe Experience Platform Data Science Workspace werden Modelle für maschinelles Lernen als Rezepte bezeichnet.

**Zuordnung**: Bei der Datenzuordnung werden Quelldatenfelder den entsprechenden Zielgruppen in einem Ziel zugeordnet.

**Marketingaktion**: Im Rahmen der Datenverwaltung ist eine Marketingaktion (auch als Marketing-Anwendungsfall bezeichnet) eine Experience Platform, die von einem Datenbenutzer ausgeführt wird und bei der überprüft werden muss, ob die Datenverwendungsrichtlinien verletzt wurden.

**Merge-Methode**: Beim Definieren einer Richtlinie zum Zusammenführen mithilfe der Plattform-Benutzeroberfläche gibt die Zusammenführungsmethode an, wie Datenfragmente bei Auftreten eines Konflikts priorisiert werden sollen. Bei Verwendung der Echtzeit-Client-Profil-API zum Definieren einer Zusammenführungsrichtlinie wird die Zusammenführungsmethode mit dem `attributeMerge`-Objekt bestimmt.

**Richtlinie** zusammenführen: Zusammenführungsrichtlinien sind Regeln, die Experience Platform verwendet, um zu bestimmen, wie Kundendatenfragmente aus mehreren Quellen kombiniert werden, um ein einzelnes Profil zu erstellen. Wenn ein Datenkonflikt auftritt, bestimmt die Richtlinie zum Zusammenführen, welche Daten für die Aufnahme in das Profil priorisiert werden sollen.

**Mixin**: Im Erlebnis-Datenmodell (XDM) können Benutzer mit einem Mixin wiederverwendbare Felder erweitern, um ein oder mehrere Attribute zu definieren, die in ein Schema eingeschlossen werden sollen.

**Modul**: Ein Modul ist  [!DNL Platform Launch]ein Snippet ausführbaren JavaScript, das von einer Erweiterung bereitgestellt wird, die Aktionen in einer Client-Umgebung ausführt, ohne dass eine Regel erstellt werden muss.

## N

**Nicht-produktions-Sandbox**: Nicht-produzierende Sandboxen sind Sandboxen, die normalerweise für Entwicklungsversuche, Tests oder Tests verwendet werden. Im Gegensatz zu Produktions-Sandboxen können Nicht-Produktions-Sandboxen zurückgesetzt und gelöscht werden.

**[!DNL Notebooks]**:  [!DNL Notebooks] werden mit  [!DNL Jupyter Notebook] und können zur Analyse von Daten ausgeführt werden.

## O

**Angebot**: Ein Angebot ist eine Marketingbotschaft, die einem (potenziellen) Kunden ein Geschäfts- oder Verkaufsangebot enthält. Angebot verfügen oft über spezifische Regeln, die bestimmen, wer berechtigt ist, sie anzuzeigen oder zu empfangen.

**[!DNL Offer Decisioning]**:  [!DNL Offer Decisioning] Ermöglicht es Marketingexperten, Regeln und geschulte Modelle von Angebotsvorschlägen zu verwalten, wenn sie mit Endbenutzern auf der Grundlage von Daten interagieren, die über Kanal und Anwendungen hinweg gesammelt wurden.

**Angebot-Bibliothek**: Die Angebot-Bibliothek ist eine zentrale Bibliothek, die zum Verwalten von personalisierten Angeboten und Ausweichmanövern, Entscheidungsregeln und Aktivitäten verwendet wird.

**Marketingaktion** zur Personalisierung vor Ort: Eine Marketingaktion, die Daten zur Personalisierung von Inhalten auf der Site verwendet. Die Personalisierung auf der Site ist jede Daten, die dazu verwendet wird, Rückschlüsse auf die Interessen der Benutzer zu ziehen, und zur Auswahl der Inhalte oder Anzeigen, die auf diesen Schlussfolgerungen basieren, verwendet wird.

**Marketingaktion** zum Onsite-Targeting: Eine Marketingaktion, die Daten für Onsite-Anzeigen verwendet, einschließlich der Auswahl und des Versands von Anzeigen auf den Websites oder Apps Ihres Unternehmens oder zur Messung des Versands und der Effektivität solcher Anzeigen.

**Speicherstrategie** überschreiben: Die Speicherstrategie &quot;Überschreiben&quot;ist eine Option zum Erfassen von Daten von Drittanbietern über eine Verbindung, bei der Sie angeben können, ob die erfassten Daten nach einem bestimmten Zeitplan überschrieben werden.

## P

**Partielle Aufnahme**: Die teilweise Erfassung ermöglicht die Erfassung gültiger Datensätze von Stapeldaten innerhalb eines festgelegten Fehlerschwellenwerts. Die Fehlerdiagnose für fehlgeschlagene Datensätze kann unter [!UICONTROL Monitoring] oder [!UICONTROL Sources]-Übersicht über die Ausführung des Datenflusses heruntergeladen oder aufgerufen werden.

**Parkettdateien**: Bei einer Parquet-Datei handelt es sich um ein Spaltendateiformat mit komplexen verschachtelten Datenstrukturen. Zum Hinzufügen von Daten zum Ausfüllen eines Schema-Datensatzes sind Parkettdateien erforderlich.

**Personalisierte Angebot**: Ein personalisiertes Angebot ist eine benutzerspezifische Marketingbotschaft, die auf Eignungsregeln und Einschränkungen basiert.

**Platzierung**: Eine Platzierung ist der Ort und/oder Kontext, in dem ein Angebot für einen Endnutzer erscheint.

**Richtlinienarbeitsbereich**: Ein Arbeitsbereich in der Plattform-Benutzeroberfläche, der Datenweiterleitungen die Ansicht und Verwaltung von Datenverwendungsbeschriftungen und -richtlinien für Ihr Unternehmen ermöglicht.

**Richtlinie**: Eine Datenverwendungsrichtlinie ist eine Regel, die Marketingaktionen angibt, die auf der Grundlage der Anwendung von Gebrauchsbeschriftungen, die auf Plattformdaten angewendet werden, eingeschränkt sind.

**Durchsetzung** der Politik: Ermöglicht es Ihnen, Datenverwendungsrichtlinien mit angewendeten Marketingaktionen zu erzwingen, um Datenoperationen zu verhindern, die Richtlinienverletzungen innerhalb eines Unternehmens darstellen.

**Primär:** Ein Primärschlüssel ist eine Bezeichnung in einem Schema, um alle Datensätze eindeutig zu identifizieren.

**Priorität**: In  [!DNL Offer Decisioning]der Prioritätseinstellung werden Angebot nach Rangfolge sortiert, die alle Einschränkungen erfüllen, wie z. B. Förderfähigkeit, Kalender und Deckelung.

**Diagramm** zur privaten Identität: Das private Identitätsdiagramm (manchmal auch als privates Diagramm bezeichnet) ist eine private Zuordnung von Beziehungen zwischen verbundenen und verknüpften Identitäten, die auf Ihren Erstanbieterdaten basiert und nur von Ihrer Organisation sichtbar ist. Für jedes Unternehmen gibt es nur ein privates Diagramm, das als strukturelles Modell für die einzelnen Identitätsdiagramme dient, die für jeden Kunden erstellt werden, der mit Ihrer Marke interagiert.

**Produkt-Profil**: Mithilfe von Profilen können Administratoren allen oder einer Untergruppe von mit der Experience Platform verbundenen Diensten Zugriff gewähren.

**Produktions-Sandbox**: Eine Produktions-Sandbox ist eine Sandbox, die für die Verwendung in Ihrer Produktions-Umgebung vorgesehen ist. Im Gegensatz zu Nicht-Produktions-Sandboxen können Produktions-Sandboxen nicht zurückgesetzt oder gelöscht werden.

**Profil**: Ein Profil, das nicht mit Echtzeit-Customer-Profil als Service verwechselt werden darf, ist eine vollständige Darstellung eines einzelnen Kunden, die aus zusammengeführten Datensatz- und Zeitreihendaten aus mehreren Quellen aufgebaut ist.

**Zugriff auf** Profil: Der  `/entities` Endpunkt in der Echtzeit-Client-Profil-API ermöglicht Ihnen den Zugriff auf Datensatzdaten und Zeitreihen-Ereignis im Profil-Datenspeicher. Siehe auch: Profil-Entitäten

**Profil-Daten**: Profil-Daten beziehen sich auf alle Daten, die sich im Datenspeicher des Profils befinden.

**Profil-Datenspeicher**: Der Profil Data Store (manchmal auch als Profil Store bezeichnet) ist ein vom Data Lake getrenntes Datenspeichersystem, das vom Echtzeit-Customer-Profil zum Erstellen und Speichern von Profilen verwendet wird.

**Profil-Entitäten**: Profil-Entitäten stellen Attribute dar, die sich auf eine Einzelperson beziehen, in der Regel auf einen Kunden. Entitäten, die unter diese Kategorie fallen, sollten durch Schema dargestellt werden, die auf der [!DNL XDM Individual Profile]-Klasse basieren. Siehe auch: Zugriff auf Profile

**Profil-Export**:  [!DNL Profile] &quot;export&quot;ist eine der beiden Bestimmungsarten in der Experience Platform. [!DNL Profile] export generiert eine Datei mit Profilen und Attributen und verwendet PII-Rohdaten mit E-Mail, um sie in Marketing- und E-Mail-Automatisierungsplattformen zu integrieren.

**Profil-Fragment**: Ein Profil-Fragment ist die Information des Profils für nur eine Identität aus der Liste der Identitäten, die für einen bestimmten Kunden vorhanden sind.

**Profil-ID**: Eine Profil-ID ist eine automatisch generierte ID, die einem Identitätstyp zugeordnet ist und ein Profil darstellt.

**Eigenschaft**: Eine Eigenschaft ist  [!DNL Platform Launch]ein Container für alles, was zum Bereitstellen eines Satzes von Tags erforderlich ist.

## Q

**Abfrage**: Abfragen sind Datenanforderungen aus Datenbanktabellen.

**Abfragen-Editor**: Abfrage Editor ist ein Tool zum Schreiben, Prüfen und Senden von SQL-Anweisungen in  [!DNL Query Service].

## R

**Echtzeit-Kundendatenplattform**:  [!DNL Real-time Customer Data Platform] führt bekannte und unbekannte Kundendaten zusammen, um vertrauenswürdige Profil mit vereinfachter Integration, intelligenter Segmentierung und Echtzeit-Aktivierung über die digitale Journey zu erstellen.

**Echtzeit-Profil**: Echtzeit-Kundendaten (manchmal auch als Profil bezeichnet) bieten eine ganzheitliche Ansicht jedes einzelnen Profils, indem Daten aus mehreren Kanälen, einschließlich Online-, Offline-, CRM- und Drittanbieterdaten, kombiniert werden. Mit Profil können Sie Ihre Kundendaten in einzelne Profil zusammenfassen, die eine umsetzbare und zeitgestempelte Kundeninteraktion ermöglichen.

**Rezept**: Ein Rezept ist der Begriff der Adobe für eine Modellspezifikation. Es handelt sich dabei um einen Container auf oberster Ebene, der bestimmte maschinelle Lernprozesse, AI-Algorithmen, Verarbeitungslogik und Konfigurationsparameter darstellt, die zum Erstellen und Ausführen eines geschulten Modells erforderlich sind, um so zur Lösung spezifischer Geschäftsprobleme beizutragen.

**Datensatz**: Ein Datensatz sind Daten, die als Zeilen in einem Datensatz beibehalten werden.

**Aufzeichnen von Daten**: Stellt Informationen zu den Attributen eines Subjekts bereit. Ein Subjekt könnte eine Organisation oder eine Einzelperson sein.

**Wiederholung**: In  [!DNL Query Service]einer Wiederholung wird definiert, ob eine Abfrage nur einmal oder wiederholt ausgeführt werden soll.

**Vertretung**: Bei  [!DNL Offer Decisioning]einer Darstellung handelt es sich um Informationen, die von einem Kanal zum Anzeigen eines Angebots verwendet werden, z. B. Ort oder Sprache.

**Ressource**: Eine Ressource ist  [!DNL Platform Launch]ein allgemeiner Begriff, der auf Optionen verweist, die der  [!DNL Platform Launch] Benutzer innerhalb der Client-Umgebung konfigurieren kann, einschließlich Erweiterungen, Datenelemente und Regeln.

**Rollenbasierte Zugriffskontrolle**: Durch rollenbasierte Zugriffskontrolle können Administratoren Benutzern von Experience Platformen Zugriff und Berechtigungen zuweisen. Zu den Berechtigungen gehören die Möglichkeit zur Ansicht und/oder Verwendung von Experience Platform-Funktionen wie das Erstellen von Sandboxen, das Definieren von Schemas und das Verwalten von Datensätzen.

**Regel**: Eine Regel  [!DNL Platform Launch]ist eine Zusammenstellung von Komponenten, die einen bestimmten Satz von Ereignissen, Bedingungen und Aktionen definieren, die logisch gruppiert werden sollen.

**Regelkomponente**: Regelkomponenten sind  [!DNL Platform Launch]die Ereignis, Bedingungen und Aktionen, aus denen eine Regel besteht.

**Laufzeit**: Laufzeitumgebung gibt eine Laufzeitumgebung für ein maschinelles Lernrezept an. [!DNL Python]Mit den Laufzeitumgebungen R,  [!DNL Spark], PySpark und Tensorflow können Sie eine URL zu einem Docker-Bild für eine Rezept-Quelle eingeben.

## S

**Beispieldaten**: Musterdaten sind eine Vorschau einer Datendatei, in der Regel die ersten 100 Zeilen, die einem Datenwissenschaftler oder -ingenieur eine Vorstellung davon vermitteln, welches Schema oder welche Daten in der Datendatei enthalten sind.

**Sandbox**: Eine Sandbox ist ein virtuelles Konstrukt, das eine Plattforminstanz in eine separate virtuelle Umgebung aufteilt, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

**Sandbox-Reset**: Beim Zurücksetzen der Sandbox werden alle Daten einschließlich Daten, Profilen und Segmenten innerhalb einer Sandbox gelöscht. Sandbox-Resets können sich auf Daten auswirken, die mit internen oder externen Zielen verbunden sind.

**Sandbox-Umschalter**: Mit dem Sandbox-Umschalter in der Experience Platform können Benutzer zwischen Sandboxen navigieren, auf die sie Zugriff haben. Durch das Umschalten einer Sandbox werden alle Inhalte geändert und der Funktionszugriff kann je nach Berechtigungen geändert werden.

**Plan**: Ein Zeitplan ist eine benutzerdefinierte Spezifikation für die Häufigkeit oder Häufigkeit der Datenerfassung von einer Datenquelle eines Drittanbieters nach Adobe Experience Platform.

**Bewertung**: Die Auswertung ist der Prozess, bei dem mithilfe eines geschulten Modells Erkenntnisse aus Daten generiert werden.

**Schema**: Ein Schema ist ein Regelsatz, der die Datenstruktur und das Datenformat darstellt und überprüft. Ein Schema besteht aus einer Klasse und optionalen Mixin(en) und wird zum Erstellen von Datensätzen und Datastreams verwendet. Ein Schema kann Verhaltensattribute, Zeitstempel, Identitäten, Attributdefinitionen, Beziehungen und mehr enthalten.

**Schema-Bibliothek**: Die Schema-Bibliothek enthält branchenübliche XDM-Ressourcen, die nach Adobe bereitgestellt werden, sowie benutzerdefinierte Ressourcen, die von Ihrem Unternehmen definiert werden.

**Schema-Registrierung**: Die Schema Registry stellt eine Benutzeroberfläche und RESTful-API zur Verfügung, mit der alle Schema-bezogenen Ressourcen in der Schema-Bibliothek Ansicht und verwaltet werden.

**Schlüssel** für geheimen Zugriff: Ein geheimer Zugriffsschlüssel ist ein  [!DNL Amazon] S3-Schlüssel, der zusammen mit der Zugriffsschlüssel-ID zum Signieren von AWS-Anforderungen verwendet wird.

**Segment**: Ein Segment ist ein Regelsatz, der Attribute und Ereignis-Daten enthält, die eine Reihe von Profilen zu einer Audience machen.

**Segmentaufbau**: Die  [!DNL Segment Builder] ist eine visuelle Entwicklungs-Umgebung, mit der Segmentdefinitionen erstellt werden. Es dient als allgemeine Komponente aller Anwendungen, die den Segmentierungsdienst für Experience Platformen verwenden.

**Segmentdefinition**: Eine Segmentdefinition ist der Regelsatz, der zur Beschreibung der Hauptmerkmale oder des Verhaltens einer Zielgruppe-Audience verwendet wird. Nach der Konzeption werden die in einer Segmentdefinition beschriebenen Regeln verwendet, um qualifizierte Zielgruppenmitglieder für ein Segment zu bestimmen.

**Segmentbewertungsverfahren**: Es gibt zwei Methoden zur Segmentbewertung: geplant und auf Abruf. Die geplante Auswertung ermöglicht einen wiederkehrenden Zeitplan für die Ausführung eines Exportauftrags zu einem bestimmten Zeitpunkt, während die On-Demand-Auswertung die Erstellung eines Segmentauftrags zur sofortigen Erstellung der Audience beinhaltet.

**Segmentexport**: Der Segmentexport ist einer der beiden Zieltypen in der Experience Platform. Beim Segmentexport können Sie die Profil senden, die qualifiziert sind und dem Ziel zugeordnet wurden. Verwendet Segment- und Benutzer-IDs und pseudonyme Daten und integriert sich in der Regel in soziale Netzwerke und andere Plattformen zur Zielgruppe digitaler Medien.

**Segment-ID**: Eine Segment-ID ist eine automatisch generierte ID, die mit einem Segment verknüpft ist.

**Segmentmitgliedschaft**: Die Segmentmitgliedschaft zeigt an, zu welchen Segmenten ein Profil derzeit gehört.

**Segmentregeln**: Segmentregeln definieren die Bedingungen, die bestimmen, ob ein Profil für ein Segment qualifiziert ist.

**Segmentierung**: Bei der Segmentierung wird eine große Gruppe von Kunden, Potenzieller Kunden oder Verbrauchern in kleinere Gruppen unterteilt, die ähnliche Attribute aufweisen und ähnlich auf spezifische Marketingstrategien reagieren.

**Sensei-ML-Framework**: Sensei ML Framework ist ein einheitliches Framework für maschinelles Lernen (ML), das Experience Platformen nutzt, um Datenwissenschaftler in die Lage zu versetzen, schneller, skalierbar und wiederverwendbar XML-gestützte Informationsdienste zu entwickeln.

**Sensible (&quot;S&quot;) Beschriftungen**: Sensible (&quot;S&quot;) Beschriftungen werden verwendet, um Daten zu kategorisieren, die als sensibel gelten, z. B. verschiedene Arten von Verhaltens- oder geografischen Daten, die als sensibel gekennzeichnet werden sollen.

**Dienste**: Ein leistungsstarkes Framework zur Operationalisierung von AI- und ML-Diensten durch Nutzung von Adobe Intelligent Services. Services liefern personalisierte Kundenerlebnisse in Echtzeit oder operalisieren benutzerdefinierte intelligente Dienste.

**Marketing-Aktion** zur Personalisierung einer einzelnen Identität: Eine Marketingaktion, die Daten zur Personalisierung von Inhalten auf der Site verwendet. Bei der Onsite-Personalisierung handelt es sich um Daten, die dazu dienen, Schlussfolgerungen über die Interessen der Benutzer zu ziehen, und die dazu dienen, anhand dieser Schlussfolgerungen festzulegen, welche Inhalte oder Anzeigen bereitgestellt werden.

**S1-Datenverwendungsbeschriftung**: Eine  `S1` Datenverwendungsbeschriftung wird verwendet, um Daten zu klassifizieren, die Breiten- und Längengrad angeben, mit denen die genaue Position eines Geräts bestimmt werden kann.

**S2-Datenverwendungsbeschriftung**: Eine  `S2` Datenverwendungsbeschriftung wird verwendet, um Daten zu klassifizieren, die zur Bestimmung eines allgemein definierten Geofence-Bereichs verwendet werden können.

**Quelle**: Eine Quelle ist ein allgemeiner Begriff für jeden Input Connector in der Plattform. Siehe auch: Quellenanschluss

**Quellenattribut**: Ein Quellattribut ist ein Feld im Quelldataset. Quellattribute werden den Feldern des Schemas Zielgruppe zugeordnet.

**Quellkatalog**: Der Quellkatalog ist die Liste der verfügbaren Quellschnittstellen in der Experience Platform.

**Quell-Kategorie**: Eine Quell-Kategorie ist eine Gruppierung von Quellen mit ähnlichen Eigenschaften.

**Quellanschluss**: Mithilfe von Source Connectors (auch als Sources bezeichnet) können Anwender Daten aus mehreren Quellen problemlos erfassen, sodass Daten strukturiert, gekennzeichnet und mithilfe von Experience Platform-Diensten erweitert werden können. Daten können aus verschiedenen Quellen wie Cloud-basierte Datenspeicherung, Drittanbieter-Software und CRM-Systeme erfasst werden.

**Streaming-Verbindung**: Eine Streaming-Verbindung ist ein eindeutiger Endpunkt, der von der Adobe bereitgestellt und an die IMS-Organisation eines Kunden zum Streamen von Daten in die Experience Platform gebunden wird.

**Standard-Identitäts-Namensraum**: Standard-Identitäts-Namensraum sind vordefinierte Identitäts-Namensraum, die von der Adobe bereitgestellt werden und die branchenübliche Lösungen darstellen, mit denen Kunden identifiziert werden.

**Streaming-Erfassung**: Mit der Streaming-Erfassung können Sie Daten von client- und serverseitigen Geräten in Echtzeit an die Experience Platform senden.

**Streaming-Segmentierung**: Die Streaming-Segmentierung ist ein fortlaufender Datenauswahlprozess, der Segmente entsprechend der Aktivität des Benutzers aktualisiert. Nachdem ein Segment erstellt und gespeichert wurde, wird die Segmentdefinition auf eingehende Daten auf [!DNL Real-time Customer Profile] angewendet. Segmentzufügungen und -entfernungen werden regelmäßig verarbeitet, um sicherzustellen, dass Ihre Audience der Zielgruppe relevant bleibt.

**System-Ansicht**: Die Ansicht des Systems ist eine visuelle Darstellung der Quelldatasets, die  [!DNL Real-time Customer Profile] zu Zielen durchlaufen.

## T

**Funktionen** der Zielgruppe: Bei der Funktionszuordnung ist eine Zielgruppe die Funktion, die von einem Modell vorhergesagt wird.

**Zeitreihendaten**: Die Zeitreihendaten liefern eine Momentaufnahme des Systems zum Zeitpunkt, zu dem eine Aktion entweder direkt oder indirekt von einem Datensatzsubjekt durchgeführt wurde.

**Praktisches Modell**: Ein trainiertes Modell stellt die ausführbare Ausgabe eines Modellschulungsprozesses dar, bei dem eine Reihe von Schulungsdaten auf die Modellinstanz angewendet wurde. Ein ausgebildetes Modell behält einen Verweis auf alle intelligenten Webdienste bei, die daraus erstellt werden. Ein geschultes Modell eignet sich für die Bewertung und Erstellung eines intelligenten Webdiensts.

**Token**: Ein Token ist eine Art zweifakultativer Authentifizierungssicherheit, mit der die Verwendung von Computerdiensten autorisiert werden kann  [!DNL Query Service].

## U

**Vereinigung Schema**: Ein Vereinigung-Schema ist eine Konsolidierung von Schemas, die dieselbe Klasse teilen und für die aktiviert wurde  [!DNL Real-time Customer Profile]. Es können mehrere Vereinigungen Schema für ein Unternehmen vorhanden sein, aber es kann nur ein Schema pro Vereinigung geben.

## V

## W

## X

**XDM**: Siehe Erlebnis-Datenmodell (XDM).

**XDM-Entscheidungsinstrument**: Das XDM Decision Ereignis ist eine zeitreihenbasierte Klasse, mit der Beobachtungen über das Ergebnis und den Kontext einer Aktivität erfasst werden. Dazu gehören Informationen darüber, wie die Entscheidung getroffen wurde, wann sie stattfand, welche Optionen vorgeschlagen (und gewählt) wurden und welcher kontextuelle Zustand existierte, der die Entscheidung beeinflusste oder während des Entscheidungsprozesses beobachtet werden konnte.

**XDM ExperienceEvent**: XDM ExperienceEvent ist eine zeitreihenbasierte Klasse, die zum Erfassen des Systemzustands verwendet wird, wenn ein Ereignis (oder eine Gruppe von Ereignissen) aufgetreten ist, einschließlich des Zeitpunkts und der Identität des betreffenden Objekts. Siehe auch: Experience Ereignis

**XDM-Profil**: XDM  [!DNL Individual Profile] ist eine Datensatzbasierte Klasse, die eine einzigartige Darstellung der Attribute sowohl identifizierter als auch teilweise identifizierter Subjekte bildet. Profil, die eindeutig identifiziert werden, können für persönliche Kommunikation oder zielgerichtete Interaktionen verwendet werden und detaillierte persönliche Informationen wie Name, Geschlecht, Geburtsdatum, Ort und Kontaktdaten wie Telefonnummern und E-Mail-Adressen enthalten.

**XDM-System**: XDM System stellt das Framework dar, das XDM-Schema für die Verwendung in Diensten der nachgelagerten Experience Platform operalisiert.

## Y

## Z
