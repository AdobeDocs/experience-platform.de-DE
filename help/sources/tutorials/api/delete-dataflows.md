---
keywords: Experience Platform; Startseite; beliebte Themen; Flussdienst; API; API; API; Löschen; Löschen von Datenflüssen
solution: Experience Platform
title: Löschen eines Datenflusses mithilfe der Flow Service-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Flow Service-API Batch- und Streaming-Datenflüsse löschen.
exl-id: ea9040b1-3a40-493d-86f0-27deef09df07
source-git-commit: a51c878bbfd3004cb597ce9244a9ed2f2318604b
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 42%

---

# Löschen eines Datenflusses mithilfe der Flow Service-API

Sie können Batch- und Streaming-Datenflüsse löschen, die Fehler enthalten oder mit dem [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

In diesem Tutorial werden die Schritte zum Löschen von Datenflüssen beschrieben, die sowohl mit Batch- als auch Streaming-Quellen mithilfe von [!DNL Flow Service].

## Erste Schritte

Für dieses Tutorial benötigen Sie eine gültige Fluss-ID. Wenn Sie keine gültige Fluss-ID haben, wählen Sie Ihren gewünschten Connector aus der [Quellen - Übersicht](../../home.md) und führen Sie die Schritte aus, die vor dem Versuch dieses Tutorials beschrieben wurden.

Für dieses Tutorial benötigen Sie außerdem ein Verständnis der folgenden Komponenten von Adobe Experience Platform:

* [Quellen](../../home.md): [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten zu strukturieren, zu beschriften und zu erweitern, indem Sie [!DNL Platform] Dienste.
* [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um einen Datenfluss mithilfe der [!DNL Flow Service] API.

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform], einschließlich der Ressourcen, die zu [!DNL Flow Service] gehören, werden in bestimmten virtuellen Sandboxes isoliert. Bei allen Anfragen an [!DNL Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* `x-sandbox-name: {SANDBOX_NAME}`

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* `Content-Type: application/json`

## Datenfluss löschen

Mit einer vorhandenen Fluss-ID können Sie einen Datenfluss löschen, indem Sie eine DELETE-Anfrage an die [!DNL Flow Service] API.

**API-Format**

```http
DELETE /flows/{FLOW_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{FLOW_ID}` | Die eindeutige `id` für den Datenfluss, den Sie löschen möchten. |

**Anfrage**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/flows/20c115bc-46e3-40f3-bfe9-fb25abe4ba76' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) und leeren Text zurück. Sie können den Löschvorgang bestätigen, indem Sie eine Nachschlageanfrage (GET) für den Datenfluss ausführen. Die API gibt einen HTTP 404-Fehler (Nicht gefunden) zurück, der angibt, dass der Datenfluss gelöscht wurde.

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich die [!DNL Flow Service] API zum Löschen eines vorhandenen Datenflusses.

Anweisungen zum Ausführen dieser Vorgänge mithilfe der Benutzeroberfläche finden Sie im Tutorial zu [Löschen von Datenflüssen in der Benutzeroberfläche](../../tutorials/ui/delete.md)
