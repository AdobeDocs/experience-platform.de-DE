---
description: Auf dieser Seite werden alle API-Vorgänge aufgelistet und beschrieben, die Sie mithilfe des API-Endpunkts „/authoring/testing/template/render“ durchführen können, um exportierte Daten für Ihr Ziel basierend auf Ihrer Nachrichtenumwandlungsvorlage zu rendern.
title: API-Vorgänge für Rendervorlagen
exl-id: e64ea89e-6064-4a05-9730-e0f7d7a3e1db
source-git-commit: b337d65bcdfbb65da1b751645ddc649d30440dc7
workflow-type: ht
source-wordcount: '806'
ht-degree: 100%

---

# API-Vorgänge für Rendervorlagen {#render-template-api-operations}

>[!IMPORTANT]
>
>**API-Endpunkt**: `https://platform.adobe.io/data/core/activation/authoring/testing/template/render`

Auf dieser Seite werden alle API-Vorgänge aufgelistet und beschrieben, die Sie mithilfe des API-Endpunkts `/authoring/testing/template/render` durchführen können, um basierend auf Ihrer [Nachrichtenumwandlungsvorlage](./message-format.md#using-templating) exportierte Profile zu rendern, die dem erwarteten Format Ihres Ziels entsprechen. Eine Beschreibung der von diesem Endpunkt unterstützten Funktionen finden Sie unter [Erstellen einer Vorlage](./create-template.md).

## Erste Schritte mit API-Vorgängen für Render-Vorlagen {#get-started}

Bevor Sie fortfahren, lesen Sie das Handbuch [Erste Schritte](./getting-started.md) für wichtige Informationen, die Sie benötigen, um die API erfolgreich aufrufen zu können, einschließlich Informationen zum Abrufen der erforderlichen Berechtigung zur Zielerstellung und der erforderlichen Kopfzeilen.

## Rendern exportierter Profile basierend auf der Vorlage für die Nachrichtenumwandlung {#render-exported-data}

Sie können exportierte Profile rendern, indem Sie eine POST-Anfrage an den Endpunkt `authoring/testing/template/render` stellen und dabei die Ziel-ID der Zielkonfiguration und die Vorlage angeben, die Sie mit dem [Beispiel-Vorlagen-API-Endpunkt](./sample-template-api.md) erstellt haben.

Sie können eine einfache Vorlage verwenden, die Ihre Rohprofile exportiert, ohne Konvertierungen vorzunehmen, und dann zu einer komplexeren Vorlage wechseln, die Umwandlungen auf Profile anwendet. Die Syntax für die einfache Vorlage lautet: <br> `"template": "{% for profile in input.profiles %}{{profile|raw}}{% endfor %}}"`

>[!TIP]
>
>* Die Ziel-ID, die Sie hier verwenden sollten, ist die `instanceId`, die einer mithilfe des `/destinations`-Endpunkts erstellten Zielkonfiguration entspricht. Weitere Informationen finden Sie unter [API-Vorgänge für die Zielkonfiguration](./destination-configuration-api.md#retrieve-list).


**API-Format**


```http
POST authoring/testing/template/render
```

| Anfrageparameter | Beschreibung |
| -------- | ----------- |
| `destinationId` | Die ID der Zielkonfiguration, für die Sie exportierte Profile rendern. |
| `template` | Die mit Escape-Zeichen versehene Version der Vorlage, basierend auf der Sie exportierte Profile rendern. |
| `profiles` | *Optional*. Sie können Profile zum Anfrageinhalt hinzufügen. Wenn Sie keine Profile hinzufügen, erstellt Experience Platform automatisch Profile und fügt sie der Anfrage hinzu. <br> Wenn Sie Profile zum Hauptteil des Aufrufs hinzufügen möchten, können Sie einige mithilfe der [API zur Erzeugung von Musterprofilen](./sample-profile-generation-api.md) erzeugen. |

{style=&quot;table-layout:auto&quot;}

Beachten Sie, dass die vom API-Endpunkt für Render-Vorlagen zurückgegebene Antwort je nach Ziel-Aggregationsrichtlinie unterschiedlich ist. Wenn Ihr Ziel über eine konfigurierbare Aggregationsrichtlinie verfügt, wird der Aggregationsschlüssel, der bestimmt, wie Profile aggregiert werden, auch in der Antwort zurückgegeben. Weitere Informationen über [Aggregationsrichtlinien](./destination-configuration.md#aggregation) finden Sie im Dokument zur Zielkonfiguration.

| Antwortparameter | Beschreibung |
| -------- | ----------- |
| `aggregationKey` | Stellt die Richtlinie dar, nach der Profile in Exporten zu Ihrem Ziel aggregiert werden. Dieser Parameter ist optional und nur vorhanden, wenn die Aggregationsrichtlinie für das Ziel auf `CONFIGURABLE_AGGREGATION` gesetzt ist. |
| `profiles` | Zeigt die in der Anfrage angegebenen Profile oder die automatisch generierten Profile an, wenn in der Anfrage keine Profile angegeben wurden. |
| `output` | Das bzw. die gerenderte(n) Profil(e) als Escape-Zeichenfolge, basierend auf der bereitgestellten Nachrichtenumwandlungsvorlage |

Die folgenden Abschnitte enthalten detaillierte Anforderungen und Antworten für beide oben beschriebenen Fälle.

* [Aggregation nach bestem Bemühen und ein im Anfrageinhalt enthaltenes Profil](#best-effort)
* [Konfigurierbare Aggregation und Profile im Anfrageinhalt](#configurable-aggregation)

### Rendern exportierter Profile nach bestem Bemühen und ein einzelnes Profil, das im Anfrageinhalt enthalten ist {#best-effort}

**Anfrage**

Die folgende Anfrage rendert ein exportiertes Profil, das dem von Ihrem Ziel erwarteten Format entspricht. In diesem Beispiel entspricht die Ziel-ID einer Zielkonfiguration mit der Aggregation nach bestem Bemühen, und ein Beispielprofil ist im Hauptteil der Anfrage enthalten.

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/template/render' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '
{
    "destinationId": "947c1c46-008d-40b0-92ec-3af86eaf41c1",
    "template": "{#- THIS is an example template for a single profile -#}\r\n{#- A '\''-'\'' at the beginning or end of a tag removes all whitespace on that side of the tag. -#}\r\n{\r\n    \"identities\": [\r\n    {%- for idMapEntry in input.profile.identityMap -%}\r\n    {%- set namespace = idMapEntry.key -%}\r\n        {%- for identity in idMapEntry.value %}\r\n        {\r\n            \"type\": \"{{ namespace }}\",\r\n            \"id\": \"{{ identity.id }}\"\r\n        }{%- if not loop.last -%},{%- endif -%}\r\n        {%- endfor -%}{%- if not loop.last -%},{%- endif -%}\r\n    {% endfor %}\r\n    ],\r\n    \"AdobeExperiencePlatformSegments\": {\r\n        \"add\": [\r\n        {%- for segment in input.profile.segmentMembership.ups | added %}\r\n            \"{{ segment.key }}\"{%- if not loop.last -%},{%- endif -%}\r\n        {% endfor %}\r\n        ],\r\n        \"remove\": [\r\n        {#- Alternative syntax for filtering segments by status: -#}\r\n        {% for segment in removedSegments(input.profile.segmentMembership.ups) %}\r\n            \"{{ segment.key }}\"{%- if not loop.last -%},{%- endif -%}\r\n        {% endfor %}\r\n        ]\r\n    }\r\n}",
    "profiles": [
        {
            "segmentMembership": {
                "ups": {
                    "segmentid1": {
                        "lastQualificationTime": "2021-10-26T16:59:00.828461Z",
                        "status": "existing"
                    },
                    "segmentid3": {
                        "lastQualificationTime": "2021-10-26T16:59:00.828469Z",
                        "status": "exited"
                    },
                    "segmentid2": {
                        "lastQualificationTime": "2021-10-26T16:59:00.828468Z",
                        "status": "realized"
                    }
                }
            },
            "identityMap": {
                "gaid": [
                    {
                        "id": "gaid-BLAcJ"
                    }
                ],
                "idfa": [
                    {
                        "id": "idfa-Iv5AG"
                    }
                ],
                "email": [
                    {
                        "id": "email-rbN62"
                    }
                ]
            },
            "attributes": {
                "key": {
                    "value": "string"
                }
            }
        }
    ]
}'
```

**Antwort**

Die Antwort gibt das Ergebnis des Renderns der Vorlage oder etwaige Fehler zurück.
Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit Details zu den exportierten Daten zurückgegeben. Das exportierte Profil finden Sie im Parameter `output` in Form einer Escape-Zeichenfolge.
Bei einer fehlerhaften Antwort wird der HTTP-Status 400 zusammen mit Beschreibungen der aufgetretenen Fehler zurückgegeben.

```json
{
    "results": [
        {
            "profiles": [
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T16:59:00.828461Z",
                                "status": "existing"
                            },
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T16:59:00.828469Z",
                                "status": "exited"
                            },
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T16:59:00.828468Z",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "gaid": [
                            {
                                "id": "gaid-BLAcJ"
                            }
                        ],
                        "idfa": [
                            {
                                "id": "idfa-Iv5AG"
                            }
                        ],
                        "email": [
                            {
                                "id": "email-rbN62"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                }
            ],
            "output": "{\r\n    \"identities\": [\r\n        {\r\n            \"type\": \"gaid\",\r\n            \"id\": \"gaid-BLAcJ\"\r\n        },\r\n        {\r\n            \"type\": \"idfa\",\r\n            \"id\": \"idfa-Iv5AG\"\r\n        },\r\n        {\r\n            \"type\": \"email\",\r\n            \"id\": \"email-rbN62\"\r\n        }\r\n    ],\r\n    \"AdobeExperiencePlatformSegments\": {\r\n        \"add\": [\r\n            \"segmentid1\",\r\n            \"segmentid2\"\r\n        ],\r\n        \"remove\": [\r\n            \"segmentid3\"\r\n        ]\r\n    }\r\n}"
        }
    ]
}    
```

### Rendern von exportierten Profilen mit konfigurierbarer Aggregation und im Anfragekörper enthaltenen Profilen {#configurable-aggregation}

**Anfrage**


Die folgende Anfrage rendert mehrere exportierte Profile, die dem von Ihrem Ziel erwarteten Format entsprechen. In diesem Beispiel entspricht die Ziel-ID einer Zielkonfiguration mit konfigurierbarer Aggregation. Im Text der Anfrage sind zwei Profile enthalten, von denen jedes drei Segmentqualifikationen und fünf Identitäten aufweist. Sie können Profile generieren, die bei dem Aufruf gesendet werden, indem Sie die [API zur Erzeugung von Musterprofilen](./sample-profile-generation-api.md) verwenden.

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/template/render' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '{
    "destinationId": "c2bc84c5-589c-43a1-96ea-becfa941f5be",
    "template": "{#- THIS is an example template for multiple profiles -#}\r\n{#- A '\''-'\'' at the beginning or end of a tag removes all whitespace on that side of the tag. -#}\r\n{\r\n    \"profiles\": [\r\n    {%- for profile in input.profiles %}\r\n        {\r\n            \"identities\": [\r\n            {%- for idMapEntry in profile.identityMap -%}\r\n            {%- set namespace = idMapEntry.key -%}\r\n                {%- for identity in idMapEntry.value %}\r\n                {\r\n                    \"type\": \"{{ namespace }}\",\r\n                    \"id\": \"{{ customerData }}\"\r\n                }{%- if not loop.last -%},{%- endif -%}\r\n                {%- endfor -%}{%- if not loop.last -%},{%- endif -%}\r\n            {% endfor %}\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                {%- for segment in profile.segmentMembership.ups | added %}\r\n                    \"{{ segment.key }}\"{%- if not loop.last -%},{%- endif -%}\r\n                {% endfor %}\r\n                ],\r\n                \"remove\": [\r\n                {#- Alternative syntax for filtering segments by status: -#}\r\n                {% for segment in removedSegments(profile.segmentMembership.ups) %}\r\n                    \"{{ segment.key }}\"{%- if not loop.last -%},{%- endif -%}\r\n                {% endfor %}\r\n                ]\r\n            }\r\n        }{%- if not loop.last -%},{%- endif -%}\r\n    {% endfor %}\r\n    ]\r\n}",
    "profiles": [
        {
            "segmentMembership": {
                "ups": {
                    "segmentid1": {
                        "lastQualificationTime": "2021-10-26T17:41:55.947859Z",
                        "status": "existing"
                    },
                    "segmentid3": {
                        "lastQualificationTime": "2021-10-26T17:41:55.947860Z",
                        "status": "exited"
                    },
                    "segmentid2": {
                        "lastQualificationTime": "2021-10-26T17:41:55.947860Z",
                        "status": "realized"
                    }
                }
            },
            "identityMap": {
                "amazon_channel": [
                    {
                        "id": "amazon_channel-biCbJ"
                    }
                ],
                "named_user_id": [
                    {
                        "id": "named_user_id-0Q3hp"
                    }
                ],
                "channel": [
                    {
                        "id": "channel-mN1Hw"
                    }
                ],
                "android_channel": [
                    {
                        "id": "android_channel-MVw4L"
                    }
                ],
                "ios_channel": [
                    {
                        "id": "ios_channel-2OjnN"
                    }
                ]
            },
            "attributes": {
                "key": {
                    "value": "string"
                }
            }
        },
        {
            "segmentMembership": {
                "ups": {
                    "segmentid1": {
                        "lastQualificationTime": "2021-10-26T17:41:55.948187Z",
                        "status": "existing"
                    },
                    "segmentid3": {
                        "lastQualificationTime": "2021-10-26T17:41:55.948188Z",
                        "status": "exited"
                    },
                    "segmentid2": {
                        "lastQualificationTime": "2021-10-26T17:41:55.948188Z",
                        "status": "realized"
                    }
                }
            },
            "identityMap": {
                "amazon_channel": [
                    {
                        "id": "amazon_channel-fxt2p"
                    }
                ],
                "named_user_id": [
                    {
                        "id": "named_user_id-sboQe"
                    }
                ],
                "channel": [
                    {
                        "id": "channel-MRelR"
                    }
                ],
                "android_channel": [
                    {
                        "id": "android_channel-M46ze"
                    }
                ],
                "ios_channel": [
                    {
                        "id": "ios_channel-40Vrf"
                    }
                ]
            },
            "attributes": {
                "key": {
                    "value": "string"
                }
            }
        }
    ]
}'
```

**Antwort**

Die Antwort gibt das Ergebnis des Renderns der Vorlage oder etwaige Fehler zurück.
Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit Details zu den exportierten Daten zurückgegeben. Beachten Sie in der Antwort, wie die Profile basierend auf der Segmentzugehörigkeit und den Identitäten aggregiert werden. Die exportierten Profile finden Sie im Parameter `output` in Form einer Escape-Zeichenfolge.
Bei einer fehlerhaften Antwort wird der HTTP-Status 400 zusammen mit Beschreibungen der aufgetretenen Fehler zurückgegeben.

```json
{
    "results": [
        {
            "aggregationKey": {
                "destinationInstanceId": "49966037-32cd-4457-a105-2cbf9c01826a",
                "segmentId": "segmentid3",
                "segmentStatus": "exited",
                "identityNamespaces": [
                    "android_channel",
                    "amazon_channel",
                    "ios_channel",
                    "channel"
                ]
            },
            "profiles": [
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "ios_channel": [
                            {
                                "id": "ios_channel-2OjnN"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "channel": [
                            {
                                "id": "channel-mN1Hw"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "amazon_channel": [
                            {
                                "id": "amazon_channel-biCbJ"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "android_channel": [
                            {
                                "id": "android_channel-MVw4L"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "ios_channel": [
                            {
                                "id": "ios_channel-40Vrf"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "channel": [
                            {
                                "id": "channel-MRelR"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "amazon_channel": [
                            {
                                "id": "amazon_channel-fxt2p"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "android_channel": [
                            {
                                "id": "android_channel-M46ze"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                }
            ],
            "output": "{\r\n    \"profiles\": [\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"ios_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"amazon_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"android_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"ios_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"amazon_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"android_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        }\r\n    ]\r\n}"
        },
        {
            "aggregationKey": {
                "destinationInstanceId": "49966037-32cd-4457-a105-2cbf9c01826a",
                "segmentId": "segmentid1",
                "segmentStatus": "existing",
                "identityNamespaces": [
                    "android_channel",
                    "amazon_channel",
                    "ios_channel",
                    "channel"
                ]
            },
            "profiles": [
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "existing"
                            }
                        }
                    },
                    "identityMap": {
                        "ios_channel": [
                            {
                                "id": "ios_channel-2OjnN"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "existing"
                            }
                        }
                    },
                    "identityMap": {
                        "channel": [
                            {
                                "id": "channel-mN1Hw"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "existing"
                            }
                        }
                    },
                    "identityMap": {
                        "amazon_channel": [
                            {
                                "id": "amazon_channel-biCbJ"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "existing"
                            }
                        }
                    },
                    "identityMap": {
                        "android_channel": [
                            {
                                "id": "android_channel-MVw4L"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "existing"
                            }
                        }
                    },
                    "identityMap": {
                        "ios_channel": [
                            {
                                "id": "ios_channel-40Vrf"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "existing"
                            }
                        }
                    },
                    "identityMap": {
                        "channel": [
                            {
                                "id": "channel-MRelR"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "existing"
                            }
                        }
                    },
                    "identityMap": {
                        "amazon_channel": [
                            {
                                "id": "amazon_channel-fxt2p"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "existing"
                            }
                        }
                    },
                    "identityMap": {
                        "android_channel": [
                            {
                                "id": "android_channel-M46ze"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                }
            ],
            "output": "{\r\n    \"profiles\": [\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"ios_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"amazon_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"android_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"ios_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"amazon_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"android_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        }\r\n    ]\r\n}"
        },
        {
            "aggregationKey": {
                "destinationInstanceId": "49966037-32cd-4457-a105-2cbf9c01826a",
                "segmentId": "segmentid2",
                "segmentStatus": "realized",
                "identityNamespaces": [
                    "android_channel",
                    "amazon_channel",
                    "ios_channel",
                    "channel"
                ]
            },
            "profiles": [
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "ios_channel": [
                            {
                                "id": "ios_channel-2OjnN"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "channel": [
                            {
                                "id": "channel-mN1Hw"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "amazon_channel": [
                            {
                                "id": "amazon_channel-biCbJ"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "android_channel": [
                            {
                                "id": "android_channel-MVw4L"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "ios_channel": [
                            {
                                "id": "ios_channel-40Vrf"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "channel": [
                            {
                                "id": "channel-MRelR"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "amazon_channel": [
                            {
                                "id": "amazon_channel-fxt2p"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "android_channel": [
                            {
                                "id": "android_channel-M46ze"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                }
            ],
            "output": "{\r\n    \"profiles\": [\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"ios_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"amazon_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"android_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"ios_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"amazon_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"android_channel\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        }\r\n    ]\r\n}"
        },
        {
            "aggregationKey": {
                "destinationInstanceId": "49966037-32cd-4457-a105-2cbf9c01826a",
                "segmentId": "segmentid3",
                "segmentStatus": "exited",
                "identityNamespaces": [
                    "named_user_id"
                ]
            },
            "profiles": [
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "named_user_id": [
                            {
                                "id": "named_user_id-0Q3hp"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid3": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "exited"
                            }
                        }
                    },
                    "identityMap": {
                        "named_user_id": [
                            {
                                "id": "named_user_id-sboQe"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                }
            ],
            "output": "{\r\n    \"profiles\": [\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"named_user_id\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"named_user_id\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                ],\r\n                \"remove\": [\r\n                    \"segmentid3\"\r\n                ]\r\n            }\r\n        }\r\n    ]\r\n}"
        },
        {
            "aggregationKey": {
                "destinationInstanceId": "49966037-32cd-4457-a105-2cbf9c01826a",
                "segmentId": "segmentid1",
                "segmentStatus": "existing",
                "identityNamespaces": [
                    "named_user_id"
                ]
            },
            "profiles": [
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "existing"
                            }
                        }
                    },
                    "identityMap": {
                        "named_user_id": [
                            {
                                "id": "named_user_id-0Q3hp"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid1": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "existing"
                            }
                        }
                    },
                    "identityMap": {
                        "named_user_id": [
                            {
                                "id": "named_user_id-sboQe"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                }
            ],
            "output": "{\r\n    \"profiles\": [\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"named_user_id\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"named_user_id\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid1\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        }\r\n    ]\r\n}"
        },
        {
            "aggregationKey": {
                "destinationInstanceId": "49966037-32cd-4457-a105-2cbf9c01826a",
                "segmentId": "segmentid2",
                "segmentStatus": "realized",
                "identityNamespaces": [
                    "named_user_id"
                ]
            },
            "profiles": [
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.947+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "named_user_id": [
                            {
                                "id": "named_user_id-0Q3hp"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                },
                {
                    "segmentMembership": {
                        "ups": {
                            "segmentid2": {
                                "lastQualificationTime": "2021-10-26T17:41:55.948+0000",
                                "status": "realized"
                            }
                        }
                    },
                    "identityMap": {
                        "named_user_id": [
                            {
                                "id": "named_user_id-sboQe"
                            }
                        ]
                    },
                    "attributes": {
                        "key": {
                            "value": "string"
                        }
                    }
                }
            ],
            "output": "{\r\n    \"profiles\": [\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"named_user_id\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        },\r\n        {\r\n            \"identities\": [\r\n                {\r\n                    \"type\": \"named_user_id\",\r\n                    \"id\": \"{moviestar_region=dIqYn-moviestar_region}\"\r\n                }\r\n            ],\r\n            \"AdobeExperiencePlatformSegments\": {\r\n                \"add\": [\r\n                    \"segmentid2\"\r\n                ],\r\n                \"remove\": [\r\n                ]\r\n            }\r\n        }\r\n    ]\r\n}"
        }
    ]
}
```

## Umgang mit API-Fehlern {#api-error-handling}

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status-Codes](../../landing/troubleshooting.md#api-status-codes) und [Fehler in der Anfragekopfzeile](../../landing/troubleshooting.md#request-header-errors) im Handbuch zur Fehlerbehebung bei Platform.

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie mit der Umwandlungsvorlage der Nachricht exportierte Profile generieren können, die dem erwarteten Datenformat Ihres Ziels entsprechen. Lesen Sie [Verwendung des Destination SDK zum Konfigurieren Ihres Ziels](./configure-destination-instructions.md), um zu verstehen, wo dieser Schritt in den Prozess der Konfiguration Ihres Ziels passt.
