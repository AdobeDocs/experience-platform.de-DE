---
title: Content API-Endpunkt
description: Erfahren Sie, wie Sie Ihre Zugriffsdaten mit der Privacy Service-API abrufen.
role: Developer
exl-id: b3b7ea0f-957d-4e51-bf92-121e9ae795f5
source-git-commit: ac54398ae8e9e06ea3581baf867ab1cf650042a2
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 5%

---

# Content-Endpunkt

Verwenden Sie den `/content`-Endpunkt zum sicheren Abrufen *Zugriffsinformationen* (die Informationen, auf die eine betroffene Person zu Recht zugreifen kann) für Ihre Kunden. Die in der Antwort auf eine `/jobs/{JOB_ID}` GET-Anfrage angegebene Download-URL verweist auf einen Adobe Service-Endpunkt. Sie können dann eine GET-Anfrage an `/jobs/:JOB_ID/content` stellen, um Ihre Kundendaten im JSON-Format zurückzugeben. Diese Zugriffsmethode implementiert mehrere Authentifizierungs- und Zugriffssteuerungsebenen, um die Sicherheit zu erhöhen.

Bevor Sie dieses Handbuch verwenden, lesen Sie das [Erste Schritte](./getting-started.md) um Informationen zu den erforderlichen Authentifizierungskopfzeilen zu erhalten, die im folgenden Beispiel-API-Aufruf dargestellt werden.

>[!TIP]
>
>Wenn Sie die Auftrags-ID für die benötigten Zugriffsinformationen derzeit nicht kennen, rufen Sie den `/jobs`-Endpunkt auf und verwenden Sie zusätzliche Abfrageparameter, um die Ergebnisse zu filtern. Eine vollständige Liste der verfügbaren Abfrageparameter finden Sie im [Handbuch zu Datenschutzaufträgen](./privacy-jobs.md).

## Abrufen von Informationen zu Datenschutzaufträgen

Um Informationen über einen bestimmten Auftrag abzurufen, z. B. seinen aktuellen Verarbeitungsstatus, fügen Sie die `jobId` dieses Auftrags in den Pfad einer GET-Anfrage an den `/jobs`-Endpunkt ein.

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
>Datenschutzaufträge müssen den Status `complete` aufweisen, um die `downloadUrl` zu enthalten.

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
| `userKey` | `userKey` ist der `key` Wert, den Sie beim Senden der Datenschutzanfrage angegeben haben. Der `key` ist Ihre Möglichkeit, eine für Sie sinnvolle Kennung für die betroffene Person anzugeben. Es handelt sich normalerweise um eine eindeutige Kennung, die Ihr System zum Tracking dieser betroffenen Person erstellt hat. TIPP: Sie können alle aktiven Datenschutzaufträge auflisten und Ihre `key` mit den einzelnen Aufträgen vergleichen. |
| `action` | Der Typ der angeforderten Aktion. Die akzeptierten Werte sind `access` und `delete`. |
| `status` | Der aktuelle Status des Datenschutzauftrags. |
| `submittedBy` | Die E-Mail-Adresse der Person, die den Datenschutzauftrag gesendet hat. |
| `createdDate` | Datum und Uhrzeit der Erstellung des Datenschutzauftrags. |
| `lastModifiedDate` | Datum und Uhrzeit der letzten Änderung des Datenschutzauftrags. |
| `userIds` | Ein Array, das Benutzerkennung und zugehörige Informationen enthält. |
| `userIds.namespace` | Der für die Benutzerkennung verwendete Namespace. |
| `userIds.value` | Der tatsächliche Wert der Benutzerkennung. |
| `userIds.type` | Der Typ der Kennung (z. B. `standard` oder `custom`). |
| `userIds.namespaceId` | Eine Kennung für den Namespace, der zum Kategorisieren und Verwalten von Benutzeridentitäten verwendet wird. |
| `userIds.isDeletedClientSide` | Ein boolescher Wert, der angibt, ob die Kennung Client-seitig gelöscht wurde. |
| `productResponses` | Ein Array, das Antworten aus verschiedenen Produkten oder Services enthält, die sich auf den Datenschutzauftrag beziehen. |
| `productResponses.product` | Der Name des Produkts oder der Dienstleistung, mit dem bzw. der Informationen über die betroffene Person erfasst wurden. |
| `productResponses.retryCount` | Die Häufigkeit, mit der die Anfrage erneut versucht wurde. |
| `productResponses.processedDate` | Datum und Uhrzeit der Verarbeitung der Produktantwort. |
| `productResponses.productStatusResponse` | Ein Objekt, das den Status der Produktantwort enthält. |
| `productResponses.productStatusResponse.status` | Der Status der Produktantwort. |
| `downloadURL` | Dieses Attribut stellt einen Endpunkt bereit, der 60 Tage nach Abschluss des Auftrags aufzurufen ist. Der Status des Auftrags muss `complete` und der `action` muss `access` sein. Andernfalls fehlt dieses Feld. |
| `regulation` | Der rechtliche Rahmen, in dem die Datenschutzanfrage verarbeitet wird, z. B. `gdpr`, `ccpa`, `lgpd_bra`, `pdpa_tha` usw. |

{style="table-layout:auto"}

## Abrufen von Kundenzugriffsinformationen {#retrieve-access-data}

Um die „Zugriffsinformationen“ zu erhalten, die als Antwort auf die Abfrage Ihrer betroffenen Person erstellt werden, stellen Sie eine GET-Anfrage an den `/jobs/{JOB_ID}/content`-Endpunkt. Die Antwort ist eine ZIP-Datei (*.zip), die einen Ordner mit Unterordnern für jedes Produkt enthält, das Daten über die betroffene Person enthält.

>[!TIP]
>
>Sie benötigen eine bestimmte Auftrags-ID, um diese Anfrage zu stellen. Wenn Sie die spezifische Auftrags-ID abrufen müssen, stellen Sie zunächst eine GET-Anfrage an den `/jobs`-Endpunkt und verwenden Sie zusätzliche Abfrageparameter, um die Ergebnisse zu filtern. Detaillierte Informationen einschließlich der zulässigen Abfrageparameter finden Sie im [Handbuch zu Datenschutzaufträgen](./privacy-jobs.md).

**API-Format**

```http
GET /jobs/{JOB_ID}/content
```

**Anfrage**

Die folgende Anfrage gibt „Zugriffsinformationen“ für die in der Anfrage angegebene Vorgangs-ID zurück.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/32d429b1-f7f4-11ee-a365-574bcf5a525d/content \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'Accept: application/json`
```

**Antwort**

Die Antwort ist eine ZIP-Datei (*.zip). Die Informationen werden normalerweise im JSON-Format zurückgegeben, dies kann jedoch nicht garantiert werden. Die extrahierten Daten können in jedem beliebigen Format zurückgegeben werden.

