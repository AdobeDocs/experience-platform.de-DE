---
description: Auf dieser Seite werden das Nachrichtenformat und die Profilumwandlung von aus Adobe Experience Platform in Ziele exportierten Daten behandelt.
title: Nachrichtenformat
exl-id: ab05d34e-530f-456c-b78a-7f3389733d35
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '2237'
ht-degree: 100%

---

# Nachrichtenformat

## Voraussetzungen – Adobe Experience Platform-Konzepte {#prerequisites}

Um das Nachrichtenformat sowie den Profilkonfigurations- und -konvertierungsprozess auf der Seite von Adobe zu verstehen, machen Sie sich mit den folgenden Konzepten von Experience Platform vertraut:

* **Experience-Datenmodell (XDM)**. [XDM-Übersicht](../../../../xdm/home.md) und [Erstellen eines XDM-Schemas in Adobe Experience Platform](../../../../xdm/tutorials/create-schema-ui.md).
* **Klasse**. [Erstellen und Bearbeiten von Klassen in der Benutzeroberfläche](../../../../xdm/ui/resources/classes.md).
* **IdentityMap**. Die Identitätszuordnung stellt eine Zuordnung aller Endbenutzeridentitäten in Adobe Experience Platform dar. Siehe `xdm:identityMap` im [Wörterbuch der XDM-Felder](../../../../xdm/schema/field-dictionary.md).
* **SegmentMembership**. Das XDM-Attribut [segmentMembership](../../../../xdm/schema/field-dictionary.md) informiert darüber, zu welchen Zielgruppen ein Profil gehört. Lesen Sie zu den drei verschiedenen Werten im Feld `status` die Dokumentation zur [Schemafeldgruppe der Zielgruppenzugehörigkeitsdetails](../../../../xdm/field-groups/profile/segmentation.md).

>[!IMPORTANT]
>
>Bei allen von Destination SDK unterstützten Parameternamen und Werten wird **nach Groß-/Kleinschreibung unterschieden**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Unterstützte Integrationstypen {#supported-integration-types}

Die nachstehende Tabelle beschreibt ausführlich, welche Integrationstypen die auf dieser Seite beschriebenen Funktionen unterstützen.

| Integrationstyp | Unterstützt Funktionen |
|---|---|
| Echtzeit-Integrationen (Streaming) | Ja |
| Dateibasierte (Batch-)Integrationen | Ja (nur die Schritte 1 und 2 im unten stehenden Diagramm) |

## Übersicht {#overview}

Auf dieser Seite werden das Nachrichtenformat und die Profilumwandlung von aus Adobe Experience Platform in Ziele exportierten Daten behandelt.

Adobe Experience Platform exportiert Daten in eine beträchtliche Anzahl von Zielen in verschiedenen Datenformaten. Beispiele für Zieltypen sind Werbeplattformen (Google), soziale Netzwerke (Facebook) und Cloud-Speicher-Standorte (Amazon S3, Azure Event Hub).

Experience Platform kann das Nachrichtenformat der exportierten Profile so anpassen, dass es dem erwarteten Format auf Ihrer Seite entspricht. Um diese Anpassung zu verstehen, sind die folgenden Konzepte wichtig:

* Das XDM-Quellschema (1) und -Zielschema (2) in Adobe Experience Platform
* Das erwartete Nachrichtenformat auf der Partnerseite (3) und
* Die Transformationsebene zwischen dem XDM-Schema und dem erwarteten Nachrichtenformat, die Sie definieren können, indem Sie eine [Nachrichtenumwandlungsvorlage](#using-templating) erstellen.

![Umwandlung von Schemata in JSON](../../assets/functionality/destination-server/transformations-3-steps.png)

XDM-Schemata dienen in Experience Platform zur konsistenten und wiederverwendbaren Beschreibung der Struktur von Daten.

<!--

Users who want to activate data to your destination need to map the fields in their Experience Platform datasets to a schema that translates to your destination's expected format. Adobe will create a custom field group for your company to add to the target schema. The fields in the field group depend on the profile attribute fields that you can receive.

-->

**XDM-Quellschema (1)**: Dieses Element bezieht sich auf das Schema, das Kundinnen und Kunden in Experience Platform verwenden. In Experience Platform können Kundinnen und Kunden im [Zuordnungsschritt](../../../ui/activate-segment-streaming-destinations.md#mapping) des Zielaktivierungs-Workflows Felder aus ihrem XDM-Schema dem Zielschema Ihres Ziels zuordnen (2).

**Ziel-XDM-Schema (2)**: Basierend auf dem JSON-Standardschema (3) des erwarteten Formats Ihres Ziels und den Attributen, die Ihr Ziel interpretieren kann, können Sie Profilattribute und Identitäten in Ihrem Ziel-XDM-Schema definieren. Dies können Sie in der Zielkonfiguration in den Objekten [schemaConfig](../../functionality/destination-configuration/schema-configuration.md) und [identityNamespaces](../../functionality/destination-configuration/identity-namespace-configuration.md) tun.

**JSON-Standardschema Ihrer Zielprofilattribute (3)**: Dieses Beispiel stellt ein [JSON-Schema](https://json-schema.org/learn/miscellaneous-examples.html) der von Ihrer Plattform unterstützten Profilattribute und der zugehörigen Typen dar (z. B.: Objekt, Zeichenfolge, Array). Beispielfelder, die Ihr Ziel unterstützt, könnten `firstName`, `lastName`, `gender`, `email`, `phone`, `productId`, `productName` usw. sein. Sie benötigen eine [Nachrichtenumwandlungsvorlage](#using-templating), um die aus Experience Platform exportierten Daten an das gewünschte Format anzupassen.

Basierend auf den oben beschriebenen Schematransformationen wird hier gezeigt, wie sich eine Profilkonfiguration zwischen dem Quell-XDM-Schema und einem Beispielschema auf Partnerseite ändert:

![Beispiel einer Umwandlungsmeldung](../../assets/functionality/destination-server/transformations-with-examples.png)

## Erste Schritte: Transformieren von drei grundlegenden Attributen {#getting-started}

Um den Prozess der Profilumwandlung zu demonstrieren, verwendet das folgende Beispiel drei gängige Profilattribute in Adobe Experience Platform: **Vorname**, **Nachname** und **E-Mail-Adresse**.

>[!NOTE]
>
>Die Kundin bzw. der Kunde ordnet die Attribute aus dem Quell-XDM-Schema dem Partner-XDM-Schema in der Adobe Experience Platform-Benutzeroberfläche zu, und zwar im Schritt **Zuordnung** [ des Zielaktivierungs-Workflows](../../../ui/activate-segment-streaming-destinations.md#mapping).

Nehmen wir an, Ihre Plattform kann ein Nachrichtenformat wie das Folgende erhalten:

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
   * Dieser Abschnitt enthält alle Zielgruppen, die im Profil vorhanden sind. Die Zielgruppen können einen von zwei Status aufweisen: `realized` oder `exited`.
* `identityMap` (immer in einem Profil vorhanden)
   * Dieser Abschnitt enthält alle Identitäten, die im Profil vorhanden sind (E-Mail, Google GAID, Apple IDFA usw.) und die von der Benutzerin bzw. dem Benutzer im Aktivierungs-Workflow für den Export zugeordnet wurden.
* Attribute (je nach Zielkonfiguration können diese im Profil vorhanden sein). Es gibt auch einen geringfügigen Unterschied zwischen vordefinierten Attributen und Freiformattributen:
   * Für *Freiformattribute* enthalten diese einen Pfad `.value`, wenn das Attribut im Profil vorhanden ist (siehe das Attribut `lastName` aus Beispiel 1). Wenn sie nicht im Profil vorhanden sind, enthalten sie den Pfad `.value` nicht (siehe das Attribut `firstName` aus Beispiel 1).
   * Für *vordefinierte Attribute* enthalten diese keinen Pfad `.value`. Alle zugeordneten Attribute, die in einem Profil vorhanden sind, werden in der Attributzuordnung angezeigt. Die nicht vorhandenen werden nicht vorhanden sein (siehe Beispiel 2, wo das Attribut `firstName` nicht im Profil vorhanden ist).

Unten sehen Sie zwei Beispiele für Profile in Experience Platform:

### Beispiel 1 mit `segmentMembership`, `identityMap` und Attributen für Freiformattribute {#example-1}

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

### Beispiel 2 mit `segmentMembership`, `identityMap` und Attributen für vordefinierte Attribute {#example-2}

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

## Verwenden einer Vorlagensprache für die Transformationen von Identitäten, Attributen und Zielgruppenzugehörigkeit {#using-templating}

Adobe verwendet [Pebble-Vorlagen](https://pebbletemplates.io/), eine Vorlagensprache, die [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) ähnelt, um die Felder aus dem XDM-Schema in ein von Ihrem Ziel unterstütztes Format umzuwandeln.

In diesem Abschnitt finden Sie mehrere Beispiele dafür, wie diese Transformationen vorgenommen werden – vom Eingabe-XDM-Schema über die Vorlage und die Ausgabe in Payload-Formaten, die von Ihrem Ziel akzeptiert werden. Die folgenden Beispiele werden mit zunehmender Komplexität wie folgt dargestellt:

1. Einfache Transformationsbeispiele. Erfahren Sie, wie die Vorlage mit einfachen Transformationen für die Felder [Profilattribute](#attributes), [Zielgruppenmitgliedschaft](#segment-membership) und [Identität](#identities) arbeitet.
2. Beispiele für komplexere Vorlagen, die die oben genannten Felder kombinieren: [Erstellen einer Vorlage zum Senden von Zielgruppen und Identitäten](./message-format.md#segments-and-identities) und [Erstellen einer Vorlage zum Senden von Segmenten, Identitäten und Profilattributen](#segments-identities-attributes).
3. Vorlagen, die den Aggregationsschlüssel enthalten. Wenn Sie [konfigurierbare Aggregation](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) in der Zielkonfiguration verwenden, gruppiert Experience Platform die in Ihr Ziel exportierten Profile anhand von Kriterien wie Zielgruppen-ID, Zielgruppenstatus oder Identity-Namespaces.

### Profilattribute {#attributes}

Informationen zum Transformieren der in Ihr Ziel exportierten Profilattribute finden Sie in den JSON- und Code-Beispielen unten.

>[!IMPORTANT]
>
>Eine Liste aller in Adobe Experience Platform verfügbaren Profilattribute finden Sie im [Wörterbuch der XDM-Felder](../../../../xdm/schema/field-dictionary.md).


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
>Bei allen Vorlagen, die Sie verwenden, müssen Sie die unzulässigen Zeichen, z. B. doppelte Anführungszeichen `""`, mit Escape-Zeichen versehen, bevor Sie die [Vorlage](../../functionality/destination-server/templating-specs.md) in die [Ziel-Server-Konfiguration](../../authoring-api/destination-server/create-destination-server.md) einfügen. Weitere Informationen zum Maskieren von doppelten Anführungszeichen mit Escape-Zeichen finden Sie in Kapitel 9 im [JSON-Standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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

### Zielgruppenmitgliedschaft {#audience-membership}

Das XDM-Attribut [segmentMembership](../../../../xdm/schema/field-dictionary.md) informiert darüber, zu welchen Zielgruppen ein Profil gehört.
Lesen Sie zu den drei verschiedenen Werten im Feld `status` die Dokumentation zur [Schemafeldgruppe der Zielgruppenzugehörigkeitsdetails](../../../../xdm/field-groups/profile/segmentation.md).

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
>Bei allen Vorlagen, die Sie verwenden, müssen Sie die unzulässigen Zeichen, z. B. doppelte Anführungszeichen `""`, mit Escape-Zeichen versehen, bevor Sie die [Vorlage](../../functionality/destination-server/templating-specs.md) in die [Ziel-Server-Konfiguration](../../authoring-api/destination-server/create-destination-server.md) einfügen. Weitere Informationen zum Maskieren von doppelten Anführungszeichen mit Escape-Zeichen finden Sie in Kapitel 9 im [JSON-Standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).


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
                {# Alternative syntax for filtering audiences by status: #}
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

Weitere Informationen zu Identitäten in Experience Platform finden Sie in der [Übersicht über Identity-Namespaces](../../../../identity-service/namespaces.md).

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
>Bei allen Vorlagen, die Sie verwenden, müssen Sie die unzulässigen Zeichen, z. B. doppelte Anführungszeichen `""`, mit Escape-Zeichen versehen, bevor Sie die [Vorlage](../../functionality/destination-server/templating-specs.md) in die [Ziel-Server-Konfiguration](../../authoring-api/destination-server/create-destination-server.md) einfügen. Weitere Informationen zum Maskieren von doppelten Anführungszeichen mit Escape-Zeichen finden Sie in Kapitel 9 im [JSON-Standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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

### Erstellen einer Vorlage, die Zielgruppen und Identitäten sendet {#segments-and-identities}

In diesem Abschnitt finden Sie ein Beispiel für eine häufig verwendete Transformation zwischen dem Adobe-XDM-Schema und dem Partnerzielschema.
Im folgenden Beispiel erfahren Sie, wie Sie die Zielgruppenzugehörigkeit und das Identitätsformat transformieren und an Ihr Ziel ausgeben.

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
>Bei allen Vorlagen, die Sie verwenden, müssen Sie die unzulässigen Zeichen, z. B. doppelte Anführungszeichen `""`, mit Escape-Zeichen versehen, bevor Sie die [Vorlage](../../functionality/destination-server/templating-specs.md) in die [Ziel-Server-Konfiguration](../../authoring-api/destination-server/create-destination-server.md) einfügen. Weitere Informationen zum Maskieren von doppelten Anführungszeichen mit Escape-Zeichen finden Sie in Kapitel 9 im [JSON-Standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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
                    {# Alternative syntax for filtering audiences by status: #}
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

Ein weiteres gängiges Anwendungsbeispiel ist der Export von Daten, die Zielgruppenzugehörigkeiten, Identitäten (z. B. E-Mail-Adresse, Telefonnummer, Werbe-ID) und Profilattribute enthalten. Um Daten auf diese Weise zu exportieren, sehen Sie sich das folgende Beispiel an:

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
>Bei allen Vorlagen, die Sie verwenden, müssen Sie die unzulässigen Zeichen, z. B. doppelte Anführungszeichen `""`, mit Escape-Zeichen versehen, bevor Sie die [Vorlage](../../functionality/destination-server/templating-specs.md) in die [Ziel-Server-Konfiguration](../../authoring-api/destination-server/create-destination-server.md) einfügen. Weitere Informationen zum Maskieren von doppelten Anführungszeichen mit Escape-Zeichen finden Sie in Kapitel 9 im [JSON-Standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

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
                {# Alternative syntax for filtering audiences by status: #}
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

### Nehmen Sie Aggregationsschlüssel in Ihre Vorlage auf, um auf exportierte Profile zuzugreifen, die nach verschiedenen Kriterien gruppiert sind {#template-aggregation-key}

Wenn Sie die [konfigurierbare Aggregation](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) in der Zielkonfiguration verwenden, können Sie die in Ihr Ziel exportierten Profile anhand von Kriterien wie Zielgruppen-ID, Zielgruppenalias, Zielgruppenzugehörigkeit oder Identity-Namespaces gruppieren.

In der Nachrichtenumwandlungsvorlage können Sie auf die oben erwähnten Aggregationsschlüssel zugreifen, wie in den Beispielen in den folgenden Abschnitten dargestellt. Verwenden Sie Aggregationsschlüssel, um die aus Experience Platform exportierte HTTP-Nachricht so zu strukturieren, dass sie den von Ihrem Ziel erwarteten Format- und Ratenbeschränkungen entspricht.

#### Verwenden des Zielgruppen-ID-Aggregationsschlüssels in der Vorlage {#aggregation-key-segment-id}

Wenn Sie [konfigurierbare Aggregation](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) verwenden und `includeSegmentId` auf „true“ gesetzt ist, werden die Profile in den an Ihr Ziel exportierten HTTP-Nachrichten nach Zielgruppen-ID gruppiert. Unten sehen Sie, wie Sie auf die Zielgruppen-ID in der Vorlage zugreifen können.

**Eingabe**

Betrachten Sie die folgenden vier Profile, bei denen:

* die ersten beiden Teil der Zielgruppe mit der Zielgruppen-ID `788d8874-8007-4253-92b7-ee6b6c20c6f3` sind
* das dritte Profil Teil der Zielgruppe mit der Zielgruppen-ID `8f812592-3f06-416b-bd50-e7831848a31a` ist
* das vierte Profil Teil beider oben genannten Zielgruppen ist.

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
>Bei allen Vorlagen, die Sie verwenden, müssen Sie die unzulässigen Zeichen, z. B. doppelte Anführungszeichen `""`, mit Escape-Zeichen versehen, bevor Sie die [Vorlage](../../functionality/destination-server/templating-specs.md) in die [Ziel-Server-Konfiguration](../../authoring-api/destination-server/create-destination-server.md) einfügen. Weitere Informationen zum Maskieren von doppelten Anführungszeichen mit Escape-Zeichen finden Sie in Kapitel 9 im [JSON-Standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

Beachten Sie, wie `audienceId` in der Vorlage verwendet wird, um auf Zielgruppen-IDs zuzugreifen. In diesem Beispiel wird davon ausgegangen, dass Sie `audienceId` für die Zielgruppenzugehörigkeit in Ihrer Zieltaxonomie verwenden. Je nach Ihrer eigenen Taxonomie können Sie stattdessen einen beliebigen anderen Feldnamen verwenden.

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

Beim Export in Ihr Ziel werden die Profile basierend auf ihrer Zielgruppen-ID in zwei Gruppen aufgeteilt.

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

#### Verwenden eines Zielgruppenalias-Aggregationsschlüssels in der Vorlage {#aggregation-key-segment-alias}

Wenn Sie [konfigurierbare Aggregation](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) verwenden und `includeSegmentId` auf „true“ gesetzt ist, können Sie auch auf den Zielgruppenalias in der Vorlage zugreifen.

Fügen Sie der Vorlage die folgende Zeile hinzu, um auf die exportierten Profile zuzugreifen, die nach Zielgruppenalias gruppiert sind.

```python
customerList={{input.aggregationKey.segmentAlias}}
```

#### Verwenden eines Zielgruppenstatus-Aggregationsschlüssels in der Vorlage {#aggregation-key-segment-status}

Wenn Sie [konfigurierbare Aggregation](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) verwenden und `includeSegmentId` und `includeSegmentStatus` auf „true“ gesetzt ist, können Sie auf den Zielgruppenstatus in der Vorlage zugreifen. Auf diese Weise können Sie Profile in den an Ihr Ziel exportierten HTTP-Nachrichten gruppieren, je nachdem, ob die Profile hinzugefügt oder aus Segmenten entfernt werden sollen.

Mögliche Werte sind:

* realized
* existing
* exited

Fügen Sie der Vorlage die folgende Zeile hinzu, um Profile aus Segmenten hinzuzufügen oder daraus zu entfernen, basierend auf den oben stehenden Werten:

```python
action={% if input.aggregationKey.segmentStatus == "exited" %}REMOVE{% else %}ADD{% endif%}
```

#### Verwenden des Identity-Namespace-Aggregationsschlüssels in der Vorlage {#aggregation-key-identity}

Im Folgenden finden Sie ein Beispiel, bei dem die [konfigurierbare Aggregation](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) in der Zielkonfiguration so eingestellt ist, dass exportierte Profile anhand von Identity-Namespaces in der Form `"namespaces": ["email", "phone"]` und `"namespaces": ["GAID", "IDFA"]` aggregiert werden. Weitere Informationen zur Gruppierung finden Sie unter dem Parameter `groups` in der Dokumentation [Erstellen der Zielkonfiguration](../../authoring-api/destination-configuration/create-destination-configuration.md).

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
>Bei allen Vorlagen, die Sie verwenden, müssen Sie die unzulässigen Zeichen, z. B. doppelte Anführungszeichen `""`, mit Escape-Zeichen versehen, bevor Sie die [Vorlage](../../functionality/destination-server/templating-specs.md) in die [Ziel-Server-Konfiguration](../../authoring-api/destination-server/create-destination-server.md) einfügen. Weitere Informationen zum Maskieren von doppelten Anführungszeichen mit Escape-Zeichen finden Sie in Kapitel 9 im [JSON-Standard](https://www.ecma-international.org/publications-and-standards/standards/ecma-404/).

Beachten Sie, dass `input.aggregationKey.identityNamespaces` in der folgenden Vorlage verwendet wird

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

Beim Export in Ihr Ziel werden die Profile basierend auf ihren Identity-Namespaces in zwei Gruppen aufgeteilt. E-Mail und Telefon sind in einer Gruppe, während GAID und IDFA in einer anderen Gruppe sind.

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

Der Kontext, der der Vorlage bereitgestellt wird, enthält `input` (die in diesem Aufruf exportierten Profile/Daten) und `destination` (Daten über das Ziel, an das Adobe Daten sendet, gültig für alle Profile).

Die nachstehende Tabelle enthält Beschreibungen der Funktionen in den obigen Beispielen.

| Funktion | Beschreibung |
|---------|----------|
| `input.profile` | Das Profil, dargestellt als ein [JsonNode](https://fasterxml.github.io/jackson-databind/javadoc/2.11/com/fasterxml/jackson/databind/node/JsonNodeType.html). Folgt dem weiter oben erwähnten Partner-XDM-Schema auf dieser Seite. |
| `destination.segmentAliases` | Ordnen Sie Zielgruppen-IDs im Adobe Experience Platform-Namespace den Zielgruppenaliasen im System des Partners zu. |
| `destination.segmentNames` | Ordnen Sie Zielgruppennamen im Adobe Experience Platform-Namespace den Zielgruppennamen im System des Partners zu. |
| `addedSegments(listOfSegments)` | Gibt nur Zielgruppen mit Status `realized` zurück. |
| `removedSegments(listOfSegments)` | Gibt nur Zielgruppen mit Status `exited` zurück. |

{style="table-layout:auto"}

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie aus Experience Platform exportierte Daten transformiert werden. Lesen Sie als Nächstes die folgenden Seiten, um Ihre Kenntnisse über die Erstellung von Nachrichtenumwandlungsvorlagen für Ihr Ziel zu vervollständigen:

* [Erstellen und Testen einer Nachrichtenumwandlungsvorlage](../../testing-api/streaming-destinations/create-template.md)
* [API-Vorgänge für Rendervorlagen](../../testing-api/streaming-destinations/render-template-api.md)
* [Unterstützte Umwandlungsfunktionen in Destination SDK](../destination-server/supported-functions.md)

Weitere Informationen zu den anderen Ziel-Server-Komponenten finden Sie in den folgenden Artikeln:

* [Server-Spezifikationen für Ziele, die mit Destination SDK erstellt wurden](server-specs.md)
* [Vorlagenspezifikationen](templating-specs.md)
* [Konfiguration der Dateiformatierung](file-formatting.md)
