---
keywords: Experience Platform;Startseite;beliebte Themen;Flow Service;Zielkonten löschen;löschen;API
solution: Experience Platform
title: Löschen eines Zielkontos mithilfe der Flow Service-API
type: Tutorial
description: Erfahren Sie, wie Sie ein Zielkonto mithilfe der Flow Service-API löschen können.
exl-id: a963073c-ecba-486b-a5c2-b85bdd426e72
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 38%

---

# Löschen eines Zielkontos mithilfe der Flow Service-API

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

Vor der Aktivierung von Daten müssen Sie eine Verbindung zum Ziel herstellen, indem Sie zunächst ein Zielkonto einrichten. In diesem Tutorial werden die Schritte zum Löschen von Zielkonten beschrieben, die nicht mehr benötigt werden, indem die -[[!DNL Flow Service]  verwendet ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>Das Löschen von Zielkonten wird derzeit nur in der Flow Service-API unterstützt. Zielkonten können nicht über die Experience Platform-Benutzeroberfläche gelöscht werden.

## Erste Schritte {#get-started}

Für dieses Tutorial benötigen Sie eine gültige Verbindungs-ID. Die Verbindungs-ID stellt die Kontoverbindung zum Ziel dar. Wenn Sie keine gültige Verbindungs-ID haben, wählen Sie Ihr Ziel aus dem [Zielkatalog](../catalog/overview.md) und führen Sie die zum Herstellen einer [ mit dem Ziel beschriebenen Schritte aus, ](../ui/connect-destination.md) Sie dieses Tutorial ausführen.

Dieses Tutorial setzt außerdem ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Ziele](../home.md): [!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.
* [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Experience Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um ein Zielkonto mithilfe der [!DNL Flow Service]-API erfolgreich löschen zu können.

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

## Suchen Sie die Verbindungs-ID des Zielkontos, das Sie löschen möchten {#find-connection-id}

>[!NOTE]
>In diesem Tutorial wird das [Airship-Ziel](../catalog/mobile-engagement/airship-attributes.md) als Beispiel verwendet, aber die beschriebenen Schritte gelten für jedes der [verfügbaren Ziele](../catalog/overview.md).

Der erste Schritt beim Löschen eines Zielkontos besteht darin, die Verbindungs-ID herauszufinden, die dem Zielkonto entspricht, das Sie löschen möchten.

Navigieren Sie in der Experience Platform-Benutzeroberfläche zu **[!UICONTROL Destinations]** > **[!UICONTROL Accounts]** und wählen Sie das zu löschende Konto aus, indem Sie die Zahl in der Spalte **[!UICONTROL Destinations]** auswählen.

![Zielkonto zum Löschen auswählen](/help/destinations/assets/api/delete-destination-account/select-destination-account.png)

Als Nächstes können Sie die Verbindungs-ID des Zielkontos über die URL in Ihrem Browser abrufen.

![Abrufen der Verbindungs-ID aus der URL](/help/destinations/assets/api/delete-destination-account/find-connection-id.png)

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
            "imsOrgId": "{ORG_ID}",
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
>>Informationen zum Löschen vorhandener Datenflüsse finden Sie auf den folgenden Seiten:
>
>* [Verwenden der Experience Platform-Benutzeroberfläche](../ui/delete-destinations.md) um vorhandene Datenflüsse zu löschen;
>* [Verwenden der Flow Service-API](delete-destination-dataflow.md) um vorhandene Datenflüsse zu löschen.

Nachdem Sie über eine Verbindungs-ID verfügen und sichergestellt haben, dass keine Datenflüsse zum Zielkonto vorhanden sind, führen Sie eine DELETE-Anfrage an die [!DNL Flow Service]-API aus.

**API-Format**

```http
DELETE /connections/{CONNECTION_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{CONNECTION_ID}` | Der eindeutige `id` für die Verbindung, die Sie löschen möchten. |

**Anfrage**

```shell
curl -X DELETE \
    'https://platform.adobe.io/data/foundation/flowservice/connections/c8622ec7-7d94-44a5-a35a-ffcc6bdcc384' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) und leeren Text zurück. Sie können den Löschvorgang bestätigen, indem Sie eine Suchanfrage (GET) an die Verbindung stellen. Die API gibt den HTTP-404-Fehler (Nicht gefunden) zurück, der angibt, dass das Zielkonto gelöscht wurde.

## Umgang mit API-Fehlern {#api-error-handling}

Die API-Endpunkte in diesem Tutorial folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status](../../landing/troubleshooting.md#api-status-codes)Codes und [Fehler in der Anfragekopfzeile](../../landing/troubleshooting.md#request-header-errors) im Handbuch zur Fehlerbehebung bei Experience Platform.

## Nächste Schritte

In diesem Tutorial haben Sie die [!DNL Flow Service]-API erfolgreich zum Löschen vorhandener Zielkonten verwendet. Weitere Informationen zur Verwendung von Zielen finden Sie unter [Ziele - Übersicht](/help/destinations/home.md).