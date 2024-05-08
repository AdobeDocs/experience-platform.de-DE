---
title: Verschlüsselte Datenaufnahme
description: Erfahren Sie, wie Sie verschlüsselte Dateien über Cloud-Speicher-Batch-Quellen mithilfe der API aufnehmen.
exl-id: 83a7a154-4f55-4bf0-bfef-594d5d50f460
source-git-commit: adb48b898c85561efb2d96b714ed98a0e3e4ea9b
workflow-type: tm+mt
source-wordcount: '1736'
ht-degree: 76%

---

# Verschlüsselte Datenaufnahme

Sie können verschlüsselte Datendateien mit Batch-Quellen für den Cloud-Speicher in Adobe Experience Platform erfassen. Mithilfe der verschlüsselten Datenaufnahme können Sie asymmetrische Verschlüsselungsmechanismen nutzen, um Batch-Daten sicher in Experience Platform zu übertragen. Derzeit werden die asymmetrischen Verschlüsselungsmechanismen PGP und GPG unterstützt.

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

## Erste Schritte {#get-started}

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
   * [Cloud-Speicherquellen](../api/collect/cloud-storage.md): Erstellen Sie einen Datenfluss, um Batch-Daten aus Ihrer Cloud-Speicherquelle in Experience Platform zu übertragen.
* [Sandboxes](../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Verwenden von Platform-APIs

Informationen darüber, wie Sie Platform-APIs erfolgreich aufrufen können, finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../landing/api-guide.md).

### Unterstützte Dateierweiterungen für verschlüsselte Dateien {#supported-file-extensions-for-encrypted-files}

Die Liste der unterstützten Dateierweiterungen für verschlüsselte Dateien ist:

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

+++ Beispielanfrage anzeigen

Die folgende Anfrage generiert mithilfe des PGP-Verschlüsselungsalgorithmus ein Verschlüsselungsschlüsselpaar.

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

+++

**Antwort**

+++ Beispielantwort anzeigen

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

+++

### Abrufen von Verschlüsselungsschlüsseln {#retrieve-encryption-keys}

Um alle Verschlüsselungsschlüssel in Ihrem Unternehmen abzurufen, stellen Sie eine GET-Anfrage an die `/encryption/keys` endpoit=nt.

**API-Format**

```http
GET /data/foundation/connectors/encryption/keys
```

**Anfrage**

+++ Beispielanfrage anzeigen

Die folgende Anfrage ruft alle Verschlüsselungsschlüssel in Ihrem Unternehmen ab.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**Antwort**

+++ Beispielantwort anzeigen

Bei einer erfolgreichen Antwort werden Ihr Verschlüsselungsalgorithmus, der öffentliche Schlüssel, die Kennung des öffentlichen Schlüssels und die entsprechende Ablaufzeit Ihrer Schlüssel zurückgegeben.

```json
{
    "encryptionAlgorithm": "{ENCRYPTION_ALGORITHM}",
    "publicKeyId": "{PUBLIC_KEY_ID}",
    "publicKey": "{PUBLIC_KEY}",
    "expiryTime": "{EXPIRY_TIME}"
}
```

+++

### Abrufen von Verschlüsselungsschlüsseln nach ID {#retrieve-encryption-keys-by-id}

Um einen bestimmten Satz von Verschlüsselungsschlüsseln abzurufen, stellen Sie eine GET-Anfrage an die `/encryption/keys` -Endpunkt und geben Sie Ihre öffentliche Schlüssel-ID als Kopfzeilenparameter an.

**API-Format**

```http
GET /data/foundation/connectors/encryption/keys/{PUBLIC_KEY_ID}
```

**Anfrage**

+++ Beispielanfrage anzeigen

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys/{publicKeyId}' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**Antwort**

+++ Beispielantwort anzeigen

Bei einer erfolgreichen Antwort werden Ihr Verschlüsselungsalgorithmus, der öffentliche Schlüssel, die Kennung des öffentlichen Schlüssels und die entsprechende Ablaufzeit Ihrer Schlüssel zurückgegeben.

```json
{
    "encryptionAlgorithm": "{ENCRYPTION_ALGORITHM}",
    "publicKeyId": "{PUBLIC_KEY_ID}",
    "publicKey": "{PUBLIC_KEY}",
    "expiryTime": "{EXPIRY_TIME}"
}
```

+++

### Erstellen eines kundenverwalteten Schlüsselpaars {#create-customer-managed-key-pair}

Sie können optional ein Schlüsselpaar für die Signaturverifizierung erstellen, um Ihre verschlüsselten Daten zu signieren und aufzunehmen.

In dieser Phase müssen Sie Ihre eigene Kombination aus privatem Schlüssel und öffentlichem Schlüssel generieren und dann den privaten Schlüssel zum Signieren Ihrer verschlüsselten Daten verwenden. Als Nächstes müssen Sie Ihren öffentlichen Schlüssel in Base64 codieren und ihn dann für Experience Platform freigeben, damit Platform Ihre Signatur überprüfen kann.

### Freigeben eines öffentlichen Schlüssels für Experience Platform

Um Ihren öffentlichen Schlüssel freizugeben, stellen Sie eine POST-Anfrage an den `/customer-keys`-Endpunkt bei der Bereitstellung Ihres Verschlüsselungsalgorithmus und Ihres Base64-codierten öffentlichen Schlüssels.

**API-Format**

```http
POST /data/foundation/connectors/encryption/customer-keys
```

**Anfrage**

+++ Beispielanfrage anzeigen

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
| `publicKey` | Der öffentliche Schlüssel, der Ihren kundenverwalteten Schlüsseln entspricht, die zum Signieren Ihrer verschlüsselten Daten verwendet werden. Dieser Schlüssel muss Base64-codiert sein. |

+++

**Antwort**

+++ Beispielantwort anzeigen

```json
{    
  "publicKeyId": "e31ae895-7896-469a-8e06-eb9207ddf1c2" 
} 
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `publicKeyId` | Diese öffentliche Schlüssel-ID wird zurückgegeben, wenn Sie Ihren kundenverwalteten Schlüssel für Experience Platform freigeben. Sie können diese öffentliche Schlüssel-ID als Kennung des Signaturverfizierungsschlüssels angeben, wenn Sie einen Datenfluss für signierte und verschlüsselte Daten erstellen. |

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

>[!BEGINTABS]

>[!TAB Erstellen eines Datenflusses für die Aufnahme verschlüsselter Daten]

**Anfrage**

+++ Beispielanfrage anzeigen

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

+++

**Antwort**

+++ Beispielantwort anzeigen

Bei einer erfolgreichen Antwort wird die ID (`id`) des neu erstellten Datenflusses für Ihre verschlüsselten Daten zurückgegeben.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

+++

>[!TAB Erstellen eines Datenflusses für die Aufnahme verschlüsselter und signierter Daten]

**Anfrage**

+++ Beispielanfrage anzeigen

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
| `params.signVerificationKeyId` | Die ID des Signaturverifizierungsschlüssels entspricht der ID des öffentlichen Schlüssels, die nach der Freigabe Ihres Base64-codierten öffentlichen Schlüssels für Experience Platform abgerufen wurde. |

+++

**Antwort**

+++ Beispielantwort anzeigen

Bei einer erfolgreichen Antwort wird die ID (`id`) des neu erstellten Datenflusses für Ihre verschlüsselten Daten zurückgegeben.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

+++

>[!ENDTABS]

### Schlüssel löschen {#delete-encryption-keys}

Um Ihre Verschlüsselungsschlüssel zu löschen, stellen Sie eine DELETE-Anfrage an die `/encryption/keys` -Endpunkt und geben Sie Ihre öffentliche Schlüssel-ID als Kopfzeilenparameter an.

**API-Format**

```http
DELETE /data/foundation/connectors/encryption/keys/{PUBLIC_KEY_ID}
```

**Anfrage**

+++ Beispielanfrage anzeigen

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys/{publicKeyId}' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 204 (Kein Inhalt) und leeren Text zurück.

### Überprüfen von Verschlüsselungsschlüsseln {#validate-encryption-keys}

Um Ihre Verschlüsselungsschlüssel zu validieren, stellen Sie eine GET-Anfrage an die `/encryption/keys/validate/` -Endpunkt und geben Sie die öffentliche Schlüssel-ID an, die Sie als Kopfzeilenparameter überprüfen möchten.

```http
GET /data/foundation/connectors/encryption/keys/validate/{PUBLIC_KEY_ID}
```

**Anfrage**

+++ Beispielanfrage anzeigen

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys/validate/{publicKeyId}' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt entweder eine Bestätigung zurück, dass Ihre IDs gültig oder ungültig sind.

>[!BEGINTABS]

>[!TAB Gültig]

Eine gültige öffentliche Schlüssel-ID gibt den Status `Active` zusammen mit Ihrer öffentlichen Schlüssel-ID.

```json
{
    "publicKeyId": "{PUBLIC_KEY_ID}",
    "status": "Active"
}
```

>[!TAB Ungültig]

Eine ungültige Kennung des öffentlichen Schlüssels gibt den Status `Expired` zusammen mit Ihrer öffentlichen Schlüssel-ID.

```json
{
    "publicKeyId": "{PUBLIC_KEY_ID}",
    "status": "Expired"
}
```

>[!ENDTABS]


## Einschränkungen bei der wiederkehrenden Erfassung {#restrictions-on-recurring-ingestion}

Die verschlüsselte Datenerfassung unterstützt nicht die Erfassung wiederkehrender oder mehrstufiger Ordner in Quellen. Alle verschlüsselten Dateien müssen in einem einzigen Ordner enthalten sein. Platzhalter mit mehreren Ordnern in einem einzelnen Quellpfad werden ebenfalls nicht unterstützt.

Im Folgenden finden Sie ein Beispiel für eine unterstützte Ordnerstruktur, bei der der Quellpfad `/ACME-customers/*.csv.gpg`.

In diesem Szenario werden die fett gedruckten Dateien in Experience Platform aufgenommen.

* ACME-Kunden
   * **File1.csv.gpg**
   * File2.json.gpg
   * **File3.csv.gpg**
   * File4.json
   * **File5.csv.gpg**

Im Folgenden finden Sie ein Beispiel für eine nicht unterstützte Ordnerstruktur, bei der der Quellpfad `/ACME-customers/*`.

In diesem Szenario schlägt die Flussausführung fehl und gibt eine Fehlermeldung zurück, die angibt, dass Daten nicht aus der Quelle kopiert werden können.

* ACME-Kunden
   * File1.csv.gpg
   * File2.json.gpg
   * Unterordner1
      * File3.csv.gpg
      * File4.json.gpg
      * File5.csv.gpg
* ACME-Loyalität
   * File6.csv.gpg


## Nächste Schritte

In diesem Tutorial haben Sie ein Verschlüsselungsschlüsselpaar für Ihre Cloud-Speicherdaten und einen Datenfluss erstellt, um Ihre verschlüsselten Daten mithilfe der [!DNL Flow Service API] aufzunehmen. Statusaktualisierungen zur Vollständigkeit, zu Fehlern und Metriken Ihres Datenflusses finden Sie im Handbuch unter [Überwachen Ihres Datenflusses mithilfe des [!DNL Flow Service] API](./monitor.md).