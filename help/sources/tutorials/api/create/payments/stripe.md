---
title: Zahlungsdaten von Ihrer [!DNL Stripe] Experience Platform mithilfe von APIs
description: Erfahren Sie, wie Sie mit der Flow Service-API Zahlungsdaten von Ihrem Stripe-Konto an die Experience Platform erfassen.
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: b5e791882ddb7cb8c87c15d4812470b3bbc9a72e
workflow-type: tm+mt
source-wordcount: '1998'
ht-degree: 45%

---

# Zahlungsdaten von Ihrer [!DNL Stripe] Experience Platform mithilfe von APIs

>[!NOTE]
>
>Die [!DNL Stripe]-Quelle befindet sich in der Beta-Phase. Lesen Sie die [Bedingungen](../../../../home.md#terms-and-conditions) in der Quellenübersicht für weitere Informationen zur Verwendung von Beta-beschrifteten Quellen.

In diesem Tutorial erfahren Sie, wie Sie Ihre Zahlungsdaten aus [!DNL Stripe] zu Adobe Experience Platform mithilfe der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Authentifizierung

Lesen Sie die [[!DNL Stripe] Übersicht](../../../../connectors/payments/stripe.md) für Informationen zum Abrufen Ihrer Authentifizierungsberechtigungen.

### Verwenden von Platform-APIs

Informationen darüber, wie Sie Platform-APIs erfolgreich aufrufen können, finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Verbinden [!DNL Stripe] auf Experience Platform

Im folgenden Handbuch erfahren Sie, wie Sie Ihre [!DNL Stripe] -Quelle, erstellen Sie eine Quellverbindung und erstellen Sie einen Datenfluss, um Ihre Zahlungsdaten an Experience Platform zu übertragen.

### Erstellen einer Basisverbindung {#base-connection}

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Experience Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Sie können Dateien in Ihrer Quelle mithilfe der Basis-Verbindungs-ID untersuchen und darin navigieren. Darüber hinaus können Sie die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Details zu den Datentypen und Formaten dieser Elemente.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an die `/connections` Endpunkt beim Bereitstellen [!DNL Stripe] Authentifizierungsberechtigungen als Teil des Anfragetexts.

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Stripe]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Stripe base connection",
      "description": "Authenticated base connection for Stripe",
      "connectionSpec": {
          "id": "cc2c31d6-7b8c-4581-b49f-5c8698aa3ab3",
          "version": "1.0"
      },
      "auth": {
          "specName": "OAuth2 Refresh Code",
          "params": {
            "accessToken": "{ACCESS_TOKEN}",
          }
      }
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name Ihrer Basisverbindung. Stellen Sie sicher, dass der Name Ihrer Basisverbindung beschreibend ist, da Sie damit Informationen zu Ihrer Basisverbindung nachschlagen können. |
| `description` | Ein optionaler Wert, den Sie angeben können, um weitere Informationen zu Ihrer Basisverbindung bereitzustellen. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID der Quelle. Die Verbindungsspezifikations-ID für [!DNL Stripe] is `cc2c31d6-7b8c-4581-b49f-5c8698aa3ab3`und diese ID fest. |
| `auth.specName` | Der Authentifizierungstyp, den Sie zum Authentifizieren Ihrer Quelle für Experience Platform verwenden. |
| `auth.params.accessToken` | Das Zugriffstoken Ihrer [!DNL Stripe] -Konto. Lesen Sie die [[!DNL Stripe] Authentifizierungshandbuch](../../../../connectors/payments/stripe.md#prerequisites) für Schritte zum Abrufen Ihres Zugriffstokens. |

**Antwort**

Eine erfolgreiche Antwort gibt die neu erstellte Basisverbindung zurück, einschließlich ihrer eindeutigen Verbindungskennung (`id`). Diese ID ist erforderlich, um die Dateistruktur und Inhalte Ihrer Quelle im nächsten Schritt zu untersuchen.

```json
{
  "id": "a9950001-a386-4642-a0cd-5eaac6db5556",
  "etag": "\"dc01244d-0000-0200-0000-65ea4e500000\""
}
```

### Durchsuchen der Quelle {#explore}

Sobald Sie über Ihre Basis-Verbindungs-ID verfügen, können Sie jetzt den Inhalt und die Struktur Ihrer Quelldaten untersuchen, indem Sie eine GET-Anfrage an die `/connections` -Endpunkt hinzugefügt, während Sie Ihre Basis-Verbindungs-ID als Abfrageparameter angeben.

**API-Format**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

**Anfrage**

Bei der Durchführung von GET-Anfragen zur Analyse der Dateistruktur und des Inhalts Ihrer Quelle müssen Sie die in der folgenden Tabelle aufgeführten Abfrageparameter einbeziehen:

| Parameter | Beschreibung |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | Die im vorherigen Schritt generierte Basisverbindungs-ID. |
| `objectType=rest` | Der Objekttyp, den Sie untersuchen möchten. Dieser Wert wird immer auf `rest`. |
| `{OBJECT}` | Dieser Parameter ist nur beim Anzeigen eines bestimmten Ordners erforderlich. Der Wert stellt den Pfad des Ordners dar, den Sie untersuchen möchten. Für diese Quelle würde der Wert `json`. |
| `fileType=json` | Der Dateityp der Datei, die Sie in Platform laden möchten. Zurzeit `json` ist der einzige unterstützte Dateityp. |
| `{PREVIEW}` | Ein boolescher Wert, der definiert, ob der Inhalt der Verbindung die Vorschau unterstützt. |
| `{SOURCE_PARAMS}` | A [!DNL Base64-]kodierte Zeichenfolge, die auf den Ressourcenpfad verweist, den Sie untersuchen möchten. Ihr Ressourcenpfad muss in kodiert werden. [!DNL Base64] um das genehmigte Format für `{SOURCE_PARAMS}`. Beispiel: `{"resourcePath":"charges"}` kodiert als `eyJyZXNvdXJjZVBhdGgiOiJjaGFyZ2VzIn0%3D`. Die Liste der verfügbaren Ressourcenpfade umfasst: <ul><li>`charges`</li><li>`subscriptions`</li><li>`refunds`</li><li>`balance_transactions`</li><li>`customers`</li><li>`prices`</li></ul> |

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/a9950001-a386-4642-a0cd-5eaac6db5556/explore?objectType=rest&object=json&fileType=json&preview=false&sourceParams=eyJyZXNvdXJjZVBhdGgiOiJjaGFyZ2VzIn0%3D' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine JSON-Struktur wie die folgende zurück:

+++Auswählen zum Anzeigen der JSON-Payload

```json
{
  "format": "hierarchical",
  "schema": {
    "type": "object",
    "properties": {
      "data": {
        "type": "object",
        "properties": {
          "balance_transaction": {},
          "billing_details": {
            "type": "object",
            "properties": {
              "address": {
                "type": "object",
                "properties": {
                  "country": {},
                  "city": {},
                  "state": {},
                  "postal_code": {},
                  "line2": {},
                  "line1": {}
                }
              },
              "phone": {},
              "name": {},
              "email": {}
            }
          },
          "metadata": {
            "type": "object",
            "properties": {}
          },
          "livemode": {
            "type": "boolean"
          },
          "radar_options": {
            "type": "object",
            "properties": {}
          },
          "destination": {},
          "description": {
            "type": "string"
          },
          "failure_message": {},
          "fraud_details": {
            "type": "object",
            "properties": {}
          },
          "source": {},
          "amount_refunded": {
            "type": "integer",
            "minimum": -9007199254740992,
            "maximum": 9007199254740991
          },
          "statement_descriptor": {
            "type": "string"
          },
          "transfer_data": {},
          "receipt_url": {
            "type": "string"
          },
          "shipping": {},
          "review": {},
          "captured": {
            "type": "boolean"
          },
          "calculated_statement_descriptor": {
            "type": "string"
          },
          "currency": {
            "type": "string"
          },
          "refunded": {
            "type": "boolean"
          },
          "id": {
            "type": "string"
          },
          "outcome": {
            "type": "object",
            "properties": {
              "reason": {},
              "risk_level": {
                "type": "string"
              },
              "risk_score": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
              },
              "seller_message": {
                "type": "string"
              },
              "network_status": {
                "type": "string"
              },
              "type": {
                "type": "string"
              }
            }
          },
          "payment_method": {
            "type": "string"
          },
          "order": {},
          "dispute": {},
          "amount": {
            "type": "integer",
            "minimum": -9007199254740992,
            "maximum": 9007199254740991
          },
          "disputed": {
            "type": "boolean"
          },
          "failure_code": {},
          "transfer_group": {},
          "on_behalf_of": {},
          "created": {
            "type": "integer",
            "minimum": -9007199254740992,
            "maximum": 9007199254740991
          },
          "payment_method_details": {
            "type": "object",
            "properties": {
              "type": {
                "type": "string"
              },
              "card": {
                "type": "object",
                "properties": {
                  "country": {
                    "type": "string"
                  },
                  "last4": {
                    "type": "string"
                  },
                  "funding": {
                    "type": "string"
                  },
                  "mandate": {},
                  "wallet": {},
                  "exp_month": {
                    "type": "integer",
                    "minimum": -9007199254740992,
                    "maximum": 9007199254740991
                  },
                  "exp_year": {
                    "type": "integer",
                    "minimum": -9007199254740992,
                    "maximum": 9007199254740991
                  },
                  "overcapture": {
                    "type": "object",
                    "properties": {
                      "maximum_amount_capturable": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                      },
                      "status": {
                        "type": "string"
                      }
                    }
                  },
                  "amount_authorized": {
                    "type": "integer",
                    "minimum": -9007199254740992,
                    "maximum": 9007199254740991
                  },
                  "network": {
                    "type": "string"
                  },
                  "network_token": {
                    "type": "object",
                    "properties": {
                      "used": {
                        "type": "boolean"
                      }
                    }
                  },
                  "incremental_authorization": {
                    "type": "object",
                    "properties": {
                      "status": {
                        "type": "string"
                      }
                    }
                  },
                  "checks": {
                    "type": "object",
                    "properties": {
                      "cvc_check": {
                        "type": "string"
                      },
                      "address_line1_check": {},
                      "address_postal_code_check": {}
                    }
                  },
                  "extended_authorization": {
                    "type": "object",
                    "properties": {
                      "status": {
                        "type": "string"
                      }
                    }
                  },
                  "installments": {},
                  "capture_before": {
                    "type": "integer",
                    "minimum": -9007199254740992,
                    "maximum": 9007199254740991
                  },
                  "fingerprint": {
                    "type": "string"
                  },
                  "three_d_secure": {},
                  "brand": {
                    "type": "string"
                  },
                  "multicapture": {
                    "type": "object",
                    "properties": {
                      "status": {
                        "type": "string"
                      }
                    }
                  }
                }
              }
            }
          },
          "amount_captured": {
            "type": "integer",
            "minimum": -9007199254740992,
            "maximum": 9007199254740991
          },
          "source_transfer": {},
          "failure_balance_transaction": {},
          "receipt_number": {},
          "application": {},
          "receipt_email": {},
          "paid": {
            "type": "boolean"
          },
          "application_fee": {},
          "payment_intent": {
            "type": "string"
          },
          "invoice": {},
          "statement_descriptor_suffix": {},
          "application_fee_amount": {},
          "object": {
            "type": "string"
          },
          "customer": {
            "type": "string"
          },
          "status": {
            "type": "string"
          }
        }
      }
    }
  }
}
```

+++

### Erstellen einer Quellverbindung {#source-connection}

Sie können eine Quellverbindung erstellen, indem Sie eine POST-Anfrage an die `/sourceConnections` Endpunkt der [!DNL Flow Service] API. Eine Quellverbindung besteht aus einer Verbindungs-ID, einem Pfad zur Quelldatendatei und einer Verbindungsspezifikations-ID.

**API-Format**

```https
POST /sourceConnections
```

**Anfrage**

Die folgende Anfrage erstellt eine Quellverbindung für [!DNL Stripe].

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Stripe Source Connection For Charges Data",
      "description": "Stripe source connection for charges data",
      "baseConnectionId": "a9950001-a386-4642-a0cd-5eaac6db5556",
      "connectionSpec": {
        "id": "cc2c31d6-7b8c-4581-b49f-5c8698aa3ab3",
        "version": "1.0"
      },
      "data": {
        "format": "json"
      },
      "params": {
        "resourcePath": "charges"
      },
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name Ihrer Quellverbindung. Stellen Sie sicher, dass der Name Ihrer Quellverbindung beschreibend ist, da Sie damit Informationen zu Ihrer Quellverbindung nachschlagen können. |
| `description` | Ein optionaler Wert, den Sie angeben können, um weitere Informationen über Ihre Quellverbindung bereitzustellen. |
| `baseConnectionId` | Die Basisverbindungs-ID von [!DNL Stripe]. Diese ID wurde in einem früheren Schritt generiert. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID, die Ihrer Quelle entspricht |
| `data.format` | Das Format der [!DNL Stripe]-Daten, die Sie aufnehmen möchten. Derzeit wird nur das Datenformat `json` unterstützt. |

Eine erfolgreiche Antwort gibt die eindeutige Kennung (`id`) der neu erstellten Quellverbindung zurück. Diese ID ist in einem späteren Schritt erforderlich, um einen Datenfluss zu erstellen.

```json
{
  "id": "abbfac4e-202c-4e04-902d-6f73e9041068",
  "etag": "\"0a033818-0000-0200-0000-65ea5a770000\""
}
```

### Erstellen eines XDM-Zielschemas {#target-schema}

Damit die Quelldaten in der Experience Platform verwendet werden können, muss ein Zielschema erstellt werden, um die Quelldaten nach Bedarf zu strukturieren. Das Zielschema wird dann verwendet, um einen Platform-Datensatz zu erstellen, in dem die Quelldaten enthalten sind.

Ein Ziel-XDM-Schema kann erstellt werden, indem eine POST-Anfrage an die [Schema-Registrierungs-API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/) durchgeführt wird.

Ausführliche Schritte zum Erstellen eines XDM-Zielschemas finden Sie im Tutorial zum [Erstellen eines Schemas mithilfe der API](../../../../../xdm/api/schemas.md#create-a-schema).

### Erstellen eines Zieldatensatzes {#target-dataset}

Ein Zieldatensatz kann erstellt werden, indem eine POST-Anfrage an die [Catalog Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) durchgeführt wird, wodurch die ID des Zielschemas in der Payload angegeben wird.

Ausführliche Anweisungen zum Erstellen eines Zieldatensatzes finden Sie im Tutorial zu [Erstellen eines Datensatzes mithilfe der API](../../../../../catalog/api/create-dataset.md).

### Erstellen einer Zielverbindung {#target-connection}

Eine Zielverbindung stellt die Verbindung zum Ziel dar, an dem die aufgenommenen Daten gespeichert werden sollen. Um eine Zielverbindung zu erstellen, müssen Sie die feste Verbindungsspezifikations-ID angeben, die dem Data Lake entspricht. Diese ID lautet: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

Sie verfügen jetzt über die eindeutigen Kennungen eines Zielschemas, eines Zieldatensatzes und der Verbindungsspezifikations-ID zum Data Lake. Anhand dieser Kennungen können Sie mit der [!DNL Flow Service]-API eine Zielverbindung erstellen, um den Datensatz anzugeben, der die eingehenden Quelldaten enthalten wird.

**API-Format**

```https
POST /targetConnections
```

**Anfrage**

Die folgende Anfrage erstellt eine Zielverbindung für [!DNL Stripe]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Stripe Target Connection For Charges Data",
      "description": "Stripe target connection for charges data",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "parquet_xdm",
          "schema": {
              "id": "https://ns.adobe.com/{ORG_ID}/schemas/5f76be8c4e4b847fdac13ca42aa6b596a89a5b91dea48b16",
              "version": "application/vnd.adobe.xed-full+json;version=1.3"
          }
      },
      "params": {
          "dataSetId": "65e622315f78042c9e8166e8"
      }
  }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `name` | Der Name Ihrer Zielverbindung. Stellen Sie sicher, dass der Name Ihrer Zielverbindung beschreibend ist, da Sie damit Informationen zu Ihrer Zielverbindung nachschlagen können. |
| `description` | Ein optionaler Wert, den Sie für weitere Informationen zu Ihrer Zielverbindung angeben können. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID, die dem Data Lake entspricht. Diese feste ID lautet: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | Das Format der [!DNL Stripe]-Daten, die Sie aufnehmen möchten. |
| `params.dataSetId` | Die ID Ihres Zieldatensatzes. Diese ID wird von [Erstellen eines Zieldatensatzes](#target-dataset). |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung der neuen Zielverbindung an (`id`). Diese ID ist in späteren Schritten erforderlich.

```json
{
  "id": "69879751-ba43-48df-8cd0-39d2bb76a5b8",
  "etag": "\"4b02ef5b-0000-0200-0000-65ea5f730000\""
}
```

### Erstellen einer Zuordnung {#mapping}

Damit die Quelldaten in einen Zieldatensatz aufgenommen werden können, müssen sie zunächst dem Zielschema zugeordnet werden, zu dem der Zieldatensatz gehört. Dies wird durch eine POST-Anfrage an die [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) mit Datenzuordnungen erreicht, die in der Anfrage-Payload definiert sind.

**API-Format**

```http
POST /conversion/mappingSets
```

Die folgende Anfrage erstellt eine Zuordnung für [!DNL Stripe].

+++Auswählen zum Anzeigen des Anforderungsbeispiels

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "version": 0,
      "xdmSchema": "https://ns.adobe.com/exchangesandboxcharlie/schemas/5f76be8c4e4b847fdac13ca42aa6b596a89a5b91dea48b16",
      "xdmVersion": "1.0",
      },
      "mappings":[
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.id",
            "sourceAttribute":"data.id",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.refunded",
            "sourceAttribute":"data.refunded",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.disputed",
            "sourceAttribute":"data.disputed",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.last4",
            "sourceAttribute":"data.payment_method_details.card.last4",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.livemode",
            "sourceAttribute":"data.livemode",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.status",
            "sourceAttribute":"data.status",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.overcapture.maximum_amount_capturable",
            "sourceAttribute":"data.payment_method_details.card.overcapture.maximum_amount_capturable",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.receipt_url",
            "sourceAttribute":"data.receipt_url",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.fingerprint",
            "sourceAttribute":"data.payment_method_details.card.fingerprint",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_intent",
            "sourceAttribute":"data.payment_intent",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.overcapture.status",
            "sourceAttribute":"data.payment_method_details.card.overcapture.status",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.network_token.used",
            "sourceAttribute":"data.payment_method_details.card.network_token.used",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.funding",
            "sourceAttribute":"data.payment_method_details.card.funding",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.amount",
            "sourceAttribute":"data.amount",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.customer",
            "sourceAttribute":"data.customer",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.incremental_authorization.status",
            "sourceAttribute":"data.payment_method_details.card.incremental_authorization.status",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.multicapture.status",
            "sourceAttribute":"data.payment_method_details.card.multicapture.status",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.amount_captured",
            "sourceAttribute":"data.amount_captured",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method",
            "sourceAttribute":"data.payment_method",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.object",
            "sourceAttribute":"data.object",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.captured",
            "sourceAttribute":"data.captured",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.created",
            "sourceAttribute":"data.created",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.paid",
            "sourceAttribute":"data.paid",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.amount_refunded",
            "sourceAttribute":"data.amount_refunded",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.currency",
            "sourceAttribute":"data.currency",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.country",
            "sourceAttribute":"data.payment_method_details.card.country",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.exp_year",
            "sourceAttribute":"data.payment_method_details.card.exp_year",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.amount_authorized",
            "sourceAttribute":"data.payment_method_details.card.amount_authorized",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.network",
            "sourceAttribute":"data.payment_method_details.card.network",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details",
            "sourceAttribute":"data.payment_method_details",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.exp_month",
            "sourceAttribute":"data.payment_method_details.card.exp_month",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.calculated_statement_descriptor",
            "sourceAttribute":"data.calculated_statement_descriptor",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.brand",
            "sourceAttribute":"data.payment_method_details.card.brand",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.balance_transaction",
            "sourceAttribute":"data.balance_transaction",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.extended_authorization.status",
            "sourceAttribute":"data.payment_method_details.card.extended_authorization.status",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.outcome",
            "sourceAttribute":"data.outcome",
            "identity":false,
            "version":0
        }
      ]
}
```


| Eigenschaft | Beschreibung |
| --- | --- |
| `xdmSchema` | Die ID Ihres Ziel-XDM-Schemas. Diese ID wird durch die Erstellung einer [Ziel-XDM-Schema](#target-schema). |
| `destinationXdmPath` | Das XDM-Feld, dem das Quellattribut zugeordnet wird. |
| `sourceAttribute` | Das Quelldatenfeld, das zugeordnet wird. |
| `identity` | Ein boolean -Wert, der definiert, ob das Feld in [Identity Service](../../../../../identity-service/home.md). |
| `version` | Die verwendete Zuordnungsversion. |

+++

**Antwort**

Eine erfolgreiche Antwort gibt Details zur neu erstellten Zuordnung an, einschließlich der eindeutigen Kennung (`id`). Dieser Wert ist in einem späteren Schritt zum Erstellen eines Datenflusses erforderlich.

```json
{
  "id": "f4aad280fdec4770b7e33066945919d8",
  "version": 0,
  "createdDate": 1709860257007,
  "modifiedDate": 1709860257007,
  "createdBy": "{CREATED_BY}",
  "modifiedBy": "{MODIFIED_BY}"
}
```

### Erstellen eines Flusses {#flow}

Der letzte Schritt zur Datenübermittlung von [!DNL Stripe] in Platform einen Datenfluss erstellen. Bislang haben Sie die folgenden erforderlichen Werte vorbereitet:

* [Quellverbindungs-ID](#source-connection)
* [Zielverbindungs-ID](#target-connection)
* [Zuordnungs-ID](#mapping)

Ein Datenfluss ist für die Planung und Erfassung von Daten aus einer Quelle verantwortlich. Sie können einen Datenfluss erstellen, indem Sie eine POST-Anfrage ausführen und dabei die oben genannten Werte in der Payload angeben.

**API-Format**

```http
POST /flows
```

**Anfrage**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Stripe Connector Flow Generic Rest",
    "description": "Stripe Connector Description Flow Generic Rest",
    "flowSpec": {
        "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "abbfac4e-202c-4e04-902d-6f73e9041068"
    ],
    "targetConnectionIds": [
        "69879751-ba43-48df-8cd0-39d2bb76a5b8"
    ],
    "transformations": [
        {
            "name": "Mapping",
            "params": {
                "mappingId": "f4aad280fdec4770b7e33066945919d8",
                "mappingVersion": 0
            }
        }
    ],
    "scheduleParams": {
        "startTime": "1710267858",
        "frequency": "minute",
        "interval": {{interval}}
    }
}'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Der Name Ihres Datenflusses. Stellen Sie sicher, dass der Name Ihres Datenflusses beschreibend ist, da Sie damit Informationen zu Ihrem Datenfluss suchen können. |
| `description` | Ein optionaler Wert, den Sie hinzufügen können, um weitere Informationen zu Ihrem Datenfluss bereitzustellen. |
| `flowSpec.id` | Die Flussspezifikations-ID, die zum Erstellen eines Datenflusses erforderlich ist. Diese feste ID lautet: `6499120c-0b15-42dc-936e-847ea3c24d72`. |
| `flowSpec.version` | Die entsprechende Version der Flussspezifikations-ID. Dieser Wert ist standardmäßig auf `1.0` festgelegt. |
| `sourceConnectionIds` | Die [Quellverbindungs-ID](#source-connection), die in einem früheren Schritt generiert wurde. |
| `targetConnectionIds` | Die [Zielverbindungs-ID](#target-connection), die in einem früheren Schritt generiert wurde. |
| `transformations` | Diese Eigenschaft enthält die verschiedenen Umwandlungen, die auf Ihre Daten angewendet werden müssen. Diese Eigenschaft ist erforderlich, wenn nicht-XDM-konforme Daten an Experience Platform übermittelt werden. |
| `transformations.name` | Der Name, der der Transformation zugewiesen wurde. |
| `transformations.params.mappingId` | Die [Zuordnungs-ID](#mapping), die in einem früheren Schritt generiert wurde. |
| `transformations.params.mappingVersion` | Die entsprechende Version der Zuordnungs-ID. Dieser Wert ist standardmäßig auf `0` festgelegt. |
| `scheduleParams.startTime` | Der Zeitpunkt, zu dem Ihr Datenfluss beginnt. Sie müssen den Startzeitwert im Format eines Unix-Zeitstempels angeben. |
| `scheduleParams.frequency` | Die Häufigkeit, mit der der Datenfluss Daten erfasst. Sie können die Erfassungsfrequenz wie folgt konfigurieren:  <ul><li>**Einmal**: Setzen Sie Ihre Häufigkeit auf `once` , um eine einmalige Erfassung zu erstellen. Konfigurationen für Intervall und Aufstockung sind beim Erstellen eines einmaligen Erfassungsdataflods nicht verfügbar. Standardmäßig ist die Planung auf einmal eingestellt.</li><li>**Minute**: Setzen Sie Ihre Häufigkeit auf `minute` , um Ihren Datenfluss so zu planen, dass Daten pro Minute erfasst werden.</li><li>**Stunde**:Setzen Sie Ihre Häufigkeit auf `hour` , um den Datenfluss so zu planen, dass Daten pro Stunde erfasst werden.</li><li>**Tag**: Setzen Sie Ihre Häufigkeit auf `day` , um Ihren Datenfluss so zu planen, dass Daten täglich erfasst werden.</li><li>**Woche**: Setzen Sie Ihre Häufigkeit auf `week` , um Ihren Datenfluss so zu planen, dass Daten pro Woche erfasst werden.</li></ul> |
| `scheduleParams.interval` | Das Intervall bezeichnet den Zeitraum zwischen zwei aufeinanderfolgenden Datenflussausführungen. Wenn Sie beispielsweise Ihre Häufigkeit auf &quot;Tag&quot;festlegen und das Intervall auf 15 konfigurieren, wird Ihr Datenfluss alle 15 Tage ausgeführt. Der Intervallwert sollte eine Ganzzahl ungleich null sein. |

**Antwort**

Bei einer erfolgreichen Antwort wird die ID (`id`) des neu erstellten Datenflusses angegeben. Mit dieser ID können Sie Ihren Datenfluss überwachen, aktualisieren oder löschen.

```json
{
     "id": "84c64142-1741-4b0b-95a9-65644eba0cf6",
     "etag": "\"3901770b-0000-0200-0000-655708970000\""
}
```

## Anhang

Im folgenden Abschnitt finden Sie Informationen zu den Schritten, die Sie zum Überwachen, Aktualisieren und Löschen Ihres Datenflusses unternehmen können.

### Überwachen Ihres Datenflusses

Nachdem Ihr Datenfluss erstellt wurde, können Sie die Datenaufnahme überwachen, um Informationen über die Datenflussausführungen, den Abschlussstatus und Fehler anzuzeigen. Die vollständigen API-Beispiele finden Sie im Handbuch unter [Überwachen der Datenflüsse Ihrer Quellen mithilfe der API](../../monitor.md).

### Aktualisieren des Datenflusses

Aktualisieren Sie die Details Ihres Datenflusses, z. B. seinen Namen und seine Beschreibung, sowie den Ausführungszeitplan und die zugehörigen Zuordnungssätze, indem Sie eine PATCH-Anfrage an den Endpunkt /flows des [!DNL Flow Service] API bei der Angabe der Kennung Ihres Datenflusses. Bei einer PATCH-Anfrage müssen Sie die eindeutige `etag` im `If-Match` -Kopfzeile. Die vollständigen API-Beispiele finden Sie im Handbuch unter [Aktualisieren von Datenflüssen für Quellen mithilfe der API](../../update-dataflows.md).

### Konto aktualisieren

Aktualisieren Sie den Namen, die Beschreibung und die Anmeldeinformationen Ihres Quellkontos, indem Sie eine PATCH-Anfrage an die [!DNL Flow Service] API bei der Bereitstellung Ihrer Basis-Verbindungs-ID als Abfrageparameter. Bei einer PATCH-Anfrage müssen Sie die eindeutige `etag` im `If-Match` -Kopfzeile. Die vollständigen API-Beispiele finden Sie im Handbuch unter [Aktualisieren Ihres Quellkontos mithilfe der API](../../update.md).

### Löschen des Datenflusses

Löschen Sie Ihren Datenfluss, indem Sie eine DELETE-Anfrage an die [!DNL Flow Service] API bei Angabe der Kennung des Datenflusses, den Sie als Teil des Abfrageparameters löschen möchten. Die vollständigen API-Beispiele finden Sie im Handbuch unter [Löschen Ihrer Datenflüsse mithilfe der API](../../delete-dataflows.md).

### Konto löschen

Löschen Sie Ihr Konto, indem Sie eine DELETE-Anfrage an die [!DNL Flow Service] API bei Angabe der grundlegenden Verbindungs-ID des Kontos, das Sie löschen möchten. Die vollständigen API-Beispiele finden Sie im Handbuch unter [Löschen Ihres Quellkontos mithilfe der API](../../delete.md).

