---
keywords: Experience Platform;home;popular topics;data prep;Data Prep;streaming;upsert;Streaming upsert
title: Teilweise Zeilen-Aktualisierungen mithilfe der Datenvorbereitung an das Echtzeit-Kundenprofil senden
description: Erfahren Sie, wie Sie mithilfe der Datenvorbereitung partielle Zeilenaktualisierungen an das Echtzeit-Kundenprofil senden.
exl-id: f9f9e855-0f72-4555-a4c5-598818fc01c2
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1241'
ht-degree: 5%

---

# Teilweise Zeilen-Updates mit [!DNL Data Prep] an [!DNL Real-Time Customer Profile] senden

>[!WARNING]
>
>Die Erfassung von Entitäts-Update-Meldungen für Experience-Datenmodell (XDM) (mit JSON-PATCH-Vorgängen) für Profilaktualisierungen über den DCS-Inlet wird nicht mehr unterstützt. Alternativ können Sie [Rohdaten in den DCS-Inlet aufnehmen](../sources/tutorials/api/create/streaming/http.md#sending-messages-to-an-authenticated-streaming-connection) und die erforderlichen Datenzuordnungen angeben, um Ihre Daten in XDM-kompatible Nachrichten für Profilaktualisierungen umzuwandeln.

Streaming-Uploads in [!DNL Data Prep] ermöglichen es Ihnen, partielle Zeilenaktualisierungen an [!DNL Real-Time Customer Profile] -Daten zu senden und gleichzeitig neue Identitäts-Links mit einer einzelnen API-Anfrage zu erstellen und zu erstellen.

Durch Streaming-Uploads können Sie das Format Ihrer Daten beibehalten und diese Daten während der Aufnahme in [!DNL Real-Time Customer Profile] PATCH-Anfragen übersetzen. Basierend auf den von Ihnen bereitgestellten Eingaben ermöglicht Ihnen [!DNL Data Prep] das Senden einer einzelnen API-Payload und die Übersetzung der Daten in sowohl [!DNL Real-Time Customer Profile] PATCH- als auch [!DNL Identity Service] CREATE-Anfragen.

>[!NOTE]
>
>Um die Upsert-Funktion zu nutzen, wird empfohlen, XDM-kompatible Konfigurationen während der Datenerfassung zu deaktivieren und die eingehende Payload mit [Datenvorbereitungs-Mapper](./ui/mapping.md) neu zuzuordnen.

Dieses Dokument enthält Informationen zum Streamen von Uploads in [!DNL Data Prep].

## Erste Schritte

Diese Übersicht setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Data Prep]](./home.md): [!DNL Data Prep] ermöglicht es Dateningenieuren, Daten dem Experience-Datenmodell (XDM) zuzuordnen, umzuwandeln und zu validieren.
* [[!DNL Identity Service]](../identity-service/home.md): Verschaffen Sie sich einen besseren Überblick über einzelne Kunden und ihr Verhalten, indem Sie Identitäten zwischen Geräten und Systemen überbrücken.
* [Echtzeit-Kundenprofil](../profile/home.md): Das Echtzeit-Kundenprofli bietet ein einheitliches, kundenspezifisches Profil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.
* [Quellen](../sources/home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.

## Verwenden von Streaming-Aufnahmen in [!DNL Data Prep] {#streaming-upserts-in-data-prep}

>[!NOTE]
>
>Die folgenden Quellen unterstützen die Verwendung von Streaming-Uploads:<ul><li>[[!DNL Amazon Kinesis]](../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../sources/connectors/streaming/http.md)</li></ul>

### Streaming aktiviert einen allgemeinen Workflow

Streaming-Aufrufe in [!DNL Data Prep] funktionieren wie folgt:

* Sie müssen zunächst einen Datensatz für den [!DNL Profile]-Verbrauch erstellen und aktivieren. Weitere Informationen finden Sie im Handbuch zum Aktivieren eines Datensatzes für  [!DNL Profile]](../catalog/datasets/enable-for-profile.md).[
* Wenn neue Identitäten verknüpft werden müssen, müssen Sie auch einen zusätzlichen Datensatz **mit demselben Schema** wie Ihren [!DNL Profile]-Datensatz erstellen.
* Nachdem Ihre Datensätze vorbereitet wurden, müssen Sie einen Datenfluss erstellen, um Ihre eingehende Anfrage dem [!DNL Profile] -Datensatz zuzuordnen.
* Als Nächstes müssen Sie die eingehende Anfrage aktualisieren, um die erforderlichen Kopfzeilen einzuschließen. Diese Header definieren:
   * Der Datenvorgang, der mit [!DNL Profile]: `create`, `merge` und `delete` ausgeführt werden muss.
   * Der optionale Identitätsvorgang, der mit [!DNL Identity Service]: `create` ausgeführt werden soll.

### Identitätsdatensatz konfigurieren

Wenn neue Identitäten verknüpft werden müssen, müssen Sie einen zusätzlichen Datensatz in der eingehenden Payload erstellen und weitergeben. Beim Erstellen eines Identitätsdatensatzes müssen Sie sicherstellen, dass die folgenden Anforderungen erfüllt sind:

* Der Identitätsdatensatz muss über sein zugewiesenes Schema als [!DNL Profile] -Datensatz verfügen. Eine Inkongruenz von Schemas kann zu inkonsistentem Systemverhalten führen.
* Sie müssen jedoch sicherstellen, dass sich der Identitätsdatensatz vom [!DNL Profile] -Datensatz unterscheidet. Wenn die Datensätze identisch sind, werden die Daten überschrieben und nicht aktualisiert.
* Während der ursprüngliche Datensatz für [!DNL Profile] aktiviert werden muss, sollte der Identitätsdatensatz **nicht aktiviert sein** für [!DNL Profile]. Andernfalls werden auch Daten überschrieben und nicht aktualisiert. Der Identitätsdatensatz **sollte jedoch für [!DNL Identity Service] aktiviert sein.**

#### Erforderliche Felder in den Schemas, die mit dem Identitätsdatensatz verknüpft sind {#identity-dataset-required-fileds}

Wenn Ihr Schema erforderliche Felder enthält, muss die Validierung des Datensatzes unterdrückt werden, damit [!DNL Identity Service] nur die Identitäten empfangen kann. Sie können die Validierung unterdrücken, indem Sie den Wert `disabled` auf den Parameter `acp_validationContext` anwenden. Siehe folgendes Beispiel:

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
| `flowId` | Eine eindeutige ID zur Identifizierung eines Datenflusses. Diese Datenfluss-ID sollte der mit [!DNL Amazon Kinesis], [!DNL Azure Event Hubs] oder [!DNL HTTP API] erstellten Quellverbindung entsprechen. Dieser Datenfluss sollte auch einen [!DNL Profile]-aktivierten Datensatz als Zieldatensatz enthalten. **Hinweis**: Die Kennung des [!DNL Profile]-aktivierten Zieldatensatzes wird auch als Ihr `datasetId` -Parameter verwendet. |
| `imsOrgId` | Die Kennung, die Ihrer Organisation entspricht. |
| `datasetId` | Die ID des [!DNL Profile]-aktivierten Zieldatensatzes Ihres Datenflusses. **Hinweis**: Dies ist dieselbe ID wie die [!DNL Profile]-aktivierte Ziel-Datensatz-ID in Ihrem Datenfluss. |
| `operations` | Dieser Parameter beschreibt die Aktionen, die [!DNL Data Prep] je nach eingehender Anfrage durchführt. |
| `operations.data` | Definiert die Aktionen, die in [!DNL Real-Time Customer Profile] ausgeführt werden müssen. |
| `operations.identity` | Definiert die Vorgänge, die für die Daten durch [!DNL Identity Service] zulässig sind. |
| `operations.identityDatasetId` | (Optional) Die Kennung des Identitätsdatensatzes, die nur erforderlich ist, wenn neue Identitäten verknüpft werden müssen. |

#### Unterstützte Vorgänge

Die folgenden Vorgänge werden von [!DNL Real-Time Customer Profile] unterstützt:

| Funktionsweise | Beschreibung |
| --- | --- | 
| `create` | Der Standardvorgang. Dadurch wird eine XDM-Entitätserstellungsmethode für [!DNL Real-Time Customer Profile] generiert. |
| `merge` | Dadurch wird eine Aktualisierungsmethode für XDM-Entitäten für [!DNL Real-Time Customer Profile] generiert. |
| `delete` | Dadurch wird eine XDM-Entitätslöschmethode für [!DNL Real-Time Customer Profile] generiert und die Daten dauerhaft aus dem [!DNL Profile store] entfernt. |

Die folgenden Vorgänge werden von [!DNL Identity Service] unterstützt:

| Funktionsweise | Beschreibungen |
| --- | --- |
| `create` | Der einzige zulässige Vorgang für diesen Parameter. Wenn `create` als Wert für `operations.identity` übergeben wird, generiert [!DNL Data Prep] eine Anforderung zum Erstellen einer XDM-Entität für [!DNL Identity Service]. Wenn die Identität bereits vorhanden ist, wird die Identität ignoriert. **Hinweis:** Wenn `operations.identity` auf `create` gesetzt ist, muss auch der `identityDatasetId` angegeben werden. Die von der Komponente [!DNL Data Prep] intern generierte XDM-Entität wird für diese Datensatz-ID generiert. |

### Nutzlast ohne Identitätskonfiguration

Wenn keine neuen Identitäten verknüpft werden müssen, können Sie die Parameter `identity` und `identityDatasetId` in den Vorgängen auslassen. Dadurch werden nur Daten an [!DNL Real-Time Customer Profile] gesendet und die [!DNL Identity Service] übersprungen. Ein Beispiel finden Sie in der folgenden Payload:

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

Bei XDM-Aktualisierungen muss das Schema für [!DNL Profile] aktiviert sein und eine primäre Identität enthalten. Sie können die primäre Identität eines XDM-Schemas auf zwei Arten angeben:

* Legen Sie ein statisches Feld als primäre Identität im XDM-Schema fest.
* Weisen Sie über die Feldergruppe &quot;Identitätszuordnung&quot;im XDM-Schema eines der Identitätsfelder als primäre Identität zu.

### Festlegen eines statischen Felds als primäres Identitätsfeld im XDM-Schema

Im folgenden Beispiel werden `state`, `homePhone.number` und andere Attribute mit ihren jeweiligen angegebenen Werten in die [!DNL Profile] mit der primären Identität von `sampleEmail@gmail.com` eingefügt. Eine Aktualisierungsmeldung zur XDM-Entität wird dann von der Streaming-Komponente [!DNL Data Prep] generiert. [!DNL Real-Time Customer Profile] bestätigt dann, dass die XDM-Aktualisierungsmeldung den Profildatensatz aktualisiert.

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

In diesem Beispiel enthält die Kopfzeile das Attribut `operations` mit den Eigenschaften `identity` und `identityDatasetId`. Dadurch können Daten mit [!DNL Real-Time Customer Profile] zusammengeführt und Identitäten an [!DNL Identity Service] weitergegeben werden.

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

Im Folgenden finden Sie eine Liste bekannter Einschränkungen, die beim Streaming von Uploads mit [!DNL Data Prep] zu beachten sind:

* Die Streaming-Upsert-Methode sollte nur verwendet werden, wenn Teilzeilenaktualisierungen an [!DNL Real-Time Customer Profile] gesendet werden. Teilzeilenaktualisierungen werden vom Data Lake **nicht** genutzt.
* Die Streaming-Upsert-Methode unterstützt nicht das Aktualisieren, Ersetzen und Entfernen von Identitäten. Neue Identitäten werden erstellt, wenn sie nicht vorhanden sind. Daher muss der Vorgang `identity` immer auf &quot;create&quot;eingestellt sein. Wenn bereits eine Identität vorhanden ist, ist der Vorgang ein no-op-Vorgang.
* Die Methode zur Streaming-Aufstockung unterstützt derzeit nicht [Adobe Experience Platform Web SDK](/help/web-sdk/home.md) und [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/).

## Nächste Schritte

Durch Lesen dieses Dokuments sollten Sie jetzt verstehen, wie Upserts in [!DNL Data Prep] gestreamt werden, um partielle Zeilenaktualisierungen an Ihre [!DNL Real-Time Customer Profile]-Daten zu senden, und gleichzeitig Identitäten erstellen und mit einer einzelnen API-Anfrage verknüpfen. Weitere Informationen zu anderen [!DNL Data Prep]-Funktionen finden Sie in der [[!DNL Data Prep] Übersicht](./home.md) . Informationen zur Verwendung von Zuordnungssätzen in der API [!DNL Data Prep] finden Sie im [[!DNL Data Prep] Entwicklerhandbuch](./api/overview.md).
