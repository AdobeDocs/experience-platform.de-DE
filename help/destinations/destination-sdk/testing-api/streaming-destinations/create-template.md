---
description: Erfahren Sie, wie Sie mit der Zieltest-API Ihre Umwandlungsvorlage für Streaming-Zielnachrichten testen können, bevor Sie das Ziel veröffentlichen.
title: Erstellen und Testen einer Nachrichtenumwandlungsvorlage
exl-id: 15e7f436-4d33-4172-bd14-ad8dfbd5e4a8
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 90%

---


# Erstellen und Testen einer Nachrichtenumwandlungsvorlage {#create-template}

## Übersicht {#overview}

Als Teil des Destination SDK bietet Adobe Entwickler-Tools, mit denen Sie Ihr Ziel konfigurieren und testen können. Auf dieser Seite wird beschrieben, wie Sie eine Nachrichtenumwandlungsvorlage erstellen und testen. Informationen zum Testen Ihres Ziels finden Sie unter [Testen der Zielkonfiguration](streaming-destination-testing-overview.md).

Zum **Erstellen und Testen einer Nachrichtenumwandlungsvorlage** zwischen dem Zielschema in Adobe Experience Platform und dem von Ihrem Ziel unterstützten Nachrichtenformat können Sie das *Authoring-Tool für Vorlagen* verwenden, das weiter unten beschrieben wird.  Weitere Informationen zur Datenumwandlung zwischen Quell- und Zielschema finden Sie im [Dokument zu Nachrichtenformaten](../../functionality/destination-server/message-format.md#using-templating).

Die folgende Abbildung zeigt, wie das Erstellen und Testen einer Nachrichtenumwandlungsvorlage in den [Zielkonfigurations-Workflow](../../guides/configure-destination-instructions.md) in Destination SDK passt:

![Abbildung, wo der Schritt „Vorlage erstellen“ in den Zielkonfigurations-Workflow passt](../../assets/testing-api/create-template-step.png)

## Gründe für das Erstellen und Testen einer Nachrichtenumwandlungsvorlage {#why-create-message-transformation-template}

Einer der ersten Schritte bei der Erstellung Ihres Ziels in Destination SDK besteht darin, darüber nachzudenken, wie das Datenformat für Zielgruppenzugehörigkeit, Identitäten und Profilattribute transformiert wird, wenn es von Adobe Experience Platform in Ihr Ziel exportiert wird. Informationen zur Transformation zwischen dem Adobe-XDM-Schema und Ihrem Zielschema finden Sie in [Dokument zu Nachrichtenformaten](../../functionality/destination-server/message-format.md#using-templating).

Damit die Transformation erfolgreich ist, müssen Sie eine Umwandlungsvorlage wie im folgenden Beispiel angeben: [Erstellen einer Vorlage zum Senden von Segmenten, Identitäten und Profilattributen](../../functionality/destination-server/message-format.md#segments-identities-attributes).

Adobe bietet ein Vorlagenwerkzeug, mit dem Sie die Nachrichtenvorlage erstellen und testen können, mit der Daten aus dem Adobe-XDM-Format in das von Ihrem Ziel unterstützte Format umgewandelt werden. Das Tool verfügt über zwei API-Endpunkte, die Sie verwenden können:

* Verwenden Sie die *Beispiel-Vorlagen-API* um eine Beispielvorlage zu erhalten.
* Verwenden Sie die *Render-Vorlagen-API*, um die Beispielvorlage zu rendern, damit Sie das Ergebnis mit dem erwarteten Datenformat Ihres Ziels vergleichen können. Nachdem Sie die exportierten Daten mit dem von Ihrem Ziel erwarteten Datenformat verglichen haben, können Sie die Vorlage bearbeiten. Auf diese Weise entsprechen die exportierten Daten, die Sie generieren, dem von Ihrem Ziel erwarteten Datenformat.

## Schritte, die vor der Erstellung der Vorlage abzuschließen sind {#prerequisites}

Bevor Sie bereit sind, die Vorlage zu erstellen, führen Sie die folgenden Schritte aus:

1. [Erstellen Sie eine Ziel-Server-Konfiguration](../../authoring-api/destination-server/create-destination-server.md). Die Vorlage, die Sie generieren, unterscheidet sich je nach dem Wert, den Sie für den Parameter `maxUsersPerRequest` angeben.
   * Verwendung `maxUsersPerRequest=1` , wenn Sie möchten, dass ein API-Aufruf an Ihr Ziel ein einzelnes Profil sowie die zugehörigen Zielgruppenqualifikationen, Identitäten und Profilattribute enthält.
   * Verwendung `maxUsersPerRequest` einen Wert größer als 1 haben, wenn Sie möchten, dass ein API-Aufruf an Ihr Ziel mehrere Profile sowie deren Zielgruppenqualifikationen, Identitäten und Profilattribute enthält.
2. [Erstellen Sie eine Zielkonfiguration](../../authoring-api/destination-configuration/create-destination-configuration.md) und fügen Sie die ID der Ziel-Server-Konfiguration in `destinationDelivery.destinationServerId` hinzu.
3. [Rufen Sie die ID der Zielkonfiguration ab](../../authoring-api/destination-configuration/retrieve-destination-configuration.md), die Sie gerade erstellt haben, sodass Sie sie im Tool zur Vorlagenerstellung verwenden können.
4. Sie müssen verstehen, [welche Funktionen und Filter Sie in der Nachrichtenumwandlungsvorlage verwenden können](../../functionality/destination-server/supported-functions.md).

## Verwendung der Beispielvorlagen-API und der Render-Vorlagen-API zum Erstellen einer Vorlage für Ihr Ziel {#iterative-process}

>[!TIP]
>
>Bevor Sie die Nachrichtenumwandlungsvorlage erstellen und bearbeiten, können Sie zunächst den [Endpunkt der Render-Vorlagen-API](../../testing-api/streaming-destinations/render-template-api.md#render-exported-data) mit einer einfachen Vorlage aufrufen, die Ihre Rohprofile exportiert, ohne Umwandlungen vorzunehmen. Die Syntax für die einfache Vorlage lautet: <br> `"template": "{% for profile in input.profiles %}{{profile|raw}}{% endfor %}}"`

Der Prozess zum Abrufen und Testen der Vorlage ist iterativ. Wiederholen Sie die folgenden Schritte, bis die exportierten Profile dem erwarteten Datenformat Ihres Ziels entsprechen.

1. Als erstes [rufen Sie eine Beispielvorlage ab](../../testing-api/streaming-destinations/create-template.md#sample-template-api).
2. Verwenden Sie die Beispielvorlage als Ausgangspunkt, um einen eigenen Entwurf zu erstellen.
3. Rufen Sie den [Endpunkt der Render-Vorlagen-API](../../testing-api/streaming-destinations/create-template.md#render-template-api) mit Ihrer eigenen Vorlage auf. Adobe generiert Beispielprofile basierend auf Ihrem Schema und gibt das Ergebnis oder etwaige aufgetretene Fehler zurück.
4. Vergleichen Sie die exportierten Daten mit dem von Ihrem Ziel erwarteten Datenformat. Bearbeiten Sie bei Bedarf die Vorlage.
5. Wiederholen Sie diesen Vorgang, bis die exportierten Profile dem erwarteten Datenformat Ihres Ziels entsprechen.

## Abrufen einer Beispielvorlage mit der Beispielvorlagen-API {#sample-template-api}

>[!NOTE]
>
>Eine vollständige API-Referenzdokumentation finden Sie unter [Abrufen von Beispielvorlagen-API-Vorgängen](../../testing-api/streaming-destinations/sample-template-api.md).

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

Wenn die von Ihnen angegebene Ziel-ID einer Zielkonfiguration mit [Aggregation nach bestem Bemühen](../../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation) und `maxUsersPerRequest=1` in der Aggregationsrichtlinie entspricht, gibt die Anfrage eine Beispielvorlage zurück, die der folgenden ähnelt:

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
        {#- Alternative syntax for filtering audiences by status: -#}
        {% for segment in removedSegments(input.profile.segmentMembership.ups) %}
            "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
        {% endfor %}
        ]
    }
}
```

Wenn die von Ihnen angegebene Ziel-ID einer Ziel-Server-Vorlage mit [konfigurierbarer Aggregation](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) oder [Aggregation nach bestem Bemühen](../../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation) mit `maxUsersPerRequest` größer als 1 entspricht, gibt die Anfrage eine Beispielvorlage zurück, die der folgenden ähnelt:

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
                {#- Alternative syntax for filtering audiences by status: -#}
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

![Video, das zeigt, wie eine Vorlage mithilfe eines Online-Tools zum Maskieren von Zeichen mit Escapezeichen versehen wird](../../assets/testing-api/escape-characters.gif)

Sie können ein Online-Tool zum Maskieren von Zeichen verwenden. In der obigen Demo wird die [JSON Escape-Formatierung](https://jsonformatter.org/json-escape) verwendet.

## Render-Vorlagen-API {#render-template-api}

Nach Erstellung einer Nachrichtenumwandlungsvorlage mit der [Beispielvorlagen-API](create-template.md#sample-template-api)können Sie [die Vorlage rendern](render-template-api.md), um exportierte Daten auf dieser Basis zu generieren. Auf diese Weise können Sie überprüfen, ob die Profile, die Adobe Experience Platform in Ihr Ziel exportieren würde, dem erwarteten Format Ihres Ziels entsprechen.

Beispiele für Aufrufe, die Sie tätigen können, finden Sie in der API-Referenz:

* [Rendern einer Vorlage ohne im Hauptteil gesendete Profile](render-template-api.md#multiple-profiles-no-body)
* [Rendern einer Vorlage mit im Hauptteil gesendeten Profilen](render-template-api.md#multiple-profiles-with-body)

Bearbeiten Sie die Vorlage und rufen Sie den Endpunkt der Render-Vorlagen-API auf, bis die exportierten Profile dem erwarteten Datenformat Ihres Ziels entsprechen.

## Fügen Sie Ihre mit Escape-Zeichen versehene Vorlage zur Ziel-Server-Konfiguration hinzu

Wenn Sie mit der Nachrichtenumwandlungsvorlage zufrieden sind, fügen Sie sie zu Ihrer [Ziel-Server-Konfiguration](../../authoring-api/destination-server/create-destination-server.md)in `httpTemplate.requestBody.value` hinzu.
