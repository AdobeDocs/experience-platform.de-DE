---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Adobe Experience Platform-Glossar
topic-legacy: getting started
description: Ein Glossar wichtiger Experience Platform-Terminologie.
exl-id: 00eae5f5-7dfa-45ac-aff9-9e1769a3a53a
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '7436'
ht-degree: 4%

---

# Glossar zu Adobe Experience Platform {#adobe-experience-platform-glossary}

## A 

**Zugriffskontrolle**: Die rollenbasierte Zugriffskontrolle ermöglicht es Administratoren, Experience Platform-Benutzern Zugriff und Berechtigungen zuzuweisen. Zu den Berechtigungen gehört die Möglichkeit, Funktionen der Experience Platform anzuzeigen und/oder zu verwenden, z. B. das Erstellen von Sandboxes, das Definieren von Schemas und das Verwalten von Datensätzen.

**Zugriffsschlüssel-ID**: Eine Zugriffsschlüssel-ID ist eine eindeutige Kennung, die mit einer [!DNL Amazon] geheimer S3-Zugriffsschlüssel. Die Zugriffsschlüssel-ID und der geheime Zugriffsschlüssel werden zusammen zum Signieren verwendet [!DNL Amazon Web Services] (AWS).

**Aktion**: Im Kontext von Tags ist eine Aktion ein bestimmter Typ von Regelkomponente, die definiert, was passieren soll, nachdem ein Ereignis auftritt und Bedingungen ausgewertet und übergeben werden.

**Aktivieren**: Activate ist die Aktion, die ein Benutzer durchführt, um ein Segment oder Profile einem Ziel zuzuordnen, z. B. [!DNL Oracle Eloqua], [!DNL Google]oder [!DNL Salesforce Marketing Cloud].

**Aktivität**: In [!DNL Offer Decisioning], enthält eine Aktivität die Logik, die über die Auswahl eines Angebots informiert.

**Administrator**: Eine oder mehrere Personen in Ihrem Unternehmen, die Berechtigungen für die Experience Platform in Adobe Admin Console konfigurieren und anpassen können.

**Adobe Admin Console**: Adobe Admin Console bietet einen zentralen Speicherort für die Verwaltung der Produktberechtigungen und den Zugriff auf Adobe für Ihr Unternehmen. Über die Konsole können Administratoren Benutzergruppen Zugriffsberechtigungen für verschiedene Platform-Funktionen erteilen, z. B. &quot;Datensätze verwalten&quot;, &quot;Datensätze anzeigen&quot;oder &quot;Profile verwalten&quot;.

**Adobe Experience Platform**: Adobe Experience Platform standardisiert Daten und Inhalte im gesamten Unternehmen, ermöglicht Echtzeit-Kundenprofile, ermöglicht Datenwissenschaft und beschleunigt Content Velocity, um die Personalisierung von Erlebnissen auf der gesamten Journey zu fördern.

**Adobe Experience Platform Query Service**: Ermöglicht es Datenanalysten, Ereignisse und Profile zur Verwendung in Analysen und maschinellem Lernen abzufragen. Mit Query Service können Datenwissenschaftler und Analytiker alle in Experience Platform gespeicherten Datensätze abrufen (einschließlich Verhaltensdaten sowie Point-of-Sale (POS), Customer Relationship Management (CRM) usw.) und diese Datensätze abfragen, um spezifische Fragen zu den Daten zu beantworten.

**Adobe Experience Platform-Segmentierungsdienst**: Ermöglicht das Erstellen von Segmenten und das Generieren von Zielgruppen aus Ihren Echtzeit-Kundenprofildaten. Diese Zielgruppen können dann in ihre eigenen Datensätze im Data Lake exportiert werden.

**Adobe Intelligent Services**: Intelligente Dienste wie Attribution AI und Customer AI sind auf maschinellem Lernen basierende, auf künstlicher Intelligenz basierende Modelle, die speziell entwickelt wurden und Experience Platform zum Ausführen und Betrieb erfordern.

**Adobe I/O**: Adobe I/O ist Teil der Experience Platform und bietet Zugriff auf alles, was Entwickler zur Integration, Erweiterung und Anpassung von Platform benötigen, einschließlich APIs, Ereignissen, Entwicklerkonsole und hilfreicher Tools.

**Adobe Sensei**: Adobe Sensei ist das intelligente Framework, das Experience Platform steuert. Es bietet außerdem eine Reihe von KI-Diensten, mit denen Marken ihre Fähigkeit verbessern können, personalisierte Echtzeit-Kundenerlebnisse bereitzustellen.

**Amazon S3-Bucket**: [!DNL Amazon S3] -Behälter sind die grundlegenden Container für Daten, die in der [!DNL Amazon] Ökosystem. Buckets enthalten Objekte. Jedes Objekt wird mit einem eindeutigen Schlüssel gespeichert und abgerufen, der dem Entwickler zugewiesen ist.

**Amazon S3-Connector**: Die [!DNL Amazon] Mit dem S3-Connector können Kunden von Experience Platform sicher eine Verbindung herstellen und auf ihre [!DNL Amazon] S3-Daten.

**Speicherstrategie anhängen**: Die Speicherstrategie &quot;Anhängen&quot;ist eine Option, die verwendet wird, wenn Daten von Drittanbietern spezifiziert werden, die über eine Verbindung aufgenommen werden sollen, und neue Daten oder Zeilen am Ende des Datensatzes angehängt werden. Die zuvor erfassten Zeilen bleiben unberührt und nur Zeilen, die seit der letzten geplanten Ausführung erstellt wurden, werden in Experience Platform aufgenommen. Alle Zeilen, die im Quellsystem geändert wurden, bleiben bei der Experience Platform unverändert.

**Array**: Arrays werden für geordnete Elemente mit demselben Datentyp verwendet.

**Künstliche Intelligenz**: Künstliche Intelligenz ist eine Theorie und Entwicklung von Computersystemen, die in der Lage sind, Aufgaben auszuführen, die normalerweise menschliche Intelligenz erfordern, wie visuelle Wahrnehmung, Spracherkennung, Entscheidungsfindung und Übersetzung zwischen Sprachen.

**Attribute**: Attribute sind bestimmte Eigenschaften, die ein Profil darstellen.

**Attributzusammenführung**: Wenn Sie eine Zusammenführungsrichtlinie mithilfe der Echtzeit-Kundenprofil-API definieren, wird die `attributeMerge` -Objekt gibt an, wie die Zusammenführungsrichtlinie Profilattribute bei Datenkonflikten priorisiert. Dies entspricht der Auswahl einer [!UICONTROL Zusammenführungsmethode] beim Definieren einer Zusammenführungsrichtlinie in der Platform-Benutzeroberfläche.

**Attribution AI**: [!DNL Attribution AI] ist ein intelligenter Dienst auf Basis von Adobe Sensei, der algorithmische Funktionen für die kanalübergreifende Zuordnung über den gesamten Kundenlebenszyklus hinweg bietet.

**Zielgruppe**: Eine Zielgruppe ist der resultierende Satz von Profilen, die den Kriterien einer Segmentdefinition entsprechen.

**Zielgruppengröße**: Eine Zielgruppengröße ist die Gesamtanzahl der Profile, die den Kriterien einer Segmentdefinition entsprechen und für die Zielgruppenzugehörigkeit qualifiziert sind.

**Audience-Schnappschuss**: Eine Audience-Momentaufnahme erfasst alle Profile, die zum Zeitpunkt der Segmentierung für die Segmentkriterien qualifiziert sind.

## B

**Aufstockung**: Bei geplanten Quellen ermöglicht die Aufstockungsoption die Erfassung historischer Daten.

**Aufstockungszeitraum**: Die Aufstockungszeit ist eine Option, um die Zeitdauer für die Aufnahme von historischen Daten von Drittanbietern über eine Quellverbindung festzulegen. Wenn Sie einen Aufstockungszeitraum von &quot;für immer&quot;wählen, wird der gesamte Verlauf der Quelldaten in die Experience Platform aufgenommen.

**Batch**: Ein Batch ist ein Datensatz, der über einen bestimmten Zeitraum erfasst und als Einheit verarbeitet wird. Datensätze bestehen aus mehreren Batches.

**Batch-Kennung**: Eine Batch-Kennung ist eine von Adoben generierte Kennung für einen DatenBatch.

**Batch-Erfassung**: Mit der Batch-Erfassung können Sie Daten als Batch-Dateien in Experience Platform erfassen. Batches sind Dateneinheiten aus einer oder mehreren Dateien, die als Ganzes aufgenommen werden.

**Batch-Segmentierung**: Die Batch-Segmentierung ist eine Alternative zu einem kontinuierlichen Datenauswahlprozess und verschiebt alle Profildaten gleichzeitig durch Segmentdefinitionen, um entsprechende Zielgruppen zu erstellen. Nach der Erstellung wird dieses Segment gespeichert, sodass es zur Verwendung exportiert werden kann.

**Build**: Im Kontext von Tags ist ein Build eine Datei bzw. ein Dateisatz, die bzw. der alle Konfigurationen und den Code enthält, die zum Ausführen der in einer Bibliothek enthaltenen Geschäftslogik erforderlich sind, sodass Sie diese Bibliothek auf Ihrer Website oder in Ihrer mobilen App bereitstellen können.

**Business Intelligence-Tools**: Business Intelligence-Tools (BI) sind in erster Linie mit [!DNL Experience Platform Query Service]. BI-Tools sind Typen von Anwendungs-Software, die große Mengen unstrukturierter Daten aus internen und externen Systemen erfassen und verarbeiten.

## C

**Begrenzung**: In [!DNL Offer Decisioning], wird in Entscheidungsregeln eine Begrenzung (auch als Frequenzlimitierung bezeichnet) verwendet, um festzulegen, wie oft ein Angebot angezeigt wird. Es gibt zwei Arten von Begrenzungen: wie oft ein Angebot für die kombinierte Zielgruppe vorgeschlagen werden kann (als &quot;globale Begrenzung&quot;bezeichnet) und wie oft ein Angebot demselben Endbenutzer vorgeschlagen werden kann (als &quot;Profilbegrenzung&quot;bezeichnet).

**Katalog**: Im Zusammenhang mit Quellen und Zielen ist ein Katalog eine Galerie mit verfügbaren Verbindungen zu Adobe-Applikationen und Drittanbietertechnologien. Nicht zu verwechseln mit [!DNL Catalog Service].

**[!DNL Catalog Service]**: [!DNL Catalog Service] (manchmal genannt [!DNL Catalog]) ist das Aufzeichnungssystem für Speicherort und Herkunft von Daten in Adobe Experience Platform. Während alle Daten, die in Experience Platform aufgenommen werden, im Data Lake als Dateien und Ordner gespeichert werden, [!DNL Catalog] enthält die Metadaten und die Beschreibung dieser Dateien und Ordner für Such-, Überwachungs- und Data-Governance-Zwecke.

**Klasse**: Im Experience-Datenmodell (XDM) definiert eine Klasse den kleinsten Satz von Feldern, die zum Erstellen eines Schemas verwendet werden, und definiert das Basisverhalten des Geschäftsobjekts, das das Schema darstellt.

**Client**: Ein Client ist ein externes Tool oder eine externe Anwendung, die eine Verbindung zu [!DNL Query Service] über das PostgreSQL-Protokoll oder die HTTP-API.

**Sammlung**: In [!DNL Offer Decisioning], sind Kollektionen Untergruppen von Angeboten, die auf von einem Marketing-Experten vordefinierten Bedingungen basieren, z. B. der Kategorie des Angebots.

**Kombinieren mit PII-Marketing-Aktion**: Eine Marketing-Aktion, die alle personenbezogenen Daten (PII) mit anonymen Daten kombiniert. Verträge über Daten, die aus Werbenetzwerken, Werbe-Servern und Drittanbietern von Daten bezogen werden, beinhalten häufig spezifische vertragliche Verbote der Verwendung solcher Daten mit direkt identifizierbaren Daten.

**Befehlszeilenschnittstelle**: Eine Befehlszeilenschnittstelle ist ein textbasiertes Tool, mit dem eine Verbindung hergestellt werden kann [!DNL Query Service] für die Ausführung der Rohabfrage.

**Komposition**: Eine Komposition ist eine Gruppierung von Komponenten, die sich zusammenbilden, um das Schema zu bilden.

**Bedingung**: Im Kontext von Tags ist eine Bedingung eine Regelkomponente, die eine logische Anweisung auswertet, die `true` oder `false`. Alle Bedingungen müssen ausgewertet werden `true` und alle Ausnahmebedingungen `false` bevor Aktionen auf der Regel ausgeführt werden.

**Konsole**: In [!DNL Query Service], stellt die Konsole Informationen zum Status und Vorgang einer Abfrage bereit. Die Konsole zeigt den Verbindungsstatus an [!DNL Query Service], und alle Fehlermeldungen, die aus diesen Abfragen resultieren.

**Vertragsbezeichnungen (&quot;C&quot;)**: Datennutzungsbezeichnungen (&quot;Contract&quot;) werden verwendet, um Daten zu kategorisieren, die vertragliche Verpflichtungen haben oder mit den Data Governance-Richtlinien eines Kunden in Zusammenhang stehen.

**C1-Vertragsbezeichnung**: A `C1` Beschriftung für die vertragliche Datennutzung gibt an, dass Daten nur in aggregierter Form aus Adobe Experience Cloud exportiert werden können, ohne dass eine Einzel- oder Gerätekennung enthalten ist. Zum Beispiel Daten, die aus Social Media stammen.

**C2-Vertragsbezeichnung**: A `C2` Die Beschriftung der vertraglichen Datennutzung gibt Daten an, die nicht an einen Drittanbieter exportiert werden können. Einige Datenanbieter haben in ihren Verträgen Klauseln, die den Export von Daten von dort verbieten, wo sie ursprünglich erfasst wurden. Beispielsweise wird die Übertragung von Daten, die Sie von sozialen Netzwerken erhalten, häufig durch Verträge beschränkt. C2 ist restriktiver als C1, was nur Aggregation und anonyme Daten erfordert.

**C3-Vertragsbezeichnung**: A `C3` Die Beschriftung der vertraglichen Datennutzung gibt Daten an, die nicht mit direkt identifizierbaren Informationen kombiniert oder anderweitig verwendet werden können. Einige Datenanbieter haben Vertragsklauseln, die die Kombination oder Verwendung dieser Daten mit direkt identifizierbaren Informationen verbieten. Verträge für Daten, die aus Werbenetzwerken, Werbeservern und Drittanbietern von Daten stammen, enthalten häufig spezifische vertragliche Verbote der Verwendung direkt identifizierbarer Daten.

**C4-Vertragsbezeichnung**: A `C4` Der Titel der Datennutzung gibt an, dass Daten nicht für das Targeting von Anzeigen oder Inhalten verwendet werden können, weder auf der Site noch auf der Site. C4 ist die restriktivste Bezeichnung, da sie C5-, C6- und C7-Beschriftungen umfasst.

**C5-Vertragsbezeichnung**: A `C5` Beschriftung für die Nutzung von Vertragsdaten gibt an, dass Daten nicht für das Site-übergreifende Targeting von interessenbasierten Inhalten oder Anzeigen verwendet werden können. Eine interessensbasierte Zielgruppenbestimmung oder Personalisierung tritt auf, wenn die folgenden drei Bedingungen erfüllt sind: Die vor Ort erfassten Daten dienen dazu, Rückschlüsse auf das Interesse eines Benutzers zu ziehen. wird in einem anderen Kontext wie auf einer anderen Site oder App verwendet; und wird verwendet, um anhand dieser Rückschlüsse festzulegen, welche Inhalte oder Anzeigen bereitgestellt werden.

**C6 Vertragsbezeichnung**: A `C6` Die Beschriftung der Vertragsdaten gibt an, dass Daten nicht für das On-site-Anzeigen-Targeting verwendet werden können. Das On-site-Anzeigen-Targeting umfasst die Auswahl und Bereitstellung von Werbung auf den Websites oder Apps Ihres Unternehmens oder zur Messung der Bereitstellung und Effektivität solcher Werbung. Dazu gehört die Verwendung zuvor erfasster Onsite-Daten über das Interesse der Benutzer an der Auswahl von Anzeigen, die Verarbeitung von Daten darüber, welche Anzeigen angezeigt wurden, wann und wo sie angezeigt wurden und ob die Benutzer im Zusammenhang mit der Anzeige irgendwelche Maßnahmen ergriffen haben, z. B. die Auswahl einer Anzeige oder den Kauf.

**C7-Vertragsbezeichnung**: A `C7` Die Beschriftung der vertraglichen Datennutzung gibt an, dass Daten nicht für das On-site-Targeting von Inhalten verwendet werden können. Das Targeting von Inhalten auf der Site umfasst die Auswahl und Bereitstellung von Inhalten auf den Websites Ihrer Organisation oder in Apps oder die Messung der Bereitstellung und Effektivität solcher Inhalte. Dazu gehören zuvor erfasste Informationen über das Interesse der Benutzer an der Auswahl von Inhalten, die Verarbeitung von Daten darüber, welcher Inhalt angezeigt wurde, wie oft oder wie lange er angezeigt wurde, wann und wo er angezeigt wurde und ob die Verwendungszwecke Aktionen im Zusammenhang mit dem Inhalt durchgeführt haben, einschließlich der Auswahl von Inhalten.

**C8-Vertragsbezeichnung**: A `C8` Beschriftung der vertraglichen Datennutzung gibt an, dass Daten nicht zur Messung der Websites oder Apps Ihres Unternehmens verwendet werden können. Dies umfasst nicht das zielgerichtete Targeting, d. h. die Sammlung von Informationen über Ihre Nutzung dieses Dienstes, um Inhalte und/oder Werbung in anderen Kontexten zu personalisieren.

**C9-Vertragsbezeichnung**: A `C9` Die Beschriftung der vertraglichen Datennutzung gibt an, dass Daten nicht in datenwissenschaftlichen Workflows verwendet werden können. Einige Verträge beinhalten ausdrücklich Verbote von Daten, die für die Datenwissenschaft verwendet werden. Manchmal werden diese Begriffe so formuliert, dass die Verwendung von Daten für künstliche Intelligenz (KI), maschinelles Lernen (ML) oder Modellierung verboten ist.

**C10-Vertragsbezeichnung**: A `C10` Beschriftung für die Verwendung von Vertragsdaten gibt an, dass Daten nicht für die Aktivierung der verknüpften Identität verwendet werden können. Einige Datennutzungsrichtlinien beschränken die Verwendung von zusammengesetzten Identitätsdaten für die Personalisierung. Die `C10` wird automatisch auf Segmente angewendet, wenn deren Zusammenführungsrichtlinien die Option &quot;Privates Diagramm&quot;verwenden.

**Spalte &quot;Erstellungsdatum&quot;**: Die Auswahl der Spalte Erstellungsdatum ist eine Option bei der Angabe von Drittanbieterdaten über eine Quellverbindung. Wenn die Speicherstrategie anhängen ausgewählt ist und das Datensatzschema mehrere Datumsfelder enthält, müssen Sie aus dem verfügbaren Schema auswählen, um eine Schlüsselspalte Erstellungsdatum anzugeben. Die Option Erstellungsdatum ist nicht verfügbar, wenn die Speicherstrategie zum Überschreiben ausgewählt ist.

**Tabelle erstellen als Auswahl**: &quot;Tabelle als Auswahl erstellen&quot;(CTAS) ist ein SQL-Befehl, der bei Ausführung im Rahmen einer vollständigen und gültigen SQL-Abfrage anweist, [!DNL Query Service] , um die Ergebnisse der Abfrage in einem Datensatz zu speichern. Sie können einen neuen Ergebnissatz erstellen, frühere Ergebnisse überschreiben oder an vorherige Ergebnisse anhängen.

**Site-übergreifende Daten**: Site-übergreifende Daten sind eine Kombination von Daten aus verschiedenen Sites, einschließlich einer Kombination aus Vor-Ort-Daten und Offsite-Daten oder einer Kombination von Daten aus verschiedenen Offsite-Quellen.

**Site-übergreifende Targeting-Marketing-Aktion**: Eine Marketing-Aktion, die Daten für Site-übergreifendes Anzeigen-Targeting verwendet. Die Kombination von Daten aus verschiedenen Sites, einschließlich einer Kombination aus Daten in einer Site und Offsite-Daten oder einer Kombination von Daten aus verschiedenen Offsite-Quellen, wird als „Site-übergreifende Daten“ bezeichnet. Site-übergreifende Daten werden in der Regel erfasst und verarbeitet, um Rückschlüsse auf die Interessen der Kunden zu ziehen.

**Benutzerdefinierter Identitäts-Namespace**: Benutzerdefinierte Identitäts-Namespaces können von Ihrer Organisation erstellt werden, um Identitäten für eine bestimmte Organisation oder einen bestimmten Geschäftsfall darzustellen.

**Benutzerdefinierte Beschriftungen**: Mit benutzerdefinierten Datennutzungsbezeichnungen können Sie spezifische Bezeichnungen erstellen und auf Datenfelder anwenden, die bestimmten Geschäftsanforderungen entsprechen.

**Customer AI**: Customer AI ist ein auf Adobe Sensei basierender intelligenter Dienst, der Kundenprofile mit KI-basierten Eigenschaften anreichert und die Kundensegmentierung und Zielgruppenbestimmung ermöglicht.

## D

**Täglich**: Im Rahmen geplanter Dateiexporte werden vollständige oder inkrementelle Dateiexporte einmal täglich vom Startdatum bis zum Enddatum zu dem vom Benutzer angegebenen Zeitpunkt geplant.

**Datenwörterbuch**: Im Kontext von Tags ist ein Datenwörterbuch (auch als Datenkarte bezeichnet) ein Satz von Datenelementen, die in einer Eigenschaft definiert sind.

**Datenelement**: Im Kontext von Tags ist ein Datenelement ein Zeiger, der in Regeln und Erweiterungen verwendet wird, um auf ein bestimmtes Datenelement zu verweisen, das auf dem Client-Gerät vorhanden ist.

**Datenerfassung**: Bei der Datenerfassung werden Daten aus einer Quelle zur Experience Platform hinzugefügt. Daten können auf verschiedene Weise in Platform erfasst werden, einschließlich Streaming, Batches oder Hinzufügen über Quell-Connectoren.

**Datenschicht**: Im Kontext von Tags ist eine Datenschicht eine Datenstruktur, die auf dem Client-Gerät vorhanden ist und Metadaten zum Kontext enthält, in dem eine Seite oder ein Bildschirm angezeigt wird.

**Data Governance**: Data Governance umfasst die Strategien und Technologien, mit denen sichergestellt wird, dass die Daten im Hinblick auf die Datennutzung den Vorschriften und organisatorischen Richtlinien entsprechen.

**Datenintegrationspartner**: Datenintegrationspartner vereinfachen und automatisieren das Laden und die Transformation massiver Datenmengen von über 200 Datenquellen in die Experience Platform, ohne Code schreiben zu müssen.

**Datensatzbezeichnungen**: Datennutzungsbezeichnungen können Datensätzen hinzugefügt werden. Alle Felder in diesem Datensatz übernehmen die Bezeichnungen des Datensatzes.

**Data Science Workspace**: [!DNL Data Science Workspace] innerhalb von Experience Platform können Kunden Modelle für maschinelles Lernen erstellen, die Daten aus Platform- und Adobe-Anwendungen nutzen, um intelligente  zu erstellen, Einblicke zu generieren und Prognosen bereitzustellen, sodass Sie digitale Erlebnisse für Endbenutzer deutlich verbessern können.

**Datenquelle**: Eine Datenquelle ist eine vom Benutzer festgelegte Quelle der Daten. Beispiele für eine Datenquelle sind eine mobile App, Profil- und/oder Erlebnisereignisse, Website-Profilereignisse oder ein CRM.

**Data Steward**: Ein Data Steward ist die Person, die für die Verwaltung, Überwachung und Durchsetzung der Daten-Assets einer Organisation verantwortlich ist. Ein Data Steward stellt außerdem sicher, dass Data Governance-Richtlinien geschützt und gepflegt werden, um mit staatlichen Vorschriften und organisatorischen Richtlinien konform zu sein.

**Datenstrom**: Ein Datenstrom ist ein Satz oder eine Sammlung von Nachrichten, die dasselbe Schema aufweisen und von derselben Quelle gesendet werden.

**Datentyp**: Ein Datentyp ist eine wiederverwendbare XDM-Ressource, die ein Objekt-Typ-Feld definiert, das mehrere Eigenschaften in einer hierarchischen Darstellung enthält.

**Datennutzungsbezeichnungen**: Mit Datennutzungsbezeichnungen können Sie Daten kategorisieren, die datenschutzbezogene Aspekte und vertragliche Bedingungen berücksichtigen, um Vorschriften und Unternehmensrichtlinien zu erfüllen. Datennutzungsbezeichnungen, die einem Datensatz hinzugefügt werden, werden vererbt oder auf alle Felder in diesem Datensatz angewendet. Datennutzungsbezeichnungen können auch direkt auf Felder angewendet werden.

**Dataflow**: Ein Datenfluss ist eine virtuelle Pipeline von Daten, die von einer Quelle an Platform und an Ziele gesendet werden.

**Datenfluss**: Ein Datenfluss ist ein Datenfluss, der auf Grundlage eines vom Benutzer festgelegten Zeitplans in der Experience Platform landet.

**Datensatz**: Ein Datensatz ist ein Speicher- und Verwaltungskonstrukt für eine Sammlung von Daten, normalerweise eine Tabelle, die ein Schema (Spalten) und Felder (Zeilen) enthält.

**Datensatz-ID**: Eine von der Adobe generierte Kennung für einen erfassten Datensatz.

**Datensatzausgabe**: Die Datensatzausgabe bietet einen Mechanismus, um zu bestimmen, welche Option &quot;Tabelle als Auswahl erstellen&quot;für eine bestimmte [!DNL Query Service] ausführen.

**Deduplizierungsschlüssel**: Ein benutzerdefinierter Primärschlüssel, der die Identität bestimmt, anhand derer Benutzer ihre Profile deduplizieren möchten. &#x200B;

**Delta-Spalte**: In einer Delta-Spalte können Sie ein Quelldatenfeld auswählen, das einen Zeitstempel für die inkrementelle Erfassung darstellt.

**Delta-Speicherstrategie**: Die Delta-Speicherstrategie ist eine Option zur Aufnahme von Drittanbieterdaten über eine Quellverbindung. Mit dieser Option kann der Benutzer angeben, dass neue oder geänderte Zeilen von Quelldaten in Experience Platform aufgenommen werden. Am Ende des Datensatzes werden neue Zeilen hinzugefügt und geänderte Zeilen werden im Datensatz bei der Experience Platform aktualisiert.

**Deskriptor**: Im Experience-Datenmodell (XDM) ist ein Deskriptor ein zusätzlicher Satz von schemabezogenen Metadaten, der ein bestimmtes Verhalten für ein Feld beschreibt. Deskriptoren können von Experience Platform verwendet werden, um das beabsichtigte Schemaverhalten zu verstehen, z. B. die Beziehung zwischen zwei Schemas.

**Ziel**: Ein Ziel ist ein allgemeiner Begriff für jeden Endpunkt, z. B. eine Adobe App, eine Werbeplattform, einen Cloud-Speicher-Dienst oder einen Marketing-Dienst, bei dem eine Zielgruppe aktiviert und bereitgestellt wird.

**Zielkategorie**: Eine Zielkategorie ist eine Gruppierung von Zielen mit ähnlichen Merkmalen.

**Zielkatalog**: Ein Zielkatalog ist eine Liste der verfügbaren Ziele in Experience Platform.

**Direktaufrufregeln**: Im Kontext von Tags ist eine Direktaufrufregel eine Regel, die ausgeführt wird, wenn sie direkt von der Seite aus aufgerufen wird, wobei Ereigniserkennungs- und Suchsysteme umgangen werden.

**Anzeigename**: Im Experience-Datenmodell (XDM) ist ein Anzeigename ein benutzerfreundlicher Name für ein Feld, der in der Benutzeroberfläche angezeigt wird.

## E

**Geeignetes Angebot**: Ein geeignetes Angebot kann einem Profil konsistent angeboten werden, da es die zuvor definierten Bedingungen erfüllt.

**Eignungsregeln**: In [!DNL Offer Decisioning], werden die Eignungsregeln auf ein Profil angewendet, das mit Kalender-, Zeitplan- und Begrenzungsbegrenzungen verbunden ist.

**Marketing-Aktion für E-Mail-Targeting**: Eine Marketing-Aktion, die Daten in E-Mail-Targeting-Kampagnen verwendet.

**Einbettungscode**: Im Kontext von Tags ist der Einbettungscode ein Skript-Tag, das auf einer Site oder Umgebung auf der HTML platziert wird. Der Einbettungscode weist den Browser an, wo der Build abgerufen werden soll.

**Auflistung**: Eine Auflistung (Enum) ist ein XDM-Feld, das auf einen Satz vordefinierter Werte beschränkt ist.

**Umgebung**: Im Kontext von Tags ist eine Umgebung ein Satz von Bereitstellungsanweisungen, die die Host-Bereitstellung und das Dateiformat eines Builds angeben. Eine Bibliothek muss mit einer Umgebung gepaart werden, bevor sie erstellt werden kann.

**Fehlerdiagnose**: Die Fehlerdiagnose ermöglicht die Erstellung detaillierter Fehlermeldungen für aufgenommene Batches. Mit dem Fehlerschwellenwert können Sie den Prozentsatz der akzeptablen Fehler konfigurieren, bevor ein Batch fehlschlägt.

**Ereignis**: Im Kontext von Tags ist ein Ereignis ein bestimmter Regeltyp, d. h. ein Trigger, der auf einem Client-Gerät auftritt, um die Ausführung einer Regel zu starten.

**Ereignisentitäten**: Im Rahmen der Datenmodellierung stellen Ereignisentitäten Konzepte dar, die sich auf Aktionen beziehen, die ein Kunde ausführen kann, Systemereignisse oder andere Konzepte, bei denen Sie Änderungen im Zeitverlauf verfolgen möchten. Stellen, die unter diese Kategorie fallen, sollten anhand der [!DNL XDM ExperienceEvent] -Klasse.

**Veranstaltungen**: Ereignisse sind die mit einem Profil verknüpften Verhaltensdaten.

**Experience-Datenmodell (XDM)** [!DNL Experience Data Model] (XDM) ist ein Open-Source-Framework, das Standardschemata verwendet, um Daten für die Verwendung mit Experience Platform- und Adobe Experience Cloud-Anwendungen zu vereinheitlichen. XDM standardisiert, wie Daten strukturiert sind, beschleunigt und vereinfacht den Prozess, Erkenntnisse aus massiven Datenmengen zu gewinnen.

**Experiment**: Bei einem Experiment wird ein trainiertes Modell erstellt, indem die Instanz mit einem Beispielabschnitt der Live-Produktionsdaten trainiert wird. Dies unterscheidet sich von einem trainierten Modell, das mit einem Holdout-Testdatensatz getestet wird. Dies unterscheidet sich auch vom Konzept eines Experiments in einigen Rahmen des maschinellen Lernens, bei dem es sich tatsächlich um ein Beispiel-Modellierungsprojekt handelt.

**Erlebnisereignis**: Ein Erlebnisereignis stellt eine Momentaufnahme des Systems dar, wenn eine Interaktion oder ein Ereignis im Zusammenhang mit einem Kundenerlebnis stattfindet. Erlebnisereignisse sind unveränderliche Tatsacheneinträge darüber, was passiert ist, und stellen dar, was ohne Aggregation oder Interpretation passiert ist. Im Experience-Datenmodell (XDM) wird dieses Konzept von der [!DNL XDM ExperienceEvent] -Klasse.

**Gesamte Datei exportieren**: Eine Exportdatei mit einer vollständigen Momentaufnahme aller Profilqualifikationen für das ausgewählte Segment.

**Inkrementelle Dateien exportieren**: Eine Reihe exportierter Dateien, bei denen die erste Datei eine vollständige Momentaufnahme aller Profilqualifikationen für das ausgewählte Segment darstellt und nachfolgende Dateien seit dem vorherigen Export inkrementelle Profilqualifikationen sind.

**Erweiterung**: Im Kontext von Tags ist eine Erweiterung ein Funktionspaket, das einer Tag-Eigenschaft hinzugefügt wird. Eine Erweiterung konzentriert sich in der Regel auf eine bestimmte Marketing- oder Analyselösung und bietet die Tools, die zum Bereitstellen dieser Technologie in einer Client-Umgebung erforderlich sind.

**Erweiterungspaket**: Im Kontext von Tags ist ein Erweiterungspaket eine ZIP-Datei, die von einem Erweiterungsentwickler erstellt und hochgeladen wurde und alle erforderlichen Informationen für Tags bereitstellt, damit Benutzer die Erweiterung in ihrer Eigenschaft installieren können. Ein Erweiterungspaket enthält ein Manifest, das Informationen über die Erweiterung, das HTML/JavaScript, das zum Konfigurieren des Verhaltens der Tag-Erweiterung erforderlich ist, und das ausführbare JavaScript, das an die Client-Umgebung gesendet wird (falls erforderlich).

## F

**Fallback-Angebote**: Ein Fallback-Angebot ist das Standardangebot, das angezeigt wird, wenn ein Endbenutzer für keines der Angebote in der verwendeten Kollektion geeignet ist.

**Funktionszuordnung**: Die Funktionszuordnung bezieht sich auf den Prozess der Zuordnung von Funktionen aus Daten zu Eingabe- und Zielfunktionen, die für ein Modell für maschinelles Lernen erforderlich sind.

**Feld**: Ein Feld ist das Element der niedrigsten Ebene eines Datensatzes, wie durch das XDM-Schema des Datensatzes definiert. Jedes Feld hat einen Namen für Verweiszwecke und einen Typ, der den darin enthaltenen Datentyp angibt. Feldtypen können Ganzzahlen, Zahlen, Zeichenfolgen, boolesche Werte und Objekte enthalten (sind jedoch nicht darauf beschränkt).

**Feldergruppe**: Siehe &quot;Schemafeldgruppe&quot;.

**Feldtitel**: Feldbezeichnungen sind Data Governance-Bezeichnungen, die entweder von einem Datensatz übernommen oder direkt auf ein Feld angewendet werden.

**Feldname**: Ein Feldname wird verwendet, um in Abfragen und nachgelagerten Diensten auf den Wert eines Felds zu verweisen.

**Häufigkeit**: In [!DNL Query Service], bestimmt die Häufigkeit, wie oft eine wiederkehrende geplante Abfrage ausgeführt wird.

## G

**Geofence**: Eine Geofence ist eine virtuelle geografische Grenze, die durch GPS- oder RFID-Technologie definiert wird und Software in die Lage versetzt, eine Antwort Trigger, wenn ein Mobilgerät ein bestimmtes Gebiet erreicht oder verlässt.

**DSGVO (Datenschutz-Grundverordnung)**: Die Datenschutz-Grundverordnung (DSGVO) ist ein Rechtsrahmen, der Richtlinien für die Erhebung und Verarbeitung personenbezogener Daten von Personen in der Europäischen Union (EU) festlegt. Die DSGVO legt die Grundsätze für das Datenmanagement und die Rechte des Einzelnen fest und erfasst alle Unternehmen, die mit den Daten von EU-Bürgern zu tun haben.

**Schutzschilde**: Limits sind Schwellenwerte, die die Datennutzung und Systemnutzung, Leistungsoptimierung und Vermeidung von Fehlern oder unerwarteten Ergebnissen in Adobe Experience Platform unterstützen. Leitlinien können sich auf Ihre Nutzung oder Verwendung von Daten und Verarbeitung im Zusammenhang mit Ihren Lizenzierungsberechtigungen beziehen.

## H

**Host**: Im Kontext von Tags gibt ein Host den Speicherort, die Domäne und die Benutzeranmeldeinformationen an, die erforderlich sind, damit das System einen Build bereitstellen kann.

**Stündlich**: Im Rahmen geplanter Dateiexporte werden inkrementelle Dateiexporte alle 3, 6, 8 oder 12 Stunden geplant.

## I

**Identität**: Eine Identität ist eine Kennung, die einen einzelnen Kunden eindeutig darstellt, z. B. eine Cookie-ID, Geräte-ID oder E-Mail-ID.

**Identitätsfelder**: Identitätsfelder sind XDM-Felder, mit denen Informationen über einzelne Kunden aus mehreren Datenquellen zusammengeführt werden. Damit das Schema zur Verwendung im Echtzeit-Kundenprofil aktiviert werden kann, muss eine einzige primäre Identität definiert werden.

**Identitätsbezeichnungen (&quot;I&quot;)**: Datennutzungsbezeichnungen (&quot;I&quot;) dienen zur Kategorisierung von Daten, mit denen eine bestimmte Person identifiziert oder kontaktiert werden kann.

**Identitätsdiagramm**: Ein Identitätsdiagramm ist eine Zuordnung der Beziehungen zwischen zugeordneten und verknüpften Identitäten, die für einen einzelnen Kunden vorhanden sind. Jedes Identitätsdiagramm wird nahezu in Echtzeit mit Kundenaktivität aktualisiert. Die gemeinsame Struktur der Identitätsbeziehungen in Ihren Daten wird durch die [!UICONTROL Privates Diagramm], der für jedes einzelne Identitätsdiagramm als Strukturvorlage dient.

**Identitäts-Namespace**: Ein Identitäts-Namespace definiert den Kontext einer Kennung wie eine E-Mail-Adresse oder eine CRM-ID.

**Identity Service**: [!DNL Experience Platform Identity Service] ermöglicht die Erstellung und Verwaltung von Identitätstypen, sodass Sie Kundenidentitäten geräteübergreifend und kanalübergreifend verknüpfen können. Die Fähigkeit des Dienstes, Identitäten miteinander zu verknüpfen, ermöglicht es Echtzeit-Kundenprofil, eine vollständige Darstellung jedes einzelnen Kunden bereitzustellen.

**Identitätszusammenfügung**: Beim Identitätszusammenfügen werden Datenfragmente identifiziert und zu einem vollständigen Profildatensatz zusammengeführt.

**Identitätssymbol**: Ein Identitätssymbol ist eine Abkürzung für einen Identitäts-Namespace, der in APIs als Referenz verwendet werden kann.

**Identitätswert**: Ein Identitätswert, kombiniert mit einem Identitäts-Namespace, ist eine Kennung, die eine eindeutige Person, Organisation oder ein Asset darstellt. Bei der Zuordnung von Datensatzdaten zu Profilfragmenten müssen Namespace und Identitätswert übereinstimmen.

**I1-Datennutzungsbezeichnung**: Die `I1` Datennutzungsbezeichnung wird verwendet, um Daten zu klassifizieren, die direkt eine bestimmte Person und nicht ein Gerät, sondern eine bestimmte Person identifizieren oder kontaktieren können.

**I2-Datennutzungsbezeichnung**: Die `I2` Datennutzungsbezeichnung wird verwendet, um Daten zu klassifizieren, die in Kombination mit anderen Daten verwendet werden können, um eine bestimmte Person indirekt zu identifizieren oder zu kontaktieren.

**IMS-Organisation**: Eine IMS-Organisation (manchmal auch als IMS-Organisation bezeichnet) ist der Name, der zur Identifikation eines Unternehmens oder einer bestimmten Unternehmensgruppe in einem Adobe-Produkt verwendet wird. Administratoren können den Zugriff und die Berechtigungen von Funktionen für Benutzer einer Organisation konfigurieren und verwalten.

**Aufnahme**: Siehe Datenerfassung.

**Aufnahmeplan**: Ein Erfassungszeitplan bietet zeitbasierte Optionen für die Aufnahme von einer Quelle in eine Experience Platform.

**Eingabefunktion**: Eine Eingabefunktion ist in der Funktionszuordnung angegeben und wird von einem Modell für maschinelles Lernen verwendet, um Prognosen zu erstellen.

**[!DNL Intelligent Services]**: [!DNL Intelligent Services] wie [!DNL Attribution AI] und [!DNL Customer AI] sind auf maschinellem Lernen basierende, auf künstlicher Intelligenz basierende Modelle, die Experience Platform (oder auf Platform aufbauende Anwendungen wie Adobe Real-time Customer Data Platform) erfordern, um ausgeführt und betrieben zu werden.

**Interessensbasiertes Targeting oder Personalisierung**: Eine interessensbasierte Zielgruppenbestimmung, auch Personalisierung genannt, tritt auf, wenn die folgenden drei Bedingungen erfüllt sind:

1. Daten, die vor Ort erfasst werden, dienen dazu, Rückschlüsse auf das Interesse eines Benutzers zu ziehen.
1. Daten werden in einem anderen Kontext wie auf einer anderen Site oder App (außerhalb der Site) verwendet.
1. Mithilfe von Daten wird festgelegt, welche Inhalte oder Anzeigen basierend auf diesen Schlussfolgerungen bereitgestellt werden.

## J

**[!DNL JupyterLab]**: Eine Open-Source-Web-basierte Schnittstelle für das Projekt [!DNL Jupyter] in die Platform-Benutzeroberfläche integriert ist.

**[!DNL Jupyter Notebook]**: Dank der Integration mit JupyterLab können Sie mit Jupyter Notebooks Daten bereinigen und umwandeln, numerische Simulationen, statistische Modellierung, Datenvisualisierung, maschinelles Lernen und vieles mehr in Experience Platformen wie Python, Scala und PySpark durchführen.

## K

## L

**Bibliothek**: Im Kontext von Tags ist eine Bibliothek ein Satz von Geschäftslogik, die Anweisungen dazu enthält, wie sich die Tag-Bibliothek auf dem Client-Gerät verhalten sollte.

**Suchentitäten**: Im Kontext der Datenmodellierung stellen Lookup-Entitäten Konzepte dar, die sich auf eine einzelne Person beziehen, aber nicht direkt zur Identifizierung der Person verwendet werden können. Entitäten, die unter diese Kategorie fallen, sollten durch Schemas dargestellt werden, die auf benutzerdefinierten Experience-Datenmodell (XDM)-Klassen basieren.

## M

**Maschinelles Lernen (ML)**: Maschinelles Lernen ist der Studienbereich, der es Computern ermöglicht zu lernen, ohne explizit programmiert zu werden.

**Modell für maschinelles Lernen**: Ein Modell für maschinelles Lernen ist eine Instanz eines Rezepts für maschinelles Lernen, das mithilfe von historischen Daten und Konfigurationen zur Lösung eines geschäftlichen Anwendungsfalls trainiert wird. In Adobe Experience Platform Data Science Workspace werden Modelle für maschinelles Lernen als Rezepte bezeichnet.

**Obligatorisches Attribut**: Ein benutzeraktiviertes Kontrollkästchen, mit dem sichergestellt wird, dass alle Profildatensätze das ausgewählte Attribut enthalten. Beispiel: alle exportierten Profile eine E-Mail-Adresse enthalten.

**Zuordnung**: Beim Daten-Mapping werden Quelldatenfelder den zugehörigen Zielfeldern in einem Ziel zugeordnet.

**Marketing-Aktion**: Im Data Governance-Framework ist eine Marketing-Aktion (auch als Marketing-Anwendungsfall bezeichnet) eine Aktion, die ein Datennutzer von Experience Platform durchführt und bei der geprüft werden muss, ob gegen Datennutzungsrichtlinien verstoßen wurde.

**Zusammenführungsmethode**: Beim Definieren einer Zusammenführungsrichtlinie mithilfe der Platform-Benutzeroberfläche gibt die Zusammenführungsmethode an, wie Datenfragmente bei einem Konflikt priorisiert werden sollen. Bei Verwendung der Echtzeit-Kundenprofil-API zur Definition einer Zusammenführungsrichtlinie wird die Zusammenführungsmethode mithilfe der `attributeMerge` -Objekt.

**Zusammenführungsrichtlinie**: Zusammenführungsrichtlinien sind Regeln, mit denen Experience Platform bestimmt, wie Kundendatenfragmente aus mehreren Quellen kombiniert werden, um ein einzelnes Profil zu erstellen. Wenn ein Datenkonflikt auftritt, bestimmt die Zusammenführungsrichtlinie, welche Daten für die Aufnahme in das Profil priorisiert werden sollen.

**Mixin**: Siehe &quot;Schemafeldgruppe&quot;.

**Modul**: Im Kontext von Tags ist ein Modul ein von einer Erweiterung bereitgestelltes ausführbares JavaScript-Snippet, das Aktionen in einer Client-Umgebung ausführt, ohne eine Regel erstellen zu müssen.

## N

**Nicht-Produktions-Sandbox**: Nicht-Produktions-Sandboxes sind Sandboxes, die normalerweise für Entwicklungsexperimente, Tests oder Versuche verwendet werden. Im Gegensatz zu Produktions-Sandboxes können Nicht-Produktions-Sandboxes zurückgesetzt und gelöscht werden.

**[!DNL Notebooks]**: [!DNL Notebooks] werden mithilfe von [!DNL Jupyter Notebook] und kann zur Datenanalyse ausgeführt werden.

## O

**Angebot**: Ein Angebot ist eine Marketing-Botschaft, die einem (potenziellen) Kunden ein Geschäfts- oder Verkaufsprojekt enthält. Angebote verfügen oft über spezifische Regeln, die bestimmen, wer sie sehen oder empfangen darf.

**[!DNL Offer Decisioning]**: [!DNL Offer Decisioning] ermöglicht es Marketing-Experten, Regeln und trainierte Modelle von Angebotsvorschlägen zu verwalten, wenn sie mit Endbenutzern auf der Grundlage von Daten interagieren, die über Kanäle und Anwendungen hinweg erfasst wurden.

**Angebotsbibliothek**: Die Angebotsbibliothek ist eine zentrale Bibliothek, die zur Verwaltung von personalisierten Angeboten und Fallback-Angeboten, Entscheidungsregeln und Aktivitäten verwendet wird.

**Marketing-Aktion für Personalisierung vor Ort**: Eine Marketing-Aktion, die Daten für die Personalisierung von Inhalten auf der Site verwendet. Bei der On-site-Personalisierung handelt es sich um Daten, die dazu dienen, Rückschlüsse auf die Interessen der Benutzer zu ziehen, und anhand derer anhand dieser Rückschlüsse ausgewählt wird, welche Inhalte oder Anzeigen bereitgestellt werden.

**Marketing-Aktion für On-site-Targeting**: Eine Marketing-Aktion, bei der Daten für On-site-Anzeigen verwendet werden, einschließlich der Auswahl und Bereitstellung von Werbung auf den Websites oder Apps Ihres Unternehmens, oder um die Bereitstellung und Effektivität solcher Werbung zu messen.

**Einmal**: Im Zusammenhang mit geplanten Dateiexporten wird ein einmaliger, bedarfsorientierter vollständiger Dateiexport geplant.

**Speicherstrategie überschreiben**: Die Speicherstrategie &quot;Überschreiben&quot;ist eine Option zur Aufnahme von Drittanbieterdaten über eine Verbindung, bei der Sie angeben können, ob erfasste Daten in einem bestimmten Zeitplan überschrieben werden.

## P

**Partielle Erfassung**: Die partielle Erfassung ermöglicht die Erfassung gültiger Datensätze von Batch-Daten innerhalb eines festgelegten Fehlerschwellenwerts. Die Fehlerdiagnose für fehlgeschlagene Datensätze kann heruntergeladen oder unter [!UICONTROL Überwachung] oder [!UICONTROL Quellen] Übersicht über die Ausführung des Datenflusses.

**Parquet-Dateien**: Eine Parquet-Datei ist ein Spaltenspeicherdateiformat mit komplexen verschachtelten Datenstrukturen. Parquet-Dateien sind erforderlich, um Daten zum Ausfüllen eines Schemadatasets hinzuzufügen.

**Personalisierte Angebote**: Ein personalisiertes Angebot ist eine anpassbare Marketing-Botschaft, die auf Eignungsregeln und Einschränkungen basiert.

**Platzierung**: Eine Platzierung ist der Ort und/oder Kontext, in dem ein Angebot für einen Endnutzer erscheint.

**Arbeitsbereich &quot;Richtlinien&quot;**: Ein Arbeitsbereich in der Platform-Benutzeroberfläche, über den Data Stewards Datennutzungsbezeichnungen und -richtlinien für Ihr Unternehmen anzeigen und verwalten können.

**Politik**: Eine Datennutzungsrichtlinie ist eine Regel, die Marketing-Aktionen angibt, die auf der Anwendung von Nutzungsbezeichnungen basieren, die auf Platform-Daten angewendet werden.

**Durchsetzung von Richtlinien**: Ermöglicht die Durchsetzung von Datennutzungsrichtlinien mit angewandten Marketing-Aktionen, um Datenvorgänge zu verhindern, die Richtlinienverletzungen innerhalb eines Unternehmens darstellen.

**Primärer Schlüssel**: Ein Primärschlüssel ist eine Bezeichnung in einem Schema zur eindeutigen Identifizierung aller Datensätze.

**Priorität**: In [!DNL Offer Decisioning], wird Priorität verwendet, um Angebote zu sortieren, die alle Einschränkungen erfüllen, wie Eignung, Kalender und Begrenzung.

**Private Identitätsdiagramm**: Das private Identitätsdiagramm (manchmal auch als privates Diagramm bezeichnet) ist eine private Zuordnung von Beziehungen zwischen zugeordneten und verknüpften Identitäten, die auf Ihren Erstanbieterdaten basiert und nur von Ihrer Organisation sichtbar ist. Für jede Organisation existiert nur ein privates Diagramm. Es dient als struktureller Entwurf für die individuellen Identitätsdiagramme, die für jeden Kunden erstellt werden, der mit Ihrer Marke interagiert.

**Produktprofil**: Mit Produktprofilen können Administratoren allen oder einer Untergruppe von Diensten, die mit der Experience Platform verknüpft sind, Benutzerzugriff gewähren.

**Produktions-Sandbox**: Eine Produktions-Sandbox ist eine Sandbox, die zur Verwendung in Ihrer Produktionsumgebung vorgesehen ist. Im Gegensatz zu Nicht-Produktions-Sandboxes können Produktions-Sandboxes nicht zurückgesetzt oder gelöscht werden.

**Profil**: Ein Profil ist nicht mit dem Echtzeit-Kundenprofil als Dienst zu verwechseln. Es ist eine vollständige Darstellung eines einzelnen Kunden, erstellt aus zusammengeführten Datensatz- und Zeitreihendaten aus mehreren Quellen.

**Profilzugriff**: Die `/entities` -Endpunkt in der Echtzeit-Kundenprofil-API ermöglicht Ihnen den Zugriff auf Datensatzdaten und Zeitreihenereignisse im Profildatenspeicher. Siehe auch: Profilentitäten

**Profildaten**: Profildaten beziehen sich auf alle Daten, die sich im Profildatenspeicher befinden.

**Profildatenspeicher**: Der Profildatenspeicher (manchmal auch als Profilspeicher bezeichnet) ist ein vom Daten-Pool getrenntes Datenspeichersystem, das vom Echtzeit-Kundenprofil zum Erstellen und Speichern von Profilen verwendet wird.

**Profilentitäten**: Profilentitäten stellen Attribute dar, die sich auf eine einzelne Person beziehen, normalerweise einen Kunden. Stellen, die unter diese Kategorie fallen, sollten anhand der [!DNL XDM Individual Profile] -Klasse. Siehe auch: Profilzugriff

**Profilexport**: [!DNL Profile] Der Export ist einer der beiden Zieltypen in der Experience Platform. [!DNL Profile] export erzeugt eine Datei mit Profilen und Attributen und verwendet rohe PII-Daten mit E-Mail, um sie in Marketing- und E-Mail-Automatisierungsplattformen zu integrieren.

**Profilfragment**: Ein Profilfragment ist die Profilinformation für nur eine Identität aus der Liste der Identitäten, die für einen bestimmten Kunden vorhanden sind.

**Profil-ID**: Eine Profil-ID ist eine automatisch generierte Kennung, die mit einem Identitätstyp verknüpft ist und ein Profil darstellt.

**Eigenschaft**: Im Kontext von Tags ist eine Eigenschaft ein Container für alles, was zum Bereitstellen eines Satzes von Tags erforderlich ist.

## Q

**Abfrage**: Abfragen sind Anforderungen für Daten aus Datenbanktabellen.

**Abfrage-Editor**: Der Abfrage-Editor ist ein Tool zum Schreiben, Validieren und Senden von SQL-Anweisungen in [!DNL Query Service].

## R

**Real-time Customer Data Platform**: Adobe Real-time Customer Data Platform (Real-Time CDP) führt bekannte und unbekannte Kundendaten zusammen, um vertrauenswürdige Kundenprofile mit vereinfachter Integration, intelligenter Segmentierung und Echtzeit-Aktivierung über die digitale Journey zu erstellen.

**Echtzeit-Kundenprofil**: Das Echtzeit-Kundenprofil (auch als Profil bezeichnet) bietet eine ganzheitliche Sicht auf jeden einzelnen Kunden, indem es Daten aus mehreren Kanälen kombiniert, einschließlich Online-, Offline-, CRM- und Drittanbieter-Kanälen. Mit Profil können Sie Ihre Kundendaten in einzelne Profile konsolidieren, die umsetzbare, mit Zeitstempel versehene Konten für jede Kundeninteraktion bieten.

**Rezept**: Ein Rezept ist der Begriff der Adobe für eine Modellspezifikation und ist ein Container auf oberster Ebene, der bestimmte maschinelle Lernprozesse, KI-Algorithmen, Verarbeitungslogik und Konfigurationsparameter darstellt, die zum Erstellen und Ausführen eines trainierten Modells erforderlich sind und somit zur Lösung spezifischer Geschäftsprobleme beitragen.

**Datensatz**: Ein Datensatz ist Daten, die als Zeilen in einem Datensatz beibehalten werden.

**Aufzeichnen von Daten**: Stellt Informationen zu den Attributen eines Subjekts bereit. Ein Subjekt könnte eine Organisation oder eine Einzelperson sein.

**Wiederholung**: In [!DNL Query Service], eine Wiederholung definiert, ob eine Abfrage nur einmal oder wiederholt ausgeführt werden soll.

**Darstellung**: In [!DNL Offer Decisioning]ist eine Darstellung die Informationen, die von einem Kanal zur Anzeige eines Angebots verwendet werden, z. B. Ort oder Sprache.

**Ressource**: Im Kontext von Tags ist eine Ressource ein allgemeiner Begriff, der auf Optionen verweist, die der Tag-Benutzer in der Client-Umgebung konfigurieren kann, einschließlich Erweiterungen, Datenelementen und Regeln.

**Rollenbasierte Zugriffssteuerung**: Die rollenbasierte Zugriffskontrolle ermöglicht es Administratoren, Experience Platform-Benutzern Zugriff und Berechtigungen zuzuweisen. Zu den Berechtigungen gehört die Möglichkeit, Funktionen der Experience Platform anzuzeigen und/oder zu verwenden, z. B. das Erstellen von Sandboxes, das Definieren von Schemas und das Verwalten von Datensätzen.

**Regel**: Im Kontext von Tags ist eine Regel eine Sammlung von Komponenten, die einen bestimmten Satz von Ereignissen, Bedingungen und Aktionen definieren, die logisch gruppiert werden sollen.

**Regelkomponente**: Im Kontext von Tags sind Regelkomponenten die Ereignisse, Bedingungen und Aktionen, aus denen eine Regel besteht.

**Laufzeit**: Runtime gibt eine Laufzeitumgebung für ein Rezept für maschinelles Lernen an. [!DNL Python], R, [!DNL Spark], PySpark- und Tensorflow-Laufzeitumgebungen ermöglichen es Ihnen, eine URL für eine Rezeptionsquelle in ein Docker-Bild einzugeben.

## S

**Beispieldaten**: Beispieldaten sind eine Vorschau einer Datendatei, normalerweise die ersten 100 Zeilen, die einem Datenwissenschaftler oder -ingenieur eine Vorstellung davon vermitteln, welches Schema oder welche Daten sich in der Datendatei befinden.

**Sandbox**: Eine Sandbox ist ein virtuelles Konstrukt, das eine einzelne Platform-Instanz in eine separate virtuelle Umgebung aufteilt, um die Entwicklung und Weiterentwicklung von Programmen für digitale Erlebnisse zu unterstützen.

**Sandbox zurücksetzen**: Beim Zurücksetzen einer Sandbox werden alle Daten, einschließlich Daten, Profilen und Segmenten, in einer Sandbox gelöscht. Sandbox-Zurücksetzungen können sich auf Daten auswirken, die mit internen oder externen Zielen verbunden sind.

**Sandbox-Umschalter**: Das Steuerelement Sandbox-Umschalter in Experience Platform ermöglicht Benutzern die Navigation zwischen Sandboxes, auf die sie Zugriff haben. Durch das Wechseln einer Sandbox werden alle Inhalte geändert und der Zugriff auf Funktionen kann je nach Berechtigungen geändert werden.

**Zeitplan**: Ein Zeitplan ist eine benutzerdefinierte Spezifikation zur Häufigkeit oder Häufigkeit der Datenerfassung von einer Datenquelle eines Drittanbieters zu Adobe Experience Platform.

**Scoring**: Bei der Auswertung werden mithilfe eines trainierten Modells Erkenntnisse aus Daten generiert.

**Schema**: Ein Schema ist ein Regelsatz, der die Datenstruktur und das Datenformat darstellt und validiert. Ein Schema besteht aus einer Klasse und optionalen Feldergruppen und wird zum Erstellen von Datensätzen und Datensätzen verwendet. Ein Schema kann Verhaltensattribute, Zeitstempel, Identitäten, Attributdefinitionen, Beziehungen und mehr enthalten.

**Schemafeldgruppe**: Im Experience-Datenmodell (XDM) können Benutzer mit einer Schemafeldgruppe wiederverwendbare Felder erweitern, um ein oder mehrere Attribute zu definieren, die in ein Schema aufgenommen werden sollen.

**Schema Library**: Die Schema Library enthält branchenübliche XDM-Ressourcen, die von Adobe bereitgestellt werden, sowie benutzerdefinierte Ressourcen, die von Ihrem Unternehmen definiert wurden.

**Schema Registry**: Die Schema Registry bietet eine Benutzeroberfläche und RESTful-API, mit der alle schemabezogenen Ressourcen in der Schema Library angezeigt und verwaltet werden können.

**Geheimer Zugriffsschlüssel**: Ein geheimer Zugriffsschlüssel ist eine [!DNL Amazon] S3-Schlüssel, der in Verbindung mit der Zugriffsschlüssel-ID zum Signieren von AWS-Anfragen verwendet wird.

**Segment**: Ein Segment ist ein Regelsatz, der Attribute und Ereignisdaten enthält, die eine Reihe von Profilen als Zielgruppe qualifizieren.

**Segment Builder**: Die [!DNL Segment Builder] ist eine visuelle Entwicklungsumgebung zum Erstellen von Segmentdefinitionen. Sie dient als gemeinsame Komponente aller Anwendungen, die den Segmentierungsdienst von Experience Platform verwenden.

**Segmentdefinition**: Eine Segmentdefinition ist der Regelsatz, der zur Beschreibung der Hauptmerkmale oder des Verhaltens einer Zielgruppe verwendet wird. Nach der Erstellung einer Segmentdefinition werden die darin beschriebenen Regeln zur Bestimmung qualifizierter Zielgruppenmitglieder für ein Segment verwendet.

**Methode zur Segmentauswertung**: Es gibt zwei Methoden zur Segmentauswertung: geplant und bei Bedarf. Die geplante Auswertung ermöglicht einen wiederkehrenden Zeitplan für die Ausführung eines Exportauftrags zu einem bestimmten Zeitpunkt, während die On-Demand-Auswertung die Erstellung eines Segmentauftrags umfasst, um die Zielgruppe sofort zu erstellen.

**Segmentexport**: Der Segmentexport ist einer der beiden Zieltypen in der Experience Platform. Beim Segmentexport können Sie die Profile senden, die sich qualifizieren und dem Ziel zugeordnet wurden. Verwendet Segment- und Benutzer-IDs und pseudonyme Daten und lässt sich in der Regel in soziale Netzwerke und andere Zielplattformen für digitale Medien integrieren.

**Segment-ID**: Eine Segment-ID ist eine automatisch generierte Kennung, die mit einem Segment verknüpft ist.

**Segmentmitgliedschaft**: Die Segmentzugehörigkeit zeigt an, zu welchen Segmenten ein Profil derzeit gehört.

**Segmentregeln**: Segmentregeln definieren die Bedingungen, die bestimmen, ob ein Profil für ein Segment qualifiziert ist.

**Segmentierung**: Bei der Segmentierung wird eine große Gruppe von Kunden, Interessenten oder Verbrauchern in kleinere Gruppen unterteilt, die ähnliche Attribute aufweisen und ähnlich auf spezifische Marketing-Strategien reagieren.

**Sensei ML Framework**: Sensei ML Framework ist ein einheitliches Framework für maschinelles Lernen (ML), das Experience Platform-Daten nutzt, um Datenwissenschaftler in die Lage zu versetzen, schneller, skalierbarer und wiederverwendbarer ML-gestützter Nachrichtendienste zu entwickeln.

**Beschriftungen für vertrauliche Elemente (&quot;S&quot;)**: Mit vertraulichen (&quot;S&quot;) Beschriftungen werden Daten kategorisiert, die als vertraulich gelten, z. B. verschiedene Arten von Verhaltens- oder geografischen Daten, die als vertraulich markiert werden sollen.

**Dienste**: Ein leistungsstarkes Framework zur Implementierung von KI- und ML-Diensten durch Nutzung von Adobe Intelligent Services. Services bieten Echtzeit-, personalisierte Kundenerlebnisse oder setzen benutzerdefinierte intelligente Dienste um.

**Marketing-Aktion für Single-Identity-Personalisierung**: Eine Marketing-Aktion, die Daten für die Personalisierung von Inhalten auf der Site verwendet. Bei der Onsite-Personalisierung geht es um alle Daten, die verwendet werden, um Rückschlüsse auf die Interessen der Benutzer zu ziehen, und darum, auszuwählen, welche Inhalte oder Anzeigen auf der Grundlage dieser Rückschlüsse bereitgestellt werden.

**S1-Datennutzungsbezeichnung**: Ein `S1` Datennutzungsbezeichnung wird verwendet, um Daten zu klassifizieren, die den Längen- und Breitengrad angeben, der zur Bestimmung der genauen Position eines Geräts verwendet werden kann.

**S2-Datennutzungsbezeichnung**: Ein `S2` Datennutzungsbezeichnung wird verwendet, um Daten zu klassifizieren, mit denen ein allgemein definierter Geofence-Bereich bestimmt werden kann.

**Quelle**: Eine Quelle ist ein allgemeiner Begriff für jeden Input-Connector in Platform. Siehe auch: Quell-Connector

**Quellattribut**: Ein Quellattribut ist ein Feld im Quelldatensatz. Quellattribute werden Zielschemafeldern zugeordnet.

**Quellkatalog**: Der Quellkatalog ist die Liste der verfügbaren Quell-Connectoren in Experience Platform.

**Quellkategorie**: Eine Quellkategorie ist eine Gruppierung von Quellen mit ähnlichen Eigenschaften.

**Quell-Connector**: Mithilfe von Quell-Connectoren (auch als Quellen bezeichnet) können Anwender Daten aus mehreren Quellen einfach erfassen und so Daten strukturieren, beschriften und erweitern, indem Experience Platform-Dienste eingesetzt werden. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Cloud-basiertem Speicher, Software von Drittanbietern und CRM-Systemen.

**Streaming-Verbindung**: Eine Streaming-Verbindung ist ein eindeutiger Endpunkt, der von Adobe bereitgestellt und an die IMS-Organisation eines Kunden gebunden wird, um Daten in Experience Platform zu streamen.

**Standard-Identitäts-Namespace**: Standard-Identitäts-Namespaces sind vordefinierte Identitäts-Namespaces, die von Adobe bereitgestellt werden und branchenübliche Lösungen darstellen, mit denen Kunden identifiziert werden können.

**Streaming-Erfassung**: Mit der Streaming-Erfassung können Sie Daten von Client- und Server-seitigen Geräten in Echtzeit an die Experience Platform senden.

**Streaming-Segmentierung**: Streaming-Segmentierung ist ein fortlaufender Datenauswahlprozess, der Segmente als Reaktion auf Benutzeraktivitäten aktualisiert. Nachdem ein Segment erstellt und gespeichert wurde, wird die Segmentdefinition auf in [!DNL Real-time Customer Profile] eingehende Daten angewendet. Segmenthinzufügungen und -entfernungen werden regelmäßig verarbeitet, um sicherzustellen, dass Ihre Zielgruppe relevant bleibt.

**Systemansicht**: Die Systemansicht ist eine visuelle Darstellung von Quelldatensätzen, die durchlaufen werden. [!DNL Real-time Customer Profile] zu Zielen.

## T

**Tags**: In Adobe Experience Platform bieten Tags Tools zum Bereitstellen, Vereinheitlichen und Verwalten von Analyse-, Marketing- und Werbe-Integrationen, die zur Unterstützung relevanter Kundenerlebnisse auf allen Client-Geräten erforderlich sind.

**Target-Funktionen**: Bei der Funktionszuordnung ist eine Zielfunktion die Funktion, die von einem Modell vorhergesagt wird.

**Zeitreihendaten**: Zeitreihendaten liefern eine Momentaufnahme des Systems zum Zeitpunkt, zu dem eine Aktion entweder direkt oder indirekt von einem Datensatzsubjekt durchgeführt wurde.

**Schulungsmodell**: Ein trainiertes Modell stellt die ausführbare Ausgabe eines Modell-Trainings-Prozesses dar, in dem ein Satz von Trainings-Daten auf die Modellinstanz angewendet wurde. Ein trainiertes Modell behält einen Verweis auf jeden intelligenten Webdienst bei, der daraus erstellt wird. Ein trainiertes Modell eignet sich zum Scoring und zur Erstellung eines intelligenten Webdienstes.

**Token**: Ein Token ist eine Art zweifakultativer Authentifizierungssicherheit, die verwendet werden kann, um die Verwendung von Computerdiensten mit [!DNL Query Service].

## U

**Vereinigungsschema**: Ein Vereinigungsschema ist eine Konsolidierung von Schemas, die dieselbe Klasse teilen und für die [!DNL Real-time Customer Profile]. Für eine Organisation können mehrere Vereinigungsschemas vorhanden sein, es kann jedoch pro Klasse nur ein Vereinigungsschema geben.

## V

## W

## X

**XDM**: Siehe Experience-Datenmodell (XDM).

**XDM-Entscheidungsereignis**: XDM-Entscheidungsereignis ist eine zeitreihenbasierte Klasse, mit der Beobachtungen zum Ergebnis und zum Kontext einer Entscheidungsaktivität erfasst werden. Dazu gehören Informationen darüber, wie die Entscheidung getroffen wurde, wann sie erfolgte, welche Optionen vorgeschlagen (und ausgewählt) wurden und welcher kontextbezogene Zustand existierte, der entweder die Entscheidung beeinflusst hat oder während des Entscheidungsprozesses beobachtet werden konnte.

**XDM ExperienceEvent**: XDM ExperienceEvent ist eine zeitreihenbasierte Klasse, mit der der Status des Systems beim Eintreten eines Ereignisses (oder einer Reihe von Ereignissen) erfasst wird, einschließlich des Zeitpunkts und der Identität des betroffenen Subjekts. Siehe auch: Erlebnisereignis

**XDM Individual Profile**: XDM [!DNL Individual Profile] ist eine auf Aufzeichnungen basierende Klasse, die eine eindeutige Darstellung der Attribute sowohl identifizierter als auch teilweise identifizierter Personen bildet. Hochgradig identifizierte Profile können für die persönliche Kommunikation oder zielgerichtete Interaktionen verwendet werden und detaillierte persönliche Informationen wie Name, Geschlecht, Geburtsdatum, Ort und Kontaktinformationen, einschließlich Telefonnummern und E-Mail-Adressen, enthalten.

**XDM-System**: XDM System stellt das Framework dar, das XDM-Schemas für die Verwendung in nachgelagerten Experience Platform-Services implementiert.

## Y

## Z
