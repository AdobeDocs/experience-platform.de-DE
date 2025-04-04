---
keywords: Experience Platform;Profil;Echtzeit-Kundenprofil;Fehlerbehebung;API;
title: Entitäten (Profilzugriff)-API-Endpunkt
type: Documentation
description: Mit Adobe Experience Platform können Sie über RESTful-APIs oder die Benutzeroberfläche auf Echtzeit-Kundenprofildaten zugreifen. In diesem Handbuch wird beschrieben, wie Sie mithilfe der Profil-API auf Entitäten zugreifen können, die häufiger als „Profile“ bezeichnet werden.
role: Developer
exl-id: 06a1a920-4dc4-4468-ac15-bf4a6dc885d4
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1706'
ht-degree: 37%

---

# Entitäten-Endpunkt (Profilzugriff)

>[!IMPORTANT]
>
>Die ExperienceEvent-Suche mit der Profilzugriffs-API wird nicht mehr unterstützt. Verwenden Sie Funktionen wie berechnete Attribute für Anwendungsfälle, in denen ExperienceEvents nachgeschlagen werden muss. Weitere Informationen zu dieser Änderung erhalten Sie bei der Adobe-Kundenunterstützung.

Adobe Experience Platform ermöglicht den Zugriff auf [!DNL Real-Time Customer Profile] mithilfe von RESTful-APIs oder der Benutzeroberfläche. In diesem Handbuch wird beschrieben, wie Sie mithilfe der API auf Entitäten, meist als „Profile“ bezeichnet, zugreifen können. Weiterführende Informationen zum Zugriff auf Profile über die [!DNL Experience Platform]-Benutzeroberfläche finden Sie im [Benutzerhandbuch für Profile](../ui/user-guide.md).

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil von [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Bevor Sie fortfahren, schauen Sie bitte im Handbuch in [Erste Schritte](getting-started.md) nach Links zu entsprechenden Dokumentationen, einem Leitfaden zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtigen Informationen zu erforderlichen Kopfzeilen, die für das Aufrufen einer [!DNL Experience Platform]-API erforderlich sind.

## Abrufen einer Entität {#retrieve-entity}

Sie können eine Profilentität abrufen, indem Sie eine GET-Anfrage zusammen mit den erforderlichen Abfrageparametern an den `/access/entities`-Endpunkt stellen.

>[!BEGINTABS]

>[!TAB Profilentität]

**API-Format**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

Die im Anfragepfad bereitgestellten Abfrageparameter geben an, auf welche Daten zugegriffen werden soll. Sie können mehrere Parameter einbeziehen, die durch kaufmännische Und-Zeichen (&amp;) voneinander getrennt werden.

Um auf eine Profilentität zuzugreifen **müssen** die folgenden Abfrageparameter angeben:

- `schema.name`: Der Name des XDM-Schemas der Entität. In diesem Anwendungsbeispiel wird die `schema.name=_xdm.context.profile`.
- `entityId`: Die ID der Entität, die Sie abrufen möchten.
- `entityIdNS`: Der Namespace der Entität, die Sie abrufen möchten. Dieser Wert muss angegeben werden, wenn die `entityId` **keine** XID ist.

Eine vollständige Liste der gültigen Parameter finden Sie im Abschnitt [Abfrageparameter](#query-parameters) des Anhangs.

**Anfrage**

Mit der folgenden Anfrage werden die E-Mail-Adresse und der Name eines Kunden mithilfe einer Identität abgerufen.

+++ Eine Beispielanfrage zum Abrufen einer Entität mithilfe einer Identität

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email&fields=identities,person.name,workEmail' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 für die angeforderte Entität zurückgegeben.

+++ Eine Beispielantwort, die die angeforderte Entität enthält

```json
{
    "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA": {
        "entityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316601",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "johnsmith@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316604",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "58832431024964181144308914570411162539",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-28T20:57:24Z"
    }
}
```

+++

>[!NOTE]
>
>Wenn ein verwandtes Diagramm mehr als 50 Identitäten verknüpft, gibt dieser Service den HTTP-Status 422 und die Meldung „Zu viele verwandte Identitäten“ zurück. Wenn Sie diese Fehlermeldung erhalten, sollten Sie weitere Abfrageparameter hinzufügen, um die Suche einzuschränken.

>[!TAB B2B-Konto]

**API-Format**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

Die im Anfragepfad bereitgestellten Abfrageparameter geben an, auf welche Daten zugegriffen werden soll. Sie können mehrere Parameter einbeziehen, die durch kaufmännische Und-Zeichen (&amp;) voneinander getrennt werden.

Um auf die B2B-Kontodaten zuzugreifen **müssen** die folgenden Abfrageparameter angeben:

- `schema.name`: Der Name des XDM-Schemas der Entität. In diesem Anwendungsfall wird dieser Wert `schema.name=_xdm.context.account`.
- `entityId`: Die ID der Entität, die Sie abrufen möchten.
- `entityIdNS`: Der Namespace der Entität, die Sie abrufen möchten. Dieser Wert muss angegeben werden, wenn die `entityId` **keine** XID ist.

Eine vollständige Liste der gültigen Parameter finden Sie im Abschnitt [Abfrageparameter](#query-parameters) des Anhangs.

**Anfrage**

+++ Beispielanfrage zum Abrufen eines B2B-Kontos

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.account&entityIdNs=b2b_account&entityId=2334262' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 für die angeforderte Entität zurückgegeben.

+++ Eine Beispielantwort, die die angeforderte Entität enthält

```json
{
    "GuQ-AUFjgjaeIw": {
        "entityId": "GuQ-AUFjgjaeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "{SOURCE_ID}",
                    "sourceKey": "{SOURCE_KEY}",
                    "sourceInstanceID": "{SOURCE_INSTANCE_ID}",
                    "sourceType": "{SOURCE_TYPE}"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_account": [
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    },
                    {
                        "id": "{SOURCE_ID}"
                    }
                ]
            },
            "isDeleted": false,
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    }
}
```

+++

>[!TAB B2B-Opportunity]

**API-Format**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

Die im Anfragepfad bereitgestellten Abfrageparameter geben an, auf welche Daten zugegriffen werden soll. Sie können mehrere Parameter einbeziehen, die durch kaufmännische Und-Zeichen (&amp;) voneinander getrennt werden.

Um auf eine B2B-Opportunity-Entität zuzugreifen **müssen** die folgenden Abfrageparameter angeben:

- `schema.name`: Der Name des XDM-Schemas der Entität. In diesem Anwendungsbeispiel wird die `schema.name=_xdm.context.opportunity`.
- `entityId`: Die ID der Entität, die Sie abrufen möchten.
- `entityIdNS`: Der Namespace der Entität, die Sie abrufen möchten. Dieser Wert muss angegeben werden, wenn die `entityId` **keine** XID ist.

Eine vollständige Liste der gültigen Parameter finden Sie im Abschnitt [Abfrageparameter](#query-parameters) des Anhangs.

**Anfrage**

+++ Beispielanfrage zum Abrufen einer B2B-Opportunity-Entität

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.opportunity&entityIdNs=b2b_opportunity&entityId=2334262' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 für die angeforderte Entität zurückgegeben.

+++ Eine Beispielantwort, die die angeforderte Entität enthält

```json
{
  "Ggw_AUFjgjaeIw": {
        "entityId": "Ggw_AUFjgjaeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    },
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    }
}
```

+++

>[!ENDTABS]

## Mehrere Entitäten abrufen {#retrieve-entities}

Sie können mehrere Profilentitäten abrufen, indem Sie eine POST-Anfrage an den `/access/entities`-Endpunkt senden und die Identitäten in der Payload angeben.

>[!BEGINTABS]

>[!TAB Profilentitäten]

**API-Format**

```http
POST /access/entities
```

**Anfrage**

Mit der folgenden Anfrage werden die Namen und E-Mail-Adressen mehrerer Kunden anhand einer Liste von Identitäten abgerufen.

+++Eine Beispielanfrage zum Abrufen mehrerer Entitäten

```shell
curl -X POST https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "schema":{
            "name":"_xdm.context.profile"
        },
        "fields":[
            "identities",
            "person.name",
            "workEmail"
        ],
        "identities":[
            {
                "entityId":"89149270342662559642753730269986316601",
                "entityIdNS":{
                    "code":"ECID"
                }
            },
            {
                "entityId":"89149270342662559642753730269986316900",
                "entityIdNS":{
                    "code":"ECID"
                }
            },
            {
                "entityId":"89149270342662559642753730269986316602",
                "entityIdNS":{
                    "code":"ECID"
                }
            }
        ],
        "timeFilter": {
            "startTime": 1539838505,
            "endTime": 1539838510
        },
        "limit": 10,
        "orderby": "-timestamp"
      }'
```

| Eigenschaft | Typ | Beschreibung |
| -------- |----- | ----------- |
| `schema.name` | Zeichenfolge | **(Erforderlich)** Der Name des XDM-Schemas, zu dem die Entität gehört. |
| `fields` | Array | Die XDM-Felder, die zurückgegeben werden sollen, als Array von Zeichenfolgen. Standardmäßig werden alle Felder zurückgegeben. |
| `identities` | Array | **(Erforderlich)** Ein Array mit einer Liste von Identitäten für die Entitäten, auf die Sie zugreifen möchten. |
| `identities.entityId` | String | Die Kennung einer Entität, auf die Sie zugreifen möchten. |
| `identities.entityIdNS.code` | String | Der Namespace einer Entitätskennung, auf die Sie zugreifen möchten. |
| `timeFilter.startTime` | Ganzzahl | Gibt die Startzeit zum Filtern von Profilentitäten an (in Millisekunden). Standardmäßig wird dieser Wert als Beginn der verfügbaren Zeit festgelegt. |
| `timeFilter.endTime` | Ganzzahl | Gibt die Endzeit zum Filtern von Profilentitäten an (in Millisekunden). Standardmäßig wird dieser Wert als Ende der verfügbaren Zeit festgelegt. |
| `limit` | Ganzzahl | Die maximale Anzahl an zurückzugebenden Datensätzen. Standardmäßig ist dieser Wert auf 1000 festgelegt. |
| `orderby` | String | Die Sortierreihenfolge der abgerufenen Erlebnisereignisse nach Zeitstempel, geschrieben als `(+/-)timestamp`, wobei `+timestamp` die Standardeinstellung ist. |

+++

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit den angeforderten Feldern von Entitäten zurückgegeben, die im Anfragetext angegeben sind.

+++ Eine Beispielantwort, die die angeforderten Entitäten enthält

```json
{
    "A29cgveD5y64ezlhxjUXNzcm": {
        "entityId": "A29cgveD5y64ezlhxjUXNzcm",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316601",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "05DD23564EC4607F0A490D44",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316603",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janesmith@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316604",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316700",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316701",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "58832431024964181144308914570411162539",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-28T20:57:24Z"
    },
    "A29cgveD5y64e2RixjUXNzcm": {
        "entityId": "A29cgveD5y64e2RixjUXNzcm",
        "sources": [
            ""
        ],
        "entity": {},
        "lastModifiedAt": "1970-01-01T00:00:00Z"
    },
    "A29cgveD5y64ezphxjUXNzcm": {
        "entityId": "A29cgveD5y64ezphxjUXNzcm",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-27T23:25:52Z"
    }
}
```

+++

>[!TAB B2B-Konto]

**API-Format**

```http
POST /access/entities
```

**Anfrage**

Mit der folgenden Anfrage werden die angeforderten B2B-Konten abgerufen.

+++Eine Beispielanfrage zum Abrufen mehrerer Entitäten

```shell
curl -X POST https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "schema":{
            "name":"_xdm.context.account"
        },
        "identities": [
            {
                "entityId": "2334262",
                "entityIdNS": {
                    "code":"b2b_account"
                }
            },
            {
                "entityId": "2334263",
                "entityIdNS": {
                    "code":"b2b_account"
                }
            },
            {
                "entityId": "2334264",
                "entityIdNS": {
                    "code":"b2b_account"
                }
            }
        ]
    }'
```

| Eigenschaft | Typ | Beschreibung |
| -------- |----- | ----------- |
| `schema.name` | Zeichenfolge | **(Erforderlich)** Der Name des XDM-Schemas, zu dem die Entität gehört. |
| `identities` | Array | **(Erforderlich)** Ein Array mit einer Liste von Identitäten für die Entitäten, auf die Sie zugreifen möchten. |
| `identities.entityId` | String | Die Kennung einer Entität, auf die Sie zugreifen möchten. |
| `identities.entityIdNS.code` | String | Der Namespace einer Entitätskennung, auf die Sie zugreifen möchten. |

+++

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit den angeforderten Entitäten zurückgegeben.

+++ Eine Beispielantwort, die die angeforderten Entitäten enthält

```json
{
    "GuQ-AUFjgjeeIw": {
        "requestedIdentity": {
            "entityId": "2334263",
            "entityIdNS": {
                "code": "b2b_account"
            }
        },
        "entityId": "GuQ-AUFjgjeeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_account": [
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    },
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "GuQ-AUFjgjaeIw": {
        "requestedIdentity": {
            "entityId": "2334262",
            "entityIdNS": {
                "code": "b2b_account"
            }
        },
        "entityId": "GuQ-AUFjgjaeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_account": [
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    },
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "GuQ-AUFjgjmeIw": {
        "requestedIdentity": {
            "entityId": "2334265",
            "entityIdNS": {
                "code": "b2b_account"
            }
        },
        "entityId": "GuQ-AUFjgjmeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334265",
            "identityMap": {
            "b2b_account": [
                {
                    "id": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                },
                {
                    "id": "2334265"
                }
            ]
        },
        "isDeleted": false,
        "accountKey": {
            "sourceID": "2334265",
            "sourceKey": "2334265",
            "sourceInstanceID": "2334265",
            "sourceType": "Random"
        }
    }
}
```

+++

>[!TAB B2B-Opportunity]

**API-Format**

```http
POST /access/entities
```

**Anfrage**

Mit der folgenden Anfrage werden die angeforderten B2B-Opportunitys abgerufen.

+++ Eine Beispielanfrage zum Abrufen mehrerer Entitäten

```shell
curl -X POST https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "schema":{
            "name":"_xdm.context.opportunity"
        },
        "identities": [
            {
                "entityId": "2334262",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            },
            {
                "entityId": "2334263",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            },
            {
                "entityId": "2334264",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            },
            {
                "entityId": "2334265",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            }
        ]
    }'
```

| Eigenschaft | Typ | Beschreibung |
| -------- |----- | ----------- |
| `schema.name` | Zeichenfolge | **(Erforderlich)** Der Name des XDM-Schemas, zu dem die Entität gehört. |
| `identities` | Array | **(Erforderlich)** Ein Array mit einer Liste von Identitäten für die Entitäten, auf die Sie zugreifen möchten. |
| `identities.entityId` | String | Die Kennung einer Entität, auf die Sie zugreifen möchten. |
| `identities.entityIdNS.code` | String | Der Namespace einer Entitätskennung, auf die Sie zugreifen möchten. |

+++

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit den angeforderten Entitäten zurückgegeben.

+++ Eine Beispielantwort, die die angeforderten Entitäten enthält

```json
{
    "Ggw_AUFjgjaeIw": {
        "requestedIdentity": {
            "entityId": "2334262",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjaeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    },
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "Ggw_AUFjgjieIw": {
        "requestedIdentity": {
            "entityId": "2334264",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjieIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0041c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334264",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "2334264"
                    },
                    {
                        "id": "0041c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334264",
                "sourceKey": "2334264",
                "sourceInstanceID": "2334264",
                "sourceType": "Salesforce"
            }
        }
    },
    "Ggw_AUFjgjeeIw": {
        "requestedIdentity": {
            "entityId": "2334263",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjeeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    },
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "Ggw_AUFjgjmeIw": {
        "requestedIdentity": {
            "entityId": "2334265",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjmeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334265",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "2334265"
                    },
                    {
                        "id": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334265",
                "sourceKey": "2334265",
                "sourceInstanceID": "2334265",
                "sourceType": "Random"
            }
        }
    }
}
```

+++

>[!ENDTABS]

### Auf eine nachfolgende Ergebnisseite zugreifen

Ergebnisse werden beim Abrufen von Zeitreihenereignissen paginiert. Wenn es weitere Seiten mit Ergebnissen gibt, enthält die `_page.next`-Eigenschaft eine Kennung. Darüber hinaus stellt die `_links.next.href`-Eigenschaft einen Anfrage-URI zum Abrufen der nächsten Seite bereit. Um die Ergebnisse abzurufen, stellen Sie eine weitere GET-Anfrage an den `/access/entities`-Endpunkt und ersetzen Sie `/entities` durch den Wert des bereitgestellten URI.

>[!NOTE]
>
>Stellen Sie sicher, dass Sie `/entities/` nicht versehentlich im Anfragepfad wiederholen. Es sollte nur einmal erscheinen, wie hier: `/access/entities?start=...`.

**API-Format**

```http
GET /access/{NEXT_URI}
```

| Parameter | Beschreibung |
|---|---|
| `{NEXT_URI}` | Der URI-Wert, der aus `_links.next.href` stammt. |

**Anfrage**

Die folgende Anfrage ruft die nächste Ergebnisseite ab, indem der `_links.next.href`-URI als Anfragepfad verwendet wird.

+++ Beispielanfrage für den Zugriff auf die nächste Ergebnisseite

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt die nächste Ergebnisseite zurück. Diese Antwort enthält keine nachfolgenden Ergebnisseiten, erkennbar an den leeren Zeichenfolgenwerten von `_page.next` und `_links.next.href`.

+++ Eine Beispielantwort, die die nächste Seite von Entitäten enthält

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "c8d11988-6b56-4571-a123-b6ce74236037",
        "count": 1,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "A29cgveD5y64e2RixjUXNzcm",
            "entityId": "c8d11988-6b56-4571-a123-b6ce74236037",
            "timestamp": 1531260477000,
            "entity": {
                "endUserIDs": {
                    "_experience": {
                        "ecid": {
                            "id": "89149270342662559642753730269986316900",
                            "namespace": {
                                "code": "ecid"
                            }
                        }
                    }
                },
                "channel": {
                    "_type": "web"
                },
                "web": {
                    "webPageDetails": {
                        "name": "Fernie Snow",
                        "pageViews": {
                            "value": 1
                        }
                    }
                }
            },
            "lastModifiedAt": "2018-08-21T06:50:01Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

+++

## Löschen einer Entität {#delete-entity}

Sie können eine Entität aus dem Profilspeicher löschen, indem Sie eine DELETE-Anfrage an den Endpunkt `/access/entities` zusammen mit den erforderlichen Abfrageparametern stellen.

**API-Format**

```http
DELETE /access/entities?{QUERY_PARAMETERS}
```

Die im Anfragepfad bereitgestellten Abfrageparameter geben an, auf welche Daten zugegriffen werden soll. Sie können mehrere Parameter einbeziehen, die durch kaufmännische Und-Zeichen (&amp;) voneinander getrennt werden.

Um eine Entität zu löschen **müssen** die folgenden Abfrageparameter angeben:

- `schema.name`: Der Name des XDM-Schemas der Entität. In diesem Anwendungsfall können Sie `schema.name=_xdm.context.profile` **nur** verwenden.
- `entityId`: Die ID der Entität, die Sie abrufen möchten.
- `entityIdNS`: Der Namespace der Entität, die Sie abrufen möchten. Dieser Wert muss angegeben werden, wenn die `entityId` **keine** XID ist.
- `mergePolicyId`: Die Zusammenführungsrichtlinien-ID der Entität. Die Zusammenführungsrichtlinie enthält Informationen zur Identitätszuordnung und zum Zusammenführen von Schlüssel-Wert-XDM-Objekten. Wenn dieser Wert nicht angegeben wird, wird die standardmäßige Zusammenführungsrichtlinie verwendet.

**Anfrage**

Die folgende Anfrage löscht die angegebene Entität.

+++ Beispielanfrage zum Löschen einer Entität

```shell
curl -X DELETE 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 202 mit einem leeren Antworttext zurück.

## Nächste Schritte

Mithilfe dieses Handbuchs haben Sie erfolgreich auf [!DNL Real-Time Customer Profile] Datenfelder, Profile und Zeitreihendaten zugegriffen. Informationen zum Zugriff auf andere in [!DNL Experience Platform] gespeicherte Datenressourcen finden Sie unter [Datenzugriff - Übersicht](../../data-access/home.md).

## Anhang {#appendix}

Der folgende Abschnitt enthält zusätzliche Informationen zum Zugriff auf [!DNL Profile] Daten mithilfe der -API.

### Abfrageparameter {#query-parameters}

Die folgenden Parameter werden im Pfad für GET-Anfragen an den `/access/entities`-Endpunkt verwendet. Sie dienen dazu, die Profilentität anzugeben, auf die Sie zugreifen möchten, und die in der Antwort zurückgegebenen Daten zu filtern. Erforderliche Parameter sind markiert, während der Rest optional ist.

| Parameter | Beschreibung | Beispiel |
| --------- | ----------- | ------- |
| `schema.name` | **(Erforderlich)** Der Name des XDM-Schemas der Entität. | `schema.name=_xdm.context.profile` |
| `relatedSchema.name` | Wenn `schema.name` `_xdm.context.experienceevent` ist, **dieser Wert (muss** das Schema für die Profilentität angeben, auf die sich die Zeitreihenereignisse beziehen. | `relatedSchema.name=_xdm.context.profile` |
| `entityId` | **(Erforderlich)** Die ID der Entität. Wenn der Wert dieses Parameters keine XID ist, muss auch ein Identity-Namespace-Parameter (`entityIdNS`) angegeben werden. | `entityId=janedoe@example.com` |
| `entityIdNS` | Wenn `entityId` nicht als XID angegeben wird, muss **Feld** Identity-Namespace angeben. | `entityIdNS=email` |
| `relatedEntityId` | Wenn `schema.name` `_xdm.context.experienceevent` ist, muss **Wert** ID der zugehörigen Profilentität angeben. Dieser Wert folgt denselben Regeln wie `entityId`. | `relatedEntityId=69935279872410346619186588147492736556` |
| `relatedEntityIdNS` | Wenn `schema.name` den Wert „_xdm.context.experience“ hat, muss dieser Wert den Identitäts-Namespace für die in `relatedEntityId` festgelegte Entität angeben. | `relatedEntityIdNS=CRMID` |
| `fields` | Filtert die in der Antwort zurückgegebenen Daten. Geben Sie hier an, welche Schemafeldwerte in abgerufene Daten einbezogen werden sollen. Trennen Sie Werte bei mehreren Feldern durch ein Komma ohne Leerzeichen dazwischen. | `fields=personalEmail,person.name,person.gender` |
| `mergePolicyId` | Gibt die Zusammenführungsrichtlinie an, mit der die zurückgegebenen Daten gesteuert werden. Wenn im Aufruf keine Zusammenführungsrichtlinie angegeben ist, wird die Standardeinstellung Ihrer Organisation für dieses Schema verwendet. Wenn keine standardmäßige Zusammenführungsrichtlinie konfiguriert wurde, ist der Standardwert keine Profilzusammenführung und keine Identitätszuordnung. | `mergePolicyId=5aa6885fcf70a301dabdfa4a` |
| `orderBy` | Die Sortierreihenfolge der abgerufenen Entitäten nach Zeitstempel. Dies wird als `(+/-)timestamp` geschrieben, wobei der Standard `+timestamp` wird. | `orderby=-timestamp` |
| `startTime` | Gibt die Startzeit zum Filtern der Entitäten an (in Millisekunden). | `startTime=1539838505` |
| `endTime` | Gibt die Endzeit zum Filtern von Entitäten an (in Millisekunden). | `endTime=1539838510` |
| `limit` | Gibt die maximale Anzahl an zurückzugebenden Entitäten an. Standardmäßig ist dieser Wert auf 1000 festgelegt. | `limit=100` |
| `property` | Filtert nach dem Eigenschaftswert. Dieser Abfrageparameter unterstützt die folgenden Auswerter: =, !=, &lt;, &lt;=, >, >= Dies kann nur mit Erlebnisereignissen verwendet werden, wobei maximal drei Eigenschaften unterstützt werden. | `property=webPageDetails.isHomepage=true&property=localTime<="2020-07-20"` |
