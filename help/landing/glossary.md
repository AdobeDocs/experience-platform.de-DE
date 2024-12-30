---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Adobe Experience Platform-Glossar
description: Ein Glossar wichtiger Experience Platform-Terminologie.
exl-id: 00eae5f5-7dfa-45ac-aff9-9e1769a3a53a
source-git-commit: b16eae9698de6c20022fdf1a3ff659df35e440f6
workflow-type: tm+mt
source-wordcount: '7996'
ht-degree: 4%

---

# Adobe Experience Platform-Glossar {#adobe-experience-platform-glossary}

## A

**Zugriffssteuerung**: Die rollenbasierte Zugriffssteuerung ermöglicht es Administratoren, Benutzenden von Experience Platform Zugriff und Berechtigungen zuzuweisen. Zu den Berechtigungen gehört die Möglichkeit, Experience Platform-Funktionen anzuzeigen und/oder zu verwenden, z. B. das Erstellen von Sandboxes, das Definieren von Schemas und das Verwalten von Datensätzen.

**Zugriffsschlüssel-ID**: Eine Zugriffsschlüssel-ID ist eine eindeutige Kennung, die mit einem geheimen [!DNL Amazon] S3-Zugriffsschlüssel verknüpft ist. Die Zugriffsschlüssel-ID und der geheime Zugriffsschlüssel werden zusammen zum Signieren von [!DNL Amazon Web Services] (AWS)-Anfragen verwendet.

**Aktion**: Im Kontext von Tags ist eine Aktion ein bestimmter Typ von Regelkomponente, die definiert, was passieren soll, nachdem ein Ereignis eintritt und Bedingungen ausgewertet und übergeben werden.

**Aktivieren**: „Aktivieren“ ist die Aktion, die eine Benutzerin oder ein Benutzer ausführt, um ein Segment oder Profile einem Ziel wie [!DNL Oracle Eloqua], [!DNL Google] oder [!DNL Salesforce Marketing Cloud] zuzuordnen.

**Aktivität**: In [!DNL Offer Decisioning] enthält eine Aktivität die Logik, die über die Auswahl eines Angebots bestimmt.

**Administrator**: Eine oder mehrere Personen in Ihrer Organisation, die Berechtigungen für das Experience Platform in Adobe Admin Console konfigurieren und anpassen können.

**Adobe Admin Console**: Adobe Admin Console bietet einen zentralen Speicherort für die Verwaltung von Adobe-Produktberechtigungen und den Zugriff für Ihr Unternehmen. Über die Konsole können Administratoren Benutzergruppen Zugriffsberechtigungen für verschiedene Platform-Funktionen erteilen, wie z. B. „Datensätze verwalten“, „Datensätze anzeigen“ oder „Profile verwalten“.

**Adobe Experience Platform**: Adobe Experience Platform standardisiert Daten und Inhalte im gesamten Unternehmen, unterstützt Echtzeit-Kundenprofile, ermöglicht Datenwissenschaft und beschleunigt die Inhaltsgeschwindigkeit, um die Erlebnispersonalisierung auf dem gesamten Kunden-Journey zu fördern.

**Adobe Experience Platform Query Service**: Ermöglicht Datenanalysten die Abfrage von Ereignissen und Profilen zur Verwendung in Analysen und maschinellem Lernen. Mit Query Service können Datenwissenschaftler und Analysten alle ihre im Experience Platform gespeicherten Datensätze abrufen (einschließlich Verhaltensdaten sowie POS (Point-of-Sale), CRM (Customer Relationship Management) und mehr) und diese Datensätze abfragen, um spezifische Fragen zu den Daten zu beantworten.

**Adobe Experience Platform-Segmentierungs-**: Ermöglicht das Erstellen von Segmenten und das Generieren von Zielgruppen aus Ihren Echtzeit-Kundenprofildaten. Diese Zielgruppen können dann in ihre eigenen Datensätze im Data Lake exportiert werden.

**Adobe Intelligent Services**: Intelligent Services wie Attribution AI und Kunden-KI sind auf maschinellem Lernen basierende Modelle auf künstlicher Intelligenz, die speziell entwickelt wurden und für die Ausführung und den Betrieb von Experience Platform erforderlich sind.

**Adobe I/O**: Adobe I/O ist Teil von Experience Platform und bietet Zugriff auf alles, was Entwickler benötigen, um Platform zu integrieren, zu erweitern und anzupassen, einschließlich APIs, Ereignisse, Entwicklerkonsole und hilfreiche Tools.

**Adobe Sensei**: Adobe Sensei ist das Intelligence-Framework, das Experience Platform unterstützt. Darüber hinaus bietet es eine Reihe von KI-Services, mit denen Marken ihre Fähigkeit verbessern können, personalisierte Kundenerlebnisse in Echtzeit bereitzustellen.

**Amazon S3-Bucket**: [!DNL Amazon S3] Buckets sind die grundlegenden Container für Daten, die im [!DNL Amazon]-Ökosystem gespeichert sind. Buckets enthalten Objekte. Jedes Objekt wird gespeichert und mit einem eindeutigen, vom Entwickler zugewiesenen Schlüssel abgerufen.

**Amazon S3-Connector**: Der [!DNL Amazon] S3-Connector ermöglicht Kunden von Experience Platform eine sichere Verbindung und den Zugriff auf ihre [!DNL Amazon] S3-Daten.

**APA**: Die [[!DNL Australia Privacy Act (Privacy Act)]](https://www.oaic.gov.au/privacy/the-privacy-act) fördert und schützt die Privatsphäre von Personen und regelt, wie australische Regierungsbehörden und Organisationen mit personenbezogenen Daten umgehen. Die [!DNL Privacy Act] enthält Grundsätze, die für Organisationen des Privatsektors gelten. So haben Privatpersonen beispielsweise das Recht zu verstehen, warum die personenbezogenen Daten erfasst werden und wie sie verwendet werden, auf ihre Daten zuzugreifen, sie zu löschen und ihre personenbezogenen Daten zu korrigieren.

**Speicherstrategie anhängen**: Die Speicherstrategie „Anhängen“ ist eine Option, die verwendet wird, wenn Daten von Drittanbietern angegeben werden, die über eine Verbindung aufgenommen werden sollen, und wenn neue Daten oder Zeilen am Ende des Datensatzes angehängt werden. Die zuvor aufgenommenen Zeilen bleiben unberührt, und nur Zeilen, die seit der letzten geplanten Ausführung erstellt wurden, werden in das Experience Platform aufgenommen. Alle Zeilen, die im Quellsystem geändert wurden, bleiben auf dem Experience Platform unverändert.

**Array**: Arrays werden für geordnete Elemente mit demselben Datentyp verwendet.

**Künstliche Intelligenz**: Künstliche Intelligenz ist eine Theorie und Entwicklung von Computersystemen, die in der Lage sind, Aufgaben auszuführen, die normalerweise menschliche Intelligenz erfordern, wie visuelle Wahrnehmung, Spracherkennung, Entscheidungsfindung und Übersetzung zwischen Sprachen.

**Attribute**: Attribute sind angegebene Merkmale, die ein Profil darstellen.

**Attributzusammenführung**: Beim Definieren einer Zusammenführungsrichtlinie mit der Echtzeit-Kundenprofil-API gibt das `attributeMerge`-Objekt an, wie die Zusammenführungsrichtlinie Profilattribute im Falle von Datenkonflikten priorisiert. Dies entspricht der Auswahl einer [!UICONTROL Zusammenführungsmethode] beim Definieren einer Zusammenführungsrichtlinie in der Platform-Benutzeroberfläche.

**Attribution AI**: [!DNL Attribution AI] ist ein Intelligent Service, der auf Adobe Sensei basiert und algorithmische Mehrkanal-Attributionsfunktionen über den gesamten Kundenlebenszyklus hinweg bietet.

**Audience**: Eine Audience ist der resultierende Satz von Profilen, die den Kriterien einer Segmentdefinition entsprechen.

**Zielgruppengröße**: Eine Zielgruppengröße ist die Gesamtzahl der Profile, die die Kriterien einer Segmentdefinition erfüllen und für die Zielgruppenzugehörigkeit qualifiziert sind.

**Zielgruppen-Schnappschuss**: Ein Zielgruppen-Schnappschuss erfasst alle Profile, die sich zum Zeitpunkt der Segmentierung für die Segmentkriterien qualifizieren.

## B

**Aufstockung**: Bei geplanten Quellen ermöglicht die Aufstockungsoption die Aufnahme historischer Daten.

**Aufstockungszeitraum**: Der Aufstockungszeitraum ist eine Option, um den Zeitraum für die Aufnahme historischer Drittanbieterdaten über eine Quellverbindung festzulegen. Wenn Sie einen Aufstockungszeitraum von „Für immer“ auswählen, wird der gesamte Verlauf der Quelldaten auf Experience Platform aufgenommen.

**Batch**: Ein Batch ist ein Satz von Daten, die über einen bestimmten Zeitraum gesammelt und als eine Einheit verarbeitet werden. Datensätze bestehen aus mehreren Batches.

**Batch-ID**: Eine Batch-ID ist eine von Adobe generierte Kennung für einen Datenstapel.

**Batch-Aufnahme**: Die Batch-Aufnahme ermöglicht es Ihnen, Daten als Batch-Dateien in Experience Platform aufzunehmen. Batches sind Dateneinheiten aus einer oder mehreren Dateien, die als Einheit aufgenommen werden.

**Batch-**: Die Batch-Segmentierung ist eine Alternative zu einem fortlaufenden Datenauswahlprozess und verschiebt alle Profildaten gleichzeitig durch Segmentdefinitionen, um entsprechende Zielgruppen zu erstellen. Nach der Erstellung wird dieses Segment gespeichert und gespeichert, sodass es zur Verwendung exportiert werden kann.

**Build**: Im Kontext von Tags ist ein Build eine Datei oder ein Satz von Dateien, die alle Konfigurationen und den Code enthalten, der zum Ausführen der in einer Bibliothek enthaltenen Geschäftslogik erforderlich ist, sodass Sie diese Bibliothek auf Ihrer Website oder in Ihrer Mobile App bereitstellen können.

**Business Intelligence-Tools**: Business Intelligence-Tools (BI) sind in erster Linie in [!DNL Experience Platform Query Service] integriert. BI-Tools sind Arten von Anwendungssoftware, die große Mengen unstrukturierter Daten aus internen und externen Systemen erfassen und verarbeiten.

## C

**Begrenzung**: In [!DNL Offer Decisioning] wird die Begrenzung (auch als Frequenzlimitierung bezeichnet) in Entscheidungsregeln verwendet, um zu definieren, wie oft ein Angebot unterbreitet wird. Es gibt zwei Arten von Obergrenzen: wie oft ein Angebot für die gesamte Ziel-Audience vorgeschlagen werden kann (eine so genannte „globale Begrenzung„) und wie oft ein Angebot demselben Endbenutzer vorgeschlagen werden kann (eine so genannte „Profilbegrenzung„).

**Catalog**: Im Kontext von Quellen und Zielen ist ein Katalog eine Galerie mit verfügbaren Anschlüssen zu Adobe-Anwendungen und Technologien von Drittanbietern. Nicht zu verwechseln mit [!DNL Catalog Service].

**[!DNL Catalog Service]**: [!DNL Catalog Service] (manchmal auch als [!DNL Catalog] bezeichnet) ist das „System of Record“ für den Speicherort und die Herkunft von Daten in Adobe Experience Platform. Alle Daten, die in Experience Platform aufgenommen werden, werden als Dateien und Ordner im Data Lake gespeichert. [!DNL Catalog] speichert die Metadaten und Beschreibungen dieser Dateien und Ordner für Such-, Überwachungs- und Data-Governance-Zwecke.

**CCPA**: Der [[!DNL California Consumer Privacy Act (CCPA)]](https://oag.ca.gov/privacy/ccpa) verbessert die Datenschutzrechte und den Verbraucherschutz für Einwohner von Kalifornien, USA. Der CCPA bietet neue Datenschutzrechte, mit denen Verbraucher u. a. ihre personenbezogenen Daten einsehen und löschen oder herausfinden können, ob (und an wen) ihre Daten verkauft oder weitergegeben wurden. Zusätzlich gibt es das Recht, den Verkauf ihrer Daten an Dritte zu verhindern.

**Klasse**: Im Experience-Datenmodell (XDM) definiert eine Klasse den kleinsten Satz von Feldern, die zum Erstellen eines Schemas verwendet werden, und definiert das Basisverhalten des Geschäftsobjekts, das das Schema darstellt.

**Client**: Ein Client ist ein externes Tool oder eine externe Anwendung, die über [!DNL PostgreSQL] Protokoll oder die HTTP-API eine Verbindung zu [!DNL Query Service] herstellt.

**Sammlung**: In [!DNL Offer Decisioning] sind Sammlungen Untergruppen von Angeboten, die auf von einem Marketing-Experten vordefinierten Bedingungen basieren, z. B. der Kategorie des Angebots.

**Mit PII-Marketing-Aktion kombinieren**: Eine Marketing-Aktion, die alle persönlich identifizierbaren Informationen (PII) mit anonymen Daten kombiniert. Verträge über Daten, die aus Werbenetzwerken, Werbe-Servern und Drittanbietern von Daten bezogen werden, beinhalten häufig spezifische vertragliche Verbote der Verwendung solcher Daten mit direkt identifizierbaren Daten.

**Befehlszeilenschnittstelle**: Eine Befehlszeilenschnittstelle ist ein textbasiertes Tool, mit dem eine Verbindung zu [!DNL Query Service] hergestellt werden kann, um Abfragen im Rohmodus auszuführen.

**Komposition**: Eine Komposition ist eine Gruppierung von Komponenten, die zusammen das Schema bilden.

**Bedingung**: Im Kontext von Tags ist eine Bedingung eine Regelkomponente, die eine logische Anweisung auswertet, die `true` oder `false` zurückgeben muss. Alle Bedingungen müssen als `true` ausgewertet werden, und alle Ausnahmebedingungen müssen als `false` ausgewertet werden, bevor Aktionen an der Regel ausgeführt werden.

**Konsole**: In [!DNL Query Service] stellt die Konsole Informationen zum Status und zum Betrieb einer Abfrage bereit. Die Konsole zeigt den Verbindungsstatus zum [!DNL Query Service], die ausgeführten Abfragen und alle Fehlermeldungen an, die aus diesen Abfragen resultieren.

**Vertrags-(„C„)-Kennzeichnungen**: Vertrags-(„C„)-Datennutzungskennzeichnungen werden verwendet, um Daten zu kategorisieren, für die vertragliche Verpflichtungen bestehen oder die mit den Data-Governance-Richtlinien Ihres Unternehmens in Zusammenhang stehen.

**CPRA**: Der [[!DNL California Consumer Privacy Rights Act (CPRA)]](https://cppa.ca.gov/regulations/consumer_privacy_act.html) erweitert und ändert Teile des [!DNL California Consumer Privacy Act (CCPA)]. Der [!DNL CPRA] schafft eine neue Grundlage für den Schutz von Verbraucherdaten in Kalifornien, indem er die Verbraucherrechte erweitert und die Art der Daten erweitert, die durch eine breitere Definition sensibler personenbezogener Daten abgedeckt werden. Darüber hinaus hat die [!DNL CPRA] die California Privacy Protection Agency eingerichtet, eine neue Behörde, die sich mit der Umsetzung und Durchsetzung von Datenschutzregeln beschäftigt.

**C1 Vertrags-**: Eine `C1` Vertrags-Datennutzungskennzeichnung gibt an, dass Daten nur in aggregierter Form aus Adobe Experience Cloud exportiert werden können, ohne dass Einzel- oder Gerätekennungen enthalten sind. Zum Beispiel Daten, die aus Social Media stammen.

**C2-**: Eine `C2`-Kennzeichnung für Vertragsdaten gibt Daten an, die nicht an einen Drittanbieter exportiert werden können. Einige Datenanbieter haben in ihren Verträgen Klauseln, die den Export von Daten von dort verbieten, wo sie ursprünglich erfasst wurden. Beispielsweise wird die Übertragung von Daten, die Sie von Social Media erhalten, oft durch deren Verträge eingeschränkt. C2 ist restriktiver als C1, das nur Aggregation und anonyme Daten erfordert.

**C3 Vertrags-Kennzeichnung**: Eine `C3` Vertrags-Datennutzungskennzeichnung gibt Daten an, die nicht mit direkt identifizierbaren Informationen kombiniert oder anderweitig verwendet werden können. Einige Datenanbieter haben Vertragsklauseln, die die Kombination oder Verwendung dieser Daten mit direkt identifizierbaren Informationen verbieten. Verträge für Daten, die von Werbenetzwerken, Anzeigen-Servern und Drittanbietern von Daten bezogen werden, enthalten beispielsweise oft spezifische vertragliche Verbote der Verwendung direkt identifizierbarer Daten.

**C4-Vertrags-**: Eine `C4` Vertrags-Datennutzungskennzeichnung gibt an, dass Daten nicht für das Targeting von Anzeigen oder Inhalten verwendet werden können, weder auf der Site noch Website-übergreifend. C4 ist die restriktivste Kennzeichnung, da sie die Kennzeichnungen C5, C6 und C7 umfasst.

**C5 Vertrags-Kennzeichnung**: Eine `C5` Vertrags-Datennutzungskennzeichnung gibt an, dass Daten nicht für das Site-übergreifende Targeting von interessenbasierten Inhalten oder Anzeigen verwendet werden können. Interessenbasiertes Targeting oder Personalisierung tritt auf, wenn die folgenden drei Bedingungen erfüllt sind: Die auf der Site gesammelten Daten werden verwendet, um Rückschlüsse auf das Interesse eines Benutzers zu ziehen; werden in einem anderen Kontext verwendet, z. B. auf einer anderen Site oder in einem Programm; und werden verwendet, um auszuwählen, welche Inhalte oder Anzeigen auf der Grundlage dieser Rückschlüsse bereitgestellt werden.

**C6-Vertrags** Kennzeichnung: Eine `C6`-Vertrags-Datennutzungskennzeichnung gibt an, dass Daten nicht für das Targeting von Anzeigen auf der Site verwendet werden können. Das Targeting von Anzeigen auf der Site umfasst die Auswahl und den Versand von Anzeigen auf den Websites oder in Programmen Ihres Unternehmens oder zur Messung der Bereitstellung und der Effektivität solcher Anzeigen. Dazu gehören die Verwendung von zuvor erfassten Onsite-Daten über das Interesse der Benutzer an der Auswahl von Anzeigen, Prozessdaten darüber, welche Anzeigen wann und wo angezeigt wurden, und ob die Benutzer irgendwelche Aktionen im Zusammenhang mit der Werbung ergriffen haben, wie z. B. das Klicken auf eine Anzeige oder das Tätigen eines Kaufs.

**C7-Vertrags** Kennzeichnung: Eine `C7`-Vertrags-Datennutzungskennzeichnung gibt an, dass Daten nicht für das Targeting von Inhalten auf der Site verwendet werden können. Das Content-Targeting auf der Site umfasst die Auswahl und Bereitstellung von Inhalten auf den Websites oder in Programmen Ihres Unternehmens oder zur Messung der Bereitstellung und der Effektivität solcher Inhalte. Dazu gehören zuvor erfasste Informationen über das Interesse der Benutzer an der Auswahl von Inhalten, die Verarbeitung von Daten darüber, welche Inhalte angezeigt wurden, wie oft und wie lange sie angezeigt wurden, wann und wo sie angezeigt wurden und ob die Benutzer irgendwelche Aktionen im Zusammenhang mit dem Inhalt durchgeführt haben, einschließlich beispielsweise des Klickens auf Inhalte.

**C8 Vertrags-Kennzeichnung**: Eine `C8` Vertrags-Datennutzungskennzeichnung gibt an, dass Daten nicht für die Messung der Websites oder Programme Ihres Unternehmens verwendet werden können. Dies umfasst nicht das interessenbasierte Targeting, d. h. die Sammlung von Informationen über Ihre Nutzung dieses Service zur späteren Personalisierung von Inhalten und/oder Werbung in anderen Kontexten.

**C9-Vertragskennzeichnung**: Eine `C9`-Vertragsdatennutzungskennzeichnung gibt an, dass Daten nicht in datenwissenschaftlichen Workflows verwendet werden können. Einige Verträge beinhalten ein explizites Verbot von Daten, die für die Datenwissenschaft verwendet werden. Manchmal werden diese so formuliert, dass sie die Verwendung von Daten für künstliche Intelligenz (KI), maschinelles Lernen (ML) oder Modellierung verbieten.

**C10 Vertrags-**: Eine `C10` Vertrags-Datennutzungskennzeichnung gibt an, dass Daten nicht für die Aktivierung zusammengefügter Identitäten verwendet werden können. Einige Datennutzungsrichtlinien beschränken die Verwendung von zusammengesetzten Identitätsdaten für die Personalisierung. Der `C10` Titel wird automatisch auf Segmente angewendet, wenn deren Zusammenführungsrichtlinien die Option „Privates Diagramm“ verwenden.

**Spalte Erstellungsdatum**: Die Auswahl einer Spalte Erstellungsdatum ist eine Option bei der Angabe von Drittanbieterdaten über eine Quellverbindung. Wenn die Strategie zum Anhängen von Speichervorgängen ausgewählt ist und das Datensatzschema mehrere Datumsfelder enthält, müssen Sie aus dem verfügbaren Schema auswählen, um eine Spalte für den Schlüssel „Erstellt am“ anzugeben. Die Option Erstellungsdatum ist nicht verfügbar, wenn die Strategie Speichern überschreiben ausgewählt ist.

**Create Table as Select**: Create Table as Select (CTAS) ist ein SQL-Befehl, der bei Ausführung als Teil einer vollständigen und gültigen SQL-Abfrage [!DNL Query Service] anweist, die Ergebnisse der Abfrage in einem Datensatz zu speichern. Sie können eine neue Ergebnismenge erstellen, vorherige Ergebnisse überschreiben oder an vorherige Ergebnisse anhängen.

**Site-übergreifende Daten**: Site-übergreifende Daten sind die Kombination von Daten aus verschiedenen Sites, einschließlich einer Kombination aus Onsite-Daten und Offsite-Daten oder einer Kombination von Daten aus verschiedenen Offsite-Quellen.

**Site-übergreifendes Targeting - Marketing** Aktion: Eine Marketing-Aktion, die Daten für Site-übergreifendes Anzeigen-Targeting verwendet. Die Kombination von Daten aus verschiedenen Sites, einschließlich einer Kombination aus Daten in einer Site und Offsite-Daten oder einer Kombination von Daten aus verschiedenen Offsite-Quellen, wird als „Site-übergreifende Daten“ bezeichnet. Site-übergreifende Daten werden in der Regel gesammelt und verarbeitet, um Rückschlüsse auf die Interessen der Kunden zu ziehen.

**Benutzerdefinierter Identity-Namespace**: Benutzerdefinierte Identity-Namespaces können von Ihrem Unternehmen erstellt werden, um Identitäten für eine bestimmte Organisation oder einen bestimmten Business-Case darzustellen.

**Benutzerdefinierte Kennzeichnungen**: Mit benutzerdefinierten Datennutzungskennzeichnungen können Sie bestimmte Kennzeichnungen erstellen und auf Datenfelder anwenden, die bestimmten Geschäftsanforderungen entsprechen.

**Kunden-KI**: Kunden-KI ist ein Intelligent Service, der auf Adobe Sensei basiert und Kundenprofile mit KI-basierten Tendenzen anreichert sowie die Kundensegmentierung und Zielgruppenbestimmung ermöglicht.

## D

**Täglich**: plant im Kontext geplanter Dateiexporte vollständige oder inkrementelle Dateiexporte einmal täglich, jeden Tag, vom Startdatum bis zum Enddatum zu der vom Benutzer angegebenen Zeit.

**Datenwörterbuch**: Im Kontext von Tags ist ein Datenwörterbuch (auch als Datenzuordnung bezeichnet) ein Satz von Datenelementen, die in einer Eigenschaft definiert sind.

**Datenelement**: Im Kontext von Tags ist ein Datenelement ein Zeiger, der in Regeln und Erweiterungen verwendet wird, um auf ein bestimmtes Datenelement zu verweisen, das auf dem Client-Gerät vorhanden ist.

**Datenaufnahme**: Bei der Datenaufnahme werden Daten aus einer Quelle zum Experience Platform hinzugefügt. Daten können auf verschiedene Weise in Platform aufgenommen werden, einschließlich Streaming, Batches oder Hinzufügen über Quell-Connectoren.

**Datenschicht**: Im Kontext von Tags ist eine Datenschicht eine Datenstruktur, die auf dem Client-Gerät vorhanden ist und Metadaten über den Kontext enthält, in dem eine Seite oder ein Bildschirm angezeigt wird.

**Data Governance**: Data Governance umfasst die Strategien und Technologien, mit denen sichergestellt wird, dass die Daten den Vorschriften und organisatorischen Richtlinien in Bezug auf die Datennutzung entsprechen.

**Datenintegrationspartner**: Datenintegrationspartner vereinfachen und automatisieren das Laden und Umwandeln großer Datenmengen aus über 200 Quellen auf Experience Platform, ohne Code zu schreiben.

**Datensatzkennzeichnungen**: Datennutzungskennzeichnungen können zu Datensätzen hinzugefügt werden. Alle Felder in diesem Datensatz übernehmen die Kennzeichnungen des Datensatzes.

**Data Science Workspace**: [!DNL Data Science Workspace] in Experience Platform ermöglicht es Kunden, anhand von Daten aus verschiedenen Platform- und Adobe-Anwendungen Modelle für maschinelles Lernen zu erstellen, um intelligente Segmente zu erstellen, Einblicke zu generieren und Prognosen zu liefern, mit denen Sie die digitalen Erlebnisse der Endbenutzer erheblich verbessern können.

**Datenquelle**: Eine Datenquelle ist eine vom Benutzer angegebene Herkunft von Daten. Beispiele für eine Datenquelle sind eine Mobile App, Profil- und/oder Erlebnisereignisse, Website-Profilereignisse oder ein CRM.

**Data Steward**: Ein Data Steward ist die Person, die für das Management, die Aufsicht und die Durchsetzung der Datenelemente eines Unternehmens verantwortlich ist. Ein Data Steward stellt außerdem sicher, dass Data-Governance-Richtlinien geschützt und gepflegt werden, um die gesetzlichen Vorschriften und organisatorischen Richtlinien einzuhalten.

**Datenstrom**: Ein Datenstrom ist ein Satz oder eine Sammlung von Nachrichten, die dasselbe Schema verwenden und von derselben Quelle gesendet werden.

**Datentyp**: Ein Datentyp ist eine wiederverwendbare XDM-Ressource, die ein Feld vom Typ „Objekt“ definiert, das mehrere Eigenschaften in einer hierarchischen Darstellung enthält.

**Datennutzungskennzeichnungen**: Mit Datennutzungskennzeichnungen können Sie Daten kategorisieren, die datenschutzbezogene Überlegungen und vertragliche Bedingungen zur Einhaltung von Verordnungen und Unternehmensrichtlinien widerspiegeln. Einem Datensatz hinzugefügte Datennutzungsbeschriftungen werden übernommen oder auf alle Felder in diesem Datensatz angewendet. Datennutzungsbeschriftungen können auch direkt auf Felder angewendet werden.

**Datenfluss**: Ein Datenfluss ist eine virtuelle Pipeline von Daten, die von einer Quelle in Platform und von dort zu Zielen fließen.

**Datenflussausführung**: Eine Datenflussausführung ist ein Datenfluss, der basierend auf einem vom Benutzer angegebenen Zeitplan auf Experience Platform landet.

**Datensatz**: Ein Datensatz ist ein Konstrukt zur Speicherung und Verwaltung von Daten, normalerweise einer Tabelle, die ein Schema (Spalten) und Felder (Zeilen) enthält.

**Datensatz-ID**: Eine von Adobe generierte Kennung für einen aufgenommenen Datensatz.

**Datensatzausgabe**: Die Datensatzausgabe bietet einen Mechanismus, um zu bestimmen, was die Option „Tabelle als Auswahl erstellen“ für eine bestimmte [!DNL Query Service]-Ausführung verwendet wird.

**Deduplizierungsschlüssel**: Ein benutzerdefinierter Primärschlüssel, der die Identität bestimmt, mit der Benutzerinnen und Benutzer ihre Profile deduplizieren lassen möchten&#x200B;

**Delta-Spalte**: Mit einer Delta-Spalte können Sie ein Quelldatenfeld auswählen, das einen Zeitstempel für die inkrementelle Aufnahme darstellt.

**Delta-Speicherstrategie**: Die Delta-Speicherstrategie ist eine Option für die Aufnahme von Drittanbieterdaten über eine Quellverbindung. Mit der Option kann der Benutzer angeben, dass neue oder geänderte Zeilen von Quelldaten in Experience Platform aufgenommen werden. Am Ende des Datensatzes werden neue Zeilen hinzugefügt und geänderte Zeilen im Datensatz auf Experience Platform aktualisiert.

**Descriptor**: Im Experience-Datenmodell (XDM) ist ein Deskriptor ein zusätzlicher Satz schemabezogener Metadaten, der ein bestimmtes Verhalten für ein Feld beschreibt. Deskriptoren können vom Experience Platform verwendet werden, um das beabsichtigte Schemaverhalten zu verstehen, z. B. die Beziehung zwischen zwei Schemas.

**Ziel**: Ein Ziel ist ein allgemeiner Begriff für einen Endpunkt, z. B. eine Adobe-Anwendung, eine Werbeplattform, einen Cloud-Speicher-Service oder einen Marketing-Service, bei dem eine Zielgruppe aktiviert und bereitgestellt wird.

**Zielkategorie**: Eine Zielkategorie ist eine Gruppierung von Zielen mit ähnlichen Eigenschaften.

**Zielkatalog**: Ein Zielkatalog ist eine Liste der verfügbaren Ziele in Experience Platform.

**Direktaufrufregeln**: Im Kontext von Tags ist eine Direktaufrufregel eine Regel, die ausgeführt wird, wenn sie direkt von der Seite aufgerufen wird, wobei die Ereigniserkennung und die Suchsysteme umgangen werden.

**Anzeigename**: Im Experience-Datenmodell (XDM) ist ein Anzeigename ein benutzerfreundlicher Name für ein Feld, das in der Benutzeroberfläche angezeigt wird.

## E

**Geeignetes Angebot**: Ein geeignetes Angebot kann einem Profil konsistent angeboten werden, da es die zuvor definierten Einschränkungen erfüllt.

**Eignungsregeln**: In [!DNL Offer Decisioning] werden Eignungsregeln auf ein Profil angewendet, das sich auf Kalender, Zeitplan und Begrenzungsregeln bezieht.

**E-Mail-Targeting-Marketing-Aktion**: Eine Marketing-Aktion, die Daten in E-Mail-Targeting-Kampagnen verwendet.

**Einbettungs-Code**: Im Kontext von Tags ist der Einbettungs-Code ein Skript-Tag, das innerhalb der HTML auf einer Site oder in einer Umgebung platziert wird. Der Einbettungs-Code weist den Browser an, wo der Build abgerufen werden soll.

**Auflistung**: Eine Auflistung (enum) ist ein XDM-Feld, das auf einen Satz vordefinierter Werte beschränkt ist.

**Umgebung**: Im Kontext von Tags ist eine Umgebung ein Satz von Bereitstellungsanweisungen, die die Host-Bereitstellung und das Dateiformat eines Builds angeben. Eine Bibliothek muss mit einer Umgebung gepaart sein, bevor sie erstellt werden kann.

**Fehlerdiagnose**: Die Fehlerdiagnose ermöglicht die Erstellung detaillierter Fehlermeldungen für aufgenommene Batches. Mit dem Fehlerschwellenwert können Sie den Prozentsatz der akzeptablen Fehler konfigurieren, bevor ein Batch fehlschlägt.

**Ereignis**: Im Kontext von Tags ist ein Ereignis ein bestimmter Typ von Regelkomponente, bei dem es sich um einen Trigger handelt, der auf einem Client-Gerät auftritt, um die Ausführung einer Regel zu starten.

**Ereignisentitäten**: Im Zusammenhang mit der Datenmodellierung stellen Ereignisentitäten Konzepte dar, die sich auf Aktionen beziehen, die eine Kundin oder ein Kunde ausführen kann, Systemereignisse oder andere Konzepte, bei denen Sie Änderungen im Laufe der Zeit verfolgen möchten. Entitäten, die unter diese Kategorie fallen, sollten durch Schemata auf Basis der [!DNL XDM ExperienceEvent] dargestellt werden.

**Ereignisse**: Ereignisse sind die Verhaltensdaten, die einem Profil zugeordnet sind.

**Experience-Datenmodell (XDM)** [!DNL Experience Data Model] (XDM) ist ein Open-Source-Framework, das Standardschemata verwendet, um Daten für die Verwendung mit Experience Platform- und Adobe Experience Cloud-Anwendungen zu vereinheitlichen. XDM standardisiert die Datenstruktur und beschleunigt und vereinfacht den Prozess der Gewinnung von Erkenntnissen aus großen Datenmengen.

**Experiment**: Ein Experiment ist der Prozess der Erstellung eines trainierten Modells durch Trainieren der Instanz mit einem Beispielteil von Live-Produktionsdaten. Dies unterscheidet sich von einem trainierten Modell, das mit einem Holdout-Testdatensatz getestet wird. Dies unterscheidet sich auch von dem Konzept eines Experiments in einigen Frameworks für maschinelles Lernen, wo es sich tatsächlich um ein Beispielmodellierungsprojekt handelt.

**Erlebnisereignis**: Ein Erlebnisereignis stellt eine Momentaufnahme des Systems dar, wenn eine Interaktion oder ein Ereignis im Zusammenhang mit einem Kundenerlebnis stattfindet. Erlebnisereignisse sind unveränderliche Faktenaufzeichnungen über das Geschehene und stellen dar, was ohne Aggregation oder Interpretation passiert ist. Im Experience-Datenmodell (XDM) wird dieses Konzept von der [!DNL XDM ExperienceEvent]-Klasse erfasst.

**Vollständige Datei exportieren**: Eine Exportdatei, die eine vollständige Momentaufnahme aller Profilqualifikationen für das ausgewählte Segment enthält.

**Inkrementelle Dateien exportieren**: Eine Reihe exportierter Dateien, bei denen die erste Datei eine vollständige Momentaufnahme aller Profilqualifikationen für das ausgewählte Segment ist und die nachfolgenden Dateien aus den inkrementellen Profilqualifikationen seit dem vorherigen Export bestehen.

**Erweiterung**: Im Kontext von Tags ist eine Erweiterung ein Paket von Funktionen, die einer Tag-Eigenschaft hinzugefügt werden. Eine Erweiterung konzentriert sich in der Regel auf eine bestimmte Marketing- oder Analyselösung und stellt die Tools bereit, die zum Bereitstellen dieser Technologie in einer Client-Umgebung erforderlich sind.

**Erweiterungspaket**: Im Kontext von Tags ist ein Erweiterungspaket eine ZIP-Datei, die von einem Erweiterungsentwickler erstellt und hochgeladen wurde und alles bereitstellt, was Tag-Benutzende benötigen, um die Erweiterung in ihrer Eigenschaft zu installieren. Ein Erweiterungspaket enthält ein Manifest, das Informationen über die Erweiterung, die HTML/JavaScript, die Endbenutzende zum Konfigurieren des Verhaltens der Tag-Erweiterung benötigen, und die ausführbare JavaScript enthält, die an die Client-Umgebung bereitgestellt wird (falls erforderlich).

## F

**Fallback-**: Ein Fallback-Angebot ist das Standardangebot, das angezeigt wird, wenn ein Endbenutzer für keines der Angebote in der verwendeten Sammlung geeignet ist.

**Funktionszuordnung**: Die Funktionszuordnung bezieht sich auf den Prozess der Zuordnung von Funktionen aus Daten in Eingabe- und Zielfunktionen, die für ein Modell für maschinelles Lernen erforderlich sind.

**Feld**: Ein Feld ist das Element auf der untersten Ebene eines Datensatzes, wie im XDM-Schema des Datensatzes definiert. Jedes Feld hat einen Namen für Referenzzwecke und einen -Typ, um den Typ der darin enthaltenen Daten anzugeben. Feldtypen können (aber nicht beschränkt auf) Ganzzahlen, Zahlen, Zeichenfolgen, boolesche Werte und Objekte sein.

**Feldergruppe** Siehe „Schemafeldgruppe“.

**Feldbezeichnungen**: Feldbezeichnungen sind Data-Governance-Bezeichnungen, die entweder von einem Datensatz übernommen oder direkt auf ein Feld angewendet werden.

**Feldname**: Ein Feldname wird verwendet, um in Abfragen und nachgelagerten Services auf den Wert eines Felds zu verweisen.

**Häufigkeit**: In [!DNL Query Service] bestimmt die Häufigkeit, mit der eine wiederkehrende geplante Abfrage ausgeführt wird.

## G

**Geofence**: Ein Geofence ist eine virtuelle geografische Begrenzung, die durch GPS- oder RFID-Technologie definiert wird und es Software ermöglicht, eine Antwort zu Trigger zu senden, wenn ein Mobilgerät in einen bestimmten Bereich eintritt oder diesen verlässt.

**DSGVO (Datenschutz-Grundverordnung)**: Die Datenschutz-Grundverordnung (DSGVO) ist ein Rechtsrahmen, der Richtlinien für die Erfassung und Verarbeitung personenbezogener Daten von Personen innerhalb der Europäischen Union (EU) festlegt. Die DSGVO legt die Grundsätze für die Datenverwaltung und die Rechte des Einzelnen fest und umfasst alle Unternehmen, die mit den Daten von EU-Bürgern arbeiten.

**Leitplanken**: Leitplanken sind Schwellenwerte, die Anhaltspunkte für die Daten- und Systemnutzung, die Leistungsoptimierung und die Vermeidung von Fehlern oder unerwarteten Ergebnissen in Adobe Experience Platform bieten. Leitplanken können sich auf Ihre Nutzung oder Verwendung von Daten und Verarbeitung im Zusammenhang mit Ihren Lizenzierungsberechtigungen beziehen.

## H

**HIPAA**: Das [[!DNL Health Insurance Portability and Accountability Act (HIPAA)]](https://www.hhs.gov/hipaa/index.html) ist ein US-Bundesgesetz, das geschaffen wurde, um die Effizienz der Gesundheitsversorgung zu verbessern, die Übertragbarkeit von Krankenversicherungen zu verbessern und die Privatsphäre von Patienten und Mitgliedern der Krankenversicherung zu schützen. Nach HIPAA haben Einzelpersonen das Recht, auf ihre Informationen zuzugreifen und diese zu ändern und Kopien ihrer Krankenakten oder Gesundheitsinformationen zu erhalten. Gedeckte Unternehmen und Geschäftspartner von gedeckten Unternehmen müssen die HIPAA-Vorschriften einhalten.

**Host**: Im Kontext von Tags gibt ein Host den Speicherort, die Domain und die Benutzeranmeldeinformationen an, die für das System zum Bereitstellen eines Builds erforderlich sind.

**Stündlich**: plant im Kontext geplanter Dateiexporte inkrementelle Dateiexporte alle 3, 6, 8 oder 12 Stunden.

## I

**Identität**: Eine Identität ist eine Kennung, die einen einzelnen Kunden eindeutig repräsentiert, z. B. eine Cookie-ID, eine Geräte-ID oder eine E-Mail-ID.

**Identitätsfelder**: Identitätsfelder sind XDM-Felder, mit denen Informationen über einzelne Kundinnen und Kunden aus mehreren Datenquellen zusammengeführt werden können. Damit das Schema zur Verwendung im Echtzeit-Kundenprofil aktiviert werden kann, muss eine einzelne primäre Identität definiert werden.

**Identitäts-(„I„)-Kennzeichnungen**: Identitäts- („I„)-Datennutzungskennzeichnungen werden verwendet, um Daten zu kategorisieren, mit denen eine bestimmte Person identifiziert oder kontaktiert werden kann.

**Identitätsdiagramm**: Ein Identitätsdiagramm ist eine Zuordnung von Beziehungen zwischen zusammengefügten und verknüpften Identitäten, die für einen einzelnen Kunden vorhanden sind. Jedes Identitätsdiagramm wird nahezu in Echtzeit mit der Kundenaktivität aktualisiert. Die allgemeine Struktur von Identitätsbeziehungen in Ihren Daten wird durch das [!UICONTROL private Diagramm] dargestellt, das als struktureller Blueprint für jedes einzelne Identitätsdiagramm dient.

**Identity-Namespace**: Ein Identity-Namespace definiert den Kontext einer Kennung wie eine E-Mail-Adresse oder eine CRM-ID.

**Identity Service**: [!DNL Experience Platform Identity Service] ermöglicht die Erstellung und Verwaltung von Identitätstypen, sodass Sie Kundenidentitäten geräte- und kanalübergreifend verknüpfen können. Durch die Fähigkeit des Service, Identitäten miteinander zu verknüpfen, kann das Echtzeit-Kundenprofil eine vollständige Darstellung jedes einzelnen Kunden bereitstellen.

**Identitätszuordnung**: Bei der Identitätszuordnung werden Datenfragmente identifiziert und zu einem vollständigen Profildatensatz zusammengefügt.

**Identitätssymbol**: Ein Identitätssymbol ist eine Abkürzung eines Identity-Namespace, der in APIs als Referenz verwendet werden kann.

**Identitätswert**: Ein Identitätswert in Kombination mit einem Identity-Namespace ist eine Kennung, die eine eindeutige Person, ein eindeutiges Unternehmen oder ein eindeutiges Asset darstellt. Bei der Zuordnung von Datensatzdaten zu Profilfragmenten müssen der Namespace und der Identitätswert übereinstimmen.

**I1 Datennutzungskennzeichnung**: Die `I1` Datennutzungskennzeichnung wird zum Klassifizieren von Daten verwendet, mit denen eine bestimmte Person direkt identifiziert oder kontaktiert werden kann, anstatt ein Gerät zu verwenden.

**I2-Datennutzungskennzeichnung**: Die `I2`-Datennutzungskennzeichnung wird verwendet, um Daten zu klassifizieren, die in Kombination mit anderen Daten verwendet werden können, um eine bestimmte Person indirekt zu identifizieren oder zu kontaktieren.

**IMS-Organisation**: Eine IMS-Organisation (manchmal auch als IMS-Organisation bezeichnet) ist der Name, der verwendet wird, um ein Unternehmen oder eine bestimmte Gruppe innerhalb eines Unternehmens über Adobe-Produkte hinweg zu identifizieren. Admins können den Zugriff und die Berechtigungen von Funktionen für Benutzende einer Organisation konfigurieren und verwalten.

**Aufnahme**: Siehe Datenaufnahme.

**Aufnahmezeitplan**: Ein Aufnahmezeitplan bietet zeitbasierte Optionen für die Aufnahme von einer Quelle auf Experience Platform.

**Eingabefunktion**: Eine Eingabefunktion wird in der Funktionszuordnung angegeben und von einem Modell für maschinelles Lernen zur Erstellung von Prognosen verwendet.

**[!DNL Intelligent Services]**: [!DNL Intelligent Services] wie [!DNL Attribution AI] und [!DNL Customer AI] sind Modelle auf Basis von maschinellem Lernen und künstlicher Intelligenz, die Experience Platform (oder auf Platform aufbauende Anwendungen wie Adobe Real-time Customer Data Platform) für die Ausführung und den Betrieb erfordern.

**Interessenbasiertes Targeting oder Personalisierung**: Interessenbasiertes Targeting, auch Personalisierung genannt, findet statt, wenn die folgenden drei Bedingungen erfüllt sind:

1. Die auf der Site gesammelten Daten werden verwendet, um Rückschlüsse auf das Interesse eines Benutzers zu ziehen.
1. Daten werden in einem anderen Kontext verwendet, z. B. auf einer anderen Website oder in einer App (extern).
1. Anhand von Daten wird ausgewählt, welche Inhalte oder Anzeigen auf der Grundlage dieser Rückschlüsse bereitgestellt werden.

## J

**[!DNL JupyterLab]**: Eine Web-basierte Open-Source-Schnittstelle für Project [!DNL Jupyter], die in die Platform-Benutzeroberfläche integriert ist.

**[!DNL Jupyter Notebook]**: Die in JupyterLab integrierten Jupyter Notebooks ermöglichen es Ihnen, Datenbereinigung und -umwandlung, numerische Simulation, statistische Modellierung, Datenvisualisierung, maschinelles Lernen und mehr über Ihre Experience Platform-Daten in einer Vielzahl von Sprachen wie Python, Scala und PySpark durchzuführen.

## K

## L

**LGPD**: Die [[!DNL Lei Geral de Proteção de Dados (LGPD)]](https://gdpr.eu/gdpr-vs-lgpd/) zielt darauf ab, die Verarbeitung personenbezogener Daten aller Einzelpersonen oder natürlichen Personen in Brasilien zu regeln. Das LGPD gibt Brasilianern das Recht, auf ihre personenbezogenen Daten zuzugreifen und sie zu löschen, um zu erfahren, ob (und an wen) ihre personenbezogenen Daten verkauft oder weitergegeben wurden, und das Recht, den Verkauf ihrer Daten an Dritte abzuwählen.

**Library**: Im Kontext von Tags ist eine Bibliothek ein Satz von Geschäftslogik, der Anweisungen enthält, wie sich die Tag-Bibliothek auf dem Client-Gerät verhalten soll.

**Lookup-Entitäten**: Im Kontext der Datenmodellierung stellen Lookup-Entitäten Konzepte dar, die sich auf eine einzelne Person beziehen, aber nicht direkt zur Identifizierung der Person verwendet werden können. Entitäten, die unter diese Kategorie fallen, sollten durch Schemata dargestellt werden, die auf benutzerdefinierten Experience-Datenmodell(XDM)-Klassen basieren, und mit einer Profilentität über eine [Schemabeziehung](../xdm/tutorials/relationship-ui.md) verknüpft sein.

## M

**Maschinelles Lernen (ML)**: Maschinelles Lernen ist der Studienbereich, der es Computern ermöglicht zu lernen, ohne explizit programmiert zu werden.

**Modell für maschinelles Lernen**: Ein Modell für maschinelles Lernen ist eine Instanz eines Rezepts für maschinelles Lernen, das mithilfe von historischen Daten und Konfigurationen trainiert wird, um einen geschäftlichen Anwendungsfall zu lösen. In Adobe Experience Platform Data Science Workspace werden Modelle für maschinelles Lernen als Rezepte bezeichnet.

**Obligatorisches Attribut**: Ein vom Benutzer aktiviertes Kontrollkästchen, das sicherstellt, dass alle Profildatensätze das ausgewählte Attribut enthalten. Beispiel: Alle exportierten Profile enthalten eine E-Mail-Adresse.

**Mapping**: Bei der Datenzuordnung werden Quelldatenfelder mit verwandten Zielfeldern in einem Ziel zugeordnet.

**Marketing-**: Im Data Governance-Framework ist eine Marketing-Aktion (auch als Marketing-Anwendungsfall bezeichnet) eine Aktion, die ein Experience Platform-Datennutzer durchführt und bei der geprüft werden muss, ob Datennutzungsrichtlinien verletzt wurden.

**Zusammenführungsmethode**: Beim Definieren einer Zusammenführungsrichtlinie mithilfe der Platform-Benutzeroberfläche gibt die Zusammenführungsmethode an, wie Datenfragmente bei einem Konflikt priorisiert werden sollen. Wenn Sie die Echtzeit-Kundenprofil-API verwenden, um eine Zusammenführungsrichtlinie zu definieren, wird die Zusammenführungsmethode mithilfe des `attributeMerge`-Objekts bestimmt.

**Zusammenführungsrichtlinie**: Zusammenführungsrichtlinien sind Regeln, mit denen Experience Platform bestimmt, wie Kundendatenfragmente aus mehreren Quellen kombiniert werden, um ein individuelles Profil zu erstellen. Wenn ein Datenkonflikt auftritt, bestimmt die Zusammenführungsrichtlinie, welche Daten für die Aufnahme in das Profil priorisiert werden sollen.

**MHMDA**: Der [[!DNL Washington My Health My Data Act]](https://app.leg.wa.gov/RCW/default.aspx?cite=19.373&amp;full=true) erweitert die Datenschutzrechte für Verbraucher in Bezug auf ihre Gesundheitsdaten. Sie schreibt Offenlegungen, Verbraucherzustimmung und Löschungsrechte für Gesundheitsdaten vor und verbietet den Verkauf von Gesundheitsdaten ohne Genehmigung. Darüber hinaus macht das Gesetz die Verwendung von Geofencing in Gesundheitseinrichtungen rechtswidrig.

**Mixin**: Siehe „Schemafeldgruppe“.

**Module**: Im Kontext von Tags ist ein Modul ein Ausschnitt von ausführbarem JavaScript, der von einer Erweiterung bereitgestellt wird. Dieses führt Aktionen in einer Client-Umgebung aus, ohne eine Regel erstellen zu müssen.

## N

**[!DNL New Zealand Privacy Act]**: Die [[!DNL New Zealand Privacy Act]](https://www.privacy.org.nz/privacy-act-2020/privacy-principles/) kontrolliert, wie Agenturen personenbezogene Daten neuseeländischer Bürger und Organisationen erfassen, verwenden, offenlegen, speichern und zugänglich machen können. Im Jahr 2020 wurden mit der neuesten Version des Gesetzes wesentliche Aktualisierungen dieser Datenschutzgesetze eingeführt, darunter neue Verstöße, die Erhöhung von Geldbußen, obligatorische Benachrichtigungen bei Datenschutzverletzungen und die Erweiterung der Befugnisse des Datenschutzbeauftragten.

**Nicht-Produktions-Sandbox**: Nicht-Produktions-Sandboxes sind Sandboxes, die normalerweise für Entwicklungsexperimente, Tests oder Versuche verwendet werden. Im Gegensatz zu Produktions-Sandboxes können Nicht-Produktions-Sandboxes zurückgesetzt und gelöscht werden.

**[!DNL Notebooks]**: [!DNL Notebooks] werden mit [!DNL Jupyter Notebook] erstellt und können zur Datenanalyse ausgeführt werden.

## O

**Angebot**: Ein Angebot ist eine Marketing-Nachricht, die einen Geschäfts- oder Verkaufsvorschlag für einen (potenziellen) Kunden enthält. Angebote verfügen häufig über spezifische Regeln, die bestimmen, wer für ihre Anzeige oder den Empfang infrage kommt.

**[!DNL Offer Decisioning]**: [!DNL Offer Decisioning] ermöglicht es Marketing-Experten, Regeln und trainierte Modelle von Angebotsvorschlägen zu verwalten, wenn sie mit Endbenutzern interagieren, die auf Daten basieren, die über verschiedene Kanäle und Anwendungen hinweg erfasst wurden.

**Angebotsbibliothek**: Die Angebotsbibliothek ist eine zentrale Bibliothek, die zum Verwalten von personalisierten Angeboten, Fallback-Angeboten, Entscheidungsregeln und Aktivitäten verwendet wird.

**Personalisierungs-Marketing-Aktion für die Site**: Eine Marketing-Aktion, die Daten für die Personalisierung von Inhalten auf der Site verwendet. Bei der Onsite-Personalisierung handelt es sich um alle Daten, die verwendet werden, um Rückschlüsse auf die Interessen der Benutzenden zu ziehen, und um auszuwählen, welche Inhalte oder Anzeigen auf der Grundlage dieser Rückschlüsse bereitgestellt werden.

**Targeting-Marketing-Aktion auf der Site**: Eine Marketing-Aktion, die Daten für Onsite-Anzeigen verwendet, einschließlich der Auswahl und Bereitstellung von Anzeigen auf den Websites oder in Programmen Ihres Unternehmens oder zur Messung der Bereitstellung und der Effektivität solcher Anzeigen.

**Einmal**: plant im Kontext geplanter Dateiexporte einen einmaligen, bedarfsgesteuerten, vollständigen Dateiexport.

**Speicherstrategie überschreiben**: Die Speicherstrategie „Überschreiben“ ist eine Option für die Aufnahme von Drittanbieterdaten über eine Verbindung, bei der Sie angeben können, ob die aufgenommenen Daten nach einem bestimmten Zeitplan überschrieben werden.

## P

**Partielle Aufnahme**: Die partielle Aufnahme ermöglicht die Aufnahme gültiger Datensätze von Batch-Daten innerhalb eines bestimmten Fehlerschwellenwerts. Die Fehlerdiagnose für fehlgeschlagene Datensätze kann unter Übersicht über die Datenflussausführung [!UICONTROL Überwachung] oder [!UICONTROL Quellen] heruntergeladen oder aufgerufen werden.

**Parquet-Dateien**: Eine Parquet-Datei ist ein säulenförmiges Speicherdateiformat mit komplexen verschachtelten Datenstrukturen. Parquet-Dateien sind erforderlich, um Daten zum Ausfüllen eines Schemadatensatzes hinzuzufügen.

**PDPA**: Die [[!DNL Personal Data Protection Act (PDPA)]](https://www.pdpc.gov.sg/Overview-of-PDPA/The-Legislation/Personal-Data-Protection-Act) wurde eingeführt, um thailändische Dateninhaber vor der illegalen Sammlung, Verwendung oder Offenlegung ihrer personenbezogenen Daten zu schützen. Auf Grundlage der DSGVO der Europäischen Union räumt die Verordnung thailändischen Bürgern das Recht ein, Auskunft über ihre gespeicherten personenbezogenen Daten oder deren Löschung zu verlangen.

<!-- Not yet released
**PDPD**: The [[!DNL Personal Data Protection Decree] (PDPD) 
-->

**Personalisierte Angebote**: Ein personalisiertes Angebot ist eine anpassbare Marketing-Nachricht, die auf Eignungsregeln und Einschränkungen basiert.

**Platzierungen**: Eine Platzierung ist der Speicherort und/oder Kontext, in dem ein Angebot für Endbenutzende erscheint.

**Arbeitsbereich Richtlinien**: Ein Arbeitsbereich in der Platform-Benutzeroberfläche, mit dem Datenverantwortliche Datennutzungsbeschriftungen und -richtlinien für Ihr Unternehmen anzeigen und verwalten können.

**Richtlinie**: Eine Datennutzungsrichtlinie ist eine Regel, die Marketing-Aktionen angibt, die aufgrund der Anwendung von Nutzungskennzeichnungen auf Platform-Daten eingeschränkt sind.

**Richtliniendurchsetzung**: Ermöglicht die Durchsetzung von Datennutzungsrichtlinien mit angewendeten Marketing-Aktionen, um Datenvorgänge zu verhindern, die Richtlinienverletzungen innerhalb einer Organisation darstellen.

**Primärer Schlüssel**: Ein Primärschlüssel ist eine Bezeichnung in einem Schema, um alle Datensätze eindeutig zu identifizieren.

**Priorität**: In [!DNL Offer Decisioning] wird die Priorität verwendet, um Angebote zu reihen, die alle Einschränkungen wie Eignung, Kalender und Begrenzung erfüllen.

**Privates Identitätsdiagramm**: Das private Identitätsdiagramm (manchmal auch als privates Diagramm bezeichnet) ist eine private Zuordnung von Beziehungen zwischen zusammengefügten und verknüpften Identitäten, die auf Grundlage Ihrer Erstanbieter-Daten erstellt wird und nur für Ihre Organisation sichtbar ist. Für jede Organisation gibt es nur ein privates Diagramm, das als struktureller Blueprint für die individuellen Identitätsdiagramme dient, die für jeden Kunden generiert werden, der mit Ihrer Marke interagiert.

**Produktprofil**: Mit Produktprofilen können Admins Benutzerzugriff auf alle oder einen Teil der mit dem Experience Platform verbundenen Services gewähren.

**Produktions-Sandbox**: Eine Produktions-Sandbox ist eine Sandbox für die Verwendung in Ihrer Produktionsumgebung. Im Gegensatz zu Nicht-Produktions-Sandboxes können Produktions-Sandboxes nicht zurückgesetzt oder gelöscht werden.

**Profil**: Nicht zu verwechseln mit dem Echtzeit-Kundenprofil als Service, ist ein Profil eine vollständige Darstellung eines einzelnen Kunden, die aus zusammengeführten Datensatz- und Zeitreihendaten aus mehreren Quellen erstellt wird.

**Profilzugriff**: Der `/entities`-Endpunkt in der Echtzeit-Kundenprofil-API ermöglicht den Zugriff auf Datensatzdaten und Zeitreihenereignisse im Profildatenspeicher. Siehe auch: Profilentitäten

**Profildaten**: Profildaten beziehen sich auf alle Daten, die sich im Profildatenspeicher befinden.

**Profildatenspeicher**: Der Profildatenspeicher (manchmal auch als Profilspeicher bezeichnet) ist ein vom Data Lake separates Datenspeichersystem, das vom Echtzeit-Kundenprofil zum Erstellen und Speichern von Profilen verwendet wird.

**Profilentitäten**: Profilentitäten stellen Attribute dar, die sich auf eine einzelne Person beziehen, normalerweise eine Kundin oder einen Kunden. Entitäten, die unter diese Kategorie fallen, sollten durch Schemata auf Basis der [!DNL XDM Individual Profile] dargestellt werden. Siehe auch: Profilzugriff

**Profilexport**: [!DNL Profile] Export ist einer von zwei Zieltypen in Experience Platform. [!DNL Profile] Export generiert eine Datei mit Profilen und Attributen und verwendet rohe PII-Daten mit E-Mail, um sie in Marketing- und E-Mail-Automatisierungsplattformen zu integrieren.

**Profilfragment**: Ein Profilfragment sind die Profilinformationen für nur eine Identität aus der Liste der Identitäten, die für einen bestimmten Kunden vorhanden sind.

**Profil-ID**: Eine Profil-ID ist eine automatisch generierte Kennung, die mit einem Identitätstyp verknüpft ist und ein Profil darstellt.

**Property**: Im Kontext von Tags ist eine Eigenschaft ein Container für alles, was zum Bereitstellen eines Satzes von Tags erforderlich ist.

## Q

**Abfrage**: Abfragen sind Anfragen nach Daten aus Datenbanktabellen.

**Abfrage-Editor**: Der Abfrage-Editor ist ein Tool zum Schreiben, Validieren und Senden von SQL-Anweisungen in [!DNL Query Service].

## R

**Real-time Customer Data Platform**: Adobe Real-time Customer Data Platform (Real-Time CDP) führt bekannte und unbekannte Kundendaten zusammen, um vertrauenswürdige Kundenprofile mit vereinfachter Integration, intelligenter Segmentierung und Echtzeit-Aktivierung auf der gesamten digitalen Kunden-Journey zu erstellen.

**Echtzeit-Kundenprofil**: Das Echtzeit-Kundenprofil (manchmal auch als Profil bezeichnet) bietet eine ganzheitliche Sicht auf jeden einzelnen Kunden, indem es Daten aus mehreren Kanälen, einschließlich Online-, Offline-, CRM- und Drittanbieter-Daten, kombiniert. Mit dem Profil können Sie Ihre Kundendaten in individuellen Profilen zusammenführen, die aussagekräftige, im Zeitverlauf gezeichnete Berichte für jede Kundeninteraktion bieten.

**Rezept**: Ein Rezept ist ein Adobe-Begriff für eine Modellspezifikation und ein Container auf oberster Ebene, der bestimmte Prozesse für maschinelles Lernen, KI-Algorithmen, Verarbeitungslogik und Konfigurationsparameter darstellt, die zum Erstellen und Ausführen eines trainierten Modells und somit zur Lösung spezifischer Geschäftsprobleme erforderlich sind.

**Datensatz**: Ein Datensatz sind Daten, die als Zeilen in einem Datensatz bestehen bleiben.

**Aufzeichnen von Daten**: Stellt Informationen zu den Attributen eines Subjekts bereit. Ein Subjekt könnte eine Organisation oder eine Einzelperson sein.

**Wiederholung**: In [!DNL Query Service] definiert eine Wiederholung, ob eine Abfrage so geplant ist, dass sie nur einmal oder wiederkehrend ausgeführt wird.

**Darstellung**: In [!DNL Offer Decisioning] handelt es sich bei einer Darstellung um Informationen, die von einem Kanal zur Anzeige eines Angebots verwendet werden, z. B. Ort oder Sprache.

**Ressource**: Im Kontext von Tags ist eine Ressource ein generischer Begriff, der auf Optionen verweist, die der Tag-Benutzer in der Client-Umgebung konfigurieren kann, einschließlich Erweiterungen, Datenelementen und Regeln.

**Rollenbasierte Zugriffssteuerung**: Die rollenbasierte Zugriffssteuerung ermöglicht es Admins, Benutzenden von Experience Platform Zugriff und Berechtigungen zuzuweisen. Zu den Berechtigungen gehört die Möglichkeit, Experience Platform-Funktionen anzuzeigen und/oder zu verwenden, z. B. das Erstellen von Sandboxes, das Definieren von Schemas und das Verwalten von Datensätzen.

**Regel**: Im Kontext von Tags ist eine Regel eine Sammlung von Komponenten, die einen bestimmten Satz von Ereignissen, Bedingungen und Aktionen definieren, die logisch gruppiert werden sollten.

**Regelkomponente**: Im Kontext von Tags sind Regelkomponenten die Ereignisse, Bedingungen und Aktionen, aus denen eine Regel besteht.

**Runtime**: Runtime gibt eine Laufzeitumgebung für ein Rezept für maschinelles Lernen an. Mit den Laufzeiten von [!DNL Python], R, [!DNL Spark], PySpark und TensorFlow können Sie eine URL zu einem Docker-Image für eine Rezeptquelle eingeben.

## S

**Beispieldaten**: Beispieldaten sind eine Vorschau einer Datendatei, normalerweise der ersten 100 Zeilen, die einem Datenwissenschaftler oder -ingenieur eine Vorstellung davon liefert, welches Schema oder welche Daten sich in der Datendatei befinden.

**Sandbox**: Eine Sandbox ist ein virtuelles Konstrukt, das eine einzelne Platform-Instanz in eine separate virtuelle Umgebung unterteilt, um die Entwicklung und Weiterentwicklung von Programmen für digitale Erlebnisse zu erleichtern.

**Sandbox zurücksetzen**: Beim Zurücksetzen einer Sandbox werden alle Daten, einschließlich Daten, Profile und Segmente, in einer Sandbox gelöscht. Das Zurücksetzen von Sandboxes kann sich auf Daten auswirken, die mit internen oder externen Zielen verbunden sind.

**Sandbox Switcher**: Das Sandbox Switcher-Steuerelement in Experience Platform ermöglicht Benutzenden das Navigieren zwischen Sandboxes, auf die sie Zugriff haben. Durch das Wechseln einer Sandbox werden alle Inhalte geändert und der Funktionszugriff kann je nach Berechtigungen geändert werden.

**Zeitplan**: Ein Zeitplan ist eine benutzerdefinierte Spezifikation für die Häufigkeit oder Kadenz der Datenaufnahme aus einer Datenquelle eines Drittanbieters in Adobe Experience Platform.

**Scoring**: Beim Scoring werden mithilfe eines trainierten Modells Insights aus Daten generiert.

**Schema**: Ein Schema ist ein Satz von Regeln, die die Struktur und das Format von Daten darstellen und überprüfen. Ein Schema besteht aus einer Klasse und optionalen Feldergruppen und wird zum Erstellen von Datensätzen und Datenströmen verwendet. Ein Schema kann Verhaltensattribute, Zeitstempel, Identitäten, Attributdefinitionen, Beziehungen und mehr enthalten.

**Schemafeldgruppe**: Im Experience-Datenmodell (XDM) ermöglicht eine Schemafeldgruppe es Benutzenden, wiederverwendbare Felder zu erweitern, um ein oder mehrere Attribute zu definieren, die in ein Schema aufgenommen werden sollen.

**Schemabibliothek**: Die Schemabibliothek enthält XDM-Ressourcen, die dem Branchenstandard entsprechen und per Adobe bereitgestellt werden, sowie benutzerdefinierte Ressourcen, die von Ihrem Unternehmen definiert wurden.

**Schemaregistrierung**: Die Schemaregistrierung bietet eine Benutzeroberfläche und eine RESTful-API, mit der alle Schema-bezogenen Ressourcen in der Schemabibliothek angezeigt und verwaltet werden.

**Geheimer Zugriffsschlüssel**: Ein geheimer Zugriffsschlüssel ist ein [!DNL Amazon] S3-Schlüssel, der zusammen mit der Zugriffsschlüssel-ID zum Signieren von AWS-Anfragen verwendet wird.

**Segment**: Ein Segment ist ein Regelsatz, der Attribute und Ereignisdaten enthält, die eine Reihe von Profilen als Zielgruppe qualifizieren.

**Segment Builder**: Die [!DNL Segment Builder] ist eine visuelle Entwicklungsumgebung zum Erstellen von Segmentdefinitionen. Es dient als gemeinsame Komponente aller Anwendungen, die den Experience Platform-Segmentierungs-Service verwenden.

**Segmentdefinition**: Eine Segmentdefinition ist der Regelsatz, mit dem die wichtigsten Merkmale oder das Verhalten einer Zielgruppe beschrieben werden. Nach der Erstellung einer Segmentdefinition werden die darin beschriebenen Regeln zur Bestimmung qualifizierter Zielgruppenmitglieder für ein Segment verwendet.

**Segmentauswertungsmethode**: Es gibt zwei Segmentauswertungsmethoden: Geplant und On-Demand. Die geplante Auswertung ermöglicht einen wiederkehrenden Zeitplan für die Ausführung eines Exportvorgangs zu einem bestimmten Zeitpunkt, während die On-Demand-Auswertung die Erstellung eines Segmentvorgangs beinhaltet, um die Zielgruppe sofort zu erstellen.

**Segmentexport**: Der Segmentexport ist einer der beiden Zieltypen in Experience Platform. Mit dem Segmentexport können Sie die Profile, die sich qualifizieren und dem Ziel zugeordnet wurden, senden. Verwendet Segment- und Benutzer-IDs sowie pseudonyme Daten und lässt sich in der Regel in soziale Netzwerke und andere Zielplattformen für digitale Medien integrieren.

**Segment-ID**: Eine Segment-ID ist eine automatisch generierte Kennung, die mit einem Segment verknüpft ist.

**Segmentzugehörigkeit**: Die Segmentzugehörigkeit zeigt an, zu welchen Segmenten ein Profil derzeit gehört.

**Segmentregeln**: Segmentregeln definieren die Bedingungen, die bestimmen, ob ein Profil für ein Segment geeignet ist.

**Segmentierung**: Bei der Segmentierung wird eine große Gruppe von Kunden, Interessenten oder Verbrauchern in kleinere Gruppen aufgeteilt, die ähnliche Attribute aufweisen und ähnlich auf bestimmte Marketing-Strategien reagieren.

**Sensei ML Framework**: Sensei ML Framework ist ein einheitliches Framework für maschinelles Lernen (ML), das Experience Platform-Daten nutzt, um Datenwissenschaftler in die Lage zu versetzen, ML-gesteuerte Intelligenz-Services schneller, skalierbar und wiederverwendbar zu entwickeln.

**Sensibel („S„)-Kennzeichnungen**: Sensibel („S„)-Kennzeichnungen werden verwendet, um als sensibel eingestufte Daten zu kategorisieren, z. B. verschiedene Typen von Verhaltens- oder geografischen Daten, die als sensibel markiert werden sollen.

**Services**: Ein leistungsstarkes Framework zur Operationalisierung von KI- und ML-Services mithilfe von Adobe Intelligent Services. Services bieten personalisierte Kundenerlebnisse in Echtzeit oder operationalisieren benutzerdefinierte Intelligent Services.

**Marketing-Aktion für Einzelidentitätspersonalisierung**: Eine Marketing-Aktion, die Daten für die Personalisierung von Inhalten auf der Site verwendet. Bei der Onsite-Personalisierung geht es um alle Daten, die verwendet werden, um Rückschlüsse auf die Interessen der Benutzer zu ziehen, und darum, auszuwählen, welche Inhalte oder Anzeigen auf der Grundlage dieser Rückschlüsse bereitgestellt werden.

**S1-Datennutzungskennzeichnung**: Eine `S1`-Datennutzungskennzeichnung wird verwendet, um Daten zu klassifizieren, die den Breiten- und Längengrad angeben und zur Bestimmung des genauen Standorts eines Geräts verwendet werden können.

**S2-Datennutzungskennzeichnung**: Eine `S2` Datennutzungskennzeichnung wird zum Klassifizieren von Daten verwendet, die zur Bestimmung eines grob definierten Geofence-Bereichs verwendet werden können.

**Source**: Eine Quelle ist ein allgemeiner Begriff für jeden Eingabe-Connector in Platform. Siehe auch: Source-Connector

**Source-**: Ein Quellattribut ist ein Feld im Quelldatensatz. Source-Attribute werden Zielschemafeldern zugeordnet.

**Source-**: Der Quellkatalog ist die Liste der verfügbaren Quell-Connectoren auf Experience Platform.

**Source-Kategorie**: Eine Quellkategorie ist eine Gruppierung von Quellen mit ähnlichen Eigenschaften.

**Source-Connector**: Source-Connectoren (auch als Quellen bezeichnet) helfen Benutzenden, Daten aus mehreren Quellen einfach aufzunehmen, wodurch die Strukturierung, Beschriftung und Optimierung von Daten mithilfe von Experience Platform-Services ermöglicht wird. Daten können aus einer Vielzahl von Quellen aufgenommen werden, z. B. aus Cloud-basiertem Speicher, Software von Drittanbietern und CRM-Systemen.

**Streaming-Verbindung**: Eine Streaming-Verbindung ist ein eindeutiger Endpunkt, der von Adobe bereitgestellt und an Ihr Unternehmen gebunden wird, um Daten in Experience Platform zu streamen.

**Standard-Identity-Namespace**: Standard-Identity-Namespaces sind vordefinierte Identity-Namespaces, die von Adobe bereitgestellt werden. Hierbei handelt es sich um branchenübliche Lösungen, mit denen Kunden identifiziert werden können.

**Streaming-Aufnahme**: Mit der Streaming-Aufnahme können Sie Daten von Client- und Server-seitigen Geräten in Echtzeit an Experience Platform senden.

**Streaming-**: Die Streaming-Segmentierung ist ein fortlaufender Datenauswahlprozess, der Segmente infolge von Benutzeraktivitäten aktualisiert. Nachdem ein Segment erstellt und gespeichert wurde, wird die Segmentdefinition auf in [!DNL Real-Time Customer Profile] eingehende Daten angewendet. Segmenthinzufügungen und -entfernungen werden regelmäßig verarbeitet, um sicherzustellen, dass Ihre Zielgruppe relevant bleibt.

**Systemansicht**: Die Systemansicht ist eine visuelle Darstellung von Quelldatensätzen, die [!DNL Real-Time Customer Profile] zu Zielen durchlaufen.

## T

**Tags**: In Adobe Experience Platform bieten Tags Tools zum Bereitstellen, Vereinheitlichen und Verwalten von Analyse-, Marketing- und Werbeintegrationen, die für relevante Kundenerlebnisse auf allen Client-Geräten erforderlich sind.

**Target-Funktionen**: Beim Feature Mapping ist ein Target-KE das KE, das von einem Modell vorhergesagt wird.

**Zeitreihendaten**: Zeitreihendaten liefern eine Momentaufnahme des Systems zum Zeitpunkt, zu dem eine Aktion entweder direkt oder indirekt von einem Datensatzsubjekt durchgeführt wurde.

**Trainiertes Modell**: Ein trainiertes Modell stellt die ausführbare Ausgabe eines Modell-Trainings-Prozesses dar, bei dem ein Satz von Trainings-Daten auf die Modellinstanz angewendet wurde. Ein trainiertes Modell behält einen Verweis auf jeden Intelligent Web Service bei, der daraus erstellt wird. Ein trainiertes Modell eignet sich für die Bewertung und Erstellung eines intelligenten Web-Services.

**Token**: Ein Token ist eine Art von Zwei-Faktor-Authentifizierungssicherheit, die zum Autorisieren der Verwendung von Computerdiensten mit [!DNL Query Service] verwendet werden kann.

## U

**UCPA**: Die [[!DNL Utah Consumer Privacy Act]](https://le.utah.gov/~2022/bills/static/SB0227.html) begründet das Recht eines Verbrauchers zu wissen, welche personenbezogenen Daten ein Unternehmen erhebt, wie das Unternehmen seine personenbezogenen Daten verwendet und ob das Unternehmen seine personenbezogenen Daten verkauft. Verbraucher können von dem Unternehmen verlangen, ihre personenbezogenen Daten zu löschen oder nicht mehr zu verkaufen.

**Vereinigungsschema**: Ein Vereinigungsschema ist eine Konsolidierung von Schemata, die dieselbe Klasse aufweisen und für die [!DNL Real-Time Customer Profile] aktiviert wurden. Für eine Organisation können mehrere Vereinigungsschemata vorhanden sein, es kann jedoch nur ein Vereinigungsschema pro Klasse geben.

## V

**VCDPA**: Der [[!DNL Virginia Consumer Data Protection Act (VCDPA)]](https://lis.virginia.gov/cgi-bin/legp604.exe?212+sum+HB2307) bietet neuen Datenschutzrechten für Einwohner Virginias („Verbraucher„), einschließlich des Rechts auf Zugriff, Löschung und Berichtigung personenbezogener Daten. Verbraucher haben auch das Recht, dem Verkauf personenbezogener Daten, dem auf personenbezogenen Daten basierenden Profiling und der Verarbeitung von personenbezogenen Daten für Werbezwecke zu widersprechen.

## W

## X

**XDM**: Siehe Experience-Datenmodell (XDM).

**XDM-Entscheidungsereignis**: XDM-Entscheidungsereignis ist eine zeitreihenbasierte Klasse, mit der Beobachtungen zum Ergebnis und Kontext einer Entscheidungsaktivität erfasst werden. Dazu gehören Informationen darüber, wie die Entscheidung getroffen wurde, wann sie stattfand, welche Optionen vorgeschlagen (und ausgewählt) wurden und welcher kontextuelle Zustand bestand, der entweder die Entscheidung beeinflusste oder während des Entscheidungsprozesses beobachtet werden konnte.

**XDM ExperienceEvent**: XDM ExperienceEvent ist eine zeitreihenbasierte Klasse, mit der der Status des Systems beim Auftreten eines Ereignisses (oder einer Reihe von Ereignissen) erfasst wird, einschließlich des Zeitpunkts und der Identität des betroffenen Subjekts. Siehe auch: Erlebnisereignis

**XDM Individual Profile**: XDM [!DNL Individual Profile] ist eine auf einem Datensatz basierende Klasse, die eine einzige Repräsentation der Attribute sowohl identifizierter als auch teilweise identifizierter Subjekte bildet. Hochgradig identifizierte Profile können für die persönliche Kommunikation oder zielgerichtete Interaktionen verwendet werden und detaillierte persönliche Informationen wie Name, Geschlecht, Geburtsdatum, Ort und Kontaktinformationen, einschließlich Telefonnummern und E-Mail-Adressen, enthalten.

**XDM-System**: Das XDM-System stellt das Framework dar, das XDM-Schemata zur Verwendung in nachgelagerten Experience Platform-Services operationalisiert.

## Y

## Z
