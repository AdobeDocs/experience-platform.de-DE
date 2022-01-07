---
description: Auf dieser Seite werden alle API-Vorgänge aufgelistet und beschrieben, die Sie mit dem API-Endpunkt "/authoring/sample-profiles"ausführen können, um Beispielprofile zu generieren, die für Zieltests verwendet werden können.
title: API-Vorgänge zur Profilerstellung
exl-id: 5f1cd00a-8eee-4454-bcae-07b05afa54af
source-git-commit: 6dd8a94e46b9bee6d1407e7ec945a722d8d7ecdb
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 3%

---

# API-Vorgänge zur Profilerstellung {#sample-profile-api-operations}

>[!IMPORTANT]
>
>**API-Endpunkt**: `https://platform.adobe.io/data/core/activation/authoring/sample-profiles`

Auf dieser Seite werden alle API-Vorgänge aufgelistet und beschrieben, die Sie mit dem `/authoring/sample-profiles` API-Endpunkt.

## Generieren verschiedener Profiltypen für verschiedene APIs {#different-profiles-different-apis}

>[!IMPORTANT]
>
>Verwenden Sie diesen API-Endpunkt, um Beispielprofile für zwei verschiedene Anwendungsfälle zu generieren. Wählen Sie eine der folgenden Möglichkeiten aus:
>* Generieren von Profilen, die verwendet werden, wenn [Erstellen und Testen einer Nachrichtenumwandlungsvorlage](./create-template.md) - durch Verwendung von *Ziel-ID* als Abfrageparameter.
>* Profile generieren, die bei Aufrufen an [Testen, ob Ihr Ziel richtig konfiguriert ist](./test-destination.md) - durch Verwendung von *Zielinstanz-ID* als Abfrageparameter.


Sie können Beispielprofile basierend entweder auf dem Adobe-XDM-Quellschema (das beim Testen Ihres Ziels verwendet werden soll) oder dem von Ihrem Ziel unterstützten Zielschema (das beim Erstellen Ihrer Vorlage verwendet werden soll) generieren. Um den Unterschied zwischen dem Adobe-XDM-Quellschema und dem Zielschema zu verstehen, lesen Sie den Übersichtsabschnitt des [Nachrichtenformat](./message-format.md) Artikel.

Beachten Sie, dass die Zwecke, für die die Beispielprofile verwendet werden können, nicht austauschbar sind. Auf der Basis der Variablen *Ziel-ID* kann nur verwendet werden, um Vorlagen für die Nachrichtenumwandlung und Profile zu erstellen, die basierend auf dem *Zielinstanz-ID* kann nur zum Testen Ihres Ziel-Endpunkts verwendet werden.

## Erste Schritte mit API-Vorgängen zur Beispielprofilerstellung {#get-started}

Bevor Sie fortfahren, lesen Sie bitte die [Erste Schritte](./getting-started.md) für wichtige Informationen, die Sie benötigen, um die API erfolgreich aufrufen zu können, einschließlich Informationen zum Abrufen der erforderlichen Authoring-Berechtigung für Ziele und der erforderlichen Kopfzeilen.

## Generieren von Beispielprofilen basierend auf dem Quellschema, das beim Testen Ihres Ziels verwendet werden soll {#generate-sample-profiles-source-schema}

>[!IMPORTANT]
>
>Fügen Sie die hier generierten Beispielprofile zu HTTP-Aufrufen hinzu, wenn [Testen des Ziels](./test-destination.md).

Sie können Beispielprofile basierend auf dem Quellschema generieren, indem Sie eine GET-Anfrage an die `authoring/sample-profiles/` -Endpunkt und die ID einer Zielinstanz angeben, die Sie basierend auf der Zielkonfiguration erstellt haben, die Sie testen möchten.

Um die ID einer Zielinstanz abzurufen, müssen Sie zunächst in der Experience Platform-Benutzeroberfläche eine Verbindung zu Ihrem Ziel erstellen, bevor Sie versuchen, Ihr Ziel zu testen. Lesen Sie die [Ziel-Tutorial aktivieren](/help/destinations/ui/activation-overview.md) und lesen Sie den unten stehenden Tipp, wie Sie die Kennung der Zielinstanz abrufen können, die für diese API verwendet werden soll.

>[!TIP]
>
>* Rufen Sie die Ziel-Instanz-ID ab, die Sie hier von der URL verwenden sollten, wenn Sie eine Verbindung mit Ihrem Ziel durchsuchen.
   >![UI-Bild, wie Sie die Ziel-Instanz-ID abrufen](./assets/get-destination-instance-id.png)


**API-Format**


```http
GET authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={COUNT}
```

| Abfrageparameter | Beschreibung |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | Die ID der Zielinstanz, basierend auf der Sie Beispielprofile generieren. |
| `{COUNT}` | *Optional*. Die Anzahl der Beispielprofile, die Sie generieren. Der Parameter kann Werte zwischen `1 - 1000`. <br> Wenn der Parameter count nicht angegeben ist, wird die Standardanzahl der generierten Profile durch die Variable `maxUsersPerRequest` Wert in [Zielserverkonfiguration](./destination-server-api.md#create). Wenn diese Eigenschaft nicht definiert ist, generiert Adobe ein Beispielprofil. |

{style=&quot;table-layout:auto&quot;}


**Anfrage**

Die folgende Anfrage generiert Beispielprofile, die von der `{DESTINATION_INSTANCE_ID}` und `{COUNT}` Abfrageparameter.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit der angegebenen Anzahl von Beispielprofilen mit Segmentmitgliedschaft, Identitäten und Profilattributen zurück, die dem Quell-XDM-Schema entsprechen.

>[!TIP]
>
> Die Antwort gibt nur Segmentzugehörigkeit, Identitäten und Profilattribute zurück, die in der Zielinstanz verwendet werden. Auch wenn Ihr Quellschema andere Felder enthält, werden diese ignoriert.

```json
[
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-7VEsJ"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-Y55JJ"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-Nd9GK"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    }
]
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `segmentMembership` | Ein map -Objekt, das die Segmentmitgliedschaften des Kontakts beschreibt. Weitere Informationen finden Sie unter `segmentMembership`, lesen [Details zur Segmentzugehörigkeit](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html). |
| `lastQualificationTime` | Ein Zeitstempel, der angibt, wann sich dieses Profil zuletzt für das Segment qualifiziert hat. |
| `xdm:status` | Gibt an, ob die Segmentzugehörigkeit im Rahmen der aktuellen Anforderung realisiert wurde. Folgende Werte werden akzeptiert: <ul><li>`existing`: Das Profil war bereits vor der Anfrage Teil des Segments und behält weiterhin seine Mitgliedschaft bei.</li><li>`realized`: Das Profil gibt das Segment als Teil der aktuellen Anforderung ein.</li><li>`exited`: Das Profil beendet das Segment als Teil der aktuellen Anforderung.</li></ul> |
| `identityMap` | Ein Feld vom Typ Zuordnung , das die verschiedenen Identitätswerte einer Person zusammen mit den zugehörigen Namespaces beschreibt. Weitere Informationen finden Sie unter `identityMap`, lesen [Grundlage der Schemakomposition](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en#identityMap). |

{style=&quot;table-layout:auto&quot;}

## Generieren von Beispielprofilen basierend auf dem Zielschema, das bei der Erstellung einer Nachrichtenumwandlungsvorlage verwendet werden soll {#generate-sample-profiles-target-schema}

>[!IMPORTANT]
>
>Verwenden Sie die Beispielprofile, die hier beim Erstellen Ihrer Vorlage generiert werden, im [Schritt zum Rendern der Vorlage](./render-template-api.md#multiple-profiles-with-body).

Sie können Beispielprofile generieren, die auf dem Zielschema basieren, das eine GET-Anfrage an die `authoring/sample-profiles/` -Endpunkt und die Ziel-ID der Zielkonfiguration angeben, basierend auf der Sie Ihre Vorlage erstellen.

>[!TIP]
>
>* Die Ziel-ID, die Sie hier verwenden sollten, ist die `instanceId` , die einer Zielkonfiguration entspricht, die mithilfe der `/destinations` -Endpunkt. Siehe Abschnitt [API-Referenz zur Zielkonfiguration](./destination-configuration-api.md#retrieve-list).


**API-Format**


```http
GET authoring/sample-profiles?destinationId={DESTINATION_ID}&count={COUNT}
```

| Abfrageparameter | Beschreibung |
| -------- | ----------- |
| `{DESTINATION_ID}` | Die ID der Zielkonfiguration, basierend auf der Sie Beispielprofile generieren. |
| `{COUNT}` | *Optional*. Die Anzahl der Beispielprofile, die Sie generieren. Der Parameter kann Werte zwischen `1 - 1000`. <br> Wenn der Parameter count nicht angegeben ist, wird die Standardanzahl der generierten Profile durch die Variable `maxUsersPerRequest` Wert in [Zielserverkonfiguration](./destination-server-api.md#create). Wenn diese Eigenschaft nicht definiert ist, generiert Adobe ein Beispielprofil. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Die folgende Anfrage generiert Beispielprofile, die von der `{DESTINATION_ID}` und `{COUNT}` Abfrageparameter.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit der angegebenen Anzahl von Beispielprofilen mit Segmentmitgliedschaft, Identitäten und Profilattributen zurück, die dem Ziel-XDM-Schema entsprechen.

```json
[
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609326Z",
                    "status": "existing"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609328Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609328Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-vizii"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-adKYs"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-t4sKv"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-C3enB"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-bfnbs"
                }
            ]
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609626Z",
                    "status": "existing"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609627Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609627Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-6YjGc"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-SfJ21"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-eQMWS"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-d3WzP"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-eWfFn"
                }
            ]
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609823Z",
                    "status": "existing"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609824Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609824Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-2PMjZ"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-3aLez"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-D2H1J"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-i6PsF"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-VPUtZ"
                }
            ]
        }
    }
]
```

## Umgang mit API-Fehlern {#api-error-handling}

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen der Experience Platform API-Fehlermeldung. Siehe [API-Statuscodes](../../landing/troubleshooting.md#api-status-codes) und [Fehler in der Anfragekopfzeile](../../landing/troubleshooting.md#request-header-errors) im Handbuch zur Fehlerbehebung bei Platform.

## Nächste Schritte

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie Beispielprofile generieren, die bei der [Testen einer Nachrichtenumwandlungsvorlage](./create-template.md) oder wenn [Testen, ob Ihr Ziel richtig konfiguriert ist](./test-destination.md).
