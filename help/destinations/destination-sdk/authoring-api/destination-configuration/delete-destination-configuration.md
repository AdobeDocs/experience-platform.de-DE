---
description: Auf dieser Seite wird der API-Aufruf zum Löschen einer vorhandenen Zielkonfiguration über Adobe Experience Platform Destination SDK erläutert.
title: Löschen einer Zielkonfiguration
exl-id: c7309ab7-1b8d-46d4-8017-fd4aa5918cdd
source-git-commit: 2dd4ae4146f7c1c5228e22d24ff2ba31010adedb
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 72%

---

# Löschen einer Zielkonfiguration

Auf dieser Seite werden die API-Anfrage und die Payload erläutert, die Sie verwenden können, um eine vorhandene Zielkonfiguration mithilfe des API-Endpunkts `/authoring/destinations` zu löschen.

>[!IMPORTANT]
>
>Bei allen von Destination SDK unterstützten Parameternamen und Werten wird **nach Groß-/Kleinschreibung unterschieden**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Erste Schritte mit API-Vorgängen für die Zielkonfiguration {#get-started}

Bevor Sie fortfahren, lesen Sie den Abschnitt [Erste Schritte](../../getting-started.md). Dort erhalten Sie wichtige Informationen darüber, wie Sie die API aufrufen und die erforderliche Authoring-Berechtigung für Ziele und die Kopfzeilen abrufen können.

## Löschen einer Zielkonfiguration {#delete}

Sie können eine [vorhandene](create-destination-configuration.md) Zielkonfiguration löschen, indem Sie eine `DELETE`-Anfrage an den `/authoring/destinations`-Endpunkt mit der `{INSTANCE_ID}`der Zielkonfiguration stellen, die Sie löschen möchten.

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

{style="table-layout:auto"}

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

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status](../../../../landing/troubleshooting.md#api-status-codes)Codes und [Fehler in der Anfragekopfzeile](../../../../landing/troubleshooting.md#request-header-errors) im Handbuch zur Fehlerbehebung bei Experience Platform.

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie eine vorhandene Zielkonfiguration über den API-Endpunkt `/authoring/destinations` von Destination SDK löschen können.

Weitere Informationen dazu, was Sie mit diesem Endpunkt tun können, finden Sie in den folgenden Artikeln:

* [Erstellen einer Zielkonfiguration](create-destination-configuration.md)
* [Abrufen einer Zielkonfiguration](retrieve-destination-configuration.md)
* [Aktualisieren einer Zielkonfiguration](update-destination-configuration.md)
