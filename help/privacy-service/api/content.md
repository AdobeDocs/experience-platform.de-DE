---
title: Content API-Endpunkt
description: Erfahren Sie, wie Sie Ihre Zugriffsdaten mit der Privacy Service-API abrufen.
role: Developer
badgePrivateBeta: label="Private Beta" type="Informative"
exl-id: b3b7ea0f-957d-4e51-bf92-121e9ae795f5
source-git-commit: e3a453ad166fe244b82bd1f90e669579fcf09d17
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 6%

---

# Content-Endpunkt

>[!IMPORTANT]
>
>Der Endpunkt `/content` befindet sich derzeit in der Beta-Phase und Ihre Organisation hat möglicherweise noch keinen Zugriff darauf. Die Funktionalität und Dokumentation können sich ändern.

Verwenden Sie den `/content` -Endpunkt, um *Zugriffsinformationen* sicher abzurufen (die Informationen, auf die ein Datenschutzsubjekt berechtigterweise Zugriff anfordern kann). Die in der Antwort auf eine `/jobs/{JOB_ID}` -GET-Anfrage angegebene Download-URL verweist auf einen Adobe-Dienstendpunkt. Anschließend können Sie eine GET-Anfrage an `/jobs/:JOB_ID/content` senden, um Ihre Kundendaten im JSON-Format zurückzugeben. Diese Zugriffsmethode implementiert mehrere Ebenen der Authentifizierung und Zugriffskontrolle, um die Sicherheit zu erhöhen.

Bevor Sie dieses Handbuch verwenden, lesen Sie bitte das Erste-Schritte-Handbuch ](./getting-started.md) , um Informationen zu den erforderlichen Authentifizierungskopfzeilen zu erhalten, das im folgenden Beispiel-API-Aufruf vorgestellt wird.[

>[!TIP]
>
>Wenn Sie die Auftrags-ID für die benötigten Zugriffsinformationen derzeit nicht kennen, rufen Sie den Endpunkt `/jobs` auf und verwenden Sie zusätzliche Abfrageparameter, um die Ergebnisse zu filtern. Eine vollständige Liste der verfügbaren Abfrageparameter finden Sie im [Endpunkthandbuch zu Datenschutzaufträgen](./privacy-jobs.md).

## Abrufen von Datenschutzauftragsinformationen

Um Informationen zu einem bestimmten Auftrag abzurufen, z. B. dessen aktuellen Verarbeitungsstatus, fügen Sie den Wert &quot;`jobId`&quot;des Auftrags in den Pfad einer GET-Anfrage zum `/jobs` -Endpunkt ein.

**API-Format**

```http
GET /jobs/{JOB_ID}
```

**Anfrage**

Die folgende Anfrage ruft die Details des Auftrags ab, dessen `jobId` im Anfragepfad angegeben ist.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/dbe3a6a6-f8e6-11ee-a365-8d1d6df81cc5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details des angegebenen Auftrags zurück.

>[!NOTE]
>
>Datenschutzaufträge müssen den Status `complete` aufweisen, um den Wert `downloadUrl` enthalten zu können.

```json
{
    "jobId":"dbe3a6a6-f8e6-11ee-a365-8d1d6df81cc5",
    "requestId":"17129380910360540RX-753",
    "userKey":"1234",
    "action":"access",
    "status":"complete",
    "submittedBy":"jsnow@adobe.com",
    "createdDate":"04/12/2024 04:08 PM GMT",
    "lastModifiedDate":"04/12/2024 04:08 PM GMT",
    "userIds":[{
        "namespace":"ECID",
        "value":"1234",
        "type":"standard",
        "namespaceId":4,
        "isDeletedClientSide":false
        }],
    "productResponses":[{
        "product":"Identity",
        "retryCount":0,
        "processedDate":"04/12/2024 04:08 PM GMT",
        "productStatusResponse":{"status":"submitted"
        }}],
    "downloadUrl":"https://platform.adobe.io/data/core/privacy/jobs/dbe3a6a6-f8e6-11ee-a365-8d1d6df81cc5/content",
    "regulation":"gdpr"
}
```

| Eigenschaft | Beschreibung |
|----------------------|---------------------------------------------------------------------------------------------------------------|
| `jobId` | Eine eindeutige Kennung für den Datenschutzauftrag. |
| `requestId` | Eine eindeutige Kennung für die spezifische Anfrage an den Privacy Service. |
| `userKey` | `userKey` ist der `key` -Wert, den Sie beim Senden der Datenschutzanfrage angegeben haben. Der Wert `key` ist Ihre Möglichkeit, eine für Sie sinnvolle Kennung für das Datensubjekt bereitzustellen. Es handelt sich normalerweise um eine eindeutige Kennung, die Ihr System zur Verfolgung dieser betroffenen Person erstellt hat. TIPP: Sie können alle aktiven Datenschutzaufträge auflisten und Ihre `key` mit jedem Auftrag vergleichen. |
| `action` | Die Art der angeforderten Aktion. Die zulässigen Werte sind `access` und `delete`. |
| `status` | Der aktuelle Status des Datenschutzauftrags. |
| `submittedBy` | Die E-Mail-Adresse der Person, die den Datenschutzauftrag gesendet hat. |
| `createdDate` | Datum und Uhrzeit der Erstellung des Datenschutzauftrags. |
| `lastModifiedDate` | Datum und Uhrzeit der letzten Änderung des Datenschutzauftrags. |
| `userIds` | Ein Array mit Benutzer-IDs und zugehörigen Informationen. |
| `userIds.namespace` | Der für die Benutzer-ID verwendete Namespace. |
| `userIds.value` | Der tatsächliche Wert der Benutzer-ID. |
| `userIds.type` | Der Typ der Kennung (z. B. `standard` oder `custom`). |
| `userIds.namespaceId` | Eine Kennung für den Namespace, der zur Kategorisierung und Verwaltung von Benutzeridentitäten verwendet wird. |
| `userIds.isDeletedClientSide` | Ein boolescher Wert, der angibt, ob die Kennung clientseitig gelöscht wurde. |
| `productResponses` | Ein Array mit Antworten aus verschiedenen Produkten oder Diensten, die sich auf den Datenschutzauftrag beziehen. |
| `productResponses.product` | Der Name des Produkts oder der Dienstleistung, mit dem bzw. der Informationen über die betroffene Person erfasst wurden. |
| `productResponses.retryCount` | Die Häufigkeit, mit der die Anfrage wiederholt wurde. |
| `productResponses.processedDate` | Datum und Uhrzeit der Verarbeitung der Produktantwort. |
| `productResponses.productStatusResponse` | Ein Objekt, das den Status der Produktantwort enthält. |
| `productResponses.productStatusResponse.status` | Der Status der Produktantwort. |
| `downloadURL` | Dieses Attribut stellt einen Endpunkt bereit, der 60 Tage nach Abschluss des Auftrags aufgerufen werden kann. Der Status des Auftrags muss `complete` und der `action` muss `access` sein. Andernfalls fehlt dieses Feld. |
| `regulation` | Das regulatorische Framework, unter dem die Datenschutzanfrage verarbeitet wird, z. B. `gdpr`, `ccpa`, `lgpd_bra`, `pdpa_tha` usw. |

{style="table-layout:auto"}

## Abrufen von Kundenzugriffsinformationen {#retrieve-access-data}

Um die &quot;Zugriffsinformationen&quot;abzurufen, die als Antwort auf die Abfrage des Datensubjekts erstellt wurden, stellen Sie eine GET-Anfrage an den `/jobs/{JOB_ID}/content` -Endpunkt. Die Antwort ist eine ZIP-Datei (*.zip), die einen Ordner mit Unterordnern für jedes Produkt enthält, das Daten zum Datensubjekt enthält.

>[!TIP]
>
>Sie benötigen eine bestimmte Auftrags-ID, um diese Anfrage ausführen zu können. Wenn Sie die spezifische Auftrags-ID abrufen müssen, stellen Sie zunächst eine GET-Anfrage an den `/jobs` -Endpunkt und verwenden Sie zusätzliche Abfrageparameter, um die Ergebnisse zu filtern. Detaillierte Informationen einschließlich der zulässigen Abfrageparameter finden Sie im [Endpoint-Handbuch zu Datenschutzaufträgen](./privacy-jobs.md).

**API-Format**

```http
GET /jobs/{JOB_ID}/content
```

**Anfrage**

Die folgende Anfrage gibt &quot;Zugriffsinformationen&quot;für die in der Anfrage angegebene Auftrags-ID zurück.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/32d429b1-f7f4-11ee-a365-574bcf5a525d/content \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'Accept: application/json`
```

**Antwort**

Die Antwort ist eine ZIP-Datei (*.zip). Die Informationen werden normalerweise im JSON-Format zurückgegeben, obwohl dies nicht garantiert werden kann. Extrahierte Daten können in jedem beliebigen Format zurückgegeben werden.

