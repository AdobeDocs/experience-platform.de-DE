---
description: Verwenden Sie den Inhalt auf dieser Seite zusammen mit den restlichen Konfigurationsoptionen für Partnerziele. Diese Seite behandelt das Nachrichtenformat von Daten, die aus Adobe Experience Platform in Ziele exportiert wurden, während die andere Seite Details zur Verbindung und Authentifizierung mit Ihrem Ziel enthält.
seo-description: Use the content on this page together with the rest of the configuration options for partner destinations. This page addresses the messaging format of data exported from Adobe Experience Platform to destinations, while the other page addresses specifics about connecting and authenticating to your destination.
seo-title: Message format
title: Nachrichtenformat
source-git-commit: d60933d2083b7befcfa8beba4b1630f372c08cfa
workflow-type: tm+mt
source-wordcount: '1505'
ht-degree: 3%

---

# Nachrichtenformat

## Voraussetzungen - Adobe Experience Platform-Konzepte {#prerequisites}

Machen Sie sich mit den folgenden Konzepten der Experience Platform vertraut, um die Adobe zu verstehen:

* **Experience-Datenmodell (XDM)**. [XDM-](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=de) Übersicht und   [Erstellen eines XDM-Schemas in Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=en).
* **Klasse**. [Erstellen und bearbeiten Sie Klassen in der Benutzeroberfläche](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/classes.html?lang=en).
* **Feldergruppe**. [Feldergruppendefinition ](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en#field-group) und  [weitere Informationen zu Feldergruppen](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=en#field-group).
* **IdentityMap**. Die Identitätszuordnung stellt eine Zuordnung aller Endbenutzeridentitäten in Adobe Experience Platform dar. Siehe `xdm:identityMap` im [XDM-Feldwörterbuch](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en).
* **Segmentzugehörigkeit**. Das XDM-Attribut [segmentMembership](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en) informiert darüber, zu welchen Segmenten ein Profil gehört. Lesen Sie für die drei verschiedenen Werte im Feld `status` die Dokumentation zu [Schema-Feldergruppe &quot;Segmentzugehörigkeitsdetails](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html).

## Übersicht {#overview}

Verwenden Sie den Inhalt auf dieser Seite zusammen mit den restlichen [Konfigurationsoptionen für Partnerziele](./configuration-options.md). Diese Seite behandelt das Nachrichtenformat von Daten, die aus Adobe Experience Platform in Ziele exportiert wurden, während die andere Seite Details zur Verbindung und Authentifizierung mit Ihrem Ziel enthält.

Adobe Experience Platform exportiert Daten in eine beträchtliche Anzahl von Zielen in verschiedenen Datenformaten. Beispiele für Zieltypen sind Werbeplattformen (Google), soziale Netzwerke (Facebook), Cloud-Speicher-Standorte (Amazon S3, Azure Event Hub).

Experience Platform kann das exportierte Nachrichtenformat an das erwartete Format auf Ihrer Seite anpassen. Um diese Anpassung zu verstehen, sind die folgenden Konzepte wichtig:
* Das XDM-Quellschema (1) und das Ziel-Schema (2) in Adobe Experience Platform
* Das Nachrichtenformat auf der Partnerseite (3) und
* Die Transformationsebene zwischen den beiden, die Sie definieren können, indem Sie eine [Nachrichtenumwandlungsvorlage](./message-format.md#using-templating) erstellen.

![Umwandlung von Schemata in JSON](./assets/transformations-3-steps.png)

Schemas dienen in Experience Platform zur konsistenten und wiederverwendbaren Beschreibung der Struktur von Daten.

Benutzer, die Daten für Ihr Ziel aktivieren möchten, müssen die für ihre Datensätze verwendeten Felder in Experience Platform zu einem Schema zuordnen, das in das erwartete Zielformat übersetzt. Adobe erstellt eine benutzerdefinierte Feldergruppe für Ihr Unternehmen, die zum Zielschema hinzugefügt werden soll. Die Felder in der Feldergruppe hängen von den Profilattributfeldern ab, die Sie empfangen können.

**Quell-XDM-Schema (1)**: Dies bezieht sich auf das Schema, das ein Kunde in Experience Platform verwendet. In Experience Platform ordneten Kunden im [Zuordnungsschritt](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en#mapping) des Zielaktivierungs-Workflows Felder aus ihrem Quellschema dem Zielschema Ihres Ziels zu (2).

**Target-XDM-Schema (2)**: Basierend auf dem JSON-Standardschema (3), das Sie für Adobe freigeben, erstellt das Team in Adobe ein benutzerdefiniertes Schema für Ihr Ziel. Beachten Sie, dass Sie in einer [künftigen Phase des Projekts](./overview.md#phased-approach) das benutzerdefinierte Schema für Ihr Ziel selbst erstellen können.

**JSON-Standardschema Ihrer Zielprofilattribute (3)**: Bitte geben Sie ein  [JSON-](https://json-schema.org/learn/miscellaneous-examples.html) Schema mit allen Profilattributen, die Ihre Plattform unterstützt, und deren Typen an (z. B.: -Objekt, -Zeichenfolge, -Array). Beispiele für Felder, die Ihr Ziel unterstützen könnte, sind `firstName`, `lastName`, `gender`, `email`, `phone`, `productId`, `productName` usw.

Basierend auf den oben beschriebenen Schematransformationen wird hier gezeigt, wie sich die Struktur einer Nachricht zwischen dem Quell-XDM-Schema und dem Beispielschema auf der Partnerseite ändert:

![Beispiel einer Umwandlungsmeldung](./assets/transformations-with-examples.png)

<br> 


## Erste Schritte - Transformieren von drei grundlegenden Attributen {#getting-started}

Zur Veranschaulichung des Umwandlungsprozesses verwendet das folgende Beispiel drei gemeinsame Profilattribute in Adobe Experience Platform: **Vorname**, **Nachname** und **E-Mail-Adresse**.

>[!NOTE]
>
>Der Kunde ordnet die Attribute aus dem Quell-XDM-Schema dem Partner-XDM-Schema in der Adobe Experience Platform-Benutzeroberfläche im Schritt **Mapping** des [Aktivieren des Ziel-Workflows](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate-destinations.html#mapping) zu.

Nehmen wir an, Ihre Plattform kann ein Nachrichtenformat wie:

```curl
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

## Verwenden einer Vorlagensprache für die Transformationen von Identitäten, Attributen und Segmentzugehörigkeiten {#using-templating}

Adobe verwendet eine Vorlagensprache ähnlich [Jinja](https://jinja.palletsprojects.com/en/2.11.x/), um die Felder aus dem XDM-Schema in ein Format umzuwandeln, das von Ihrem Ziel unterstützt wird.

In diesem Abschnitt finden Sie mehrere Beispiele dafür, wie diese Umwandlungen durchgeführt werden, vom Eingabe-XDM-Schema über die Vorlage bis hin zur Ausgabe in Payload-Formaten, die von Ihrem Ziel akzeptiert werden. Die folgenden Beispiele werden nach zunehmender Komplexität sortiert:

1. Einfache Transformationsbeispiele. Erfahren Sie, wie die Vorlagenerstellung mit einfachen Transformationen für die Felder [Profilattribute](./message-format.md#attributes), [Segmentzugehörigkeit](./message-format.md#segment-membership) und [Identität](./message-format.md#identities) funktioniert.
2. Beispiele für komplexere Vorlagen, die die oben genannten Felder kombinieren: [Erstellen Sie eine Vorlage, die Segmente und Identitäten sendet](./message-format.md#segments-and-identities) und [Erstellen Sie eine Vorlage, die Segmente, Identitäten und Profilattribute sendet](./message-format.md#segments-identities-attributes).
3. Tief eintauchen, zwei Beispiele von Vorlagen von Branchenpartnern.

### Profilattribute {#attributes}

Informationen zum Transformieren der in Ihr Ziel exportierten Profilattribute finden Sie in den JSON- und Codebeispielen unten.


>[!IMPORTANT]
>
>Eine Liste aller in Adobe Experience Platform verfügbaren Profilattribute finden Sie im [XDM-Feldwörterbuch](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en).



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
>Bei allen von Ihnen verwendeten Vorlagen müssen Sie die unzulässigen Zeichen, z. B. doppelte Anführungszeichen `""`, vor dem Einfügen der Vorlage in die [Zielserverkonfiguration](./server-and-template-configuration.md#template-specs) umgehen. Weitere Informationen zum Maskieren doppelter Anführungszeichen finden Sie in Kapitel 9 des [JSON-Standards](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf).

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

### Segmentmitgliedschaft {#segment-membership}

Das XDM-Attribut [segmentMembership](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/field-dictionary.html?lang=en) informiert darüber, zu welchen Segmenten ein Profil gehört.
Lesen Sie für die drei verschiedenen Werte im Feld `status` die Dokumentation zu [Schema-Feldergruppe &quot;Segmentzugehörigkeitsdetails](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html).

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
        "status": "existing"
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
        "status": "existing"
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
>Bei allen von Ihnen verwendeten Vorlagen müssen Sie die unzulässigen Zeichen, z. B. doppelte Anführungszeichen `""`, vor dem Einfügen der Vorlage in die [Zielserverkonfiguration](./server-and-template-configuration.md#template-specs) umgehen. Weitere Informationen zum Maskieren doppelter Anführungszeichen finden Sie in Kapitel 9 des [JSON-Standards](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf).

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

Informationen zu Identitäten in Experience Platform finden Sie unter [Übersicht über Identitäts-Namespaces](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=de).

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
>Bei allen von Ihnen verwendeten Vorlagen müssen Sie die unzulässigen Zeichen, z. B. doppelte Anführungszeichen `""`, vor dem Einfügen der Vorlage in die [Zielserverkonfiguration](./server-and-template-configuration.md#template-specs) umgehen. Weitere Informationen zum Maskieren doppelter Anführungszeichen finden Sie in Kapitel 9 des [JSON-Standards](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf).

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
              "status": "existing"
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
>Bei allen von Ihnen verwendeten Vorlagen müssen Sie die unzulässigen Zeichen, z. B. doppelte Anführungszeichen `""`, vor dem Einfügen der Vorlage in die [Zielserverkonfiguration](./server-and-template-configuration.md#template-specs) umgehen. Weitere Informationen zum Maskieren doppelter Anführungszeichen finden Sie in Kapitel 9 des [JSON-Standards](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf).

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

Die nachstehende `json` stellt die aus Adobe Experience Platform exportierten Daten dar.

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
              "status": "existing"
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
>Bei allen von Ihnen verwendeten Vorlagen müssen Sie die unzulässigen Zeichen, z. B. doppelte Anführungszeichen `""`, vor dem Einfügen der Vorlage in die [Zielserverkonfiguration](./server-and-template-configuration.md#template-specs) umgehen. Weitere Informationen zum Maskieren doppelter Anführungszeichen finden Sie in Kapitel 9 des [JSON-Standards](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf).

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

Die nachstehende `json` stellt die aus Adobe Experience Platform exportierten Daten dar.

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

### Referenz: Kontext und Funktionen, die in Umwandlungsvorlagen verwendet werden

Der der Vorlage bereitgestellte Kontext enthält `input` (die Profile/Daten, die in diesen Aufruf exportiert werden) und `destination` (Daten über das Ziel, an das die Adobe Daten sendet, gültig für alle Profile).

Die nachstehende Tabelle enthält Beschreibungen der Funktionen in den obigen Beispielen.

| Funktion | Beschreibung |
|---------|----------|
| `input.profile` | Das Profil, dargestellt als [JsonNode](http://fasterxml.github.io/jackson-databind/javadoc/2.11/com/fasterxml/jackson/databind/node/JsonNodeType.html). Folgt dem weiter oben erwähnten Partner-XDM-Schema auf dieser Seite. |
| `destination.segmentAliases` | Ordnen Sie Segmentkennungen im Adobe Experience Platform-Namespace Segmentaliasen im System des Partners zu. |
| `destination.segmentNames` | Ordnen Sie Segmentnamen im Adobe Experience Platform-Namespace Segmentnamen im System des Partners zu. |
| `addedSegments(listOfSegments)` | Gibt nur die Segmente mit dem Status `realized` oder `existing` zurück. |
| `removedSegments(listOfSegments)` | Gibt nur die Segmente mit dem Status `exited` zurück. |

<!--

## What Adobe needs from you to set up your destination {#what-adobe-needs}

Based on the transformations outlined in the sections above, Adobe needs the following information to set up your destination:

* Considering *all* the fields that your platform can receive, Adobe needs the standard JSON schema that corresponds to your expected message format. Having the template allows Adobe to define transformations and to create a custom XDM schema for your company, which customers would use to export data to your destination.

-->
