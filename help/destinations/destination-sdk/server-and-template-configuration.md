---
description: Die Server- und Vorlagenspezifikationen können in Adobe Experience Platform Destination SDK über den allgemeinen Endpunkt "/authoring/destination-servers"konfiguriert werden.
title: Konfigurationsoptionen für Server- und Vorlagenspezifikationen in Destination SDK
exl-id: cf493ed5-0bdb-4b90-b84d-73926a566a2a
source-git-commit: 92bca3600d854540fd2badd925e453fba41601a7
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 8%

---

# Konfigurationsoptionen für Streaming-Zielserver und Vorlagenspezifikationen

## Übersicht {#overview}

Die Server- und Vorlagenspezifikationen können in Adobe Experience Platform Destination SDK über den gemeinsamen Endpunkt konfiguriert werden. `/authoring/destination-servers`. Lesen [API-Endpunktvorgänge für Ziele](./destination-server-api.md) für eine vollständige Liste der Vorgänge, die Sie am -Endpunkt ausführen können.

## Serverspezifikationen {#server-specs}

![Serverkonfiguration hervorgehoben](./assets/server-configuration.png)

Kunden können Daten über HTTP-Exporte von Adobe Experience Platform an Ihr Ziel aktivieren. Die Serverkonfiguration enthält Informationen zum Server, der die Nachrichten erhält (der Server auf Ihrer Seite).

Dieser Prozess stellt Benutzerdaten als eine Reihe von HTTP-Nachrichten an Ihre Zielplattform bereit. Die folgenden Parameter bilden die Vorlage für HTTP-Server-Spezifikationen.

| Parameter | Typ | Beschreibung |
|---|---|---|
| `name` | Zeichenfolge | *Erforderlich.* Stellt einen Anzeigenamen Ihres Servers dar, der nur für Adobe sichtbar ist. Dieser Name ist für Partner oder Kunden nicht sichtbar. Beispiel `Moviestar destination server`. |
| `destinationServerType` | Zeichenfolge | *Erforderlich.* Legen Sie fest auf `URL_BASED` für Streaming-Ziele. |
| `templatingStrategy` | Zeichenfolge | *Erforderlich.* <ul><li>Verwendung `PEBBLE_V1` Wenn Sie ein Makro anstelle eines festen Werts im `value` -Feld. Verwenden Sie diese Option, wenn Sie einen Endpunkt wie haben: `https://api.moviestar.com/data/{{customerData.region}}/items` </li><li> Verwendung `NONE` wenn keine Transformation auf der Seite der Adobe erforderlich ist, z. B. wenn Sie einen Endpunkt wie: `https://api.moviestar.com/data/items` </li></ul> |
| `value` | Zeichenfolge | *Erforderlich.* Geben Sie die Adresse des API-Endpunkts ein, mit dem sich Experience Platform verbinden soll. |

{style=&quot;table-layout:auto&quot;}

## Vorlagenspezifikationen {#template-specs}

![Vorlagenkonfiguration hervorgehoben](./assets/template-configuration.png)

Mit der Vorlagenspezifikation können Sie konfigurieren, wie Sie die exportierte Nachricht an Ihr Ziel formatieren. Adobe verwendet eine Vorlagensprache, die der folgenden ähnelt: [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) , um die Felder aus dem XDM-Schema in ein Format umzuwandeln, das von Ihrem Ziel unterstützt wird. Weitere Informationen zur Transformation finden Sie unter den folgenden Links:

* [Nachrichtenformat](./message-format.md)
* [Verwenden einer Vorlagensprache für die Transformationen von Identitäten, Attributen und Segmentzugehörigkeiten ](./message-format.md#using-templating)

>[!TIP]
>
>Adobe bietet eine [Entwickler-Tool](./create-template.md) die Ihnen beim Erstellen und Testen einer Nachrichtenumwandlungsvorlage hilft.

## Beispielkonfiguration für Streaming-Ziele  {#example-configuration}

```json
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.region}}/items"
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
| `httpMethod` | Zeichenfolge | *Erforderlich.* Die Methode, die Adobe bei Aufrufen an Ihren Server verwendet. Optionen sind `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden von `PEBBLE_V1`. |
| `value` | Zeichenfolge | *Erforderlich.* Diese Zeichenfolge ist die mit Zeichen versehene Version, die die Daten von Platform-Kunden in das Format umwandelt, das Ihr Dienst erwartet. <br> Informationen zum Schreiben der Vorlage finden Sie in der [Verwenden des Vorlagenabschnitts](./message-format.md#using-templating). <br> Weitere Informationen zum Escapen von Zeichen finden Sie im Abschnitt [RFC JSON-Standard, Abschnitt 7](https://tools.ietf.org/html/rfc8259#section-7). <br> Ein Beispiel für eine einfache Umwandlung finden Sie im Abschnitt [Profilattribute](./message-format.md#attributes) Umwandlung. |
| `contentType` | Zeichenfolge | *Erforderlich.* Der Inhaltstyp, den Ihr Server akzeptiert. Dieser Wert ist höchstwahrscheinlich `application/json`. |

{style=&quot;table-layout:auto&quot;}