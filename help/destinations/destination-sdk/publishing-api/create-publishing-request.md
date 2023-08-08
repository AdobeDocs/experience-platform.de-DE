---
description: Erfahren Sie, wie Sie einen API-Aufruf formatieren, um eine Anfrage zur Veröffentlichung über Adobe Experience Platform Destination SDK zu senden.
title: Erstellen einer Zielveröffentlichungsanfrage
source-git-commit: 8ec5d450d2856b9a12457e1b1b0b46baf930253a
workflow-type: ht
source-wordcount: '447'
ht-degree: 100%

---


# Erstellen einer Zielveröffentlichungsanfrage

>[!IMPORTANT]
>
>Sie müssen diesen API-Endpunkt nur verwenden, wenn Sie ein produktbezogenes (öffentliches) Ziel einreichen, das von anderen Experience Platform-Kundinnen und -Kunden verwendet werden soll. Wenn Sie ein privates Ziel für Ihre eigene Verwendung erstellen, müssen Sie das Ziel nicht formell mit der Publishing-API übermitteln.

>[!IMPORTANT]
>
>**API-Endpunkt**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

Nachdem Sie Ihr Ziel konfiguriert und getestet haben, können Sie es zur Überprüfung und Veröffentlichung an Adobe senden. Lesen Sie [Einreichen eines in Destination SDK erstellten Ziels zur Überprüfung](../guides/submit-destination.md), um alle weiteren Schritte zu erfahren, die Sie im Rahmen des Einreichungsprozesses für ein Ziel durchführen müssen.

Verwenden Sie den API-Endpunkt für Veröffentlichungsziele, um eine Veröffentlichungsanfrage zu senden, wenn Sie:

* als Destination SDK-Partner Ihr produktbezogenes Ziel über alle Experience Platform-Organisationen für alle Experience Platform-Kundinnen und -Kunden verfügbar machen möchten.
* *Aktualisierungen jeglicher Art* an Ihren Konfigurationen vornehmen. Konfigurationsaktualisierungen werden erst dann im Ziel angezeigt, wenn Sie eine neue Veröffentlichungsanfrage senden, die vom Experience Platform-Team genehmigt wurde.

>[!IMPORTANT]
>
>Bei allen von Destination SDK unterstützten Parameternamen und Werten wird **nach Groß-/Kleinschreibung unterschieden**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Erste Schritte mit API-Vorgängen zur Zielveröffentlichung {#get-started}

Bevor Sie fortfahren, lesen Sie bitte [Erste Schritte](../getting-started.md), um sich wichtige Informationen zu verschaffen, die Sie benötigen, um die API erfolgreich aufrufen zu können. Dies betrifft auch Informationen zur Vorgehensweise beim Abrufen der erforderlichen Authoring-Berechtigung für Ziele und der erforderlichen Header.

## Senden einer Zielkonfiguration für das Veröffentlichen {#create}

Sie können eine Zielkonfiguration zum Veröffentlichen übermitteln, indem Sie eine POST-Anfrage an den Endpunkt `/authoring/destinations/publish` stellen.

**API-Format**

```http
POST /authoring/destinations/publish
```

+++Anfrage

Mit der folgenden Anfrage wird ein Ziel für eine Veröffentlichung in allen Organisationen gesendet, die von den in der Payload bereitgestellten Parametern konfiguriert wurden. Die nachstehende Payload enthält alle Parameter, die für den Endpunkt `/authoring/destinations/publish` zulässig sind.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "destinationAccess":"ALL"
}
```

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `destinationId` | Zeichenfolge | Die Ziel-ID der Zielkonfiguration, die Sie für eine Veröffentlichung übermitteln. Rufen Sie die Ziel-ID einer Zielkonfiguration ab, indem Sie den API-Aufruf zum [Abrufen einer Zielkonfiguration](../authoring-api/destination-configuration/retrieve-destination-configuration.md) verwenden. |
| `destinationAccess` | Zeichenfolge | Verwenden Sie `ALL`, damit Ihr Ziel im Katalog für alle Experience Platform-Kundinnen und -Kunden angezeigt wird. |

{style="table-layout:auto"}

+++

+++Antwort

Bei einer erfolgreichen Antwort wird der HTTP-Status 201 mit Details zu Ihrer Zielveröffentlichungsanfrage zurückgegeben.

+++

## Umgang mit API-Fehlern

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status-Codes](../../../landing/troubleshooting.md#api-status-codes) und [Fehler im Anfrage-Header](../../../landing/troubleshooting.md#request-header-errors) in der Anleitung zur Fehlerbehebung für Platform.

## Nächste Schritte

Nach dem Studium dieses Dokuments wissen Sie jetzt, wie Sie eine Veröffentlichungsanfrage für Ihr Ziel senden können. Das Adobe Experience Platform-Team prüft Ihre Veröffentlichungsanfrage und setzt sich innerhalb von fünf Werktagen mit Ihnen in Verbindung.