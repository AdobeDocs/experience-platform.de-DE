---
description: Auf dieser Seite wird der API-Aufruf veranschaulicht, mit dem Details zu einer Zielveröffentlichungsanfrage über Adobe Experience Platform Destination SDK abgerufen werden.
title: Abrufen einer Zielveröffentlichungsanfrage
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: ht
source-wordcount: '834'
ht-degree: 100%

---


# Abrufen einer Zielveröffentlichungsanfrage

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

## Auflisten der Zielveröffentlichungsanfragen {#retrieve-list}

Sie können eine Liste aller für Ihre IMS-Organisation zur Veröffentlichung übermittelten Ziele abrufen, indem Sie eine GET-Anfrage an den Endpunkt `/authoring/destinations/publish` stellen.

**API-Format**

Verwenden Sie das folgende API-Format, um alle Veröffentlichungsanfragen für Ihr Konto abzurufen.

```http
GET /authoring/destinations/publish
```

Verwenden Sie das folgende API-Format, um eine bestimmte Veröffentlichungsanfrage abzurufen, die durch den Parameter `{DESTINATION_ID}` bestimmt wird.

```http
GET /authoring/destinations/publish/{DESTINATION_ID}
```

**Anfrage**

Die folgenden beiden Anfragen rufen alle Veröffentlichungsanfragen für Ihre IMS-Organisation ab oder eine bestimmte Veröffentlichungsanfrage, je nachdem, ob Sie den Parameter `DESTINATION_ID` in der Anfrage übergeben.

Wählen Sie die einzelnen Registerkarten unten aus, um die entsprechende Payload anzuzeigen.

>[!BEGINTABS]

>[!TAB Alle Veröffentlichungsanfragen abrufen]

+++Anfrage

Die folgende Anfrage ruft auf der Grundlage der [!DNL IMS Org ID] und der Sandbox-Konfiguration die Liste der Veröffentlichungsanfragen ab, die Sie übermittelt haben.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Antwort

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit einer Liste von Zielen zurückgegeben, die zur Veröffentlichung übermittelt wurden und auf die Sie Zugriff haben. Diese Liste basiert auf der von Ihnen verwendeten IMS-Organisations-ID und dem Sandbox-Namen der IMS-Organisation. Eine `configId` entspricht der Veröffentlichungsanfrage für jeweils ein Ziel.

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

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `destinationId` | Zeichenfolge | Die Ziel-ID der Zielkonfiguration, die Sie zur Veröffentlichung übermittelt haben. |
| `publishDetailsList.configId` | Zeichenfolge | Die eindeutige ID der Zielveröffentlichungsanfrage für Ihr übermitteltes Ziel. |
| `publishDetailsList.allowedOrgs` | Zeichenfolge | Gibt die Experience Platform-Organisationen zurück, für die das Ziel verfügbar ist. <br> <ul><li> Für `"destinationType": "PUBLIC"` gibt dieser Parameter `"*"` zurück, was bedeutet, dass das Ziel für alle Experience Platform-Organisationen verfügbar ist.</li><li> Für `"destinationType": "DEV"` gibt dieser Parameter die Organisations-ID der Organisation zurück, die Sie zum Erstellen und Testen des Ziels verwendet haben.</li></ul> |
| `publishDetailsList.status` | Zeichenfolge | Der Status Ihrer Anfrage zum Ziel der Veröffentlichung. Mögliche Werte sind `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`. Ziele mit dem Wert `PUBLISHED` sind live und können von Experience Platform-Kundinnen und -Kunden verwendet werden. |
| `publishDetailsList.destinationType` | Zeichenfolge | Der Typ des Ziels. Werte können `DEV` und `PUBLIC` sein. `DEV` entspricht dem Ziel in Ihrer Experience Platform-Organisation. `PUBLIC` entspricht dem Ziel, das Sie zur Veröffentlichung übermittelt haben. Stellen Sie sich diese beiden Optionen in Git-Begriffen vor, wobei die Version `DEV` für Ihre lokale Authoring-Verzweigung steht und die Version `PUBLIC` für den Remote-Hauptzweig. |
| `publishDetailsList.publishedDate` | Zeichenfolge | Das Datum, an dem das Ziel zur Veröffentlichung gesendet wurde, angegeben in Epochenzeit. |

{style="table-layout:auto"}

+++

>[!TAB Bestimmte Veröffentlichungsanfrage abrufen]

+++Anfrage

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish/{DESTINATION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{DESTINATION_ID}` | Die ID des Ziels, für das Sie den Veröffentlichungsstatus abrufen möchten. |

+++

+++Antwort

Wenn Sie eine `DESTINATION_ID` im API-Aufruf übergeben haben, gibt die Antwort den HTTP-Status 200 mit detaillierten Informationen zur angegebenen Ziel-Veröffentlichungsanfrage zurück.

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
| `publishDetailsList.allowedOrgs` | Zeichenfolge | Gibt die Experience Platform-Organisationen zurück, für die das Ziel verfügbar ist. <br> <ul><li> Für `"destinationType": "PUBLIC"` gibt dieser Parameter `"*"` zurück, was bedeutet, dass das Ziel für alle Experience Platform-Organisationen verfügbar ist.</li><li> Für `"destinationType": "DEV"` gibt dieser Parameter die Organisations-ID der Organisation zurück, die Sie zum Erstellen und Testen des Ziels verwendet haben.</li></ul> |
| `publishDetailsList.status` | Zeichenfolge | Der Status Ihrer Anfrage zum Ziel der Veröffentlichung. Mögliche Werte sind `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`. Ziele mit dem Wert `PUBLISHED` sind live und können von Experience Platform-Kundinnen und -Kunden verwendet werden. |
| `publishDetailsList.destinationType` | Zeichenfolge | Der Typ des Ziels. Werte können `DEV` und `PUBLIC` sein. `DEV` entspricht dem Ziel in Ihrer Experience Platform-Organisation. `PUBLIC` entspricht dem Ziel, das Sie zur Veröffentlichung übermittelt haben. Stellen Sie sich diese beiden Optionen in Git-Begriffen vor, wobei die Version `DEV` für Ihre lokale Authoring-Verzweigung steht und die Version `PUBLIC` für den Remote-Hauptzweig. |
| `publishDetailsList.publishedDate` | Zeichenfolge | Das Datum, an dem das Ziel zur Veröffentlichung gesendet wurde, angegeben in Epochenzeit. |

{style="table-layout:auto"}

+++

>[!ENDTABS]

## Umgang mit API-Fehlern

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status-Codes](../../../landing/troubleshooting.md#api-status-codes) und [Fehler im Anfrage-Header](../../../landing/troubleshooting.md#request-header-errors) in der Anleitung zur Fehlerbehebung für Platform.