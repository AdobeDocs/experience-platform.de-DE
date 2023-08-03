---
keywords: Experience Platform;Aktivierung;Fehlerbehebung;Leitplanken;Richtlinien;Limit
title: Standard-Leitplanken für Aktivierungsdaten
solution: Experience Platform
product: experience platform
type: Documentation
description: Erfahren Sie mehr über die Standardnutzung und die Ratenbeschränkungen für die Datenaktivierung.
exl-id: a755f224-3329-42d6-b8a9-fadcf2b3ca7b
source-git-commit: 51f65799a45229fc810a1d41f8b40b215d3666da
workflow-type: tm+mt
source-wordcount: '1272'
ht-degree: 77%

---

# Leitplanken für Aktivierungsdaten

Auf dieser Seite finden Sie standardmäßige Nutzungs- und Ratenbeschränkungen in Bezug auf das Aktivierungsverhalten. Bei der Betrachtung der folgenden Leitplanken wird angenommen, dass Sie eine ordnungsgemäße [Verbindung zu Zielen hergestellt haben](/help/destinations/ui/connect-destination.md).

>[!NOTE]
>
>* Die meisten Kunden überschreiten diese Standardbeschränkungen nicht. Wenden Sie sich an Ihren Kundenbetreuer, wenn Sie mehr über benutzerdefinierte Beschränkungen erfahren möchten.
>* Die in diesem Dokument dargelegten Beschränkungen werden ständig verbessert. Achten Sie regelmäßig auf Updates.
>* Je nach den individuellen Downstream-Beschränkungen können einige Ziele engere Leitplanken als die auf dieser Seite dokumentierten haben. Stellen Sie sicher, dass Sie auch die Seite [Katalog](/help/destinations/catalog/overview.md) des Ziels, zu dem Sie Daten verbinden und aktivieren, überprüfen.

## Arten von Beschränkungen {#limit-types}

In diesem Dokument gibt es zwei Arten von Standardbeschränkungen:

* **Weiche Grenze:** Es ist möglich, über eine weiche Grenze hinauszugehen, jedoch bieten weiche Grenzen eine empfohlene Richtlinie für die Systemleistung.
* **Feste Grenze**: Eine feste Grenze bietet ein absolutes Maximum. Die Experience Platform-Benutzeroberfläche oder die API erlaubt es Ihnen nicht, dieses Limit zu überschreiten, oder es wird bei Überschreitung ein Fehler zurückgegeben.


## Aktivierungsbeschränkungen {#activation-limits}

Die folgenden Limits bieten empfohlene Einschränkungen bei der Aktivierung von Echtzeit-Kundenprofildaten für Ziele.

### Allgemeine Aktivierungsleitplanken {#general-activation-guardrails}

Die folgenden Leitplanken gelten generell für die Aktivierung durch [alle Zieltypen](/help/destinations/destination-types.md#destination-types).

| Leitplanke | Limit | Art von Limit | Beschreibung |
| --- | --- | --- | --- |
| Maximale Anzahl an Zielgruppen zu einem einzelnen Ziel | 250 | Soft | Es wird empfohlen, maximal 250 Zielgruppen einem einzelnen Ziel in einem Datenfluss zuzuordnen. <br><br> Wenn Sie mehr als 250 Zielgruppen für ein Ziel aktivieren müssen, haben Sie folgende Möglichkeiten: <ul><li> die Zuordnung von Zielgruppen aufheben, die Sie nicht mehr aktivieren möchten, oder</li><li>Erstellen Sie einen neuen Datenfluss zum gewünschten Ziel und ordnen Sie Zielgruppen diesem neuen Datenfluss zu.</li></ul> <br> Beachten Sie, dass Sie bei einigen Zielen auf weniger als 250 Zielgruppen beschränkt sein können, die dem Ziel zugeordnet sind. Diese Ziele werden weiter unten auf der Seite in den jeweiligen Abschnitten aufgeführt. |
| Maximale Anzahl von Zielen | 100 | Soft | Es wird empfohlen, maximal 100 Ziele zu erstellen, mit denen Sie *pro Sandbox* Daten verbinden und aktivieren können. [Edge-Personalisierungsziele (benutzerdefinierte Personalisierung)](#edge-destinations-activation) können maximal 10 der 100 empfohlenen Ziele ausmachen. |
| Maximale Anzahl von Attributen, die einem Ziel zugeordnet sind | 50 | Soft | Bei mehreren Zielen und Zieltypen können Sie Profilattribute und Identitäten auswählen, die dem Export zugeordnet werden sollen. Für eine optimale Leistung sollten maximal 50 Attribute in einem Datenfluss einem Ziel zugeordnet werden. |
| Art der für Ziele aktivierten Daten | Profildaten, einschließlich Identitäten und Identitätszuordnung | Hard | Derzeit ist es nur möglich, *Profilsatzattribute* zu Zielen zu exportieren. XDM-Attribute, die Ereignisdaten beschreiben, werden derzeit nicht für den Export unterstützt. |
| Art der für Ziele aktivierten Daten – Unterstützung von Array- und Zuordnungsattributen | Nicht verfügbar | Hard | Zur Zeit ist es **nicht** möglich, *Array- oder Zuordnungsattribute* zu Zielen zu exportieren. Die Ausnahme von dieser Regel ist die [Identitätszuordnung](/help/xdm/field-groups/profile/identitymap.md), die sowohl bei Streaming- als auch bei dateibasierten Aktivierungen exportiert wird. |

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
| Aktivierungshäufigkeit | Ein vollständiger Export pro Tag oder häufigere inkrementelle Exporte alle 3, 6, 8 oder 12 Stunden. | Hard | Lesen Sie die Dokumentationsabschnitte [Vollständige Dateien exportieren](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) und [Inkrementelle Dateien exportieren](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) für weitere Informationen über die Häufigkeitsabstufungen für Batch-Exporte. |
| Maximale Anzahl an Zielgruppen, die zu einer bestimmten Stunde exportiert werden können | 100 | Soft | Es wird empfohlen, den Batch-Ziel-Datenflüssen maximal 100 Zielgruppen hinzuzufügen. |
| Maximale Anzahl der zu aktivierenden Zeilen (Datensätze) pro Datei | 5 Millionen | Hard | Adobe Experience Platform teilt die exportierten Dateien automatisch mit 5 Millionen Datensätzen (Zeilen) pro Datei auf. Jede Zeile stellt ein Profil dar. Bei aufgeteilten Dateien wird eine Nummer an den Namen angehängt, die anzeigt, dass die Datei Teil eines größeren Exports ist, z. B. `filename.csv`, `filename_2.csv`, `filename_3.csv`. Weitere Informationen finden Sie im [Planungsabschnitt](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) des Tutorials zum Aktivieren von Batch-Zielen. |

{style="table-layout:auto"}

### Ad-hoc-Aktivierung {#ad-hoc-activation}

Die folgenden Leitplanken gelten für die Methode der [Ad-hoc-Aktivierung](/help/destinations/api/ad-hoc-activation-api.md).

| Leitplanke | Limit | Art von Limit | Beschreibung |
| --- | --- | --- | --- |
| Zielgruppen, die pro Ad-hoc-Aktivierungsauftrag aktiviert werden | 80 | Hard | Derzeit kann jeder Ad-hoc-Aktivierungsauftrag bis zu 80 Zielgruppen aktivieren. Der Versuch, mehr als 80 Zielgruppen pro Auftrag zu aktivieren, führt dazu, dass der Auftrag fehlschlägt. Dieses Verhalten kann sich in zukünftigen Versionen ändern. |
| Gleichzeitige Ad-hoc-Aktivierungsaufträge pro Zielgruppe | 1 | Hard | Führen Sie nicht mehr als einen gleichzeitigen Ad-hoc-Aktivierungsauftrag pro Zielgruppe aus. |

{style="table-layout:auto"}

### Aktivierung von Edge-Personalisierungszielen {#edge-destinations-activation}

Die folgenden Leitplanken gelten für die Aktivierung durch [Edge-Personalisierungsziele](/help/destinations/destination-types.md#streaming-profile-export).

| Leitplanke | Limit | Art von Limit | Beschreibung |
| --- | --- | --- | --- |
| Maximale Anzahl an Zielen der [benutzerdefinierten Personalisierung](/help/destinations/catalog/personalization/custom-personalization.md) | 10 | Soft | Sie können Datenflüsse zu 10 benutzerdefinierten Personalisierungszielen pro Sandbox einrichten. |
| Maximale Anzahl von Attributen, die einem Personalisierungsziel pro Sandbox zugeordnet sind | 30 | Hard | Pro Sandbox können maximal 30 Attribute in einem Datenfluss einem Personalisierungsziel zugeordnet werden. |
| Maximale Anzahl von Zielgruppen, die einer einzelnen [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) Ziel | 50 | Soft | Sie können maximal 50 Zielgruppen in einem Aktivierungsfluss zu einem einzelnen Adobe Target-Ziel aktivieren. |

{style="table-layout:auto"}

### [!BADGE Beta]{type=Informative} Datensatzexporte {#dataset-exports}

Datensatzexporte werden derzeit in einer **[!UICONTROL Zuerst vollständig und dann inkrementell]** [pattern](/help/destinations/ui/export-datasets.md#scheduling). Die in diesem Abschnitt beschriebenen Limits gelten für den ersten vollständigen Export, der nach der Einrichtung eines Workflows für den Datensatzexport erfolgt.

| Leitplanke | Limit | Art von Limit | Beschreibung |
| --- | --- | --- | --- |
| Größe der exportierten Datensätze | 5 Mrd. | Soft | Die hier beschriebene Beschränkung für Datensatzexporte ist eine *Soft Guardral*. Die Benutzeroberfläche blockiert Sie zwar nicht daran, Datensätze zu exportieren, die über 5 Milliarden Datensätze hinausgehen, das Verhalten ist jedoch unvorhersehbar und Exporte schlagen möglicherweise fehl oder haben eine sehr lange Exportlatenz. |

{style="table-layout:auto"}

<!--

### Dataset Types {#dataset-types}

Datasets exported from Experience Platform can be of two types, as described below:

**Timeseries**
Timeseries datasets are also known as *XDM Experience Events* datasets in Experience Platform terminology.
The dataset schema includes a top level *timestamp* column. Data is ingested in an append-only fashion.

**Record** 
Record datasets are also known as *XDM Individual Profile* datasets in Experience Platform terminology.
The dataset schema does not include a top level *timestamp* column. Data is ingested in upsert fashion.

The guardrails below are grouped by the format of the exported file, and then further by dataset type.

**Parquet output**

|Dataset type | Compression | Guardrail | Description |
|---------|----------|---------|-----------|
| Timeseries | N/A | Last seven days per file | The data from the last seven days only is exported. |
| Record | N/A | Five billion records per file | Only the data from the last seven days is exported. |

{style="table-layout:auto"}

**JSON output**

|Dataset type | Compression | Guardrail | Description |
|---------|----------|---------|-----------|
| Timeseries | N/A | Last seven days per file | The data from the last seven days only is exported. |
| <p>Record</p> | <p><ul><li>Yes</li><li>No</li></ul></p> | <p><ul><li>Five billion records per compressed file</li><li>One million records per uncompressed file</li></ul></p> | <p>The record count of the dataset must be less than five billion for compressed files and one million for uncompressed files, otherwise the export fails. Reduce the size of the dataset that you are trying to export if it is larger than the allowed threshold.</p> |

{style="table-layout:auto"}

-->

<!--

<table>
<thead>
  <tr>
    <th>Output format</th>
    <th>Dataset type</th>
    <th>Compression</th>
    <th>Guardrail</th>
    <th>Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="2">Parquet</td>
    <td>Timeseries</td>
    <td>-</td>
    <td>Last seven days per file</td>
    <td>Only the data from the last seven days is exported.</td>
  </tr>
  <tr>
    <td>Record</td>
    <td>-</td>
    <td>Five billion records per file</td>
    <td>The record count of the dataset must be less than five billion, otherwise the export fails. Reduce the size of the dataset that you are trying to export if it is larger than the allowed threshold.</td>
  </tr>
  <tr>
    <td rowspan="3">JSON</td>
    <td>Timeseries</td>
    <td>-</td>
    <td>Last seven days per file</td>
    <td>Only the data from the last seven days is exported.</td>
  </tr>
  <tr>
    <td rowspan="2">Record</td>
    <td>Yes</td>
    <td>Five billion records per file</td>
    <td>The record count of the dataset must be less than five billion, otherwise the export fails. Reduce the size of the dataset that you are trying to export if it is larger than the allowed threshold.</td>
  </tr>
  <tr>
    <td>No</td>
    <td>One million records per file</td>
    <td>The record count of the dataset must be less than one million, otherwise the export fails. Reduce the size of the dataset that you are trying to export if it is larger than the allowed threshold.</td>
  </tr>
</tbody>
</table>

-->

### Leitplanken des Destination SDK {#destination-sdk-guardrails}

[Das Destination SDK](/help/destinations/destination-sdk/overview.md) ist eine Suite von Konfigurations-APIs, mit denen Sie Zielintegrationsmuster für Experience Platform konfigurieren können, um Zielgruppen- und Profildaten basierend auf den von Ihnen ausgewählten Daten- und Authentifizierungsformaten an Ihren Endpunkt zu senden. Die folgenden Leitplanken gelten für die Ziele, die Sie mit Destination SDK konfigurieren.

| Leitplanke | Limit | Art von Limit | Beschreibung |
| --- | --- | --- | --- |
| Maximale Anzahl an [privaten benutzerdefinierten Zielen](/help/destinations/destination-sdk/overview.md#productized-custom-integrations) | 5 | Soft | Sie können mit dem Destination SDK maximal fünf private benutzerdefinierte Streaming- oder Batch-Ziele erstellen. Wenden Sie sich an einen Kundenbetreuer, wenn Sie mehr als fünf solcher Ziele erstellen müssen. |
| Profilexportrichtlinie für das Destination SDK | <ul><li>`maxBatchAgeInSecs` (mindestens 1.800 und höchstens 3.600)</li><li>`maxNumEventsInBatch` (mindestens 1.000, höchstens 10.000)</li></ul> | Hard | Wenn Sie die Option [Konfigurierbare Aggregation](destination-sdk/functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) für Ihr Ziel verwenden, achten Sie auf die Mindest- und Höchstwerte, die festlegen, wie oft HTTP-Meldungen an Ihr API-basiertes Ziel gesendet werden und wie viele Profile die Meldungen enthalten sollen. |

{style="table-layout:auto"}

### Drosselung- und Wiederholungsrichtlinie für Ziele {#destination-throttling-and-retry-policy}

Details zu Drosselungsschwellwerten oder -beschränkungen für bestimmte Ziele. Dieser Abschnitt enthält auch Informationen zur Wiederholungsrichtlinie für Ziele.

| Zieltyp | Beschreibung |
| --- | --- |
| Unternehmensziele (HTTP-API, Amazon Kinesis, Azure EventHubs) | In 95 Prozent der Fälle versucht Experience Platform, eine Durchsatzlatenz von weniger als 10 Minuten für erfolgreich gesendete Nachrichten mit einer Rate von weniger als 10.000 Anfragen pro Sekunde für jeden Datenfluss an ein Unternehmensziel anzubieten. <br> Bei fehlgeschlagenen Anfragen an Ihr Unternehmensziel speichert Experience Platform die fehlgeschlagenen Anfragen und versucht es zweimal, die Anfragen an Ihren Endpunkt zu senden. |

{style="table-layout:auto"}

## Leitplanken für andere Services von Experience Platform {#guardrails-other-services}

Hier finden Sie Informationen zu Leitplanken für andere Experience Platform-Services:

* Schutzmaßnahmen bei der [Datenaufnahme](/help/ingestion/guardrails.md)
* Leitplanken für [[!DNL Identity Service] Daten](/help/identity-service/guardrails.md)
* Leitplanken für [[!DNL Real-Time Customer Profile] Daten](/help/profile/guardrails.md)
* Leitplanken für [[!DNL Query Service] Daten](/help/query-service/guardrails.md)
