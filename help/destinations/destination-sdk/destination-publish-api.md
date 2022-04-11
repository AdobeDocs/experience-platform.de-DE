---
description: Auf dieser Seite sind alle API-Vorgänge aufgelistet und beschrieben, die Sie mithilfe des API-Endpunkts „/authoring/destinations/publish“ ausführen können.
title: API-Endpunktvorgänge für Veröffentlichungsziele
exl-id: 0564a132-42f4-478c-9197-9b051acf093c
source-git-commit: 702a5b7154724faa9f5e6847b462e0ae90475571
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 75%

---

# API-Vorgänge für Endpunkte von Veröffentlichungszielen {#publish-destination}

>[!IMPORTANT]
>
>**API-Endpunkt**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

Auf dieser Seite werden alle API-Vorgänge aufgelistet und beschrieben, die Sie mit dem API-Endpunkt `/authoring/destinations/publish` ausführen können.

Nachdem Sie Ihr Ziel konfiguriert und getestet haben, können Sie es zur Überprüfung und Veröffentlichung an Adobe senden. Lesen [Zur Überprüfung eines in Destination SDK erstellten Ziels übermitteln](./submit-destination.md) für alle anderen Schritte, die Sie im Rahmen des Zielübermittlungsprozesses ausführen müssen.

Verwenden Sie den API-Endpunkt für Veröffentlichungsziele, um eine Veröffentlichungsanfrage zu senden, wenn:

* Als Destination SDK-Partner möchten Sie Ihr produktbezogenes Ziel über alle Experience Platform-Unternehmen für alle Experience Platform-Kunden verfügbar machen.
* Sie möchten Ihr benutzerdefiniertes Ziel in Ihrer eigenen Experience Platform-Organisation für alle Sandboxes verfügbar machen.

## Erste Schritte mit API-Vorgängen zur Zielveröffentlichung {#get-started}

Bevor Sie fortfahren, lesen Sie bitte [Erste Schritte](./getting-started.md), um sich wichtige Informationen zu verschaffen, die Sie benötigen, um die API erfolgreich aufrufen zu können. Dies betrifft auch Informationen zur Vorgehensweise beim Abrufen der erforderlichen Authoring-Berechtigung für Ziele und der erforderlichen Header.

## Senden einer Zielkonfiguration für das Veröffentlichen {#create}

Sie können eine Zielkonfiguration zum Veröffentlichen übermitteln, indem Sie eine POST-Anfrage an den Endpunkt `/authoring/destinations/publish` stellen.

**API-Format**

```http
POST /authoring/destinations/publish
```

**Anfrage**

Mit der folgenden Anfrage wird ein Ziel für eine Veröffentlichung in allen Organisationen gesendet, die von den in der Payload bereitgestellten Parametern konfiguriert wurden. Die nachstehende Payload enthält alle Parameter, die für den Endpunkt `/authoring/destinations/publish` zulässig sind.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `destinationId` | Zeichenfolge | Die Ziel-ID der Zielkonfiguration, die Sie für eine Veröffentlichung übermitteln. Rufen Sie die Ziel-ID einer Zielkonfiguration unter Verwendung der [API-Referenz für die Zielkonfiguration](./destination-configuration-api.md#retrieve-list) ab. |
| `destinationAccess` | Zeichenfolge | Verwendung `ALL` damit Ihr Ziel im Katalog für alle Experience Platform-Kunden angezeigt wird. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 201 mit Details zu Ihrer Zielveröffentlichungsanfrage zurückgegeben.

## Auflisten der Zielveröffentlichungsanfragen {#retrieve-list}

Sie können eine Liste aller für Ihre IMS-Organisation zur Veröffentlichung übermittelten Ziele abrufen, indem Sie eine GET-Anfrage an den Endpunkt `/authoring/destinations/publish` stellen.

**API-Format**

```http
GET /authoring/destinations/publish
```

**Anfrage**

Die folgende Anfrage ruft basierend auf der IMS-Organisation und der Sandbox-Konfiguration die Liste der Ziele ab, die zur Veröffentlichung gesendet wurden, auf die Sie Zugriff haben.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Die folgende Antwort gibt den HTTP-Status 200 mit einer Liste von Zielen zurück, die zur Veröffentlichung übermittelt wurden und auf die Sie Zugriff haben. Diese Liste basiert auf der von Ihnen verwendeten IMS-Organisations-ID und dem Sandbox-Namen der IMS-Organisation. Eine `configId` entspricht der Veröffentlichungsanfrage für jeweils ein Ziel.

```json
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "publishDetailsList":[
      {
         "configId":"123cs780-ce29-434f-921e-4ed6ec2a6c35",
         "allowedOrgs": [
            "*"
         ],    
         "status":"PUBLISHED",
         "destinationType": "PUBLIC",
         "publishedDate":"1630617746"
      }
   ]
}
```

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `destinationId` | Zeichenfolge | Die Ziel-ID der Zielkonfiguration, die Sie zur Veröffentlichung übermittelt haben. |
| `publishDetailsList.configId` | Zeichenfolge | Die eindeutige ID der Zielveröffentlichungsanfrage für Ihr übermitteltes Ziel. |
| `publishDetailsList.allowedOrgs` | Zeichenfolge | Gibt die Organisationen der Experience Platform zurück, für die das Ziel verfügbar ist. <br> <ul><li> Für `"destinationType": "PUBLIC"`, gibt dieser Parameter `"*"`, was bedeutet, dass das Ziel für alle Organisationen der Experience Platform verfügbar ist.</li><li> Für `"destinationType": "DEV"`gibt dieser Parameter die Organisations-ID der Organisation zurück, die Sie zum Erstellen und Testen des Ziels verwendet haben.</li></ul> |
| `publishDetailsList.status` | Zeichenfolge | Der Status Ihrer Anfrage zum Ziel der Veröffentlichung. Mögliche Werte sind `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`. Ziele mit dem Wert `PUBLISHED` sind live und können von Experience Platform-Kunden verwendet werden. |
| `publishDetailsList.destinationType` | Zeichenfolge | Der Zieltyp. Werte können `DEV` und `PUBLIC`. `DEV` entspricht dem Ziel in Ihrer Experience Platform-Organisation. `PUBLIC` entspricht dem Ziel, das Sie zur Veröffentlichung übermittelt haben. Stellen Sie sich diese beiden Optionen in Git-Begriffen vor, wobei die `DEV` -Version steht für Ihre lokale Authoring-Verzweigung und die `PUBLIC` version steht für den Remote-Hauptzweig. |
| `publishDetailsList.publishedDate` | Zeichenfolge | Das Datum, an dem das Ziel zur Veröffentlichung gesendet wurde, angegeben in Epochenzeit. |

{style=&quot;table-layout:auto&quot;}

## Abrufen des Status einer bestimmten Anfrage zum Ziel einer Veröffentlichung {#get}

Sie können detaillierte Informationen zu einer bestimmten Anfrage bezüglich des Ziels einer Veröffentlichung abrufen, indem Sie eine GET-Anfrage an den `/authoring/destinations/publish`-Endpunkt senden und darin die ID des Ziels angeben, für das Sie den Veröffentlichungsstatus abrufen möchten.

**API-Format**

```http
GET /authoring/destinations/publish/{DESTINATION_ID}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{DESTINATION_ID}` | Die ID des Ziels, für das Sie den Veröffentlichungsstatus abrufen möchten. |

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish/1230e5e4-4ab8-4655-ae1e-a6296b30f2ec \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit detaillierten Informationen zur angegebenen Anfrage bezüglich des Ziels der Veröffentlichung zurück.

```json
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "publishDetailsList":[
      {
         "configId":"ab41387c0-4772-4709-a3ce-6d5fee654520",
         "allowedOrgs":[
            "716543205DB85F7F0A495E5B@AdobeOrg"
         ],
         "status":"TEST",
         "destinationType":"DEV"
      },
      {
         "configId":"cd568c67-f25e-47e4-b9a2-d79297a20b27",
         "allowedOrgs":[
            "*"
         ],
         "status":"DEPRECATED",
         "destinationType":"PUBLIC",
         "publishedDate":1630525501009
      },
      {
         "configId":"ef6f07154-09bc-4bee-8baf-828ea9c92fba",
         "allowedOrgs":[
            "*"
         ],
         "status":"PUBLISHED",
         "destinationType":"PUBLIC",
         "publishedDate":1630531586002
      }
   ]
}
```

## Umgang mit API-Fehlern

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status-Codes](../../landing/troubleshooting.md#api-status-codes) und [Fehler im Anfrage-Header](../../landing/troubleshooting.md#request-header-errors) in der Anleitung zur Fehlerbehebung für Platform.

## Nächste Schritte

Nach dem Studium dieses Dokuments wissen Sie jetzt, wie Sie eine Veröffentlichungsanfrage für Ihr Ziel senden können. Das Adobe Experience Platform-Team prüft Ihre Veröffentlichungsanfrage und setzt sich innerhalb von fünf Werktagen mit Ihnen in Verbindung.
