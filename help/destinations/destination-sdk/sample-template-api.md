---
description: Auf dieser Seite werden alle API-Vorgänge aufgelistet und beschrieben, die Sie mit dem API-Endpunkt "/authoring/testing/template/sample"ausführen können, um eine Vorlage zur Testnachrichten-Transformation für Ihr Ziel zu erhalten.
title: Abrufen von Beispielvorlagen-API-Vorgängen
source-git-commit: 19307fba8f722babe5b6d57e80735ffde00fc851
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 2%

---

# Abrufen von Beispielvorlagen-API-Vorgängen {#get=sample-template-api-operations}

>[!IMPORTANT]
>
>**API-Endpunkt**: `https://platform.adobe.io/data/core/activation/authoring/testing/template/sample`

Auf dieser Seite werden alle API-Vorgänge aufgelistet und beschrieben, die Sie mit dem API-Endpunkt `/authoring/testing/template/sample` ausführen können, um eine [Nachrichtenumwandlungsvorlage](./message-format.md#using-templating) für Ihr Ziel zu generieren. Eine Beschreibung der von diesem Endpunkt unterstützten Funktionen finden Sie unter [Vorlage erstellen](./create-template.md).

## Erste Schritte mit API-Vorlagenvorgängen {#get-started}

Bevor Sie fortfahren, lesen Sie zunächst das [Erste-Schritte-Handbuch](./getting-started.md) , um wichtige Informationen zu erhalten, die Sie benötigen, um die API erfolgreich aufrufen zu können. Dazu gehören das Abrufen der erforderlichen Zielerstellungsberechtigung und der erforderlichen Kopfzeilen.

## Beispielvorlage abrufen {#generate-sample-template}

Sie können eine Beispielvorlage abrufen, indem Sie eine GET-Anfrage an den Endpunkt `authoring/testing/template/sample/` senden und die Ziel-ID der Zielkonfiguration angeben, auf deren Grundlage Sie die Vorlage erstellen.

>[!TIP]
>
>* Die Ziel-ID, die Sie hier verwenden sollten, ist die `instanceId` , die einer Zielkonfiguration entspricht, die mit dem Endpunkt `/destinations` erstellt wurde. Weitere Informationen finden Sie unter [API-Referenz zur Zielkonfiguration](./destination-configuration-api.md#retrieve-list).


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
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit einer Beispielvorlage zurück, die Sie bearbeiten können, um Ihrem erwarteten Datenformat zu entsprechen.

Wenn die von Ihnen angegebene Ziel-ID einer Zielservervorlage mit `maxUsersPerRequest=1` entspricht, gibt die Anforderung eine Beispielvorlage zurück, die der folgenden ähnelt:

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

Wenn die von Ihnen angegebene Ziel-ID einer Zielservervorlage mit `maxUsersPerRequest` größer als 1 entspricht, gibt die Anforderung eine Beispielvorlage zurück, die der folgenden ähnelt:

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

Die Ziel-SDK-API-Endpunkte folgen den allgemeinen Grundsätzen der Experience Platform API-Fehlermeldung. Weitere Informationen finden Sie unter [API-Status-Codes](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) und [Fehler in der Anforderungsheader](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) im Handbuch zur Fehlerbehebung für Platform.

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie eine Nachrichtenumwandlungsvorlage mit dem API-Endpunkt `/authoring/testing/template/sample` generieren. Als Nächstes können Sie den [API-Endpunkt für Rendervorlagen](./render-template-api.md) verwenden, um exportierte Profile basierend auf der Vorlage zu generieren und mit dem erwarteten Datenformat Ihres Ziels zu vergleichen.