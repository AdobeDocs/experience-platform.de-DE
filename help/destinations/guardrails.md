---
keywords: Experience Platform;Aktivierung;Fehlerbehebung;Leitplanken;Richtlinien;Limit
title: Standard-Leitplanken für die Datenaktivierung
solution: Experience Platform
product: experience platform
type: Documentation
description: Erfahren Sie mehr über die Standardnutzung und die Ratenbeschränkungen für die Datenaktivierung.
exl-id: a755f224-3329-42d6-b8a9-fadcf2b3ca7b
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1712'
ht-degree: 47%

---

# Leitplanken für die Datenaktivierung

>[!IMPORTANT]
>
>Überprüfen Sie zusätzlich zu dieser Seite mit Leitplanken Ihre Lizenzberechtigungen in Ihrem Kundenauftrag und [ entsprechenden ](https://helpx.adobe.com/de/legal/product-descriptions.html)Produktbeschreibung) die tatsächlichen Nutzungsbeschränkungen.

Auf dieser Seite finden Sie standardmäßige Nutzungs- und Ratenbeschränkungen in Bezug auf das Aktivierungsverhalten. Bei der Betrachtung der folgenden Leitplanken wird angenommen, dass Sie eine ordnungsgemäße [Verbindung zu Zielen hergestellt haben](/help/destinations/ui/connect-destination.md).

>[!NOTE]
>
>* Die meisten Kunden überschreiten diese Standardbeschränkungen nicht. Wenden Sie sich an Ihren Kundenbetreuer, wenn Sie mehr über benutzerdefinierte Beschränkungen erfahren möchten.
>* Die in diesem Dokument dargelegten Beschränkungen werden ständig verbessert. Suchen Sie regelmäßig nach Updates.
>* Je nach den individuellen Downstream-Beschränkungen können einige Ziele engere Leitplanken als die auf dieser Seite dokumentierten haben. Stellen Sie sicher, dass Sie auch die Seite [Katalog](/help/destinations/catalog/overview.md) des Ziels, zu dem Sie Daten verbinden und aktivieren, überprüfen.

## Schutzmechanismen-Typen {#limit-types}

In diesem Dokument gibt es zwei Arten von Standardbeschränkungen:

| Art der Leitplanke | Beschreibung |
|----------|---------|
| **Leistungs-Schutzmaßnahme (weiches Limit)** | Die Leistung betreffende Leitplanken sind Nutzungsbeschränkungen, die sich auf den Umfang Ihrer Anwendungsfälle beziehen. Beim Überschreiten der Leistungsleitplanken kann es zu Leistungseinbußen und Latenzzeiten kommen. Adobe ist für eine solche Leistungsbeeinträchtigung nicht verantwortlich. Kunden, die ständig eine Leistungsschutzmaßnahme überschreiten, können sich dafür entscheiden, zusätzliche Kapazität zu lizenzieren, um eine Leistungsbeeinträchtigung zu vermeiden. |
| **Vom System erzwungene Leitplanken (feste Grenze)** | Systemerzwungene Leitplanken werden von der Real-Time CDP-Benutzeroberfläche oder -API erzwungen. Dies sind Beschränkungen, die Sie nicht überschreiten können, da die Benutzeroberfläche und die API Sie daran hindern oder einen Fehler zurückgeben. |

{style="table-layout:auto"}


## Aktivierungsbeschränkungen {#activation-limits}

Die folgenden Leitplanken enthalten empfohlene Beschränkungen für die Aktivierung von Echtzeit-Kundenprofildaten für Ziele.

### Allgemeine Aktivierungsleitplanken {#general-activation-guardrails}

Die folgenden Leitplanken gelten generell für die Aktivierung durch [alle Zieltypen](/help/destinations/destination-types.md#destination-types).

| Leitplanke | Limit | Art von Limit | Beschreibung |
| --- | --- | --- | --- |
| Maximale Anzahl von Zielgruppen für ein einzelnes Ziel | 250 | Leistungs-Schutzmaßnahme | Es wird empfohlen, maximal 250 Zielgruppen einem einzelnen Ziel in einem Datenfluss zuzuordnen. <br><br> Wenn Sie mehr als 250 Zielgruppen für ein Ziel aktivieren müssen, haben Sie folgende Möglichkeiten: <ul><li> Heben Sie die Zuordnung von Zielgruppen auf, die Sie nicht mehr aktivieren möchten, oder</li><li>Erstellen Sie einen neuen Datenfluss zum gewünschten Ziel und ordnen Sie Zielgruppen diesem neuen Datenfluss zu.</li></ul> <br> Beachten Sie, dass Sie bei einigen Zielen auf weniger als 250 dem Ziel zugeordnete Zielgruppen beschränkt sein können. Diese Ziele werden weiter unten auf der Seite in den jeweiligen Abschnitten aufgeführt. |
| Maximale Anzahl von Attributen, die einem Ziel zugeordnet sind | 50 | Leistungs-Schutzmaßnahme | Bei mehreren Zielen und Zieltypen können Sie Profilattribute und Identitäten auswählen, die dem Export zugeordnet werden sollen. Für eine optimale Performance sollten maximal 50 Attribute in einem Datenfluss einem Ziel zugeordnet werden. |
| Maximale Anzahl von Zielen | 100 | Vom System erzwungene Leitplanken | Sie können maximal 100 Ziele erstellen, mit denen Sie (pro Sandbox) Daten verbinden *aktivieren*. [Edge-Personalisierungsziele (benutzerdefinierte Personalisierung)](#edge-destinations-activation) können maximal 10 der 100 empfohlenen Ziele ausmachen. |
| Art der für Ziele aktivierten Daten | Profildaten, einschließlich Identitäten und Identitätszuordnung | Vom System erzwungene Leitplanken | Derzeit ist es nur möglich, *Profileintragsattribute* zu Zielen zu exportieren. XDM-Attribute, die Ereignisdaten beschreiben, werden derzeit nicht für den Export unterstützt. |
| Art der für Ziele aktivierten Daten – Unterstützung von Array- und Zuordnungsattributen | Teilweise verfügbar | Vom System erzwungene Leitplanken | Sie können Array-Attribute in [dateibasierte Ziele“ ](/help/destinations/destination-types.md#file-based). [Weitere Informationen](/help/destinations/ui/export-arrays-maps-objects.md) über die Funktion. |

{style="table-layout:auto"}

### Streaming-Aktivierung {#streaming-activation}

Die folgenden Leitplanken gelten für die Aktivierung über [Streaming-Ziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

| Leitplanke | Limit | Art von Limit | Beschreibung |
| --- | --- | --- | --- |
| Anzahl der Aktivierungen (HTTP-Nachrichten mit Profilexporten) pro Sekunde | K. A. | – | Die Anzahl der Nachrichten pro Sekunde, die von Experience Platform an die API-Endpunkte der Partnerziele gesendet werden, ist derzeit nicht beschränkt. <br> Alle Beschränkungen oder Latenzen werden von dem Endpunkt bestimmt, der an Experience Platform Daten sendet. Stellen Sie sicher, dass Sie auch die [Katalog](/help/destinations/catalog/overview.md)-Seite des Ziels überprüfen, zu dem Sie Daten verbinden und aktivieren. |

{style="table-layout:auto"}

### Batch-Aktivierung (dateibasiert) {#batch-file-based-activation}

Die folgenden Leitplanken gelten für die Aktivierung über [Batch-Ziele (dateibasiert)](/help/destinations/ui/activate-batch-profile-destinations.md).

| Leitplanke | Limit | Art von Limit | Beschreibung |
| --- | --- | --- | --- |
| Aktivierungshäufigkeit | Ein vollständiger Export pro Tag oder häufigere inkrementelle Exporte alle 3, 6, 8 oder 12 Stunden. | Vom System erzwungene Leitplanken | Lesen Sie die Dokumentationsabschnitte [Vollständige Dateien exportieren](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) und [Inkrementelle Dateien exportieren](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) für weitere Informationen über die Häufigkeitsabstufungen für Batch-Exporte. |
| Maximale Anzahl von Zielgruppen, die zu einer bestimmten Stunde exportiert werden können | 100 | Leistungs-Schutzmaßnahme | Es wird empfohlen, maximal 100 Zielgruppen zu Batch-Ziel-Datenflüssen hinzuzufügen. |
| Maximale Anzahl der zu aktivierenden Zeilen (Einträge) pro Datei | 5 Millionen | Vom System erzwungene Leitplanken | Adobe Experience Platform teilt die exportierten Dateien automatisch mit 5 Millionen Einträgen (Zeilen) pro Datei auf. Jede Zeile stellt ein Profil dar. Bei aufgeteilten Dateien wird eine Nummer an den Namen angehängt, die anzeigt, dass die Datei Teil eines größeren Exports ist, z. B. `filename.csv`, `filename_2.csv`, `filename_3.csv`. Weitere Informationen finden Sie im [Planungsabschnitt](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) des Tutorials zum Aktivieren von Batch-Zielen. |
| Maximale Anzahl benutzerdefinierter Upload-Zielgruppen, die in einem Datenfluss aktiviert werden sollen | 10 | Vom System erzwungene Leitplanken | Beim Aktivieren [benutzerdefinierter Upload-](/help/segmentation/ui/audience-portal.md#import-audience)) für Batch-dateibasierte Ziele gibt es eine Beschränkung von 10 solcher Zielgruppen, die Sie in einem Datenfluss aktivieren können. Lesen Sie mehr über den Workflow zum [Aktivieren benutzerdefinierter Upload-Zielgruppen für Batch-dateibasierte Ziele](/help/destinations/ui/activate-batch-profile-destinations.md#select-audiences). |

{style="table-layout:auto"}

### Ad-hoc-Aktivierung {#ad-hoc-activation}

Die folgenden Leitplanken gelten für die Methode der [Ad-hoc-Aktivierung](/help/destinations/api/ad-hoc-activation-api.md).

| Leitplanke | Limit | Art von Limit | Beschreibung |
| --- | --- | --- | --- |
| Aktivierte Zielgruppen pro Ad-hoc-Aktivierungsauftrag | 80 | Vom System erzwungene Leitplanken | Derzeit kann jeder Ad-hoc-Aktivierungsauftrag bis zu 80 Zielgruppen aktivieren. Der Versuch, mehr als 80 Zielgruppen pro Auftrag zu aktivieren, führt zum Fehlschlagen des Auftrags. Dieses Verhalten kann sich in zukünftigen Versionen ändern. |
| Gleichzeitige Ad-hoc-Aktivierungsaufträge pro Zielgruppe | 1 | Vom System erzwungene Leitplanken | Führen Sie nicht mehr als einen gleichzeitigen Ad-hoc-Aktivierungsauftrag pro Zielgruppe aus. |

{style="table-layout:auto"}

### Aktivierung von Edge-Personalisierungszielen {#edge-destinations-activation}

Die folgenden Leitplanken gelten für die Aktivierung durch [Edge-Personalisierungsziele](/help/destinations/destination-types.md#advanced-enterprise-destinations).

| Leitplanke | Limit | Art von Limit | Beschreibung |
| --- | --- | --- | --- |
| Maximale Anzahl an Zielen der [benutzerdefinierten Personalisierung](/help/destinations/catalog/personalization/custom-personalization.md) | 10 | Leistungs-Schutzmaßnahme | Sie können Datenflüsse zu 10 benutzerdefinierten Personalisierungszielen pro Sandbox einrichten. |
| Maximale Anzahl von Attributen, die einem Personalisierungsziel pro Sandbox zugeordnet sind | 30 | Vom System erzwungene Leitplanken | Pro Sandbox können maximal 30 Attribute in einem Datenfluss einem Personalisierungsziel zugeordnet werden. |
| Maximale Anzahl von Zielgruppen, die einem einzelnen [Adobe Target-Ziel zugeordnet ](/help/destinations/catalog/personalization/adobe-target-connection.md) | 50 | Leistungs-Schutzmaßnahme | Sie können in einem Aktivierungsfluss maximal 50 Zielgruppen für ein einzelnes Adobe Target-Ziel aktivieren. |

{style="table-layout:auto"}

### Datensatzexporte {#dataset-exports}

Datensatzexporte werden derzeit in einem **[!UICONTROL First Full and then Incremental]** ([) ](/help/destinations/ui/export-datasets.md#scheduling). Die in diesem Abschnitt beschriebenen Leitplanken *gelten für den ersten vollständigen Export* der nach der Einrichtung eines Datensatzexport-Workflows erfolgt.

<!--

| Guardrail | Limit | Limit Type | Description |
| --- | --- | --- | --- |
| Size of exported datasets | 5 billion records | Soft | The limit described here for dataset exports is a *soft guardrail*. For example, while the user interface will not block you from exporting datasets larger than 5 billion records, the behavior is unpredictable and exports might either fail or have very long export latency. |

{style="table-layout:auto"}

-->

#### Datensatztypen {#dataset-types}

Die Leitplanken für den Datensatzexport gelten für zwei Arten von Datensätzen, die aus Experience Platform exportiert werden, wie unten beschrieben:

**Datensätze, die auf dem XDM-Erlebnisereignis-Schema basieren, und Datensätze, die auf einem anderen Schema basieren**

Bei Datensätzen, die auf dem XDM-Erlebnisereignis-Schema basieren, enthält das Datensatzschema eine Zeitstempelspalte der obersten Ebene. Die Daten werden nur angehängt aufgenommen. Bei Datensätzen, die auf einem anderen Schema basieren, kann das Datensatzschema eine Zeitstempelspalte enthalten, und die Daten werden upsert aufgenommen.

Die nachstehende weiche Leitplanke gilt für alle Datensätze, die aus Experience Platform exportiert wurden. Beachten Sie auch die weiter unten stehenden harten Leitplanken, die speziell für verschiedene Datensatz- und Komprimierungstypen gelten.

| Leitplanke | Limit | Art von Limit | Beschreibung |
| --- | --- | --- | --- |
| Größe der exportierten Datensätze | 5 Milliarden Datensätze | Leistungs-Schutzmaßnahme | Das hier beschriebene Limit für Datensatzexporte ist eine *weiche*. Während Sie beispielsweise durch die Benutzeroberfläche nicht daran gehindert werden, Datensätze zu exportieren, die größer als 5 Milliarden Datensätze sind, ist das Verhalten unvorhersehbar und Exporte können entweder fehlschlagen oder eine sehr lange Exportlatenz aufweisen. |

{style="table-layout:auto"}

#### Leitplanken für geplante Datensatzexporte

Bei geplanten oder wiederkehrenden Datensatzexporten sind die folgenden Leitplanken für die beiden Formate der exportierten Datei (JSON oder Parquet) identisch und werden nach Datensatztyp gruppiert.

>[!WARNING]
>
>Exporte in JSON-Dateien werden nur im komprimierten Modus unterstützt.

| Datensatztyp | Leitplanke | Art der Leitplanke | Beschreibung |
|---------|----------|---------|-------|
| Datensätze, die auf dem **XDM-Erlebnisereignis-Schema basieren** | Daten der letzten 365 Tage | Vom System erzwungene Leitplanken | Die Daten aus dem letzten Kalenderjahr werden exportiert. |
| Datensätze, die auf **einem beliebigen Schema außer dem XDM-Erlebnisereignis-Schema** | Zehn Milliarden Datensätze in allen exportierten Dateien in einem Datenfluss | Vom System erzwungene Leitplanken | Die Datensatzanzahl des Datensatzes muss bei komprimierten JSON- oder Parquet-Dateien weniger als zehn Milliarden und bei unkomprimierten Parquet-Dateien weniger als eine Million betragen, da der Export sonst fehlschlägt. Verringern Sie die Größe des Datensatzes, den Sie exportieren möchten, wenn er größer als der zulässige Schwellenwert ist. |

{style="table-layout:auto"}

<!--

#### Ad-hoc dataset exports

Exporting datasets in an-hoc manner is currently supported via API only. For ad-hoc dataset exports, you must use the backfill parameter in the API to limit the timeframe of exported data. 

The guardrails below are the same whether you are exporting parquet of JSON files ad-hoc. 

**Parquet and JSON output**

|Dataset type | Backfill parameter provided | Guardrail | Guardrail type | Description |
|---------|---------|-----------|-----------|------------|
| Datasets based on the **XDM Experience Events schema** |  <p><ul><li>Both start and end date provided in `backfill` parameter in API call</li><li>Incomplete `backfill` parameter provided in API call</li></ul></p> | <p><ul><li>Last 30 days</li><li>Last 365 days</li></ul></p> | Hard | <p><ul><li>The export fails if the `startDate - endDate` interval is over 30 days</li><li>Either the `startDate` or `endDate` are missing or  incorrectly formatted in the API call. Expected format: `yyyy-MM-dd'T'HH:mm:ss.SSS'Z'`</li></ul></p> |
| Datasets based on the **XDM Individual Profile schema** |  - | Ten billion records across all files exported in a dataflow | Hard | The record count of the dataset must be less than ten billion for compressed JSON or parquet files and one million for uncompressed parquet files, otherwise the export fails. Reduce the size of the dataset that you are trying to export if it is larger than the allowed threshold. |

{style="table-layout:auto"}

-->

Weitere Informationen über [Exportieren von Datensätzen](/help/destinations/ui/export-datasets.md).


### Leitplanken des Destination SDK {#destination-sdk-guardrails}

[Das Destination SDK](/help/destinations/destination-sdk/overview.md) ist eine Suite von Konfigurations-APIs, mit denen Sie Zielintegrationsmuster für Experience Platform konfigurieren können, um Zielgruppen- und Profildaten basierend auf den von Ihnen ausgewählten Daten- und Authentifizierungsformaten an Ihren Endpunkt zu senden. Die folgenden Leitplanken gelten für die Ziele, die Sie mit Destination SDK konfigurieren.

| Leitplanke | Limit | Art von Limit | Beschreibung |
| --- | --- | --- | --- |
| Maximale Anzahl an [privaten benutzerdefinierten Zielen](/help/destinations/destination-sdk/overview.md#productized-custom-integrations) | 5 | Leistungs-Schutzmaßnahme | Sie können mit dem Destination SDK maximal fünf private benutzerdefinierte Streaming- oder Batch-Ziele erstellen. Wenden Sie sich an einen Kundenbetreuer, wenn Sie mehr als fünf solcher Ziele erstellen müssen. |
| Profilexportrichtlinie für das Destination SDK | <ul><li>`maxBatchAgeInSecs` (mindestens 1.800 und höchstens 3.600)</li><li>`maxNumEventsInBatch` (mindestens 1.000 und höchstens 10.000)</li></ul> | Vom System erzwungene Leitplanken | Wenn Sie die Option [Konfigurierbare Aggregation](destination-sdk/functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) für Ihr Ziel verwenden, achten Sie auf die Mindest- und Höchstwerte, die festlegen, wie oft HTTP-Meldungen an Ihr API-basiertes Ziel gesendet werden und wie viele Profile die Meldungen enthalten sollen. |

{style="table-layout:auto"}

### Drosselung- und Wiederholungsrichtlinie für Ziele {#destination-throttling-and-retry-policy}

Details zu Drosselungsschwellwerten oder -beschränkungen für bestimmte Ziele. Dieser Abschnitt enthält auch Informationen zur Wiederholungsrichtlinie für Ziele.

| Zieltyp | Beschreibung |
| --- | --- |
| Unternehmensziele (HTTP-API, Amazon Kinesis, Azure EventHubs) | In 95 Prozent der Fälle versucht Experience Platform, eine Durchsatzlatenz von weniger als 10 Minuten für erfolgreich gesendete Nachrichten mit einer Rate von weniger als 10.000 Anfragen pro Sekunde für jeden Datenfluss an ein Unternehmensziel anzubieten. <br> Bei fehlgeschlagenen Anfragen an Ihr Unternehmensziel speichert Experience Platform die fehlgeschlagenen Anfragen und versucht es zweimal, die Anfragen an Ihren Endpunkt zu senden. |

{style="table-layout:auto"}

## Nächste Schritte

In der folgenden Dokumentation finden Sie weitere Informationen zu anderen Experience Platform-Services-Leitplanken, zu End-to-End-Latenzinformationen und Lizenzinformationen aus Real-Time CDP-Produktbeschreibungsdokumenten:

* [Real-Time CDP-Leitplanken](/help/rtcdp/guardrails/overview.md)
* [End-to-End-Latenzdiagramme](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) für verschiedene Experience Platform-Services.
* [Real-Time Customer Data Platform (B2C Edition - Prime- und Ultimate-Pakete)](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2P - Prime- und Ultimate-Pakete)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2B - Prime- und Ultimate-Pakete)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
