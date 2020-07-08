---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Segment erstellen
topic: tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1328'
ht-degree: 2%

---


# Segment erstellen

Dieses Dokument bietet eine Anleitung zum Entwickeln, Testen, Anzeigen einer Vorschau und Speichern einer Segmentdefinition mithilfe der [Segmentierungs-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml).

Informationen zum Erstellen von Segmenten mithilfe der Benutzeroberfläche finden Sie im Handbuch [Segmentaufbau](../ui/overview.md).

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der verschiedenen Adobe Experience Platformen, die beim Erstellen von Audiencen-Segmenten erforderlich sind. Bevor Sie mit diesem Lernprogramm beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [Echtzeit-Profil](../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
- [Adobe Experience Platform Segmentation Service](../home.md): Ermöglicht Ihnen das Erstellen von Segmenten für Audiencen aus Echtzeitdaten zum Profil von Kunden.
- [Erlebnisdatenmodell (XDM)](../../xdm/home.md): Das standardisierte Framework, mit dem Platform Kundenerlebnisdaten organisiert.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die Platformen-APIs erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Lernprogramm finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt [zum Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung bei Experience Platformen.

### Werte für erforderliche Kopfzeilen sammeln

Um Platformen-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungslehrgang](../../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungtutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform API-Aufrufen bereit, wie unten dargestellt:

- Genehmigung: Träger `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in der Experience Platform werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an Platform-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxen in der Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Für alle Anforderungen mit einer Payload (POST, PUT, PATCH) ist ein zusätzlicher Header erforderlich:

- Content-Type: application/json

## Entwickeln einer Segmentdefinition

Der erste Schritt bei der Segmentierung besteht darin, ein Segment zu definieren, das in einem Konstrukt namens **Segmentdefinition** dargestellt wird. Eine Segmentdefinition ist ein Objekt, das eine in Profil Abfrage Language (PQL) geschriebene Abfrage kapselt. Dieses Objekt wird auch als **PQL-Vorhersage** bezeichnet. PQL-Prädikate definieren die Segmentregeln basierend auf Bedingungen, die sich auf die Daten aus Datensatz oder Zeitreihen beziehen, die Sie dem Echtzeit-Kunden-Profil bereitstellen. Weitere Informationen zum Schreiben von PQL-Abfragen finden Sie im [PQL-Handbuch](../pql/overview.md) .

Sie können eine neue Segmentdefinition erstellen, indem Sie eine POST-Anforderung an den `/segment/definitions` Endpunkt in der Echtzeit-Client-Profil-API senden. Im folgenden Beispiel wird beschrieben, wie eine Definitionsanforderung formatiert wird, einschließlich der Informationen, die erforderlich sind, damit ein Segment erfolgreich definiert werden kann.

Segmentdefinitionen können auf zwei Arten bewertet werden: Batch-Segmentierung und Streaming-Segmentierung. Bei der Stapelsegmentierung werden Segmente auf der Grundlage eines vorgegebenen Zeitplans oder bei manueller Auslösung der Auswertung ausgewertet, während bei der Streaming-Segmentierung Segmente ausgewertet werden, sobald Daten in die Platform aufgenommen werden. In diesem Lernprogramm wird die **Stapelsegmentierung** verwendet. Weitere Informationen zur Streaming-Segmentierung finden Sie in der [Übersicht zur Streaming-Segmentierung](../api/streaming-segmentation.md).

**API-Format**

```http
POST /segment/definitions
```

**Anfrage**

Die folgende Anforderung erstellt eine neue Segmentdefinition für ein Schema namens &quot;MyProfile&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/definitions \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "My Sample Cart Abandons Segment Definition",
        "schema": {
            "name": "MyProfile",
        },
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "xEvent.metrics.commerce.abandons.value > 0",
        },
        "mergePolicyId": "mpid1",
        "description": "This Segment represents those users who have abandoned a cart"
    }'
```

| Eigenschaft | Beschreibung |
| --------- | ------------ | 
| `name` | **Erforderlich.** Ein eindeutiger Name, unter dem auf das Segment verwiesen wird. |
| `schema` | **Erforderlich.** Das Schema, das den Entitäten im Segment zugeordnet ist. Besteht aus einem `id` oder einem `name` Feld. |
| `expression` | **Erforderlich.** Eine Entität, die Feldinformationen zur Segmentdefinition enthält. |
| `expression.type` | Gibt den Ausdruck-Typ an. Derzeit wird nur &quot;PQL&quot;unterstützt. |
| `expression.format` | Gibt die Wertstruktur des Ausdrucks an. Derzeit wird folgendes Format unterstützt: <ul><li>`pql/text`: Eine Textdarstellung einer Segmentdefinition gemäß der veröffentlichten PQL-Grammatik.  Beispiel: `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Ein Ausdruck, der dem unter `expression.format`Angabe angegebenen Typ entspricht. |
| `mergePolicyId` | Der Bezeichner der Mergerichtlinie, die für die exportierten Daten verwendet wird. Weitere Informationen finden Sie im Dokument zur Konfiguration der [Zusammenführungsrichtlinie](../../profile/api/merge-policies.md). |
| `description` | Eine für Menschen lesbare Beschreibung der Definition. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der neu erstellten Segmentdefinition zurück, einschließlich der systemgenerierten schreibgeschützten Segmentdefinition, `id` die später in diesem Lernprogramm verwendet wird.

```json
{
    "id": "1234",
    "name": "My Sample Cart Abandons Segment Definition",
    "description": "This Segment represents those users who have abandoned a cart",
    "type": "PQL",
    "format": "pql/text",
    "expression": "xEvent.metrics.commerce.abandons.value > 0",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/core/ups/segment/definitions/1234"
        }
    }
}
```

## Schätzung und Vorschau einer Audience {#estimate-and-preview-an-audience}

Während Sie Ihre Segmentdefinition entwickeln, können Sie die Tools für Schätzung und Vorschau innerhalb des Echtzeit-Profils des Kunden verwenden, um Informationen auf der Ebene der Ansicht zu erhalten, um sicherzustellen, dass Sie die erwartete Audience isolieren. Schätzungen liefern statistische Informationen zu einer Segmentdefinition, wie zum Beispiel die projizierte Audience und das Konfidenzintervall. Vorschauen bieten paginierte Listen von qualifizierten Profilen für eine Segmentdefinition, mit denen Sie die Ergebnisse mit Ihren Erwartungen vergleichen können.

Durch die Schätzung und Vorschau Ihrer Audience können Sie Ihre PQL-Vorhersagen testen und optimieren, bis sie ein erwünschtes Ergebnis erzielen und dann in einer aktualisierten Segmentdefinition verwendet werden können.

Zur Vorschau oder Schätzung Ihres Segments sind zwei Schritte erforderlich:

1. [Erstellen eines Vorschau-Auftrags](#create-a-preview-job)
2. [Schätzung der Ansicht oder Vorschau](#view-an-estimate-or-preview) mithilfe der ID des Vorschau-Auftrags

### Erstellung von Schätzungen

Mithilfe von Datenmustern können Sie Segmente bewerten und die Anzahl der qualifizierten Profil schätzen. Jeden Morgen werden neue Daten in den Speicher geladen (zwischen 12AM-2AM PT, was 7-9AM UTC entspricht), und alle Abfragen der Segmentierung werden anhand der Musterdaten dieses Tages geschätzt. Daher werden alle neuen Felder, die hinzugefügt oder zusätzliche Daten gesammelt werden, am folgenden Tag in Schätzungen übernommen.

Die Stichprobengröße hängt von der Gesamtanzahl der Entitäten in Ihrem Profil-Store ab. Diese Stichprobengrößen sind in der folgenden Tabelle dargestellt:

| Entitäten im Profil Store | Stichprobengröße |
| ------------------------- | ----------- |
| Weniger als 1 Million | Vollständiger Datensatz |
| 1 bis 20 Mio. | 1 Mio. |
| Über 20 Mio. | 5 % des Gesamtbetrags |

Schätzungen laufen in der Regel über 10-15 Sekunden, beginnend mit einer groben Schätzung und einer Feinabstimmung, wenn mehr Datensätze gelesen werden.

### Erstellen eines Vorschau-Auftrags

Sie können einen neuen Auftrag für die Vorschau erstellen, indem Sie eine POST-Anforderung an den `/preview` Endpunkt senden.

**API-Format**

```http
POST /preview
```

**Anfrage**

Mit der folgenden Anforderung wird ein neuer Vorschau-Auftrag erstellt. Der Anforderungstext enthält die Segmentinformationen zur Abfrage.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/preview \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
        "predicateType": "pql/text",
        "predicateModel": "_xdm.context.profile",
        "graphType": "simple",
        "mergeStrategy": "simple"
    }'
```

| Eigenschaft | Beschreibung |
| --------- | ----------- |
| `predicateExpression` | Der PQL-Ausdruck, um die Daten Abfrage. |
| `predicateModel` | Der Name des XDM-Schemas, auf dem die Profil-Daten basieren. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details des neu erstellten Vorschau-Auftrags zurück, einschließlich der ID und des aktuellen Verarbeitungsstatus.

```json
{
   "state": "RUNNING",
   "previewQueryId": "4a45e853-ac91-4bb7-a426-150937b6af5c",
   "previewQueryStatus": "RUNNING",
   "previewId": "MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg",
   "previewExecutionId": 42
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `state` | Der aktuelle Status des Auftrags für die Vorschau. Es befindet sich im Status &quot;WIRD AUSGEFÜHRT&quot;bis die Verarbeitung abgeschlossen ist. An diesem Punkt wird es zu &quot;ERGEBNIS_READY&quot;oder &quot;FEHLGESCHLAGEN&quot;. |
| `previewId` | Die ID des Auftrags für die Vorschau, der für Nachschlagezwecke bei Ansicht einer Schätzung oder Vorschau verwendet wird, wie im folgenden Abschnitt beschrieben. |

### Ansicht einer Schätzung oder Vorschau

Schätzungs- und Vorschauen-Vorgänge werden asynchron ausgeführt, da unterschiedliche Abfragen unterschiedliche Zeiträume benötigen können. Nachdem eine Abfrage initiiert wurde, können Sie mit API-Aufrufen den aktuellen Status der Schätzung oder Vorschau abrufen (GET), während sie fortschreitet.

Mithilfe der Echtzeit-Client-Profil-API können Sie den aktuellen Status eines Vorschau-Auftrags anhand seiner ID suchen. Wenn der Status &quot;RESULT_READY&quot;lautet, können Sie die Ansichten durchführen. Je nachdem, ob Sie eine Schätzung oder eine Vorschau Ansicht haben möchten, verfügen alle über einen eigenen Endpunkt in der API. Beispiele für beide sind nachfolgend aufgeführt.

### Ansicht und Schätzung

**API-Format**

```http
GET /estimate/{PREVIEW_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{PREVIEW_ID}` | Die ID des Vorschau-Auftrags, der Ansicht werden soll. |

**Anfrage**

Mit der folgenden Anforderung wird eine Schätzung unter Verwendung des im vorherigen Schritt `previewId` erstellten abgerufen.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/estimate/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der Schätzung zurück.

```json
{
    "estimatedSize": 45,
    "state": "RESULT_READY",
    "profilesReadSoFar": 83834,
    "standardError": 0,
    "error": {
        "description": "",
        "traceback": ""
    },
    "profilesMatchedSoFar": 46,
    "totalRows": 82473,
    "confidenceInterval": "95%",
    "_links": {
        "preview": "https://platform.adobe.io/data/core/ups/preview?previewQueryId=f88bc056-ee48-40d5-9ddb-8865d7d6a0e0"
    }
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `state` | Der aktuelle Status des Auftrags für die Vorschau. Ist &quot;WIRD AUSGEFÜHRT&quot;bis die Verarbeitung abgeschlossen ist, und wird dann &quot;ERGEBNIS_BEREIT&quot;oder &quot;FEHLGESCHLAGEN&quot;. |
| `_links.preview` | Wenn der aktuelle Status des Vorschau-Auftrags &quot;RESULT_READY&quot;lautet, stellt dieses Attribut eine URL zur Ansicht der Schätzung bereit. |

### Ansicht einer Vorschau

**API-Format**

```http
GET /preview/{PREVIEW_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{PREVIEW_ID}` | Die ID des Vorschau-Auftrags, der Ansicht werden soll. |

**Anfrage**

Mit der folgenden Anforderung wird eine Vorschau mit dem im vorherigen Schritt `previewId` erstellten abgerufen.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/preview/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt Details zur Vorschau zurück.

```json
{
   "results": [{
         "XID_ADOBE-MARKETING-CLOUD-ID-1": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_ADOBE-MARKETING-CLOUD-ID-1",
            "endCustomerIds": {
               "XID_COOKIE_ID_1": {
                  "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE_ID_1"
               },
               "XID_PROFILE_ID_1": {
                  "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_PROFILE_ID_1"
               }
            }
         }
      },
      {
         "XID_COOKIE-ID-2": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE-ID-2",
            "endCustomerIds": {
               "XID_COOKIE_ID_2-1": {
                  "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE_ID_2-1"

               },
               "XID_PROFILE_ID_2": {
                  "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_PROFILE_ID_2"
               }
            }
         },
         "XID_ADOBE-MARKETING-CLOUD-ID-3": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_ADOBE-MARKETING-CLOUD-ID-1000"
         },
         "state": "RESULT_READY",
         "links": {
            "_self": "https://platform.adobe.io/data/core/ups/preview?expression=<expr-1>&limit=1000",
            "next": "",
            "prev": ""
         }
      }
   ],
   "page": {
      "offset": 0,
      "size": 3
   }
}
```

## Nächste Schritte

Nachdem Sie Ihre Segmentdefinition entwickelt, getestet und gespeichert haben, können Sie einen Segmentauftrag erstellen, um eine Audience mit der Echtzeit-Customer Profil-API zu erstellen. Ausführliche Anweisungen dazu finden Sie im Tutorial zur [Evaluierung und zum Zugriff auf Segmentergebnisse](./evaluate-a-segment.md) .