---
description: Auf dieser Seite wird der API-Aufruf veranschaulicht, der zum Erstellen einer Zielgruppenvorlage über Adobe Experience Platform Destination SDK verwendet wird.
title: Erstellen einer Zielgruppenvorlage
exl-id: 98d30002-d462-4008-9337-7de0cd608194
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 88%

---

# Erstellen einer Zielgruppenvorlage

>[!IMPORTANT]
>
>**API-Endpunkt**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Für einige Ziele, die mit Destination SDK erstellt wurden, müssen Sie eine Zielgruppen-Metadatenkonfiguration erstellen, um Zielgruppenmetadaten im Ziel programmgesteuert zu erstellen, zu aktualisieren oder zu löschen. Auf dieser Seite erfahren Sie, wie Sie den API-Endpunkt `/authoring/audience-templates` zum Erstellen der Konfiguration verwenden.

Eine ausführliche Beschreibung der Funktionen, die Sie über diesen Endpunkt konfigurieren können, finden Sie unter [Verwaltung von Zielgruppen-Metadaten](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Bei allen von Destination SDK unterstützten Parameternamen und Werten wird **nach Groß-/Kleinschreibung unterschieden**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Erste Schritte mit API-Vorgängen für Zielgruppenvorlagen {#get-started}

Bevor Sie fortfahren, lesen Sie [Erste Schritte](../getting-started.md). Dort finden Sie die nötigen Informationen für den erfolgreichen Aufruf der API, einschließlich Details für den Abruf der erforderlichen Authoring-Berechtigung für Ziele und zu den erforderlichen Kopfzeilen.

## Erstellen einer Zielgruppenvorlage {#create}

Sie können eine neue Zielgruppenvorlage erstellen, indem Sie eine `POST`-Anfrage an den Endpunkt `/authoring/audience-templates` stellen.

**API-Format**

```http
POST /authoring/audience-templates
```

+++Anfrage

Die folgende Anfrage erstellt eine neue Zielgruppenvorlage, die durch die in der Payload angegebenen Parameter konfiguriert wird. Die nachstehende Payload enthält alle Parameter, die vom Endpunkt `/authoring/audience-templates` akzeptiert werden. Beachten Sie, dass Sie nicht alle Parameter für den Aufruf hinzufügen müssen und dass die Vorlage entsprechend Ihren API-Anforderungen angepasst werden kann.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/audience-templates \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
  "metadataTemplate": {
    "name": "Test Webhook Audience Template",
    "create": {
      "url": "https://your-webhook-site/0bd222fa-8ae2-433b-8f0e-f2ce137b0ee4/{{customerData.customerID}}/segments",
      "httpMethod": "POST",
      "headers": [
        {
          "value": "application/json",
          "header": "Content-Type"
        },
        {
          "value": "Bearer {{authData.token}}",
          "header": "Authorization"
        }
      ],
      "requestBody": {
        "json": {
          "name": "{{segment.name}}",
          "type": "segment",
          "metadata": {
            "org_id": "{{destination.imsOrgId}}",
            "sandbox": "{{destination.sandboxName}}",
            "destination_id": "{{destination.id}}",
            "destination_name": "{{destination.name}}",
            "segmentEnrichmentAttributes": "{% set columns = [] %}{% for atr in segmentEnrichmentAttributes %}{% set columns = columns|merge([atr.source]) %}{% endfor %}{{ columns | toJson }}"
          },
          "external_id": "{{segment.id}}"
        }
      },
      "responseFields": [
        {
          "value": "{{headers.X-Request-Id}}",
          "name": "externalAudienceId"
        }
      ],
      "responseErrorFields": [
        {
          "value": "{{root}}",
          "name": "message"
        }
      ]
    },
    "update": {
      "url": "https://your-webhook-site/0bd222fa-8ae2-433b-8f0e-f2ce137b0ee4/{{customerData.customerID}}/segments/{{segment.alias}}",
      "httpMethod": "PUT",
      "headers": [
        {
          "value": "application/json",
          "header": "Content-Type"
        },
        {
          "value": "Bearer {{authData.token}}",
          "header": "Authorization"
        }
      ],
      "requestBody": {
        "json": {
          "name": "{{segment.name}}",
          "type": "segment",
          "metadata": {
            "org_id": "{{destination.imsOrgId}}",
            "sandbox": "{{destination.sandboxName}}",
            "destination_id": "{{destination.id}}",
            "destination_name": "{{destination.name}}",
            "segmentEnrichmentAttributes": "{% set columns = [] %}{% for atr in segmentEnrichmentAttributes %}{% set columns = columns|merge([atr.source]) %}{% endfor %}{{ columns | toJson }}"
          },
          "external_id": "{{segment.id}}"
        }
      },
      "responseFields": [
        {
          "value": "{{headers.X-Request-Id}}",
          "name": "externalAudienceId"
        }
      ],
      "responseErrorFields": [
        {
          "value": "{{root}}",
          "name": "message"
        }
      ]
    },
    "delete": {
      "url": "https://your-webhook-site/0bd222fa-8ae2-433b-8f0e-f2ce137b0ee4/{{customerData.customerID}}/segments/{{segment.alias}}",
      "httpMethod": "DELETE",
      "headers": [
        {
          "value": "Bearer {{authData.token}}",
          "header": "Authorization"
        }
      ],
      "responseErrorFields": [
        {
          "value": "{{root}}",
          "name": "message"
        }
      ]
    },
    "createDestination": {
      "url": "https://your-webhook-site/0bd222fa-8ae2-433b-8f0e-f2ce137b0ee4/{{customerData.customerID}}/createDestination",
      "httpMethod": "POST",
      "headers": [
        {
          "value": "application/json",
          "header": "Content-Type"
        },
        {
          "value": "Bearer {{authData.token}}",
          "header": "Authorization"
        }
      ],
      "requestBody": {
        "json": {
          "name": "{{destination.name}}",
          "type": "destination",
          "metadata": {
            "org_id": "{{destination.imsOrgId}}",
            "sandbox": "{{destination.sandboxName}}",
            "destination_id": "{{destination.id}}",
            "destination_name": "{{destination.name}}",
            "enrichmentAttributes": "{{destination.enrichmentAttributes}}"
          },
          "external_id": "{{destination.id}}"
        }
      },
      "responseFields": [
        {
          "value": "{{headers.X-Request-Id}}",
          "name": "externalAudienceId"
        }
      ],
      "responseErrorFields": [
        {
          "value": "{{root}}",
          "name": "message"
        }
      ]
    },
    "updateDestination": {
      "url": "https://your-webhook-site/0bd222fa-8ae2-433b-8f0e-f2ce137b0ee4/{{customerData.customerID}}/updateDestination",
      "httpMethod": "POST",
      "headers": [
        {
          "value": "application/json",
          "header": "Content-Type"
        },
        {
          "value": "Bearer {{authData.token}}",
          "header": "Authorization"
        }
      ],
      "requestBody": {
        "json": {
          "name": "{{destination.name}}",
          "type": "destination",
          "metadata": {
            "org_id": "{{destination.imsOrgId}}",
            "sandbox": "{{destination.sandboxName}}",
            "destination_id": "{{destination.id}}",
            "destination_name": "{{destination.name}}",
            "enrichmentAttributes": "{{destination.enrichmentAttributes}}"
          },
          "external_id": "{{destination.id}}"
        }
      },
      "responseFields": [
        {
          "value": "{{headers.X-Request-Id}}",
          "name": "externalAudienceId"
        }
      ],
      "responseErrorFields": [
        {
          "value": "{{root}}",
          "name": "message"
        }
      ]
    },
    "deleteDestination": {
      "url": "https://your-webhook-site/0bd222fa-8ae2-433b-8f0e-f2ce137b0ee4/{{customerData.customerID}}/deleteDestination",
      "httpMethod": "DELETE",
      "headers": [
        {
          "value": "Bearer {{authData.token}}",
          "header": "Authorization"
        }
      ],
      "responseErrorFields": [
        {
          "value": "{{root}}",
          "name": "message"
        }
      ]
    }
  },
  "validations":[
      {
         "field":"string",
         "regex":"string"
      }
   ]
}'
```

| Eigenschaft | Typ | Beschreibung |
| -------- | ----------- | ----------- |
| `name` | Zeichenfolge | Der Name der Zielgruppen-Metadatenvorlage für Ihr Ziel. Dieser Name wird in jeder partnerspezifischen Fehlermeldung in der Benutzeroberfläche von Experience Platform angezeigt. |
| `url` | String | Die URL und der Endpunkt Ihrer API, die zum Erstellen, Aktualisieren, Löschen oder Validieren von Audiences und/oder Datenflüssen in Ihrer Plattform verwendet wird. Zwei branchenübliche Beispiele sind `https://adsapi.snapchat.com/v1/adaccounts/{{customerData.accountId}}/segments` und `https://api.linkedin.com/v2/dmpSegments/{{segment.alias}}`. |
| `httpMethod` | Zeichenfolge | Die Methode, die für Ihren Endpunkt verwendet wird, um die Zielgruppe in Ihrem Ziel programmgesteuert zu erstellen, zu aktualisieren, zu löschen oder zu validieren. Beispiel: `POST`, `PUT`, `DELETE` |
| `headers.header` | Zeichenfolge | Gibt alle HTTP-Header an, die zum Aufruf Ihrer API hinzugefügt werden sollen. Beispiel: `"Content-Type"` |
| `headers.value` | Zeichenfolge | Gibt den Wert von HTTP-Headern an, die zum Aufruf Ihrer API hinzugefügt werden sollen. Beispiel: `"application/x-www-form-urlencoded"` |
| `requestBody` | Zeichenfolge | Gibt den Inhalt des Nachrichtentextes an, der an Ihre API gesendet werden soll. Welche Parameter zum Objekt `requestBody` hinzugefügt werden sollten, hängt davon ab, welche Felder Ihre API akzeptiert. In der [Dokumentation zu unterstützten Makros](../functionality/audience-metadata-management.md#macros) erfahren Sie, was Sie in den Nachrichtentext einfügen können. |
| `responseFields.name` | Zeichenfolge | Geben Sie alle Antwortfelder an, die Ihre API beim Aufruf zurückgibt. Ein Beispiel finden Sie im Abschnitt [Vorlagenbeispiele](../functionality/audience-metadata-management.md#examples) im Dokument über die Funktionalität von Zielgruppen-Metadaten. |
| `responseFields.value` | Zeichenfolge | Geben Sie den Wert aller Antwortfelder an, die Ihre API beim Aufruf zurückgibt. |
| `responseErrorFields.name` | Zeichenfolge | Geben Sie alle Antwortfelder an, die Ihre API beim Aufruf zurückgibt. Ein Beispiel finden Sie im Abschnitt [Vorlagenbeispiele](../functionality/audience-metadata-management.md#examples) im Dokument über die Funktionalität von Zielgruppen-Metadaten. |
| `responseErrorFields.value` | Zeichenfolge | Analysiert alle Fehlermeldungen, die bei Antworten auf API-Aufrufe von Ihrem Ziel zurückgegeben werden. Diese Fehlermeldungen werden Benutzerinnen und Benutzern in der Benutzeroberfläche von Experience Platform angezeigt. |
| `validations.field` | Zeichenfolge | Gibt an, ob Überprüfungen für Felder durchgeführt werden sollen, bevor API-Aufrufe an Ihr Ziel gesendet werden. Sie können beispielsweise `{{validations.accountId}}` verwenden, um die Konto-ID des Benutzers zu überprüfen. |
| `validations.regex` | Zeichenfolge | Gibt an, wie das Feld strukturiert sein sollte, damit die Validierung erfolgreich ist. |

{style="table-layout:auto"}

+++

+++Antwort

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit Details zur neu erstellten Zielgruppenvorlage zurückgegeben.

+++

## Umgang mit API-Fehlern

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status](../../../landing/troubleshooting.md#api-status-codes)Codes und [Fehler in der Anfragekopfzeile](../../../landing/troubleshooting.md#request-header-errors) im Handbuch zur Fehlerbehebung bei Experience Platform.

## Nächste Schritte

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wann Sie Zielgruppenvorlagen verwenden sollten und wie Sie eine Zielgruppenvorlage mithilfe des API-Endpunkts `/authoring/audience-templates` konfigurieren. Lesen Sie [Verwenden des Destination SDK zum Konfigurieren Ihres Ziels](../guides/configure-destination-instructions.md), um zu verstehen, wo dieser Schritt in den Prozess der Konfiguration Ihres Ziels passt.
