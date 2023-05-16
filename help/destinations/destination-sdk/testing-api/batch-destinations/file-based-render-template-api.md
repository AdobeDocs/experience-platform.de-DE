---
description: Auf dieser Seite wird erläutert, wie Sie mit dem Endpunkt /authoring/testing/template/render visualisieren können, wie die in Ihrer Zielkonfiguration definierten vorlagenbasierten Kundendatenfelder aussehen.
title: Überprüfen von vorlagenbasierten Kundenfeldern
exl-id: 8ed93f0c-3439-4d11-bb2f-d417a1e0b6a8
source-git-commit: 6bd169075cd3826ae2a0907e6e624fd901076a4a
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 22%

---


# Überprüfen von vorlagenbasierten Kundenfeldern

## Übersicht {#overview}

Die `/authoring/testing/template/render` Endpunkt hilft Ihnen bei der Visualisierung der Vorlagenerstellung [Kundendatenfelder](../../functionality/destination-configuration/customer-data-fields.md) in Ihrer Zielkonfiguration definiert wurde, würde so aussehen.

Der Endpunkt generiert zufällige Werte für Ihre Kundendatenfelder und gibt sie in der Antwort zurück. Auf diese Weise können Sie die semantische Struktur von Kundendatenfeldern, wie z. B. Behälternamen oder Ordnerpfaden, überprüfen.

## Erste Schritte {#getting-started}

Bevor Sie fortfahren, lesen Sie [Erste Schritte](../../getting-started.md). Dort finden Sie die nötigen Informationen für den erfolgreichen Aufruf der API, einschließlich Details für den Abruf der erforderlichen Authoring-Berechtigung für Ziele und zu den erforderlichen Kopfzeilen.

## Voraussetzungen {#prerequisites}

Bevor Sie die `/template/render` -Endpunkt verwenden, stellen Sie sicher, dass Sie die folgenden Bedingungen erfüllen:

* Sie haben ein vorhandenes dateibasiertes Ziel, das über die Destination SDK erstellt wurde, und Sie können es in Ihrem [Zielkatalog](../../../ui/destinations-workspace.md).
* Für eine erfolgreiche API-Anfrage benötigen Sie die Ziel-Instanz-ID, die der zu testenden Zielinstanz entspricht. Rufen Sie die Ziel-Instanz-ID ab, die Sie beim Durchsuchen einer Verbindung mit Ihrem Ziel in der Platform-Benutzeroberfläche im API-Aufruf über die URL verwenden sollten.

   ![UI-Bild, das zeigt, wie die Ziel-Instanz-ID von der URL abgerufen wird.](../../assets/testing-api/get-destination-instance-id.png)

## Rendern von vorlagenbasierten Kundenfeldern {#render-customer-fields}

**API-Format**

```http
POST /authoring/testing/template/render/destination
```

Um das Verhalten dieses API-Endpunkts zu veranschaulichen, betrachten wir ein dateibasiertes Ziel mit der folgenden Konfiguration von Kundendatenfeldern:

```json
"fileBasedS3Destination":{
   "bucket":{
      "templatingStrategy":"PEBBLE_V1",
      "value":"{{customerData.bucket}}"
   },
   "path":{
      "templatingStrategy":"PEBBLE_V1",
      "value":"{{customerData.path}}"
   }
}
```

**Anfrage**

Die nachstehende Anfrage ruft die `/authoring/testing/template/render` -Endpunkt, der eine Antwort mit zufällig generierten Werten für die beiden oben genannten Kundendatenfelder zurückgibt.

```shell
curl -X POST 'https://platform.adobe.io/data/core/activation/authoring/testing/template/render/destination' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
    "destinationId": "{DESTINATION_CONFIGURATION_ID}",
    "templates": {
        "bucket": "{{customerData.bucket}}",
        "path": "{{customerData.bucket}}/{{customerData.path}}"
    }
}'
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `destinationId` | Die ID der [Zielkonfiguration](../../authoring-api/destination-configuration/retrieve-destination-configuration.md) die Sie testen. |
| `templates` | Die in Ihrer [Zielserverkonfiguration](../../authoring-api/destination-server/create-destination-server.md). |

**Antwort**

Eine erfolgreiche Antwort gibt eine `HTTP 200 OK` und der Hauptteil zufällig generierte Werte für Ihre Vorlagenfelder enthält.

Diese Antwort kann Ihnen dabei helfen, die richtige Struktur Ihrer Kundendatenfelder zu überprüfen, z. B. Behälternamen oder Ordnerpfade.


```json
{
    "results": {
        "bucket": "hfWpE-bucket",
        "path": "hfWpE-bucket/ceC"
    }
}
```

## Umgang mit API-Fehlern {#api-error-handling}

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status-Codes](../../../../landing/troubleshooting.md#api-status-codes) und [Fehler im Anfrage-Header](../../../../landing/troubleshooting.md#request-header-errors) in der Anleitung zur Fehlerbehebung für Platform.

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie die in Ihrem [Zielserver](../../authoring-api/destination-server/create-destination-server.md).
