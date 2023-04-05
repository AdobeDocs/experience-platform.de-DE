---
description: Auf dieser Seite werden das Nachrichtenformat und die Profilumwandlung von aus Adobe Experience Platform in Ziele exportierten Daten behandelt.
title: Nachrichtenformat
exl-id: 1212c1d0-0ada-4ab8-be64-1c62a1158483
source-git-commit: 9aba3384b320b8c7d61a875ffd75217a5af04815
workflow-type: tm+mt
source-wordcount: '2267'
ht-degree: 4%

---

# Nachrichtenformat

## Voraussetzungen - Adobe Experience Platform-Konzepte {#prerequisites}

Um das Nachrichtenformat sowie den Profilkonfigurations- und -konvertierungsprozess auf der Adobe zu verstehen, machen Sie sich mit den folgenden Konzepten der Experience Platform vertraut:

* **Experience-Datenmodell (XDM)**. [XDM-Übersicht](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=de) und  [Erstellen eines XDM-Schemas in Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=de).
* **Klasse**. [Erstellen und Bearbeiten von Klassen in der Benutzeroberfläche](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/classes.html?lang=en).
* **IdentityMap**. Die Identitätszuordnung stellt eine Zuordnung aller Endbenutzeridentitäten in Adobe Experience Platform dar. Siehe `xdm:identityMap` im [Wörterbuch der XDM-Felder](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en).
* **SegmentMembership**. Die [segmentMembership](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en) Das XDM-Attribut informiert darüber, zu welchen Segmenten ein Profil gehört. Für die drei verschiedenen Werte im `status` -Feld, lesen Sie die Dokumentation unter [Feldergruppe Segmentzugehörigkeitsdetails](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html).

## Übersicht {#overview}

Verwenden Sie den Inhalt dieser Seite zusammen mit dem Rest der [Konfigurationsoptionen für Partnerziele](./configuration-options.md). Auf dieser Seite werden das Nachrichtenformat und die Profilumwandlung von aus Adobe Experience Platform in Ziele exportierten Daten behandelt. Die andere Seite behandelt Details zur Verbindung und Authentifizierung mit Ihrem Ziel.

Adobe Experience Platform exportiert Daten in eine beträchtliche Anzahl von Zielen in verschiedenen Datenformaten. Beispiele für Zieltypen sind Werbeplattformen (Google), soziale Netzwerke (Facebook) und Cloud-Speicher-Standorte (Amazon S3, Azure Event Hub).

Experience Platform kann das Nachrichtenformat der exportierten Profile so anpassen, dass es dem erwarteten Format auf Ihrer Seite entspricht. Um diese Anpassung zu verstehen, sind die folgenden Konzepte wichtig:
* Das XDM-Quellschema (1) und das Ziel-Schema (2) in Adobe Experience Platform
* Das erwartete Nachrichtenformat auf der Partnerseite (3) und
* Die Transformationsebene zwischen dem XDM-Schema und dem erwarteten Nachrichtenformat, die Sie definieren können, indem Sie eine [Nachrichtenumwandlungsvorlage](./message-format.md#using-templating).

![Umwandlung von Schemata in JSON](./assets/transformations-3-steps.png)

Experience Platform verwendet XDM-Schemas, um die Datenstruktur konsistent und wiederverwendbar zu beschreiben.

<!--

Users who want to activate data to your destination need to map the fields in their Experience Platform datasets to a schema that translates to your destination's expected format. Adobe will create a custom field group for your company to add to the target schema. The fields in the field group depend on the profile attribute fields that you can receive.

-->

**Quell-XDM-Schema (1)**: Dieses Element bezieht sich auf das Schema, das Kunden in Experience Platform verwenden. In Experience Platform im [Zuordnungsschritt](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en#mapping) des Workflows &quot;Ziel aktivieren&quot;können Kunden Felder aus ihrem XDM-Schema dem Zielschema Ihres Ziels zuordnen (2).

**Target-XDM-Schema (2)**: Basierend auf dem JSON-Standardschema (3) des erwarteten Formats Ihres Ziels und den Attributen, die Ihr Ziel interpretieren kann, können Sie Profilattribute und Identitäten in Ihrem Ziel-XDM-Schema definieren. Dies können Sie in der Zielkonfiguration im Abschnitt [schemaConfig](./destination-configuration.md#schema-configuration) und [identityNamespaces](./destination-configuration.md#identities-and-attributes) Objekte.

**JSON-Standardschema Ihrer Zielprofilattribute (3)**: Dieses Beispiel stellt eine [JSON-Schema](https://json-schema.org/learn/miscellaneous-examples.html) der von Ihrer Plattform unterstützten Profilattribute und der zugehörigen Typen (z. B.: -Objekt, -Zeichenfolge, -Array). Beispielfelder, die Ihr Ziel unterstützen könnte `firstName`, `lastName`, `gender`, `email`, `phone`, `productId`, `productName`usw. Sie benötigen eine [Nachrichtenumwandlungsvorlage](./message-format.md#using-templating) , um die aus der Experience Platform exportierten Daten an das gewünschte Format anzupassen.

Basierend auf den oben beschriebenen Schematransformationen wird hier gezeigt, wie sich eine Profilkonfiguration zwischen dem Quell-XDM-Schema und einem Beispielschema auf der Partnerseite ändert:

![Beispiel einer Umwandlungsmeldung](./assets/transformations-with-examples.png)

## Erste Schritte - Transformieren von drei grundlegenden Attributen {#getting-started}

Um den Prozess der Profilumwandlung zu demonstrieren, verwendet das folgende Beispiel drei gemeinsame Profilattribute in Adobe Experience Platform: **Vorname**, **Nachname** und **E-Mail-Adresse**.

>[!NOTE]
>
>Der Kunde ordnet die Attribute aus dem Quell-XDM-Schema dem Partner-XDM-Schema in der Adobe Experience Platform-Benutzeroberfläche in der **Zuordnung** Schritt [Zielarbeitsablauf aktivieren](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping).

Nehmen wir an, Ihre Plattform kann ein Nachrichtenformat wie:

```shell
POST https://YOUR_REST_API_URL/users/
Content-Type: application/json
Authorization: Bearer YOUR_REST_API_KEY

{
  "attributes":
    {
      "first_name": "Yours",
      "last_name": "Truly",
      "external_id": "yourstruly@adobe.com"
    }
}
```

In Bezug auf das Nachrichtenformat lauten die entsprechenden Umwandlungen wie folgt:

| Attribut im Partner-XDM-Schema auf der Adobe-Seite | Umwandlung | Attribut in HTTP-Nachricht auf Ihrer Seite |
|---------|----------|---------|
| `_your_custom_schema.firstName` | ` attributes.first_name` | `first_name` |
| `_your_custom_schema.lastName` | `attributes.last_name` | `last_name` |
| `personalEmail.address` | `attributes.external_id` | `external_id` |

{style="table-layout:auto"}

## Profilstruktur in Experience Platform {#profile-structure}

Um die unten aufgeführten Beispiele auf der Seite zu verstehen, müssen Sie die Profilstruktur in Experience Platform kennen.

Profile haben drei Bereiche:

* `segmentMembership` (immer in einem Profil vorhanden)
   * Dieser Abschnitt enthält alle Segmente, die im Profil vorhanden sind. Die Segmente können einen von zwei Status aufweisen: `realized` oder `exited`.
* `identityMap` (immer in einem Profil vorhanden)
   * Dieser Abschnitt enthält alle Identitäten, die im Profil vorhanden sind (E-Mail, Google GAID, Apple IDFA usw.) und die der Benutzer für den Export im Aktivierungs-Workflow zugeordnet hat.
* -Attribute (je nach Zielkonfiguration können diese im Profil vorhanden sein). Es gibt auch einen geringfügigen Unterschied zwischen vordefinierten Attributen und Freiformattributen:
   * für *Freiformattribute* enthalten, enthalten diese `.value` Pfad, wenn das Attribut im Profil vorhanden ist (siehe `lastName` -Attribut aus Beispiel 1). Wenn sie nicht im Profil vorhanden sind, enthalten sie nicht die `.value` path (siehe `firstName` -Attribut aus Beispiel 1).
   * für *vordefinierte Attribute* enthalten, enthalten diese keine `.value` Pfad. Alle zugeordneten Attribute, die in einem Profil vorhanden sind, werden in der Attributzuordnung angezeigt. Die nicht vorhandenen werden nicht vorhanden sein (siehe Beispiel 2 - `firstName` -Attribut nicht im Profil vorhanden ist).

Siehe zwei Beispiele für Profile in Experience Platform:

### Beispiel 1 mit `segmentMembership`, `identityMap` und -Attribute für Freiformattribute {#example-1}

```json
{
  "segmentMembership": {
    "ups": {
      "11111111-1111-1111-1111-111111111111": {
        "lastQualificationTime": "2019-04-15T02:41:50.000+0000",
        "status": "realized"
      }
    }
  },
  "identityMap": {
    "mobileIds": [
      {
        "id": "e86fb215-0921-4537-bc77-969ff775752c"
      }
    ]
  },
  "attributes": {
    "firstName": {
    },
    "lastName": {
      "value": "lastName"
    }
  }
}
```

### Beispiel 2 mit `segmentMembership`, `identityMap` und Attribute für vordefinierte Attribute {#example-2}

```json
{
  "segmentMembership": {
    "ups": {
      "11111111-1111-1111-1111-111111111111": {
        "lastQualificationTime": "2019-04-15T02:41:50.000+0000",
        "status": "realized"
      }
    }
  },
  "identityMap": {
    "mobileIds": [
      {
        "id": "e86fb215-0921-4537-bc77-969ff775752c"
      }
    ]
  },
  "attributes": {
    "lastName": "lastName"
  }
}
```

## Verwenden einer Vorlagensprache für die Transformationen von Identitäten, Attributen und Segmentzugehörigkeiten {#using-templating}

Verwendung von Adoben [Kiesvorlagen](https://pebbletemplates.io/), eine Vorlagensprache, die der [Jinja](https://jinja.palletsprojects.com/en/2.11.x/), um die Felder aus dem Experience Platform-XDM-Schema in ein von Ihrem Ziel unterstütztes Format umzuwandeln.

In diesem Abschnitt finden Sie mehrere Beispiele dafür, wie diese Umwandlungen vorgenommen werden - vom Eingabe-XDM-Schema über die Vorlage und die Ausgabe in Payload-Formaten, die von Ihrem Ziel akzeptiert werden. Die folgenden Beispiele werden durch zunehmende Komplexität dargestellt:

1. Einfache Transformationsbeispiele. Erfahren Sie, wie die Vorlage mit einfachen Umwandlungen für [Profilattribute](./message-format.md#attributes), [Segmentmitgliedschaft](./message-format.md#segment-membership)und [Identität](./message-format.md#identities) -Felder.
2. Beispiele für komplexere Vorlagen, die die oben genannten Felder kombinieren: [Erstellen einer Vorlage, die Segmente und Identitäten sendet](./message-format.md#segments-and-identities) und [Erstellen einer Vorlage zum Senden von Segmenten, Identitäten und Profilattributen](./message-format.md#segments-identities-attributes).
3. Vorlagen, die den Aggregationsschlüssel enthalten. Wenn Sie [konfigurierbare Aggregation](./destination-configuration.md#configurable-aggregation) in der Zielkonfiguration gruppiert Experience Platform die in Ihr Ziel exportierten Profile anhand von Kriterien wie Segment-ID, Segmentstatus oder Identitäts-Namespaces.

### Profilattribute {#attributes}

Informationen zum Transformieren der in Ihr Ziel exportierten Profilattribute finden Sie in den JSON- und Codebeispielen unten.

>[!IMPORTANT]
>
>Eine Liste aller in Adobe Experience Platform verfügbaren Profilattribute finden Sie im Abschnitt [Wörterbuch der XDM-Felder](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en).


**Eingabe**

Profil 1:

```json
{
    "attributes": {
        "firstName": {
            "value": "Hermione"
    },
    "birthDate": {}
  }
}
```

Profil 2:

```json
{
  "attributes": {
    "firstName": {
      "value": "Harry"
    },
    "birthDate": {
        "value": "1980/07/31"
    }
  }
}
```

**Vorlage**

>[!IMPORTANT]
>
>Bei allen Vorlagen, die Sie verwenden, müssen Sie die unzulässigen Zeichen, z. B. doppelte Anführungszeichen, maskieren `""` vor dem Einfügen der Vorlage in die [Zielserverkonfiguration](./server-and-template-configuration.md#template-specs). Weitere Informationen zum Escapen von doppelten Anführungszeichen finden Sie in Kapitel 9 im Abschnitt [JSON-Standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            {% for attribute in profile.attributes %}
            "{{ attribute.key }}":
                {% if attribute.value is empty %}
                    null
                {% else %}
                    "{{ attribute.value.value }}"
                {% endif %}
            {% if not loop.last %},{% endif %}
            {% endfor %}
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**Ergebnis**


```json
{
    "profiles": [
        {
            "firstName": "Hermione",
            "birthDate": null
        },
        {
            "firstName": "Harry",
            "birthDate": "1980/07/31"
        }
    ]
}
```

### Segmentzugehörigkeit {#segment-membership}

Die [segmentMembership](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en) Das XDM-Attribut informiert darüber, zu welchen Segmenten ein Profil gehört.
Für die drei verschiedenen Werte im `status` -Feld, lesen Sie die Dokumentation unter [Feldergruppe Segmentzugehörigkeitsdetails](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html).

**Eingabe**

Profil 1:

```json
{
  "segmentMembership": {
    "ups": {
      "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "788d8874-8007-4253-92b7-ee6b6c20c6f3": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "realized"
      },
      "8f812592-3f06-416b-bd50-e7831848a31a": {
        "lastQualificationTime": "2019-11-20T13:15:49Z",
        "status": "exited"
      }
    }
  }
}
```

Profil 2:

```json
{
  "segmentMembership": {
    "ups": {
      "32396e4b-16f6-4033-9702-fc69b5e24e7c": {
        "lastQualificationTime": "2021-08-20T17:23:04Z",
        "status": "realized"
      },
      "af854278-894a-4192-a96b-320fbf2623fd": {
        "lastQualificationTime": "2021-08-20T16:44:37Z",
        "status": "realized"
      },
      "66505bf9-bc08-4bac-afbc-8b6706650ea4": {
        "lastQualificationTime": "2019-08-20T17:23:04Z",
        "status": "realized"
      }
    }
  }
}
```

**Vorlage**


>[!IMPORTANT]
>
>Bei allen Vorlagen, die Sie verwenden, müssen Sie die unzulässigen Zeichen, z. B. doppelte Anführungszeichen, maskieren `""` vor dem Einfügen der Vorlage in die [Zielserverkonfiguration](./server-and-template-configuration.md#template-specs). Weitere Informationen zum Escapen von doppelten Anführungszeichen finden Sie in Kapitel 9 im Abschnitt [JSON-Standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "AdobeExperiencePlatformSegments": {
                "add": [
                {% for segment in profile.segmentMembership.ups | added %}
                "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ],
                "remove": [
                {# Alternative syntax for filtering segments by status: #}
                {% for segment in removedSegments(profile.segmentMembership.ups) %}
                "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ]
            }
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**Ergebnis**

```json
{
    "profiles": [
        {
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075",
                    "788d8874-8007-4253-92b7-ee6b6c20c6f3"
                ],
                "remove": [
                    "8f812592-3f06-416b-bd50-e7831848a31a"
                ]
            }
        },
        {
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "32396e4b-16f6-4033-9702-fc69b5e24e7c",
                    "af854278-894a-4192-a96b-320fbf2623fd",
                    "66505bf9-bc08-4bac-afbc-8b6706650ea4"
                ],
                "remove": [
                ]
            }
        }
    ]
}
```

### Identitäten {#identities}

Weitere Informationen zu Identitäten in Experience Platform finden Sie unter [Übersicht über Identitäts-Namespaces](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=de).

**Eingabe**

Profil 1:

```json
{
    "identityMap": {
        "email": [
            {
                "id": "johndoe@example.com"
            },
            {
                "id": "jd@example.com"
            }
        ],
        "external_id": [
            {
                "id": "123456"
            }
        ]
    }
}
```

Profil 2:

```json
{
    "identityMap": {
        "email": [
            {
                "id": "jane.doe@example.com"
            }
        ]
    }
}
```

**Vorlage**


>[!IMPORTANT]
>
>Bei allen Vorlagen, die Sie verwenden, müssen Sie die unzulässigen Zeichen, z. B. doppelte Anführungszeichen, maskieren `""` vor dem Einfügen der Vorlage in die [Zielserverkonfiguration](./server-and-template-configuration.md#template-specs). Weitere Informationen zum Escapen von doppelten Anführungszeichen finden Sie in Kapitel 9 im Abschnitt [JSON-Standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "identities": [
                {% for email in profile.identityMap.email %}
                {
                    "type": "email",
                    "id": "{{ email.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}

                {# Add a comma only if you have both emails and external_ids. #}
                {% if profile.identityMap.email is not empty and profile.identityMap.external_id is not empty %}
                    ,
                {% endif %}

                {% for external in profile.identityMap.external_id %}
                {
                    "type": "external_id",
                    "id": "{{ external.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
            ]
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**Ergebnis**

```json
{
    "profiles": [
        {
            "identities": [
                {
                    "type": "email",
                    "id": "johndoe@example.com"
                },
                {
                    "type": "email",
                    "id": "jd@example.com"
                },
                {
                    "type": "external_id",
                    "id": "123456"
                }
            ]
        },
        {
            "identities": [
                {
                    "type": "email",
                    "id": "jane.doe@example.com"
                }
            ]
        }
    ]
}
```

### Erstellen einer Vorlage, die Segmente und Identitäten sendet {#segments-and-identities}

In diesem Abschnitt finden Sie ein Beispiel für eine häufig verwendete Transformation zwischen dem Adobe-XDM-Schema und dem Partnerzielschema.
Im folgenden Beispiel erfahren Sie, wie Sie die Segmentzugehörigkeit und das Identitätsformat transformieren und an Ihr Ziel ausgeben.

**Eingabe**

Profil 1:

```json
{
    "identityMap": {
        "email": [
            {
                "id": "johndoe@example.com"
            },
            {
                "id": "jd@example.com"
            }
        ],
        "external_id": [
            {
                "id": "123456"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "realized"
            },
            "788d8874-8007-4253-92b7-ee6b6c20c6f3": {
              "lastQualificationTime": "2019-11-20T13:15:49Z",
              "status": "realized"
            },
            "8f812592-3f06-416b-bd50-e7831848a31a": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "exited"
            }
        }
    }
}
```

Profil 2:

```json
{
    "identityMap": {
        "email": [
            {
                "id": "jane.doe@example.com"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2021-08-31T10:01:42Z",
                "status": "realized"
            }
        }
    }
}
```

**Vorlage**

>[!IMPORTANT]
>
>Bei allen Vorlagen, die Sie verwenden, müssen Sie die unzulässigen Zeichen, z. B. doppelte Anführungszeichen, maskieren `""` vor dem Einfügen der Vorlage in die [Zielserverkonfiguration](./server-and-template-configuration.md#template-specs). Weitere Informationen zum Escapen von doppelten Anführungszeichen finden Sie in Kapitel 9 im Abschnitt [JSON-Standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "identities": [
                {% for email in profile.identityMap.email %}
                {
                    "type": "email",
                    "id": "{{ email.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
                
                {# Add a comma only if you have both emails and external_ids. #}
                {% if profile.identityMap.email is not empty and profile.identityMap.external_id is not empty %}
                    ,
                {% endif %}
                
                {% for external in profile.identityMap.external_id %}
                {
                    "type": "external_id",
                    "id": "{{ external.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    {% for segment in profile.segmentMembership.ups | added %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                    {% endfor %}
                ],
                "remove": [
                    {# Alternative syntax for filtering segments by status: #}
                    {% for segment in removedSegments(profile.segmentMembership.ups) %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                    {% endfor %}
                ]
            }
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**Ergebnis**

Die `json` unten zeigt die aus Adobe Experience Platform exportierten Daten.

```json
{
    "profiles": [
        {
            "identities": [
                {
                    "type": "email",
                    "id": "johndoe@example.com"
                },
                {
                    "type": "email",
                    "id": "jd@example.com"
                },
                {
                    "type": "external_id",
                    "id": "123456"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075",
                    "788d8874-8007-4253-92b7-ee6b6c20c6f3"
                ],
                "remove": [
                    "8f812592-3f06-416b-bd50-e7831848a31a"
                ]
            }
        },
        {
            "identities": [
                {
                    "type": "email",
                    "id": "jane.doe@example.com"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075"
                ],
                "remove": []
            }
        }
    ]
}
```

### Erstellen einer Vorlage zum Senden von Segmenten, Identitäten und Profilattributen {#segments-identities-attributes}

In diesem Abschnitt finden Sie ein Beispiel für eine häufig verwendete Transformation zwischen dem Adobe-XDM-Schema und dem Partnerzielschema.

Ein weiteres gängiges Anwendungsbeispiel ist der Export von Daten, die Segmentzugehörigkeiten und Identitäten enthalten (z. B.: E-Mail-Adresse, Telefonnummer, Werbe-ID) und Profilattribute. Um Daten auf diese Weise zu exportieren, sehen Sie sich das folgende Beispiel an:

**Eingabe**

Profil 1:

```json
{
    "attributes": {
        "firstName": {
            "value": "Hermione"
        },
        "birthDate": {}
    },
    "identityMap": {
        "email": [
            {
                "id": "johndoe@example.com"
            },
            {
                "id": "jd@example.com"
            }
        ],
        "external_id": [
            {
                "id": "123456"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "realized"
            },
            "788d8874-8007-4253-92b7-ee6b6c20c6f3": {
              "lastQualificationTime": "2019-11-20T13:15:49Z",
              "status": "realized"
            },
            "8f812592-3f06-416b-bd50-e7831848a31a": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "exited"
            }
        }
    }
}
```

Profil 2:

```json
{
    "attributes": {
        "firstName": {
            "value": "Harry"
        },
        "birthDate": {
            "value": "1980/07/31"
        }
    },
    "identityMap": {
        "email": [
            {
                "id": "harry.p@example.com"
            }
        ]
    },
    "segmentMembership": {
        "ups": {
            "36a51c13-9dd6-4d2c-8aa3-07d785ea5075": {
                "lastQualificationTime": "2019-11-20T13:15:49Z",
                "status": "realized"
            }
        }
    }
}
```

**Vorlage**

>[!IMPORTANT]
>
>Bei allen Vorlagen, die Sie verwenden, müssen Sie die unzulässigen Zeichen, z. B. doppelte Anführungszeichen, maskieren `""` vor dem Einfügen der Vorlage in die [Zielserverkonfiguration](./server-and-template-configuration.md#template-specs). Weitere Informationen zum Escapen von doppelten Anführungszeichen finden Sie in Kapitel 9 im Abschnitt [JSON-Standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

```python
{
    "profiles": [
        {% for profile in input.profiles %}
        {
            "attributes": {
            {% for attribute in profile.attributes %}
                "{{ attribute.key }}":
                    {% if attribute.value is empty %}
                        null
                    {% else %}
                        "{{ attribute.value.value }}"
                    {% endif %}
                {% if not loop.last %},{% endif %}
            {% endfor %}
            },
            "identities": [
                {% for email in profile.identityMap.email %}
                {
                    "type": "email",
                    "id": "{{ email.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}

                {# Add a comma only if we have both emails and external_ids. #}
                {% if profile.identityMap.email is not empty and profile.identityMap.external_id is not empty %}
                    ,
                {% endif %}

                {% for external in profile.identityMap.external_id %}
                {
                    "type": "external_id",
                    "id": "{{ external.id }}"
                }{% if not loop.last %},{% endif %}
                {% endfor %}
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                {% for segment in profile.segmentMembership.ups | added %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ],
                "remove": [
                {# Alternative syntax for filtering segments by status: #}
                {% for segment in removedSegments(profile.segmentMembership.ups) %}
                    "{{ segment.key }}"{% if not loop.last %},{% endif %}
                {% endfor %}
                ]
            }
        }
    ]
}
```

**Ergebnis**

Die `json` unten zeigt die aus Adobe Experience Platform exportierten Daten.

```json
{
    "profiles": [
        {
            "attributes": {
                "firstName": "Hermione",
                "birthDate": null
            },
            "identities": [
                {
                    "type": "email",
                    "id": "johndoe@example.com"
                },
                {
                    "type": "email",
                    "id": "jd@example.com"
                },
                {
                    "type": "external_id",
                    "id": "123456"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075",
                    "788d8874-8007-4253-92b7-ee6b6c20c6f3"
                ],
                "remove": [
                    "8f812592-3f06-416b-bd50-e7831848a31a"
                ]
            }
        },
        {
            "attributes": {
                "firstName": "Harry",
                "birthDate": "1980/07/21"
            },
            "identities": [
                {
                    "type": "email",
                    "id": "harry.p@example.com"
                }
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                    "36a51c13-9dd6-4d2c-8aa3-07d785ea5075"
                ],
                "remove": []
            }
        }
    ]
}
```

### Aggregationsschlüssel in Ihre Vorlage aufnehmen, um auf exportierte Profile zuzugreifen, die nach verschiedenen Kriterien gruppiert sind {#template-aggregation-key}

Wenn Sie [konfigurierbare Aggregation](./destination-configuration.md#configurable-aggregation) in der Zielkonfiguration können Sie die in Ihr Ziel exportierten Profile anhand von Kriterien wie Segment-ID, Segmentalias, Segmentzugehörigkeit oder Identitäts-Namespaces gruppieren.

In der Vorlage für die Nachrichtenumwandlung können Sie auf die oben erwähnten Aggregationsschlüssel zugreifen, wie in den Beispielen in den folgenden Abschnitten dargestellt. Verwenden Sie Aggregationsschlüssel, um die aus Experience Platform exportierte HTTP-Nachricht so zu strukturieren, dass sie den von Ihrem Ziel erwarteten Format- und Ratenbeschränkungen entspricht.

#### Verwenden des Segment-ID-Aggregationsschlüssels in der Vorlage {#aggregation-key-segment-id}

Wenn Sie [konfigurierbare Aggregation](./destination-configuration.md#configurable-aggregation) und `includeSegmentId` auf &quot;true&quot;gesetzt ist, werden die Profile in den an Ihr Ziel exportierten HTTP-Nachrichten nach Segment-ID gruppiert. Unten sehen Sie, wie Sie auf die Segment-ID in der Vorlage zugreifen können.

**Eingabe**

Betrachten Sie die folgenden vier Profile, bei denen:
* die ersten beiden sind Teil des Segments mit der Segment-ID `788d8874-8007-4253-92b7-ee6b6c20c6f3`
* das dritte Profil ist Teil des Segments mit der Segment-ID `8f812592-3f06-416b-bd50-e7831848a31a`
* Das vierte Profil ist Teil beider oben genannten Segmente.

Profil 1:

```json
{
   "attributes":{
      "firstName":{
         "value":"Hermione"
      }
   },
   "segmentMembership":{
      "ups":{
         "788d8874-8007-4253-92b7-ee6b6c20c6f3":{
            "lastQualificationTime":"2020-11-20T13:15:49Z",
            "status":"realized"
         }
      }
   }
}
```

Profil 2:

```json
{
   "attributes":{
      "firstName":{
         "value":"Harry"
      }
   },
   "segmentMembership":{
      "ups":{
         "788d8874-8007-4253-92b7-ee6b6c20c6f3":{
            "lastQualificationTime":"2020-11-20T13:15:49Z",
            "status":"realized"
         }
      }
   }
}
```

Profil 3:

```json
{
   "attributes":{
      "firstName":{
         "value":"Tom"
      }
   },
   "segmentMembership":{
      "ups":{
         "8f812592-3f06-416b-bd50-e7831848a31a":{
            "lastQualificationTime":"2021-02-20T12:00:00Z",
            "status":"realized"
         }
      }
   }
}
```

Profil 4:

```json
{
   "attributes":{
      "firstName":{
         "value":"Jerry"
      }
   },
   "segmentMembership":{
      "ups":{
         "8f812592-3f06-416b-bd50-e7831848a31a":{
            "lastQualificationTime":"2021-02-20T12:00:00Z",
            "status":"realized"
         },
         "788d8874-8007-4253-92b7-ee6b6c20c6f3":{
            "lastQualificationTime":"2020-11-20T13:15:49Z",
            "status":"realized"
         }
      }
   }
}
```

**Vorlage**

>[!IMPORTANT]
>
>Bei allen Vorlagen, die Sie verwenden, müssen Sie die unzulässigen Zeichen, z. B. doppelte Anführungszeichen, maskieren `""` vor dem Einfügen der Vorlage in die [Zielserverkonfiguration](./server-and-template-configuration.md#template-specs). Weitere Informationen zum Escapen von doppelten Anführungszeichen finden Sie in Kapitel 9 im Abschnitt [JSON-Standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

Beachten Sie Folgendes: `audienceId` wird in der Vorlage verwendet, um auf Segment-IDs zuzugreifen. In diesem Beispiel wird davon ausgegangen, dass Sie `audienceId` für die Segmentzugehörigkeit in Ihrer Zieltaxonomie. Je nach Ihrer eigenen Taxonomie können Sie stattdessen einen beliebigen anderen Feldnamen verwenden.

```python
{
    "audienceId": "{{ input.aggregationKey.segmentId }}",
    "profiles": [
        {% for profile in input.profiles %}
        {
            "first_name": "{{ profile.attributes.firstName.value }}"
        }{% if not loop.last %},{% endif %}
        {% endfor %}
    ]
}
```

**Ergebnis**

Beim Export in Ihr Ziel werden die Profile basierend auf ihrer Segment-ID in zwei Gruppen aufgeteilt.

```json
{
   "audienceId":"788d8874-8007-4253-92b7-ee6b6c20c6f3",
   "profiles":[
      {
         "firstName":"Hermione"
      },
      {
         "firstName":"Harry"
      },
      {
         "firstName":"Jerry"
      }
   ]
}
```

```json
{
   "audienceId":"8f812592-3f06-416b-bd50-e7831848a31a",
   "profiles":[
      {
         "firstName":"Tom"
      },
      {
         "firstName":"Jerry"
      }
   ]
}
```

#### Segmentalias-Aggregationsschlüssel in der Vorlage verwenden {#aggregation-key-segment-alias}

Wenn Sie [konfigurierbare Aggregation](./destination-configuration.md#configurable-aggregation) und `includeSegmentId` auf &quot;true&quot;gesetzt ist, können Sie auch auf den Segmentalias in der Vorlage zugreifen.

Fügen Sie der Vorlage die folgende Zeile hinzu, um auf die exportierten Profile zuzugreifen, die nach Segmentalias gruppiert sind.

```python
customerList={{input.aggregationKey.segmentAlias}}
```

#### Segmentstatus-Aggregationsschlüssel in der Vorlage verwenden {#aggregation-key-segment-status}

Wenn Sie [konfigurierbare Aggregation](./destination-configuration.md#configurable-aggregation) und `includeSegmentId` und `includeSegmentStatus` auf &quot;true&quot;gesetzt ist, können Sie auf den Segmentstatus in der Vorlage zugreifen. Auf diese Weise können Sie Profile in den an Ihr Ziel exportierten HTTP-Nachrichten gruppieren, je nachdem, ob die Profile hinzugefügt oder aus Segmenten entfernt werden sollen.

Mögliche Werte sind:

* realisiert
* vorhanden
* beendet

Fügen Sie der Vorlage die folgende Zeile hinzu, um Profile aus Segmenten hinzuzufügen oder daraus zu entfernen, basierend auf den oben stehenden Werten:

```python
action={% if input.aggregationKey.segmentStatus == "exited" %}REMOVE{% else %}ADD{% endif%}
```

#### Verwenden Sie den Identitäts-Namespace-Aggregationsschlüssel in der Vorlage. {#aggregation-key-identity}

Im Folgenden finden Sie ein Beispiel, bei dem die Variable [konfigurierbare Aggregation](./destination-configuration.md#configurable-aggregation) in der Zielkonfiguration so eingestellt ist, dass exportierte Profile anhand von Identitäts-Namespaces im Formular aggregiert werden `"namespaces": ["email", "phone"]` und `"namespaces": ["GAID", "IDFA"]`. Siehe Abschnitt `groups` -Parameter in der [API-Referenz zur Zielkonfiguration](./destination-configuration-api.md) für weitere Informationen zu dieser Gruppierung.

**Eingabe**

Profil 1:

```json
{
   "identityMap":{
      "email":[
         {
            "id":"e1@example.com"
         },
         {
            "id":"e2@example.com"
         }
      ],
      "phone":[
         {
            "id":"+40744111222"
         }
      ],
      "IDFA":[
         {
            "id":"AEBE52E7-03EE-455A-B3C4-E57283966239"
         }
      ],
      "GAID":[
         {
            "id":"e4fe9bde-caa0-47b6-908d-ffba3fa184f2"
         }
      ]
   }
}
```

Profil 2:

```json
{
   "identityMap":{
      "email":[
         {
            "id":"e3@example.com"
         }
      ],
      "phone":[
         {
            "id":"+40744333444"
         },
         {
            "id":"+40744555666"
         }
      ],
      "IDFA":[
         {
            "id":"134GHU45-34HH-GHJ7-K0H8-LHN665998NN0"
         }
      ],
      "GAID":[
         {
            "id":"47bh00i9-8jv6-334n-lll8-nb7f24sghg76"
         }
      ]
   }
}
```

**Vorlage**

>[!IMPORTANT]
>
>Bei allen Vorlagen, die Sie verwenden, müssen Sie die unzulässigen Zeichen, z. B. doppelte Anführungszeichen, maskieren `""` vor dem Einfügen der Vorlage in die [Zielserverkonfiguration](./server-and-template-configuration.md#template-specs). Weitere Informationen zum Escapen von doppelten Anführungszeichen finden Sie in Kapitel 9 im Abschnitt [JSON-Standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

Beachten Sie Folgendes: `input.aggregationKey.identityNamespaces` wird in der folgenden Vorlage verwendet

```python
{
            "profiles": [
            {% for profile in input.profiles %}
            {
                {% for ns in input.aggregationKey.identityNamespaces %}
                "{{ns}}": [
                    {% for id in profile.identityMap[ns] %}
                    "{{id.id}}"{% if not loop.last %},{% endif %}
                    {% endfor %}
                ]{% if not loop.last %},{% endif %}
                {% endfor %}
            }{% if not loop.last %},{% endif %}
            {% endfor %}
        ]
}
```

**Ergebnis**

Beim Export in Ihr Ziel werden die Profile basierend auf ihren Identitäts-Namespaces in zwei Gruppen aufgeteilt. E-Mail und Telefon sind in einer Gruppe, während GAID und IDFA in einer anderen Gruppe sind.

```json
{
   "profiles":[
      {
         "email":[
            "e1@example.com",
            "e2@example.com"
         ],
         "phone":[
            "+40744111222"
         ]
      },
      {
         "email":[
            "e3@example.com"
         ],
         "phone":[
            "+40744333444",
            "+40744555666"
         ]
      }
   ]
}
```

```json
{
   "profiles":[
      {
         "IDFA":[
            "AEBE52E7-03EE-455A-B3C4-E57283966239"
         ],
         "GAID":[
            "e4fe9bde-caa0-47b6-908d-ffba3fa184f2"
         ]
      },
      {
         "IDFA":[
            "134GHU45-34HH-GHJ7-K0H8-LHN665998NN0"
         ],
         "GAID":[
            "47bh00i9-8jv6-334n-lll8-nb7f24sghg76"
         ]
      }
   ]
}
```

#### Verwenden des Aggregationsschlüssels in einer URL-Vorlage {#aggregation-key-url-template}

Je nach Anwendungsfall können Sie auch die hier beschriebenen Aggregationsschlüssel in einer URL verwenden, wie unten dargestellt:

```python
https://api.example.com/audience/{{input.aggregationKey.segmentId}}
```

### Referenz: Kontext und Funktionen, die in Umwandlungsvorlagen verwendet werden {#reference}

Der Kontext, der der Vorlage bereitgestellt wird, enthält `input`  (die in diesem Aufruf exportierten Profile/Daten) und `destination` (Daten über das Ziel, an das die Adobe Daten sendet, gültig für alle Profile).

Die nachstehende Tabelle enthält Beschreibungen der Funktionen in den obigen Beispielen.

| Funktion | Beschreibung |
|---------|----------|
| `input.profile` | Das Profil, dargestellt als [JsonNode](https://fasterxml.github.io/jackson-databind/javadoc/2.11/com/fasterxml/jackson/databind/node/JsonNodeType.html). Folgt dem weiter oben erwähnten Partner-XDM-Schema auf dieser Seite. |
| `destination.segmentAliases` | Ordnen Sie Segmentkennungen im Adobe Experience Platform-Namespace Segmentaliasen im System des Partners zu. |
| `destination.segmentNames` | Ordnen Sie Segmentnamen im Adobe Experience Platform-Namespace Segmentnamen im System des Partners zu. |
| `addedSegments(listOfSegments)` | Gibt nur Segmente mit Status zurück `realized`. |
| `removedSegments(listOfSegments)` | Gibt nur Segmente mit Status zurück `exited`. |

{style="table-layout:auto"}

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie aus Experience Platform exportierte Daten transformiert werden. Lesen Sie als Nächstes die folgenden Seiten, um Ihre Kenntnisse über die Erstellung von Vorlagen zur Nachrichtenumwandlung für Ihr Ziel zu vervollständigen:

* [Erstellen und Testen einer Nachrichten-Umwandlungsvorlage](/help/destinations/destination-sdk/create-template.md)
* [API-Vorgänge für Rendervorlagen](/help/destinations/destination-sdk/render-template-api.md)
* [Unterstützte Umwandlungsfunktionen in Destination SDK](/help/destinations/destination-sdk/supported-functions.md)
