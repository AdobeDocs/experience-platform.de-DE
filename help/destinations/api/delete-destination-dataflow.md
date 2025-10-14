---
keywords: Experience Platform;Startseite;beliebte Themen;Flow Service;API;api;Löschen;Löschen von Ziel-Datenflüssen
solution: Experience Platform
title: Löschen eines Ziel-Datenflusses mithilfe der Flow Service-API
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Flow Service-API Datenflüsse zu Batch- und Streaming-Zielen löschen.
exl-id: fa40cf97-46c6-4a10-b53c-30bed2dd1b2d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 49%

---

# Löschen eines Ziel-Datenflusses mithilfe der Flow Service-API

Datenflüsse, die Fehler enthalten oder veraltet sind, können Sie mit der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) löschen.

In diesem Tutorial werden die Schritte zum Löschen von Datenflüssen zu Batch- und Streaming-Zielen mithilfe von [!DNL Flow Service] beschrieben.

## Erste Schritte {#get-started}

Für dieses Tutorial benötigen Sie eine gültige Fluss-ID. Wenn Sie keine gültige Fluss-ID haben, wählen Sie Ihr Ziel aus dem [Zielkatalog](../catalog/overview.md) und befolgen Sie die beschriebenen Schritte zum [Herstellen einer Verbindung mit dem Ziel](../ui/connect-destination.md) und [Aktivieren von Daten](../ui/activation-overview.md), bevor Sie dieses Tutorial ausführen.

Dieses Tutorial setzt außerdem ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Ziele](../home.md): [!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.
* [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Experience Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um einen Datenfluss mithilfe der [!DNL Flow Service]-API erfolgreich löschen zu können.

### Lesen von Beispiel-API-Aufrufen {#reading-sample-api-calls}

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen {#gather-values-for-required-headers}

Um [!DNL Experience Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform], einschließlich der Ressourcen, die zu [!DNL Flow Service] gehören, werden in bestimmten virtuellen Sandboxes isoliert. Bei allen Anfragen an [!DNL Experience Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Wenn die `x-sandbox-name`-Kopfzeile nicht angegeben ist, werden Anfragen unter der `prod`-Sandbox aufgelöst.

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* `Content-Type: application/json`

## Löschen eines Ziel-Datenflusses {#delete-destination-dataflow}

Mit einer vorhandenen Fluss-ID können Sie einen Ziel-Datenfluss löschen, indem Sie eine DELETE-Anfrage an die [!DNL Flow Service]-API stellen.

**API-Format**

```http
DELETE /flows/{FLOW_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{FLOW_ID}` | Der eindeutige `id` für den Ziel-Datenfluss, den Sie löschen möchten. |

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

Eine erfolgreiche Antwort gibt den HTTP-Status 202 (Kein Inhalt) und leeren Text zurück. Sie können den Löschvorgang bestätigen, indem Sie eine Suchanfrage (GET) an den Datenfluss stellen. Die API gibt den HTTP-Fehler 404 (Nicht gefunden) zurück, der angibt, dass der Datenfluss gelöscht wurde.

## Umgang mit API-Fehlern {#api-error-handling}

Die API-Endpunkte in diesem Tutorial folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Weitere Informationen [&#x200B; Interpretieren von Fehlerantworten finden Sie unter &#x200B;](/help/landing/troubleshooting.md#api-status-codes)API-Status-Codes[&#x200B; und &#x200B;](/help/landing/troubleshooting.md#request-header-errors)Fehler in der Anfragekopfzeile im Handbuch zur Fehlerbehebung bei Experience Platform .

## Nächste Schritte {#next-steps}

In diesem Tutorial haben Sie die [!DNL Flow Service]-API erfolgreich zum Löschen eines vorhandenen Datenflusses zu einem Ziel verwendet.

Wie Sie diese Vorgänge mithilfe der Benutzeroberfläche durchführen können, erfahren Sie im Tutorial zum [Löschen von Datenflüssen in der Benutzeroberfläche](../ui/delete-destinations.md).

Sie können jetzt mit der [!DNL Flow Service]-API [Zielkonten löschen](/help/destinations/api/delete-destination-account.md).
