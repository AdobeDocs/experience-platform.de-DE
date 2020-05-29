---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Entwicklerhandbuch für Customer Profil-API in Echtzeit
topic: guide
translation-type: tm+mt
source-git-commit: 9600f315f162b6cd86e2dbe2fffc793cc91c9319
workflow-type: tm+mt
source-wordcount: '1694'
ht-degree: 1%

---


# Entitäten (Profil-Zugriff)

Mit der Adobe Experience Platform können Sie über RESTful-APIs oder die Benutzeroberfläche auf Daten aus dem Echtzeit-Profil von Kunden zugreifen. In diesem Handbuch wird beschrieben, wie Sie mithilfe der API auf Entitäten zugreifen, die häufiger als &quot;Profil&quot;bezeichnet werden. Weitere Informationen zum Zugriff auf Profil-Daten über die Plattform-Benutzeroberfläche finden Sie im [Profil-Benutzerhandbuch](../ui/user-guide.md).

## Erste Schritte

Die in diesem Handbuch verwendeten API-Endpunkte sind Teil der Real-time Customer Profil API. Bevor Sie fortfahren, lesen Sie bitte das Entwicklerhandbuch [zur](getting-started.md)Echtzeit-Customer Profil API.

Insbesondere enthält der [Abschnitt](getting-started.md#getting-started) &quot;Erste Schritte&quot;des Profil-Entwicklerhandbuchs Links zu verwandten Themen, eine Anleitung zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtige Informationen zu erforderlichen Kopfzeilen, die für das erfolgreiche Aufrufen von Experience Platform-APIs benötigt werden.

## Zugriff auf Profil-Daten nach Identität

Sie können auf eine Entität eines Profils zugreifen, indem Sie eine GET-Anforderung an den `/access/entities` Endpunkt stellen und die Entität als eine Reihe von Abfragen-Parametern angeben. Diese ID besteht aus einem ID-Wert (`entityId`) und dem Identitäts-Namensraum (`entityIdNS`).

Die im Anforderungspfad bereitgestellten Abfragen geben an, auf welche Daten zugegriffen werden soll. Sie können mehrere Parameter einschließen, die durch ein kaufmännisches Und (&amp;) getrennt sind. Eine vollständige Liste der gültigen Parameter finden Sie im Abschnitt [Abfrage Parameter](#query-parameters) im Anhang.

**API-Format**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**Anfrage**

Die folgende Anforderung ruft die E-Mail-Adresse und den Namen eines Kunden mithilfe einer Identität ab:

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email&fields=identities,person.name,workEmail' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
>Wenn ein verwandtes Diagramm mehr als 50 Identitäten verknüpft, gibt dieser Dienst den HTTP-Status 422 und die Meldung &quot;Zu viele verwandte Identitäten&quot;zurück. Wenn Sie diese Fehlermeldung erhalten, sollten Sie weitere Abfragen hinzufügen, um die Suche einzuschränken.

## Zugriff auf Profil-Daten nach Liste von Identitäten

Sie können auf mehrere Profil-Entitäten über ihre Identitäten zugreifen, indem Sie eine POST-Anforderung an den `/access/entities` Endpunkt senden und die Identitäten in der Payload angeben. Diese Identitäten bestehen aus einem ID-Wert (`entityId`) und einem Identitäts-Namensraum (`entityIdNS`).

**API-Format**

```http
POST /access/entities
```

**Anfrage**

Mit der folgenden Anforderung werden die Namen und E-Mail-Adressen mehrerer Kunden anhand einer Liste von Identitäten abgerufen:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `fields` | Die XDM-Felder, die als Zeichenfolgen-Array zurückgegeben werden sollen. Standardmäßig werden alle Felder zurückgegeben. |
| `identities` | ***(Erforderlich)*** Ein Array mit einer Liste von Identitäten für die Entitäten, auf die Sie zugreifen möchten. |
| `identities.entityId` | Die ID einer Entität, auf die Sie zugreifen möchten. |
| `identities.entityIdNS.code` | Der Namensraum einer Entitäts-ID, auf die Sie zugreifen möchten. |
| `timeFilter.startTime` | Beginn des Zeitraumfilters, eingeschlossen. Muss eine Millisekunde-Granularität aufweisen. Die Standardeinstellung ist, falls nicht angegeben, der Beginn der verfügbaren Zeit. |
| `timeFilter.endTime` | Endzeit des Zeitraumfilters, ausgeschlossen. Muss eine Millisekunde-Granularität aufweisen. Wenn kein Wert angegeben ist, ist der Standardwert das Ende der verfügbaren Zeit. |
| `limit` | Anzahl der zurückzugebenden Datensätze. Gilt nur für die Anzahl der zurückgegebenen Erlebnis-Ereignis. Standard: 1.000. |
| `orderby` | Die Sortierreihenfolge der abgerufenen Erlebnis-Ereignis nach Zeitstempel, wie `(+/-)timestamp` bei der Standardeinstellung geschrieben `+timestamp`. |
| `withCA` | Funktionsmarkierung zur Aktivierung berechneter Attribute für die Suche. Standard: false. |

**Antwort** Eine erfolgreiche Antwort gibt die angeforderten Felder von Entitäten zurück, die im Anforderungstext angegeben sind.

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

## Zugriff auf Zeitreihen-Ereignis für ein Profil nach Identität

Sie können auf Zeitreihen-Ereignis über die Identität der zugehörigen Profil-Entität zugreifen, indem Sie eine GET-Anforderung an den `/access/entities` Endpunkt senden. Diese ID besteht aus einem ID-Wert (`entityId`) und einem Identitäts-Namensraum (`entityIdNS`).

Die im Anforderungspfad bereitgestellten Abfragen geben an, auf welche Daten zugegriffen werden soll. Sie können mehrere Parameter einschließen, die durch ein kaufmännisches Und (&amp;) getrennt sind. Eine vollständige Liste der gültigen Parameter finden Sie im Abschnitt [Abfrage Parameter](#query-parameters) im Anhang.

**API-Format**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**Anfrage**

Die folgende Anforderung findet eine Profil-Entität nach ID und ruft die Werte für die Eigenschaften `endUserIDs`, `web`und `channel` für alle Zeitreihen-Ereignis ab, die der Entität zugeordnet sind.

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine paginierte Liste von Ereignissen der Zeitreihen und zugehörigen Feldern zurück, die in den Anforderungsparametern für die Abfrage angegeben wurden.

>[!NOTE]
>In der Anforderung wurde eine Grenze von einem (`limit=1`) festgelegt, daher ist der Wert `count` in der Antwort unten 1 und es wird nur eine Entität zurückgegeben.

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

Die Ergebnisse werden beim Abrufen von Zeitreihen-Ereignissen paginiert. Wenn sich die Ergebnisse auf den folgenden Seiten befinden, enthält die `_page.next` Eigenschaft eine ID. Darüber hinaus stellt die `_links.next.href` Eigenschaft einen Anforderungs-URI zum Abrufen der nächsten Seite bereit. Um die Ergebnisse abzurufen, stellen Sie eine weitere GET-Anforderung an den `/access/entities` Endpunkt. Sie müssen jedoch sicherstellen, dass Sie `/entities` den Wert des angegebenen URI ersetzen.

>[!NOTE]
>Stellen Sie sicher, dass Sie `/entities/` im Anforderungspfad nicht versehentlich wiederholen. Es sollte nur einmal erscheinen wie: `/access/entities?start=...`

**API-Format**

```http
GET /access/{NEXT_URI}
```

| Parameter | Beschreibung |
|---|---|
| `{NEXT_URI}` | Der URI-Wert, aus dem `_links.next.href`er stammt. |

**Anfrage**

Die folgende Anforderung ruft die nächste Ergebnisseite ab, indem der `_links.next.href` URI als Anforderungspfad verwendet wird.

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die nächste Ergebnisseite zurück. Diese Antwort enthält keine nachfolgenden Ergebnisseiten, wie durch die leeren Zeichenfolgenwerte von `_page.next` und `_links.next.href`angegeben.

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

## Zugriff auf Zeitreihen-Ereignis für mehrere Profil nach Identitäten

Sie können auf Zeitreihen-Ereignis aus mehreren verknüpften Profilen zugreifen, indem Sie eine POST-Anforderung an den `/access/entities` Endpunkt senden und die Profil-ID in der Nutzlast angeben. Diese Identitäten bestehen jeweils aus einem ID-Wert (`entityId`) und einem Identitäts-Namensraum (`entityIdNS`).

**API-Format**

```http
POST /access/entities
```

**Anfrage**

Mit der folgenden Anforderung werden Benutzer-IDs, Ortszeiten und Ländercodes für Zeitreihenfolgen-Ereignis abgerufen, die mit einer Liste von Profil-IDs verknüpft sind:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `schema.name` | **(ERFORDERLICH)** Das XDM-Schema der Entität, die abgerufen werden soll |
| `relatedSchema.name` | Wenn `schema.name` dies `_xdm.context.experienceevent` ist, muss dieser Wert das Schema für die Profil-Entität angeben, mit dem die Zeitreihen-Ereignis verwandt sind. |
| `identities` | **(ERFORDERLICH)** Ein Array, das Profil auflistet, aus denen die Ereignis der zugehörigen Zeitreihen abgerufen werden sollen. Jeder Eintrag im Array ist auf eine der folgenden Weisen eingestellt: 1) Verwendung einer voll qualifizierten ID, bestehend aus ID-Wert und Namensraum, oder 2) Bereitstellung einer XID. |
| `fields` | Isoliert die Daten, die an einen bestimmten Feldsatz zurückgegeben werden. Mit diesem Filter können Sie filtern, welche Schema-Felder in den abgerufenen Daten enthalten sind. Beispiel: personalEmail,person.name,person.gender |
| `mergePolicyId` | Identifiziert die Merge Policy, mit der die zurückgegebenen Daten gesteuert werden. Wenn im Dienstaufruf keiner angegeben ist, wird die Standardeinstellung Ihres Unternehmens für dieses Schema verwendet. Wenn keine Merge Policy-Standardeinstellung konfiguriert wurde, ist die Standardeinstellung keine Profil-Zusammenführung und keine Identitätszuordnung. |
| `orderby` | Die Sortierreihenfolge der abgerufenen Erlebnis-Ereignis nach Zeitstempel, wie `(+/-)timestamp` bei der Standardeinstellung geschrieben `+timestamp`. |
| `timeFilter.startTime` | Geben Sie die Beginn-Zeit an, um Zeitreihenobjekte zu filtern (in Millisekunden). |
| `timeFilter.endTime` | Geben Sie die Endzeit zum Filtern von Zeitreihenobjekten an (in Millisekunden). |
| `limit` | Numerischer Wert, der die maximale Anzahl der zurückzugebenden Objekte angibt. Standard: 1000 |
| `withCA` | Funktionsmarkierung zur Aktivierung berechneter Attribute für die Suche. Standard: false |

**Antwort**

Eine erfolgreiche Antwort gibt eine paginierte Liste von Zeitreihen-Ereignissen zurück, die mit den in der Anforderung angegebenen mehreren Profilen verknüpft sind.

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

In dieser Beispielantwort liefert das erste aufgelistete Profil (&quot;GkouAW-yD9aoRCPhRYROJ-TetAFW&quot;) einen Wert für `_links.next.payload`, d. h. es gibt zusätzliche Ergebnisseiten für dieses Profil. Weitere Informationen zum Zugriff auf diese zusätzlichen Ergebnisse finden Sie im folgenden Abschnitt zum [Zugriff auf zusätzliche Ergebnisse](#access-additional-results) .

### Zusätzliche Ergebnisse {#access-additional-results}

Beim Abrufen von Zeitreihen-Ereignissen werden möglicherweise viele Ergebnisse zurückgegeben, daher werden die Ergebnisse häufig paginiert. Wenn für ein bestimmtes Profil nachfolgende Ergebnisseiten vorhanden sind, enthält der `_links.next.payload` Wert für dieses Profil ein Nutzdatenobjekt.

Mithilfe dieser Nutzlast im Anforderungstext können Sie eine zusätzliche POST-Anforderung an den `access/entities` Endpunkt ausführen, um die nachfolgende Seite der Zeitreihendaten für dieses Profil abzurufen.

## Zugriff auf Zeitreihen-Ereignis in mehreren Schemas

Sie können auf mehrere Entitäten zugreifen, die über einen Beziehungsdeskriptor verbunden sind. Der folgende Beispiel-API-Aufruf geht davon aus, dass zwischen zwei Schemas bereits eine Beziehung definiert wurde. Weitere Informationen zu Beziehungsdeskriptoren finden Sie im [Unterhandbuch](../../xdm/api/descriptors.md)zur Schema Registry API-Entwicklerhandbuch.

Sie können Parameter für die Abfrage in den Anforderungspfad einbeziehen, um anzugeben, auf welche Daten zugegriffen werden soll. Sie können mehrere Parameter einschließen, die durch ein kaufmännisches Und (&amp;) getrennt sind. Eine vollständige Liste der gültigen Parameter finden Sie im Abschnitt [Abfrage Parameter](#query-parameters) im Anhang.

**API-Format**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**Anfrage**

Mit der folgenden Anforderung wird eine Entität abgerufen, die einen zuvor eingerichteten Beziehungsdeskriptor enthält, um auf Informationen über verschiedene Schema hinweg zuzugreifen.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/access/entities?relatedSchema.name=_xdm.context.profile&schema.name=_xdm.context.experienceevent&relatedEntityId=GkouAW-2Xkftzer3bBtHiW8GkaFL \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Antwort**

Eine erfolgreiche Antwort gibt eine paginierte Liste von Zeitreihen-Ereignissen zurück, die mit mehreren Entitäten verknüpft sind.

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

Die Ergebnisse werden beim Abrufen von Zeitreihen-Ereignissen paginiert. Wenn sich die Ergebnisse auf den folgenden Seiten befinden, enthält die `_page.next` Eigenschaft eine ID. Darüber hinaus stellt die `_links.next.href` Eigenschaft eine Anforderungs-URI zum Abrufen der folgenden Seite bereit, indem zusätzliche GET-Anforderungen an den `access/entities` Endpunkt gesendet werden.

## Nächste Schritte

In diesem Handbuch haben Sie erfolgreich auf die Datenfelder, Profil und Zeitreihendaten zum Echtzeit-Profil von Kunden zugegriffen. Informationen zum Zugriff auf andere in der Plattform gespeicherte Datenressourcen finden Sie in der Übersicht über den [Datenzugriff](../../data-access/home.md).

## Anhang {#appendix}

Im folgenden Abschnitt finden Sie zusätzliche Informationen zum Zugriff auf Profil-Daten mithilfe der API.

### Abfrage {#query-parameters}

Die folgenden Parameter werden im Pfad für GET-Anforderungen an den `/access/entities` Endpunkt verwendet. Sie dienen dazu, die Profil-Entität zu identifizieren, auf die Sie zugreifen möchten, und die in der Antwort zurückgegebenen Daten zu filtern. Erforderliche Parameter sind beschriftet, während der Rest optional ist.

| Parameter | Beschreibung | Beispiel |
|---|---|---|
| `schema.name` | **(ERFORDERLICH)** Das XDM-Schema der Entität, die abgerufen werden soll | `schema.name=_xdm.context.experienceevent` |
| `relatedSchema.name` | Wenn `schema.name` der Wert &quot;_xdm.context.experience&quot; lautet, muss dieser Wert das Schema für die Profil-Entität angeben, mit dem die Zeitreihen-Ereignis verknüpft sind. | `relatedSchema.name=_xdm.context.profile` |
| `entityId` | **(ERFORDERLICH)** Die ID der Entität. Wenn der Wert dieses Parameters keine XID ist, muss auch ein Identitäts-Namensraum-Parameter angegeben werden (siehe `entityIdNS` unten). | `entityId=janedoe@example.com` |
| `entityIdNS` | Wenn `entityId` keine XID angegeben wird, muss dieses Feld den Identitäts-Namensraum angeben. | `entityIdNE=email` |
| `relatedEntityId` | Wenn `schema.name` der Wert &quot;_xdm.context.experience&quot; lautet, muss dieser Wert den Identitäts-Namensraum der verwandten Profil-Entität angeben. Dieser Wert folgt denselben Regeln wie `entityId`. | `relatedEntityId=69935279872410346619186588147492736556` |
| `relatedEntityIdNS` | Wenn `schema.name` der Wert &quot;_xdm.context.experience&quot; lautet, muss dieser Wert den Identitäts-Namensraum für die in `relatedEntityId`angegebene Entität angeben. | `relatedEntityIdNS=CRMID` |
| `fields` | Filter der in der Antwort zurückgegebenen Daten. Geben Sie hier an, welche Schema-Feldwerte in die abgerufenen Daten einbezogen werden sollen. Trennen Sie bei mehreren Feldern die Werte durch ein Komma ohne Leerzeichen zwischen | `fields=personalEmail,person.name,person.gender` |
| `mergePolicyId` | Identifiziert die Merge Policy, mit der die zurückgegebenen Daten gesteuert werden. Wenn im Aufruf keine Angabe gemacht wird, wird die Standardeinstellung Ihres Unternehmens für dieses Schema verwendet. Wenn keine Merge Policy-Standardeinstellung konfiguriert wurde, ist die Standardeinstellung keine Profil-Zusammenführung und keine Identitätszuordnung. | `mergePoilcyId=5aa6885fcf70a301dabdfa4a` |
| `orderBy` | Die Sortierreihenfolge der abgerufenen Erlebnis-Ereignis nach Zeitstempel, wie `(+/-)timestamp` bei der Standardeinstellung geschrieben `+timestamp`. | `orderby=-timestamp` |
| `startTime` | Geben Sie die Beginn-Zeit an, um Zeitreihenobjekte zu filtern (in Millisekunden). | `startTime=1539838505` |
| `endTime` | Geben Sie die Endzeit zum Filtern von Zeitreihenobjekten an (in Millisekunden). | `endTime=1539838510` |
| `limit` | Numerischer Wert, der die maximale Anzahl der zurückzugebenden Objekte angibt. Standard: 1000 | `limit=100` |
| `withCA` | Funktionsmarkierung zur Aktivierung berechneter Attribute für die Suche. Standard: false | `withCA=true` |