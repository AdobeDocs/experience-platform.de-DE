---
keywords: Experience Platform;Profil;Echtzeit-Kundenprofil;Fehlerbehebung;API;
title: API-Endpunkt "Entitäten (Profilzugriff)"
type: Documentation
description: Mit Adobe Experience Platform können Sie mithilfe von RESTful-APIs oder der Benutzeroberfläche auf Echtzeit-Kundenprofil-Daten zugreifen. In diesem Handbuch wird beschrieben, wie Sie mithilfe der Profil-API auf Entitäten zugreifen, die häufiger als "Profile"bezeichnet werden.
exl-id: 06a1a920-4dc4-4468-ac15-bf4a6dc885d4
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1732'
ht-degree: 89%

---

# Entitäten-Endpunkt (Profilzugriff)

Adobe Experience Platform ermöglicht Ihnen den Zugriff auf [!DNL Real-Time Customer Profile] Daten mithilfe von RESTful-APIs oder der Benutzeroberfläche. In diesem Handbuch wird beschrieben, wie Sie mithilfe der API auf Entitäten, meist als „Profile“ bezeichnet, zugreifen können. Weitere Informationen zum Zugriff auf Profile mithilfe des [!DNL Platform] Benutzeroberfläche, siehe [Profil-Benutzerhandbuch](../ui/user-guide.md).

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil von [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Bevor Sie fortfahren, schauen Sie bitte im Handbuch in [Erste Schritte](getting-started.md) nach Links zu entsprechenden Dokumentationen, einem Leitfaden zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtigen Informationen zu erforderlichen Kopfzeilen, die für das Aufrufen einer [!DNL Experience Platform]-API erforderlich sind.

## Zugriff auf Profildaten nach Identität

Sie können auf eine [!DNL Profile] -Entität, indem Sie eine GET-Anfrage an die `/access/entities` -Endpunkt und Angabe der Identität der Entität als Reihe von Abfrageparametern. Diese Identität besteht aus einem ID-Wert (`entityId`) und dem Identitäts-Namespace (`entityIdNS`).

Die im Anfragepfad bereitgestellten Abfrageparameter geben an, auf welche Daten zugegriffen werden soll. Sie können mehrere Parameter einschließen, getrennt durch ein kaufmännisches Und-Zeichen (&amp;). Eine vollständige Liste der gültigen Parameter finden Sie im Abschnitt [Abfrageparameter](#query-parameters) des Anhangs.

**API-Format**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**Anfrage**

Die folgende Anfrage ruft die E-Mail-Adresse und den Namen eines Kunden mit einer Identität ab:

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email&fields=identities,person.name,workEmail' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

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

>[!NOTE]
>
>Wenn ein verwandtes Diagramm mehr als 50 Identitäten verknüpft, gibt dieser Service den HTTP-Status 422 und die Meldung „Zu viele verwandte Identitäten“ zurück. Wenn Sie diese Fehlermeldung erhalten, sollten Sie weitere Abfrageparameter hinzufügen, um die Suche einzuschränken.

## Profildaten anhand von Liste mit Identitäten aufrufen

Sie können anhand von Identitäten auf verschiedene Profilentitäten zugreifen, indem Sie eine POST-Anfrage an den `/access/entities`-Endpunkt senden und die Identitäten in der Payload angeben. Diese Identitäten bestehen aus einem ID-Wert (`entityId`) und einem Identitäts-Namespace (`entityIdNS`).

**API-Format**

```http
POST /access/entities
```

**Anfrage**

Mit der folgenden Anfrage werden die Namen und E-Mail-Adressen mehrerer Kunden anhand einer Liste von Identitäten abgerufen:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/access/entities \
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
        "orderby": "-timestamp",
        "withCA": true
      }'
```

| Eigenschaft | Beschreibung |
|---|---|
| `schema.name` | ***(Erforderlich)*** Der Name des XDM-Schemas, zu dem die Entität gehört. |
| `fields` | Die XDM-Felder, die zurückgegeben werden sollen, als Array von Zeichenfolgen. Standardmäßig werden alle Felder zurückgegeben. |
| `identities` | ***(Erforderlich)*** Ein Array mit einer Liste von Identitäten für die Entitäten, auf die Sie zugreifen möchten. |
| `identities.entityId` | Die Kennung einer Entität, auf die Sie zugreifen möchten. |
| `identities.entityIdNS.code` | Der Namespace einer Entitätskennung, auf die Sie zugreifen möchten. |
| `timeFilter.startTime` | Startzeit des Zeitbereichfilters, eingeschlossen. Muss eine Granularität im Millisekundenbereich aufweisen. Die Standardeinstellung ist, falls nicht angegeben, der Beginn der verfügbaren Zeit. |
| `timeFilter.endTime` | Endzeit des Zeitbereichfilters, ausgeschlossen. Muss eine Granularität im Millisekundenbereich aufweisen. Wenn kein Wert angegeben ist, ist der Standardwert das Ende der verfügbaren Zeit. |
| `limit` | Anzahl der zurückzugebenden Datensätze. Gilt nur für die Anzahl der zurückgegebenen Erlebnisereignisse. Standardwert: „1.000“. |
| `orderby` | Die Sortierreihenfolge der abgerufenen Erlebnisereignisse nach Zeitstempel, geschrieben als `(+/-)timestamp`, wobei `+timestamp` die Standardeinstellung ist. |
| `withCA` | Feature Flag zur Aktivierung berechneter Attribute für das Nachschlagen. Standardwert: „false“. |

**Antwort** Eine erfolgreiche Antwort gibt die angeforderten Felder von Entitäten zurück, die im Anfragentext angegeben sind.

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

## Auf Zeitreihenereignisse für ein Profil nach Identität zugreifen

Sie können auf Zeitreihenereignisse anhand der Identität der zugehörigen Profilentität zugreifen, indem Sie eine GET-Anfrage an den `/access/entities`-Endpunkt senden. Diese Identität besteht aus einem ID-Wert (`entityId`) und einem Identitäts-Namespace (`entityIdNS`).

Die im Anfragepfad bereitgestellten Abfrageparameter geben an, auf welche Daten zugegriffen werden soll. Sie können mehrere Parameter einschließen, getrennt durch ein kaufmännisches Und-Zeichen (&amp;). Eine vollständige Liste der gültigen Parameter finden Sie im Abschnitt [Abfrageparameter](#query-parameters) des Anhangs.

**API-Format**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**Anfrage**

Die folgende Anfrage sucht nach einer Profilentität anhand der Kennung und ruft für alle Zeitreihenereignisse, die der Entität zugeordnet sind, die Werte der Eigenschaften `endUserIDs`, `web` und `channel` ab.

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine paginierte Liste mit Zeitreihenereignissen und zugehörigen Feldern zurück, die in den Abfrageparametern der Anfrage angegeben wurden.

>[!NOTE]
>
>In der Anfrage wurde eine Grenze von 1 (`limit=1`) festgelegt; daher ist der `count`-Wert in der Antwort unten 1 und wird nur eine Entität zurückgegeben.

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "c8d11988-6b56-4571-a123-b6ce74236036",
        "count": 1,
        "next": "c8d11988-6b56-4571-a123-b6ce74236037"
    },
    "children": [
        {
            "relatedEntityId": "A29cgveD5y64e2RixjUXNzcm",
            "entityId": "c8d11988-6b56-4571-a123-b6ce74236036",
            "timestamp": 1531260476000,
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
            "lastModifiedAt": "2018-08-21T06:49:02Z"
        }
    ],
    "_links": {
        "next": {
            "href": "/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1"
        }
    }
}
```

### Auf eine nachfolgende Ergebnisseite zugreifen

Ergebnisse werden beim Abrufen von Zeitreihenereignissen paginiert. Wenn es weitere Seiten mit Ergebnissen gibt, enthält die `_page.next`-Eigenschaft eine Kennung. Darüber hinaus stellt die `_links.next.href`-Eigenschaft einen Anfrage-URI zum Abrufen der nächsten Seite bereit. Um die Ergebnisse abzurufen, senden Sie eine weitere GET-Anfrage an den `/access/entities`-Endpunkt. Sie müssen jedoch sicherstellen, dass Sie `/entities` durch den Wert des angegebenen URI ersetzen.

>[!NOTE]
>
>Sorgen Sie dafür, dass Sie `/entities/` im Anfragepfad nicht versehentlich wiederholen. Es sollte nur einmal erscheinen, wie hier: `/access/entities?start=...`.

**API-Format**

```http
GET /access/{NEXT_URI}
```

| Parameter | Beschreibung |
|---|---|
| `{NEXT_URI}` | Der URI-Wert, der aus `_links.next.href` stammt. |

**Anfrage**

Die folgende Anfrage ruft die nächste Ergebnisseite ab, indem der `_links.next.href`-URI als Anfragepfad verwendet wird.

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die nächste Ergebnisseite zurück. Diese Antwort enthält keine nachfolgenden Ergebnisseiten, erkennbar an den leeren Zeichenfolgenwerten von `_page.next` und `_links.next.href`.

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

## Auf Zeitreihenereignisse für mehrere Profile nach Identitäten zugreifen

Sie können auf Zeitreihenereignisse aus mehreren verknüpften Profilen zugreifen, indem Sie eine POST-Anfrage an den `/access/entities`-Endpunkt senden und die Profilidentitäten in der Payload angeben. Diese Identitäten bestehen jeweils aus einem ID-Wert (`entityId`) und einem Identitäts-Namespace (`entityIdNS`).

**API-Format**

```http
POST /access/entities
```

**Anfrage**

Mit der folgenden Anfrage werden Benutzerkennungen, Ortszeiten und Ländercodes für Zeitreihenfolgenereignisse abgerufen, die mit einer Liste von Profilidentitäten verknüpft sind:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema": {
        "name": "_xdm.context.experienceevent"
    },
    "relatedSchema": {
        "name": "_xdm.context.profile"
    },
    "identities": [
        {
            "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW"
        }
        {
            "relatedEntityId": "GkouAW-2u-7iWt5vQ9u2wm40JOZY"
        }
    ],
    "fields": [
        "endUserIDs",
        "placeContext.localTime",
        "placeContext.geo.countryCode"
    ],
    
    "timeFilter": {
        "startTime": 11539838505
        "endTime": 1539838510
    },
    "limit": 10
}'
```

| Eigenschaft | Beschreibung |
|---|---|
| `schema.name` | **(ERFORDERLICH)** Das XDM-Schema der Entität, die abgerufen werden soll. |
| `relatedSchema.name` | Wenn `schema.name` den Wert `_xdm.context.experienceevent` hat, muss dieser Wert das Schema für die Profilentität angeben, mit der die Zeitreihenereignisse verbunden sind. |
| `identities` | **(ERFORDERLICH)** Ein Array, das Profile auflistet, aus denen zugehörige Zeitreihenereignisse abgerufen werden sollen. Jeder Eintrag im Array ist auf eine der folgenden Weisen eingestellt: 1) Verwendung einer vollqualifizierten Identität, bestehend aus ID-Wert und Namespace oder 2) Bereitstellung einer XID. |
| `fields` | Isoliert die Daten, die für einen bestimmten Satz von Feldern zurückgegeben werden. Filtern Sie damit, welche Schemafelder in abgerufenen Daten enthalten sind. Beispiel: personalEmail,person.name,person.gender |
| `mergePolicyId` | Gibt die Zusammenführungsrichtlinie an, die für die zurückgegebenen Daten gelten soll. Wenn im Dienstaufruf keine Zusammenführungsrichtlinie angegeben ist, wird die Standardeinstellung Ihrer Organisation für dieses Schema verwendet. Wenn keine standardmäßige Zusammenführungsrichtlinie konfiguriert wurde, lautet die Standardeinstellung: keine Profilzusammenführung und keine Identitätszuordnung. |
| `orderby` | Die Sortierreihenfolge der abgerufenen Erlebnisereignisse nach Zeitstempel, geschrieben als `(+/-)timestamp`, wobei `+timestamp` die Standardeinstellung ist. |
| `timeFilter.startTime` | Geben Sie die Startzeit zum Filtern von Zeitreihenobjekten an (in Millisekunden). |
| `timeFilter.endTime` | Geben Sie die Endzeit zum Filtern von Zeitreihenobjekten an (in Millisekunden). |
| `limit` | Numerischer Wert, der die maximale Anzahl der zurückzugebenden Objekte angibt. Standardwert: „1000“. |
| `withCA` | Feature Flag zur Aktivierung berechneter Attribute für das Nachschlagen. Standardwert: „false“. |

**Antwort**

Eine erfolgreiche Antwort gibt eine paginierte Liste von Zeitreihenereignissen zurück, die mit den verschiedenen in der Anfrage angegebenen Profilen verknüpft sind.

```json
{
    "GkouAW-yD9aoRCPhRYROJ-TetAFW": {
        "_page": {
            "orderby": "timestamp",
            "start": "ee0fa8eb-f09c-4d72-a432-fea7f189cfcd",
            "count": 10,
            "next": "40cb2fb3-78cd-49d3-806f-9bdb22748226"
        },
        "children": [
            {
                "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW",
                "entityId": "ee0fa8eb-f09c-4d72-a432-fea7f189cfcd",
                "timestamp": 1537275882000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "67971860962043911970658021809222795905",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "50353446361742744826197433431642033796",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a00003314-2fd9c00000000026",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-18T13:04:42Z",
                        "geo": {
                            "countryCode": "MX"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:35:01Z"
            },
            {
                "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW",
                "entityId": "a9e137b4-1348-4878-8167-e308af523d8b",
                "timestamp": 1537275889000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "67971860962043911970658021809222795905",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "50353446361742744826197433431642033796",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a00003314-2fd9c00000000026",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-18T13:04:49Z",
                        "geo": {
                            "countryCode": "MX"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:35:01Z"
            }
        ],
        "_links": {
            "next": {
                "href": "/entities",
                "payload": {
                    "schema": {
                        "name": "_xdm.context.experienceevent"
                    },
                    "relatedSchema": {
                        "name": "_xdm.context.profile"
                    },
                    "timeFilter": {
                        "startTime": 1537275882000
                    },
                    "fields": [
                        "endUserIDs",
                        "placeContext.localTime",
                        "placeContext.geo.countryCode"
                    ],
                    "identities": [
                        {
                            "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW",
                            "start": "40cb2fb3-78cd-49d3-806f-9bdb22748226"
                        }
                    ],
                    "limit": 10
                }
            }
        }
    },
    "GkouAW-2u-7iWt5vQ9u2wm40JOZY": {
        "_page": {
            "orderby": "timestamp",
            "start": "2746d0db-fa64-4e29-b67e-324bec638816",
            "count": 9,
            "next": ""
        },
        "children": [
            {
                "relatedEntityId": "GkouAW-2u-7iWt5vQ9u2wm40JOZY",
                "entityId": "2746d0db-fa64-4e29-b67e-324bec638816",
                "timestamp": 1537559483000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "76436745599328540420034822220063618863",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "48593470048917738786405847327596263131",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a80007451-03da600000000028",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-21T19:51:23Z",
                        "geo": {
                            "countryCode": "US"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:34:58Z"
            },
            {
                "relatedEntityId": "GkouAW-2u-7iWt5vQ9u2wm40JOZY",
                "entityId": "9bf337a1-3256-431e-a38c-5c0d42d121d1",
                "timestamp": 1537559486000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "76436745599328540420034822220063618863",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "48593470048917738786405847327596263131",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a80007451-03da600000000028",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-21T19:51:26Z",
                        "geo": {
                            "countryCode": "US"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:34:58Z"
            }
        ],
        "_links": {
            "next": {
                "href": ""
            }
        }
    }
}`
```

In dieser Beispielantwort stellt das erste aufgelistete Profil („GkouAW-yD9aoRCPhRYROJ-TetAFW“) einen Wert für `_links.next.payload` bereit; es gibt also weitere Ergebnisseiten für dieses Profil. Weiterführende Informationen zum Zugriff auf diese zusätzlichen Ergebnisse finden Sie im folgenden Abschnitt zum [Zugreifen auf weitere Ergebnisse](#access-additional-results).

### Weitere Ergebnisse aufrufen {#access-additional-results}

Beim Abrufen von Zeitreihenereignissen werden möglicherweise viele Ergebnisse zurückgegeben; daher werden die Ergebnisse oft paginiert. Wenn für ein bestimmtes Profil nachfolgende Ergebnisseiten vorhanden sind, enthält der `_links.next.payload`-Wert für dieses Profil ein Payload-Objekt.

Mithilfe dieser Payload im Anfragetext können Sie eine weitere POST-Anfrage an den `access/entities`-Endpunkt senden, um die nachfolgende Seite der Zeitreihendaten für dieses Profil abzurufen.

## Zeitreihenereignisse in mehreren Schemaentitäten aufrufen

Sie können auf mehrere Entitäten zugreifen, die über einen Beziehungsdeskriptor miteinander verbunden sind. Im folgenden Beispiel-API-Aufruf wird davon ausgegangen, dass bereits eine Beziehung zwischen zwei Schemas definiert wurde. Weitere Informationen zu Beziehungsdeskriptoren finden Sie im [!DNL Schema Registry] API-Entwicklerhandbuch [Endpunktleitfaden für Deskriptoren](../../xdm/api/descriptors.md).

Sie können in den Anfragepfad Abfrageparameter einbeziehen, um anzugeben, auf welche Daten zugegriffen werden soll. Sie können mehrere Parameter einschließen, getrennt durch ein kaufmännisches Und-Zeichen (&amp;). Eine vollständige Liste der gültigen Parameter finden Sie im Abschnitt [Abfrageparameter](#query-parameters) des Anhangs.

**API-Format**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**Anfrage**

Mit der folgenden Anfrage wird eine Entität abgerufen, die einen zuvor eingerichteten Beziehungsdeskriptor enthält, um in verschiedenen Schemas auf Daten zuzugreifen.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/access/entities?relatedSchema.name=_xdm.context.profile&schema.name=_xdm.context.experienceevent&relatedEntityId=GkouAW-2Xkftzer3bBtHiW8GkaFL \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Antwort**

Eine erfolgreiche Antwort gibt eine paginierte Liste mit Zeitreihenereignissen zurück, die mit mehreren Entitäten verknüpft sind.

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "cb10369f-a47b-4e65-afb4-06e1ad78a648",
        "count": 1,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "GkouAW-2Xkftzer3bBtHiW8GkaFL",
            "entityId": "cb10369f-a47b-4e65-afb4-06e1ad78a648",
            "timestamp": 1564614939000,
            "entity": {
                "environment": {
                    "browserDetails": {}
                },
                "identityMap": {
                    "CRMId": [
                        {
                            "id": "78520026455138218785449796480922109723",
                            "primary": true
                        }
                    ]
                },

                "commerce": {
                    "productViews": {
                        "value": 1
                    }
                },
                "productListItems": [
                    {
                        "name": "Red shoe",
                        "quantity": 85,
                        "storesAvailableIn": [
                            "da6dced5-9574-4dda-89b5-9dc106903f80",
                            "981bb433-2ee5-4db0-a19a-449ec9dbf39f"
                        ],
                        "SKU": "8f998279-797b-4da2-9e60-88bf73a9f15a",
                        "priceTotal": 934.8
                    }
                ],
                "_id": "cb10369f-a47b-4e65-afb4-06e1ad78a648",
                "commerce": {
                    "order": {}
                },
                "placeContext": {
                    "geo": {
                        "_schema": {}
                    }
                },
                "device": {},
                "timestamp": "2019-07-31T23:15:39Z",
                "_experience": {
                    "profile": {
                        "identityNamespaces": {
                            "/productListItems[*]/SKU": {
                                "namespace": {
                                    "code": "ECID"
                                }
                            }
                        }
                    }
                }
            },
            "lastModifiedAt": "2019-10-10T00:14:19Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

### Auf eine nachfolgende Ergebnisseite zugreifen

Ergebnisse werden beim Abrufen von Zeitreihenereignissen paginiert. Wenn es weitere Seiten mit Ergebnissen gibt, enthält die `_page.next`-Eigenschaft eine Kennung. Darüber hinaus stellt die `_links.next.href`-Eigenschaft einen Anfrage-URI zum Abrufen der folgenden Seite bereit, indem zusätzliche GET-Anfragen an den `access/entities`-Endpunkt gesendet werden.

## Nächste Schritte

In diesem Handbuch haben Sie erfolgreich auf [!DNL Real-Time Customer Profile] Datenfelder, Profile und Zeitreihendaten. Informationen zum Zugriff auf andere in gespeicherte Datenressourcen [!DNL Platform], siehe [Übersicht über den Datenzugriff](../../data-access/home.md).

## Anhang {#appendix}

Im folgenden Abschnitt finden Sie zusätzliche Informationen zum Zugriff auf [!DNL Profile] Daten mithilfe der API.

### Abfrageparameter {#query-parameters}

Die folgenden Parameter werden im Pfad für GET-Anfragen an den `/access/entities`-Endpunkt verwendet. Sie dienen dazu, die Profilentität anzugeben, auf die Sie zugreifen möchten, und die in der Antwort zurückgegebenen Daten zu filtern. Erforderliche Parameter sind markiert, während der Rest optional ist.

| Parameter | Beschreibung | Beispiel |
|---|---|---|
| `schema.name` | **(ERFORDERLICH)** Das XDM-Schema der Entität, die abgerufen werden soll. | `schema.name=_xdm.context.experienceevent` |
| `relatedSchema.name` | Wenn `schema.name` den Wert „_xdm.context.experience“ hat, muss dieser Wert das Schema für die Profilentität angeben, mit dem die Zeitreihenereignisse verbunden sind. | `relatedSchema.name=_xdm.context.profile` |
| `entityId` | **(ERFORDERLICH)** Die Kennung der Entität. Wenn der Wert dieses Parameters keine XID ist, muss auch ein Identitäts-Namespace-Parameter angegeben werden (siehe `entityIdNS` unten). | `entityId=janedoe@example.com` |
| `entityIdNS` | Wenn `entityId` nicht als XID angegeben wird, muss dieses Feld den Identitäts-Namespace angeben. | `entityIdNE=email` |
| `relatedEntityId` | Wenn `schema.name` den Wert „_xdm.context.experience“ hat, muss dieser Wert den Identitäts-Namespace der verwandten Profilentität angeben. Dieser Wert folgt denselben Regeln wie `entityId`. | `relatedEntityId=69935279872410346619186588147492736556` |
| `relatedEntityIdNS` | Wenn `schema.name` den Wert „_xdm.context.experience“ hat, muss dieser Wert den Identitäts-Namespace für die in `relatedEntityId` festgelegte Entität angeben. | `relatedEntityIdNS=CRMID` |
| `fields` | Filtert die in der Antwort zurückgegebenen Daten. Geben Sie hier an, welche Schemafeldwerte in abgerufene Daten einbezogen werden sollen. Trennen Sie bei mehreren Feldern die Werte durch ein Komma ohne Leerzeichen dazwischen. | `fields=personalEmail,person.name,person.gender` |
| `mergePolicyId` | Gibt die Zusammenführungsrichtlinie an, die für die zurückgegebenen Daten gelten soll. Wenn im Aufruf keine Zusammenführungsrichtlinie angegeben ist, wird die Standardeinstellung Ihrer Organisation für dieses Schema verwendet. Wenn keine standardmäßige Zusammenführungsrichtlinie konfiguriert wurde, lautet die Standardeinstellung: keine Profilzusammenführung und keine Identitätszuordnung. | `mergePoilcyId=5aa6885fcf70a301dabdfa4a` |
| `orderBy` | Die Sortierreihenfolge der abgerufenen Erlebnisereignisse nach Zeitstempel, geschrieben als `(+/-)timestamp`, wobei `+timestamp` die Standardeinstellung ist. | `orderby=-timestamp` |
| `startTime` | Geben Sie die Startzeit zum Filtern von Zeitreihenobjekten an (in Millisekunden). | `startTime=1539838505` |
| `endTime` | Geben Sie die Endzeit zum Filtern von Zeitreihenobjekten an (in Millisekunden). | `endTime=1539838510` |
| `limit` | Numerischer Wert, der die maximale Anzahl der zurückzugebenden Objekte angibt. Standardwert: „1000“. | `limit=100` |
| `property` | Filtert nach dem Eigenschaftswert. Unterstützt die folgenden Auswerter: =, !=, &lt;, &lt;=, >, >=. Kann nur mit Erlebnisereignissen verwendet werden, wobei maximal drei Eigenschaften unterstützt werden. | `property=webPageDetails.isHomepage=true&property=localTime<="2020-07-20"` |
| `withCA` | Feature Flag zur Aktivierung berechneter Attribute für das Nachschlagen. Standardwert: „false“. | `withCA=true` |
