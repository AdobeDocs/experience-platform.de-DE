---
description: Die Server- und Vorlagenspezifikationen können im Adobe Experience Platform Destination SDK über den allgemeinen Endpunkt „/authoring/destination-servers“ konfiguriert werden.
title: Konfigurationsoptionen für Server- und Vorlagenspezifikationen im Destination SDK
exl-id: cf493ed5-0bdb-4b90-b84d-73926a566a2a
source-git-commit: a08201c4bc71b0e37202133836e9347ed4d3cd6b
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 100%

---

# Konfigurationsoptionen für Streaming-Ziel-Server und Vorlagenspezifikationen

## Übersicht {#overview}

Die Server- und Vorlagenspezifikationen können im Adobe Experience Platform Destination SDK über den gemeinsamen Endpunkt konfiguriert werden. `/authoring/destination-servers`. Eine vollständige Liste der Vorgänge, die Sie mit dem Endpunkt durchführen können, finden Sie unter [API-Endpunktvorgänge für Ziele](./destination-server-api.md).

## Server-Spezifikationen {#server-specs}

![Server-Konfiguration hervorgehoben](./assets/server-configuration.png)

Kunden können Daten über HTTP-Exporte von Adobe Experience Platform an Ihr Ziel aktivieren. Die Server-Konfiguration enthält Informationen zum Server, der die Nachrichten erhält (der Server auf Ihrer Seite).

Dieser Prozess stellt Benutzerdaten als eine Reihe von HTTP-Nachrichten an Ihre Zielplattform bereit. Die folgenden Parameter bilden die Vorlage für HTTP-Server-Spezifikationen.

| Parameter | Typ | Beschreibung |
|---|---|---|
| `name` | Zeichenfolge | *Erforderlich.* Stellt einen Anzeigenamen Ihres Servers dar, der nur für Adobe sichtbar ist. Dieser Name ist für Partner oder Kunden nicht sichtbar. Beispiel `Moviestar destination server`. |
| `destinationServerType` | Zeichenfolge | *Erforderlich.* Festlegen auf `URL_BASED` für Streaming-Ziele. |
| `templatingStrategy` | Zeichenfolge | *Erforderlich.* <ul><li>Verwenden Sie `PEBBLE_V1`, wenn Sie im Feld `value` ein Makro anstelle eines festen Werts verwenden. Verwenden Sie diese Option, wenn Sie einen Endpunkt wie `https://api.moviestar.com/data/{{customerData.region}}/items` haben. </li><li> Verwenden Sie `NONE`, wenn auf der Adobe-Seite keine Transformation erforderlich ist, z. B. wenn Sie einen Endpunkt wie `https://api.moviestar.com/data/items` haben. </li></ul> |
| `value` | Zeichenfolge | *Erforderlich.* Geben Sie die Adresse des API-Endpunkts ein, mit dem sich Experience Platform verbinden soll. |

{style=&quot;table-layout:auto&quot;}

## Vorlagenspezifikationen {#template-specs}

![Vorlagenkonfiguration hervorgehoben](./assets/template-configuration.png)

Mit der Vorlagenspezifikation können Sie konfigurieren, wie Sie die exportierte Nachricht an Ihr Ziel formatieren. Adobe verwendet eine Vorlagensprache, die [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) ähnelt, um die Felder aus dem XDM-Schema in ein von Ihrem Ziel unterstütztes Format umzuwandeln. Weitere Informationen zur Transformation finden Sie unter den folgenden Links:

* [Nachrichtenformat](./message-format.md)
* [Verwenden einer Vorlagensprache für die Transformationen von Identitäten, Attributen und Segmentzugehörigkeiten ](./message-format.md#using-templating)

>[!TIP]
>
>Adobe bietet ein [Entwickler-Tool](./create-template.md), das Ihnen beim Erstellen und Testen einer Nachrichtenumwandlungsvorlage hilft.

## Beispielkonfiguration für Streaming-Ziele  {#example-configuration}

```json
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.endpointRegion}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"POST",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{ \"attributes\": [ {% for ns in [\"external_id\", \"yourdestination_id\"] %} {% if input.profile.identityMap[ns] is not empty and first_namespace_encountered %} , {% endif %} {% set first_namespace_encountered = true %} {% for identity in input.profile.identityMap[ns]%} { \"{{ ns }}\": \"{{ identity.id }}\" {% if input.profile.segmentMembership.ups is not empty %} , \"AEPSegments\": { \"add\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"realized\" or segment.value.status == \"existing\" %} {% if added_segment_found %} , {% endif %} {% set added_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ], \"remove\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"exited\" %} {% if removed_segment_found %} , {% endif %} {% set removed_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ] } {% set removed_segment_found = false %} {% set added_segment_found = false %} {% endif %} {% if input.profile.attributes is not empty %} , {% endif %} {% for attribute in input.profile.attributes %} \"{{ attribute.key }}\": {% if attribute.value is empty %} null {% else %} \"{{ attribute.value.value }}\" {% endif %} {% if not loop.last%} , {% endif %} {% endfor %} } {% if not loop.last %} , {% endif %} {% endfor %} {% endfor %} ] }"
      },
      "contentType":"application/json"
   }
}
```

| Parameter | Typ | Beschreibung |
|---|---|---|
| `httpMethod` | Zeichenfolge | *Erforderlich.* Die Methode, die Adobe bei Aufrufen an Ihren Server verwendet. Es gibt die Optionen `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden Sie `PEBBLE_V1`. |
| `value` | Zeichenfolge | *Erforderlich.* Diese Zeichenfolge ist die von Sonderzeichen bereinigte Version, die die Daten von Platform-Kunden in das Format umwandelt, das Ihr Service erwartet. <br> Informationen zum Schreiben der Vorlage finden Sie im Abschnitt [Verwenden von Vorlagen](./message-format.md#using-templating). <br> Weitere Informationen zur Bereinigung von Zeichen finden Sie im Abschnitt [RFC-JSON-Standard, Abschnitt 7](https://tools.ietf.org/html/rfc8259#section-7). <br> Ein einfaches Beispiel finden Sie unter [Umwandlung von Profilattributen](./message-format.md#attributes). |
| `contentType` | Zeichenfolge | *Erforderlich.* Der Content-Typ, den Ihr Server akzeptiert. Dieser Wert ist höchstwahrscheinlich `application/json`. |

{style=&quot;table-layout:auto&quot;}