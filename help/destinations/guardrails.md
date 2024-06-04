---
keywords: Experience Platform;Aktivierung;Fehlerbehebung;Leitplanken;Richtlinien;Limit
title: Standardmäßige Limits für die Datenaktivierung
solution: Experience Platform
product: experience platform
type: Documentation
description: Erfahren Sie mehr über die Standardnutzung und die Ratenbeschränkungen für die Datenaktivierung.
exl-id: a755f224-3329-42d6-b8a9-fadcf2b3ca7b
source-git-commit: 5d6b70e397a252e037589c3200053ebcb7eb8291
workflow-type: tm+mt
source-wordcount: '1685'
ht-degree: 51%

---

# Limits für die Datenaktivierung

>[!IMPORTANT]
>
>Überprüfen Sie Ihre Lizenzberechtigungen in Ihrem Kundenauftrag und den entsprechenden [Produktbeschreibung](https://helpx.adobe.com/de/legal/product-descriptions.html) über die tatsächlichen Nutzungsbeschränkungen zusätzlich zu dieser Limits-Seite.

Auf dieser Seite finden Sie standardmäßige Nutzungs- und Ratenbeschränkungen in Bezug auf das Aktivierungsverhalten. Bei der Betrachtung der folgenden Leitplanken wird angenommen, dass Sie eine ordnungsgemäße [Verbindung zu Zielen hergestellt haben](/help/destinations/ui/connect-destination.md).

>[!NOTE]
>
>* Die meisten Kunden überschreiten diese Standardbeschränkungen nicht. Wenden Sie sich an Ihren Kundenbetreuer, wenn Sie mehr über benutzerdefinierte Beschränkungen erfahren möchten.
>* Die in diesem Dokument dargelegten Beschränkungen werden ständig verbessert. Suchen Sie regelmäßig nach Updates.
>* Je nach den individuellen Downstream-Beschränkungen können einige Ziele engere Leitplanken als die auf dieser Seite dokumentierten haben. Stellen Sie sicher, dass Sie auch die Seite [Katalog](/help/destinations/catalog/overview.md) des Ziels, zu dem Sie Daten verbinden und aktivieren, überprüfen.

## Schutzarten {#limit-types}

In diesem Dokument gibt es zwei Arten von Standardbeschränkungen:

| Schutztyp | Beschreibung |
|----------|---------|
| **Leistungsgarantie (weiche Begrenzung)** | Leistungsgarantien sind Nutzungsbeschränkungen, die sich auf das Scoping Ihrer Anwendungsfälle beziehen. Wenn Sie die Leistungsgarantien überschreiten, kann es zu Leistungseinbußen und Latenzzeiten kommen. Adobe ist nicht für eine solche Leistungsbeeinträchtigung verantwortlich. Kunden, die eine Leistungsgarantie konsequent überschreiten, können zusätzliche Kapazität lizenzieren, um Leistungsbeeinträchtigungen zu vermeiden. |
| **Systemerzwungene Limits (Hard Limit)** | Systemerzwungene Limits werden von der Real-Time CDP-Benutzeroberfläche oder -API erzwungen. Dies sind Beschränkungen, die Sie nicht überschreiten können, da die Benutzeroberfläche und API Sie davon abhält oder einen Fehler zurückgibt. |

{style="table-layout:auto"}


## Aktivierungsbeschränkungen {#activation-limits}

Die folgenden Limits bieten empfohlene Einschränkungen bei der Aktivierung von Echtzeit-Kundenprofildaten für Ziele.

### Allgemeine Aktivierungsleitplanken {#general-activation-guardrails}

Die folgenden Leitplanken gelten generell für die Aktivierung durch [alle Zieltypen](/help/destinations/destination-types.md#destination-types).

| Leitplanke | Limit | Art von Limit | Beschreibung |
| --- | --- | --- | --- |
| Maximale Anzahl an Zielgruppen zu einem einzelnen Ziel | 250 | Leistungsgarantie | Es wird empfohlen, maximal 250 Zielgruppen einem einzelnen Ziel in einem Datenfluss zuzuordnen. <br><br> Wenn Sie mehr als 250 Zielgruppen für ein Ziel aktivieren müssen, haben Sie folgende Möglichkeiten: <ul><li> die Zuordnung von Zielgruppen aufheben, die Sie nicht mehr aktivieren möchten, oder</li><li>Erstellen Sie einen neuen Datenfluss zum gewünschten Ziel und ordnen Sie Zielgruppen diesem neuen Datenfluss zu.</li></ul> <br> Beachten Sie, dass Sie bei einigen Zielen auf weniger als 250 Zielgruppen beschränkt sein können, die dem Ziel zugeordnet sind. Diese Ziele werden weiter unten auf der Seite in den jeweiligen Abschnitten aufgeführt. |
| Maximale Anzahl von Attributen, die einem Ziel zugeordnet sind | 50 | Leistungsgarantie | Bei mehreren Zielen und Zieltypen können Sie Profilattribute und Identitäten auswählen, die dem Export zugeordnet werden sollen. Für eine optimale Performance sollten maximal 50 Attribute in einem Datenfluss einem Ziel zugeordnet werden. |
| Maximale Anzahl von Zielen | 100 | Systemerzwungene Limits | Sie können maximal 100 Ziele erstellen, mit denen Sie Daten verbinden und aktivieren können. *per Sandbox*. [Edge-Personalisierungsziele (benutzerdefinierte Personalisierung)](#edge-destinations-activation) können maximal 10 der 100 empfohlenen Ziele ausmachen. |
| Art der für Ziele aktivierten Daten | Profildaten, einschließlich Identitäten und Identitätszuordnung | Systemerzwungene Limits | Derzeit ist es nur möglich, *Profilsatzattribute* zu Zielen zu exportieren. XDM-Attribute, die Ereignisdaten beschreiben, werden derzeit nicht für den Export unterstützt. |
| Art der für Ziele aktivierten Daten – Unterstützung von Array- und Zuordnungsattributen | Nicht verfügbar | Systemerzwungene Limits | Zur Zeit ist es **nicht** möglich, *Array- oder Zuordnungsattribute* zu Zielen zu exportieren. Die Ausnahme von dieser Regel ist die [Identitätszuordnung](/help/xdm/field-groups/profile/identitymap.md), die sowohl bei Streaming- als auch bei dateibasierten Aktivierungen exportiert wird. |

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
| Aktivierungshäufigkeit | Ein vollständiger Export pro Tag oder häufigere inkrementelle Exporte alle 3, 6, 8 oder 12 Stunden. | Systemerzwungene Limits | Lesen Sie die Dokumentationsabschnitte [Vollständige Dateien exportieren](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) und [Inkrementelle Dateien exportieren](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) für weitere Informationen über die Häufigkeitsabstufungen für Batch-Exporte. |
| Maximale Anzahl an Zielgruppen, die zu einer bestimmten Stunde exportiert werden können | 100 | Leistungsgarantie | Es wird empfohlen, den Batch-Ziel-Datenflüssen maximal 100 Zielgruppen hinzuzufügen. |
| Maximale Anzahl der zu aktivierenden Zeilen (Datensätze) pro Datei | 5 Millionen | Systemerzwungene Limits | Adobe Experience Platform teilt die exportierten Dateien automatisch mit 5 Millionen Datensätzen (Zeilen) pro Datei auf. Jede Zeile stellt ein Profil dar. Bei aufgeteilten Dateien wird eine Nummer an den Namen angehängt, die anzeigt, dass die Datei Teil eines größeren Exports ist, z. B. `filename.csv`, `filename_2.csv`, `filename_3.csv`. Weitere Informationen finden Sie im [Planungsabschnitt](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) des Tutorials zum Aktivieren von Batch-Zielen. |

{style="table-layout:auto"}

### Ad-hoc-Aktivierung {#ad-hoc-activation}

Die folgenden Leitplanken gelten für die Methode der [Ad-hoc-Aktivierung](/help/destinations/api/ad-hoc-activation-api.md).

| Leitplanke | Limit | Art von Limit | Beschreibung |
| --- | --- | --- | --- |
| Zielgruppen, die pro Ad-hoc-Aktivierungsauftrag aktiviert werden | 80 | Systemerzwungene Limits | Derzeit kann jeder Ad-hoc-Aktivierungsauftrag bis zu 80 Zielgruppen aktivieren. Der Versuch, mehr als 80 Zielgruppen pro Auftrag zu aktivieren, führt dazu, dass der Auftrag fehlschlägt. Dieses Verhalten kann sich in zukünftigen Versionen ändern. |
| Gleichzeitige Ad-hoc-Aktivierungsaufträge pro Zielgruppe | 1 | Systemerzwungene Limits | Führen Sie nicht mehr als einen gleichzeitigen Ad-hoc-Aktivierungsauftrag pro Zielgruppe aus. |

{style="table-layout:auto"}

### Aktivierung von Edge-Personalisierungszielen {#edge-destinations-activation}

Die folgenden Leitplanken gelten für die Aktivierung durch [Edge-Personalisierungsziele](/help/destinations/destination-types.md#streaming-profile-export).

| Leitplanke | Limit | Art von Limit | Beschreibung |
| --- | --- | --- | --- |
| Maximale Anzahl an Zielen der [benutzerdefinierten Personalisierung](/help/destinations/catalog/personalization/custom-personalization.md) | 10 | Leistungsgarantie | Sie können Datenflüsse zu 10 benutzerdefinierten Personalisierungszielen pro Sandbox einrichten. |
| Maximale Anzahl von Attributen, die einem Personalisierungsziel pro Sandbox zugeordnet sind | 30 | Systemerzwungene Limits | Pro Sandbox können maximal 30 Attribute in einem Datenfluss einem Personalisierungsziel zugeordnet werden. |
| Maximale Anzahl von Zielgruppen, die einer einzelnen [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) Ziel | 50 | Leistungsgarantie | Sie können maximal 50 Zielgruppen in einem Aktivierungsfluss zu einem einzelnen Adobe Target-Ziel aktivieren. |

{style="table-layout:auto"}

### Datensatzexporte {#dataset-exports}

Datensatzexporte werden derzeit in einer **[!UICONTROL Zuerst vollständig und dann inkrementell]** [pattern](/help/destinations/ui/export-datasets.md#scheduling). Die in diesem Abschnitt beschriebenen Limits *auf die erste vollständige Ausfuhr* , das nach der Einrichtung eines Workflows für den Datensatzexport auftritt.

<!--

| Guardrail | Limit | Limit Type | Description |
| --- | --- | --- | --- |
| Size of exported datasets | 5 billion records | Soft | The limit described here for dataset exports is a *soft guardrail*. For example, while the user interface will not block you from exporting datasets larger than 5 billion records, the behavior is unpredictable and exports might either fail or have very long export latency. |

{style="table-layout:auto"}

-->

#### Datensatztypen {#dataset-types}

Die Limits für den Datensatzexport gelten für zwei vom Experience Platform exportierte Datensatztypen, wie unten beschrieben:

**Auf dem XDM-Erlebnisereignis-Schema basierende Datensätze**
Bei Datensätzen, die auf dem XDM Experience Events-Schema basieren, enthält das Datensatzschema eine oberste Ebene *timestamp* Spalte. Daten werden nur als Anhang erfasst.

**Auf dem Schema &quot;XDM Individual Profile&quot;basierende Datensätze**
Bei Datensätzen, die auf dem Schema &quot;XDM Individual Profile&quot;basieren, enthält das Datensatzschema keine oberste Ebene *timestamp* Spalte. Die Daten werden in aufbereiteter Weise erfasst.

Die nachstehende Limits gelten für alle Datensätze, die aus Experience Platform exportiert werden. Sehen Sie sich auch die unten aufgeführten harten Limits an, die für verschiedene Datensätze und Komprimierungstypen spezifisch sind.

| Leitplanke | Limit | Art von Limit | Beschreibung |
| --- | --- | --- | --- |
| Größe der exportierten Datensätze | 5 Mrd. | Leistungsgarantie | Die hier beschriebene Beschränkung für Datensatzexporte ist eine *Soft Guardral*. Die Benutzeroberfläche blockiert Sie zwar nicht daran, Datensätze zu exportieren, die über 5 Milliarden Datensätze hinausgehen, das Verhalten ist jedoch unvorhersehbar und Exporte schlagen möglicherweise fehl oder haben eine sehr lange Exportlatenz. |

{style="table-layout:auto"}

#### Limits für geplante Datensatzexporte

Bei geplanten oder wiederkehrenden Datensatzexporten sind die folgenden Limits für die beiden Formate der exportierten Datei (JSON oder Parquet) identisch und werden nach Datensatztyp gruppiert.

>[!WARNING]
>
>Exporte in JSON-Dateien werden nur im komprimierten Modus unterstützt.

| Datensatztyp | Leitplanke | Schutztyp | Beschreibung |
---------|----------|---------|-------|
| Auf der Variablen **XDM-Erlebnisereignisschema** | Daten der letzten 365 Tage | Systemerzwungene Limits | Die Daten des letzten Kalenderjahres werden exportiert. |
| Auf der Variablen **Schema &quot;XDM Individual Profile&quot;** | Zehn Milliarden Datensätze über alle exportierten Dateien in einem Datenfluss | Systemerzwungene Limits | Die Datensatzanzahl für komprimierte JSON- oder Parquet-Dateien muss weniger als zehn Milliarden und für unkomprimierte Parquet-Dateien eine Million betragen. Andernfalls schlägt der Export fehl. Reduzieren Sie die Größe des Datensatzes, den Sie exportieren möchten, wenn er den zulässigen Schwellenwert überschreitet. |

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

Mehr dazu [Exportieren von Datensätzen](/help/destinations/ui/export-datasets.md).


### Leitplanken des Destination SDK {#destination-sdk-guardrails}

[Das Destination SDK](/help/destinations/destination-sdk/overview.md) ist eine Suite von Konfigurations-APIs, mit denen Sie Zielintegrationsmuster für Experience Platform konfigurieren können, um Zielgruppen- und Profildaten basierend auf den von Ihnen ausgewählten Daten- und Authentifizierungsformaten an Ihren Endpunkt zu senden. Die folgenden Leitplanken gelten für die Ziele, die Sie mit Destination SDK konfigurieren.

| Leitplanke | Limit | Art von Limit | Beschreibung |
| --- | --- | --- | --- |
| Maximale Anzahl an [privaten benutzerdefinierten Zielen](/help/destinations/destination-sdk/overview.md#productized-custom-integrations) | 5 | Leistungsgarantie | Sie können mit dem Destination SDK maximal fünf private benutzerdefinierte Streaming- oder Batch-Ziele erstellen. Wenden Sie sich an einen Kundenbetreuer, wenn Sie mehr als fünf solcher Ziele erstellen müssen. |
| Profilexportrichtlinie für das Destination SDK | <ul><li>`maxBatchAgeInSecs` (mindestens 1.800 und höchstens 3.600)</li><li>`maxNumEventsInBatch` (mindestens 1.000, höchstens 10.000)</li></ul> | Systemerzwungene Limits | Wenn Sie die Option [Konfigurierbare Aggregation](destination-sdk/functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) für Ihr Ziel verwenden, achten Sie auf die Mindest- und Höchstwerte, die festlegen, wie oft HTTP-Meldungen an Ihr API-basiertes Ziel gesendet werden und wie viele Profile die Meldungen enthalten sollen. |

{style="table-layout:auto"}

### Drosselung- und Wiederholungsrichtlinie für Ziele {#destination-throttling-and-retry-policy}

Details zu Drosselungsschwellwerten oder -beschränkungen für bestimmte Ziele. Dieser Abschnitt enthält auch Informationen zur Wiederholungsrichtlinie für Ziele.

| Zieltyp | Beschreibung |
| --- | --- |
| Unternehmensziele (HTTP-API, Amazon Kinesis, Azure EventHubs) | In 95 Prozent der Fälle versucht Experience Platform, eine Durchsatzlatenz von weniger als 10 Minuten für erfolgreich gesendete Nachrichten mit einer Rate von weniger als 10.000 Anfragen pro Sekunde für jeden Datenfluss an ein Unternehmensziel anzubieten. <br> Bei fehlgeschlagenen Anfragen an Ihr Unternehmensziel speichert Experience Platform die fehlgeschlagenen Anfragen und versucht es zweimal, die Anfragen an Ihren Endpunkt zu senden. |

{style="table-layout:auto"}

## Nächste Schritte

Weitere Informationen zu anderen Limits für Experience Platform-Services, End-to-End-Latenzinformationen und Lizenzinformationen aus Real-Time CDP Product Description-Dokumenten finden Sie in der folgenden Dokumentation:

* [Limits in Real-Time CDP](/help/rtcdp/guardrails/overview.md)
* [End-to-End-Latenzdiagramme](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) für verschiedene Experience Platform-Dienste.
* [Real-time Customer Data Platform (B2C Edition - Prime und Ultimate Packages)](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2P - Prime und Ultimate Packages)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2B - Prime und Ultimate Packages)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
