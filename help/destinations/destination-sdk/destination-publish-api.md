---
description: Auf dieser Seite werden alle API-Vorgänge aufgelistet und beschrieben, die Sie mit dem API-Endpunkt "/authoring/destinations/publish"ausführen können.
title: API-Endpunktvorgänge für Veröffentlichungsziele
exl-id: 0564a132-42f4-478c-9197-9b051acf093c
source-git-commit: 6ad556e3b7bf15f1d6ff522307ff232b8fd947d3
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 6%

---

# API-Vorgänge für Veröffentlichungsziele-Endpunkte {#publish-destination}

>[!IMPORTANT]
>
>**API-Endpunkt**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

Auf dieser Seite werden alle API-Vorgänge aufgelistet und beschrieben, die Sie mit dem `/authoring/destinations/publish` API-Endpunkt.

Nachdem Sie Ihr Ziel konfiguriert und getestet haben, können Sie es zur Überprüfung und Veröffentlichung an Adobe senden.

Verwenden Sie den API-Endpunkt für Veröffentlichungsziele, um eine Veröffentlichungsanforderung zu senden, wenn:

* Als Destination SDK-Partner möchten Sie Ihr produktives Ziel in allen Experience Platform-Unternehmen für alle Experience Platform-Kunden zur Verfügung stellen.
* Sie möchten Ihr benutzerdefiniertes Ziel in Ihrer eigenen Experience Platform-Organisation für alle Sandboxes verfügbar machen.

## Erste Schritte mit API-Vorgängen für die Zielveröffentlichung {#get-started}

Bevor Sie fortfahren, lesen Sie bitte die [Erste Schritte](./getting-started.md) für wichtige Informationen, die Sie benötigen, um die API erfolgreich aufrufen zu können, einschließlich Informationen zum Abrufen der erforderlichen Authoring-Berechtigung für Ziele und der erforderlichen Kopfzeilen.

## Senden einer Zielkonfiguration zur Veröffentlichung {#create}

Sie können eine Zielkonfiguration zur Veröffentlichung senden, indem Sie eine POST-Anfrage an die `/authoring/destinations/publish` -Endpunkt.

**API-Format**

```http
POST /authoring/destinations/publish
```

**Anfrage**

Mit der folgenden Anfrage wird ein Ziel zur Veröffentlichung in allen Organisationen gesendet, die von den in der Payload bereitgestellten Parametern konfiguriert wurden. Die nachstehende Payload enthält alle Parameter, die vom `/authoring/destinations/publish` -Endpunkt.

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
   "destinationAccess":"LIMITED",
   "allowedOrgs":[
      "xyz@AdobeOrg",
      "lmn@AdobeOrg"
   ]
}
```

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `destinationId` | Zeichenfolge | Die Ziel-ID der Zielkonfiguration, die Sie zur Veröffentlichung übermitteln. Rufen Sie die Ziel-ID einer Zielkonfiguration ab, indem Sie die [API-Referenz zur Zielkonfiguration](./destination-configuration-api.md#retrieve-list). |
| `destinationAccess` | Zeichenfolge | `ALL` oder `LIMITED`. Geben Sie an, ob Ihr Ziel im Katalog für alle Experience Platform-Kunden oder nur für bestimmte Unternehmen angezeigt werden soll. <br> **Hinweis**: Wenn Sie `LIMITED`festgelegt ist, wird das Ziel nur für Ihre Experience Platform-Organisation veröffentlicht. Wenn Sie das Ziel für Kundentestzwecke in einer Untergruppe von Experience Platform-Organisationen veröffentlichen möchten, wenden Sie sich an den Support von Adobe. |
| `allowedOrgs` | Zeichenfolge | Wenn Sie `"destinationAccess":"LIMITED"`, geben Sie die Organisationen der Experience Platform an, für die das Ziel verfügbar sein soll. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 201 mit Details zu Ihrer Ziel-Veröffentlichungsanforderung zurück.

## Veröffentlichungsanforderungen des Ziels auflisten {#retrieve-list}

Sie können eine Liste aller Ziele abrufen, die zur Veröffentlichung für Ihre IMS-Organisation übermittelt wurden, indem Sie eine GET-Anfrage an die `/authoring/destinations/publish` -Endpunkt.

**API-Format**

```http
GET /authoring/destinations/publish
```

**Anfrage**

Mit der folgenden Anfrage wird die Liste der Ziele abgerufen, die zur Veröffentlichung gesendet wurden und auf die Sie Zugriff haben, basierend auf der IMS-Organisation und der Sandbox-Konfiguration.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Die folgende Antwort gibt den HTTP-Status 200 mit einer Liste von Zielen zurück, die zur Veröffentlichung gesendet wurden und auf die Sie Zugriff haben. Diese Liste basiert auf der von Ihnen verwendeten IMS-Organisations-ID und dem Sandbox-Namen der IMS-Organisation. One `configId` entspricht der Veröffentlichungsanforderung für ein Ziel.

```json
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "publishDetailsList":[
      {
         "configId":"string",
         "allowedOrgs":[
            "xyz@AdobeOrg",
            "lmn@AdobeOrg"
         ],
         "status":"TEST",
         "publishedDate":"1630617746"
      }
   ]
}
```

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `destinationId` | Zeichenfolge | Die Ziel-ID der Zielkonfiguration, die Sie zur Veröffentlichung gesendet haben. |
| `publishDetailsList.configId` | Zeichenfolge | Die eindeutige ID der Ziel-Veröffentlichungsanforderung für Ihr gesendetes Ziel. |
| `publishDetailsList.allowedOrgs` | Zeichenfolge | Gibt die Organisationen der Experience Platform zurück, für die das Ziel verfügbar sein soll. |
| `publishDetailsList.status` | Zeichenfolge | Der Status Ihrer Ziel-Veröffentlichungsanforderung. Mögliche Werte `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`. |
| `publishDetailsList.publishedDate` | Zeichenfolge | Das Datum, an dem das Ziel zur Veröffentlichung gesendet wurde, in Epochenzeit. |

{style=&quot;table-layout:auto&quot;}

## Vorhandene Ziel-Veröffentlichungsanforderung aktualisieren {#update}

Sie können die zulässigen Organisationen in einer bestehenden Ziel-Veröffentlichungsanforderung aktualisieren, indem Sie eine PUT-Anfrage an die `/authoring/destinations/publish` -Endpunkt und geben die ID des Ziels an, für das Sie die zulässigen Organisationen aktualisieren möchten. Geben Sie im Text des Aufrufs die aktualisierten zulässigen Organisationen an.

**API-Format**

```http
PUT /authoring/destinations/publish/{DESTINATION_ID}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{DESTINATION_ID}` | Die ID des Ziels, für das Sie die Veröffentlichungsanforderung aktualisieren möchten. |

**Anfrage**

Mit der folgenden Anfrage wird eine vorhandene Ziel-Veröffentlichungsanforderung aktualisiert, die durch die in der Payload bereitgestellten Parameter konfiguriert wird. Im folgenden Beispielaufruf aktualisieren wir die zulässigen Organisationen.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destinations/publish/1230e5e4-4ab8-4655-ae1e-a6296b30f2ec \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "destinationAccess":"LIMITED",
   "allowedOrgs":[
      "abc@AdobeOrg",
      "def@AdobeOrg"
   ]
}
```

## Abrufen des Status einer bestimmten Ziel-Veröffentlichungsanforderung {#get}

Sie können detaillierte Informationen zu einer bestimmten Ziel-Veröffentlichungsanforderung abrufen, indem Sie eine GET-Anfrage an die `/authoring/destinations/publish` -Endpunkt und die ID des Ziels angeben, für das Sie den Veröffentlichungsstatus abrufen möchten.

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

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit detaillierten Informationen zur angegebenen Ziel-Veröffentlichungsanforderung zurück.

```json
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "publishDetailsList":[
      {
         "configId":"string",
         "allowedOrgs":[
            "xyz@AdobeOrg",
            "lmn@AdobeOrg"
         ],
         "status":"TEST",
         "publishedDate":"string"
      }
   ]
}
```

## Umgang mit API-Fehlern

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen der Experience Platform API-Fehlermeldung. Siehe [API-Statuscodes](../../landing/troubleshooting.md#api-status-codes) und [Fehler in der Anfragekopfzeile](../../landing/troubleshooting.md#request-header-errors) im Handbuch zur Fehlerbehebung bei Platform.

## Nächste Schritte

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie eine Veröffentlichungsanforderung für Ihr Ziel senden können. Das Adobe Experience Platform-Team prüft Ihre Veröffentlichungsanforderung und setzt sich innerhalb von fünf Werktagen mit Ihnen in Verbindung.
