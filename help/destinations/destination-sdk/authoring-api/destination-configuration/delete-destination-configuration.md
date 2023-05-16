---
description: Auf dieser Seite wird der API-Aufruf zum Löschen einer vorhandenen Zielkonfiguration über Adobe Experience Platform Destination SDK erläutert.
title: Zielkonfiguration löschen
source-git-commit: acb7075f49b4194c31371d2de63709eea7821329
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 35%

---


# Zielkonfiguration löschen

Auf dieser Seite werden die API-Anfrage und die Payload erläutert, die Sie verwenden können, um eine vorhandene Zielkonfiguration mithilfe der `/authoring/destinations` API-Endpunkt.

>[!IMPORTANT]
>
>Alle von Destination SDK unterstützten Parameternamen und Werte sind **Groß-/Kleinschreibung**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Erste Schritte mit API-Vorgängen zur Zielkonfiguration {#get-started}

Bevor Sie fortfahren, lesen Sie [Erste Schritte](../../getting-started.md). Dort finden Sie die nötigen Informationen für den erfolgreichen Aufruf der API, einschließlich Details für den Abruf der erforderlichen Authoring-Berechtigung für Ziele und zu den erforderlichen Kopfzeilen.

## Zielkonfiguration löschen {#delete}

Sie können eine [vorhandene](create-destination-configuration.md) Konfiguration des Zielservers durch `DELETE` Anfrage an `/authoring/destinations` Endpunkt mit der `{INSTANCE_ID}`der Zielkonfiguration, die Sie löschen möchten.

>[!TIP]
>
>**API-Endpunkt**: `platform.adobe.io/data/core/activation/authoring/destinations`

So rufen Sie eine vorhandene Zielkonfiguration und die zugehörigen `{INSTANCE_ID}`, siehe Artikel zu [Abrufen einer Zielkonfiguration](retrieve-destination-configuration.md).

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

Eine erfolgreiche Antwort gibt den HTTP-Status 200 zusammen mit einer leeren HTTP-Antwort zurück.


## Umgang mit API-Fehlern {#error-handling}

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status-Codes](../../../../landing/troubleshooting.md#api-status-codes) und [Fehler im Anfrage-Header](../../../../landing/troubleshooting.md#request-header-errors) in der Anleitung zur Fehlerbehebung für Platform.

## Nächste Schritte

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie eine vorhandene Zielkonfiguration über die Destination SDK löschen können `/authoring/destinations` API-Endpunkt.

Weitere Informationen dazu, was Sie mit diesem Endpunkt tun können, finden Sie in den folgenden Artikeln:

* [Erstellen einer Zielkonfiguration](create-destination-configuration.md)
* [Abrufen einer Zielkonfiguration](retrieve-destination-configuration.md)
* [Zielkonfiguration aktualisieren](update-destination-configuration.md)

