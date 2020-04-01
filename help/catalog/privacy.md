---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Verarbeitung von Datenschutzanfragen im Data Lake
topic: overview
translation-type: tm+mt
source-git-commit: 5f0e0deb4a2fae636ac4d2313a6541c25309c294

---


# Verarbeitung von Datenschutzanfragen im Data Lake

Der Adobe Experience Platform Privacy Service verarbeitet Anfragen von Kunden zum Zugriff auf ihre personenbezogenen Daten, zu Opt-out oder zu löschen, wie sie in Datenschutzbestimmungen wie der Allgemeinen Datenschutzverordnung (GDPR) und dem California Consumer Privacy Act (CCPA) definiert sind.

In diesem Dokument werden wesentliche Konzepte zur Verarbeitung von Datenschutzanforderungen für im Data Lake gespeicherte Kundendaten behandelt.

## Erste Schritte

Es wird empfohlen, die folgenden Experience Platform-Dienste zu verstehen, bevor Sie dieses Handbuch lesen:

* [Datenschutzdienst](../privacy-service/home.md): Verwaltet Kundenanforderungen für den Zugriff auf, die Einstellung des Verkaufs oder das Löschen ihrer personenbezogenen Daten in allen Adobe Experience Cloud-Anwendungen.
* [Katalogdienst](home.md): Das Datensatzsystem für die Position und die Lineage von Daten in Experience Platform. Stellt eine API bereit, mit der die Metadaten des Datensatzes aktualisiert werden können.
* [Erlebnis-Datenmodell (XDM)-System](../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.

## Hinzufügen von Datenschutzbezeichnungen zu Datensätzen {#privacy-labels}

Damit ein Datensatz in einer Datenschutzanforderung für den Data Lake verarbeitet werden kann, muss der Datensatz mit Datenschutzetiketten versehen werden. Datenschutzetiketten geben an, welche Felder im zugehörigen Schema eines Datasets auf die Namensraum zutreffen, die voraussichtlich in Datenschutzanfragen gesendet werden.

Dieser Abschnitt zeigt, wie Sie einem Datensatz Datenschutzbeschriftungen hinzufügen, die in Datenschutzanforderungen von Data Lake verwendet werden können. Beachten Sie zunächst den folgenden Datensatz:

```json
{
    "5d8e9cf5872f18164763f971": {
        "name": "Loyalty Members",
        "description": "Dataset for the Loyalty Members schema",
        "imsOrg": "{IMS_ORG}",
        "tags": {
            "adobe/pqs/table": [
                "loyalty_members"
            ]
        },
        "namespace": "ACP",
        "state": "DRAFT",
        "id": "5d8e9cf5872f18164763f971",
        "dule": {
            "identity": [],
            "contract": [
                "C2",
                "C5"
            ],
            "sensitive": [],
            "contracts": [
                "C2",
                "C5"
            ],
            "identifiability": [],
            "specialTypes": []
        },
        "version": "1.0.2",
        "created": 1569627381749,
        "updated": 1569880723282,
        "createdClient": "acp_ui_platform",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "viewId": "5d8e9cf5872f18164763f972",
        "aspect": "production",
        "status": "enabled",
        "fileDescription": {
            "persisted": true,
            "containerFormat": "parquet",
            "format": "parquet"
        },
        "files": "@/dataSets/5d8e9cf5872f18164763f971/views/5d8e9cf5872f18164763f972/files",
        "schemaMetadata": {
            "primaryKey": [],
            "delta": [],
            "dule": [
                {
                    "path": "/properties/personalEmail/properties/address",
                    "identity": [
                        "I1"
                    ],
                    "contract": [],
                    "sensitive": [],
                    "contracts": [],
                    "identifiability": [
                        "I1"
                    ],
                    "specialTypes": []
                }
            ],
            "gdpr": []
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    }
}
```

Die `schemaMetadata` Eigenschaft für den Datensatz enthält ein `gdpr` Array, das zurzeit leer ist. Um dem Datensatz Datenschutzbeschriftungen hinzuzufügen, muss dieses Array mit einer PATCH-Anforderung an die [Katalogdienst-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)aktualisiert werden.

>[!NOTE] Obwohl das Array benannt ist `gdpr`, ermöglicht es das Hinzufügen von Bezeichnungen für Datenschutzaufträge sowohl für GDPR- als auch für CCPA-Regeln.

**API-Format**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{DATASET_ID}` | Der `id` Wert des zu aktualisierenden Datensatzes. |

**Anfrage**

In diesem Beispiel enthält ein Datensatz eine E-Mail-Adresse in das `personalEmail.address` Feld. Damit dieses Feld als Bezeichner für Datenschutzanforderungen von Data Lake fungiert, muss ein Etikett mit einem nicht registrierten Namensraum in sein `gdpr` Array aufgenommen werden.

Die folgende Anforderung fügt eine Datenschutzbeschriftung hinzu, mit der der Namensraum &quot;email_label&quot;dem `personalEmail.address` Feld zugewiesen wird.

>[!IMPORTANT] Wenn Sie einen PATCH-Vorgang für die `schemaMetadata` Eigenschaft eines Datensatzes ausführen, stellen Sie sicher, dass Sie alle vorhandenen Untereigenschaften innerhalb der Anforderungsnutzlast kopieren. Wenn Sie vorhandene Werte aus der Nutzlast ausschließen, werden sie aus dem Datensatz entfernt.

```shell
curl -X PATCH 'https://platform.adobe.io/data/foundation/catalog/dataSets/5d8e9cf5872f18164763f971' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{ 
    "schemaMetadata": { 
      "primaryKey": [],
      "delta": [],
      "dule": [
        {
          "path": "/properties/personalEmail/properties/address",
          "identity": [
              "I1"
          ],
          "contract": [],
          "sensitive": [],
          "contracts": [],
          "identifiability": [
              "I1"
          ],
          "specialTypes": []
        }
      ],
      "gdpr": [
          {
              "namespace": ["email_label"],
              "path": "/properties/personalEmail/properties/address"
          }
      ]
  }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `namespace` | Ein Array, das die Namensraum auflistet, die mit dem in `path`angegebenen Feld verknüpft werden sollen. Namensraum werden verwendet, um datenschutzbezogene Felder beim [Senden von Zugriffs- oder Löschanforderungen](#submit) in der Datenschutzdienst-API zu identifizieren. |
| `path` | Der Pfad zum Feld im zugehörigen Schema des Datensatzes, der für das `namespace`Feld gilt. Im Idealfall sollten Datenschutzbeschriftungen nur auf &quot;Blattfelder&quot;(Felder ohne Unterfelder) angewendet werden. |

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 (OK) mit der ID des Datensatzes zurück, der in der Payload bereitgestellt wird. Wenn Sie die ID zum Nachschlagen des Datensatzes verwenden, wird deutlich, dass die Datenschutzbeschriftungen hinzugefügt wurden.

```json
[
    "@/dataSets/5d8e9cf5872f18164763f971"
]
```

### Bezeichnen verschachtelter Kartenfelder

Beachten Sie, dass es zwei Arten von verschachtelten Kartenfeldern gibt, die keine Datenschutzkennzeichnung unterstützen:

* Ein Feld vom Typ &quot;map&quot;in einem Feld vom Typ &quot;array&quot;
* Ein Feld vom Typ &quot;Map&quot;in einem anderen Feld vom Typ &quot;map&quot;

Die Verarbeitung von Datenschutzaufträgen für eines der beiden obigen Beispiele schlägt schließlich fehl. Aus diesem Grund wird empfohlen, verschachtelte Felder vom Typ &quot;Map&quot;nicht zum Speichern von Daten privater Kunden zu verwenden. Relevante Kunden-IDs sollten als Nicht-Map-Datentyp innerhalb des `identityMap` Felds (selbst ein Zuordnungsfeld) für Datensatzdatasets oder als `endUserID` Feld für zeitreihenbasierte Datensätze gespeichert werden.

## Einreichen von Anträgen {#submit}

>[!NOTE] In diesem Abschnitt wird beschrieben, wie Sie Datenschutzanforderungen für den Data Lake formatieren. Es wird dringend empfohlen, die Dokumentation der [Datenschutzdienst-API](../privacy-service/api/getting-started.md) oder der Benutzeroberfläche [des](../privacy-service/ui/overview.md) Datenschutzdienstes zu lesen, um die vollständigen Schritte zum Senden eines Datenschutzauftrags zu erfahren, einschließlich der richtigen Formatierung gesendeter Benutzeridentitätsdaten in Anforderungs-Nutzdaten.

Im folgenden Abschnitt wird beschrieben, wie Sie mit der Datenschutzdienst-API oder der Benutzeroberfläche Datenschutzanforderungen für den Data Lake durchführen.

### Verwenden der API

Beim Erstellen von Auftragsanforderungen in der API müssen alle `userIDs` bereitgestellten Aufträge einen bestimmten `namespace` und `type` je nach Datenspeicher verwenden, für den sie gelten. IDs für den Data Lake müssen für ihren `type` Wert &quot;nicht registriert&quot;und einen `namespace` Wert verwenden, der mit einer der [Datenschutzbeschriftungen](#privacy-labels) übereinstimmt, die den entsprechenden Datensätzen hinzugefügt wurden.

Darüber hinaus muss das `include` Array der Anforderungs-Nutzlast die Produktwerte für die verschiedenen Datenspeicher enthalten, an die die Anforderung gesendet wird. Bei Anforderungen an den Data Lake muss das Array den Wert &quot;aepDataLake&quot;enthalten.

Die folgende Anforderung erstellt einen neuen Datenschutzauftrag für den Data Lake mit dem nicht registrierten Namensraum &quot;email_label&quot;. Er enthält außerdem den Produktwert für den Data Lake im `include` Array:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
      }
    ],
    "users": [
      {
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "email_label",
            "value": "ajones@acme.com",
            "type": "unregistered"
          },
          {
            "namespace": "email_label",
            "value": "jdoe@example.com",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["aepDataLake"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "ccpa"
}'
```

### Verwenden der Benutzeroberfläche

Wählen Sie beim Erstellen von Auftragsanforderungen in der Benutzeroberfläche **AEP Data Lake** und/oder **Profil** unter _Products_ aus, um Aufträge für Daten zu verarbeiten, die im Data Lake bzw. im Real-Time Customer Profil gespeichert werden.

<img src="images/privacy/product-value.png" width="450"><br>

## Anforderungsverarbeitung löschen

Wenn Experience Platform eine Löschanforderung vom Datenschutzdienst erhält, sendet Platform eine Bestätigung an den Datenschutzdienst, dass die Anforderung empfangen wurde und die betroffenen Daten zum Löschen markiert wurden. Die Datensätze werden dann innerhalb von sieben Tagen aus dem Data Lake entfernt. Während dieses siebentägigen Fensters werden die Daten weich gelöscht und stehen daher keinem Plattformdienst zur Verfügung.

In zukünftigen Versionen sendet Platform eine Bestätigung an den Datenschutzdienst, nachdem die Daten physisch gelöscht wurden.

## Nächste Schritte

Durch das Lesen dieses Dokuments wurden Sie zu den wichtigen Konzepten der Verarbeitung von Datenschutzanforderungen für den Data Lake vorgestellt. Es wird empfohlen, die Dokumentation in diesem Handbuch weiter zu lesen, um Ihr Verständnis für die Verwaltung von Identitätsdaten und die Erstellung von Datenschutzaufträgen zu vertiefen.

Anweisungen zur Verarbeitung von Datenschutzanforderungen für den Profil Store finden Sie im Dokument zur Verarbeitung von [Datenschutzanforderungen für Echtzeit-Kundendaten](../profile/privacy.md) .