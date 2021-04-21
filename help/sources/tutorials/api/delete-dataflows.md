---
keywords: Experience Platform;Home;beliebte Themen;Flussdienst;API;API;Löschen;Datenflüsse löschen
solution: Experience Platform
title: Löschen eines Datenflusses mit der Flussdienst-API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie Batch- und Streaming-Datenflüsse mithilfe der Flow Service API löschen.
exl-id: ea9040b1-3a40-493d-86f0-27deef09df07
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 28%

---

# Löschen eines Datenflusses mithilfe der Flow Service API

Sie können Stapel- und Streaming-Datenflüsse löschen, die Fehler enthalten oder mit der [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) veraltet sind.

Dieses Lernprogramm beschreibt die Schritte zum Löschen von Datenflüssen, die sowohl mit Batch- als auch mit Streaming-Quellen mit [!DNL Flow Service] durchgeführt werden.

## Erste Schritte

Für dieses Lernprogramm ist eine gültige Fluss-ID erforderlich. Wenn Sie keine gültige Fluss-ID haben, wählen Sie Ihren gewünschten Connector aus dem [Sources-Überblick](../../home.md) und befolgen Sie die Schritte, die vor dem Versuch dieses Lernprogramms beschrieben werden.

Für dieses Lernprogramm müssen Sie außerdem die folgenden Komponenten von Adobe Experience Platform kennen:

* [Quellen](../../home.md):  [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von  [!DNL Platform] Diensten zu strukturieren, zu beschriften und zu verbessern.
* [Sandboxen](../../../sandboxes/home.md):  [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne  [!DNL Platform] Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um einen Datendurchlauf mithilfe der API [!DNL Flow Service] erfolgreich zu löschen.

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Fehlerbehebungshandbuch für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://www.adobe.com/go/platform-api-authentication-en) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform], einschließlich derjenigen, die zu [!DNL Flow Service] gehören, werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an [!DNL Platform]-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird in:

* `x-sandbox-name: {SANDBOX_NAME}`

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* `Content-Type: application/json`

## Löschen eines Datenflusses

Mit einer vorhandenen Fluss-ID können Sie einen Datenflug löschen, indem Sie eine DELETE-Anforderung an die API [!DNL Flow Service] durchführen.

**API-Format**

```http
DELETE /flows/{FLOW_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{FLOW_ID}` | Der eindeutige Wert `id` für den Datendurchlauf, den Sie löschen möchten. |

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

In diesem Lernprogramm haben Sie erfolgreich die API [!DNL Flow Service] zum Löschen eines vorhandenen Datenflusses verwendet.

Anweisungen zum Ausführen dieser Vorgänge mithilfe der Benutzeroberfläche finden Sie im Lernprogramm zum Löschen von Datenflüssen in der Benutzeroberfläche[](../../tutorials/ui/delete.md)
