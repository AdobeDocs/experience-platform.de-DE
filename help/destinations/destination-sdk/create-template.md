---
description: Als Teil der Destination SDK bietet Adobe Entwicklertools, mit denen Sie Ihr Ziel konfigurieren und testen können. Auf dieser Seite wird beschrieben, wie Sie eine Vorlage für die Nachrichtenumwandlung erstellen und testen.
title: Erstellen und Testen einer Nachrichten-Umwandlungsvorlage
exl-id: 15e7f436-4d33-4172-bd14-ad8dfbd5e4a8
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 2%

---

# Erstellen und Testen einer Nachrichten-Umwandlungsvorlage {#create-template}

## Übersicht {#overview}

Als Teil der Destination SDK bietet Adobe Entwicklertools, mit denen Sie Ihr Ziel konfigurieren und testen können. Auf dieser Seite wird beschrieben, wie Sie eine Vorlage für die Nachrichtenumwandlung erstellen und testen. Informationen zum Testen Ihres Ziels finden Sie unter [Testen der Zielkonfiguration](./test-destination.md).

nach **Erstellen und Testen einer Nachrichtenumwandlungsvorlage** zwischen dem Zielschema in Adobe Experience Platform und dem von Ihrem Ziel unterstützten Nachrichtenformat, verwenden Sie die *Authoring-Tool für Vorlagen* weiter unten beschrieben.  Weitere Informationen zur Datenumwandlung zwischen Quell- und Zielschema finden Sie im Abschnitt [Nachrichtenformat-Dokument](./message-format.md#using-templating).

Die folgende Abbildung zeigt, wie das Erstellen und Testen einer Vorlage für die Nachrichtenumwandlung in die [Zielkonfigurations-Workflow](./configure-destination-instructions.md) in Destination SDK:

![Abbildung, wo der Schritt &quot;Vorlage erstellen&quot;in den Zielkonfigurations-Workflow passt](./assets/create-template-step.png)

## Gründe für die Erstellung und den Test einer Umwandlungsvorlage für Nachrichten {#why-create-message-transformation-template}

Einer der ersten Schritte bei der Erstellung Ihres Ziels in Destination SDK besteht darin, darüber nachzudenken, wie das Datenformat für Segmentzugehörigkeit, Identitäten und Profilattribute transformiert wird, wenn es von Adobe Experience Platform in Ihr Ziel exportiert wird. Informationen zur Transformation zwischen dem Adobe-XDM-Schema und Ihrem Zielschema finden Sie in [Nachrichtenformat-Dokument](./message-format.md#using-templating).

Damit die Transformation erfolgreich ist, müssen Sie eine Umwandlungsvorlage wie im folgenden Beispiel angeben: [Erstellen einer Vorlage zum Senden von Segmenten, Identitäten und Profilattributen](./message-format.md#segments-identities-attributes).

Adobe bietet ein Vorlagenwerkzeug, mit dem Sie die Nachrichtenvorlage erstellen und testen können, mit der Daten aus dem Adobe-XDM-Format in das von Ihrem Ziel unterstützte Format umgewandelt werden. Das Tool verfügt über zwei API-Endpunkte, die Sie verwenden können:
* Verwenden Sie die *Beispiel-Vorlagen-API* um eine Beispielvorlage zu erhalten.
* Verwenden Sie die *render template API* , um die Beispielvorlage zu rendern, damit Sie das Ergebnis mit dem erwarteten Datenformat Ihres Ziels vergleichen können. Nachdem Sie die exportierten Daten mit dem von Ihrem Ziel erwarteten Datenformat verglichen haben, können Sie die Vorlage bearbeiten. Auf diese Weise stimmen die exportierten Daten, die Sie generieren, mit dem von Ihrem Ziel erwarteten Datenformat überein.

## Schritte, die vor der Erstellung der Vorlage abzuschließen sind {#prerequisites}

Bevor Sie bereit sind, die Vorlage zu erstellen, führen Sie die folgenden Schritte aus:

1. [Erstellen einer Zielserverkonfiguration](./destination-server-api.md). Die Vorlage, die Sie generieren, unterscheidet sich je nach dem Wert, den Sie für die `maxUsersPerRequest` Parameter.
   * Verwendung `maxUsersPerRequest=1` , wenn Sie möchten, dass ein API-Aufruf an Ihr Ziel ein einzelnes Profil sowie die zugehörigen Segmentqualifikationen, Identitäten und Profilattribute enthält.
   * Verwendung `maxUsersPerRequest` einen Wert größer als 1 haben, wenn Sie möchten, dass ein API-Aufruf an Ihr Ziel mehrere Profile sowie deren Segmentqualifikationen, Identitäten und Profilattribute enthält.
2. [Erstellen einer Zielkonfiguration](./destination-configuration-api.md#create) und fügen Sie die ID der Zielserverkonfiguration in `destinationDelivery.destinationServerId`.
3. [ID der Zielkonfiguration abrufen](./destination-configuration-api.md#retrieve-list) die Sie gerade erstellt haben, sodass Sie sie im Tool zur Vorlagenerstellung verwenden können.
4. Grundlegendes [Welche Funktionen und Filter können Sie verwenden](./supported-functions.md) in der Nachrichtenumwandlungsvorlage.

## Verwendung der API für Beispielvorlagen und Rendering-Vorlagen-API zum Erstellen einer Vorlage für Ihr Ziel {#iterative-process}

>[!TIP]
>
>Bevor Sie die Umwandlungsvorlage für Nachrichten erstellen und bearbeiten, können Sie zunächst die [API-Endpunkt der Render-Vorlage](./render-template-api.md#render-exported-data) mit einer einfachen Vorlage, die Ihre Rohprofile exportiert, ohne Konvertierungen vorzunehmen. Die Syntax für die einfache Vorlage lautet: <br> `"template": "{% for profile in input.profiles %}{{profile|raw}}{% endfor %}}"`

Der Prozess zum Abrufen und Testen der Vorlage ist iterativ. Wiederholen Sie die folgenden Schritte, bis die exportierten Profile dem erwarteten Datenformat Ihres Ziels entsprechen.

1. Erstens: [Beispielvorlage abrufen](./create-template.md#sample-template-api).
2. Verwenden Sie die Beispielvorlage als Ausgangspunkt, um einen eigenen Entwurf zu erstellen.
3. Rufen Sie die [API-Endpunkt der Render-Vorlage](./create-template.md#render-template-api) mit Ihrer eigenen Vorlage. Adobe generiert Beispielprofile basierend auf Ihrem Schema und gibt das Ergebnis oder etwaige aufgetretene Fehler zurück.
4. Vergleichen Sie die exportierten Daten mit dem von Ihrem Ziel erwarteten Datenformat. Bearbeiten Sie bei Bedarf die Vorlage.
5. Wiederholen Sie diesen Vorgang, bis die exportierten Profile dem erwarteten Datenformat Ihres Ziels entsprechen.

## Beispielvorlage mit der Beispielvorlagen-API abrufen {#sample-template-api}

>[!NOTE]
>
>Eine vollständige API-Referenzdokumentation finden Sie unter [Abrufen von Beispielvorlagen-API-Vorgängen](./sample-template-api.md).

Fügen Sie dem Aufruf eine Ziel-ID hinzu, wie unten dargestellt, und die Antwort gibt ein Vorlagenbeispiel zurück, das der Ziel-ID entspricht.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/testing/template/sample/5114d758-ce71-43ba-b53e-e2a91d67b67f' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

Wenn die von Ihnen angegebene Ziel-ID einer Zielkonfiguration mit [Aggregation des besten Aufwands](./destination-configuration.md#best-effort-aggregation) und `maxUsersPerRequest=1` in der Aggregationsrichtlinie gibt die Anfrage eine Beispielvorlage zurück, die der folgenden ähnelt:

```python
{#- THIS is an example template for a single profile -#}
{#- A '-' at the beginning or end of a tag removes all whitespace on that side of the tag. -#}
{
    "identities": [
    {%- for idMapEntry in input.profile.identityMap -%}
    {%- set namespace = idMapEntry.key -%}
        {%- for identity in idMapEntry.value %}
        {
            "type": "{{ namespace }}",
            "id": "{{ identity.id }}"
        }{%- if not loop.last -%},{%- endif -%}
        {%- endfor -%}{%- if not loop.last -%},{%- endif -%}
    {% endfor %}
    ],
    "AdobeExperiencePlatformSegments": {
        "add": [
        {%- for segment in input.profile.segmentMembership.ups | added %}
            "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
        {% endfor %}
        ],
        "remove": [
        {#- Alternative syntax for filtering segments by status: -#}
        {% for segment in removedSegments(input.profile.segmentMembership.ups) %}
            "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
        {% endfor %}
        ]
    }
}
```

Wenn die von Ihnen angegebene Ziel-ID einer Zielservervorlage mit [konfigurierbare Aggregation](./destination-configuration.md#configurable-aggregation) oder [Aggregation des besten Aufwands](./destination-configuration.md#best-effort-aggregation) mit `maxUsersPerRequest` größer als 1, gibt die Anfrage eine Beispielvorlage zurück, die der folgenden ähnelt:

```python
{#- THIS is an example template for multiple profiles -#}
{#- A '-' at the beginning or end of a tag removes all whitespace on that side of the tag. -#}
{
    "profiles": [
    {%- for profile in input.profiles %}
        {
            "identities": [
            {%- for idMapEntry in profile.identityMap -%}
            {%- set namespace = idMapEntry.key -%}
                {%- for identity in idMapEntry.value %}
                {
                    "type": "{{ namespace }}",
                    "id": "{{ identity.id }}"
                }{%- if not loop.last -%},{%- endif -%}
                {%- endfor -%}{%- if not loop.last -%},{%- endif -%}
            {% endfor %}
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                {%- for segment in profile.segmentMembership.ups | added %}
                    "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
                {% endfor %}
                ],
                "remove": [
                {#- Alternative syntax for filtering segments by status: -#}
                {% for segment in removedSegments(profile.segmentMembership.ups) %}
                    "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
                {% endfor %}
                ]
            }
        }{%- if not loop.last -%},{%- endif -%}
    {% endfor %}
    ]
}
```

## Escape-Zeichen für Ihre Vorlage {#character-escape-template}

Bevor Sie die Vorlage zum Rendern von Profilen verwenden, die dem erwarteten Format Ihres Ziels entsprechen, müssen Sie die Vorlage mit einem Escape-Zeichen versehen, wie in der folgenden Bildschirmaufzeichnung dargestellt.

![Video, das zeigt, wie eine Vorlage mit einem Tool zum Maskieren von Online-Zeichen mit Escapezeichen versehen wird](./assets/escape-characters.gif)

Sie können ein Online-Tool zum Maskieren von Zeichen verwenden. In der obigen Demo wird die [JSON Escape-Formatierung](https://jsonformatter.org/json-escape).

## Render Template API {#render-template-api}

Nach Erstellung einer Nachrichtenumwandlungsvorlage mit dem [Beispiel-Vorlagen-API](./create-template.md#sample-template-api)können Sie [Rendern der Vorlage](./render-template-api.md) , um exportierte Daten auf dieser Basis zu generieren. Auf diese Weise können Sie überprüfen, ob die Profile, die Adobe Experience Platform in Ihr Ziel exportiert, dem erwarteten Format Ihres Ziels entsprechen.

Beispiele für Aufrufe, die Sie tätigen können, finden Sie in der API-Referenz:

* [Rendern einer Vorlage ohne im Hauptteil gesendete Profile](./render-template-api.md#multiple-profiles-no-body)
* [Rendern einer Vorlage mit Profilen im Hauptteil](./render-template-api.md#multiple-profiles-with-body)

Bearbeiten Sie die Vorlage und rufen Sie den API-Endpunkt der Rendervorlage auf, bis die exportierten Profile dem erwarteten Datenformat Ihres Ziels entsprechen.

## Fügen Sie Ihre mit Zeichen versehene Vorlage zur Zielserverkonfiguration hinzu.

Wenn Sie mit der Umwandlungsvorlage Ihrer Nachricht zufrieden sind, fügen Sie sie zu Ihrer [Zielserverkonfiguration](./server-and-template-configuration.md)in `httpTemplate.requestBody.value`.
