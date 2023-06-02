---
keywords: Experience Platform; Startseite; beliebte Themen; Datenvorbereitung; Datenvorbereitung; Streaming; Upset; Streaming-Upset
title: Teilweise Zeilenaktualisierungen an den Profildienst mithilfe der Datenvorbereitung senden
description: In diesem Dokument erfahren Sie, wie Sie mithilfe der Datenvorbereitung Teilzeilenaktualisierungen an den Profildienst senden.
exl-id: f9f9e855-0f72-4555-a4c5-598818fc01c2
source-git-commit: d167975c9c7a267f2888153a05c5857748367822
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 12%

---

# Teilweise Zeilenaktualisierungen senden an [!DNL Profile Service] using [!DNL Data Prep]

Das Streamen von Upserts in [!DNL Data Prep] ermöglicht es Ihnen, partielle Zeilenaktualisierungen an [!DNL Profile Service]-Daten zu senden und gleichzeitig neue Identitätsverknüpfungen mit einer einzigen API-Anfrage zu erstellen und herzustellen.

Durch Streaming-Uploads können Sie das Format Ihrer Daten beibehalten und diese Daten in [!DNL Profile Service] PATCH-Anfragen während der Aufnahme. Basierend auf den von Ihnen bereitgestellten Eingaben, [!DNL Data Prep] ermöglicht es Ihnen, eine einzige API-Payload zu senden und die Daten in beide zu übersetzen [!DNL Profile Service] PATCH und [!DNL Identity Service] ERSTELLEN SIE -Anfragen.

Dieses Dokument enthält Informationen zum Streamen von Uploads in [!DNL Data Prep].

## Erste Schritte

Diese Übersicht setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Data Prep]](./home.md): [!DNL Data Prep] ermöglicht Dateningenieuren das Zuordnen, Transformieren und Validieren von Daten in und aus dem Experience-Datenmodell (XDM).
* [[!DNL Identity Service]](../identity-service/home.md): Verschaffen Sie sich einen besseren Überblick über einzelne Kundinnen und Kunden und deren Verhalten, indem Sie Identitäten geräte- und systemübergreifend verknüpfen.
* [Echtzeit-Kundenprofil](../profile/home.md): Das Echtzeit-Kundenprofli bietet ein einheitliches, kundenspezifisches Profil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.
* [Quellen](../sources/home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.

## Verwenden von Streaming-Uploads in [!DNL Data Prep] {#streaming-upserts-in-data-prep}

>[!NOTE]
>
>Die folgenden Quellen unterstützen die Verwendung von Streaming-Uploads:<ul><li>[[!DNL Amazon Kinesis]](../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../sources/connectors/streaming/http.md)</li></ul>

### Streaming aktiviert einen allgemeinen Workflow

Streaming-Aktualisierungen in [!DNL Data Prep] funktioniert wie folgt:

* Sie müssen zunächst einen Datensatz für [!DNL Profile] Verbrauch. Siehe Handbuch unter [Aktivieren eines Datensatzes für [!DNL Profile]](../catalog/datasets/enable-for-profile.md) für weitere Informationen.
* Wenn neue Identitäten verknüpft werden müssen, müssen Sie auch einen zusätzlichen Datensatz erstellen **mit demselben Schema** als [!DNL Profile] Datensatz.
* Nachdem Ihre Datensätze vorbereitet wurden, müssen Sie einen Datenfluss erstellen, um Ihre eingehende Anfrage der [!DNL Profile] Datensatz;
* Als Nächstes müssen Sie die eingehende Anfrage aktualisieren, um die erforderlichen Kopfzeilen einzuschließen. Diese Header definieren:
   * Der Datenvorgang, der mit [!DNL Profile]: `create`, `merge`und `delete`.
   * Der optionale Identitätsvorgang, der mit [!DNL Identity Service]: `create`.

### Identitätsdatensatz konfigurieren

Wenn neue Identitäten verknüpft werden müssen, müssen Sie einen zusätzlichen Datensatz in der eingehenden Payload erstellen und weitergeben. Beim Erstellen eines Identitätsdatensatzes müssen Sie sicherstellen, dass die folgenden Anforderungen erfüllt sind:

* Der Identitätsdatensatz muss sein zugewiesenes Schema als [!DNL Profile] Datensatz. Eine Inkongruenz von Schemas kann zu inkonsistentem Systemverhalten führen.
* Sie müssen jedoch sicherstellen, dass sich der Identitätsdatensatz von der [!DNL Profile] Datensatz. Wenn die Datensätze identisch sind, werden die Daten überschrieben und nicht aktualisiert.
* Während der ursprüngliche Datensatz für [!DNL Profile], den Identitätsdatensatz **sollte nicht aktiviert sein** für [!DNL Profile]. Andernfalls werden auch Daten überschrieben und nicht aktualisiert. Der Identitätsdatensatz **sollte aktiviert sein** für [!DNL Identity Service].

#### Erforderliche Felder in den Schemas, die mit dem Identitätsdatensatz verknüpft sind {#identity-dataset-required-fileds}

Wenn Ihr Schema erforderliche Felder enthält, muss die Validierung des Datensatzes unterdrückt werden, damit [!DNL Identity Service] um nur die Identitäten zu empfangen. Sie können die Validierung unterdrücken, indem Sie die `disabled` -Wert `acp_validationContext` Parameter. Siehe Beispiel unten:

```shell
curl -X POST 'https://platform.adobe.io/data/foundation/catalog/dataSets/62257bef7a75461948ebcaaa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "tags": {
        "acp_validationContext": [
            "disabled"
        ],
        "unifiedProfile": [
            "enabled:false"
        ],
        "unifiedIdentity": [
            "enabled:true"
        ]
    }
}'
```

>[!TIP]
>
>Sie müssen keine zusätzliche Konfiguration vornehmen, wenn das mit dem Identitätsdatensatz verknüpfte Schema keine erforderlichen Felder aufweist.

## Eingehende Payload-Struktur

Im Folgenden finden Sie ein Beispiel einer eingehenden Payload-Struktur, die neue Identitätslinks erstellt.

### Nutzdaten mit Identitätskonfiguration

```shell
{
  "header": {
    "flowId": "923e2ac3-3869-46ec-9e6f-7012c4e23f69",
    "imsOrgId": "{ORG_ID}",
    "datasetId": "621fc19ab33d941949af16c8",
    "operations": {
        "data": "create" (default)/"merge"/"delete",
        "identity": "create",
        "identityDatasetId": "621fc19ab33d941949af16d9"
    }
  }
... //The raw data attributes are included here as the key/value pairs of the "body" property.
}
```

| Parameter | Beschreibung |
| --- | --- |
| `flowId` | Eine eindeutige ID zur Identifizierung eines Datenflusses. Diese Datenfluss-ID sollte mit der Quellverbindung übereinstimmen, die mit [!DNL Amazon Kinesis], [!DNL Azure Event Hubs]oder [!DNL HTTP API]. Dieser Datenfluss sollte auch eine [!DNL Profile]-aktivierter Datensatz als Zieldatensatz. **Hinweis**: Die ID der [!DNL Profile]-aktivierter Zieldatensatz wird auch als `datasetId` Parameter. |
| `imsOrgId` | Die Kennung, die Ihrer Organisation entspricht. |
| `datasetId` | Die ID der [!DNL Profile]-aktivierter Zieldatensatz Ihres Datenflusses. **Hinweis**: Diese Kennung entspricht der des [!DNL Profile]-aktivierte Ziel-Datensatz-ID in Ihrem Datenfluss. |
| `operations` | Dieser Parameter beschreibt die Aktionen, die [!DNL Data Prep] wird basierend auf der eingehenden Anfrage ausgeführt. |
| `operations.data` | Definiert die Aktionen, die in [!DNL Profile Service]. |
| `operations.identity` | Definiert die Vorgänge, die für die Daten zulässig sind durch [!DNL Identity Service]. |
| `operations.identityDatasetId` | (Optional) Die Kennung des Identitätsdatensatzes, die nur erforderlich ist, wenn neue Identitäten verknüpft werden müssen. |

#### Unterstützte Vorgänge

Die folgenden Vorgänge werden von [!DNL Profile Service]:

| Funktionsweise | Beschreibung |
| --- | --- | 
| `create` | Der Standardvorgang. Dadurch wird eine XDM-Entitätserstellungsmethode für [!DNL Profile Service]. |
| `merge` | Dadurch wird eine Aktualisierungsmethode für XDM-Entitäten für [!DNL Profile Service]. |
| `delete` | Dadurch wird eine XDM-Entitätslöschmethode für [!DNL Profile Service] und entfernt die Daten dauerhaft aus der [!DNL Profile Store]. |

Die folgenden Vorgänge werden von [!DNL Identity Service]:

| Funktionsweise | Beschreibungen |
| --- | --- |
| `create` | Der einzige zulässige Vorgang für diesen Parameter. Wenn `create` wird als Wert für `operations.identity`, dann [!DNL Data Prep] generiert eine XDM-Entitätserstellungsanforderung für [!DNL Identity Service]. Wenn die Identität bereits vorhanden ist, wird die Identität ignoriert. **Hinweis:** Wenn `operations.identity` auf `create`, dann `identityDatasetId` muss ebenfalls angegeben werden. Die XDM-Entität erstellt eine Nachricht, die intern von [!DNL Data Prep] wird für diese Datensatz-ID generiert. |

### Nutzlast ohne Identitätskonfiguration

Wenn neue Identitäten nicht verknüpft werden müssen, können Sie die `identity` und `identityDatasetId` Parameter in den Vorgängen. Dadurch werden nur Daten an gesendet [!DNL Profile Service] und überspringt die [!DNL Identity Service]. Ein Beispiel finden Sie in der folgenden Payload:

```shell
{
  "header": {
    "flowId": "923e2ac3-3869-46ec-9e6f-7012c4e23f69",
    "imsOrgId": "{ORG_ID}",
    "datasetId": "621fc19ab33d941949af16c8",
    "operations": {
        "data": "create"/"merge"/"delete",
    }
  }
... //The raw data attributes are included here as the key/value pairs of the "body" property.
}
```

## Primäre Identitäten dynamisch übergeben

Bei XDM-Aktualisierungen muss das Schema für [!DNL Profile] und eine primäre Identität enthalten. Sie können die primäre Identität eines XDM-Schemas auf zwei Arten angeben:

* Legen Sie ein statisches Feld als primäre Identität im XDM-Schema fest.
* Weisen Sie über die Feldergruppe &quot;Identitätszuordnung&quot;im XDM-Schema eines der Identitätsfelder als primäre Identität zu.

### Festlegen eines statischen Felds als primäres Identitätsfeld im XDM-Schema

Im folgenden Beispiel: `state`, `homePhone.number` und andere Attribute werden mit ihren jeweiligen angegebenen Werten in die [!DNL Profile] mit der primären Identität von `sampleEmail@gmail.com`. Eine Aktualisierungsmeldung zur XDM-Entität wird dann vom Streaming generiert [!DNL Data Prep] -Komponente. [!DNL Profile Service] bestätigt dann, dass die XDM-Aktualisierungsmeldung den Profildatensatz aktualisiert.

>[!NOTE]
>
>In diesem Beispiel werden Identitäten nicht miteinander verknüpft, da keine für die Identität definierten Vorgänge definiert sind.

```shell
curl -X POST 'https://dcs.adobedc.net/collection/9aba816d350a69c4abbd283eb5818ec3583275ffce4880ffc482be5a9d810c4b' \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: d5262d48-0f47-4949-be6d-795f06933527' \
  -d '{
    "header": {
        "flowId" : "d5262d48-0f47-4949-be6d-795f06933527",
        "imsOrgId": "{ORG_ID}",
        "datasetId": "62259f817f62d71947929a7b",
        "operations": {
         "data": "create"
     }
    },
    {
        "body": {
        "homeAddress": {
            "country": "US",
            "state": "GA",
            "region": "va7"
        },
        "homePhone": {
            "number": "123.456.799"
        },
        "identityMap": {
            "Email": [{
                "id": "sampleEmail@gmail.com",
                "primary": true
            }]
        },
      "personalEmail": {
            "address": "sampleEmail@gmail.com",
            "primary": true
       },
      "personID": "346576345",
      "_id": "346576345",
      "timestamp": "2021-05-05T17:51:45.1880+02",
      "workEmail": "sampleWorkEmail@gmail.com"
  }
}'
```

### Weisen Sie eines der Identitätsfelder als primäre Identität über die Feldergruppe &quot;Identitätszuordnung&quot;im XDM-Schema zu.

In diesem Beispiel enthält die Kopfzeile die `operations` -Attribut mit dem `identity` und `identityDatasetId` Eigenschaften. Dadurch können Daten zusammengeführt werden mit [!DNL Profile Service] sowie für Identitäten, die an weitergegeben werden sollen [!DNL Identity Service].

```shell
curl -X POST 'https://dcs.adobedc.net/collection/9aba816d350a69c4abbd283eb5818ec3583275ffce4880ffc482be5a9d810c4b' \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: d5262d48-0f47-4949-be6d-795f06933527' \
  -d '{
    "header": {
        "flowId" : "d5262d48-0f47-4949-be6d-795f06933527",
        "imsOrgId": "{ORG_ID}",
        "datasetId": "62259f817f62d71947929a7b",
        "operations": {          
            "data": "merge",
            "identity": "create",
            "identityDatasetId": "6254a93b851ecd194b64af9e"
      }
    },
    {        
       "body": {
        "homeAddress": {
            "country": "US",
            "state": "GA",
            "region": "va7"
        },
        "homePhone": {
            "number": "123.456.799"
        },
        "identityMap": {
            "Email": [{
                "id": "sampleEmail@gmail.com",
                "primary": true
            }]
        },
      "personalEmail": {
            "address": "sampleEmail@gmail.com",
            "primary": true
       },
      "personID": "346576345",
      "_id": "346576345",
      "timestamp": "2021-05-05T17:51:45.1880+02",
      "workEmail": "sampleWorkEmail@gmail.com"
  }
 }'
```

## Bekannte Einschränkungen und wichtige Überlegungen

Im Folgenden finden Sie eine Liste bekannter Einschränkungen, die beim Streaming von Uploads mit [!DNL Data Prep]:

* Die Streaming-Upsermethode sollte nur verwendet werden, wenn Teilzeilenaktualisierungen an [!DNL Profile Service]. Teilzeilenaktualisierungen sind **not** von Data Lake verbraucht.
* Die Streaming-Upsert-Methode unterstützt nicht das Aktualisieren, Ersetzen und Entfernen von Identitäten. Neue Identitäten werden erstellt, wenn sie nicht vorhanden sind. Daher `identity` -Vorgang muss immer auf &quot;Erstellen&quot;eingestellt sein. Wenn bereits eine Identität vorhanden ist, ist der Vorgang ein no-op-Vorgang.
* Die Streaming-Upsermethode unterstützt derzeit nicht [Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=de) und [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/).

## Nächste Schritte

Durch Lesen dieses Dokuments sollten Sie jetzt verstehen, wie Uploads in gestreamt werden [!DNL Data Prep] , um Teilzeilenaktualisierungen an Ihre [!DNL Profile Service] Daten, während Identitäten auch mit einer einzelnen API-Anfrage erstellt und verknüpft werden. Weitere Informationen zu anderen [!DNL Data Prep] Funktionen, lesen Sie bitte die [[!DNL Data Prep] Übersicht](./home.md). So erfahren Sie, wie Sie Zuordnungssätze im [!DNL Data Prep] API, lesen Sie bitte die [[!DNL Data Prep] Entwicklerhandbuch](./api/overview.md).
