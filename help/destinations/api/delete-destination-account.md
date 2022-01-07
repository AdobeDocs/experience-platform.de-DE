---
keywords: Experience Platform; Startseite; beliebte Themen; Flussdienst; Löschen von Zielkonten; Löschen; API
solution: Experience Platform
title: Löschen eines Zielkontos mithilfe der Flow Service-API
type: Tutorial
description: Erfahren Sie, wie Sie ein Zielkonto mithilfe der Flow Service-API löschen.
source-git-commit: df89f8ce8050b26068e0ab7aa01f1c964f5d2422
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 37%

---

# Löschen eines Zielkontos mithilfe der Flow Service-API

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

Bevor Sie Daten aktivieren, müssen Sie eine Verbindung zum Ziel herstellen, indem Sie zunächst ein Zielkonto einrichten. In diesem Tutorial werden die Schritte zum Löschen von Zielkonten beschrieben, die nicht mehr benötigt werden, indem Sie die [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>Das Löschen von Zielkonten wird derzeit nur in der Flow Service-API unterstützt. Zielkonten können nicht über die Experience Platform-Benutzeroberfläche gelöscht werden.

## Erste Schritte {#get-started}

Für dieses Tutorial benötigen Sie eine gültige Verbindungs-ID. Die Verbindungs-ID stellt die Kontoverbindung zum Ziel dar. Wenn Sie keine gültige Verbindungs-ID haben, wählen Sie Ihr Ziel aus der [Zielkatalog](../catalog/overview.md) und führen Sie die Schritte aus, die beschrieben wurden, um [Verbindung zum Ziel herstellen](../ui/connect-destination.md) vor dem Versuch dieses Tutorials.

Für dieses Tutorial benötigen Sie außerdem ein Verständnis der folgenden Komponenten von Adobe Experience Platform:

* [Ziele sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. ](../home.md)[!DNL Destinations] Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.
* [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um ein Zielkonto mit der [!DNL Flow Service] API.

### Lesen von Beispiel-API-Aufrufen {#reading-sample-api-calls}

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen {#gather-values-for-required-headers}

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de#platform-apis) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform], einschließlich der Ressourcen, die zu [!DNL Flow Service] gehören, werden in bestimmten virtuellen Sandboxes isoliert. Bei allen Anfragen an [!DNL Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Wenn die Variable `x-sandbox-name` -Kopfzeile nicht angegeben ist, werden Anfragen unter der `prod` Sandbox.

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* `Content-Type: application/json`

## Suchen Sie die Verbindungs-ID des Zielkontos, das Sie löschen möchten {#find-connection-id}

>[!NOTE]
>In diesem Tutorial wird die [Bestimmungsort des Luftschiffes](../catalog/mobile-engagement/airship-attributes.md) Beispiel: Die beschriebenen Schritte gelten jedoch für alle [verfügbare Ziele](../catalog/overview.md).

Der erste Schritt beim Löschen eines Zielkontos besteht darin, die Verbindungs-ID zu ermitteln, die dem Zielkonto entspricht, das Sie löschen möchten.

Navigieren Sie in der Experience Platform-Benutzeroberfläche zu **[!UICONTROL Ziele]** > **[!UICONTROL Konten]** und wählen Sie das Konto aus, das Sie löschen möchten, indem Sie die Nummer im **[!UICONTROL Ziele]** Spalte.

![Zielkonto zum Löschen auswählen](/help/destinations/assets/api/delete-destination-account/select-destination-account.png)

Als Nächstes können Sie die Verbindungs-ID des Zielkontos aus der URL in Ihrem Browser abrufen.

![Verbindungs-ID von URL abrufen](/help/destinations/assets/api/delete-destination-account/find-connection-id.png)

<!--

## Look up connection ID {#look-up-connection-id}

The first step in updating your connection information is to retrieve connection details using your connection ID.

**API format**

```http
GET /connections/{CONNECTION_ID}
```

| Parameter | Description |
| --------- | ----------- |
| `{CONNECTION_ID}` | The unique `id` value for the connection you want to retrieve. |

**Request**

The following request retrieves information regarding your connection ID.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/c8622ec7-7d94-44a5-a35a-ffcc6bdcc384' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Response**

A successful response returns the current details of your connection including its credentials, unique identifier (`id`), and version.

```json
{
    "items": [
        {
            "id": "c8622ec7-7d94-44a5-a35a-ffcc6bdcc384",
            "createdAt": 1640103419202,
            "updatedAt": 1640104751063,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{IMS_ORG}",
            "name": "Airship Attributes",
            "description": "test account connection to Airship Attributes destination",
            "connectionSpec": {
                "id": "34cd3131-b208-474b-b779-b487b5a2bd01",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Bearer Token",
                "params": {
                    "authorizedDate": "2021-12-21",
                    "token": "xxxx"
                }
            },
            "version": "\"8c01091c-0000-0200-0000-61c2032f0000\"",
            "etag": "\"8c01091c-0000-0200-0000-61c2032f0000\""
        }
    ]
}
```

-->

## Verbindung löschen {#delete-connection}

>[!IMPORTANT]
>
>Bevor Sie das Zielkonto löschen, müssen Sie alle vorhandenen Datenflüsse zum Zielkonto löschen.
>Informationen zum Löschen vorhandener Datenflüsse finden Sie auf den folgenden Seiten:
>* [Verwenden der Experience Platform-Benutzeroberfläche](../ui/delete-destinations.md) Löschen vorhandener Datenflüsse;
>* [Verwenden der Flow Service-API](delete-destination-dataflow.md) , um vorhandene Datenflüsse zu löschen.


Nachdem Sie über eine Verbindungs-ID verfügen und sichergestellt haben, dass keine Datenflüsse zum Zielkonto vorhanden sind, führen Sie eine DELETE-Anfrage an die [!DNL Flow Service] API.

**API-Format**

```http
DELETE /connections/{CONNECTION_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{CONNECTION_ID}` | Die eindeutige `id` für die Verbindung, die Sie löschen möchten. |

**Anfrage**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/connections/c8622ec7-7d94-44a5-a35a-ffcc6bdcc384' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) und leeren Text zurück. Sie können den Löschvorgang bestätigen, indem Sie eine Nachschlageanfrage (GET) für die Verbindung ausführen. Die API gibt einen HTTP 404-Fehler (Nicht gefunden) zurück, der angibt, dass das Zielkonto gelöscht wurde.

## Umgang mit API-Fehlern {#api-error-handling}

Die API-Endpunkte in diesem Tutorial folgen den allgemeinen Grundsätzen für die Fehlermeldung bei der Experience Platform-API. Siehe [API-Statuscodes](../../landing/troubleshooting.md#api-status-codes) und [Fehler in der Anfragekopfzeile](../../landing/troubleshooting.md#request-header-errors) im Handbuch zur Fehlerbehebung bei Platform.

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich die [!DNL Flow Service] API zum Löschen vorhandener Zielkonten.
