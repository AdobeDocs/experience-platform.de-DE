---
description: Erfahren Sie, wie Sie einen API-Aufruf formatieren, um eine Anfrage zur Veröffentlichung über Adobe Experience Platform Destination SDK zu senden.
title: Erstellen einer Zielveröffentlichungsanfrage
exl-id: 913be9de-a699-4756-885d-b3761ec729cb
source-git-commit: 20427c4c8826905a77fac04d055d523b12a6f739
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 85%

---

# Erstellen einer Zielveröffentlichungsanfrage

>[!IMPORTANT]
>
>Sie müssen diesen API-Endpunkt nur verwenden, wenn Sie ein produktbezogenes (öffentliches) Ziel einreichen, das von anderen Experience Platform-Kundinnen und -Kunden verwendet werden soll. Wenn Sie ein privates Ziel für Ihre eigene Verwendung erstellen, müssen Sie das Ziel nicht formell mit der Veröffentlichungs-API übermitteln.

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

Bevor Sie fortfahren, lesen Sie den Abschnitt [Erste Schritte](../getting-started.md). Dort erhalten Sie wichtige Informationen darüber, wie Sie die API aufrufen und die erforderliche Authoring-Berechtigung für Ziele und die Kopfzeilen abrufen können.

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

## Umgang mit API-Fehlern {#error-handling}

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status](../../../landing/troubleshooting.md#api-status-codes)Codes und [Fehler in der Anfragekopfzeile](../../../landing/troubleshooting.md#request-header-errors) im Handbuch zur Fehlerbehebung bei Experience Platform.

## Nächste Schritte {#next-steps}

Nach dem Studium dieses Dokuments wissen Sie jetzt, wie Sie eine Veröffentlichungsanfrage für Ihr Ziel senden können. Das [!DNL Adobe Experience Platform]-Team prüft Ihre Veröffentlichungsanfrage und setzt sich innerhalb von fünf Werktagen mit Ihnen in Verbindung.
