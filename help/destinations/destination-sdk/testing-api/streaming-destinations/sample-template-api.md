---
description: Erfahren Sie, wie Sie mit der Ziel-Test-API eine Vorlage zur Testnachrichten-Transformation für Ihr Ziel generieren.
title: Erstellen einer Vorlage zur Konvertierung von Beispielnachrichten
exl-id: d18a06f7-0c3a-4b4d-a7d5-011690d00e2c
source-git-commit: adf75720f3e13c066b5c244d6749dd0939865a6f
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 29%

---


# Erstellen einer Vorlage zur Konvertierung von Beispielnachrichten {#get-sample-template-api-operations}

>[!IMPORTANT]
>
>**API-Endpunkt**: `https://platform.adobe.io/data/core/activation/authoring/testing/template/sample`

Auf dieser Seite werden alle API-Vorgänge aufgelistet und beschrieben, die Sie mit dem `/authoring/testing/template/sample` API-Endpunkt, um eine [Nachrichtenumwandlungsvorlage](../../functionality/destination-server/message-format.md#using-templating) für Ihr Ziel. Eine Beschreibung der von diesem Endpunkt unterstützten Funktionen finden Sie unter [Erstellen einer Vorlage](create-template.md).

## Erste Schritte mit API-Vorlagenvorgängen {#get-started}

Bevor Sie fortfahren, lesen Sie [Erste Schritte](../../getting-started.md). Dort finden Sie die nötigen Informationen für den erfolgreichen Aufruf der API, einschließlich Details für den Abruf der erforderlichen Authoring-Berechtigung für Ziele und zu den erforderlichen Kopfzeilen.

## Beispielvorlage abrufen {#generate-sample-template}

Sie können eine Beispielvorlage abrufen, indem Sie eine GET-Anfrage an die `authoring/testing/template/sample/` -Endpunkt und die Ziel-ID der Zielkonfiguration angeben, basierend auf der Sie Ihre Vorlage erstellen.

>[!TIP]
>
>* Die Ziel-ID, die Sie hier verwenden sollten, ist die `instanceId`, die einer mithilfe des `/destinations`-Endpunkts erstellten Zielkonfiguration entspricht. Siehe Abschnitt [Zielkonfiguration abrufen](../../authoring-api/destination-configuration/retrieve-destination-configuration.md) für weitere Details.


**API-Format**

```http
GET authoring/testing/template/sample/{DESTINATION_ID}
```

| Parameter | Beschreibung |
| -------- | ----------- |
| `{DESTINATION_ID}` | Die ID der Zielkonfiguration, für die Sie eine Nachrichtenumwandlungsvorlage generieren. |

**Anfrage**

Die folgende Anfrage generiert eine neue Beispielvorlage, die von den in der Payload bereitgestellten Parametern konfiguriert wird.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/testing/template/sample/5114d758-ce71-43ba-b53e-e2a91d67b67f' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit einer Beispielvorlage zurück, die Sie bearbeiten können, um Ihrem erwarteten Datenformat zu entsprechen.

Wenn die von Ihnen angegebene Ziel-ID einer Zielkonfiguration mit [Aggregation des besten Aufwands](../../functionality/destination-configuration/aggregation-policy.md) und `maxUsersPerRequest=1` in der Aggregationsrichtlinie gibt die Anfrage eine Beispielvorlage zurück, die der folgenden ähnelt:

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

Wenn die von Ihnen angegebene Ziel-ID einer Zielservervorlage mit [konfigurierbare Aggregation](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) oder [Aggregation des besten Aufwands](../../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation) mit `maxUsersPerRequest` größer als 1, gibt die Anfrage eine Beispielvorlage zurück, die der folgenden ähnelt:

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

## Umgang mit API-Fehlern {#api-error-handling}

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status-Codes](../../../../landing/troubleshooting.md#api-status-codes) und [Fehler im Anfrage-Header](../../../../landing/troubleshooting.md#request-header-errors) in der Anleitung zur Fehlerbehebung für Platform.

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie eine Nachrichtenumwandlungsvorlage mit dem `/authoring/testing/template/sample` API-Endpunkt. Als Nächstes können Sie die [API-Endpunkt für Rendervorlage](render-template-api.md) , um exportierte Profile basierend auf der Vorlage zu generieren und mit dem erwarteten Datenformat Ihres Ziels zu vergleichen.
