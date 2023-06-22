---
description: Auf dieser Seite wird der API-Aufruf veranschaulicht, der zum Erstellen einer Zielgruppenvorlage über Adobe Experience Platform Destination SDK verwendet wird.
title: Erstellen einer Zielgruppenvorlage
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: ht
source-wordcount: '626'
ht-degree: 100%

---


# Erstellen einer Zielgruppenvorlage

>[!IMPORTANT]
>
>**API-Endpunkt**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Für einige Ziele, die mit Destination SDK erstellt wurden, müssen Sie eine Zielgruppen-Metadatenkonfiguration erstellen, um Segmentmetadaten im Ziel programmgesteuert zu erstellen, zu aktualisieren oder zu löschen. Auf dieser Seite erfahren Sie, wie Sie den API-Endpunkt `/authoring/audience-templates` zum Erstellen der Konfiguration verwenden.

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
   "metadataTemplate":{
      "name":"string",
      "create":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "update":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "delete":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "validate":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
            }
         ]
      },
      "notify":{
         "url":"string",
         "httpMethod":"string",
         "headers":[
            {
               "header":"string",
               "value":"string"
            }
         ],
         "requestBody":{
            
         },
         "responseFields":[
            {
               "name":"string",
               "value":"string"
            }
         ],
         "responseErrorFields":[
            {
               "name":"string",
               "value":"string"
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
| `name` | Zeichenfolge | Der Name der Zielgruppen-Metadatenvorlage für Ihr Ziel. Dieser Name wird in jeder partnerspezifischen Fehlermeldung in der Benutzeroberfläche von Experience Platform angezeigt, gefolgt von der aus `metadataTemplate.create.errorSchemaMap` ausgewerteten Fehlermeldung. |
| `url` | Zeichenfolge | Die URL und der Endpunkt Ihrer API, die zum Erstellen, Aktualisieren, Löschen oder Überprüfen von Zielgruppen/Segmenten in Ihrer Plattform verwendet wird. Zwei branchenübliche Beispiele sind `https://adsapi.snapchat.com/v1/adaccounts/{{customerData.accountId}}/segments` und `https://api.linkedin.com/v2/dmpSegments/{{segment.alias}}`. |
| `httpMethod` | Zeichenfolge | Die Methode, die für Ihren Endpunkt verwendet wird, um das Segment/die Zielgruppe in Ihrem Ziel programmgesteuert zu erstellen, zu aktualisieren, zu löschen oder zu validieren. Beispiel: `POST`, `PUT`, `DELETE` |
| `headers.header` | Zeichenfolge | Gibt alle HTTP-Header an, die zum Aufruf Ihrer API hinzugefügt werden sollen. Beispiel: `"Content-Type"` |
| `headers.value` | Zeichenfolge | Gibt den Wert von HTTP-Headern an, die zum Aufruf Ihrer API hinzugefügt werden sollen. Beispiel: `"application/x-www-form-urlencoded"` |
| `requestBody` | Zeichenfolge | Gibt den Inhalt des Nachrichtentextes an, der an Ihre API gesendet werden soll. Welche Parameter zum Objekt `requestBody` hinzugefügt werden sollten, hängt davon ab, welche Felder Ihre API akzeptiert. Ein Beispiel finden Sie im [Beispiel einer ersten Vorlage](../functionality/audience-metadata-management.md#example-1) im Dokument über die Funktionalität von Zielgruppen-Metadaten. |
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

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status-Codes](../../../landing/troubleshooting.md#api-status-codes) und [Fehler im Anfrage-Header](../../../landing/troubleshooting.md#request-header-errors) in der Anleitung zur Fehlerbehebung für Platform.

## Nächste Schritte

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wann Sie Zielgruppenvorlagen verwenden sollten und wie Sie eine Zielgruppenvorlage mithilfe des API-Endpunkts `/authoring/audience-templates` konfigurieren. Lesen Sie [Verwenden des Destination SDK zum Konfigurieren Ihres Ziels](../guides/configure-destination-instructions.md), um zu verstehen, wo dieser Schritt in den Prozess der Konfiguration Ihres Ziels passt.
