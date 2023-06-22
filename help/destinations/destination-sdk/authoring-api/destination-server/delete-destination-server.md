---
description: Auf dieser Seite wird der API-Aufruf zum Löschen einer vorhandenen Ziel-Server-Konfiguration über Adobe Experience Platform Destination SDK erläutert.
title: Löschen einer Ziel-Server-Konfiguration
source-git-commit: acb7075f49b4194c31371d2de63709eea7821329
workflow-type: ht
source-wordcount: '329'
ht-degree: 100%

---


# Löschen einer Ziel-Server-Konfiguration

Auf dieser Seite werden die API-Anfrage und die Payload erläutert, die Sie verwenden können, um eine vorhandene Ziel-Server-Konfiguration mithilfe des API-Endpunkts `/authoring/destination-servers` zu löschen.

Eine ausführliche Beschreibung der Funktionen, die Sie über diesen Endpunkt löschen können, finden Sie in den folgenden Artikeln:

* [Server-Spezifikationen für Ziele, die mit Destination SDK erstellt wurden](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [Vorlagenspezifikationen für Ziele, die mit Destination SDK erstellt wurden](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [Nachrichtenformat](../../../destination-sdk/functionality/destination-server/message-format.md)
* [Konfiguration der Dateiformatierung](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Bei allen von Destination SDK unterstützten Parameternamen und Werten wird **nach Groß-/Kleinschreibung unterschieden**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Erste Schritte mit API-Vorgängen für Ziel-Server {#get-started}

Bevor Sie fortfahren, lesen Sie [Erste Schritte](../../getting-started.md) für wichtige Informationen, die Sie benötigen, um die API erfolgreich aufrufen zu können, einschließlich Informationen zum Abrufen der erforderlichen Authoring-Berechtigung für Ziele und der erforderlichen Kopfzeilen.

## Löschen einer Ziel-Server-Konfiguration {#delete}

Sie können eine [vorhandene](create-destination-server.md) Konfiguration des Ziel-Servers löschen, indem Sie eine `DELETE`-Anfrage an den Endpunkt `/authoring/destination-servers` mit der `{INSTANCE_ID}` der Ziel-Server-Konfiguration stellen, die Sie löschen möchten.

>[!TIP]
>
>**API-Endpunkt**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

Um eine vorhandene Ziel-Server-Konfiguration und die zugehörige `{INSTANCE_ID}` abzurufen, lesen Sie den Artikel über das [Abrufen einer Ziel-Server-Konfiguration](retrieve-destination-server.md).

**API-Format**

```http
DELETE /authoring/destination-servers/{INSTANCE_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{INSTANCE_ID}` | Die `ID` der Ziel-Server-Konfiguration, die Sie löschen möchten. |

+++Anfrage

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++Antwort

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 zusammen mit einer leeren HTTP-Antwort zurückgegeben.

## Umgang mit API-Fehlern {#error-handling}

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status-Codes](../../../../landing/troubleshooting.md#api-status-codes) und [Fehler im Anfrage-Header](../../../../landing/troubleshooting.md#request-header-errors) in der Anleitung zur Fehlerbehebung für Platform.

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie einen vorhandenen Ziel-Server über den API-Endpunkt `/authoring/destination-servers` von Destination SDK löschen können.

Weitere Informationen dazu, was Sie mit diesem Endpunkt tun können, finden Sie in den folgenden Artikeln:

* [Erstellen einer Ziel-Server-Konfiguration](create-destination-server.md)
* [Abrufen einer Ziel-Server-Konfiguration](retrieve-destination-server.md)
* [Aktualisieren einer Ziel-Server-Konfiguration](update-destination-server.md)

