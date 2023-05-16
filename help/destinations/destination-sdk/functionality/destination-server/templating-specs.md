---
description: Erfahren Sie, wie Sie die an Ihren -Endpunkt gesendeten HTTP-Anfragen formatieren. Verwenden Sie den Endpunkt /authoring/destination-servers , um die Vorlagenspezifikationen des Zielservers in Adobe Experience Platform Destination SDK zu konfigurieren.
title: Vorlagenspezifikationen für Ziele, die mit Destination SDK erstellt wurden
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 24%

---


# Vorlagenspezifikationen für Ziele, die mit Destination SDK erstellt wurden

Verwenden Sie den Vorlagenspezifikteil der Zielserverkonfiguration, um zu konfigurieren, wie die an Ihr Ziel gesendeten HTTP-Anforderungen formatiert werden.

In einer Vorlagenspezifikation können Sie definieren, wie Sie Profilattributfelder zwischen dem XDM-Schema und dem Format transformieren können, das Ihre Plattform unterstützt.

Vorlagenspezifikationen sind Teil der Zielserverkonfiguration für Echtzeit-Ziele (Streaming).

Informationen dazu, wo diese Komponente in eine mit Destination SDK erstellte Integration passt, finden Sie im Diagramm im [Konfigurationsoptionen](../configuration-options.md) Dokumentation oder lesen Sie das Handbuch zu [Verwenden von Destination SDK zum Konfigurieren eines Streaming-Ziels](../../guides/configure-destination-instructions.md#create-server-template-configuration).

Sie können die Vorlagenspezifikationen für Ihr Ziel über die `/authoring/destination-servers` -Endpunkt. Detaillierte Beispiele für API-Aufrufe, in denen Sie die auf dieser Seite angezeigten Komponenten konfigurieren können, finden Sie auf den folgenden API-Referenzseiten.

* [Erstellen einer Zielserverkonfiguration](../../authoring-api/destination-server/create-destination-server.md)
* [Aktualisieren der Zielserverkonfiguration](../../authoring-api/destination-server/update-destination-server.md)

>[!IMPORTANT]
>
>Alle von Destination SDK unterstützten Parameternamen und Werte sind **Groß-/Kleinschreibung**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Unterstützte Integrationstypen {#supported-integration-types}

Die nachstehende Tabelle beschreibt ausführlich, welche Integrationstypen die auf dieser Seite beschriebenen Funktionen unterstützen.

| Integrationstyp | Unterstützt Funktionen |
|---|---|
| Echtzeit-Integrationen (Streaming) | Ja |
| Dateibasierte (Batch-)Integrationen | Nein |

## Vorlagenspezifikation konfigurieren {#configure-template-spec}

Adobe verwendet eine Vorlagensprache, die [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) ähnelt, um die Felder aus dem XDM-Schema in ein von Ihrem Ziel unterstütztes Format umzuwandeln.

![Vorlagenkonfiguration hervorgehoben](../../assets/functionality/destination-server/template-configuration.png)

Weitere Informationen zur Transformation finden Sie unter den folgenden Links:

* [Nachrichtenformat](message-format.md)
* [Verwenden einer Vorlagensprache für die Transformationen von Identitäten, Attributen und Segmentzugehörigkeiten ](message-format.md#using-templating)

>[!TIP]
>
>Adobe bietet ein [Entwickler-Tool](../../testing-api/streaming-destinations/create-template.md), das Ihnen beim Erstellen und Testen einer Nachrichtenumwandlungsvorlage hilft.

Unten finden Sie ein Beispiel einer HTTP-Anforderungsvorlage mit Beschreibungen der einzelnen Parameter.

```json
{
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
| `httpMethod` | Zeichenfolge | *Erforderlich.* Die Methode, die Adobe bei Aufrufen an Ihren Server verwendet. Unterstützte Methoden: `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `templatingStrategy` | Zeichenfolge | *Erforderlich.* Verwenden Sie `PEBBLE_V1`. |
| `value` | Zeichenfolge | *Erforderlich.* Diese Zeichenfolge ist die mit Zeichen versehene Version der Vorlage, die die von Platform gesendeten HTTP-Anforderungen in das von Ihrem Ziel erwartete Format formatiert. <br> Informationen zum Schreiben der Vorlage finden Sie im Abschnitt unter [mit Vorlage](message-format.md#using-templating). <br> Weitere Informationen zur Bereinigung von Zeichen finden Sie im Abschnitt [RFC-JSON-Standard, Abschnitt 7](https://tools.ietf.org/html/rfc8259#section-7). <br> Ein Beispiel für eine einfache Umwandlung finden Sie im Abschnitt [Profilattribute](message-format.md#attributes) Umwandlung. |
| `contentType` | Zeichenfolge | *Erforderlich.* Der Content-Typ, den Ihr Server akzeptiert. Je nachdem, welcher Typ von Ausgabe Ihre Umwandlungsvorlage erzeugt, kann dies eine der unterstützten sein [Content-Typen von HTTP-Anwendungen](https://www.iana.org/assignments/media-types/media-types.xhtml#application). In den meisten Fällen sollte dieser Wert auf `application/json`. |

{style="table-layout:auto"}

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Artikels sollten Sie besser verstehen, was eine Vorlagenspezifikation ist und wie Sie sie konfigurieren können.

Weitere Informationen zu den anderen Ziel-Server-Komponenten finden Sie in den folgenden Artikeln:

* [Serverspezifikationen für Ziele, die mit Destination SDK erstellt wurden](server-specs.md)
* [Nachrichtenformat](message-format.md)
* [Konfiguration der Dateiformatierung](file-formatting.md)