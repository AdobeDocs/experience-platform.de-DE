---
keywords: Experience Platform;Aktivierung;Fehlerbehebung;Limits;Richtlinien;Begrenzung
title: Standardmäßige Limits für Aktivierungsdaten
solution: Experience Platform
product: experience platform
type: Documentation
description: Erfahren Sie mehr über die Standardnutzung und die Ratenbeschränkungen für die Datenaktivierung.
source-git-commit: 69496d2e00ce866413786160d4524cabd03ae350
workflow-type: tm+mt
source-wordcount: '1198'
ht-degree: 18%

---

# Schutzmechanismen für Aktivierungsdaten

Auf dieser Seite finden Sie standardmäßige Nutzungs- und Ratenbeschränkungen im Hinblick auf das Aktivierungsverhalten. Bei der Überprüfung der folgenden Limits wird davon ausgegangen, dass Sie [mit Zielen verbunden](/help/destinations/ui/connect-destination.md).

>[!NOTE]
>
>* Die meisten Kunden überschreiten diese Standardbeschränkungen nicht. Wenden Sie sich an Ihren Kundenbetreuer, wenn Sie mehr über benutzerdefinierte Beschränkungen erfahren möchten.
>* Die in diesem Dokument dargelegten Beschränkungen werden ständig verbessert. Achten Sie regelmäßig auf Updates.
>* Abhängig von den einzelnen nachgelagerten Beschränkungen bieten einige Ziele möglicherweise strengere Limits als die auf dieser Seite dokumentierten. Überprüfen Sie auch die [Katalog](/help/destinations/catalog/overview.md) Seite des Ziels, mit dem Sie Daten verbinden und aktivieren möchten.


## Arten von Beschränkungen {#limit-types}

In diesem Dokument gibt es zwei Arten von Standardbeschränkungen:

* **Weiche Grenze:** Es ist möglich, über eine weiche Grenze hinauszugehen, jedoch bieten weiche Grenzen eine empfohlene Richtlinie für die Systemleistung.
* **Harte Grenze:** Eine harte Grenze bietet ein absolutes Maximum. Die Experience Platform-Benutzeroberfläche oder -API erlaubt es Ihnen nicht, diese Beschränkung zu überschreiten. Wenn Sie diese Beschränkung überschreiten, wird ein Fehler zurückgegeben.


## Aktivierungsbeschränkungen {#activation-limits}

Die folgenden Limits bieten empfohlene Einschränkungen bei der Aktivierung von Echtzeit-Kundenprofildaten für Ziele.

### Allgemeine Aktivierungsgarantien {#general-activation-guardrails}

Die nachstehenden Limits gelten im Allgemeinen für die Aktivierung durch [alle Zieltypen](/help/destinations/destination-types.md#destination-types).

| Beschränkung | Limit | Art von Limit | Beschreibung |
| --- | --- | --- | --- |
| Maximale Anzahl von Segmenten an ein einzelnes Ziel | 250 | Soft | Es wird empfohlen, maximal 250 Segmente einem einzelnen Ziel in einem Datenfluss zuzuordnen. <br><br> Wenn Sie mehr als 250 Segmente für ein Ziel aktivieren müssen, haben Sie folgende Möglichkeiten: <ul><li> Aufheben der Zuordnung von Segmenten, die Sie nicht mehr aktivieren möchten, oder</li><li>Erstellen Sie einen neuen Datenfluss zum gewünschten Ziel und ordnen Sie diesem neuen Datenfluss Segmente zu.</li></ul> <br> Beachten Sie, dass Sie bei einigen Zielen auf weniger als 250 Segmente beschränkt sein können, die dem Ziel zugeordnet sind. Diese Ziele werden weiter unten auf der Seite in den entsprechenden Abschnitten aufgerufen. |
| Maximale Anzahl von Zielen | 100 | Soft | Es wird empfohlen, maximal 100 Ziele zu erstellen, mit denen Sie eine Verbindung herstellen und Daten aktivieren können *per Sandbox*. [Edge-Personalisierungsziele (benutzerdefinierte Personalisierung)](#edge-destinations-activation) kann maximal 10 der 100 empfohlenen Ziele ausmachen. |
| Maximale Anzahl von Attributen, die einem Ziel zugeordnet sind | 50 | Soft | Bei mehreren Zielen und Zieltypen können Sie Profilattribute und Identitäten auswählen, die für den Export zugeordnet werden sollen. Für eine optimale Leistung sollten maximal 50 Attribute in einem Datenfluss einem Ziel zugeordnet werden. |
| Art der für Ziele aktivierten Daten | Profildaten, einschließlich Identitäten und Identitätszuordnungen | Hard | Derzeit ist es nur möglich, *Profilattribute* zu Zielen. XDM-Attribute, die Ereignisdaten beschreiben, werden derzeit nicht für den Export unterstützt. |
| Art der für Ziele aktivierten Daten - Unterstützung von Array- und Zuordnungsattributen | Nicht verfügbar | Hard | Zu diesem Zeitpunkt ist es **not** Export möglich *Array- oder Zuordnungsattribute* zu Zielen. Die Ausnahme für diese Regel ist die [Identitätszuordnung](/help/xdm/field-groups/profile/identitymap.md), der sowohl bei Streaming- als auch bei dateibasierten Aktivierungen exportiert wird. |

{style=&quot;table-layout:auto&quot;}

### Streaming-Aktivierung {#streaming-activation}

Die folgenden Limits gelten für die Aktivierung durch [Streaming-Ziele](/help/destinations/ui/activate-segment-streaming-destinations.md).

| Beschränkung | Limit | Art von Limit | Beschreibung |
| --- | --- | --- | --- |
| Anzahl der Aktivierungen (HTTP-Nachrichten mit Profilexporten) pro Sekunde | K. A. | – | Die Anzahl der Nachrichten pro Sekunde, die von Experience Platform an die API-Endpunkte der Partnerziele gesendet werden, ist derzeit nicht beschränkt. <br> Einschränkungen oder Latenzen werden vom Endpunkt bestimmt, an den die Experience Platform Daten sendet. Überprüfen Sie auch die [Katalog](/help/destinations/catalog/overview.md) Seite des Ziels, mit dem Sie Daten verbinden und aktivieren möchten. |

{style=&quot;table-layout:auto&quot;}

### Batch-Aktivierung (dateibasiert) {#batch-file-based-activation}

Die folgenden Limits gelten für die Aktivierung durch [Batch-Ziele (dateibasiert)](/help/destinations/ui/activate-batch-profile-destinations.md).

| Beschränkung | Limit | Art von Limit | Beschreibung |
| --- | --- | --- | --- |
| Aktivierungsfrequenz | Ein täglicher vollständiger Export oder häufigere inkrementelle Exporte alle 3, 6, 8 oder 12 Stunden. | Hard | Lesen Sie die [vollständige Dateien exportieren](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) und [inkrementelle Dateien exportieren](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) Dokumentationsabschnitte mit weiteren Informationen zu den Frequenzinkrementen für Batch-Exporte. |
| Maximale Anzahl von Segmenten, die zu einer bestimmten Stunde exportiert werden können | 100 | Soft | Es wird empfohlen, Batch-Ziel-Datenflüssen maximal 100 Segmente hinzuzufügen. |
| Maximale Anzahl Zeilen (Datensätze) pro Datei zur Aktivierung | 5 Mio. | Hard | Adobe Experience Platform teilt die exportierten Dateien automatisch mit 5 Millionen Datensätzen (Zeilen) pro Datei auf. Jede Zeile stellt ein Profil dar. Bei aufgeteilten Dateien wird eine Nummer an den Namen angehängt, die anzeigt, dass die Datei Teil eines größeren Exports ist, z. B. `filename.csv`, `filename_2.csv`, `filename_3.csv`. Weitere Informationen finden Sie im Abschnitt [Planungsabschnitt](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) des Tutorials zum Aktivieren von Batch-Zielen. |

{style=&quot;table-layout:auto&quot;}

### Ad-hoc-Aktivierung {#ad-hoc-activation}

Die folgenden Limits gelten für die [Ad-hoc-Aktivierung](/help/destinations/api/ad-hoc-activation-api.md) -Methode.

| Beschränkung | Limit | Art von Limit | Beschreibung |
| --- | --- | --- | --- |
| Pro Ad-hoc-Aktivierungsauftrag aktivierte Segmente | 80 | Hard | Derzeit kann jeder Ad-hoc-Aktivierungsauftrag bis zu 80 Segmente aktivieren. Der Versuch, mehr als 80 Segmente pro Auftrag zu aktivieren, führt dazu, dass der Auftrag fehlschlägt. Dieses Verhalten kann sich in zukünftigen Versionen ändern. |
| Gleichzeitige Ad-hoc-Aktivierungsaufträge pro Segment | 1 | Hard | Führen Sie nicht mehr als einen gleichzeitigen Ad-hoc-Aktivierungsauftrag pro Segment aus. |

{style=&quot;table-layout:auto&quot;}

### Aktivierung von Edge-Personalisierungszielen {#edge-destinations-activation}

Die folgenden Limits gelten für die Aktivierung durch [Edge-Personalisierungsziele](/help/destinations/destination-types.md#streaming-profile-export).

| Beschränkung | Limit | Art von Limit | Beschreibung |
| --- | --- | --- | --- |
| Maximale Anzahl an [Benutzerdefinierte Personalisierung](/help/destinations/catalog/personalization/custom-personalization.md) Ziele | 10 | Soft | Sie können Datenflüsse zu 10 benutzerdefinierten Personalisierungszielen pro Sandbox einrichten. |
| Maximale Anzahl von Attributen, die einem Personalisierungsziel pro Sandbox zugeordnet sind | 20 | Hard | Pro Sandbox können maximal 20 Attribute in einem Datenfluss einem Personalisierungsziel zugeordnet werden. |
| Maximale Anzahl von Segmenten, die einer einzelnen [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) Ziel | 50 | Soft | Sie können maximal 50 Segmente in einem Aktivierungsfluss zu einem einzelnen Adobe Target-Ziel aktivieren. |

{style=&quot;table-layout:auto&quot;}

### Limits bei Destinationen SDK {#destination-sdk-guardrails}

[Das Destination SDK ist eine Suite von Konfigurations-APIs, mit denen Sie Zielintegrationsmuster für Experience Platform konfigurieren können, um Zielgruppen- und Profildaten basierend auf den von Ihnen ausgewählten Daten- und Authentifizierungsformaten an Ihren Endpunkt zu senden. ](/help/destinations/destination-sdk/overview.md) Die folgenden Limits gelten für die Ziele, die Sie mit Destination SDK konfigurieren.

| Beschränkung | Limit | Art von Limit | Beschreibung |
| --- | --- | --- | --- |
| Maximale Anzahl an [private benutzerdefinierte Ziele](/help/destinations/destination-sdk/overview.md#productized-custom-integrations) | 5 | Weich | Sie können mit Destination SDK maximal 5 private benutzerdefinierte Streaming- oder Batch-Ziele erstellen. Wenden Sie sich an einen Kundenbetreuer, wenn Sie mehr als fünf dieser Ziele erstellen müssen. |
| Profilexportrichtlinie für Destination SDK | <ul><li>`maxBatchAgeInSecs` (mindestens 1.800 und höchstens 3.600)</li><li>`maxNumEventsInBatch` (mindestens 1.000, höchstens 10.000)</li></ul> | Hard | Bei Verwendung von [konfigurierbare Aggregation](/help/destinations/destination-sdk/destination-configuration.md#configurable-aggregation) Beachten Sie die Mindest- und Höchstwerte, die bestimmen, wie oft HTTP-Nachrichten an Ihr API-basiertes Ziel gesendet werden und wie viele Profile die Nachrichten enthalten sollen. |

{style=&quot;table-layout:auto&quot;}

### Richtlinie für Einschränkungen und Wiederholungen bei Zielen {#destination-throttling-and-retry-policy}

Details zu Einschränkungsschwellen oder -beschränkungen für bestimmte Ziele. Dieser Abschnitt enthält auch Informationen zur Wiederholungsrichtlinie für Ziele.

| Zieltyp | Beschreibung |
| --- | --- |
| Enterprise-Ziele (HTTP-API, Amazon Kinesis, Azure EventHubs) | In 95 Prozent der Fälle versucht Experience Platform, eine Durchsatzlatenz von weniger als 10 Minuten für erfolgreich gesendete Nachrichten mit einer Rate von weniger als 10.000 Anfragen pro Sekunde für jeden Datenfluss an ein Unternehmensziel anzubieten. <br> Bei fehlgeschlagenen Anfragen an Ihr Enterprise-Ziel speichert Experience Platform die fehlgeschlagenen Anfragen und versucht es zweimal, die Anfragen an Ihren Endpunkt zu senden. |

{style=&quot;table-layout:auto&quot;}

## Limits für andere Dienstleistungen der Experience Platform {#guardrails-other-services}

Informationen zu Limits für andere Experience Platform-Dienste anzeigen:

* Limits [Datenerfassung](/help/ingestion/guardrails.md)
* Limits [[!DNL Identity Service] data](/help/identity-service/guardrails.md)
* Limits [[!DNL Real-time Customer Profile] data](/help/profile/guardrails.md)
* Limits [[!DNL Query Service] data](/help/query-service/guardrails.md)