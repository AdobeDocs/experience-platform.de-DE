---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Segment bewerten
topic: tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '2841'
ht-degree: 2%

---


# Segmentergebnisse auswerten und darauf zugreifen

In diesem Dokument finden Sie eine Anleitung zur Segmentbewertung und zum Zugriff auf Segmentergebnisse mithilfe der [Segmentierungs-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml).

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der verschiedenen Adobe Experience Platformen, die beim Erstellen von Audiencen-Segmenten erforderlich sind. Bevor Sie mit diesem Lernprogramm beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [Echtzeit-Profil](../../profile/home.md): Bietet ein einheitliches, kundenspezifisches Profil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.
- [Adobe Experience Platform Segmentation Service](../home.md): Ermöglicht Ihnen das Erstellen von Segmenten für Audiencen aus Echtzeitdaten zum Profil von Kunden.
- [Erlebnisdatenmodell (XDM)](../../xdm/home.md): Das standardisierte Framework, mit dem Platform Kundenerlebnisdaten organisiert.
- [Sandboxen](../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxen, die eine Instanz einer Platform in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

### Erforderliche Kopfzeilen

Für dieses Lernprogramm müssen Sie außerdem das [Authentifizierungstraining](../../tutorials/authentication.md) abgeschlossen haben, um erfolgreich Platform-APIs aufzurufen. Das Abschließen des Authentifizierungtutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform API-Aufrufen bereit, wie unten dargestellt:

- Genehmigung: Träger `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in der Experience Platform werden zu bestimmten virtuellen Sandboxen isoliert. Anforderungen an Platform-APIs erfordern einen Header, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird in:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxen in der Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Für alle POST-, PUT- und PATCH-Anforderungen ist ein zusätzlicher Header erforderlich:

- Content-Type: application/json

## Segment bewerten

Nachdem Sie Ihre Segmentdefinition entwickelt, getestet und gespeichert haben, können Sie das Segment entweder durch eine geplante Bewertung oder eine On-Demand-Bewertung bewerten.

[Die geplante Auswertung](#scheduled-evaluation) (auch als &quot;geplante Segmentierung&quot;bezeichnet) ermöglicht es Ihnen, einen wiederkehrenden Zeitplan für die Ausführung eines Exportauftrags zu einem bestimmten Zeitpunkt zu erstellen, während bei der [On-Demand-Auswertung](#on-demand-evaluation) ein Segmentauftrag erstellt werden muss, um die Audience sofort zu erstellen. Die Schritte für die einzelnen Schritte sind nachfolgend beschrieben.

Wenn Sie das Tutorial zum [Erstellen eines Segments mit der Echtzeit-Kundensegment-API](./create-a-segment.md) noch nicht abgeschlossen haben oder eine Segmentdefinition mit dem [Segmentaufbau](../ui/overview.md)erstellt haben, führen Sie dies bitte vor dem Fortfahren mit diesem Tutorial durch.

## Geplante Bewertung {#scheduled-evaulation}

Durch die geplante Auswertung kann Ihr IMS-Org einen wiederkehrenden Zeitplan erstellen, um Exportaufträge automatisch auszuführen.

>[!NOTE]
>
>Geplante Auswertung kann für Sandboxen mit maximal fünf (5) Zusammenführungsrichtlinien für XDM Individuelles Profil aktiviert werden. Wenn Ihr Unternehmen über mehr als fünf Richtlinien zum Zusammenführen von XDM-Profilen innerhalb einer einzelnen Sandbox-Umgebung verfügt, können Sie keine geplante Auswertung verwenden.

### Zeitplan erstellen

Wenn Sie eine POST-Anforderung an den `/config/schedules` Endpunkt senden, können Sie einen Zeitplan erstellen und die Uhrzeit einschließen, zu der der Zeitplan ausgelöst werden soll.

**API-Format**

```http
POST /config/schedules
```

**Anfrage**

Mit der folgenden Anforderung wird ein neuer Zeitplan basierend auf den in der Nutzlast bereitgestellten Spezifikationen erstellt.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "{SCHEDULE_NAME}",
        "type": "batch_segmentation",
        "properties": {
            "segments": ["*"]
        },
        "schedule": "0 0 1 * * ?",
        "state": "inactive"
        }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `name` | **(Erforderlich)** Der Name des Zeitplans. Muss eine Zeichenfolge sein. |
| `type` | **(Erforderlich)** Der Auftragstyp im Zeichenfolgenformat. Die unterstützten Typen sind `batch_segmentation` und `export`. |
| `properties` | **(Erforderlich)** Ein Objekt, das zusätzliche Eigenschaften im Zusammenhang mit dem Zeitplan enthält. |
| `properties.segments` | **(Erforderlich, wenn`type`gleich`batch_segmentation`)** Die Verwendung `["*"]` stellt sicher, dass alle Segmente einbezogen werden. |
| `schedule` | **(Erforderlich)** Eine Zeichenfolge, die den Auftragsplan enthält. Aufträge können nur einmal pro Tag ausgeführt werden, d. h., Sie können nicht planen, dass ein Auftrag mehr als einmal während eines Zeitraums von 24 Stunden ausgeführt wird. Das folgende Beispiel (`0 0 1 * * ?`) bedeutet, dass der Auftrag jeden Tag um 1:00:00 UTC ausgelöst wird. Weitere Informationen finden Sie in der Dokumentation zum [Cron-Ausdruck](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) . |
| `state` | *(Optional)* String, der den Planstatus enthält. Verfügbare Werte: `active` und `inactive`. Der Standardwert ist `inactive`. Eine IMS-Organisation kann nur einen Zeitplan erstellen. Schritte zum Aktualisieren des Zeitplans sind weiter unten in diesem Lernprogramm verfügbar. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details des neu erstellten Zeitplans zurück.

```json
{
    "id": "cd585edf-962d-420d-94ad-3be03e619ac2",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "e7e17720-c5bb-11e9-aafb-87c71c35cac8",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "{SCHEDULE_NAME}",
    "state": "inactive",
    "type": "batch_segmentation",
    "schedule": "0 0 1 * * ?",
    "properties": {
        "segments": [
            "*"
        ]
    },
    "createEpoch": 1568267948,
    "updateEpoch": 1568267948
}
```

### Zeitplan aktivieren

Standardmäßig ist ein Zeitplan bei der Erstellung inaktiv, es sei denn, die `state` Eigenschaft ist im Anforderungstext &quot;Erstellen&quot;(POST) auf `active` eingestellt. Sie können einen Zeitplan aktivieren ( `state` auf `active`), indem Sie eine PATCH-Anforderung an den `/config/schedules` Endpunkt senden und die ID des Zeitplans in den Pfad einschließen.

**API-Format**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Anfrage**

Die folgende Anforderung verwendet die [JSON-Patch-Formatierung](http://jsonpatch.com/) , um den Zeitplan `state` zu aktualisieren `active`.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules/cd585edf-962d-420d-94ad-3be03e619ac2 \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "op": "add",
          "path": "/state",
          "value": "active"
        }
      ]'
```

**Antwort**

Bei einer erfolgreichen Aktualisierung werden ein leerer Antworttext und HTTP-Status 204 (Kein Inhalt) zurückgegeben.

Derselbe Vorgang kann zum Deaktivieren eines Zeitplans verwendet werden, indem der &quot;Wert&quot;in der vorherigen Anforderung durch &quot;inaktiv&quot;ersetzt wird.

### Zeitplanaktualisierung

Die Zeitplanung kann aktualisiert werden, indem eine PATCH-Anforderung an den `/config/schedules` Endpunkt gesendet wird und die ID des Zeitplans im Pfad enthalten ist.

**API-Format**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Anfrage**

Die folgende Anforderung verwendet die [JSON-Patch-Formatierung](http://jsonpatch.com/) , um den [Cron-Ausdruck](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) für den Zeitplan zu aktualisieren. In diesem Beispiel wird der Zeitplan jetzt um 10:15:00 UTC ausgelöst.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules/cd585edf-962d-420d-94ad-3be03e619ac2 \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "op": "add",
          "path": "/schedule",
          "value": "0 15 10 * * ?"
        }
      ]'
```

**Antwort**

Bei einer erfolgreichen Aktualisierung werden ein leerer Antworttext und HTTP-Status 204 (Kein Inhalt) zurückgegeben.

## On-Demand-Bewertung

Mit der On-Demand-Auswertung können Sie einen Segmentauftrag erstellen, um bei Bedarf ein Audiencen-Segment zu generieren. Im Gegensatz zur geplanten Auswertung erfolgt dies nur auf Anfrage und nicht wiederholt.

### Erstellen eines Segmentauftrags

Ein Segmentauftrag ist ein asynchroner Vorgang, bei dem ein neues Audiencen-Segment erstellt wird. Er verweist auf eine Segmentdefinition sowie auf alle Zusammenführungsrichtlinien, die steuern, wie Echtzeit-Kundenattribute in Ihren Profil-Fragmenten überlappende Attribute zusammenführen. Nach erfolgreichem Abschluss eines Segmentauftrags können Sie verschiedene Segmentinformationen sammeln, z. B. Fehler, die während der Verarbeitung aufgetreten sind, und die endgültige Größe Ihrer Audience.

Sie können einen neuen Segmentauftrag erstellen, indem Sie eine POST-Anforderung an den `/segment/jobs` Endpunkt in der Echtzeit-Client-Profil-API senden.

**API-Format**

```http
POST /segment/jobs
```

**Anfrage**

Mit der folgenden Anforderung wird ein neuer Segmentauftrag basierend auf den beiden in der Nutzlast bereitgestellten Segmentdefinitionen erstellt.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "segmentId" : "42f49f2d-edb0-474f-b29d-2799d89cd5a6"
        },
        {
          "segmentId" : "54a20f19-9a0w-293a-9b82-409b1p3v0192"
        }
    ]'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `segmentId` | Der Bezeichner einer Segmentdefinition, aus der die Audience erstellt werden soll. Im Payload-Array muss mindestens eine Segment-ID angegeben werden. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details des neu erstellten Segmentauftrags zurück, einschließlich `id`eines schreibgeschützten, systemgenerierten Werts, der für diesen Segmentauftrag eindeutig ist.

```json
{
    "profileInstanceId": "ups",
    "computeJobId": 1,
    "id": "b0f99dde-6d3b-4d92-aa92-28072ded71a0",
    "status": "PROCESSING",
    "segments": [
        {
            "segmentId": "42f49f2d-edb0-474f-b29d-2799d89cd5a6",
            "segment": {
                "id": "42f49f2d-edb0-474f-b29d-2799d89cd5a6",
                "version": 1,
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "homeAddress.country = \"US\""
                },
                "mergePolicy": {
                    "id": "mpid1",
                    "version": 1
                }
            }
        },
        {
            "segmentId": "54a20f19-9a0w-293a-9b82-409b1p3v0192",
            "segment": {
                "id": "54a20f19-9a0w-293a-9b82-409b1p3v0192",
                "version": 1,
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "homeAddress.country = \"US\""
                },
                "mergePolicy": {
                    "id": "mpid1",
                    "version": 1
                }
            }
        }
    ],
    "updateTime": 1533581808162,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1533581808162,
    "_links": {
        "cancel": {
            "href": "/segment/jobs/b0f99dde-6d3b-4d92-aa92-28072ded71a0",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/b0f99dde-6d3b-4d92-aa92-28072ded71a0",
            "method": "GET"
        }
    }
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `id` | Der Bezeichner des neuen Segmentauftrags, der für Nachschlagezwecke verwendet wird. |
| `status` | Der aktuelle Status des Segmentauftrags. Wird &quot;VERARBEITUNG&quot;, bis die Verarbeitung abgeschlossen ist, und wird dann &quot;ERFOLGT&quot; oder &quot;FEHLGESCHLAGEN&quot;. |

### Status des Segmentauftrags suchen

Sie können den `id` für einen bestimmten Segmentauftrag verwenden, um eine Nachschlageanforderung (GET) durchzuführen, um den aktuellen Auftragsstatus Ansicht.

**API-Format**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{SEGMENT_JOB_ID}` | Der `id` Segmentauftrag, auf den Sie zugreifen möchten. |

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/segment/jobs/80388706-29fa-40d3-81cf-a297d0224ad9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details des Segmentierungsauftrags zurück und stellt je nach aktuellem Auftragsstatus unterschiedliche Informationen bereit. Sie können die Suchanfrage wiederholen, bis der Wert &quot;ERFOLGT&quot; `status` erreicht ist. Anschließend können Sie das Segment in einen Datensatz exportieren.


```json
{
    "profileInstanceId": "ups",
    "errors": [],
    "computeJobId": 13377,
    "modelName": "_xdm.context.profile",
    "id": "80388706-29fa-40d3-81cf-a297d0224ad9",
    "status": "SUCCEEDED",
    "segments": [
        {
            "segmentId": "b560a09a-de85-4a1c-8477-2f3da1d9e86b",
            "segment": {
                "id": "b560a09a-de85-4a1c-8477-2f3da1d9e86b",
                "version": 1,
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "homeAddress.country = \"US\""
                },
                "mergePolicy": {
                    "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
                    "version": 1
                }
            }
        }
    ],
    "requestId": "prgu92v4VNvsGuuXticcsqX96UXGjXtS",
    "computeGatewayJobId": "a7c33b77-3aeb-497f-bc88-807915c57b5f",
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1547063631503,
            "endTimeInMs": 1547063731181,
            "totalTimeInMs": 99678
        },
        "profileSegmentationTime": {
            "startTimeInMs": 1547063669001,
            "endTimeInMs": 1547063720887,
            "totalTimeInMs": 51886
        },
        "segmentedProfileCounter": {
            "ca763983-5572-4ea4-809c-b7dff7e0d79b": 4195,
            "251e3a1f-645c-4444-836b-18e6b668bdf8": 0,
            "3da8bad9-29fb-40e0-b39e-f80322e964de": 0,
            "30230300-ccf1-48ad-8012-c5563a007069": 0
        },
        "segmentedProfileByNamespaceCounter": {
            "ca763983-5572-4ea4-809c-b7dff7e0d79b": {
                "email": 4195
            },
            "251e3a1f-645c-4444-836b-18e6b668bdf8": {},
            "3da8bad9-29fb-40e0-b39e-f80322e964de": {},
            "30230300-ccf1-48ad-8012-c5563a007069": {}
        }     
    },
    "updateTime": 1547063731181,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1547063631503,
    "_links": {
        "cancel": {
            "href": "/segment/jobs/80388706-29fa-40d3-81cf-a297d0224ad9",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/80388706-29fa-40d3-81cf-a297d0224ad9",
            "method": "GET"
        }
    }
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `segmentedProfileCounter` | Die Gesamtzahl der zusammengeführten Profil, die für das Segment infrage kommen. |
| `segmentedProfileByNamespaceCounter` | Eine Aufschlüsselung der Profil, die für das Namensraum infrage kommen, nach Identitäts-Code. Eine Liste der Identitäts-Namensraum-Codes finden Sie in der Übersicht über den [Identitäts-Namensraum](../../identity-service/namespaces.md). |

## Segmentergebnisse interpretieren

Wenn Segmentaufträge erfolgreich ausgeführt werden, wird die `segmentMembership` Zuordnung für jedes Profil im Segment aktualisiert. `segmentMembership` speichert auch alle vorab ausgewerteten Audiencen, die in die Platform eingebunden werden, was eine Integration mit anderen Lösungen wie Adobe Audience Manager ermöglicht.

Das folgende Beispiel zeigt, wie das `segmentMembership` Attribut für jeden einzelnen Profil-Datensatz aussieht:

```json
{
  "segmentMembership": {
    "UPS": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "timestamp": "2018-04-26T15:52:25+00:00",
        "status": "existing"
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "status": "realized"
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "status": "exited"
      }
    }
  }
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `lastQualificationTime` | Der Zeitstempel, zu dem die Zusicherung der Segmentmitgliedschaft erfolgte und das Profil das Segment ein- oder ausstieg. |
| `status` | Der Status der Segmentbeteiligung als Teil der aktuellen Anforderung. muss einem der folgenden bekannten Werte entsprechen: <ul><li>`existing`: Die Entität befindet sich weiterhin im Segment.</li><li>`realized`: Entität tritt in das Segment ein.</li><li>`exited`: Entität beendet das Segment.</li></ul> |

## Zugriff auf Segmentergebnisse

Auf die Ergebnisse eines Segmentauftrags kann auf zwei Arten zugegriffen werden: Sie können auf einzelne Profil zugreifen oder eine ganze Audience in einen Datensatz exportieren.

Die folgenden Abschnitte beschreiben diese Optionen detaillierter.

## Profil nachschlagen

Wenn Sie das spezifische Profil kennen, auf das Sie zugreifen möchten, können Sie dies mit der Echtzeit-Client-Profil-API tun. Die vollständigen Schritte für den Zugriff auf einzelne Profil finden Sie in der Anleitung zum [Zugriff auf Echtzeit-Kundendaten mithilfe der Profil-API](../../profile/api/entities.md) .

## Segment exportieren {#export}

Nachdem ein Segmentierungsauftrag erfolgreich abgeschlossen wurde (der `status` Attributwert &quot;ERFOLGT&quot;ist), können Sie Ihre Audience in ein Dataset exportieren, in dem darauf zugegriffen und darauf reagiert werden kann.

Die folgenden Schritte sind erforderlich, um Ihre Audience zu exportieren:

- [Erstellen Sie einen Dataset](#create-a-target-dataset) der Zielgruppe - Erstellen Sie den Datensatz, der Audiencen enthält.
- [Generieren von Profilen zur Audience im Datensatz](#generate-profiles-for-audience-members) - Füllen Sie den Datensatz mit XDM-Profilen auf Basis der Ergebnisse eines Segmentauftrags.
- [Überwachung des Exportfortschritts](#monitor-export-progress) - Überprüfen Sie den aktuellen Fortschritt des Exportprozesses.
- [Lesen Sie die Daten](#next-steps) zur Audience - Rufen Sie die resultierenden XDM-Profil für die Mitglieder Ihrer Audience ab.

### Zielgruppen-Dataset erstellen

Beim Exportieren einer Audience muss zunächst ein Zielgruppe-Datensatz erstellt werden. Es ist wichtig, dass der Datensatz korrekt konfiguriert wird, um sicherzustellen, dass der Export erfolgreich ist.

Eine der wichtigsten Überlegungen ist das Schema, auf dem der Datensatz basiert (`schemaRef.id` in der unten stehenden API-Musteranforderung). Um ein Segment zu exportieren, muss der Datensatz auf dem XDM Individual Profil Vereinigung Schema (`https://ns.adobe.com/xdm/context/profile__union`) basieren. Ein Vereinigung-Schema ist ein systemgeneriertes, schreibgeschütztes Schema, das die Felder von Schemas, die dieselbe Klasse besitzen, Aggregat gibt, in diesem Fall die XDM-Klasse Individuelles Profil. Weitere Informationen zu Schemas der Vereinigung Ansicht finden Sie im Abschnitt zum [Echtzeit-Kundenmanagement im Schema Registry-Entwicklerhandbuch](../../xdm/api/getting-started.md).

Es gibt zwei Möglichkeiten, den erforderlichen Datensatz zu erstellen:

- **Verwenden von APIs:** In den folgenden Schritten wird beschrieben, wie Sie ein Dataset erstellen, das auf das Schema zur Vereinigung einzelner XDM-Profil mithilfe der Katalog-API verweist.
- **Verwenden der Benutzeroberfläche:** Um mithilfe der Benutzeroberfläche &quot;Adobe Experience Platform&quot;einen Datensatz zu erstellen, der auf das Schema &quot;Vereinigung&quot;verweist, führen Sie die Schritte im [UI-Lernprogramm](../ui/overview.md) aus und kehren Sie dann zu diesem Lernprogramm zurück, um mit den Schritten zum [Generieren von Profilen](#generate-xdm-profiles-for-audience-members)der Audience fortzufahren.

Wenn Sie bereits über einen kompatiblen Datensatz verfügen und dessen ID kennen, können Sie direkt mit dem Schritt zum [Generieren von Profilen](#generate-xdm-profiles-for-audience-members)zur Audience fortfahren.

**API-Format**

```http
POST /dataSets
```

**Anfrage**

Mit der folgenden Anforderung wird ein neuer Datensatz erstellt, der Konfigurationsparameter in der Nutzlast bereitstellt.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Segment Export",
    "schemaRef": {
        "id": "https://ns.adobe.com/xdm/context/profile__union",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    }
}'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `name` | Ein beschreibender Name für den Datensatz. |
| `schemaRef.id` | Die ID der Vereinigung-Ansicht (Schema), der der Datensatz zugeordnet werden soll. |
| `fileDescription.persisted` | Ein boolescher Wert, der bei Festlegung auf `true`die Persistenz des Datensatzes in der Ansicht &quot;Vereinigung&quot;ermöglicht. |

**Antwort**

Eine erfolgreiche Antwort gibt ein Array zurück, das die schreibgeschützte, systemgenerierte eindeutige ID des neu erstellten Datensatzes enthält. Für den erfolgreichen Export von Audiencen-Mitgliedern ist eine ordnungsgemäß konfigurierte Dataset-ID erforderlich.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Generieren von Profilen für Audiencen-Mitglieder

Sobald Sie über einen Datensatz mit Vereinigung-Speicherung verfügen, können Sie einen Exportauftrag erstellen, um die Audiencen im Datensatz zu erhalten, indem Sie eine POST-Anforderung an den `/export/jobs` Endpunkt in der Echtzeit-Client-Profil-API senden und die Dataset-ID und Segmentinformationen für die Segmente bereitstellen, die Sie exportieren möchten.

**API-Format**

```http
POST /export/jobs
```

**Anfrage**

Mit der folgenden Anforderung wird ein neuer Exportauftrag erstellt, der Konfigurationsparameter in der Nutzlast bereitstellt.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ],
      "segmentQualificationTime": {
            "startTime": "2019-09-01T00:00:00Z",
            "endTime": "2019-09-02T00:00:00Z"
        },
      "fromIngestTimestamp": "2018-10-25T13:22:04-07:00",
      "emptyProfiles": false
    },
    "additionalFields" : {
      "eventList": {
        "fields": "environment.browserDetails.name,environment.browserDetails.version",
        "filter": {
          "fromIngestTimestamp": "2018-10-25T13:22:04-07:00"
        }
      }
    },
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": true
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `fields` | *(Optional)* Beschränkt die Datenfelder, die in den Export einbezogen werden sollen, auf die in diesem Parameter bereitgestellten Felder. Derselbe Parameter ist auch bei der Erstellung eines Segments verfügbar. Daher wurden die Felder im Segment möglicherweise bereits gefiltert. Wird dieser Wert nicht angegeben, werden alle Felder in die exportierten Daten einbezogen |
| `mergePolicy` | *(Optional)* Gibt die Richtlinie zum Zusammenführen an, die für die exportierten Daten gilt. Schließen Sie diesen Parameter ein, wenn mehrere Segmente exportiert werden. Wird dieser Wert nicht angegeben, verwendet der Exportdienst die vom Segment bereitgestellte Mergerichtlinie. |
| `mergePolicy.id` | Die ID der Richtlinie zum Zusammenführen |
| `mergePolicy.version` | Die spezifische Version der zu verwendenden Mergerichtlinie. Wenn Sie diesen Wert auslassen, wird standardmäßig die neueste Version verwendet. |
| `filter` | *(Optional)* Gibt einen oder mehrere der folgenden Filter an, die vor dem Exportieren auf das Segment angewendet werden sollen: |
| `filter.segments` | *(Optional)* Gibt die zu exportierenden Segmente an. Wird dieser Wert nicht angegeben, werden alle Daten aus allen Profilen exportiert. Akzeptiert ein Array von Segmentobjekten, die jeweils die folgenden Felder enthalten: |
| `filter.segments.segmentId` | **(Erforderlich bei Verwendung`segments`)** der Segment-ID für Profil, die exportiert werden sollen. |
| `filter.segments.segmentNs` | *(Optional)* Segmentcode für den jeweiligen Namensraum `segmentID`. |
| `filter.segments.status` | *(Optional)* Ein Array von Zeichenfolgen, das einen Statusfilter für die `segmentID`Zeichenfolge bereitstellt. Standardmäßig `status` wird der Wert `["realized", "existing"]` verwendet, der alle Profil darstellt, die zum aktuellen Zeitpunkt in das Segment fallen. Mögliche Werte sind: `"realized"`, `"existing"`und `"exited"`. |
| `filter.segmentQualificationTime` | *(Optional)* Filtern Sie nach der Segmentqualifizierungszeit. Die Beginn- und/oder Endzeit können angegeben werden. |
| `filter.segmentQualificationTime.startTime` | *(Optional)* Segmentqualifizierungs-Beginn für eine Segment-ID für einen bestimmten Status. Es wurde nicht angegeben, es wird kein Filter für die Zeit des Beginns für eine Segment-ID-Qualifizierung angezeigt. Der Zeitstempel muss im [RFC 3339](https://tools.ietf.org/html/rfc3339) -Format angegeben werden. |
| `filter.segmentQualificationTime.endTime` | *(Optional)* Endzeit der Segmentqualifizierung für eine Segment-ID für einen bestimmten Status. Es wurde kein Filter für die Endzeit einer Segment-ID-Qualifizierung bereitgestellt. Der Zeitstempel muss im [RFC 3339](https://tools.ietf.org/html/rfc3339) -Format angegeben werden. |
| `filter.fromIngestTimestamp` | *(Optional)* Beschränkt exportierte Profil auf diejenigen, die nach diesem Zeitstempel aktualisiert wurden. Der Zeitstempel muss im [RFC 3339](https://tools.ietf.org/html/rfc3339) -Format angegeben werden. |
| `filter.fromIngestTimestamp` für **Profile**, falls vorhanden | Umfasst alle zusammengeführten Profil, bei denen der zusammengeführte aktualisierte Zeitstempel größer als der angegebene Zeitstempel ist. Unterstützt `greater_than` Operand. |
| `filter.fromTimestamp` für Ereignisse | Alle nach diesem Zeitstempel erfassten Ereignis werden entsprechend dem resultierenden Profil exportiert. Dies ist nicht die Ereignis-Zeit selbst, sondern die Aufnahmezeit für die Ereignisse. |
| `filter.emptyProfiles` | *(Optional)* Boolescher Wert. Profil können Profil-Datensätze, ExperienceEvent-Datensätze oder beides enthalten. Profil ohne Profil-Datensätze und nur ExperienceEvent-Datensätze werden als &quot;emptyProfiles&quot;bezeichnet. Um alle Profil im Profil-Store einschließlich &quot;emptyProfiles&quot;zu exportieren, setzen Sie den Wert `emptyProfiles` auf `true`. Wenn `emptyProfiles` dies auf `false`festgelegt ist, werden nur Profil mit Profil-Datensätzen im Store exportiert. Wenn `emptyProfiles` das Attribut nicht enthalten ist, werden standardmäßig nur Profil exportiert, die Profil-Datensätze enthalten. |
| `additionalFields.eventList` | *(Optional)* Steuert die Zeitreihen-Ereignis-Felder, die für untergeordnete oder zugehörige Objekte exportiert werden, indem eine oder mehrere der folgenden Einstellungen bereitgestellt werden: |
| `additionalFields.eventList.fields` | Steuerung der zu exportierenden Felder. |
| `additionalFields.eventList.filter` | Gibt Kriterien an, die die Ergebnisse verknüpfter Objekte einschränken. Erwartet einen für den Export erforderlichen Mindestwert, normalerweise ein Datum. |
| `additionalFields.eventList.filter.fromIngestTimestamp` | Filter erhalten Zeitreihen-Ereignis zu denen, die nach dem bereitgestellten Zeitstempel erfasst wurden. Dies ist nicht die Ereignis-Zeit selbst, sondern die Aufnahmezeit für die Ereignisse. |
| `destination` | **(Erforderlich)** Zielinformationen für die exportierten Daten |
| `destination.datasetId` | **(Erforderlich)** Die ID des Datensatzes, in den Daten exportiert werden sollen. |
| `destination.segmentPerBatch` | *(Optional)* Ein boolescher Wert, der, falls nicht angegeben, standardmäßig `false`lautet. Beim Wert `false` werden alle Segment-IDs in eine einzige Stapel-ID exportiert. Ein Wert von `true` exportiert eine Segment-ID in eine Stapel-ID. Beachten Sie, dass die Einstellung des Werts sich auf die Exportleistung des Stapels auswirken `true` kann. |
| `schema.name` | **(Erforderlich)** Der Name des Schemas, das mit dem Datensatz verknüpft ist, in den Daten exportiert werden sollen. |

**Antwort**

Eine erfolgreiche Antwort gibt einen Datensatz zurück, der mit Profilen gefüllt ist, die für die letzte abgeschlossene Ausführung des Segmentauftrags qualifiziert sind. Alle Profil, die im Datensatz bereits vorhanden waren, sich aber während der letzten abgeschlossenen Ausführung des Segmentauftrags nicht für das Segment qualifiziert haben, wurden entfernt.

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "NEW",
    "requestId": "IwkVcD4RupdSmX376OBVORvcvTdA4ypN",
    "computeGatewayJobId": {},
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1559674261657
        }
    },
    "destination": {
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

Wenn `destination.segmentPerBatch` sie nicht in die Anforderung einbezogen wurde (falls sie nicht vorhanden ist, wird sie standardmäßig auf `false`) oder der Wert auf festgelegt wurde `false`, hätte das `destination` Objekt in der Antwort oben kein `batches` Array und würde stattdessen nur ein `batchId`wie unten dargestellt enthalten. Dieser einzelne Stapel würde alle Segment-IDs enthalten, während die obige Antwort eine einzelne Segment-ID pro Stapel-ID anzeigt.

```json
  "destination": {
    "datasetId": "5cf6bcf79ecc7c14530fe436",
    "segmentPerBatch": false,
    "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
  }
```

### Liste aller Exportaufträge

Sie können eine Liste aller Exportaufträge für eine bestimmte IMS-Organisation zurückgeben, indem Sie eine GET-Anforderung an den `export/jobs` Endpunkt ausführen. Die Anforderung unterstützt auch die Abfrage Parameter `limit` und `offset`, wie unten dargestellt.

**API-Format**

```http
GET /export/jobs
GET /export/jobs?limit=4
GET /export/jobs?offset=2
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `limit` | Geben Sie die Anzahl der zurückzugebenden Datensätze an. |
| `offset` | Versetzen Sie die Seite der Ergebnisse, die durch die angegebene Zahl zurückgegeben werden sollen. |


**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Die Antwort enthält ein `records` Objekt, das die von Ihrer IMS-Organisation erstellten Exportaufträge enthält.

```json
{
  "records": [
    {
      "profileInstanceId": "ups",
      "jobType": "BATCH",
      "filter": {
          "segments": [
              {
                  "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff"
              }
          ]
      },
      "id": 726,
      "schema": {
          "name": "_xdm.context.profile"
      },
      "mergePolicy": {
          "id": "timestampOrdered-none-mp",
          "version": 1
      },
      "status": "SUCCEEDED",
      "requestId": "d995479c-8a08-4240-903b-af469c67be1f",
      "computeGatewayJobId": {
          "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94",
          "pushJob": "feaeca05-d137-4605-aa4e-21d19d801fc6"
      },
      "metrics": {
          "totalTime": {
              "startTimeInMs": 1538615973895,
              "endTimeInMs": 1538616233239,
              "totalTimeInMs": 259344
          },
          "profileExportTime": {
              "startTimeInMs": 1538616067445,
              "endTimeInMs": 1538616139576,
              "totalTimeInMs": 72131
          },
          "aCPDatasetWriteTime": {
              "startTimeInMs": 1538616195172,
              "endTimeInMs": 1538616195715,
              "totalTimeInMs": 543
          }
      },
      "destination": {
          "datasetId": "5b7c86968f7b6501e21ba9df",
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
      },
      "updateTime": 1538616233239,
      "imsOrgId": "{IMS_ORG}",
      "creationTime": 1538615973895
    },
    {
      "profileInstanceId": "test_xdm_latest_profile_20_e2e_1538573005395",
      "errors": [
        {
          "code": "0090000009",
          "msg": "Error writing profiles to output path 'adl://va7devprofilesnapshot.azuredatalakestore.net/snapshot/722'",
          "callStack": "com.adobe.aep.unifiedprofile.common.logging.Logger" 
        },
        {
          "code": "unknown",
          "msg": "Job aborted.",
          "callStack": "org.apache.spark.SparkException: Job aborted."
        }
      ],
      "jobType": "BATCH",
      "filter": {
        "segments": [
            {
                "segmentId": "7a93d2ff-a220-4bae-9a4e-5f3c35032be3"
            }
        ]
      },
      "id": 722,
      "schema": {
          "name": "_xdm.context.profile"
      },
      "mergePolicy": {
          "id": "7972e3d6-96ea-4ece-9627-cbfd62709c5d",
          "version": 1
      },
      "status": "FAILED",
      "requestId": "KbOAsV7HXmdg262lc4yZZhoml27UWXPZ",
      "computeGatewayJobId": {
          "exportJob": "15971e0f-317c-4390-9038-1a0498eb356f"
      },
      "metrics": {
          "totalTime": {
              "startTimeInMs": 1538573416687,
              "endTimeInMs": 1538573922551,
              "totalTimeInMs": 505864
          },
          "profileExportTime": {
              "startTimeInMs": 1538573872211,
              "endTimeInMs": 1538573918809,
              "totalTimeInMs": 46598
          }
      },
      "destination": {
          "datasetId": "5bb4c46757920712f924a3eb",
          "batchId": ""
      },
      "updateTime": 1538573922551,
      "imsOrgId": "{IMS_ORG}",
      "creationTime": 1538573416687
    }
  ],
  "page": {
      "sortField": "createdTime",
      "sort": "desc",
      "pageOffset": "1538573416687_722",
      "pageSize": 2
  },
  "link": {
      "next": "/export/jobs/?limit=2&offset=1538573416687_722"
  }
}
```

### Überwachung des Exportfortschritts

Als Exportauftragsprozess können Sie den Status überwachen, indem Sie eine GET-Anforderung an den `/export/jobs` Endpunkt senden und den Pfad `id` des Exportauftrags einschließen. Der Exportauftrag ist abgeschlossen, sobald das `status` Feld den Wert &quot;SUCCEEDED&quot;zurückgibt.

**API-Format**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | Der `id` Exportauftrag, auf den Sie zugreifen möchten. |

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/24115 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "SUCCEEDED",
    "requestId": "YwMt1H8QbVlGT2pzyxgwFHTwzpMbHrTq",
    "computeGatewayJobId": {
      "exportJob": "305a2e5c-2cf3-4746-9b3d-3c5af0437754",
      "pushJob": "963f275e-91a3-4fa1-8417-d2ca00b16a8a"
    },
    "metrics": {
      "totalTime": {
        "startTimeInMs": 1547053539564,
        "endTimeInMs": 1547054743929,
        "totalTimeInMs": 1204365
      },
      "profileExportTime": {
        "startTimeInMs": 1547053667591,
        "endTimeInMs": 1547053778195,
        "totalTimeInMs": 110604
      },
      "aCPDatasetWriteTime": {
        "startTimeInMs": 1547054660416,
        "endTimeInMs": 1547054698918,
        "totalTimeInMs": 38502
      }
    },
    "destination": {
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `batchId` | Der Bezeichner der Stapel, die aus einem erfolgreichen Export erstellt wurden und für Nachschlagezwecke beim Lesen der Daten zur Audience verwendet werden. |

## Nächste Schritte

Nach erfolgreichem Abschluss des Exports sind Ihre Daten im Data Lake in der Experience Platform verfügbar. Sie können dann mit der [Datenzugriff-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) auf die Daten zugreifen, indem Sie die mit dem Export verknüpfte `batchId` Datei verwenden. Je nach Größe des Segments können die Daten in Blöcken vorliegen und der Stapel kann aus mehreren Dateien bestehen.

Eine schrittweise Anleitung zum Zugriff auf und Herunterladen von Stapeldateien mit der Datenzugriff-API finden Sie im Lernprogramm [Datenzugriff](../../data-access/tutorials/dataset-data.md).

Sie können auch über den Adobe Experience Platform Abfrage Service auf erfolgreich exportierte Segmentdaten zugreifen. Mithilfe der Benutzeroberfläche oder RESTful-API können Sie mit dem Abfrage Service Abfragen für Daten im Data Lake schreiben, überprüfen und ausführen.

Weitere Informationen zur Abfrage von Audiencen finden Sie in der Dokumentation zum [Abfrage Service](../../query-service/home.md).
