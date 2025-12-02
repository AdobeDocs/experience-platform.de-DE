---
keywords: Experience Platform;Startseite;beliebte Themen;Datenvorbereitung;Datenvorbereitung;Streaming;Upsert;Streaming Upsert
title: Senden von partiellen Zeilenaktualisierungen an das Echtzeit-Kundenprofil mithilfe der Datenvorbereitung
description: Erfahren Sie, wie Sie mithilfe der Datenvorbereitung partielle Zeilenaktualisierungen an das Echtzeit-Kundenprofil senden.
exl-id: f9f9e855-0f72-4555-a4c5-598818fc01c2
source-git-commit: f988d7665a40b589ca281d439b6fca508f23cd03
workflow-type: tm+mt
source-wordcount: '1363'
ht-degree: 3%

---

# Senden Sie partielle Zeilenaktualisierungen an [!DNL Real-Time Customer Profile] mithilfe von [!DNL Data Prep]

>[!IMPORTANT]
>
>* Die Aufnahme von Meldungen zur Aktualisierung der Experience-Datenmodell (XDM)-Entität (mit JSON-PATCH-Vorgängen) für Profilaktualisierungen über den DCS-Eingang ist veraltet. Führen Sie alternativ dazu die in diesem Handbuch beschriebenen Schritte aus.
>
>* Sie können auch die HTTP-API-Quelle verwenden[ um Rohdaten in den DCS-Eingang aufzunehmen ](../sources/tutorials/api/create/streaming/http.md#sending-messages-to-an-authenticated-streaming-connection) die erforderlichen Datenzuordnungen anzugeben, um Ihre Daten in XDM-konforme Nachrichten für Profilaktualisierungen umzuwandeln.
>
>* Bei der Verwendung von Arrays beim Streaming von Upserts müssen Sie explizit `upsert_array_append` oder `upsert_array_replace` verwenden, um einen klaren Zweck des Vorgangs zu definieren. Möglicherweise werden Fehler angezeigt, wenn diese Funktionen fehlen.

Verwenden Sie das Streaming von Upserts in [!DNL Data Prep], um partielle Zeilenaktualisierungen an [!DNL Real-Time Customer Profile]-Daten zu senden und gleichzeitig neue Identitätsverknüpfungen mit einer einzigen API-Anfrage zu erstellen und herzustellen.

Durch das Streamen von Upserts können Sie das Format Ihrer Daten beibehalten, während Sie diese Daten während der Aufnahme in [!DNL Real-Time Customer Profile] PATCH-Anfragen übersetzen. Basierend auf den von Ihnen bereitgestellten Eingaben können Sie mit [!DNL Data Prep] eine einzige API-Payload senden und die Daten sowohl an [!DNL Real-Time Customer Profile] PATCH- als auch [!DNL Identity Service] CREATE-Anfragen übersetzen.

[!DNL Data Prep] verwendet Header-Parameter, um zwischen Einfügungen und Upserts zu unterscheiden. Alle Zeilen, die Upserts verwenden, müssen eine Kopfzeile haben. Sie können Upserts mit oder ohne Identitätsdeskriptoren verwenden. Wenn Sie Upserts mit Identitäten verwenden, müssen Sie die Konfigurationsschritte ausführen, die im Abschnitt „Konfigurieren [ Identitätsdatensatzes“ beschrieben ](#configure-the-identity-dataset). Wenn Sie Upserts ohne Identitäten verwenden, müssen Sie in Ihrer Anfrage keine Identitätskonfigurationen angeben. Weitere Informationen finden Sie im Abschnitt [Streamen von Upserts ohne ](#payload-without-identity-configuration)&quot;.

>[!NOTE]
>
>Um die Upsert-Funktion zu nutzen, wird empfohlen, XDM-kompatible Konfigurationen während der Datenaufnahme zu deaktivieren und die eingehende Payload mit [Data Prep Mapper) neu ](./ui/mapping.md).

Dieses Dokument enthält Informationen zum Streamen von Upserts in [!DNL Data Prep].

## Erste Schritte

Diese Übersicht setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Data Prep]](./home.md): [!DNL Data Prep] ermöglicht es Dateningenieuren, Daten dem Experience-Datenmodell (XDM) zuzuordnen, umzuformen und zu validieren.
* [[!DNL Identity Service]](../identity-service/home.md): Verschaffen Sie sich einen besseren Überblick über einzelne Kunden und deren Verhalten, indem Sie Identitäten geräte- und systemübergreifend verknüpfen.
* [Echtzeit-Kundenprofil](../profile/home.md): Das Echtzeit-Kundenprofli bietet ein einheitliches, kundenspezifisches Profil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.
* [Quellen](../sources/home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.

## Streamen von Upserts in [!DNL Data Prep] verwenden {#streaming-upserts-in-data-prep}

>[!NOTE]
>
>Die folgenden Quellen unterstützen die Verwendung von Streaming-Upserts:<ul><li>[[!DNL Amazon Kinesis]](../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../sources/connectors/streaming/http.md)</li></ul>

### Hochrangiger Workflow zum Streamen von Upserts

Das Streamen von Upserts in [!DNL Data Prep] funktioniert wie folgt:

* Sie müssen zunächst einen Datensatz für die [!DNL Profile]-Nutzung erstellen und aktivieren. Weitere Informationen finden Sie in der Anleitung [Aktivieren eines Datensatzes für [!DNL Profile]](../catalog/datasets/enable-for-profile.md) .
* Wenn neue Identitäten verknüpft werden müssen, müssen Sie auch einen zusätzlichen Datensatz **mit demselben Schema)** Ihren [!DNL Profile] Datensatz erstellen.
* Nachdem Ihre Datensätze vorbereitet wurden, müssen Sie einen Datenfluss erstellen, um Ihre eingehende Anfrage dem [!DNL Profile] Datensatz zuzuordnen.
* Als Nächstes müssen Sie die eingehende Anfrage aktualisieren, um die erforderlichen Kopfzeilen einzuschließen. Diese Kopfzeilen definieren:
   * Der Datenvorgang, der mit [!DNL Profile] ausgeführt werden muss: `create`, `merge` und `delete`.
   * Der optionale Identitätsvorgang, der mit [!DNL Identity Service] ausgeführt werden soll: `create`.

### Identitätsdatensatz konfigurieren {#configure-the-identity-dataset}

Wenn neue Identitäten verknüpft werden müssen, müssen Sie einen zusätzlichen Datensatz in der eingehenden Payload erstellen und übergeben. Beim Erstellen eines Identitätsdatensatzes müssen Sie sicherstellen, dass die folgenden Anforderungen erfüllt sind:

* Der Identitätsdatensatz muss sein verknüpftes Schema als [!DNL Profile] Datensatz haben. Inkonsistente Schemata können zu inkonsistentem Systemverhalten führen.
* Sie müssen jedoch sicherstellen, dass sich der Identitätsdatensatz vom [!DNL Profile] unterscheidet. Wenn die Datensätze identisch sind, werden die Daten überschrieben anstatt aktualisiert.
* Während der ursprüngliche Datensatz für [!DNL Profile] aktiviert werden muss, **der Identitätsdatensatz für** nicht [!DNL Profile] werden. Andernfalls werden auch Daten überschrieben, anstatt aktualisiert zu werden. Der Identitätsdatensatz (sollte **aktiviert sein** für [!DNL Identity Service].

#### Erforderliche Felder in den mit dem Identitätsdatensatz verknüpften Schemata {#identity-dataset-required-fileds}

Wenn Ihr Schema erforderliche Felder enthält, muss die Validierung des Datensatzes unterdrückt werden, damit [!DNL Identity Service] nur die Identitäten erhalten können. Sie können die Validierung unterdrücken, indem Sie den `disabled` auf den `acp_validationContext` anwenden. Siehe folgendes Beispiel:

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
>Sie müssen keine zusätzliche Konfiguration vornehmen, wenn das mit dem Identitätsdatensatz verknüpfte Schema über keine erforderlichen Felder verfügt.

## Struktur der eingehenden Payloads

Im Folgenden sehen Sie ein Beispiel für eine Struktur eingehender Payloads, die neue Identitäts-Links erstellt.

### Payload mit Identitätskonfiguration

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
| `flowId` | Eine eindeutige ID zur Identifizierung eines Datenflusses. Diese Datenfluss-ID sollte der Quellverbindung entsprechen, die mit [!DNL Amazon Kinesis], [!DNL Azure Event Hubs] oder [!DNL HTTP API] erstellt wurde. Dieser Datenfluss sollte auch über einen [!DNL Profile]-aktivierten Datensatz als Zieldatensatz verfügen. **Hinweis**: Die ID des [!DNL Profile] Zieldatensatzes wird auch als `datasetId` verwendet. |
| `imsOrgId` | Die ID, die Ihrer Organisation entspricht. |
| `datasetId` | Die ID des [!DNL Profile] Zieldatensatzes Ihres Datenflusses. **Hinweis**: Dies ist die gleiche ID wie die [!DNL Profile]-aktivierte Zieldatensatz-ID in Ihrem Datenfluss. |
| `operations` | Dieser Parameter beschreibt die Aktionen, die [!DNL Data Prep] basierend auf der eingehenden Anfrage ausführen. |
| `operations.data` | Definiert die Aktionen, die in [!DNL Real-Time Customer Profile] ausgeführt werden müssen. |
| `operations.identity` | Definiert die für die Daten nach [!DNL Identity Service] zulässigen Vorgänge. |
| `operations.identityDatasetId` | (Optional) Die ID des Identitätsdatensatzes, die nur erforderlich ist, wenn neue Identitäten verknüpft werden müssen. |

#### Unterstützte Vorgänge

Die folgenden Vorgänge werden von [!DNL Real-Time Customer Profile] unterstützt:

| Funktionsweise | Beschreibung |
| --- | --- | 
| `create` | Der Standardvorgang. Dadurch wird eine XDM-Entitäts-Erstellungsmethode für [!DNL Real-Time Customer Profile] generiert. |
| `merge` | Dadurch wird eine XDM-Entitäts-Aktualisierungsmethode für [!DNL Real-Time Customer Profile] generiert. |
| `delete` | Dadurch wird eine XDM-Entitätslöschmethode für [!DNL Real-Time Customer Profile] generiert und die Daten dauerhaft aus der [!DNL Profile store] entfernt. |

Die folgenden Vorgänge werden von [!DNL Identity Service] unterstützt:

| Funktionsweise | Beschreibungen |
| --- | --- |
| `create` | Der einzige zulässige Vorgang für diesen Parameter. Wenn `create` als Wert für `operations.identity` übergeben wird, generiert [!DNL Data Prep] eine XDM-Entitäts-Erstellungsanfrage für [!DNL Identity Service]. Wenn die Identität bereits vorhanden ist, wird sie ignoriert. **Hinweis:** Wenn `operations.identity` auf `create` gesetzt ist, muss auch der `identityDatasetId` angegeben werden. Die intern von [!DNL Data Prep] Komponente generierte XDM-Entitäts-Erstellungsnachricht wird für diese Datensatz-ID generiert. |

### Payload ohne Identitätskonfiguration {#payload-without-identity-configuration}

Wenn neue Identitäten nicht verknüpft werden müssen, können Sie die Parameter `identity` und `identityDatasetId` in den Vorgängen auslassen. Dadurch werden Daten nur an [!DNL Real-Time Customer Profile] gesendet und die [!DNL Identity Service] übersprungen. Ein Beispiel finden Sie unten in der Payload:

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

## Dynamisches Übergeben primärer Identitäten

Für XDM-Aktualisierungen muss das Schema für die [!DNL Profile] aktiviert sein und eine primäre Identität enthalten. Sie können die primäre Identität eines XDM-Schemas auf zwei Arten angeben:

* Bestimmen Sie ein statisches Feld als primäre Identität im XDM-Schema.
* Bestimmen Sie eines der Identitätsfelder als primäre Identität über die Feldergruppe „Identitätszuordnung“ im XDM-Schema.

### Bestimmen Sie ein statisches Feld als primäres Identitätsfeld im XDM-Schema

Im folgenden Beispiel werden `state`, `homePhone.number` und andere Attribute mit ihren jeweiligen angegebenen Werten in die [!DNL Profile] mit der primären Identität `sampleEmail@gmail.com` upsertiert. Eine XDM-Entitäts-Aktualisierungsmeldung wird dann von der Streaming-[!DNL Data Prep] generiert. [!DNL Real-Time Customer Profile] bestätigt dann, dass die XDM-Aktualisierungsmeldung den Profildatensatz upsert.

>[!NOTE]
>
>In diesem Beispiel werden Identitäten nicht miteinander verknüpft, da für Identität keine Vorgänge definiert sind.

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

### Bestimmen Sie eines der Identitätsfelder als primäre Identität über die Feldergruppe „Identitätszuordnung“ im XDM-Schema

In diesem Beispiel enthält die Kopfzeile das Attribut `operations` mit den Eigenschaften `identity` und `identityDatasetId` . Auf diese Weise können Daten mit [!DNL Real-Time Customer Profile] zusammengeführt und Identitäten an [!DNL Identity Service] übergeben werden.

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

Im Folgenden finden Sie eine Liste bekannter Einschränkungen, die beim Streaming von Upserts mit [!DNL Data Prep] zu beachten sind:

* Die Streaming-Upserts-Methode sollte nur verwendet werden, wenn partielle Zeilenaktualisierungen an [!DNL Real-Time Customer Profile] gesendet werden. Teilweise Zeilenaktualisierungen werden **nicht** vom Data Lake genutzt.
* Die Streaming-Methode upserts unterstützt nicht das Aktualisieren, Ersetzen und Entfernen von Identitäten. Neue Identitäten werden erstellt, wenn sie nicht vorhanden sind. Daher muss für den `identity`-Vorgang immer „Erstellen“ festgelegt sein. Wenn bereits eine Identität vorhanden ist, ist der Vorgang ein No-op-Vorgang.
* Die Streaming-Upsert-Methode unterstützt derzeit nicht die [Adobe Experience Platform Web SDK](/help/collection/js/js-overview.md) oder die [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/).

## Nächste Schritte

Durch Lesen dieses Dokuments sollten Sie jetzt verstehen, wie Sie Upserts in streamen, [!DNL Data Prep] partielle Zeilenaktualisierungen an Ihre [!DNL Real-Time Customer Profile]-Daten zu senden und gleichzeitig Identitäten mit einer einzigen API-Anfrage zu erstellen und zu verknüpfen. Weitere Informationen zu anderen [!DNL Data Prep]-Funktionen finden Sie unter [[!DNL Data Prep] Übersicht](./home.md). Informationen zur Verwendung von Zuordnungssätzen in der [!DNL Data Prep]-API finden Sie im [[!DNL Data Prep] Entwicklerhandbuch](./api/overview.md).
