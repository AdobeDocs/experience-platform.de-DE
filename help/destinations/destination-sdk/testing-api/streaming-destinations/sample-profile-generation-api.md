---
description: Erfahren Sie, wie Sie mit der Zieltest-API Beispielprofile für Ihr Streaming-Ziel generieren können, die Sie für Zieltests verwenden können.
title: Generieren von Beispielprofilen basierend auf einem Quellschema
exl-id: 5f1cd00a-8eee-4454-bcae-07b05afa54af
source-git-commit: c1ba465a8a866bd8bdc9a2b294ec5d894db81e11
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 86%

---


# Generieren von Beispielprofilen basierend auf einem Quellschema {#sample-profile-api-operations}

>[!IMPORTANT]
>
>**API-Endpunkt**: `https://platform.adobe.io/data/core/activation/authoring/sample-profiles`

Auf dieser Seite werden alle API-Vorgänge aufgelistet und beschrieben, die Sie mit dem API-Endpunkt `/authoring/sample-profiles` ausführen können.

## Generieren verschiedener Profiltypen für verschiedene APIs {#different-profiles-different-apis}

>[!IMPORTANT]
>
>Verwenden Sie diesen API-Endpunkt, um Beispielprofile für zwei verschiedene Anwendungsfälle zu generieren. Sie haben die Möglichkeit zum:
>* Generieren von Profilen, die beim [Erstellen und Testen einer Nachrichtenumwandlungsvorlage](create-template.md) verwendet werden – durch Verwendung der *Ziel-ID* als Abfrageparameter.
>* Generieren von Profilen, die bei Aufrufen zum [Testen, ob Ihr Ziel richtig konfiguriert ist](streaming-destination-testing-overview.md) verwendet werden – durch Verwendung der *Zielinstanz-ID* als Abfrageparameter.

Sie können Beispielprofile basierend entweder auf dem Adobe-XDM-Quellschema (das beim Testen Ihres Ziels verwendet werden soll) oder dem von Ihrem Ziel unterstützten Zielschema (das beim Erstellen Ihrer Vorlage verwendet werden soll) generieren. Um den Unterschied zwischen dem Adobe-XDM-Quellschema und dem Zielschema zu verstehen, lesen Sie den Übersichtsabschnitt des Artikels [Nachrichtenformat](../../functionality/destination-server/message-format.md).

Beachten Sie, dass die Zwecke, für die die Beispielprofile verwendet werden können, nicht austauschbar sind. Profile, die auf der Grundlage der *Ziel-ID* generiert wurden, können nur verwendet werden, um Vorlagen für die Nachrichtenumwandlung zu erstellen, und Profile, die auf der Grundlage der *Zielinstanz-ID* generiert wurden, können nur zum Testen Ihres Ziel-Endpunkts verwendet werden.

## Erste Schritte mit API-Vorgängen zur Beispielprofilerstellung {#get-started}

Bevor Sie fortfahren, lesen Sie [Erste Schritte](../../getting-started.md). Dort finden Sie die nötigen Informationen für den erfolgreichen Aufruf der API, einschließlich Details für den Abruf der erforderlichen Authoring-Berechtigung für Ziele und zu den erforderlichen Kopfzeilen.

## Generieren von Beispielprofilen basierend auf dem Quellschema, das beim Testen Ihres Ziels verwendet werden soll {#generate-sample-profiles-source-schema}

>[!IMPORTANT]
>
>Fügen Sie die hier generierten Beispielprofile zu HTTP-Aufrufen hinzu, wenn Sie [Ihr Ziel testen](streaming-destination-testing-overview.md).

Sie können Beispielprofile basierend auf dem Quellschema generieren, indem Sie eine GET-Anfrage an den `authoring/sample-profiles/`-Endpunkt stellen und die ID einer Zielinstanz angeben, die Sie basierend auf der Zielkonfiguration erstellt haben, die Sie testen möchten.

Um die ID einer Zielinstanz abzurufen, müssen Sie zunächst in der Experience Platform-Benutzeroberfläche eine Verbindung zu Ihrem Ziel erstellen, bevor Sie versuchen, Ihr Ziel zu testen. Lesen Sie das [Tutorial zum Aktivieren von Zielen](../../../ui/activation-overview.md) und sehen Sie sich den unten stehenden Tipp an, wie Sie die Kennung der Zielinstanz abrufen können, die für diese API verwendet werden soll.

>[!IMPORTANT]
>
>* Um diese API verwenden zu können, müssen Sie über eine bestehende Verbindung zu Ihrem Ziel in der Experience Platform-Benutzeroberfläche verfügen. Lesen [Verbindung zum Ziel herstellen](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=de) und [Profile und Audiences für ein Ziel aktivieren](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=de) für weitere Informationen.
> * Nachdem Sie die Verbindung zu Ihrem Ziel hergestellt haben, rufen Sie die ID der Zielinstanz ab, die Sie in API-Aufrufen an diesen Endpunkt verwenden sollten, wenn Sie [eine Verbindung mit Ihrem Ziel durchsuchen](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/destination-details-page.html?lang=de).
>![UI-Bild, wie Sie die Ziel-Instanz-ID abrufen](../../assets/testing-api/get-destination-instance-id.png)

**API-Format**

```http
GET authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={COUNT}
```

| Abfrageparameter | Beschreibung |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | Die ID der Zielinstanz, auf deren Basis Sie Beispielprofile generieren. |
| `{COUNT}` | *Optional*. Die Anzahl der Beispielprofile, die Sie generieren. Der Parameter kann Werte von `1 - 1000` annehmen. <br> Wenn der Parameter „count“ nicht angegeben ist, wird die Standardanzahl der generierten Profile durch den Wert von `maxUsersPerRequest` in der [Ziel-Server-Konfiguration](../../authoring-api/destination-server/create-destination-server.md) bestimmt. Wenn diese Eigenschaft nicht definiert ist, generiert Adobe ein Beispielprofil. |

{style="table-layout:auto"}


**Anfrage**

Die folgende Anfrage generiert Beispielprofile, die von den Abfrageparametern`{DESTINATION_INSTANCE_ID}` und `{COUNT}` konfiguriert werden.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit der angegebenen Anzahl von Beispielprofilen mit Zielgruppenmitgliedschaft, Identitäten und Profilattributen zurück, die dem Quell-XDM-Schema entsprechen.

>[!TIP]
>
> Die Antwort gibt nur Zielgruppenzugehörigkeit, Identitäten und Profilattribute zurück, die in der Zielinstanz verwendet werden. Selbst wenn Ihr Quellschema andere Felder enthält, werden diese ignoriert.

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
| `segmentMembership` | Ein map -Objekt, das die Zielgruppenmitgliedschaften des Kontakts beschreibt. Weitere Informationen finden Sie unter `segmentMembership`, lesen [Details zur Zielgruppenmitgliedschaft](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html?lang=de). |
| `lastQualificationTime` | Ein Zeitstempel, der angibt, wann sich dieses Profil zuletzt für das Segment qualifiziert hat. |
| `xdm:status` | Ein Zeichenfolgenfeld, das anzeigt, ob die Zielgruppenzugehörigkeit im Rahmen der aktuellen Anfrage realisiert wurde. Folgende Werte werden akzeptiert: <ul><li>`realized`: Das Profil ist Teil des Segments.</li><li>`exited`: Das Profil beendet die Zielgruppe im Rahmen der aktuellen Anfrage.</li></ul> |
| `identityMap` | Ein Feld vom Typ „Zuordnung“, das die verschiedenen Identitätswerte einer Person zusammen mit den zugehörigen Namespaces beschreibt. Weitere Informationen zu `identityMap` finden Sie unter [Grundlage der Schemakomposition](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=de#identityMap). |

{style="table-layout:auto"}

## Generieren von Beispielprofilen basierend auf dem Zielschema, das bei der Erstellung einer Nachrichtenumwandlungsvorlage verwendet werden soll {#generate-sample-profiles-target-schema}

>[!IMPORTANT]
>
>Verwenden Sie die Beispielprofile, die hier beim Erstellen Ihrer Vorlage generiert werden, im [Schritt zum Rendern der Vorlage](render-template-api.md#multiple-profiles-with-body).

Sie können Beispielprofile generieren, die auf dem Zielschema basieren, indem Sie eine GET-Anfrage an den `authoring/sample-profiles/`-Endpunkt stellen und die Ziel-ID der Zielkonfiguration angeben, auf deren Basis Sie Ihre Vorlage erstellen.

>[!TIP]
>
>* Die Ziel-ID, die Sie hier verwenden sollten, ist die `instanceId`, die einer mithilfe des `/destinations`-Endpunkts erstellten Zielkonfiguration entspricht. Siehe [Abrufen einer Zielkonfiguration](../../authoring-api/destination-configuration/retrieve-destination-configuration.md) für weitere Details.

**API-Format**


```http
GET authoring/sample-profiles?destinationId={DESTINATION_ID}&count={COUNT}
```

| Abfrageparameter | Beschreibung |
| -------- | ----------- |
| `{DESTINATION_ID}` | Die ID der Zielkonfiguration, basierend auf der Sie Beispielprofile generieren. |
| `{COUNT}` | *Optional*. Die Anzahl der Beispielprofile, die Sie generieren. Der Parameter kann Werte von `1 - 1000` annehmen. <br> Wenn der Parameter „count“ nicht angegeben ist, wird die Standardanzahl der generierten Profile durch den Wert von `maxUsersPerRequest` in der [Ziel-Server-Konfiguration](../../authoring-api/destination-server/create-destination-server.md) bestimmt. Wenn diese Eigenschaft nicht definiert ist, generiert Adobe ein Beispielprofil. |

{style="table-layout:auto"}

**Anfrage**

Die folgende Anfrage generiert Beispielprofile, die von den Abfrageparametern`{DESTINATION_ID}` und `{COUNT}` konfiguriert werden.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit der angegebenen Anzahl von Beispielprofilen mit Zielgruppenmitgliedschaft, Identitäten und Profilattributen zurück, die dem Ziel-XDM-Schema entsprechen.

```json
[
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609326Z",
                    "status": "realized"
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
                    "status": "realized"
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
                    "status": "realized"
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

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status-Codes](../../../../landing/troubleshooting.md#api-status-codes) und [Fehler im Anfrage-Header](../../../../landing/troubleshooting.md#request-header-errors) in der Anleitung zur Fehlerbehebung für Platform.

## Nächste Schritte

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie Beispielprofile generieren, um eine [Nachrichtenumwandlungsvorlage](create-template.md) zu testen oder um zu [prüfen, ob Ihr Ziel richtig konfiguriert ist](streaming-destination-testing-overview.md).
