---
title: Content API-Endpunkt
description: Erfahren Sie, wie Sie Ihre Zugriffsdaten mit der Privacy Service-API abrufen.
role: Developer
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 8bd4bd293b68d01e072c1c0a776080379692c5ee
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 6%

---

# Content-Endpunkt

>[!IMPORTANT]
>
>Die `/content` -Endpunkt befindet sich derzeit in der Beta-Phase und Ihre Organisation hat möglicherweise noch keinen Zugriff darauf. Die Funktionalität und Dokumentation können sich ändern.

<!-- Q) Should this be called 'access information' or 'customer content'? -->

Genießen Sie mehr Sicherheit beim Abrufen von &quot;Zugriffsinformationen&quot;(die Informationen, die ein Datenschutzsubjekt zu Recht anfordern kann, auf sie zuzugreifen). Die Download-URL, die in der Antwort auf eine `/jobs/{JOB_ID}` GET-Anfrage verweist jetzt auf einen Adobe-Dienstendpunkt. Anschließend können Sie eine GET-Anfrage an `/jobs/:JOB_ID/content` , um Ihre Kundendaten im JSON-Format zurückzugeben. Diese Zugriffsmethode implementiert mehrere Ebenen der Authentifizierung und Zugriffskontrolle, um die Sicherheit zu erhöhen.

Bevor Sie dieses Handbuch verwenden, lesen Sie bitte den Abschnitt [Erste Schritte](./getting-started.md) Informationen zu den erforderlichen Authentifizierungskopfzeilen finden Sie im folgenden Beispiel-API-Aufruf.

>[!TIP]
>
>Wenn Sie die Auftrags-ID für die benötigten Zugriffsinformationen derzeit nicht kennen, rufen Sie die `/jobs`-Endpunkt und verwenden Sie zusätzliche Abfrageparameter, um die Ergebnisse zu filtern. Eine vollständige Liste der verfügbaren Abfrageparameter finden Sie im Abschnitt [Endleitfaden für Datenschutzaufträge](./privacy-jobs.md).

## Abrufen von Datenschutzauftragsinformationen

Um Informationen zu einem bestimmten Auftrag abzurufen, z. B. dessen aktuellen Verarbeitungsstatus, schließen Sie die `jobId` im Pfad einer GET-Anfrage an die `/jobs` -Endpunkt.

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
>Datenschutzaufträge müssen `complete` -Status, der `downloadUrl`.

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
    "downloadUrl":"https://platform-stage.adobe.io/data/core/privacy/jobs/dbe3a6a6-f8e6-11ee-a365-8d1d6df81cc5/content",
    "regulation":"gdpr"
}
```

| Eigenschaft | Beschreibung |
|----------------------|---------------------------------------------------------------------------------------------------------------|
| `jobId` | Eine eindeutige Kennung für den Datenschutzauftrag. |
| `requestId` | Eine eindeutige Kennung für die spezifische Anfrage an den Privacy Service. |
| `userKey` | `userKey` ist die `key` -Wert, den Sie beim Senden der Datenschutzanfrage angegeben haben. Die `key` -Wert ist Ihre Möglichkeit, eine für Sie sinnvolle Kennung für das Datensubjekt bereitzustellen. Es handelt sich normalerweise um eine eindeutige Kennung, die Ihr System zur Verfolgung dieser betroffenen Person erstellt hat. TIPP: Sie können alle aktiven Datenschutzaufträge auflisten und Ihre `key` zu jedem Auftrag. |
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
| `downloadURL` | Dieses Attribut stellt einen Endpunkt bereit, der 60 Tage nach Abschluss des Auftrags aufgerufen werden kann. Der Status des Auftrags muss `complete` und `action` muss `access`. Andernfalls fehlt dieses Feld. |
| `regulation` | Der Rechtsrahmen, unter dem die Datenschutzanfrage verarbeitet wird, z. B. `gdpr`, `ccpa`, `lgpd_bra`, `pdpa_tha`usw. |

{style="table-layout:auto"}

## Abrufen von Kundenzugriffsinformationen {#retrieve-access-data}

Um die auf die Abfrage Ihres Datensubjekts bezogenen &quot;Zugriffsinformationen&quot;abzurufen, wenden Sie eine GET-Anfrage an die `/jobs/{JOB_ID}/content` -Endpunkt. Die Antwort ist eine ZIP-Datei (*.zip), die einen Ordner mit Unterordnern für jedes Produkt enthält, das Daten zum Datensubjekt enthält.

>[!TIP]
>
>Sie benötigen eine bestimmte Auftrags-ID, um diese Anfrage ausführen zu können. Wenn Sie die spezifische Auftrags-ID abrufen müssen, stellen Sie zunächst eine GET-Anfrage an die `/jobs` -Endpunkt und verwenden Sie zusätzliche Abfrageparameter, um die Ergebnisse zu filtern. Detaillierte Informationen einschließlich der zulässigen Abfrageparameter finden Sie im Abschnitt [Endleitfaden für Datenschutzaufträge](./privacy-jobs.md).

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

