---
keywords: Experience Platform;Startseite;beliebte Themen;Flow Service;API;api;Löschen;Löschen von Datenflüssen
solution: Experience Platform
title: Löschen eines Datenflusses mithilfe der Flow Service-API
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Flow Service-API Batch- und Streaming-Datenflüsse löschen können.
exl-id: ea9040b1-3a40-493d-86f0-27deef09df07
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 100%

---

# Löschen eines Datenflusses mithilfe der Flow Service-API

Sie können Batch- und Streaming-Datenflüsse, die Fehler enthalten oder veraltet sind, mithilfe der [[!DNL Flow Service] -API](https://www.adobe.io/experience-platform-apis/references/flow-service/) löschen.

In diesem Tutorial werden die Schritte zum Löschen von Datenflüssen aus Batch- und Streaming-Quellen mithilfe von [!DNL Flow Service] beschrieben.

## Erste Schritte

Für dieses Tutorial benötigen Sie eine gültige Fluss-ID. Wenn Sie keine gültige Fluss-ID haben, wählen Sie Ihren gewünschten Connector aus der [Quellen – Übersicht](../../home.md) und befolgen Sie die beschriebenen Schritte, bevor Sie dieses Tutorial beginnen.

Dieses Tutorial setzt außerdem ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Verwenden von Platform-APIs

Informationen darüber, wie Sie Platform-APIs erfolgreich aufrufen können, finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../landing/api-guide.md).

## Löschen eines Datenflusses

Mit einer vorhandenen Flow-ID können Sie einen Datenfluss löschen, indem Sie eine DELETE-Anfrage an die [!DNL Flow Service]-API stellen.

**API-Format**

```http
DELETE /flows/{FLOW_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{FLOW_ID}` | Der eindeutige `id`-Wert für den Datenfluss, den Sie löschen möchten. |

**Anfrage**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/flows/20c115bc-46e3-40f3-bfe9-fb25abe4ba76' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) und leeren Text zurück. Sie können den Löschvorgang bestätigen, indem Sie eine Suchanfrage (GET) an den Datenfluss stellen. Die API gibt den HTTP-Fehler 404 (Nicht gefunden) zurück, der angibt, dass der Datenfluss gelöscht wurde.

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie erfolgreich einen vorhandenen Datenfluss mithilfe der [!DNL Flow Service]-API gelöscht.

Wie Sie diese Vorgänge mithilfe der Benutzeroberfläche durchführen können, erfahren Sie im Tutorial [Löschen von Datenflüssen in der Benutzeroberfläche](../../tutorials/ui/delete.md)
