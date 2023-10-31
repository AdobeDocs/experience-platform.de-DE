---
description: Auf dieser Seite wird der API-Aufruf zum Löschen einer vorhandenen Zielkonfiguration über Adobe Experience Platform Destination SDK erläutert.
title: Löschen einer Zielkonfiguration
exl-id: c7309ab7-1b8d-46d4-8017-fd4aa5918cdd
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 100%

---

# Löschen einer Zielkonfiguration

Auf dieser Seite werden die API-Anfrage und die Payload erläutert, die Sie verwenden können, um eine vorhandene Zielkonfiguration mithilfe des API-Endpunkts `/authoring/destinations` zu löschen.

>[!IMPORTANT]
>
>Bei allen von Destination SDK unterstützten Parameternamen und Werten wird **nach Groß-/Kleinschreibung unterschieden**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Erste Schritte mit API-Vorgängen für die Zielkonfiguration {#get-started}

Bevor Sie fortfahren, lesen Sie [Erste Schritte](../../getting-started.md). Dort finden Sie die nötigen Informationen für den erfolgreichen Aufruf der API, einschließlich Details für den Abruf der erforderlichen Authoring-Berechtigung für Ziele und zu den erforderlichen Kopfzeilen.

## Löschen einer Zielkonfiguration {#delete}

Sie können eine [vorhandene](create-destination-configuration.md) Konfiguration des Ziel-Servers löschen, indem Sie eine `DELETE`-Anfrage an den Endpunkt `/authoring/destinations` mit der `{INSTANCE_ID}` der Zielkonfiguration stellen, die Sie löschen möchten.

>[!TIP]
>
>**API-Endpunkt**: `platform.adobe.io/data/core/activation/authoring/destinations`

Wie Sie eine vorhandene Zielkonfiguration und die dazugehörige `{INSTANCE_ID}` abrufen, erfahren Sie im Artikel zum [Abrufen einer Zielkonfiguration](retrieve-destination-configuration.md).

**API-Format**

```http
DELETE /authoring/destinations/{INSTANCE_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{INSTANCE_ID}` | Die `ID` der Zielkonfiguration, die Sie löschen möchten. |

+++Anfrage

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destinations/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++Antwort

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 zusammen mit einer leeren HTTP-Antwort zurückgegeben.


## Umgang mit API-Fehlern {#error-handling}

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status-Codes](../../../../landing/troubleshooting.md#api-status-codes) und [Fehler im Anfrage-Header](../../../../landing/troubleshooting.md#request-header-errors) in der Anleitung zur Fehlerbehebung für Platform.

## Nächste Schritte

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie eine vorhandene Zielkonfiguration über den API-Endpunkt `/authoring/destinations` von Destination SDK löschen können.

Weitere Informationen dazu, was Sie mit diesem Endpunkt tun können, finden Sie in den folgenden Artikeln:

* [Erstellen einer Zielkonfiguration](create-destination-configuration.md)
* [Abrufen einer Zielkonfiguration](retrieve-destination-configuration.md)
* [Aktualisieren einer Zielkonfiguration](update-destination-configuration.md)
