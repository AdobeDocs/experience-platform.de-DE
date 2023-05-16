---
description: Erfahren Sie, wie Sie einen API-Aufruf formatieren, um eine Anfrage zur Veröffentlichung über Adobe Experience Platform Destination SDK zu senden.
title: Erstellen einer Zielveröffentlichungsanforderung
source-git-commit: acb7075f49b4194c31371d2de63709eea7821329
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 56%

---


# Erstellen einer Zielveröffentlichungsanforderung

>[!IMPORTANT]
>
>Sie müssen diesen API-Endpunkt nur verwenden, wenn Sie ein produktives (öffentliches) Ziel senden, das von anderen Experience Platform-Kunden verwendet werden soll. Wenn Sie ein privates Ziel für Ihre eigene Verwendung erstellen, müssen Sie das Ziel nicht formell mit der Publishing-API übermitteln.

>[!IMPORTANT]
>
>**API-Endpunkt**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

Nachdem Sie Ihr Ziel konfiguriert und getestet haben, können Sie es zur Überprüfung und Veröffentlichung an Adobe senden. Lesen [Zur Überprüfung eines in Destination SDK erstellten Ziels übermitteln](../guides/submit-destination.md) für alle anderen Schritte, die Sie im Rahmen des Zielübermittlungsprozesses ausführen müssen.

Verwenden Sie den API-Endpunkt für Veröffentlichungsziele, um eine Veröffentlichungsanfrage zu senden, wenn:

* Als Destination SDK-Partner möchten Sie Ihr produktbezogenes Ziel über alle Experience Platform-Unternehmen für alle Experience Platform-Kunden verfügbar machen.
* Sie machen *alle Aktualisierungen* zu Ihren Konfigurationen hinzufügen. Konfigurationsaktualisierungen werden erst dann im Ziel angezeigt, wenn Sie eine neue Veröffentlichungsanforderung senden, die vom Experience Platform-Team genehmigt wurde.

>[!IMPORTANT]
>
>Alle von Destination SDK unterstützten Parameternamen und Werte sind **Groß-/Kleinschreibung**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

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
| `destinationId` | Zeichenfolge | Die Ziel-ID der Zielkonfiguration, die Sie für eine Veröffentlichung übermitteln. Rufen Sie die Ziel-ID einer Zielkonfiguration ab, indem Sie die [Zielkonfiguration abrufen](../authoring-api/destination-configuration/retrieve-destination-configuration.md) API-Aufruf. |
| `destinationAccess` | Zeichenfolge | Verwendung `ALL` damit Ihr Ziel im Katalog für alle Experience Platform-Kunden angezeigt wird. |

{style="table-layout:auto"}

+++Antwort

Bei einer erfolgreichen Antwort wird der HTTP-Status 201 mit Details zu Ihrer Zielveröffentlichungsanfrage zurückgegeben.

## Umgang mit API-Fehlern

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status-Codes](../../../landing/troubleshooting.md#api-status-codes) und [Fehler im Anfrage-Header](../../../landing/troubleshooting.md#request-header-errors) in der Anleitung zur Fehlerbehebung für Platform.

## Nächste Schritte

Nach dem Studium dieses Dokuments wissen Sie jetzt, wie Sie eine Veröffentlichungsanfrage für Ihr Ziel senden können. Das Adobe Experience Platform-Team prüft Ihre Veröffentlichungsanfrage und setzt sich innerhalb von fünf Werktagen mit Ihnen in Verbindung.