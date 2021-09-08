---
description: Auf dieser Seite werden alle API-Vorgänge aufgelistet und beschrieben, die Sie mit dem API-Endpunkt "/authoring/sample-profiles"ausführen können, um Beispielprofile zu generieren, die für Zieltests verwendet werden können.
title: API-Vorgänge zur Profilerstellung
source-git-commit: 19307fba8f722babe5b6d57e80735ffde00fc851
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 2%

---

# API-Vorgänge zur Profilerstellung {#sample-profile-api-operations}

>[!IMPORTANT]
>
>**API-Endpunkt**: `https://platform.adobe.io/data/core/activation/authoring/sample-profiles`

Auf dieser Seite werden alle API-Vorgänge aufgelistet und beschrieben, die Sie mit dem API-Endpunkt `/authoring/sample-profiles` ausführen können.

Mit diesem API-Endpunkt können Sie Beispielprofile zur Verwendung generieren:
* Beim Testen einer Nachrichtenumwandlungsvorlage. Weitere Informationen finden Sie unter [Erstellen und testen Sie eine Nachrichtenumwandlungsvorlage](./create-template.md).
* Beim Testen, ob Ihr Ziel richtig konfiguriert ist. Weitere Informationen finden Sie unter [Testen der Zielkonfiguration](./test-destination.md).

Sie können Beispielprofile auf Grundlage des Adobe-XDM-Quellschemas oder des von Ihrem Ziel unterstützten Zielschemas generieren. Um den Unterschied zwischen dem Adobe-XDM-Quellschema und dem Zielschema zu verstehen, lesen Sie den Artikel [Nachrichtenformat](./message-format.md) .

## Erste Schritte mit API-Vorgängen zur Beispielprofilerstellung {#get-started}

Bevor Sie fortfahren, lesen Sie zunächst das [Erste-Schritte-Handbuch](./getting-started.md) , um wichtige Informationen zu erhalten, die Sie benötigen, um die API erfolgreich aufrufen zu können. Dazu gehören das Abrufen der erforderlichen Zielerstellungsberechtigung und der erforderlichen Kopfzeilen.

## Generieren von Beispielprofilen basierend auf dem Quellschema {#generate-sample-profiles-source-schema}

Sie können Beispielprofile basierend auf dem Quellschema generieren, indem Sie eine GET-Anfrage an den Endpunkt `authoring/sample-profiles/` senden und die Kennung einer Zielinstanz angeben, die Sie basierend auf der Zielkonfiguration erstellt haben, die Sie testen möchten.

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
| `{COUNT}` | *Optional*. Die Anzahl der Beispielprofile, die Sie generieren. Der Parameter kann Werte zwischen `1 - 1000` annehmen. <br> Wenn der Parameter count nicht angegeben ist, wird die Standardanzahl der generierten Profile durch den  `maxUsersPerRequest` Wert in der  [Zielserverkonfiguration](./destination-server-api.md#create) bestimmt. Wenn diese Eigenschaft nicht definiert ist, generiert Adobe ein Beispielprofil. |


**Anfrage**

Die folgende Anfrage generiert Beispielprofile, die von den Abfrageparametern `{DESTINATION_INSTANCE_ID}` und `{COUNT}` konfiguriert werden.

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
| `segmentMembership` | Ein map -Objekt, das die Segmentmitgliedschaften des Kontakts beschreibt. Weitere Informationen zu `segmentMembership` finden Sie unter [Details zur Segmentmitgliedschaft](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html). |
| `lastQualificationTime` | Ein Zeitstempel, der angibt, wann sich dieses Profil zuletzt für das Segment qualifiziert hat. |
| `xdm:status` | Gibt an, ob die Segmentzugehörigkeit im Rahmen der aktuellen Anforderung realisiert wurde. Folgende Werte werden akzeptiert: <ul><li>`existing`: Das Profil war bereits vor der Anfrage Teil des Segments und behält weiterhin seine Mitgliedschaft bei.</li><li>`realized`: Das Profil gibt das Segment als Teil der aktuellen Anforderung ein.</li><li>`exited`: Das Profil beendet das Segment als Teil der aktuellen Anforderung.</li></ul> |
| `identityMap` | Ein Feld vom Typ Zuordnung , das die verschiedenen Identitätswerte einer Person zusammen mit den zugehörigen Namespaces beschreibt. Weitere Informationen zu `identityMap` finden Sie unter [Basis der Schemakomposition](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en#identityMap). |


## Erstellen von Beispielprofilen basierend auf dem Zielschema {#generate-sample-profiles-target-schema}

Sie können Beispielprofile generieren, die auf dem Zielschema basieren, das eine GET-Anfrage an den Endpunkt `authoring/sample-profiles/` sendet und die Ziel-ID der Zielkonfiguration angibt, basierend auf der Sie Ihre Vorlage erstellen.

>[!TIP]
>
>* Die Ziel-ID, die Sie hier verwenden sollten, ist die `instanceId` , die einer Zielkonfiguration entspricht, die mit dem Endpunkt `/destinations` erstellt wurde. Weitere Informationen finden Sie unter [API-Referenz zur Zielkonfiguration](./destination-configuration-api.md#retrieve-list).


**API-Format**


```http
GET authoring/sample-profiles?destinationId={DESTINATION_ID}&count={COUNT}
```

| Abfrageparameter | Beschreibung |
| -------- | ----------- |
| `{DESTINATION_ID}` | Die ID der Zielkonfiguration, basierend auf der Sie Beispielprofile generieren. |
| `{COUNT}` | *Optional*. Die Anzahl der Beispielprofile, die Sie generieren. Der Parameter kann Werte zwischen `1 - 1000` annehmen. <br> Wenn der Parameter count nicht angegeben ist, wird die Standardanzahl der generierten Profile durch den  `maxUsersPerRequest` Wert in der  [Zielserverkonfiguration](./destination-server-api.md#create) bestimmt. Wenn diese Eigenschaft nicht definiert ist, generiert Adobe ein Beispielprofil. |

**Anfrage**

Die folgende Anfrage generiert Beispielprofile, die von den Abfrageparametern `{DESTINATION_ID}` und `{COUNT}` konfiguriert werden.

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

Die Ziel-SDK-API-Endpunkte folgen den allgemeinen Grundsätzen der Experience Platform API-Fehlermeldung. Weitere Informationen finden Sie unter [API-Status-Codes](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) und [Fehler in der Anforderungsheader](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) im Handbuch zur Fehlerbehebung für Platform.

## Nächste Schritte

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie Beispielprofile generieren, die beim [Testen einer Nachrichtenumwandlungsvorlage](./create-template.md) oder beim [Testen verwendet werden, ob Ihr Ziel korrekt konfiguriert ist](./test-destination.md).