---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Bewerten eines Segments
topic: tutorial
translation-type: tm+mt
source-git-commit: c0eacfba2feea66803e63ed55ad9d0a97e9ae47c
workflow-type: tm+mt
source-wordcount: '1543'
ht-degree: 17%

---


# Segmentergebnisse auswerten und darauf zugreifen

In diesem Dokument finden Sie eine Anleitung zur Bewertung von Segmenten und zum Zugriff auf Segmentergebnisse mit der [!DNL Segmentation API](../api/getting-started.md).

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der verschiedenen [!DNL Adobe Experience Platform] Dienste, die beim Erstellen von Segmenten für die Audience erforderlich sind. Bevor Sie mit dem Tutorial beginnen, lesen Sie bitte die Dokumentation für folgende Dienste:

- [!DNL Real-time Customer Profile](../../profile/home.md): Bietet ein einheitliches, kundenspezifisches Profil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.
- [!DNL Adobe Experience Platform Segmentation Service](../home.md): Ermöglicht Ihnen das Erstellen von Segmenten für Audiencen aus [!DNL Real-time Customer Profile] Daten.
- [!DNL Experience Data Model (XDM)](../../xdm/home.md): Das standardisierte Framework, mit dem Plattform Kundenerlebnisdaten organisiert.
- [Sandboxen](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

### Erforderliche Kopfzeilen

This tutorial also requires you to have completed the [authentication tutorial](../../tutorials/authentication.md) in order to successfully make calls to [!DNL Platform] APIs. Completing the authentication tutorial provides the values for each of the required headers in all [!DNL Experience Platform] API calls, as shown below:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

All resources in [!DNL Experience Platform] are isolated to specific virtual sandboxes. Requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in [!DNL Platform], see the [sandbox overview documentation](../../sandboxes/home.md).

Für alle POST-, PUT- und PATCH-Anforderungen ist ein zusätzlicher Header erforderlich:

- Content-Type: application/json

## Bewerten eines Segments

Nachdem Sie Ihre Segmentdefinition entwickelt, getestet und gespeichert haben, können Sie das Segment entweder durch eine geplante Auswertung oder eine On-Demand-Auswertung bewerten.

[Die geplante Auswertung](#scheduled-evaluation) (auch als &quot;geplante Segmentierung&quot;bezeichnet) ermöglicht es Ihnen, einen wiederkehrenden Zeitplan für die Ausführung eines Exportauftrags zu einem bestimmten Zeitpunkt zu erstellen, während bei der [On-Demand-Auswertung](#on-demand-evaluation) ein Segmentauftrag erstellt werden muss, um die Audience sofort zu erstellen. Die Schritte für die einzelnen Schritte sind nachfolgend beschrieben.

Wenn Sie das [Erstellen eines Segments noch nicht mithilfe des Segmentierungs-API](./create-a-segment.md) -Tutorials abgeschlossen haben oder eine Segmentdefinition mit dem [Segmentaufbau](../ui/overview.md)erstellt haben, führen Sie dies bitte vor dem Fortfahren dieses Tutorials durch.

## Geplante Bewertung {#scheduled-evaluation}

Durch die geplante Auswertung kann Ihr IMS-Org einen wiederkehrenden Zeitplan erstellen, um Exportaufträge automatisch auszuführen.

>[!NOTE]
>
>Geplante Auswertung kann für Sandboxes mit maximal fünf (5) Zusammenführungsrichtlinien für XDM Individual Profile aktiviert werden. Wenn Ihre Organisation innerhalb einer Sandbox-Umgebung über mehr als fünf Zusammenführungsrichtlinien für XDM Individual Profile verfügt, können Sie keine geplante Auswertung verwenden.

### Zeitplan erstellen

Wenn Sie eine POST-Anfrage an den `/config/schedules`-Endpunkt senden, können Sie einen Zeitplan erstellen und die genaue Zeit einschließen, zu der der Zeitplan ausgelöst werden soll.

Detailliertere Informationen zur Verwendung dieses Endpunkts finden Sie im Leitfaden zum Endpunkt &quot; [Zeitpläne&quot;.](../api/schedules.md#create)

### Zeitplan aktivieren

Standardmäßig ist ein Zeitplan bei der Erstellung inaktiv, es sei denn, die `state`-Eigenschaft ist im Text der POST-Anfrage (Erstellen) auf `active` gesetzt. Sie können einen Zeitplan aktivieren (setzen Sie `state` auf `active`), indem Sie eine PATCH-Anfrage an den `/config/schedules`-Endpunkt senden und die Kennung des Zeitplans in den Pfad einschließen.

Detailliertere Informationen zur Verwendung dieses Endpunkts finden Sie im Leitfaden zum Endpunkt &quot; [Zeitpläne&quot;.](../api/schedules.md#update-state)

### Zeitplanaktualisierung

Die Zeitplanung kann aktualisiert werden, indem eine PATCH-Anforderung an den `/config/schedules` Endpunkt gesendet wird und die ID des Zeitplans im Pfad enthalten ist.

Detailliertere Informationen zur Verwendung dieses Endpunkts finden Sie im Leitfaden zum Endpunkt &quot; [Zeitpläne&quot;.](../api/schedules.md#update-schedule)

## On-Demand-Bewertung

Mit der On-Demand-Auswertung können Sie einen Segmentauftrag erstellen, um bei Bedarf ein Audiencen-Segment zu generieren. Im Gegensatz zur geplanten Auswertung erfolgt dies nur auf Anfrage und nicht wiederholt.

### Erstellen eines Segmentauftrags

Ein Segmentauftrag ist ein asynchroner Vorgang, bei dem ein neues Zielgruppensegment erstellt wird. It references a segment definition, as well as any merge policies controlling how [!DNL Real-time Customer Profile] merges overlapping attributes across your profile fragments. Nach erfolgreichem Abschluss eines Segmentauftrags können Sie verschiedene Informationen über das Segment sammeln, z. B. Fehler, die bei der Verarbeitung aufgetreten sind, oder die endgültige Größe Ihrer Zielgruppe.

You can create a new segment job by making a POST request to the `/segment/jobs` endpoint in the [!DNL Real-time Customer Profile] API.

Detailliertere Informationen zur Verwendung dieses Endpunkts finden Sie im Handbuch [Segmentauftragsendpunkt](../api/segment-jobs.md#create)


### Status des Segmentauftrags suchen

Sie können den `id` für einen bestimmten Segmentauftrag verwenden, um eine Nachschlageanforderung (GET) durchzuführen, um den aktuellen Auftragsstatus Ansicht.

Detailliertere Informationen zur Verwendung dieses Endpunkts finden Sie im Handbuch [Segmentauftragsendpunkt](../api/segment-jobs.md#get)

## Segmentergebnisse interpretieren

Wenn Segmentaufträge erfolgreich ausgeführt werden, wird die `segmentMembership` Zuordnung für jedes Profil im Segment aktualisiert. `segmentMembership` speichert auch alle vorab ausgewerteten Audiencen, die in eingegliedert werden, [!DNL Platform]sodass eine Integration mit anderen Lösungen wie [!DNL Adobe Audience Manager].

Das folgende Beispiel zeigt, wie das `segmentMembership` Attribut für jeden einzelnen Profil-Datensatz aussieht:

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
| `lastQualificationTime` | Der Zeitstempel, zu dem die Zusicherung der Segmentmitgliedschaft erfolgte und das Profil das Segment ein- oder ausstieg. |
| `status` | Der Status der Segmentbeteiligung als Teil der aktuellen Anforderung. muss einem der folgenden bekannten Werte entsprechen: <ul><li>`existing`: Die Entität befindet sich weiterhin im Segment.</li><li>`realized`: Entität tritt in das Segment ein.</li><li>`exited`: Entität beendet das Segment.</li></ul> |

## Zugriff auf Segmentergebnisse

Auf die Ergebnisse eines Segmentauftrags kann auf zwei Arten zugegriffen werden: Sie können auf einzelne Profil zugreifen oder eine ganze Audience in einen Datensatz exportieren.

Die folgenden Abschnitte beschreiben diese Optionen detaillierter.

## Profil nachschlagen

Wenn Sie das spezifische Profil kennen, auf das Sie zugreifen möchten, können Sie dies mithilfe der [!DNL Real-time Customer Profile] API tun. Die vollständigen Schritte für den Zugriff auf einzelne Profil finden Sie in der Anleitung zum [Zugriff auf Echtzeit-Kundendaten mithilfe der Profil-API](../../profile/api/entities.md) .

## Segment exportieren {#export}

Nachdem ein Segmentierungsauftrag erfolgreich abgeschlossen wurde (der Wert des `status`-Attributs lautet „SUCCEEDED“ (GELUNGEN)), können Sie Ihre Zielgruppe in einen Datensatz exportieren. In diesem Datensatz ist die Zielgruppe zugänglich und bearbeitbar.

Die folgenden Schritte sind erforderlich, um Ihre Audience zu exportieren:

- [Erstellen Sie einen Dataset](#create-a-target-dataset) der Zielgruppe - Erstellen Sie den Datensatz, der Audiencen enthält.
- [Generieren von Profilen zur Audience im Datensatz](#generate-profiles-for-audience-members) - Füllen Sie den Datensatz mit XDM-Profilen auf Basis der Ergebnisse eines Segmentauftrags.
- [Überwachung des Exportfortschritts](#monitor-export-progress) - Überprüfen Sie den aktuellen Fortschritt des Exportprozesses.
- [Lesen Sie die Daten](#next-steps) zur Audience - Rufen Sie die resultierenden XDM-Profil für die Mitglieder Ihrer Audience ab.

### Zielgruppen-Dataset erstellen

Beim Exportieren einer Audience muss zunächst ein Zielgruppe-Datensatz erstellt werden. Es ist wichtig, dass der Datensatz korrekt konfiguriert wird, um sicherzustellen, dass der Export erfolgreich ist.

Eine der wichtigsten Überlegungen ist das Schema, auf dem der Datensatz basiert (`schemaRef.id` in der unten stehenden API-Musteranforderung). Um ein Segment zu exportieren, muss der Datensatz auf dem XDM Individual Profil Vereinigung Schema (`https://ns.adobe.com/xdm/context/profile__union`) basieren. Ein Vereinigung-Schema ist ein systemgeneriertes, schreibgeschütztes Schema, das die Felder von Schemas, die dieselbe Klasse besitzen, Aggregat gibt, in diesem Fall die XDM-Klasse Individuelles Profil. Weitere Informationen zu Schemas der Vereinigung Ansicht finden Sie im Abschnitt zum [Echtzeit-Kundenmanagement im Schema Registry-Entwicklerhandbuch](../../xdm/api/getting-started.md).

Es gibt zwei Möglichkeiten, den erforderlichen Datensatz zu erstellen:

- **Verwenden von APIs:** In den folgenden Schritten wird beschrieben, wie Sie ein Dataset erstellen, das auf das Schema zur Vereinigung einzelner XDM-Profil mithilfe der Katalog-API verweist.
- **Verwenden der Benutzeroberfläche:** Um mithilfe der [!DNL Adobe Experience Platform] Benutzeroberfläche einen Datensatz zu erstellen, der auf das Schema &quot;Vereinigung&quot;verweist, führen Sie die Schritte im [UI-Lernprogramm](../ui/overview.md) aus und kehren Sie dann zu diesem Lernprogramm zurück, um mit den Schritten zum [Generieren von Profilen](#generate-xdm-profiles-for-audience-members)der Audience fortzufahren.

Wenn Sie bereits über einen kompatiblen Datensatz verfügen und dessen ID kennen, können Sie direkt mit dem Schritt zum [Generieren von Profilen](#generate-xdm-profiles-for-audience-members)zur Audience fortfahren.

**API-Format**

```http
POST /dataSets
```

**Anfrage**

Mit der folgenden Anforderung wird ein neuer Datensatz erstellt, der Konfigurationsparameter in der Nutzlast bereitstellt.

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
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    }
}'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `name` | Ein beschreibender Name für den Datensatz. |
| `schemaRef.id` | Die ID der Vereinigung-Ansicht (Schema), der der Datensatz zugeordnet werden soll. |
| `fileDescription.persisted` | Ein boolescher Wert, der bei Festlegung auf `true`die Persistenz des Datensatzes in der Ansicht &quot;Vereinigung&quot;ermöglicht. |

**Antwort**

Eine erfolgreiche Antwort gibt ein Array zurück, das die schreibgeschützte, systemgenerierte eindeutige ID des neu erstellten Datensatzes enthält. Für den erfolgreichen Export von Audiencen-Mitgliedern ist eine ordnungsgemäß konfigurierte Dataset-ID erforderlich.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Generieren von Profilen für Audiencen-Mitglieder {#generate-profiles}

Sobald Sie über einen Datensatz mit Vereinigung-Speicherung verfügen, können Sie einen Exportauftrag erstellen, um die Audiencen im Datensatz zu erhalten, indem Sie eine POST-Anforderung an den `/export/jobs` Endpunkt in der [!DNL Real-time Customer Profile] -API senden und die Dataset-ID sowie die Segmentinformationen für die zu exportierenden Segmente angeben.

Detailliertere Informationen zur Verwendung dieses Endpunkts finden Sie im Handbuch [für Exportaufträge](../api/export-jobs.md#create)

### Überwachung des Exportfortschritts

Als Exportauftragsprozess können Sie den Status überwachen, indem Sie eine GET-Anforderung an den `/export/jobs` Endpunkt senden und den Pfad `id` des Exportauftrags einschließen. Der Exportauftrag ist abgeschlossen, sobald das `status` Feld den Wert &quot;SUCCEEDED&quot;zurückgibt.

Detailliertere Informationen zur Verwendung dieses Endpunkts finden Sie im Handbuch [für Exportaufträge](../api/export-jobs.md#get)

## Nächste Schritte

Nach erfolgreichem Abschluss des Exports sind Ihre Daten im Data Lake in [!DNL Experience Platform]verfügbar. Sie können dann mit der [Datenzugriff-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) auf die Daten zugreifen, indem Sie die mit dem Export verknüpfte `batchId` Datei verwenden. Je nach Größe des Segments können die Daten in Blöcken vorliegen und der Stapel kann aus mehreren Dateien bestehen.

Eine schrittweise Anleitung zum Zugriff auf und Herunterladen von Stapeldateien mit der [!DNL Data Access] API finden Sie im [Lernprogramm](../../data-access/tutorials/dataset-data.md)&quot;Datenzugriff&quot;.

Sie können auch auf erfolgreich exportierte Segmentdaten zugreifen [!DNL Adobe Experience Platform Query Service]. Mithilfe der Benutzeroberfläche oder RESTful-API können [!DNL Query Service] Sie Abfragen für Daten im Data Lake schreiben, überprüfen und ausführen.

Weitere Informationen zur Abfrage von Daten zur Audience finden Sie in der Dokumentation zu [!DNL Query Service](../../query-service/home.md).
