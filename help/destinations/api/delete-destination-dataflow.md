---
keywords: Experience Platform; Startseite; beliebte Themen; Flussdienst; API; API; API; löschen; Löschen von Ziel-Datenflüssen
solution: Experience Platform
title: Löschen eines Ziel-Datenflusses mithilfe der Flow Service-API
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Flow Service-API Datenflüsse an Batch- und Streaming-Ziele löschen.
exl-id: fa40cf97-46c6-4a10-b53c-30bed2dd1b2d
source-git-commit: c35a29d4e9791b566d9633b651aecd2c16f88507
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 57%

---

# Löschen eines Ziel-Datenflusses mithilfe der Flow Service-API

Sie können Datenflüsse löschen, die Fehler enthalten oder mit der Funktion [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

In diesem Tutorial werden die Schritte zum Löschen von Datenflüssen an Batch- und Streaming-Ziele mithilfe von [!DNL Flow Service].

## Erste Schritte {#get-started}

Für dieses Tutorial benötigen Sie eine gültige Fluss-ID. Wenn Sie keine gültige Fluss-ID haben, wählen Sie Ihr Ziel aus der [Zielkatalog](../catalog/overview.md) und führen Sie die Schritte aus, die beschrieben wurden, um [Verbindung zum Ziel herstellen](../ui/connect-destination.md) und [Daten aktivieren](../ui/activation-overview.md) vor dem Versuch dieses Tutorials.

Dieses Tutorial setzt außerdem ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Ziele sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. ](../home.md)[!DNL Destinations] Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.
* [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um einen Datenfluss mithilfe der [!DNL Flow Service] API.

### Lesen von Beispiel-API-Aufrufen {#reading-sample-api-calls}

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen {#gather-values-for-required-headers}

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform], einschließlich der Ressourcen, die zu [!DNL Flow Service] gehören, werden in bestimmten virtuellen Sandboxes isoliert. Bei allen Anfragen an [!DNL Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Wenn die Variable `x-sandbox-name` -Kopfzeile nicht angegeben ist, werden Anfragen unter der `prod` Sandbox.

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* `Content-Type: application/json`

## Ziel-Datenfluss löschen {#delete-destination-dataflow}

Mit einer vorhandenen Fluss-ID können Sie einen Ziel-Datenfluss löschen, indem Sie eine DELETE-Anfrage an die [!DNL Flow Service] API.

**API-Format**

```http
DELETE /flows/{FLOW_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{FLOW_ID}` | Die eindeutige `id` -Wert für den Ziel-Datenfluss, den Sie löschen möchten. |

**Anfrage**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/flows/455fa81b-f290-4222-94b6-540a73e3fbc2' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 202 (kein Inhalt) und leeren Text zurück. Sie können den Löschvorgang bestätigen, indem Sie eine Suchanfrage (GET) an den Datenfluss stellen. Die API gibt den HTTP-Fehler 404 (Nicht gefunden) zurück, der angibt, dass der Datenfluss gelöscht wurde.

## Umgang mit API-Fehlern {#api-error-handling}

Die API-Endpunkte in diesem Tutorial folgen den allgemeinen Grundsätzen für die Fehlermeldung bei der Experience Platform-API. Siehe [API-Statuscodes](/help/landing/troubleshooting.md#api-status-codes) und [Fehler in der Anfragekopfzeile](/help/landing/troubleshooting.md#request-header-errors) Weitere Informationen zur Interpretation von Fehlerantworten finden Sie im Handbuch zur Fehlerbehebung bei Platform .

## Nächste Schritte {#next-steps}

In diesem Tutorial haben Sie erfolgreich die [!DNL Flow Service] API zum Löschen eines vorhandenen Datenflusses in ein Ziel.

Wie Sie diese Vorgänge mithilfe der Benutzeroberfläche durchführen können, erfahren Sie im Tutorial [Löschen von Datenflüssen in der Benutzeroberfläche](../ui/delete-destinations.md).

Sie können jetzt fortfahren und [Zielkonten löschen](/help/destinations/api/delete-destination-account.md) mithilfe der [!DNL Flow Service] API.
