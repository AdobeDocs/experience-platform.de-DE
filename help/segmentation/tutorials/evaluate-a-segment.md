---
keywords: Experience Platform;home;popular topics;segment evaluation;Segmentation Service;segmentation;Segmentation;evaluate a segment;access segment results;evaluate and access segment;
solution: Experience Platform
title: Evaluate and Access Segment Results
topic-legacy: tutorial
type: Tutorial
description: Follow this tutorial to learn how to evaluate segments and access segment results using the Adobe Experience Platform Segmentation Service API.
exl-id: 47702819-f5f8-49a8-a35d-034ecac4dd98
source-git-commit: 8325ae6fd7d0013979e80d56eccd05b6ed6f5108
workflow-type: tm+mt
source-wordcount: '1572'
ht-degree: 17%

---

# Segmentergebnisse bewerten und darauf zugreifen

Dieses Dokument bietet einen Lehrgang zum Auswerten von Segmenten und zum Zugriff auf Segmentergebnisse mithilfe der [[!DNL Segmentation API]](../api/getting-started.md).

## Erste Schritte

Dieses Tutorial erfordert ein Verständnis der verschiedenen [!DNL Adobe Experience Platform] Dienste, die mit der Erstellung von Audiencen-Segmenten verbunden sind. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Provides a unified, customer profile in real time based on aggregated data from multiple sources.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Ermöglicht es Ihnen, Audiencen-Segmente zu erstellen von [!DNL Real-time Customer Profile] Daten.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Platform Kundenerlebnisdaten organisiert. Um die Segmentierung optimal zu nutzen, stellen Sie sicher, dass Ihre Daten als Profil und Ereignis gemäß der [Best Practices für die Datenmodellierung](../../xdm/schema/best-practices.md).
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Erforderliche Kopfzeilen

Für dieses Tutorial müssen Sie außerdem die [Authentifizierungslehrgang](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de#platform-apis) , um erfolgreich Aufrufe von [!DNL Platform] APIs. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Anforderungen an [!DNL Platform] APIs erfordern einen Header, der den Namen der Sandbox angibt, in der der Vorgang stattfinden soll in:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Für alle POST-, PUT- und PATCH-Anforderungen ist ein zusätzlicher Header erforderlich:

- Content-Type: application/json

## Bewerten eines Segments

Nachdem Sie Ihre Segmentdefinition entwickelt, getestet und gespeichert haben, können Sie das Segment entweder durch eine geplante Auswertung oder eine On-Demand-Auswertung bewerten.

[Geplante Evaluierung](#scheduled-evaluation) (auch als &quot;geplante Segmentierung&quot; bekannt) ermöglicht es Ihnen, einen wiederholten Zeitplan für die Ausführung eines Exportauftrags zu einem bestimmten Zeitpunkt zu erstellen. [Bedarfsorientierte Bewertung](#on-demand-evaluation) umfasst die Erstellung eines Segmentauftrags, um die Audience sofort zu erstellen. Die einzelnen Schritte sind nachstehend beschrieben.

If you have not yet completed the [create a segment using the Segmentation API](./create-a-segment.md) tutorial or created a segment definition using [Segment Builder](../ui/overview.md), please do so before proceeding with this tutorial.

## Scheduled evaluation {#scheduled-evaluation}

Through scheduled evaluation, your IMS Org can create a recurring schedule to automatically run export jobs.

>[!NOTE]
>
>Die geplante Evaluierung kann für Sandboxen mit maximal fünf (5) Zusammenführungsrichtlinien aktiviert werden für [!DNL XDM Individual Profile]. Wenn Ihr Unternehmen mehr als fünf Zusammenführungsrichtlinien für [!DNL XDM Individual Profile] innerhalb einer einzigen Sandbox-Umgebung können Sie keine geplante Evaluierung verwenden.

### Zeitplan erstellen

Wenn Sie eine POST-Anfrage an den `/config/schedules`-Endpunkt senden, können Sie einen Zeitplan erstellen und die genaue Zeit einschließen, zu der der Zeitplan ausgelöst werden soll.

Ausführlichere Informationen zur Verwendung dieses Endpunkts finden Sie im [Zeitplanendpunkt-Handbuch](../api/schedules.md#create)

### Zeitplan aktivieren

Standardmäßig ist ein Zeitplan bei der Erstellung inaktiv, es sei denn, die `state`-Eigenschaft ist im Text der POST-Anfrage (Erstellen) auf `active` gesetzt. Sie können einen Zeitplan aktivieren (setzen Sie `state` auf `active`), indem Sie eine PATCH-Anfrage an den `/config/schedules`-Endpunkt senden und die Kennung des Zeitplans in den Pfad einschließen.

Ausführlichere Informationen zur Verwendung dieses Endpunkts finden Sie im [Zeitplanendpunkt-Handbuch](../api/schedules.md#update-state)

### Planungszeit aktualisieren

Der Zeitplan kann aktualisiert werden, indem Sie eine PATCH an die folgende Stelle senden: `/config/schedules` Endpunkt und einschließlich der ID des Zeitplans im Pfad.

Ausführlichere Informationen zur Verwendung dieses Endpunkts finden Sie im [Zeitplanendpunkt-Handbuch](../api/schedules.md#update-schedule)

## Bedarfsorientierte Bewertung

Mit der Bedarfsanalyse können Sie einen Segmentauftrag erstellen, um ein Audience-Segment zu generieren, wann immer Sie es benötigen. Unlike scheduled evaluation, this will happen only when requested and is not recurring.

### Segmentauftrag erstellen

Ein Segmentauftrag ist ein asynchroner Vorgang, bei dem ein neues Zielgruppensegment erstellt wird. Es verweist auf eine Segmentdefinition sowie auf alle Zusammenführungsrichtlinien, die bestimmen, wie [!DNL Real-time Customer Profile] Führt überlappende Attribute in Ihren Profil-Fragmenten zusammen. Nach erfolgreichem Abschluss eines Segmentauftrags können Sie verschiedene Informationen über das Segment sammeln, z. B. Fehler, die bei der Verarbeitung aufgetreten sind, oder die endgültige Größe Ihrer Zielgruppe.

Sie können einen neuen Segmentauftrag erstellen, indem Sie eine POST anfordern an die `/segment/jobs` Endpunkt im [!DNL Real-time Customer Profile] API.

Ausführlichere Informationen zur Verwendung dieses Endpunkts finden Sie im [Endpunkt für Segmentaufträge](../api/segment-jobs.md#create)


### Segmentauftragsstatus nachschlagen

Sie können `id` für einen bestimmten Segmentauftrag, um eine Suchanfrage (GET) auszuführen, um den aktuellen Auftragsstatus Ansicht.

Ausführlichere Informationen zur Verwendung dieses Endpunkts finden Sie im [Endpunkt für Segmentaufträge](../api/segment-jobs.md#get)

## Segmentergebnisse interpretieren

Wenn Segmentaufträge erfolgreich ausgeführt werden, `segmentMembership` Karte wird für jedes Profil im Segment aktualisiert. `segmentMembership` speichert auch alle vorausgewerteten Segmente der Audience, die in [!DNL Platform], die Integration in andere Lösungen wie [!DNL Adobe Audience Manager].

Das folgende Beispiel zeigt Folgendes: `segmentMembership` Attribut sieht für jeden einzelnen Profil-Datensatz aus:

```json
{
  "segmentMembership": {
    "UPS": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "timestamp": "2018-04-26T15:52:25+00:00",
        "status": "existing"
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "status": "realized"
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "status": "exited"
      }
    }
  }
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `lastQualificationTime` | Der Zeitstempel, mit dem die Segmentmitgliedschaft bestätigt wurde und das Profil das Segment ein- oder ausstieg. |
| `status` | Der Status der Segmentbeteiligung als Teil der aktuellen Anforderung. muss gleich einem der folgenden bekannten Werte sein: <ul><li>`existing`: Entität befindet sich weiterhin im Segment.</li><li>`realized`: Entität tritt in das Segment ein.</li><li>`exited`: Entität verlässt das Segment.</li></ul> |

## Segmentergebnisse

Auf die Ergebnisse eines Segmentauftrags kann auf zwei Arten zugegriffen werden: Sie können auf einzelne Profil zugreifen oder eine ganze Audience in ein Dataset exportieren.

In den folgenden Abschnitten werden diese Optionen detaillierter beschrieben.

## Profil nachschlagen

If you know the specific profile that you would like to access, you can do so using the [!DNL Real-time Customer Profile] API. Die vollständigen Schritte für den Zugriff auf einzelne Profil finden Sie im [Zugriff auf Echtzeit-Kundendaten mithilfe der Profil-API](../../profile/api/entities.md) Tutorial.

## Segment exportieren {#export}

Nachdem ein Segmentierungsauftrag erfolgreich abgeschlossen wurde (der Wert des `status`-Attributs lautet „SUCCEEDED“ (GELUNGEN)), können Sie Ihre Zielgruppe in einen Datensatz exportieren. In diesem Datensatz ist die Zielgruppe zugänglich und bearbeitbar.

Die folgenden Schritte sind erforderlich, um Ihre Audience zu exportieren:

- [Zielgruppe-Dataset erstellen](#create-a-target-dataset) - Erstellen Sie das Dataset, um Mitglieder der Audience aufzunehmen.
- [Audience-Profil im DataSet erstellen](#generate-profiles-for-audience-members) - Füllen Sie das Dataset mit individuellen XDM-Profilen auf Basis der Ergebnisse eines Segmentauftrags aus.
- [Fortschritt beim Exportieren überwachen](#monitor-export-progress) - Überprüfen Sie den aktuellen Fortschritt des Exportvorgangs.
- [Daten zur Audience lesen](#next-steps) - Rufen Sie die resultierenden XDM-Profil für einzelne Mitglieder Ihrer Audience ab.

### Zielgruppe-Dataset erstellen

Beim Exportieren einer Audience muss zunächst ein Dataset der Zielgruppe erstellt werden. Es ist wichtig, dass der Datensatz korrekt konfiguriert wird, damit der Export erfolgreich ist.

Eine der wichtigsten Erwägungen ist das Schema, auf dem der Datensatz basiert (`schemaRef.id` in der API-Beispielanforderung unten). Um ein Segment zu exportieren, muss der Datensatz auf [!DNL XDM Individual Profile Union Schema] (`https://ns.adobe.com/xdm/context/profile__union`). Ein Vereinigung-Schema ist ein vom System generiertes, schreibgeschütztes Schema, das die Felder von Schemas mit derselben Klasse Aggregat, in diesem Fall die XDM Individual Profil-Klasse. Weitere Informationen zu Schemas der Ansicht der Vereinigung finden Sie im [Echtzeitabschnitt zum Kunden-Profil im Schema Registry-Entwicklerleitfaden](../../xdm/api/getting-started.md).

Es gibt zwei Möglichkeiten, den erforderlichen Datensatz zu erstellen:

- **Verwenden von APIs:** In diesem Tutorial wird beschrieben, wie Sie ein Dataset erstellen, das auf die [!DNL XDM Individual Profile Union Schema] mit [!DNL Catalog] API.
- **Verwenden der Benutzeroberfläche:** So verwenden Sie [!DNL Adobe Experience Platform] Benutzerschnittstelle zum Erstellen eines Datasets, das auf das Schema der Vereinigung verweist, führen Sie die folgenden Schritte aus: [UI-Tutorial](../ui/overview.md) und kehren dann zu diesem Tutorial zurück, um mit den Schritten für [Audience-Profil werden erstellt](#generate-xdm-profiles-for-audience-members).

Wenn Sie bereits über ein kompatibles DataSet verfügen und dessen ID kennen, können Sie direkt zum Schritt wechseln für [Audience-Profil werden erstellt](#generate-xdm-profiles-for-audience-members).

**API-Format**

```http
POST /dataSets
```

**Anfrage**

Mit der folgenden Anforderung wird ein neues DataSet erstellt, das Konfigurationsparameter in der Nutzlast bereitstellt.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Segment Export",
    "schemaRef": {
        "id": "https://ns.adobe.com/xdm/context/profile__union",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    }
}'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `name` | A descriptive name for the dataset. |
| `schemaRef.id` | Die ID der Vereinigung-Ansicht (Schema), der das Dataset zugeordnet werden soll. |

**Antwort**

Eine erfolgreiche Antwort gibt ein Array mit der schreibgeschützten, systemgenerierten eindeutigen ID des neu erstellten Datensatzes zurück. Eine ordnungsgemäß konfigurierte DataSet-ID ist erforderlich, um Audiencen erfolgreich exportieren zu können.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Profil für Audience-Mitglieder generieren {#generate-profiles}

Sobald Sie über ein Vereinigung persistierendes Dataset verfügen, können Sie einen Exportauftrag erstellen, um die Mitglieder der Audience im Dataset zu behalten, indem Sie eine POST an den `/export/jobs` Endpunkt im [!DNL Real-time Customer Profile] API und geben die DataSet-ID und die Segmentinformationen für die Segmente an, die Sie exportieren möchten.

Ausführlichere Informationen zur Verwendung dieses Endpunkts finden Sie im [Endpunkt-Handbuch für Exportaufträge](../api/export-jobs.md#create)

### Fortschritt beim Exportieren überwachen

Bei einem Exportauftrag können Sie den Status überwachen, indem Sie eine GET an die `/export/jobs` Endpunkt und einschließlich `id` des Exportauftrags im Pfad. Der Exportauftrag wurde abgeschlossen, sobald der `status` gibt den Wert &quot;ERFOLGREICH&quot; zurück.

Ausführlichere Informationen zur Verwendung dieses Endpunkts finden Sie im [Endpunkt-Handbuch für Exportaufträge](../api/export-jobs.md#get)

## Nächste Schritte

Once the export has completed successfully, your data is available within the [!DNL Data Lake] in [!DNL Experience Platform]. Sie können dann [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) um auf die Daten zuzugreifen, indem `batchId` mit dem Export verbunden. Depending on the size of the segment, the data may be in chunks and the batch may consist of several files.

For step-by-step instructions on how to use the [!DNL Data Access] API to access and download batch files, follow the [Data Access tutorial](../../data-access/tutorials/dataset-data.md).

You can also access successfully exported segment data using [!DNL Adobe Experience Platform Query Service]. Using the UI or RESTful API, [!DNL Query Service] allows you to write, validate, and run queries on data within the [!DNL Data Lake].

Weitere Informationen zur Abfrage von Daten zur Audience finden Sie in der Dokumentation zu [[!DNL Query Service]](../../query-service/home.md).
