---
title: Verschlüsselte Datenaufnahme
description: Erfahren Sie, wie Sie verschlüsselte Dateien über Cloud-Speicher-Batch-Quellen mithilfe der API aufnehmen.
hide: true
hidefromtoc: true
exl-id: 83a7a154-4f55-4bf0-bfef-594d5d50f460
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 75%

---

# Verschlüsselte Datenaufnahme

Mit Adobe Experience Platform können Sie verschlüsselte Dateien über Cloud-Speicher-Batch-Quellen aufnehmen. Mithilfe der verschlüsselten Datenaufnahme können Sie asymmetrische Verschlüsselungsmechanismen nutzen, um Batch-Daten sicher in Experience Platform zu übertragen. Derzeit werden die asymmetrischen Verschlüsselungsmechanismen PGP und GPG unterstützt.

Die verschlüsselte Datenaufnahme läuft wie folgt ab:

1. [Erstellen Sie zunächst ein Verschlüsselungsschlüsselpaar mit Experience Platform-APIs](#create-encryption-key-pair). Das Verschlüsselungsschlüsselpaar besteht aus einem privaten Schlüssel und einem öffentlichen Schlüssel. Nach der Erstellung können Sie den öffentlichen Schlüssel zusammen mit der zugehörigen öffentlichen Schlüssel-ID und der Ablaufzeit kopieren oder herunterladen. Während dieses Vorgangs wird der private Schlüssel von Experience Platform in einem sicheren Tresor gespeichert. **HINWEIS**: Der öffentliche Schlüssel in der Antwort ist mit Base64 verschlüsselt und muss vor der Verwendung entschlüsselt werden.
2. Verwenden Sie den öffentlichen Schlüssel, um die aufzunehmende Datendatei zu verschlüsseln.
3. Legen Sie Ihre verschlüsselte Datei in Ihrem Cloud-Speicher ab.
4. Sobald die verschlüsselte Datei fertig ist, [erstellen Sie eine Quellverbindung und einen Datenfluss für Ihre Cloud-Speicherquelle](#create-a-dataflow-for-encrypted-data). Während des Schritts zur Flusserstellung müssen Sie einen `encryption`-Parameter angeben und Ihre öffentliche Schlüssel-ID einschließen.
5. Experience Platform ruft den privaten Schlüssel aus dem sicheren Tresor ab, um die Daten zum Zeitpunkt der Aufnahme zu entschlüsseln.

>[!IMPORTANT]
>
>Die maximale Größe einer einzelnen verschlüsselten Datei beträgt 1 GB. Sie können beispielsweise eine Datenmenge von 2 GB in einem einzelnen Datenfluss aufnehmen, jedoch darf jede einzelne Datei in diesen Daten nicht größer als 1 GB sein.

In diesem Dokument wird beschrieben, wie Sie ein Verschlüsselungsschlüsselpaar zum Verschlüsseln Ihrer Daten generieren und diese verschlüsselten Daten mithilfe von Cloud-Speicherquellen in Experience Platform aufnehmen.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
   * [Cloud-Speicherquellen](../api/collect/cloud-storage.md): Erstellen Sie einen Datenfluss, um Batch-Daten aus Ihrer Cloud-Speicherquelle in Experience Platform zu übertragen.
* [Sandboxes](../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Verwenden von Platform-APIs

Informationen darüber, wie Sie Platform-APIs erfolgreich aufrufen können, finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../landing/api-guide.md).

### Unterstützte Dateierweiterungen für verschlüsselte Dateien

Folgende Dateierweiterungen werden für verschlüsselte Dateien unterstützt:

* .csv 
* .tsv
* .json
* .parquet
* .csv.gpg
* .tsv.gpg
* .json.gpg
* .parquet.gpg
* .csv.pgp
* .tsv.pgp
* .json.pgp
* .parquet.pgp
* .gpg
* .pgp

>[!NOTE]
>
>Die Aufnahme verschlüsselter Dateien in Adobe Experience Platform-Quellen unterstützt openPGP und keine bestimmte proprietäre PGP-Version.

## Erstellen eines Verschlüsselungsschlüsselpaars {#create-encryption-key-pair}

Der erste Schritt bei der Aufnahme verschlüsselter Daten in Experience Platform besteht darin, Ihr Verschlüsselungsschlüsselpaar durch eine POST-Anfrage an den `/encryption/keys`-Endpunkt der [!DNL Connectors]-API zu erstellen.

**API-Format**

```http
POST /data/foundation/connectors/encryption/keys
```

**Anfrage**

Die folgende Anfrage generiert mithilfe des PGP-Verschlüsselungsalgorithmus ein Verschlüsselungs-Schlüsselpaar.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' 
  -d '{
      "encryptionAlgorithm": "PGP",
      "params": {
          "passPhrase": "{{PASSPHRASE}}"
      }
  }'
```

| Parameter | Beschreibung |
| --- | --- |
| `encryptionAlgorithm` | Der Typ des von Ihnen verwendeten Verschlüsselungsalgorithmus. Die unterstützten Verschlüsselungstypen sind `PGP` und `GPG`. |
| `params.passPhrase` | Die Passphrase bietet eine zusätzliche Schutzschicht für Ihre Verschlüsselungsschlüssel. Bei der Erstellung speichert Experience Platform die Passphrase in einem anderen sicheren Tresor als den öffentlichen Schlüssel. Sie müssen eine nicht leere Zeichenfolge als Passphrase angeben. |

**Antwort**

Bei erfolgreicher Antwort werden Ihr öffentlicher, mit Base64 verschlüsselter Schlüssel, die ID des öffentlichen Schlüssels und die Ablaufzeit Ihrer Schlüssel zurückgegeben. Die Ablaufzeit wird automatisch auf 180 Tage nach dem Datum der Schlüsselgenerierung eingestellt. Die Ablaufzeit kann derzeit nicht konfiguriert werden.

```json
{
    ​"publicKey": "{PUBLIC_KEY}",
    ​"publicKeyId": "{PUBLIC_KEY_ID}",
    ​"expiryTime": "1684843168"
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `publicKey` | Der öffentliche Schlüssel wird zum Verschlüsseln der Daten in Ihrem Cloud-Speicher verwendet. Dieser Schlüssel entspricht dem privaten Schlüssel, der in diesem Schritt ebenfalls erstellt wurde. Der private Schlüssel wird jedoch sofort an Experience Platform gesendet. |
| `publicKeyId` | Die öffentliche Schlüssel-ID wird verwendet, um einen Datenfluss zu erstellen und Ihre verschlüsselten Cloud-Speicherdaten in Experience Platform zu erfassen. |
| `expiryTime` | Die Ablaufzeit definiert das Ablaufdatum Ihres Verschlüsselungsschlüsselpaars. Dieses Datum wird automatisch auf 180 Tage nach dem Datum der Schlüsselgenerierung gesetzt und im Unix-Zeitstempelformat angezeigt. |

+++(Optional) Erstellen Sie ein Schlüsselpaar für die Signierüberprüfung für signierte Daten

### Kundenverwaltetes Schlüsselpaar erstellen

Sie können optional ein Schlüsselpaar für die Signaturüberprüfung erstellen, um Ihre verschlüsselten Daten zu signieren und zu erfassen.

In dieser Phase müssen Sie Ihre eigene Kombination aus privatem Schlüssel und öffentlichem Schlüssel generieren und dann Ihren privaten Schlüssel zum Signieren Ihrer verschlüsselten Daten verwenden. Als Nächstes müssen Sie Ihren öffentlichen Schlüssel in Base64 kodieren und ihn dann für Experience Platform freigeben, damit Platform Ihre Signatur überprüfen kann.

### Öffentlichen Schlüssel für Experience Platform freigeben

Um Ihren öffentlichen Schlüssel freizugeben, stellen Sie eine POST-Anfrage an die `/customer-keys` -Endpunkt bei der Bereitstellung Ihres Verschlüsselungsalgorithmus und Ihres Base64-kodierten öffentlichen Schlüssels.

**API-Format**

```http
POST /data/foundation/connectors/encryption/customer-keys
```

**Anfrage**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/encryption/customer-keys' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' 
  -d '{
      "encryptionAlgorithm": {{ENCRYPTION_ALGORITHM}},       
      "publicKey": {{BASE_64_ENCODED_PUBLIC_KEY}}
    }'
```

| Parameter | Beschreibung |
| --- | --- |
| `encryptionAlgorithm` | Der Typ des von Ihnen verwendeten Verschlüsselungsalgorithmus. Die unterstützten Verschlüsselungstypen sind `PGP` und `GPG`. |
| `publicKey` | Der öffentliche Schlüssel, der Ihren kundenverwalteten Schlüsseln entspricht, die zum Signieren Ihrer verschlüsselten Datei verwendet werden. Dieser Schlüssel muss Base64-kodiert sein. |

**Antwort**

```json
{    
  "publicKeyId": "e31ae895-7896-469a-8e06-eb9207ddf1c2" 
} 
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `publicKeyId` | Diese öffentliche Schlüssel-ID wird zurückgegeben, wenn Sie Ihren kundenverwalteten Schlüssel für Experience Platform freigeben. Sie können diese Kennung des öffentlichen Schlüssels als Kennung des Signierüberprüfungsschlüssels angeben, wenn Sie einen Datenfluss für signierte und verschlüsselte Daten erstellen. |

+++

## Verbinden Ihrer Cloud-Speicherquelle mit Experience Platform mithilfe der [!DNL Flow Service]-API

Nachdem Sie Ihr Verschlüsselungsschlüsselpaar abgerufen haben, können Sie nun fortfahren, indem Sie eine Quellverbindung für Ihre Cloud-Speicherquelle erstellen und Ihre verschlüsselten Daten an Platform übertragen.

Zunächst müssen Sie eine Basisverbindung erstellen, um Ihre Quelle für Platform zu authentifizieren. Um eine Basisverbindung zu erstellen und Ihre Quelle zu authentifizieren, wählen Sie die gewünschte Quelle aus der folgenden Liste aus:

* [Amazon S3](../api/create/cloud-storage/s3.md)
* [[!DNL Apache HDFS]](../api/create/cloud-storage/hdfs.md)
* [Azure Blob](../api/create/cloud-storage/blob.md)
* [Azure Data Lake Storage Gen2](../api/create/cloud-storage/adls-gen2.md)
* [Azure File Storage](../api/create/cloud-storage/azure-file-storage.md)
* [Data Landing Zone](../api/create/cloud-storage/data-landing-zone.md)
* [FTP](../api/create/cloud-storage/ftp.md)
* [Google Cloud Storage](../api/create/cloud-storage/google.md)
* [Oracle Object Storage](../api/create/cloud-storage/oracle-object-storage.md)
* [SFTP](../api/create/cloud-storage/sftp.md)

Nachdem Sie eine Basisverbindung erstellt haben, müssen Sie die Schritte im Tutorial zum [Erstellen einer Quellverbindung für eine Cloud-Speicherquelle](../api/collect/cloud-storage.md) befolgen, um eine Quellverbindung, eine Zielverbindung und eine Zuordnung zu erstellen.

## Erstellen eines Datenflusses für verschlüsselte Daten {#create-a-dataflow-for-encrypted-data}

>[!NOTE]
>
>Sie müssen über Folgendes verfügen, um einen Datenfluss für die verschlüsselte Datenaufnahme zu erstellen:
>
>* [ID des öffentlichen Schlüssels](#create-encryption-key-pair)
>* [Quellverbindungs-ID](../api/collect/cloud-storage.md#source)
>* [Zielverbindungs-ID](../api/collect/cloud-storage.md#target)
>* [Zuordnungs-ID](../api/collect/cloud-storage.md#mapping)

Um einen Datenfluss zu erstellen, stellen Sie eine POST-Anfrage an den `/flows`-Endpunkt der [!DNL Flow Service]-API. Zum Aufnehmen verschlüsselter Daten müssen Sie einen Abschnitt `encryption` zur `transformations`-Eigenschaft hinzufügen und die in einem früheren Schritt erstellte `publicKeyId` einschließen.

**API-Format**

```http
POST /flows
```

**Anfrage**

>[!BEGINTABS]

>[!TAB Erstellen eines Datenflusses für die verschlüsselte Datenerfassung]

Die folgende Anfrage erstellt einen Datenfluss zum Aufnehmen verschlüsselter Daten für eine Cloud-Speicherquelle.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "ACME Customer Data",
    "description": "ACME Customer Data (Encrypted)",
    "flowSpec": {
        "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "655f7c1b-1977-49b3-a429-51379ecf0e15"
    ],
    "targetConnectionIds": [
        "de688225-d619-481c-ae3b-40c250fd7c79"
    ],
    "transformations": [
        {
            "name": "Mapping",
            "params": {
                "mappingId": "6b6e24213dbe4f57bd8207d21034ff03",
                "mappingVersion":"0"
            }
        },
        {
            "name": "Encryption",
            "params": {
                "publicKeyId":"311ef6f8-9bcd-48cf-a9e9-d12c45fb7a17"
            }
        }
    ],
    "scheduleParams": {
        "startTime": "1675793392",
        "frequency": "once"
    }
}'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `flowSpec.id` | Die Flussspezifikations-ID, die Cloud-Speicherquellen entspricht. |
| `sourceConnectionIds` | Die ID der Quellverbindung. Diese ID stellt die Übertragung von Daten von der Quelle an Platform dar. |
| `targetConnectionIds` | Die ID der Zielverbindung. Diese ID stellt dar, wo die Daten landen, sobald sie an Platform übermittelt werden. |
| `transformations[x].params.mappingId` | Die ID der Zuordnung. |
| `transformations.name` | Bei der Aufnahme verschlüsselter Dateien müssen Sie `Encryption` als zusätzlichen Transformationsparameter für Ihren Datenfluss angeben. |
| `transformations[x].params.publicKeyId` | Die von Ihnen erstellte ID des öffentlichen Schlüssels. Diese ID entspricht einer Hälfte des Verschlüsselungsschlüsselpaars, das zum Verschlüsseln Ihrer Cloud-Speicherdaten verwendet wird. |
| `scheduleParams.startTime` | Die Startzeit für den Datenfluss in Epochenzeit. |
| `scheduleParams.frequency` | Die Häufigkeit, mit der der Datenfluss Daten erfasst. Zulässige Werte sind: `once`, `minute`, `hour`, `day` oder `week`. |
| `scheduleParams.interval` | Das Intervall bezeichnet den Zeitraum zwischen zwei aufeinanderfolgenden Datenflussausführungen. Der Wert des Intervalls sollte eine Ganzzahl ungleich null sein. Das Intervall ist nicht erforderlich, wenn die Häufigkeit auf `once` festgelegt ist, und sollte größer oder gleich `15` für andere Frequenzwerte sein. |


>[!TAB Erstellen eines Datenflusses zur Erfassung verschlüsselter und signierter Daten]

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "ACME Customer Data (with Sign Verification)",
    "description": "ACME Customer Data (with Sign Verification)",
    "flowSpec": {
        "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "655f7c1b-1977-49b3-a429-51379ecf0e15"
    ],
    "targetConnectionIds": [
        "de688225-d619-481c-ae3b-40c250fd7c79"
    ],
    "transformations": [
        {
            "name": "Mapping",
            "params": {
                "mappingId": "6b6e24213dbe4f57bd8207d21034ff03",
                "mappingVersion":"0"
            }
        },
        {
            "name": "Encryption",
            "params": {
                "publicKeyId":"311ef6f8-9bcd-48cf-a9e9-d12c45fb7a17",
                "signVerificationKeyId":"e31ae895-7896-469a-8e06-eb9207ddf1c2"
            }
        }
    ],
    "scheduleParams": {
        "startTime": "1675793392",
        "frequency": "once"
    }
}'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `params.signVerificationKeyId` | Die ID des Signaturüberprüfungsschlüssels entspricht der Kennung des öffentlichen Schlüssels, die nach der Freigabe Ihres Base64-kodierten öffentlichen Schlüssels für Experience Platform abgerufen wurde. |

>[!ENDTABS]

**Antwort**

Bei einer erfolgreichen Antwort wird die ID (`id`) des neu erstellten Datenflusses für Ihre verschlüsselten Daten zurückgegeben.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie ein Verschlüsselungsschlüsselpaar für Ihre Cloud-Speicherdaten und einen Datenfluss erstellt, um Ihre verschlüsselten Daten mithilfe der [!DNL Flow Service API] aufzunehmen. Statusaktualisierungen zur Vollständigkeit, zu Fehlern und Metriken Ihres Datenflusses finden Sie im Handbuch unter [Überwachen Ihres Datenflusses mithilfe des [!DNL Flow Service] API](./monitor.md).
