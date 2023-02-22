---
title: Verschlüsselte Datenerfassung
description: Mit Adobe Experience Platform können Sie verschlüsselte Dateien über Cloud-Speicher-Batch-Quellen erfassen.
hide: true
hidefromtoc: true
source-git-commit: f0bbefcd9b4595f02c400ea0c5bb76bfa6c5e33e
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 21%

---

# Verschlüsselte Datenerfassung

Mit Adobe Experience Platform können Sie verschlüsselte Dateien über Cloud-Speicher-Batch-Quellen erfassen. Mit der verschlüsselten Datenerfassung können Sie asymmetrische Verschlüsselungsmechanismen nutzen, um Batch-Daten sicher in Experience Platform zu übertragen. Derzeit werden asymmetrische Verschlüsselungsmechanismen von PGP und GPG unterstützt.

Der verschlüsselte Datenerfassungsprozess sieht wie folgt aus:

1. [Erstellen eines Verschlüsselungs-Schlüsselpaars mit Experience Platform-APIs](#create-encryption-key-pair). Das Verschlüsselungsschlüsselpaar besteht aus einem privaten Schlüssel und einem öffentlichen Schlüssel. Nach der Erstellung können Sie den öffentlichen Schlüssel zusammen mit der zugehörigen öffentlichen Schlüssel-ID und der Ablaufzeit kopieren oder herunterladen. Während dieses Vorgangs wird der private Schlüssel von Experience Platform in einem sicheren Vault gespeichert.
2. Verwenden Sie den öffentlichen Schlüssel, um die Datendatei zu verschlüsseln, die Sie erfassen möchten.
3. Platzieren Sie Ihre verschlüsselte Datei in Ihrem Cloud-Speicher.
4. Sobald die verschlüsselte Datei fertig ist, [Quellverbindung und einen Datenfluss für Ihre Cloud-Speicherquelle erstellen](#create-a-dataflow-for-encrypted-data). Während des Schritts zur Flusserstellung müssen Sie eine `encryption` und fügen Sie Ihre öffentliche Schlüssel-ID hinzu.
5. Experience Platform ruft den privaten Schlüssel aus dem sicheren Vault ab, um die Daten zum Zeitpunkt der Erfassung zu entschlüsseln.

In diesem Dokument wird beschrieben, wie Sie ein Verschlüsselungsschlüsselpaar zum Verschlüsseln Ihrer Daten generieren und diese verschlüsselten Daten mithilfe von Cloud-Speicher-Quellen in die Experience Platform aufnehmen.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
   * [Cloud-Speicherquellen](../api/collect/cloud-storage.md): Erstellen Sie einen Datenfluss, um Batch-Daten aus Ihrer Cloud-Speicherquelle in die Experience Platform zu übertragen.
* [Sandboxes](../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Verwenden von Platform-APIs

Informationen darüber, wie Sie Platform-APIs erfolgreich aufrufen können, finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../landing/api-guide.md).

## Verschlüsselungs-Schlüsselpaar erstellen {#create-encryption-key-pair}

Der erste Schritt bei der Erfassung verschlüsselter Daten in Experience Platform besteht darin, Ihr Verschlüsselungsschlüsselpaar zu erstellen, indem Sie eine POST-Anfrage an die `/encryption/keys` Endpunkt der [!DNL Connectors] API.

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
| `params.passPhrase` | Die Passphrase bietet eine zusätzliche Schutzschicht für Ihre Verschlüsselungsschlüssel. Nach der Erstellung speichert Experience Platform die Passphrase in einem anderen sicheren Vault als den öffentlichen Schlüssel. Sie müssen eine nicht leere Zeichenfolge als Passphrase angeben. |

**Antwort**

Bei einer erfolgreichen Antwort werden Ihr öffentlicher Schlüssel, die Kennung des öffentlichen Schlüssels und die Ablaufzeit Ihrer Schlüssel zurückgegeben. Die Ablaufzeit wird automatisch auf 180 Tage nach dem Datum der Schlüsselgenerierung eingestellt. Die Ablaufzeit kann derzeit nicht konfiguriert werden.

```json
{
    ​"publicKey": "{PUBLIC_KEY}",
    ​"publicKeyId": "{PUBLIC_KEY_ID}",
    ​"expiryTime": "1684843168"
}
```

## Verbinden Sie Ihre Cloud-Speicherquelle mit Experience Platform mithilfe der [!DNL Flow Service] API

Nachdem Sie Ihr Verschlüsselungsschlüsselpaar abgerufen haben, können Sie jetzt fortfahren und eine Quellverbindung für Ihre Cloud-Speicherquelle erstellen und Ihre verschlüsselten Daten an Platform übertragen.

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

Nachdem Sie eine Basisverbindung erstellt haben, müssen Sie die im Tutorial für [Erstellen einer Quellverbindung für eine Cloud-Speicher-Quelle](../api/collect/cloud-storage.md) um eine Quellverbindung, eine Zielverbindung und eine Zuordnung zu erstellen.

## Erstellen eines Datenflusses für verschlüsselte Daten {#create-a-dataflow-for-encrypted-data}

>[!NOTE]
>
>Sie müssen über Folgendes verfügen, um einen Datenfluss für die verschlüsselte Datenerfassung zu erstellen:
>* [Öffentliche Schlüssel-ID](#create-encryption-key-pair)
>* [Quellverbindungs-ID](../api/collect/cloud-storage.md#source)
>* [Zielverbindungs-ID](../api/collect/cloud-storage.md#target)
>* [Zuordnungs-ID](../api/collect/cloud-storage.md#mapping)


Um einen Datenfluss zu erstellen, stellen Sie eine POST-Anfrage an die `/flows` Endpunkt der [!DNL Flow Service] API. Zum Erfassen verschlüsselter Daten müssen Sie eine `encryption` Abschnitt `transformations` -Eigenschaft und schließen Sie die `publicKeyId` , die in einem früheren Schritt erstellt wurde.

**API-Format**

```http
POST /flows
```

**Anfrage**

Die folgende Anfrage erstellt einen Datenfluss zum Erfassen verschlüsselter Daten für eine Cloud-Speicherquelle.

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
| `flowSpec.id` | Die Flussspezifikations-ID, die Cloud-Speicher-Quellen entspricht. |
| `sourceConnectionIds` | Die Kennung der Quellverbindung. Diese ID stellt die Übertragung von Daten von der Quelle an Platform dar. |
| `targetConnectionIds` | Die Kennung der Zielverbindung. Diese ID stellt dar, wo die Daten landen, sobald sie an Platform übermittelt werden. |
| `transformations[x].params.mappingId` | Die Zuordnungs-ID. |
| `transformations.name` | Bei der Erfassung verschlüsselter Dateien müssen Sie `Encryption` als zusätzlichen Transformationsparameter für Ihren Datenfluss. |
| `transformations[x].params.publicKeyId` | Die von Ihnen erstellte öffentliche Schlüssel-ID. Diese ID entspricht der Hälfte des Verschlüsselungsschlüsselpaars, das zum Verschlüsseln Ihrer Cloud-Speicherdaten verwendet wird. |
| `scheduleParams.startTime` | Die Startzeit für den Datenfluss in Epochenzeit. |
| `scheduleParams.frequency` | Die Häufigkeit, mit der der Datenfluss Daten erfasst. Zulässige Werte sind: `once`, `minute`, `hour`, `day` oder `week`. |
| `scheduleParams.interval` | Das Intervall bezeichnet den Zeitraum zwischen zwei aufeinanderfolgenden Datenflussausführungen. Der Wert des Intervalls sollte eine Ganzzahl ungleich null sein. Das Intervall ist nicht erforderlich, wenn die Häufigkeit auf `once` festgelegt ist, und sollte größer oder gleich `15` für andere Frequenzwerte sein. |

**Antwort**

Eine erfolgreiche Antwort gibt die ID (`id`) des neu erstellten Datenflusses für Ihre verschlüsselten Daten.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie ein Verschlüsselungsschlüsselpaar für Ihre Cloud-Speicherdaten und einen Datenfluss erstellt, um Ihre verschlüsselten Daten mit der [!DNL Flow Service API]. Statusaktualisierungen zur Vollständigkeit, zu Fehlern und Metriken Ihres Datenflusses finden Sie im Handbuch unter [Überwachen Ihres Datenflusses mithilfe des [!DNL Flow Service] API](./monitor.md).