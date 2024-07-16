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

# Glossar zu Adobe Experience Platform {#adobe-experience-platform-glossary}

## A

**Zugriffskontrolle**: Rollenbasierte Zugriffskontrolle ermöglicht Administratoren die Zuweisung von Zugriff und Berechtigungen an Benutzer von Experience Platform. Zu den Berechtigungen gehört die Möglichkeit, Experience Platform-Funktionen anzuzeigen und/oder zu verwenden, z. B. das Erstellen von Sandboxes, das Definieren von Schemas und das Verwalten von Datensätzen.

**Zugriffsschlüssel-ID**: Eine Zugriffsschlüssel-ID ist eine eindeutige Kennung, die mit einem geheimen Zugriffsschlüssel des Typs [!DNL Amazon] S3 verknüpft ist. Die Zugriffsschlüssel-ID und der geheime Zugriffsschlüssel werden zusammen verwendet, um [!DNL Amazon Web Services] (AWS)-Anfragen zu signieren.

**Aktion**: Im Kontext von Tags ist eine Aktion ein bestimmter Typ von Regelkomponente, der definiert, was geschehen soll, nachdem ein Ereignis auftritt und Bedingungen ausgewertet und weitergegeben werden.

**Aktivieren**: Activate ist die Aktion, die ein Benutzer durchführt, um ein Segment oder Profile einem Ziel wie [!DNL Oracle Eloqua], [!DNL Google] oder [!DNL Salesforce Marketing Cloud] zuzuordnen.

**Aktivität**: In [!DNL Offer Decisioning] enthält eine Aktivität die Logik, die über die Auswahl eines Angebots informiert.

**Administrator**: Mindestens eine Person in Ihrem Unternehmen, die Berechtigungen für das Experience Platform in Adobe Admin Console konfigurieren und anpassen kann.

**Adobe Admin Console**: Adobe Admin Console bietet einen zentralen Speicherort für die Verwaltung von Adobe-Produktberechtigungen und den Zugriff für Ihr Unternehmen. Über die Konsole können Administratoren Benutzergruppen Zugriffsberechtigungen für verschiedene Platform-Funktionen erteilen, z. B. &quot;Datensätze verwalten&quot;, &quot;Datensätze anzeigen&quot;oder &quot;Profile verwalten&quot;.

**Adobe Experience Platform**: Adobe Experience Platform standardisiert Daten und Inhalte im gesamten Unternehmen, ermöglicht Echtzeit-Kundenprofile, ermöglicht Datenwissenschaft und beschleunigt Content Velocity, um die Personalisierung von Erlebnissen auf der gesamten Journey zu fördern.

**Adobe Experience Platform Query Service**: Ermöglicht es Datenanalysten, Ereignisse und Profile zur Verwendung in Analysen und maschinellem Lernen abzufragen. Mit Query Service können Datenwissenschaftler und Analytiker alle in Experience Platform gespeicherten Datensätze abrufen (einschließlich Verhaltensdaten sowie Point-of-Sale (POS), Customer Relationship Management (CRM) usw.) und diese Datensätze abfragen, um spezifische Fragen zu den Daten zu beantworten.

**Adobe Experience Platform Segmentation Service**: Ermöglicht das Erstellen von Segmenten und das Generieren von Zielgruppen aus Ihren Echtzeit-Kundenprofildaten. Diese Zielgruppen können dann in ihre eigenen Datensätze im Data Lake exportiert werden.

**Adobe Intelligent Services**: Intelligente Dienste wie Attribution AI und Customer AI sind auf maschinellem Lernen basierende Modelle mit künstlicher Intelligenz, die speziell für den Betrieb und Betrieb von Experience Platform entwickelt wurden.

**Adobe I/O**: Adobe I/O ist Teil von Experience Platform und bietet allen Entwicklern Zugriff auf alle Funktionen, die zur Integration, Erweiterung und Anpassung von Plattformen erforderlich sind, einschließlich APIs, Ereignissen, Entwicklerkonsole und hilfreicher Tools.

**Adobe Sensei**: Adobe Sensei ist das intelligente Framework, das Experience Platform steuert. Es bietet außerdem eine Reihe von KI-Diensten, mit denen Marken ihre Fähigkeit verbessern können, personalisierte Echtzeit-Kundenerlebnisse bereitzustellen.

**Amazon S3 Bucket**: [!DNL Amazon S3] Behälter sind die grundlegenden Container für Daten, die im 3} -Ökosystem gespeichert sind. [!DNL Amazon] Buckets enthalten Objekte. Jedes Objekt wird mit einem eindeutigen Schlüssel gespeichert und abgerufen, der dem Entwickler zugewiesen ist.

**Amazon S3-Connector**: Der [!DNL Amazon] S3-Connector ermöglicht Kunden von Experience Platform, eine sichere Verbindung herzustellen und auf ihre [!DNL Amazon] S3-Daten zuzugreifen.

**APA**: Der [[!DNL Australia Privacy Act (Privacy Act)]](https://www.oaic.gov.au/privacy/the-privacy-act) fördert und schützt die Privatsphäre von Einzelpersonen und regelt, wie Behörden und Organisationen der australischen Regierung mit personenbezogenen Daten umgehen. Der [!DNL Privacy Act] enthält Grundsätze, die für Organisationen des privaten Sektors gelten. So haben Einzelpersonen beispielsweise das Recht zu verstehen, warum die personenbezogenen Daten erfasst und wie sie verwendet werden, und die Möglichkeit, auf ihre Daten zuzugreifen, sie zu löschen und ihre personenbezogenen Daten zu korrigieren.

**Speicherstrategie anhängen**: Die Speicherstrategie &quot;anhängen&quot;ist eine Option, die verwendet wird, wenn Drittanbieterdaten angegeben werden, die über eine Verbindung aufgenommen werden sollen, und neue Daten oder Zeilen am Ende des Datensatzes angehängt werden. Die zuvor aufgenommenen Zeilen bleiben unberührt und nur Zeilen, die seit der letzten geplanten Ausführung erstellt wurden, werden in Experience Platform aufgenommen. Alle Zeilen, die im Quellsystem geändert wurden, bleiben beim Experience Platform unverändert.

**Array**: Arrays werden für geordnete Elemente mit demselben Datentyp verwendet.

**Künstliche Intelligenz**: Künstliche Intelligenz ist eine Theorie und Entwicklung von Computersystemen, die Aufgaben erledigen können, die normalerweise menschliche Intelligenz erfordern, wie visuelle Wahrnehmung, Spracherkennung, Entscheidungsfindung und Übersetzung zwischen Sprachen.

**Attribute**: Attribute sind angegebene Eigenschaften, die ein Profil darstellen.

**Attributzusammenführung**: Beim Definieren einer Zusammenführungsrichtlinie mithilfe der Echtzeit-Kundenprofil-API gibt das `attributeMerge` -Objekt an, wie die Zusammenführungsrichtlinie Profilattribute bei Datenkonflikten priorisiert. Dies entspricht der Auswahl einer [!UICONTROL Zusammenführungsmethode] beim Definieren einer Zusammenführungsrichtlinie in der Platform-Benutzeroberfläche.

**Attribution AI**: [!DNL Attribution AI] ist ein intelligenter Dienst auf Basis von Adobe Sensei, der algorithmische Mehrkanalzuordnungsfunktionen über den gesamten Kundenlebenszyklus hinweg bietet.

**Zielgruppe**: Eine Zielgruppe ist der resultierende Satz von Profilen, die den Kriterien einer Segmentdefinition entsprechen.

**Zielgruppengröße**: Eine Zielgruppengröße ist die Gesamtanzahl der Profile, die den Kriterien einer Segmentdefinition entsprechen und für die Zielgruppenzugehörigkeit qualifiziert sind.

**Zielgruppen-Schnappschuss**: Eine Zielgruppen-Momentaufnahme erfasst alle Profile, die zum Zeitpunkt der Segmentierung für die Segmentkriterien qualifiziert sind.

## B

**Aufstockung**: Für geplante Quellen ermöglicht die Aufstockungsoption die Erfassung historischer Daten.

**Aufstockungszeitraum**: Der Aufstockungszeitraum ist eine Option zum Festlegen der Zeitdauer für die Aufnahme von historischen Daten von Drittanbietern über eine Quellverbindung. Wenn Sie einen Aufstockungszeitraum von &quot;für immer&quot;wählen, wird der gesamte Verlauf der Quelldaten auf Experience Platform erfasst.

**Batch**: Ein Batch ist ein Datensatz, der über einen bestimmten Zeitraum erfasst und als einzelne Einheit verarbeitet wird. Datensätze bestehen aus mehreren Batches.

**Batch-Kennung**: Eine Batch-Kennung ist eine vom Adobe generierte Kennung für einen DatenBatch.

**Batch-Erfassung**: Mit der Batch-Erfassung können Sie Daten als Batch-Dateien in Experience Platform erfassen. Batches sind Dateneinheiten, die aus einer oder mehreren Dateien bestehen, die als Einheit erfasst werden sollen.

**Batch-Segmentierung**: Die Batch-Segmentierung ist eine Alternative zu einem fortlaufenden Datenauswahlprozess und verschiebt alle Profildaten gleichzeitig über Segmentdefinitionen, um entsprechende Zielgruppen zu erstellen. Nach der Erstellung wird dieses Segment gespeichert und kann exportiert werden.

**Erstellen**: Im Kontext von Tags ist ein Build eine Datei oder ein Dateisatz, die bzw. der alle Konfigurationen und den Code enthält, die zum Ausführen der Geschäftslogik in einer Bibliothek erforderlich sind, sodass Sie diese Bibliothek auf Ihrer Website oder in Ihrer mobilen App bereitstellen können.

**Business Intelligence-Tools**: Business Intelligence-Tools (BI) sind in erster Linie in [!DNL Experience Platform Query Service] integriert. BI-Tools sind Typen von Anwendungs-Software, die große Mengen unstrukturierter Daten aus internen und externen Systemen erfassen und verarbeiten.

## C

**Begrenzung**: In [!DNL Offer Decisioning] wird bei Entscheidungsregeln eine Begrenzung (auch als Frequenzlimitierung bezeichnet) verwendet, um festzulegen, wie oft ein Angebot unterbreitet wird. Es gibt zwei Arten von Begrenzungen: wie oft ein Angebot für die kombinierte Zielgruppe vorgeschlagen werden kann (als &quot;globale Begrenzung&quot;bezeichnet) und wie oft ein Angebot demselben Endbenutzer vorgeschlagen werden kann (als &quot;Profilbegrenzung&quot;bezeichnet).

**Katalog**: Im Kontext von Quellen und Zielen ist ein Katalog eine Galerie mit verfügbaren Verbindungen zu Adobe-Anwendungen und Drittanbietertechnologien. Nicht zu verwechseln mit [!DNL Catalog Service].

**[!DNL Catalog Service]**: [!DNL Catalog Service] (manchmal auch als [!DNL Catalog] bezeichnet) ist das Aufzeichnungssystem für Speicherort und Herkunft von Daten in Adobe Experience Platform. Während alle Daten, die in Experience Platform aufgenommen werden, als Dateien und Ordner im Data Lake gespeichert sind, enthält [!DNL Catalog] die Metadaten und Beschreibungen dieser Dateien und Ordner für Such-, Überwachungs- und Data-Governance-Zwecke.

**CCPA**: Der [[!DNL California Consumer Privacy Act (CCPA)]](https://oag.ca.gov/privacy/ccpa) verbessert die Datenschutzrechte und den Verbraucherschutz für Einwohner von Kalifornien (USA). Der CCPA bietet neue Datenschutzrechte für Einwohner Kaliforniens, einschließlich des Rechts, auf ihre personenbezogenen Daten zuzugreifen und sie zu löschen, um zu erfahren, ob ihre personenbezogenen Daten verkauft oder weitergegeben werden (und an wen), und das Recht, sich gegen den Verkauf ihrer Daten an Dritte zu entscheiden.

**Klasse**: Im Experience-Datenmodell (XDM) definiert eine Klasse den kleinsten Satz von Feldern, die zum Erstellen eines Schemas verwendet werden, und definiert das Basisverhalten des Geschäftsobjekts, das das Schema darstellt.

**Client**: Ein Client ist ein externes Tool oder eine externe Anwendung, das bzw. die eine Verbindung zu [!DNL Query Service] über das Protokoll [!DNL PostgreSQL] oder die HTTP-API herstellt.

**Sammlung**: In [!DNL Offer Decisioning] sind Sammlungen Untergruppen von Angeboten, die auf von einem Marketing-Experten vordefinierten Bedingungen basieren, z. B. der Kategorie des Angebots.

**Kombinieren mit PII-Marketing-Aktion**: Eine Marketing-Aktion, die personenbezogene Daten (PII) mit anonymen Daten kombiniert. Verträge über Daten, die aus Werbenetzwerken, Werbe-Servern und Drittanbietern von Daten bezogen werden, beinhalten häufig spezifische vertragliche Verbote der Verwendung solcher Daten mit direkt identifizierbaren Daten.

**Befehlszeilenschnittstelle**: Eine Befehlszeilenschnittstelle ist ein textbasiertes Tool, mit dem eine Verbindung zu [!DNL Query Service] hergestellt werden kann, um eine Rohabfrage auszuführen.

**Komposition**: Eine Komposition ist eine Gruppierung von Komponenten, die sich zusammenbilden, um das Schema zu bilden.

**Bedingung**: Im Kontext von Tags ist eine Bedingung eine Regelkomponente, die eine logische Anweisung auswertet, die `true` oder `false` zurückgeben muss. Alle Bedingungen müssen zu `true` ausgewertet werden und alle Ausnahmebedingungen müssen zu `false` ausgewertet werden, bevor Aktionen für die Regel ausgeführt werden.

**Konsole**: In [!DNL Query Service] stellt die Konsole Informationen zum Status und zum Betrieb einer Abfrage bereit. Die Konsole zeigt den Verbindungsstatus zum [!DNL Query Service], die ausgeführten Abfragen und alle Fehlermeldungen an, die aus diesen Abfragen resultieren.

**Beschriftungen für Verträge (&quot;C&quot;)**: Datennutzungsbezeichnungen für Verträge (&quot;C&quot;) werden verwendet, um Daten zu kategorisieren, die vertragliche Verpflichtungen haben oder mit den Data Governance-Richtlinien Ihres Unternehmens in Zusammenhang stehen.

**CPRA**: Der [[!DNL California Consumer Privacy Rights Act (CPRA)]](https://cppa.ca.gov/regulations/consumer_privacy_act.html) erweitert und ändert Teile des [!DNL California Consumer Privacy Act (CCPA)]. Mit dem [!DNL CPRA] wird eine neue Grundlage für den Datenschutz von Verbraucherdaten in Kalifornien geschaffen, indem die Verbraucherrechte erhöht und die Art der Daten erweitert wird, die durch eine umfassendere Definition sensibler personenbezogener Daten abgedeckt werden. Darüber hinaus gründete die [!DNL CPRA] die California Privacy Protection Agency, eine neue Agentur, die für die Implementierung und Durchsetzung von Datenschutzregeln zuständig ist.

**C1-Vertragsbezeichnung**: Eine `C1` Beschriftung für die vertragliche Datennutzung gibt an, dass Daten nur in aggregierter Form aus Adobe Experience Cloud exportiert werden können, ohne dass eine Einzel- oder Gerätekennung enthalten ist. Zum Beispiel Daten, die aus Social Media stammen.

**C2-Vertragsbeschriftung**: Eine `C2` Beschriftung für die vertragliche Datennutzung gibt Daten an, die nicht an einen Drittanbieter exportiert werden können. Einige Datenanbieter haben in ihren Verträgen Klauseln, die den Export von Daten von dort verbieten, wo sie ursprünglich erfasst wurden. Beispielsweise wird die Übertragung von Daten, die Sie von sozialen Netzwerken erhalten, häufig durch Verträge beschränkt. C2 ist restriktiver als C1, was nur Aggregation und anonyme Daten erfordert.

**C3-Vertragsbeschriftung**: Eine `C3` Beschriftung für die vertragliche Datennutzung gibt Daten an, die nicht mit direkt identifizierbaren Informationen kombiniert oder anderweitig verwendet werden können. Einige Datenanbieter haben Vertragsklauseln, die die Kombination oder Verwendung dieser Daten mit direkt identifizierbaren Informationen verbieten. Verträge für Daten, die aus Werbenetzwerken, Werbeservern und Drittanbietern von Daten stammen, enthalten häufig spezifische vertragliche Verbote der Verwendung direkt identifizierbarer Daten.

**C4-Vertragsbezeichnung**: Eine `C4` Beschriftung für die vertragliche Datennutzung gibt an, dass Daten nicht für das Targeting von Anzeigen oder Inhalten verwendet werden können, weder auf der Site noch auf der Site. C4 ist die restriktivste Bezeichnung, da sie C5-, C6- und C7-Beschriftungen umfasst.

**C5-Vertragsbezeichnung**: Eine `C5` Beschriftung für die Nutzung von Vertragsdaten gibt an, dass Daten nicht für das Site-übergreifende Targeting von interessensbasierten Inhalten oder Anzeigen verwendet werden können. Interessensbasiertes Targeting oder Personalisierung tritt auf, wenn die folgenden drei Bedingungen erfüllt sind: Die vor Ort erfassten Daten werden verwendet, um Rückschlüsse auf das Interesse eines Benutzers zu ziehen, werden in einem anderen Kontext wie auf einer anderen Site oder App verwendet und dienen dazu, anhand dieser Rückschlüsse festzulegen, welche Inhalte oder Anzeigen bereitgestellt werden.

**C6-Vertragsbezeichnung**: Eine `C6` Beschriftung für die vertragliche Datennutzung gibt an, dass Daten nicht für das On-site-Anzeigen-Targeting verwendet werden können. Das On-site-Anzeigen-Targeting umfasst die Auswahl und Bereitstellung von Werbung auf den Websites oder Apps Ihres Unternehmens oder zur Messung der Bereitstellung und Effektivität solcher Werbung. Dazu gehört die Verwendung zuvor erfasster Onsite-Daten über das Interesse der Benutzer an der Auswahl von Anzeigen, die Verarbeitung von Daten darüber, welche Anzeigen angezeigt wurden, wann und wo sie angezeigt wurden und ob die Benutzer im Zusammenhang mit der Anzeige irgendwelche Maßnahmen ergriffen haben, z. B. die Auswahl einer Anzeige oder den Kauf.

**C7-Vertragsbezeichnung**: Eine `C7` Beschriftung für die vertragliche Datennutzung gibt an, dass Daten nicht für das On-site-Targeting von Inhalten verwendet werden können. Das Targeting von Inhalten auf der Site umfasst die Auswahl und Bereitstellung von Inhalten auf den Websites Ihrer Organisation oder in Apps oder die Messung der Bereitstellung und Effektivität solcher Inhalte. Dazu gehören zuvor erfasste Informationen über das Interesse der Benutzer an der Auswahl von Inhalten, die Verarbeitung von Daten darüber, welcher Inhalt angezeigt wurde, wie oft oder wie lange er angezeigt wurde, wann und wo er angezeigt wurde und ob die Verwendungszwecke Aktionen im Zusammenhang mit dem Inhalt durchgeführt haben, einschließlich der Auswahl von Inhalten.

**C8-Vertragsbezeichnung**: Eine `C8` Beschriftung für die vertragliche Datennutzung gibt an, dass Daten nicht zur Messung der Websites oder Apps Ihres Unternehmens verwendet werden können. Dies umfasst nicht das zielgerichtete Targeting, d. h. die Sammlung von Informationen über Ihre Nutzung dieses Dienstes, um Inhalte und/oder Werbung in anderen Kontexten zu personalisieren.

**C9-Vertragsbezeichnung**: Eine `C9` Beschriftung für die Nutzung von Vertragsdaten gibt an, dass Daten in datenwissenschaftlichen Workflows nicht verwendet werden können. Einige Verträge beinhalten ausdrücklich Verbote von Daten, die für die Datenwissenschaft verwendet werden. Manchmal werden diese Begriffe so formuliert, dass die Verwendung von Daten für künstliche Intelligenz (KI), maschinelles Lernen (ML) oder Modellierung verboten ist.

**C10-Vertragsbeschriftung**: Eine `C10` Beschriftung für die vertragliche Datennutzung gibt an, dass Daten nicht für die Aktivierung der verknüpften Identität verwendet werden können. Einige Datennutzungsrichtlinien beschränken die Verwendung von zusammengesetzten Identitätsdaten für die Personalisierung. Die Bezeichnung `C10` wird automatisch auf Segmente angewendet, wenn deren Zusammenführungsrichtlinien die Option &quot;Privates Diagramm&quot;verwenden.

**Spalte &quot;Erstellungsdatum&quot;**: Die Auswahl einer Spalte &quot;Erstellungsdatum&quot;ist eine Option bei der Angabe von Drittanbieterdaten über eine Quellverbindung. Wenn die Speicherstrategie anhängen ausgewählt ist und das Datensatzschema mehrere Datumsfelder enthält, müssen Sie aus dem verfügbaren Schema auswählen, um eine Schlüsselspalte Erstellungsdatum anzugeben. Die Option Erstellungsdatum ist nicht verfügbar, wenn die Speicherstrategie zum Überschreiben ausgewählt ist.

**Tabelle als Auswahl erstellen**: Tabelle als Auswahl erstellen (CTAS) ist ein SQL-Befehl, der bei Ausführung als Teil einer vollständigen und gültigen SQL-Abfrage [!DNL Query Service] anweist, die Ergebnisse der Abfrage in einem Datensatz zu behalten. Sie können einen neuen Ergebnissatz erstellen, frühere Ergebnisse überschreiben oder an vorherige Ergebnisse anhängen.

**Site-übergreifende Daten**: Site-übergreifende Daten sind die Kombination von Daten aus verschiedenen Sites, einschließlich einer Kombination aus Vor-Ort-Daten und Offsite-Daten oder einer Kombination von Daten aus verschiedenen Offsite-Quellen.

**Site-übergreifende Targeting-Marketing-Aktion**: Eine Marketing-Aktion, die Daten für Site-übergreifendes Anzeigen-Targeting verwendet. Die Kombination von Daten aus verschiedenen Sites, einschließlich einer Kombination aus Daten in einer Site und Offsite-Daten oder einer Kombination von Daten aus verschiedenen Offsite-Quellen, wird als „Site-übergreifende Daten“ bezeichnet. Site-übergreifende Daten werden in der Regel erfasst und verarbeitet, um Rückschlüsse auf die Interessen der Kunden zu ziehen.

**Benutzerdefinierter Identitäts-Namespace**: Benutzerdefinierte Identitäts-Namespaces können von Ihrer Organisation erstellt werden, um Identitäten für eine bestimmte Organisation oder einen bestimmten Geschäftsfall darzustellen.

**Benutzerdefinierte Beschriftungen**: Mit benutzerdefinierten Datennutzungsbezeichnungen können Sie bestimmte Beschriftungen erstellen und auf Datenfelder anwenden, die bestimmten Geschäftsanforderungen entsprechen.

**Customer AI**: Customer AI ist ein intelligenter Dienst auf Basis von Adobe Sensei, der Kundenprofile mit KI-basierten Eigenschaften anreichert und die Kundensegmentierung und Zielgruppenbestimmung ermöglicht.

## D

**Täglich**: Im Rahmen geplanter Dateiexporte werden vollständige oder inkrementelle Dateiexporte einmal täglich vom Startdatum bis zum Enddatum zu dem vom Benutzer angegebenen Zeitpunkt geplant.

**Datenwörterbuch**: Im Kontext von Tags ist ein Datenwörterbuch (auch als Datenkarte bezeichnet) ein Satz von Datenelementen, die in einer Eigenschaft definiert sind.

**Datenelement**: Im Kontext von Tags ist ein Datenelement ein Zeiger, der in Regeln und Erweiterungen verwendet wird, um auf ein bestimmtes Datenelement zu verweisen, das auf dem Client-Gerät vorhanden ist.

**Datenerfassung**: Bei der Datenerfassung werden Daten aus einer Quelle zu Experience Platform hinzugefügt. Daten können auf verschiedene Weise in Platform erfasst werden, einschließlich Streaming, Batches oder Hinzufügen über Quell-Connectoren.

**Datenschicht**: Im Kontext von Tags ist eine Datenschicht eine Datenstruktur, die auf dem Client-Gerät vorhanden ist und Metadaten zum Kontext enthält, in dem eine Seite oder ein Bildschirm angezeigt wird.

**Data Governance**: Data Governance umfasst die Strategien und Technologien, mit denen sichergestellt wird, dass die Daten den Vorschriften und organisatorischen Richtlinien bezüglich der Datennutzung entsprechen.

**Datenintegrationspartner**: Datenintegrationspartner vereinfachen und automatisieren das Laden und die Transformation massiver Datenmengen von über 200 Quellen in Experience Platform, ohne Code schreiben zu müssen.

**Datensatzbezeichnungen**: Datennutzungsbezeichnungen können Datensätzen hinzugefügt werden. Alle Felder in diesem Datensatz übernehmen die Bezeichnungen des Datensatzes.

**Data Science Workspace**: [!DNL Data Science Workspace] innerhalb von Experience Platform ermöglicht es Kunden, Modelle für maschinelles Lernen zu erstellen, die Daten aus Platform- und Adobe-Anwendungen nutzen, um intelligente Segmente zu erstellen, Einblicke zu generieren und Prognosen bereitzustellen, sodass digitale Erlebnisse für Endbenutzer deutlich verbessert werden können.

**Datenquelle**: Eine Datenquelle ist eine vom Benutzer festgelegte Quelle der Daten. Beispiele für eine Datenquelle sind eine mobile App, Profil- und/oder Erlebnisereignisse, Website-Profilereignisse oder ein CRM.

**Data Steward**: Ein Data Steward ist die Person, die für die Verwaltung, Überwachung und Durchsetzung der Daten-Assets einer Organisation verantwortlich ist. Ein Data Steward stellt außerdem sicher, dass Data Governance-Richtlinien geschützt und gepflegt werden, um mit staatlichen Vorschriften und organisatorischen Richtlinien konform zu sein.

**Datenstrom**: Ein Datenstrom ist ein Satz oder eine Sammlung von Nachrichten, die dasselbe Schema aufweisen und von derselben Quelle gesendet werden.

**Datentyp**: Ein Datentyp ist eine wiederverwendbare XDM-Ressource, die ein Objekt-Typ-Feld definiert, das mehrere Eigenschaften in einer hierarchischen Darstellung enthält.

**Datennutzungsbezeichnungen**: Mit Datennutzungsbezeichnungen können Sie Daten kategorisieren, die datenschutzbezogene Aspekte und vertragliche Bedingungen berücksichtigen, um Vorschriften und Unternehmensrichtlinien zu erfüllen. Datennutzungsbezeichnungen, die einem Datensatz hinzugefügt werden, werden vererbt oder auf alle Felder in diesem Datensatz angewendet. Datennutzungsbezeichnungen können auch direkt auf Felder angewendet werden.

**Datenfluss**: Ein Datenfluss ist eine virtuelle Pipeline von Daten, die von einer Quelle zu Zielen in Platform fließen.

**Datenfluss-Lauf**: Ein Datenfluss-Lauf ist ein Datenfluss, der auf der Grundlage eines vom Benutzer angegebenen Zeitplans auf Experience Platform landet.

**Datensatz**: Ein Datensatz ist ein Speicher- und Verwaltungskonstrukt für eine Sammlung von Daten, normalerweise eine Tabelle, die ein Schema (Spalten) und Felder (Zeilen) enthält.

**Datensatz-ID**: Eine Adobe-generierte Kennung für einen erfassten Datensatz.

**Datensatzausgabe**: Die Datensatzausgabe bietet einen Mechanismus, um zu bestimmen, welche Option &quot;Tabelle als Auswahl erstellen&quot;für eine bestimmte Ausführung mit [!DNL Query Service] verwendet wird.

**Deduplizierungsschlüssel**: Ein benutzerdefinierter Primärschlüssel, der die Identität bestimmt, anhand deren Benutzer ihre Profile deduplizieren möchten. &#x200B;

**Delta-Spalte**: Mit einer Delta-Spalte können Sie ein Quelldatenfeld auswählen, das einen Zeitstempel für die inkrementelle Erfassung darstellt.

**Delta-Speicherstrategie**: Die Delta-Speicherstrategie ist eine Option zum Erfassen von Drittanbieterdaten über eine Quellverbindung. Mit dieser Option kann der Benutzer angeben, dass neue oder geänderte Zeilen von Quelldaten in Experience Platform aufgenommen werden. Am Ende des Datensatzes werden neue Zeilen hinzugefügt und geänderte Zeilen werden im Datensatz auf der Experience Platform aktualisiert.

**Deskriptor**: Im Experience-Datenmodell (XDM) ist ein Deskriptor ein zusätzlicher Satz von schemabezogenen Metadaten, der ein bestimmtes Verhalten für ein Feld beschreibt. Deskriptoren können von Experience Platform verwendet werden, um das beabsichtigte Schemaverhalten zu verstehen, z. B. die Beziehung zwischen zwei Schemas.

**Ziel**: Ein Ziel ist ein allgemeiner Begriff für jeden Endpunkt, z. B. eine Adobe-Anwendung, Werbeplattform, einen Cloud-Speicher-Dienst oder einen Marketing-Dienst, bei der eine Zielgruppe aktiviert und bereitgestellt wird.

**Zielkategorie**: Eine Zielkategorie ist eine Gruppe von Zielen mit ähnlichen Merkmalen.

**Zielkatalog**: Ein Zielkatalog ist eine Liste der verfügbaren Ziele im Experience Platform.

**Direktaufrufregeln**: Im Kontext von Tags ist eine Direktaufrufregel eine Regel, die ausgeführt wird, wenn sie direkt von der Seite aus aufgerufen wird, wobei Ereigniserkennungs- und Suchsysteme umgangen werden.

**Anzeigename**: Im Experience-Datenmodell (XDM) ist ein Anzeigename ein benutzerfreundlicher Name für ein Feld, der in der Benutzeroberfläche angezeigt wird.

## E

**Geeignetes Angebot**: Ein geeignetes Angebot kann einem Profil konsistent angeboten werden, da es die zuvor definierten Bedingungen erfüllt.

**Eignungsregeln**: In [!DNL Offer Decisioning] werden Eignungsregeln auf ein Profil angewendet, das sich auf Kalender-, Zeitplan- und Begrenzungsbegrenzungen bezieht.

**E-Mail-Targeting-Marketing-Aktion**: Eine Marketing-Aktion, die Daten in E-Mail-Targeting-Kampagnen verwendet.

**Einbettungscode**: Im Kontext von Tags ist der Einbettungscode ein Skript-Tag, das auf einer Site oder Umgebung auf der HTML platziert wird. Der Einbettungscode weist den Browser an, wo der Build abgerufen werden soll.

**Enumeration**: Eine Auflistung (enum) ist ein XDM-Feld, das auf einen Satz vordefinierter Werte beschränkt ist.

**Umgebung**: Im Kontext von Tags ist eine Umgebung ein Satz von Bereitstellungsanweisungen, der die Host-Bereitstellung und das Dateiformat eines Builds angibt. Eine Bibliothek muss mit einer Umgebung gepaart werden, bevor sie erstellt werden kann.

**Fehlerdiagnose**: Die Fehlerdiagnose ermöglicht die Erstellung detaillierter Fehlermeldungen für erfasste Batches. Mit dem Fehlerschwellenwert können Sie den Prozentsatz der akzeptablen Fehler konfigurieren, bevor ein Batch fehlschlägt.

**Ereignis**: Im Kontext von Tags ist ein Ereignis ein bestimmter Regeltyp, d. h. ein Trigger, der auf einem Clientgerät auftritt, um die Ausführung einer Regel zu starten.

**Ereignisentitäten**: Im Kontext der Datenmodellierung stellen Ereignisentitäten Konzepte dar, die sich auf Aktionen beziehen, die ein Kunde ausführen kann, Systemereignisse oder andere Konzepte, bei denen Sie Änderungen im Zeitverlauf verfolgen möchten. Entitäten, die unter diese Kategorie fallen, sollten durch Schemas dargestellt werden, die auf der [!DNL XDM ExperienceEvent]-Klasse basieren.

**Ereignisse**: Ereignisse sind die mit einem Profil verknüpften Verhaltensdaten.

**Experience-Datenmodell (XDM)** [!DNL Experience Data Model] (XDM) ist ein Open-Source-Framework, das Standardschemata verwendet, um Daten für die Verwendung mit Experience Platform- und Adobe Experience Cloud-Anwendungen zu vereinheitlichen. XDM standardisiert, wie Daten strukturiert sind, beschleunigt und vereinfacht den Prozess, Erkenntnisse aus massiven Datenmengen zu gewinnen.

**Experiment**: Ein Experiment ist der Prozess zum Erstellen eines trainierten Modells, indem die Instanz mit einem Beispielabschnitt der Live-Produktionsdaten trainiert wird. Dies unterscheidet sich von einem trainierten Modell, das mit einem Holdout-Testdatensatz getestet wird. Dies unterscheidet sich auch vom Konzept eines Experiments in einigen Rahmen des maschinellen Lernens, bei dem es sich tatsächlich um ein Beispiel-Modellierungsprojekt handelt.

**Erlebnisereignis**: Ein Erlebnisereignis stellt einen Schnappschuss des Systems dar, wenn eine Interaktion oder ein Ereignis im Zusammenhang mit einem Kundenerlebnis stattfindet. Erlebnisereignisse sind unveränderliche Tatsacheneinträge darüber, was passiert ist, und stellen dar, was ohne Aggregation oder Interpretation passiert ist. Im Experience-Datenmodell (XDM) wird dieses Konzept von der [!DNL XDM ExperienceEvent] -Klasse erfasst.

**Vollständige Datei exportieren**: Eine Exportdatei mit einer vollständigen Momentaufnahme aller Profilqualifikationen für das ausgewählte Segment.

**Inkrementelle Dateien exportieren**: Eine Reihe exportierter Dateien, bei denen die erste Datei eine vollständige Momentaufnahme aller Profilqualifikationen für das ausgewählte Segment darstellt und nachfolgende Dateien inkrementelle Profilqualifikationen seit dem vorherigen Export darstellen.

**Erweiterung**: Im Kontext von Tags ist eine Erweiterung ein Funktionspaket, das zu einer Tag-Eigenschaft hinzugefügt wird. Eine Erweiterung konzentriert sich in der Regel auf eine bestimmte Marketing- oder Analyselösung und bietet die Tools, die zum Bereitstellen dieser Technologie in einer Client-Umgebung erforderlich sind.

**Erweiterungspaket**: Im Kontext von Tags ist ein Erweiterungspaket eine ZIP-Datei, die von einem Erweiterungsentwickler erstellt und hochgeladen wurde und alle erforderlichen Informationen enthält, damit Tags von Benutzern in ihrer Eigenschaft die Erweiterung installieren können. Ein Erweiterungspaket enthält ein Manifest, das Informationen über die Erweiterung, die HTML/JavaScript, die zum Konfigurieren des Verhaltens der Tag-Erweiterung erforderlich sind, und die ausführbare JavaScript, die an die Client-Umgebung gesendet wird (falls erforderlich), angibt.

## F

**Fallback-Angebote**: Ein Fallback-Angebot ist das Standardangebot, das angezeigt wird, wenn ein Endbenutzer für keines der Angebote in der verwendeten Sammlung geeignet ist.

**Funktionszuordnung**: Die Funktionszuordnung bezieht sich auf den Prozess der Zuordnung von Funktionen aus Daten zu Eingabe- und Zielfunktionen, die für ein Modell für maschinelles Lernen erforderlich sind.

**Feld**: Ein Feld ist das Element der niedrigsten Ebene eines Datensatzes, wie durch das XDM-Schema des Datensatzes definiert. Jedes Feld hat einen Namen für Verweiszwecke und einen Typ, der den darin enthaltenen Datentyp angibt. Feldtypen können Ganzzahlen, Zahlen, Zeichenfolgen, boolesche Werte und Objekte enthalten (sind jedoch nicht darauf beschränkt).

**Feldergruppe**: Siehe &quot;Schemafeldergruppe&quot;.

**Feldbezeichnungen**: Feldbezeichnungen sind Data Governance-Bezeichnungen, die entweder von einem Datensatz übernommen oder direkt auf ein Feld angewendet werden.

**Feldname**: Ein Feldname wird verwendet, um in Abfragen und nachgelagerten Diensten auf den Wert eines Felds zu verweisen.

**Häufigkeit**: In [!DNL Query Service] bestimmt die Häufigkeit, wie oft eine wiederkehrende geplante Abfrage ausgeführt wird.

## G

**Geofence**: Ein Geofence ist eine virtuelle geografische Grenze, die durch GPS- oder RFID-Technologie definiert wird und es Software ermöglicht, eine Antwort Trigger, wenn ein Mobilgerät ein bestimmtes Gebiet erreicht oder verlässt.

**DSGVO (Datenschutz-Grundverordnung)**: Die Datenschutz-Grundverordnung (DSGVO) ist ein Rechtsrahmen, der Richtlinien für die Erhebung und Verarbeitung personenbezogener Daten von Einzelpersonen in der Europäischen Union (EU) festlegt. Die DSGVO legt die Grundsätze für das Datenmanagement und die Rechte des Einzelnen fest und erfasst alle Unternehmen, die mit den Daten von EU-Bürgern zu tun haben.

**Schutzmechanismen**: Schutzmechanismen sind Schwellenwerte, die die Datennutzung und Systemnutzung, Leistungsoptimierung und Vermeidung von Fehlern oder unerwarteten Ergebnissen in Adobe Experience Platform unterstützen. Leitplanken können sich auf Ihre Nutzung oder Verwendung von Daten und Verarbeitung im Zusammenhang mit Ihren Lizenzierungsberechtigungen beziehen.

## H

**HIPAA**: Der [[!DNL Health Insurance Portability and Accountability Act (HIPAA)]](https://www.hhs.gov/hipaa/index.html) ist ein US-Bundesgesetz, das geschaffen wurde, um die Effizienz der Gesundheitsfürsorge zu verbessern, die Portabilität von Krankenversicherungen zu verbessern und die Privatsphäre von Patienten und Mitgliedern des Gesundheitsplans zu schützen. Im Rahmen des HIPAA haben Einzelpersonen das Recht, auf ihre Informationen zuzugreifen und sie zu ändern und Kopien ihrer medizinischen Aufzeichnungen oder Gesundheitsinformationen zu erhalten. Gedeckte Stellen und Geschäftspartner der abgedeckten Stellen müssen den HIPAA-Vorschriften entsprechen.

**Host**: Im Kontext von Tags gibt ein Host den Speicherort, die Domäne und die Benutzerberechtigungen an, die erforderlich sind, damit das System einen Build bereitstellen kann.

**Stündlich**: Im Zusammenhang mit geplanten Dateiexporten werden inkrementelle Dateiexporte alle 3, 6, 8 oder 12 Stunden geplant.

## I

**Identität**: Eine Identität ist eine Kennung, die einen einzelnen Kunden eindeutig kennzeichnet, z. B. eine Cookie-ID, Geräte-ID oder E-Mail-ID.

**Identitätsfelder**: Identitätsfelder sind XDM-Felder, mit denen Informationen über einzelne Kunden aus mehreren Datenquellen zusammengeführt werden. Damit das Schema zur Verwendung im Echtzeit-Kundenprofil aktiviert werden kann, muss eine einzige primäre Identität definiert werden.

**Identitätsbezeichnungen (&quot;I&quot;)**: Datennutzungsbezeichnungen (&quot;I&quot;) werden verwendet, um Daten zu kategorisieren, mit denen eine bestimmte Person identifiziert oder kontaktiert werden kann.

**Identitätsdiagramm**: Ein Identitätsdiagramm ist eine Zuordnung der Beziehungen zwischen zugeordneten und verknüpften Identitäten, die für einen einzelnen Kunden vorhanden sind. Jedes Identitätsdiagramm wird nahezu in Echtzeit mit Kundenaktivität aktualisiert. Die gemeinsame Struktur der Identitätsbeziehungen in Ihren Daten wird durch das [!UICONTROL private Diagramm] dargestellt, das als Strukturvorlage für jedes einzelne Identitätsdiagramm dient.

**Identitäts-Namespace**: Ein Identitäts-Namespace definiert den Kontext einer Kennung wie eine E-Mail-Adresse oder eine CRM-ID.

**Identitätsdienst**: [!DNL Experience Platform Identity Service] ermöglicht die Erstellung und Verwaltung von Identitätstypen, sodass Sie Kundenidentitäten geräteübergreifend und kanalübergreifend verknüpfen können. Die Fähigkeit des Dienstes, Identitäten miteinander zu verknüpfen, ermöglicht es dem Echtzeit-Kundenprofil, eine vollständige Darstellung jedes einzelnen Kunden bereitzustellen.

**Identitätszusammenfügung**: Beim Identitätszusammenfügen werden Datenfragmente identifiziert und zu einem vollständigen Profildatensatz zusammengefügt.

**Identitätssymbol**: Ein Identitätssymbol ist eine Abkürzung eines Identitäts-Namespace, der in APIs als Referenz verwendet werden kann.

**Identitätswert**: Ein Identitätswert in Kombination mit einem Identitäts-Namespace ist eine Kennung, die eine eindeutige Person, Organisation oder ein Asset darstellt. Bei der Zuordnung von Datensatzdaten zu Profilfragmenten müssen Namespace und Identitätswert übereinstimmen.

**I1-Datennutzungsbezeichnung**: Mit der `I1`-Datennutzungsbezeichnung werden Daten klassifiziert, mit denen eine bestimmte Person und kein Gerät direkt identifiziert oder kontaktiert werden kann.

**I2-Datennutzungsbezeichnung**: Mit der `I2`-Datennutzungsbezeichnung werden Daten klassifiziert, die in Kombination mit anderen Daten verwendet werden können, um eine bestimmte Person indirekt zu identifizieren oder zu kontaktieren.

**IMS-Organisation**: Eine IMS-Organisation (manchmal auch als IMS-Organisation bezeichnet) ist der Name, mit dem ein Unternehmen oder eine bestimmte Gruppe innerhalb eines Unternehmens über verschiedene Adobe-Produkte hinweg identifiziert wird. Administratoren können den Zugriff und die Berechtigungen von Funktionen für Benutzer einer Organisation konfigurieren und verwalten.

**Aufnahme**: Siehe Datenerfassung.

**Aufnahmeplan**: Ein Erfassungszeitplan bietet zeitbasierte Optionen bei der Aufnahme von einer Quelle in eine Experience Platform.

**Eingabefunktion**: Eine Eingabefunktion ist in der Funktionszuordnung angegeben und wird von einem Modell für maschinelles Lernen verwendet, um Prognosen zu erstellen.

**[!DNL Intelligent Services]**: [!DNL Intelligent Services] wie [!DNL Attribution AI] und [!DNL Customer AI] sind auf maschinellem Lernen basierende Modelle mit künstlicher Intelligenz, bei denen Experience Platform (oder auf Platform aufbauende Anwendungen wie Adobe Real-time Customer Data Platform) ausgeführt und betrieben werden müssen.

**Interessenbasiertes Targeting oder Personalisierung**: Interessenbasiertes Targeting, auch Personalisierung genannt, tritt auf, wenn die folgenden drei Bedingungen erfüllt sind:

1. Daten, die vor Ort erfasst werden, dienen dazu, Rückschlüsse auf das Interesse eines Benutzers zu ziehen.
1. Daten werden in einem anderen Kontext wie auf einer anderen Site oder App (außerhalb der Site) verwendet.
1. Mithilfe von Daten wird festgelegt, welche Inhalte oder Anzeigen basierend auf diesen Schlussfolgerungen bereitgestellt werden.

## J

**[!DNL JupyterLab]**: Eine Open-Source-Web-basierte Schnittstelle für Projekt [!DNL Jupyter], die in die Platform-Benutzeroberfläche integriert ist.

**[!DNL Jupyter Notebook]**: Dank der Integration von JupyterLab mit Jupyter Notebooks können Sie Daten bereinigen und umwandeln, numerische Simulationen, statistische Modellierung, Datenvisualisierung, maschinelles Lernen und vieles mehr in Experience Platform-Daten in verschiedenen Sprachen wie Python, Scala und PySpark durchführen.

## K

## L

**LGPD**: Der [[!DNL Lei Geral de Proteção de Dados (LGPD)]](https://gdpr.eu/gdpr-vs-lgpd/) zielt darauf ab, die Behandlung personenbezogener Daten aller Personen oder natürlichen Personen in Brasilien zu regeln. Das LGPD verleiht brasilianischen Bürgern das Recht, auf ihre personenbezogenen Daten zuzugreifen und sie zu löschen, um zu erfahren, ob ihre personenbezogenen Daten verkauft oder weitergegeben werden (und an wen), und das Recht, sich gegen den Verkauf ihrer Daten an Dritte zu entscheiden.

**Bibliothek**: Im Kontext von Tags ist eine Bibliothek ein Satz von Geschäftslogik, die Anweisungen zum Verhalten der Tag-Bibliothek auf dem Client-Gerät enthält.

**Lookup-Entitäten**: Im Kontext der Datenmodellierung stellen Lookup-Entitäten Konzepte dar, die sich auf eine einzelne Person beziehen, aber nicht direkt zur Identifizierung der Person verwendet werden können. Entitäten, die unter diese Kategorie fallen, sollten durch Schemas dargestellt werden, die auf benutzerdefinierten Experience-Datenmodell (XDM)-Klassen basieren, und mit einer Profilentität über eine [Schemabeziehung](../xdm/tutorials/relationship-ui.md) verknüpft werden.

## M

**Machine learning (ML)**: Machine learning ist der Studienbereich, der es Computern ermöglicht, zu lernen, ohne explizit programmiert zu werden.

**Modell für maschinelles Lernen**: Ein Modell für maschinelles Lernen ist eine Instanz eines Rezepts für maschinelles Lernen, das mithilfe von historischen Daten und Konfigurationen zur Lösung eines geschäftlichen Anwendungsfalls trainiert wird. In Adobe Experience Platform Data Science Workspace werden maschinelles Lernen als Rezepte bezeichnet.

**Obligatorisches Attribut**: Ein benutzeraktiviertes Kontrollkästchen, mit dem sichergestellt wird, dass alle Profildatensätze das ausgewählte Attribut enthalten. Beispiel: Alle exportierten Profile enthalten eine E-Mail-Adresse.

**Zuordnung**: Die Datenzuordnung ist der Prozess der Zuordnung von Quelldatenfeldern zu verwandten Zielfeldern in einem Ziel.

**Marketing-Aktion**: Im Data Governance-Framework ist eine Marketing-Aktion (auch als Marketing-Anwendungsfall bezeichnet) eine Aktion, die ein Experience Platform-Datenverbraucher durchführt und bei der geprüft werden muss, ob Verstöße gegen Datennutzungsrichtlinien vorliegen.

**Zusammenführungsmethode**: Beim Definieren einer Zusammenführungsrichtlinie mithilfe der Platform-Benutzeroberfläche gibt die Zusammenführungsmethode an, wie Datenfragmente bei einem Konflikt priorisiert werden sollen. Wenn Sie die Echtzeit-Kundenprofil-API zum Definieren einer Zusammenführungsrichtlinie verwenden, wird die Zusammenführungsmethode mithilfe des Objekts `attributeMerge` bestimmt.

**Zusammenführungsrichtlinie**: Zusammenführungsrichtlinien sind Regeln, mit denen Experience Platform bestimmt, wie Kundendatenfragmente aus mehreren Quellen kombiniert werden, um ein einzelnes Profil zu erstellen. Wenn ein Datenkonflikt auftritt, bestimmt die Zusammenführungsrichtlinie, welche Daten für die Aufnahme in das Profil priorisiert werden sollen.

**MHMDAa**: Der [[!DNL Washington My Health My Data Act]](https://app.leg.wa.gov/RCW/default.aspx?cite=19.373&amp;full=true) verbessert die Datenschutzrechte für Verbraucher in Bezug auf ihre Gesundheitsdaten. Sie schreibt Offenlegungs-, Zustimmungs- und Löschungsrechte für Gesundheitsdaten vor und verbietet den Verkauf von Gesundheitsdaten ohne Genehmigung. Darüber hinaus ist es nach dem Gesetz rechtswidrig, Geofencing rund um Gesundheitseinrichtungen zu nutzen.

**Mixin**: Siehe &quot;Schema field group&quot;.

**Modul**: Im Kontext von Tags ist ein Modul ein Snippet aus ausführbarem JavaScript, das von einer Erweiterung bereitgestellt wird und Aktionen in einer Client-Umgebung ausführt, ohne eine Regel erstellen zu müssen.

## N

**[!DNL New Zealand Privacy Act]**: Der [[!DNL New Zealand Privacy Act]](https://www.privacy.org.nz/privacy-act-2020/privacy-principles/) steuert, wie Agenturen die personenbezogenen Daten von neuseeländischen Bürgern und Organisationen erfassen, verwenden, offenlegen, speichern und zugänglich machen können. Im Jahr 2020 führte die neueste Fassung des Gesetzes wesentliche Änderungen an diesen Datenschutzgesetzen ein, darunter neue Straftaten, die Erhöhung der Geldbußen, die obligatorische Meldung von Datenverstößen und die Ausweitung der Befugnisse des Datenschutzbeauftragten.

**Nicht-Produktions-Sandbox**: Nicht-Produktions-Sandboxes sind Sandboxes, die normalerweise für Entwicklungsexperimente, Tests oder Versuche verwendet werden. Im Gegensatz zu Produktions-Sandboxes können Nicht-Produktions-Sandboxes zurückgesetzt und gelöscht werden.

**[!DNL Notebooks]**: [!DNL Notebooks] werden mit [!DNL Jupyter Notebook] erstellt und können zur Datenanalyse ausgeführt werden.

## O

**Angebot**: Ein Angebot ist eine Marketing-Botschaft, die einen Geschäfts- oder Verkaufsvorschlag für einen (potenziellen) Kunden enthält. Angebote verfügen oft über spezifische Regeln, die bestimmen, wer sie sehen oder empfangen darf.

**[!DNL Offer Decisioning]**: [!DNL Offer Decisioning] ermöglicht es Marketing-Experten, Regeln und trainierte Modelle von Angebotsvorschlägen zu verwalten, wenn sie mit Endbenutzern interagieren, basierend auf Daten, die über Kanäle und Anwendungen hinweg erfasst wurden.

**Angebotsbibliothek**: Die Angebotsbibliothek ist eine zentrale Bibliothek, die zum Verwalten von personalisierten Angeboten und Fallback-Angeboten, Entscheidungsregeln und Aktivitäten verwendet wird.

**Marketing-Aktion für Personalisierung auf der Site**: Eine Marketing-Aktion, die Daten für die Personalisierung von Inhalten auf der Site verwendet. Bei der On-site-Personalisierung handelt es sich um Daten, die dazu dienen, Rückschlüsse auf die Interessen der Benutzer zu ziehen, und anhand derer anhand dieser Rückschlüsse ausgewählt wird, welche Inhalte oder Anzeigen bereitgestellt werden.

**On-site-Targeting-Marketing-Aktion**: Eine Marketing-Aktion, bei der Daten für On-site-Anzeigen verwendet werden, einschließlich der Auswahl und Bereitstellung von Werbung auf den Websites oder Apps Ihrer Organisation, oder um die Bereitstellung und Effektivität solcher Werbung zu messen.

**Einmal**: Im Kontext geplanter Dateiexporte wird ein einmaliger, On-Demand-vollständiger Dateiexport geplant.

**Speicherstrategie überschreiben**: Die Speicherstrategie &quot;Überschreiben&quot;ist eine Option zum Erfassen von Drittanbieterdaten über eine Verbindung, über die Sie angeben können, ob erfasste Daten in einem festgelegten Zeitplan überschrieben werden.

## P

**Partielle Erfassung**: Die partielle Erfassung ermöglicht die Erfassung gültiger Datensätze von Batch-Daten innerhalb eines festgelegten Fehlerschwellenwerts. Die Fehlerdiagnose für fehlgeschlagene Datensätze kann unter [!UICONTROL Überwachung] oder [!UICONTROL Quellen] Datenfluss-Übersicht heruntergeladen oder aufgerufen werden.

**Parquet-Dateien**: Eine Parquet-Datei ist ein Spaltenspeicherdateiformat mit komplexen verschachtelten Datenstrukturen. Parquet-Dateien sind erforderlich, um Daten zum Ausfüllen eines Schemadatasets hinzuzufügen.

**PDPA**: Der [[!DNL Personal Data Protection Act (PDPA)]](https://www.pdpc.gov.sg/Overview-of-PDPA/The-Legislation/Personal-Data-Protection-Act) wurde eingeführt, um die thailändischen Dateneigner vor der illegalen Sammlung, Verwendung oder Weitergabe ihrer personenbezogenen Daten zu schützen. Inspiriert durch die DSGVO der Europäischen Union gewährt die Verordnung den thailändischen Bürgern das Recht, Zugang zu ihren gespeicherten personenbezogenen Daten oder deren Löschung zu beantragen.

<!-- Not yet released
**PDPD**: The [[!DNL Personal Data Protection Decree] (PDPD) 
-->

**Personalisierte Angebote**: Ein personalisiertes Angebot ist eine anpassbare Marketing-Botschaft, die auf Eignungsregeln und Einschränkungen basiert.

**Platzierungen**: Eine Platzierung ist der Speicherort und/oder Kontext, in dem ein Angebot für Endbenutzende erscheint.

**Arbeitsbereich &quot;Richtlinien&quot;**: Ein Arbeitsbereich in der Platform-Benutzeroberfläche, über den Data Stewards Datennutzungsbezeichnungen und -richtlinien für Ihr Unternehmen anzeigen und verwalten können.

**Richtlinie**: Eine Datennutzungsrichtlinie ist eine Regel, die Marketing-Aktionen angibt, die auf der Anwendung der auf Platform-Daten angewendeten Nutzungsbezeichnungen beschränkt sind.

**Richtliniendurchsetzung**: Ermöglicht Ihnen das Durchsetzen von Datennutzungsrichtlinien mit angewandten Marketing-Aktionen, um Datenvorgänge zu verhindern, die Richtlinienverletzungen innerhalb eines Unternehmens darstellen.

**Primärer Schlüssel**: Ein Primärschlüssel ist eine Bezeichnung in einem Schema, mit der alle Datensätze eindeutig identifiziert werden können.

**Priorität**: In [!DNL Offer Decisioning] wird die Priorität verwendet, um Angebote zu ordnen, die alle Einschränkungen erfüllen, wie Eignung, Kalender und Begrenzungen.

**Privates Identitätsdiagramm**: Das private Identitätsdiagramm (manchmal auch als privates Diagramm bezeichnet) ist eine private Zuordnung von Beziehungen zwischen zugeordneten und verknüpften Identitäten, die auf Ihren Erstanbieterdaten basiert und nur von Ihrer Organisation sichtbar ist. Für jede Organisation existiert nur ein privates Diagramm. Es dient als struktureller Entwurf für die individuellen Identitätsdiagramme, die für jeden Kunden erstellt werden, der mit Ihrer Marke interagiert.

**Produktprofil**: Produktprofile ermöglichen es Administratoren, Benutzern Zugriff auf alle oder eine Untergruppe von Diensten zu gewähren, die mit Experience Platform verknüpft sind.

**Produktions-Sandbox**: Eine Produktions-Sandbox ist eine Sandbox, die zur Verwendung in Ihrer Produktionsumgebung vorgesehen ist. Im Gegensatz zu Nicht-Produktions-Sandboxes können Produktions-Sandboxes nicht zurückgesetzt oder gelöscht werden.

**Profil**: Dieses Profil ist nicht mit dem Echtzeit-Kundenprofil als Dienst zu verwechseln. Es ist eine vollständige Darstellung eines einzelnen Kunden, erstellt aus zusammengeführten Datensatz- und Zeitreihendaten aus mehreren Quellen.

**Profilzugriff**: Der `/entities` -Endpunkt in der Echtzeit-Kundenprofil-API ermöglicht Ihnen den Zugriff auf Datensatzdaten und Zeitreihenereignisse im Profildatenspeicher. Siehe auch: Profilentitäten

**Profildaten**: Profildaten beziehen sich auf alle Daten, die sich im Profildatenspeicher befinden.

**Profildatenspeicher**: Der Profildatenspeicher (manchmal auch als Profilspeicher bezeichnet) ist ein vom Daten-Pool getrenntes Datenspeichersystem, das vom Echtzeit-Kundenprofil zum Erstellen und Speichern von Profilen verwendet wird.

**Profilentitäten**: Profilentitäten stellen Attribute dar, die sich auf eine einzelne Person beziehen, normalerweise einen Kunden. Entitäten, die unter diese Kategorie fallen, sollten durch Schemas dargestellt werden, die auf der [!DNL XDM Individual Profile]-Klasse basieren. Siehe auch: Profilzugriff

**Profilexport**: [!DNL Profile] Der Export ist einer der beiden Zieltypen im Experience Platform. Der Export von [!DNL Profile] erzeugt eine Datei mit Profilen und Attributen und verwendet PII-Rohdaten mit E-Mails, um sie in Marketing- und E-Mail-Automatisierungsplattformen zu integrieren.

**Profilfragment**: Ein Profilfragment ist die Profilinformation für nur eine Identität aus der Liste der Identitäten, die für einen bestimmten Kunden vorhanden sind.

**Profil-ID**: Eine Profil-ID ist eine automatisch generierte Kennung, die mit einem Identitätstyp verknüpft ist und ein Profil darstellt.

**Eigenschaft**: Im Kontext von Tags ist eine Eigenschaft ein Container für alles, was zum Bereitstellen eines Satzes von Tags erforderlich ist.

## Q

**Abfrage**: Abfragen sind Anforderungen für Daten aus Datenbanktabellen.

**Abfrage-Editor**: Der Abfrage-Editor ist ein Tool zum Schreiben, Validieren und Senden von SQL-Anweisungen in [!DNL Query Service].

## R

**Real-time Customer Data Platform**: Adobe Real-time Customer Data Platform (Real-Time CDP) führt bekannte und unbekannte Kundendaten zusammen, um vertrauenswürdige Kundenprofile mit vereinfachter Integration, intelligenter Segmentierung und Echtzeit-Aktivierung über die digitale Journey zu erstellen.

**Echtzeit-Kundenprofil**: Das Echtzeit-Kundenprofil (auch als Profil bezeichnet) bietet eine ganzheitliche Sicht auf jeden einzelnen Kunden, indem es Daten aus verschiedenen Kanälen kombiniert, einschließlich Online, Offline, CRM und Drittanbieter. Mit Profil können Sie Ihre Kundendaten in einzelne Profile konsolidieren, die umsetzbare, mit Zeitstempel versehene Konten für jede Kundeninteraktion bieten.

**Rezept** Ein Rezept ist ein Adobe für eine Modellspezifikation. Es handelt sich dabei um einen Container auf oberster Ebene, der bestimmte maschinelle Lernprozesse, KI-Algorithmen, Verarbeitungslogik und Konfigurationsparameter darstellt, die zum Erstellen und Ausführen eines trainierten Modells erforderlich sind und somit zur Lösung spezifischer Geschäftsprobleme beitragen.

**Datensatz**: Ein Datensatz sind Daten, die als Zeilen in einem Datensatz beibehalten werden.

**Aufzeichnen von Daten**: Stellt Informationen zu den Attributen eines Subjekts bereit. Ein Subjekt könnte eine Organisation oder eine Einzelperson sein.

**Wiederholung**: In [!DNL Query Service] definiert eine Wiederholung, ob eine Abfrage nur einmal oder wiederkehrend ausgeführt werden soll.

**Darstellung**: In [!DNL Offer Decisioning] ist eine Darstellung Informationen, die von einem Kanal zur Anzeige eines Angebots verwendet werden, z. B. Ort oder Sprache.

**Ressource**: Im Kontext von Tags ist eine Ressource ein allgemeiner Begriff, der auf Optionen verweist, die der Tag-Benutzer in der Client-Umgebung konfigurieren kann, einschließlich Erweiterungen, Datenelementen und Regeln.

**Rollenbasierte Zugriffssteuerung**: Rollenbasierte Zugriffskontrolle ermöglicht Administratoren die Zuweisung von Zugriff und Berechtigungen zu Benutzern von Experience Platform. Zu den Berechtigungen gehört die Möglichkeit, Experience Platform-Funktionen anzuzeigen und/oder zu verwenden, z. B. das Erstellen von Sandboxes, das Definieren von Schemas und das Verwalten von Datensätzen.

**Regel**: Im Kontext von Tags ist eine Regel eine Sammlung von Komponenten, die einen bestimmten Satz von Ereignissen, Bedingungen und Aktionen definieren, die logisch gruppiert werden sollen.

**Regelkomponente**: Im Kontext von Tags sind Regelkomponenten die Ereignisse, Bedingungen und Aktionen, aus denen eine Regel besteht.

**Laufzeit**: Laufzeitumgebung gibt eine Laufzeitumgebung für ein Rezept für maschinelles Lernen an. Mit den Laufzeitumgebungen [!DNL Python], R, [!DNL Spark], PySpark und TensorFlow können Sie eine URL für ein Docker-Bild für eine Rezept-Quelle eingeben.

## S

**Beispieldaten**: Beispieldaten sind eine Vorschau einer Datendatei, normalerweise die ersten 100 Zeilen, die einem Datenwissenschaftler oder -ingenieur eine Vorstellung davon vermitteln, welches Schema oder welche Daten sich in der Datendatei befinden.

**Sandbox**: Eine Sandbox ist ein virtuelles Konstrukt, das eine einzelne Platform-Instanz in eine separate virtuelle Umgebung partitioniert, um die Entwicklung und Weiterentwicklung von Programmen für digitale Erlebnisse zu unterstützen.

**Sandbox-Zurücksetzen**: Durch ein Sandbox-Zurücksetzen werden alle Daten, einschließlich Daten, Profilen und Segmenten, in einer Sandbox gelöscht. Sandbox-Zurücksetzungen können sich auf Daten auswirken, die mit internen oder externen Zielen verbunden sind.

**Sandbox-Umschalter**: Mit dem Sandbox-Umschalter auf Experience Platform können Benutzer zwischen Sandboxes navigieren, auf die sie Zugriff haben. Durch das Wechseln einer Sandbox werden alle Inhalte geändert und der Zugriff auf Funktionen kann je nach Berechtigungen geändert werden.

**Zeitplan**: Ein Zeitplan ist eine benutzerdefinierte Spezifikation der Häufigkeit oder Häufigkeit der Datenerfassung von einer Drittanbieter-Datenquelle zu Adobe Experience Platform.

**Scoring**: Beim Scoring werden mithilfe eines trainierten Modells Einblicke aus Daten generiert.

**Schema**: Ein Schema ist ein Regelsatz, der die Struktur und das Format der Daten darstellt und validiert. Ein Schema besteht aus einer Klasse und optionalen Feldergruppen und wird zum Erstellen von Datensätzen und Datensätzen verwendet. Ein Schema kann Verhaltensattribute, Zeitstempel, Identitäten, Attributdefinitionen, Beziehungen und mehr enthalten.

**Schemafeldgruppe**: Im Experience-Datenmodell (XDM) können Benutzer mit einer Schemafeldergruppe wiederverwendbare Felder erweitern, um ein oder mehrere Attribute zu definieren, die in ein Schema aufgenommen werden sollen.

**Schema Library**: Die Schema Library enthält branchenübliche XDM-Ressourcen, die von Adobe zur Verfügung gestellt werden, sowie benutzerdefinierte Ressourcen, die von Ihrem Unternehmen definiert werden.

**Schema Registry**: Die Schema Registry bietet eine Benutzeroberfläche und RESTful-API, mit der alle schemabezogenen Ressourcen in der Schema Library angezeigt und verwaltet werden.

**Geheimer Zugriffsschlüssel**: Ein geheimer Zugriffsschlüssel ist ein S3-Schlüssel, der in Verbindung mit der Zugriffsschlüssel-ID zum Signieren von AWS-Anfragen verwendet wird.[!DNL Amazon]

**Segment**: Ein Segment ist ein Regelsatz, der Attribute und Ereignisdaten enthält, die eine Reihe von Profilen als Zielgruppe qualifizieren.

**Segmentaufbau**: Der [!DNL Segment Builder] ist eine visuelle Entwicklungsumgebung, die zum Erstellen von Segmentdefinitionen verwendet wird. Sie dient als gemeinsame Komponente aller Anwendungen, die den Experience Platform Segmentation Service verwenden.

**Segmentdefinition**: Eine Segmentdefinition ist der Regelsatz, der zur Beschreibung der Schlüsselmerkmale oder des Verhaltens einer Zielgruppe verwendet wird. Nach der Erstellung einer Segmentdefinition werden die darin beschriebenen Regeln zur Bestimmung qualifizierter Zielgruppenmitglieder für ein Segment verwendet.

**Methode zur Segmentauswertung**: Es gibt zwei Methoden zur Segmentauswertung: Geplant und On-Demand. Die geplante Auswertung ermöglicht einen wiederkehrenden Zeitplan für die Ausführung eines Exportauftrags zu einem bestimmten Zeitpunkt, während die On-Demand-Auswertung die Erstellung eines Segmentauftrags umfasst, um die Zielgruppe sofort zu erstellen.

**Segmentexport**: Der Segmentexport ist einer der beiden Zieltypen im Experience Platform. Beim Segmentexport können Sie die Profile senden, die sich qualifizieren und dem Ziel zugeordnet wurden. Verwendet Segment- und Benutzer-IDs und pseudonyme Daten und lässt sich normalerweise in soziale Netzwerke und andere Zielplattformen für digitale Medien integrieren.

**Segment-ID**: Eine Segment-ID ist eine automatisch generierte Kennung, die mit einem Segment verknüpft ist.

**Segmentzugehörigkeit**: Die Segmentzugehörigkeit zeigt an, zu welchen Segmenten ein Profil derzeit gehört.

**Segmentregeln**: Segmentregeln definieren die Bedingungen, die bestimmen, ob ein Profil für ein Segment qualifiziert ist.

**Segmentierung**: Bei der Segmentierung wird eine große Gruppe von Kunden, Interessenten oder Verbrauchern in kleinere Gruppen unterteilt, die ähnliche Attribute aufweisen und ähnlich auf bestimmte Marketing-Strategien reagieren.

**Sensei ML Framework**: Sensei ML Framework ist ein einheitliches Framework für maschinelles Lernen (ML), das Experience Platform-Daten nutzt, um Datenwissenschaftler in die Lage zu versetzen, ML-gestützte Informationsdienste schneller, skalierbarer und wiederverwendbarer zu entwickeln.

**Vertrauliche (&quot;S&quot;) Beschriftungen**: Vertrauliche (&quot;S&quot;) Beschriftungen werden verwendet, um Daten zu kategorisieren, die als vertraulich gelten, z. B. verschiedene Verhaltens- oder geografische Datentypen, die als vertraulich markiert werden sollen.

**Dienste**: Ein leistungsstarkes Framework zur Implementierung von KI- und ML-Diensten durch Nutzung von Adobe Intelligent Services. Services bieten Echtzeit-, personalisierte Kundenerlebnisse oder setzen benutzerdefinierte intelligente Dienste um.

**Marketing-Aktion zur Personalisierung einer einzelnen Identität**: Eine Marketing-Aktion, die Daten zur Personalisierung von Inhalten auf der Site verwendet. Bei der Onsite-Personalisierung geht es um alle Daten, die verwendet werden, um Rückschlüsse auf die Interessen der Benutzer zu ziehen, und darum, auszuwählen, welche Inhalte oder Anzeigen auf der Grundlage dieser Rückschlüsse bereitgestellt werden.

**S1-Datennutzungsbezeichnung**: Mit einer `S1`-Datennutzungsbezeichnung werden Daten klassifiziert, die den Längen- und Breitengrad angeben, mit dem die genaue Position eines Geräts ermittelt werden kann.

**S2-Datennutzungsbezeichnung**: Eine `S2` Datennutzungsbezeichnung wird verwendet, um Daten zu klassifizieren, die zur Bestimmung eines breit definierten Geofence-Bereichs verwendet werden können.

**Source**: Eine Quelle ist ein allgemeiner Begriff für jeden Input-Connector in Platform. Siehe auch: Source-Connector

**Source-Attribut**: Ein Quellattribut ist ein Feld im Quelldatensatz. Source-Attribute werden Zielschemafeldern zugeordnet.

**Source catalog**: Der Quellkatalog ist die Liste der verfügbaren Quell-Connectoren im Experience Platform.

**Source-Kategorie**: Eine Quellkategorie ist eine Gruppierung von Quellen mit ähnlichen Eigenschaften.

**Source-Connector**: Source-Connectoren (auch als Quellen bezeichnet) helfen Benutzern, Daten aus verschiedenen Quellen einfach zu erfassen, sodass Daten mithilfe von Experience Platform-Diensten strukturiert, beschriftet und verbessert werden können. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Cloud-basiertem Speicher, Software von Drittanbietern und CRM-Systemen.

**Streaming-Verbindung**: Eine Streaming-Verbindung ist ein eindeutiger Endpunkt, der von Adobe bereitgestellt und an Ihr Unternehmen gebunden wird, um Daten an Experience Platform zu streamen.

**Standardatdentitäts-Namespace**: Standardidentitäts-Namespaces sind vordefinierte Identitäts-Namespaces, die von Adobe bereitgestellt werden und branchenübliche Lösungen darstellen, mit denen Kunden identifiziert werden.

**Streaming-Erfassung**: Mit der Streaming-Erfassung können Sie Daten von Client- und Server-seitigen Geräten in Echtzeit an Experience Platform senden.

**Streaming-Segmentierung**: Streaming-Segmentierung ist ein fortlaufender Datenauswahlprozess, der Segmente als Reaktion auf Benutzeraktivitäten aktualisiert. Nachdem ein Segment erstellt und gespeichert wurde, wird die Segmentdefinition auf in [!DNL Real-Time Customer Profile] eingehende Daten angewendet. Segmenthinzufügungen und -entfernungen werden regelmäßig verarbeitet, um sicherzustellen, dass Ihre Zielgruppe relevant bleibt.

**Systemansicht**: Die Systemansicht ist eine visuelle Darstellung von Quelldatensätzen, die durch [!DNL Real-Time Customer Profile] zu Zielen geleitet werden.

## T

**Tags**: In Adobe Experience Platform bieten Tags Tools zum Bereitstellen, Vereinheitlichen und Verwalten von Analyse-, Marketing- und Werbe-Integrationen, die für relevante Kundenerlebnisse auf allen Clientgeräten erforderlich sind.

**Target-Funktionen**: Bei der Funktionszuordnung ist eine Zielfunktion die Funktion, die von einem Modell vorhergesagt wird.

**Zeitreihendaten**: Zeitreihendaten liefern eine Momentaufnahme des Systems zum Zeitpunkt, zu dem eine Aktion entweder direkt oder indirekt von einem Datensatzsubjekt durchgeführt wurde.

**Trainiertes Modell**: Ein trainiertes Modell stellt die ausführbare Ausgabe eines Modell-Trainings-Prozesses dar, in dem ein Satz von Trainings-Daten auf die Modellinstanz angewendet wurde. Ein trainiertes Modell behält einen Verweis auf jeden intelligenten Webdienst bei, der daraus erstellt wird. Ein trainiertes Modell eignet sich zum Scoring und zur Erstellung eines intelligenten Webdienstes.

**Token**: Ein Token ist eine Art zweifaktorieller Authentifizierungssicherheit, die verwendet werden kann, um die Verwendung von Computerdiensten mit [!DNL Query Service] zu autorisieren.

## U

**UCPA**: Der [[!DNL Utah Consumer Privacy Act]](https://le.utah.gov/~2022/bills/static/SB0227.html) schafft das Recht eines Verbrauchers zu erfahren, welche personenbezogenen Daten ein Unternehmen erfasst, wie das Unternehmen seine personenbezogenen Daten verwendet und ob das Unternehmen seine personenbezogenen Daten verkauft. Verbraucher können von Unternehmen verlangen, ihre personenbezogenen Daten zu löschen oder nicht mehr zu verkaufen.

**Vereinigungsschema**: Ein Vereinigungsschema ist eine Konsolidierung von Schemas, die dieselbe Klasse teilen und für [!DNL Real-Time Customer Profile] aktiviert wurden. Für eine Organisation können mehrere Vereinigungsschemas vorhanden sein, es kann jedoch pro Klasse nur ein Vereinigungsschema geben.

## V

**VCDPA**: Der [[!DNL Virginia Consumer Data Protection Act (VCDPA)]](https://lis.virginia.gov/cgi-bin/legp604.exe?212+sum+HB2307) bietet neuen Datenschutzrechten für Virginia-Einwohner (&quot;Verbraucher&quot;), einschließlich des Rechts, auf personenbezogene Daten zuzugreifen, sie zu löschen und zu korrigieren. Die Verbraucher haben auch das Recht, sich vom Verkauf personenbezogener Daten abzumelden, sich gegen die Profilerstellung auf der Grundlage personenbezogener Daten zu entscheiden und persönliche Werbezwecke zu bearbeiten.

## W

## X

**XDM**: Siehe Experience-Datenmodell (XDM).

**XDM-Entscheidungsereignis**: XDM-Entscheidungsereignis ist eine zeitreihenbasierte Klasse, mit der Beobachtungen zum Ergebnis und zum Kontext einer Entscheidungsaktivität erfasst werden. Dazu gehören Informationen darüber, wie die Entscheidung getroffen wurde, wann sie erfolgte, welche Optionen vorgeschlagen (und ausgewählt) wurden und welcher kontextbezogene Zustand existierte, der entweder die Entscheidung beeinflusst hat oder während des Entscheidungsprozesses beobachtet werden konnte.

**XDM ExperienceEvent**: XDM ExperienceEvent ist eine zeitreihenbasierte Klasse, mit der der Status des Systems beim Eintreten eines Ereignisses (oder einer Reihe von Ereignissen) erfasst wird, einschließlich des Zeitpunkts und der Identität des beteiligten Subjekts. Siehe auch: Erlebnisereignis

**XDM Individual Profile**: XDM [!DNL Individual Profile] ist eine auf einem Datensatz basierende Klasse, die eine Singular-Darstellung der Attribute sowohl identifizierter als auch teilweise identifizierter Personen bildet. Hochgradig identifizierte Profile können für die persönliche Kommunikation oder zielgerichtete Interaktionen verwendet werden und detaillierte persönliche Informationen wie Name, Geschlecht, Geburtsdatum, Ort und Kontaktinformationen, einschließlich Telefonnummern und E-Mail-Adressen, enthalten.

**XDM-System**: XDM System stellt das Framework dar, das XDM-Schemas für die Verwendung in nachgelagerten Experience Platform-Diensten operationalisiert.

## Y

## Z
