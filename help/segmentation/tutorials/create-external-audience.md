---
title: Erstellen und Aktivieren einer externen Zielgruppe
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Experience Platform-APIs eine externe Zielgruppe in Adobe Experience Platform erstellen.
source-git-commit: 0a37ef2f5fc08eb515c7c5056936fd904ea6d360
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 6%

---


# Erstellen und Aktivieren einer externen Zielgruppe mithilfe der API

In diesem Tutorial werden die Schritte erläutert, die zum Erstellen einer externen Zielgruppe mithilfe der Adobe Experience Platform-APIs erforderlich sind.

## Erste Schritte

Dieses Tutorial setzt Grundkenntnisse der verschiedenen Experience Platform-Services voraus, die bei der Erstellung einer externen Zielgruppe zum Einsatz kommen. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Services:

- [Quellen](../../sources/home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Ermöglicht das Erstellen von Zielgruppen aus den externen Daten.
- [Ziele](../../destinations/home.md): Ziele sind vorgefertigte Integrationen mit häufig verwendeten Programmen, die die nahtlose Aktivierung von Daten aus Experience Platform für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und mehr ermöglichen.

### Erforderliche Kopfzeilen

Für dieses Tutorial müssen Sie auch das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abgeschlossen haben, um [!DNL Experience Platform] APIs erfolgreich aufrufen zu können. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Anfragen an [!DNL Experience Platform]-APIs erfordern eine Kopfzeile, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in [!DNL Experience Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Für alle POST-, PUT- und PATCH-Anfragen ist eine zusätzliche -Kopfzeile erforderlich:

- Content-Type: application/json

## Externe Zielgruppe vorbereiten {#prepare}

Bevor Sie eine externe Zielgruppe in Experience Platform erstellen können, müssen Sie eine Datei vorbereiten, die die Zielgruppendaten enthält.

Für dieses Beispiel sollten Sie eine CSV-Datei verwenden. Stellen Sie sicher, dass Ihre CSV **Datei** eine Spalte mit einem Identitätswert wie einer ECID, einer E-Mail-ID oder einer CRM-ID enthält. Stellen Sie außerdem sicher, dass alle Anreicherungsattribute enthält, die Sie für die Segmentierung und Aktivierung benötigen.

Außerdem müssen Sie sicherstellen, dass die Datei den Anforderungen Ihres Experience Platform-Schemas entspricht. Weitere Informationen zum Erstellen eines Schemas finden Sie entweder im [Tutorial zum Erstellen eines Schemas mithilfe der ](/help/xdm/tutorials/create-schema-api.md) oder im [Tutorial zum Erstellen eines Schemas mithilfe der Benutzeroberfläche](/help/xdm/tutorials/create-schema-ui.md).

Nachdem Sie bestätigt haben, dass Ihre CSV-Datei alle benötigten Informationen enthält und dem Schema entspricht, müssen Sie die CSV-Datei in Ihren Cloud-Speicheranbieter hochladen, damit Sie Quellen verwenden können, um die Daten in Experience Platform aufzunehmen. Weitere Informationen zur Verwendung einer Cloud-Speicherquelle finden Sie entweder im [Tutorial zum Erkunden von Cloud-Speicheroptionen mithilfe der API](/help/sources/tutorials/api/explore/cloud-storage.md) oder in der [Quellen - Übersicht](/help/sources/home.md#cloud-storage).

## Erstellen einer externen Zielgruppe {#create}

Nachdem Sie Ihre CSV-Datei vorbereitet haben, können Sie jetzt mit dem Erstellen der externen Zielgruppe beginnen.

Sie können eine externe Zielgruppe erstellen, indem Sie eine POST-Anfrage an den `/external-audience/`-Endpunkt senden.

Bei dieser Anfrage müssen Sie die folgenden Informationen angeben:

- Der Name der Zielgruppe
- Eine Beschreibung für die Zielgruppe
- Die entsprechenden Felder zwischen der CSV-Datei und dem Schema
- Informationen zur Quellspezifikation
   - Dazu gehört der Dateipfad der CSV-Datei für die Aufnahme
      - Der Dateipfad **darf** Leerzeichen enthalten. Wenn Ihr Pfad beispielsweise `activation/sample-source/Example CSV File.csv` ist, legen Sie den Pfad auf `activation/sample-source/ExampleCSVFile.csv` fest.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im [Handbuch zu Endpunkten für externe Zielgruppen](/help/segmentation/api/external-audiences.md#create-audience).

+++Anfrage

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/ \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "params": {
                "path": "activation/sample-source/example.csv",
                "type": "file",
                "sourceType": "Cloud Storage",
                "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
            }
        },
        "ttlInDays": "40",
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    }'
```

+++

Nachdem Sie diese Anfrage gestellt haben, notieren Sie sich die `operationId`, die Sie von der Antwort erhalten, damit Sie die Zielgruppen-ID abrufen können.

## Abrufen der Zielgruppen-ID {#retrieve-audience-id}

Nachdem Sie die externe Zielgruppe erstellt haben, müssen Sie die Zielgruppen-ID abrufen, damit Sie die Zielgruppe in Experience Platform aufnehmen können.

Sie können die Zielgruppen-ID abrufen, indem Sie eine GET-Anfrage an den `/external-audiences/operations`-Endpunkt stellen und die ID des Vorgangs angeben, den Sie zuvor aus der Antwort zum Erstellen einer externen Zielgruppe erhalten haben.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im [Handbuch für Endpunkte externer Zielgruppen](/help/segmentation/api/external-audiences.md#retrieve-status).

+++ Anfrage

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/operations/{OPERATION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

Nachdem Sie diese Anfrage gestellt haben, notieren Sie sich die `audienceId`, die Sie von der Antwort erhalten, damit Sie den Aufnahmeauftrag für die Zielgruppe als Trigger verwenden können.

## Zielgruppenerfassung starten {#start-ingestion}

Da Sie Ihre `audienceId` haben, können Sie jetzt die Aufnahme Ihrer externen Zielgruppe in Experience Platform als Trigger festlegen.

Sie können eine Zielgruppenaufnahme starten, indem Sie eine POST-Anfrage an den folgenden Endpunkt senden und dabei die Zielgruppen-ID angeben. Darüber hinaus müssen Sie die Startzeit angeben, um zu bestimmen, welche Dateien verarbeitet werden.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im [Handbuch zu Endpunkten für externe Zielgruppen](/help/segmentation/api/external-audiences.md#start-audience-ingestion)

+++ Anfrage

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/{AUDIENCE_ID}/runs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "dataFilterStartTime": 764245635
 }' 
```

+++

Nachdem Sie diese Anfrage gestellt haben, notieren Sie sich die `runId`, die Sie von der Antwort erhalten, damit Sie den Aufnahmestatus überwachen können.

## Überwachen des Aufnahmestatus {#monitor-ingestion}

Nachdem Sie die Aufnahme der Zielgruppe ausgelöst haben, können Sie jetzt den Fortschritt der Aufnahme überwachen, um den Erfolg der Aufnahme zu bestätigen und die Verfügbarkeit der Zielgruppe für die nachgelagerte Aktivierung zu überprüfen.

Sie können den Status einer Zielgruppenaufnahme abrufen, indem Sie eine GET-Anfrage an den folgenden Endpunkt senden und dabei sowohl die Zielgruppen- als auch die Ausführungs-IDs angeben.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im [Handbuch für Endpunkte externer Zielgruppen](/help/segmentation/api/external-audiences.md#retrieve-ingestion-status).

+++ Anfrage

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/{AUDIENCE_ID}/runs/{RUN_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

## Nächste Schritte {#next-steps}

>[!IMPORTANT]
>
>Um die extern generierte Zielgruppe zu verwenden, **müssen** warten, bis der tägliche Segmentierungsauftrag abgeschlossen ist.

Nachdem Sie bestätigt haben, dass die externe Zielgruppe erfolgreich aufgenommen wurde, können Sie sie in Audience Portal sehen und in nachgelagerten Services wie Zielen verwenden.

Weitere Informationen zu Audience Portal finden Sie im [Handbuch zur Audience Portal-Benutzeroberfläche](/help/segmentation/ui/audience-portal.md). Weitere Informationen zu Zielen finden Sie unter [Ziele - Übersicht](/help/destinations/home.md).

