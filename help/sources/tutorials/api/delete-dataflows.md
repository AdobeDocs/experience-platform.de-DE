---
keywords: Experience Platform;home;popular topics;flow service;API;api;delete;delete dataflows
solution: Experience Platform
title: Löschen eines Datenflusses mithilfe der Flow Service API
topic: overview
type: Tutorial
description: In diesem Lernprogramm werden die Schritte zum Löschen von Batch- und Streaming-Datenflüssen mithilfe der Flow Service API beschrieben.
translation-type: tm+mt
source-git-commit: b63b17f2a7271fc673abc8245a4917c0daca4ef3
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 29%

---


# Löschen eines Datenflusses mithilfe der Flow Service API

Sie können Stapel- und Streaming-Datenflüsse löschen, die Fehler enthalten oder mit der [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)veraltet sind.

In diesem Lernprogramm werden die Schritte zum Löschen von Datenblättern beschrieben, die sowohl mit Batch- als auch mit Streaming-Quellen mithilfe von [!DNL Flow Service]vorgenommen werden.

## Erste Schritte

Für dieses Lernprogramm ist eine gültige Fluss-ID erforderlich. Wenn Sie keine gültige Fluss-ID haben, wählen Sie den gewünschten Connector aus der [Quellenübersicht](../../home.md) und führen Sie die Schritte aus, die Sie vor dem Versuch dieses Tutorials beschrieben haben.

Für dieses Lernprogramm müssen Sie außerdem die folgenden Komponenten von Adobe Experience Platform kennen:

* [Quellen](../../home.md): [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu verbessern.
* [Sandboxen](../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

The following sections provide additional information that you will need to know in order to successfully delete a dataflow using the [!DNL Flow Service] API.

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](../../../tutorials/authentication.md) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

All resources in [!DNL Experience Platform], including those belonging to [!DNL Flow Service], are isolated to specific virtual sandboxes. All requests to [!DNL Platform] APIs require a header that specifies the name of the sandbox the operation will take place in:

* `x-sandbox-name: {SANDBOX_NAME}`

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* `Content-Type: application/json`

## Löschen eines Datenflusses

Mit einer vorhandenen Fluss-ID können Sie einen Datenflug löschen, indem Sie eine DELETE-Anforderung an die [!DNL Flow Service] API ausführen.

**API-Format**

```http
DELETE /flows/{FLOW_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{FLOW_ID}` | Der eindeutige `id` Wert des zu löschenden Datenflusses. |

**Anfrage**

```shell
curl -X DELETE \
    'https://platform-int.adobe.io/data/foundation/flowservice/flows/20c115bc-46e3-40f3-bfe9-fb25abe4ba76' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) und leeren Text zurück. Sie können den Löschvorgang bestätigen, indem Sie eine Nachschlageanfrage (GET) an den Dataflow senden. Die API gibt einen HTTP-Fehler 404 (Nicht gefunden) zurück, der angibt, dass der Datendurchlauf gelöscht wurde.

## Nächste Schritte

In diesem Lernprogramm haben Sie die [!DNL Flow Service] API erfolgreich zum Löschen eines vorhandenen Datenflusses verwendet.

Anweisungen zum Ausführen dieser Vorgänge mithilfe der Benutzeroberfläche finden Sie im Lernprogramm zum [Löschen von Datenflüssen in der Benutzeroberfläche](../../tutorials/ui/delete.md)
