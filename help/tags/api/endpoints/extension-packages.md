---
title: Extension packages-Endpunkt
description: Erfahren Sie, wie Sie den /extension_packages-Endpunkt in der Reactor-API aufrufen.
exl-id: a91c6f32-6c72-4118-a43f-2bd8ef50709f
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '951'
ht-degree: 100%

---

# Extension packages-Endpunkt

>[!WARNING]
>
>Die Implementierung des `/extension_packages`-Endpunkts ist im Fluss, da Funktionen hinzugefügt, entfernt und überarbeitet werden.

Ein Erweiterungspaket stellt eine [Erweiterung](./extensions.md) dar, die von einem Erweiterungsentwickler verfasst wurde. Ein Erweiterungspaket definiert zusätzliche Funktionen, die Tag-Benutzern zur Verfügung gestellt werden können. In den meisten Fällen sind diese Funktionen in Form von [Regelkomponenten](./rule-components.md) (Ereignisse, Bedingungen und Aktionen) und [Datenelementen](./data-elements.md) verfügbar, können aber auch Hauptmodule und freigegebene Module enthalten.

Erweiterungspakete werden im Erweiterungskatalog in der Datenerfassungs-Benutzeroberfläche angezeigt, sodass Benutzer sie installieren können. Das Hinzufügen eines Erweiterungspakets zu einer Eigenschaft wird erreicht, indem eine Erweiterung mit einem Link zum Erweiterungspaket erstellt wird.

Ein Erweiterungspaket gehört dem [Unternehmen](./companies.md) des Entwicklers, der es erstellt hat.

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der [Reactor-API](https://www.adobe.io/experience-platform-apis/references/reactor/). Bevor Sie fortfahren, lesen Sie zunächst das [Erste-Schritte-Handbuch](../getting-started.md), um wichtige Informationen zur Authentifizierung bei der API zu erhalten.

Sie müssen nicht nur verstehen, wie die Reactor API aufgerufen wird, sondern auch, wie die Attribute `status` und `availability` eines Erweiterungspakets beeinflussen, welche Aktionen Sie darauf durchführen können. Diese werden im Folgenden erläutert.

### Status

Erweiterungspakete haben drei potenzielle Status: `pending`, `succeeded` und `failed`.

| Status | Beschreibung |
| --- | --- |
| `pending` | Wenn ein Erweiterungspaket erstellt wird, wird sein `status` auf `pending` gesetzt. Dies bedeutet, dass das System die Informationen für das Erweiterungspaket erhalten hat und mit der Verarbeitung beginnen wird. Erweiterungspakete mit dem Status `pending` können nicht verwendet werden. |
| `succeeded` | Der Status eines Erweiterungspakets wird auf `succeeded` aktualisiert, wenn die Verarbeitung erfolgreich abgeschlossen wurde. |
| `failed` | Der Status eines Erweiterungspakets wird auf `failed` aktualisiert, wenn die Verarbeitung nicht erfolgreich abgeschlossen wurde. Ein Erweiterungspaket mit dem Status `failed` kann aktualisiert werden, bis die Verarbeitung erfolgreich ist. Erweiterungspakete mit dem Status `failed` können nicht verwendet werden. |

### Verfügbarkeit

Es gibt Verfügbarkeitsstufen für ein Erweiterungspaket: `development`, `private` und `public`.

| Verfügbarkeit | Beschreibung |
| --- | --- |
| `development` | Ein Erweiterungspaket in `development` ist nur für das Unternehmen sichtbar, das Eigentümer des Pakets ist, und nur innerhalb dieses Unternehmens verfügbar. Darüber hinaus kann es nur für Eigenschaften verwendet werden, die für die Erweiterungsentwicklung konfiguriert sind. |
| `private` | Ein `private` Erweiterungspaket ist nur für das Unternehmen sichtbar, das Eigentümer des Pakets ist, und kann nur für Eigenschaften installiert werden, die dem Unternehmen gehören. |
| `public` | Ein `public` Erweiterungspaket ist sichtbar und steht allen Unternehmen und für alle Eigenschaften zur Verfügung. |

>[!NOTE]
>
>Wenn ein Erweiterungspaket erstellt wird, wird `availability` auf `development` gesetzt. Nach Abschluss des Tests können Sie das Erweiterungspaket auf `private` oder `public` umstellen.

## Abrufen einer Liste von Erweiterungspaketen {#list}

Sie können eine Liste von Erweiterungspaketen abrufen, indem Sie eine GET-Anfrage an `/extension_packages` stellen.

**API-Format**

```http
GET /extension_packages
```

>[!NOTE]
>
>Mithilfe von Abfrageparametern können aufgelistete Erweiterungspakete anhand der folgenden Attribute gefiltert werden:<ul><li>`archive`</li><li>`created_at`</li><li>`name`</li><li>`stage`</li><li>`token`</li><li>`updated_at`</li></ul>Weitere Informationen finden Sie im Handbuch zum [Filtern von Antworten](../guides/filtering.md).

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von Erweiterungspaketen zurück.

```json
{
  "data": [
    {
      "id": "EP6860e2485de2413ea9b295d6f5321ad3",
      "type": "extension_packages",
      "attributes": {
        "actions": [

        ],
        "author": {
          "url": "http://adobe.com",
          "name": "Adobe Systems",
          "email": "reactor@adobe.com"
        },
        "availability": "development",
        "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP6860e2485de2413ea9b295d6f5321ad3",
        "conditions": [

        ],
        "configuration": null,
        "created_at": "2020-11-09T17:58:32.694Z",
        "data_elements": [

        ],
        "description": "Provides nothing.",
        "discontinued": false,
        "display_name": "Kessel Template Test",
        "events": [

        ],
        "exchange_url": null,
        "hosted_lib_files": null,
        "icon_path": "resources/icons/core.svg",
        "main": null,
        "name": "test-1604944710",
        "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
        "resources": null,
        "shared_modules": null,
        "status": "succeeded",
        "platform": "web",
        "updated_at": "2020-11-09T17:58:35.754Z",
        "version": "1.0.0",
        "view_base_path": "dist/"
      },
      "links": {
        "self": "https://reactor.adobe.io/extension_packages/EP6860e2485de2413ea9b295d6f5321ad3"
      }
    },
    {
      "id": "EP1b173c8316954e0986e5a405b4e715e3",
      "type": "extension_packages",
      "attributes": {
        "actions": [

        ],
        "author": {
          "url": "http://adobe.com",
          "name": "Adobe Systems",
          "email": "reactor@adobe.com"
        },
        "availability": "development",
        "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP1b173c8316954e0986e5a405b4e715e3",
        "conditions": [

        ],
        "configuration": null,
        "created_at": "2020-11-09T17:58:34.632Z",
        "data_elements": [

        ],
        "description": "Provides nothing.",
        "discontinued": false,
        "display_name": "Kessel Template Test",
        "events": [

        ],
        "exchange_url": null,
        "hosted_lib_files": null,
        "icon_path": "resources/icons/core.svg",
        "main": null,
        "name": "test-1604944712",
        "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
        "resources": null,
        "shared_modules": null,
        "status": "succeeded",
        "platform": "web",
        "updated_at": "2020-11-09T17:58:36.655Z",
        "version": "1.0.0",
        "view_base_path": "dist/"
      },
      "links": {
        "self": "https://reactor.adobe.io/extension_packages/EP1b173c8316954e0986e5a405b4e715e3"
      }
    },
    {
      "id": "EPb8eca81769a64af3892af5202a57ce15",
      "type": "extension_packages",
      "attributes": {
        "actions": [

        ],
        "author": {
          "url": "http://adobe.com",
          "name": "Adobe Systems",
          "email": "reactor@adobe.com"
        },
        "availability": "development",
        "cdn_path": "https://assets.adobedtm.com/staging/extensions/EPb8eca81769a64af3892af5202a57ce15",
        "conditions": [

        ],
        "configuration": null,
        "created_at": "2020-11-09T18:32:29.271Z",
        "data_elements": [

        ],
        "description": "Provides nothing.",
        "discontinued": false,
        "display_name": "Kessel Template Test",
        "events": [

        ],
        "exchange_url": null,
        "hosted_lib_files": null,
        "icon_path": "resources/icons/core.svg",
        "main": null,
        "name": "test-1604946740",
        "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
        "resources": null,
        "shared_modules": null,
        "status": "succeeded",
        "platform": "web",
        "updated_at": "2020-11-09T18:32:43.710Z",
        "version": "1.0.0",
        "view_base_path": "dist/"
      },
      "links": {
        "self": "https://reactor.adobe.io/extension_packages/EPb8eca81769a64af3892af5202a57ce15"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 3
    }
  }
}
```

## Suchen eines Erweiterungspakets {#lookup}

Sie können nach einem Erweiterungspaket suchen, indem Sie dessen ID im Pfad einer GET-Anfrage angeben.

**API-Format**

```http
GET /extension_packages/{EXTENSION_PACKAGE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | Die `id` des Erweiterungspakets, das Sie suchen möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details des Erweiterungspakets zurück, einschließlich der Delegaten-Ressourcen wie `actions`, `conditions`, `data_elements` und mehr. Die folgende Beispielantwort wurde aus Platzgründen gekürzt.

```json
{
  "data": {
    "id": "EP75db2452065b44e2b8a38ca883ce369a",
    "type": "extension_packages",
    "attributes": {
      "actions": [
        {
          "id": "kessel-test::actions::custom-code",
          "name": "custom-code",
          "schema": {
            "type": "object",
            "oneOf": [
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "global": {
                    "type": "boolean"
                  },
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "javascript"
                    ]
                  }
                },
                "additionalProperties": false
              },
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "html"
                    ]
                  }
                },
                "additionalProperties": false
              }
            ],
            "$schema": "http://json-schema.org/draft-04/schema#"
          },
          "libPath": "src/lib/actions/customCode.js",
          "viewPath": "actions/customCode.html",
          "displayName": "Custom Code"
        }
      ],
      "author": {
        "url": "http://adobe.com",
        "name": "Adobe Systems",
        "email": "reactor@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP75db2452065b44e2b8a38ca883ce369a",
      "conditions": [
        {
          "id": "kessel-test::conditions::browser",
          "name": "browser",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "browsers"
            ],
            "properties": {
              "browsers": {
                "type": "array",
                "items": {
                  "enum": [
                    "Chrome",
                    "Firefox",
                    "IE",
                    "Edge",
                    "Safari",
                    "Mobile Safari"
                  ],
                  "type": "string"
                }
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/conditions/browser.js",
          "viewPath": "conditions/browser.html",
          "displayName": "Browser",
          "categoryName": "Technology"
        }
      ],
      "configuration": null,
      "created_at": "2020-11-09T17:51:59.433Z",
      "data_elements": [
        {
          "id": "kessel-test::dataElements::cookie",
          "name": "cookie",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "name"
            ],
            "properties": {
              "name": {
                "type": "string",
                "minLength": 1
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/dataElements/cookie.js",
          "viewPath": "dataElements/cookie.html",
          "displayName": "Cookie"
        }
      ],
      "description": "Provides default event, condition, and data element types available to all tags users.",
      "discontinued": false,
      "display_name": "Kessel Test",
      "events": [
        {
          "id": "kessel-test::events::blur",
          "name": "blur",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "properties": {
              "bubbleStop": {
                "type": "boolean"
              },
              "elementSelector": {
                "type": "string",
                "minLength": 1
              },
              "elementProperties": {
                "type": "array",
                "items": {
                  "type": "object",
                  "required": [
                    "name",
                    "value"
                  ],
                  "properties": {
                    "name": {
                      "type": "string",
                      "minLength": 1
                    },
                    "value": {
                      "type": "string"
                    },
                    "valueIsRegex": {
                      "type": "boolean"
                    }
                  },
                  "additionalProperties": false
                }
              },
              "bubbleFireIfParent": {
                "type": "boolean"
              },
              "bubbleFireIfChildFired": {
                "type": "boolean"
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/events/blur.js",
          "viewPath": "events/blur.html",
          "displayName": "Blur",
          "categoryName": "Form"
        }
      ],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": null,
      "name": "kessel-test",
      "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2020-11-09T17:54:01.487Z",
      "version": "1.2.0",
      "view_base_path": "dist/"
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    }
  }
}
```

## Erstellen eines Erweiterungspakets {#create}

Erweiterungspakete werden mit einem Node.js-Strukturvorlagen-Tool erstellt und auf Ihrem lokalen Computer gespeichert, bevor sie an die Reactor-API gesendet werden. Weitere Informationen zum Konfigurieren eines Erweiterungspakets finden Sie im Handbuch [Erste Schritte bei der Erweiterungsentwicklung](../../extension-dev/getting-started.md).

Nachdem Sie die Paketdatei für die Erweiterung erstellt haben, können Sie sie über eine POST-Anfrage an die Reactor-API senden.

**API-Format**

```http
POST /extension_packages
```

**Anfrage**

Die folgende Anfrage erstellt ein neues Erweiterungspaket. Der lokale Pfad zur hochgeladenen Paketdatei wird als Formulardaten (`package`) referenziert, weshalb dieser Endpunkt einen `Content-Type`-Header von `multipart/form-data` erfordert.

```shell
curl -X POST \
  https://reactor.adobe.io/extension_packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: multipart/form-data' \
  -F 'package=@"/Users/temp/extension-package.zip"'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details des neu erstellten Erweiterungspakets zurück.

```json
{
  "data": {
    "id": "EP75db2452065b44e2b8a38ca883ce369a",
    "type": "extension_packages",
    "attributes": {
      "actions": [
        {
          "id": "kessel-test::actions::custom-code",
          "name": "custom-code",
          "schema": {
            "type": "object",
            "oneOf": [
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "global": {
                    "type": "boolean"
                  },
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "javascript"
                    ]
                  }
                },
                "additionalProperties": false
              },
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "html"
                    ]
                  }
                },
                "additionalProperties": false
              }
            ],
            "$schema": "http://json-schema.org/draft-04/schema#"
          },
          "libPath": "src/lib/actions/customCode.js",
          "viewPath": "actions/customCode.html",
          "displayName": "Custom Code"
        }
      ],
      "author": {
        "url": "http://adobe.com",
        "name": "Adobe Systems",
        "email": "reactor@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP75db2452065b44e2b8a38ca883ce369a",
      "conditions": [
        {
          "id": "kessel-test::conditions::browser",
          "name": "browser",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "browsers"
            ],
            "properties": {
              "browsers": {
                "type": "array",
                "items": {
                  "enum": [
                    "Chrome",
                    "Firefox",
                    "IE",
                    "Edge",
                    "Safari",
                    "Mobile Safari"
                  ],
                  "type": "string"
                }
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/conditions/browser.js",
          "viewPath": "conditions/browser.html",
          "displayName": "Browser",
          "categoryName": "Technology"
        }
      ],
      "configuration": null,
      "created_at": "2020-11-09T17:51:59.433Z",
      "data_elements": [
        {
          "id": "kessel-test::dataElements::cookie",
          "name": "cookie",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "name"
            ],
            "properties": {
              "name": {
                "type": "string",
                "minLength": 1
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/dataElements/cookie.js",
          "viewPath": "dataElements/cookie.html",
          "displayName": "Cookie"
        }
      ],
      "description": "Provides default event, condition, and data element types available to all tags users.",
      "discontinued": false,
      "display_name": "Kessel Test",
      "events": [
        {
          "id": "kessel-test::events::blur",
          "name": "blur",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "properties": {
              "bubbleStop": {
                "type": "boolean"
              },
              "elementSelector": {
                "type": "string",
                "minLength": 1
              },
              "elementProperties": {
                "type": "array",
                "items": {
                  "type": "object",
                  "required": [
                    "name",
                    "value"
                  ],
                  "properties": {
                    "name": {
                      "type": "string",
                      "minLength": 1
                    },
                    "value": {
                      "type": "string"
                    },
                    "valueIsRegex": {
                      "type": "boolean"
                    }
                  },
                  "additionalProperties": false
                }
              },
              "bubbleFireIfParent": {
                "type": "boolean"
              },
              "bubbleFireIfChildFired": {
                "type": "boolean"
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/events/blur.js",
          "viewPath": "events/blur.html",
          "displayName": "Blur",
          "categoryName": "Form"
        }
      ],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": null,
      "name": "kessel-test",
      "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2020-11-09T17:54:01.487Z",
      "version": "1.2.0",
      "view_base_path": "dist/"
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    }
  }
}
```

## Aktualisieren eines Erweiterungspakets {#update}

Sie können ein Erweiterungspaket aktualisieren, indem Sie seine ID in den Pfad einer PATCH-Anfrage aufnehmen.

**API-Format**

```http
PATCH /extension_packages/{EXTENSION_PACKAGE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | Die `id` des Erweiterungspakets, das Sie aktualisieren möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Wie beim [Erstellen eines Erweiterungspakets](#create) muss eine lokale Version des aktualisierten Pakets über Formulardaten hochgeladen werden.

```shell
curl -X PATCH \
  https://reactor.adobe.io/extension_packages/EP10bb503178694d73bc0cd84387b82172 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: multipart/form-data' \
  -F 'package=@"/Users/temp/extension-package.zip"'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details des aktualisierten Erweiterungspakets zurück.

```json
{
  "data": {
    "id": "EP75db2452065b44e2b8a38ca883ce369a",
    "type": "extension_packages",
    "attributes": {
      "actions": [
        {
          "id": "kessel-test::actions::custom-code",
          "name": "custom-code",
          "schema": {
            "type": "object",
            "oneOf": [
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "global": {
                    "type": "boolean"
                  },
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "javascript"
                    ]
                  }
                },
                "additionalProperties": false
              },
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "html"
                    ]
                  }
                },
                "additionalProperties": false
              }
            ],
            "$schema": "http://json-schema.org/draft-04/schema#"
          },
          "libPath": "src/lib/actions/customCode.js",
          "viewPath": "actions/customCode.html",
          "displayName": "Custom Code"
        }
      ],
      "author": {
        "url": "http://adobe.com",
        "name": "Adobe Systems",
        "email": "reactor@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP75db2452065b44e2b8a38ca883ce369a",
      "conditions": [
        {
          "id": "kessel-test::conditions::browser",
          "name": "browser",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "browsers"
            ],
            "properties": {
              "browsers": {
                "type": "array",
                "items": {
                  "enum": [
                    "Chrome",
                    "Firefox",
                    "IE",
                    "Edge",
                    "Safari",
                    "Mobile Safari"
                  ],
                  "type": "string"
                }
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/conditions/browser.js",
          "viewPath": "conditions/browser.html",
          "displayName": "Browser",
          "categoryName": "Technology"
        }
      ],
      "configuration": null,
      "created_at": "2020-11-09T17:51:59.433Z",
      "data_elements": [
        {
          "id": "kessel-test::dataElements::cookie",
          "name": "cookie",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "name"
            ],
            "properties": {
              "name": {
                "type": "string",
                "minLength": 1
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/dataElements/cookie.js",
          "viewPath": "dataElements/cookie.html",
          "displayName": "Cookie"
        }
      ],
      "description": "Provides default event, condition, and data element types available to all tags users.",
      "discontinued": false,
      "display_name": "Kessel Test",
      "events": [
        {
          "id": "kessel-test::events::blur",
          "name": "blur",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "properties": {
              "bubbleStop": {
                "type": "boolean"
              },
              "elementSelector": {
                "type": "string",
                "minLength": 1
              },
              "elementProperties": {
                "type": "array",
                "items": {
                  "type": "object",
                  "required": [
                    "name",
                    "value"
                  ],
                  "properties": {
                    "name": {
                      "type": "string",
                      "minLength": 1
                    },
                    "value": {
                      "type": "string"
                    },
                    "valueIsRegex": {
                      "type": "boolean"
                    }
                  },
                  "additionalProperties": false
                }
              },
              "bubbleFireIfParent": {
                "type": "boolean"
              },
              "bubbleFireIfChildFired": {
                "type": "boolean"
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/events/blur.js",
          "viewPath": "events/blur.html",
          "displayName": "Blur",
          "categoryName": "Form"
        }
      ],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": null,
      "name": "kessel-test",
      "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2020-11-09T17:54:01.487Z",
      "version": "1.2.0",
      "view_base_path": "dist/"
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    }
  }
}
```

## Privates Freigeben eines Erweiterungspakets {#private-release}

Nachdem Sie das Testen des Erweiterungspakets abgeschlossen haben, können Sie es privat freigeben. Dadurch wird es für alle Eigenschaften in Ihrem Unternehmen verfügbar.

Nachdem Sie die Veröffentlichung privat durchgeführt haben, können Sie den Prozess der öffentlichen Veröffentlichung starten, indem Sie das [Anfrageformular für die öffentliche Freigabe](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=7DRB5U) ausfüllen.

**API-Format**

```http
PATCH /extension_packages/{EXTENSION_PACKAGE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | Die `id` des Erweiterungspakets, das Sie privat freigeben möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Eine private Veröffentlichung wird erreicht, indem eine `action` mit dem Wert `release_private` in den `meta` der Anfragedaten bereitgestellt wird.

```shell
curl -X PATCH \
  https://reactor.adobe.io/extension_packages/EP10bb503178694d73bc0cd84387b82172 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "meta": {
            "action": "release_private"
          },
          "id": "EP27e9323eb585411fae6086fc78a3b70b",
          "type": "extension_packages"
        }
      }'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details des Erweiterungspakets zurück.

```json
{
  "data": {
    "id": "EP75db2452065b44e2b8a38ca883ce369a",
    "type": "extension_packages",
    "attributes": {
      "actions": [
        {
          "id": "kessel-test::actions::custom-code",
          "name": "custom-code",
          "schema": {
            "type": "object",
            "oneOf": [
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "global": {
                    "type": "boolean"
                  },
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "javascript"
                    ]
                  }
                },
                "additionalProperties": false
              },
              {
                "required": [
                  "language",
                  "source"
                ],
                "properties": {
                  "source": {
                    "type": "string",
                    "minLength": 1
                  },
                  "language": {
                    "enum": [
                      "html"
                    ]
                  }
                },
                "additionalProperties": false
              }
            ],
            "$schema": "http://json-schema.org/draft-04/schema#"
          },
          "libPath": "src/lib/actions/customCode.js",
          "viewPath": "actions/customCode.html",
          "displayName": "Custom Code"
        }
      ],
      "author": {
        "url": "http://adobe.com",
        "name": "Adobe Systems",
        "email": "reactor@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP75db2452065b44e2b8a38ca883ce369a",
      "conditions": [
        {
          "id": "kessel-test::conditions::browser",
          "name": "browser",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "browsers"
            ],
            "properties": {
              "browsers": {
                "type": "array",
                "items": {
                  "enum": [
                    "Chrome",
                    "Firefox",
                    "IE",
                    "Edge",
                    "Safari",
                    "Mobile Safari"
                  ],
                  "type": "string"
                }
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/conditions/browser.js",
          "viewPath": "conditions/browser.html",
          "displayName": "Browser",
          "categoryName": "Technology"
        }
      ],
      "configuration": null,
      "created_at": "2020-11-09T17:51:59.433Z",
      "data_elements": [
        {
          "id": "kessel-test::dataElements::cookie",
          "name": "cookie",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "required": [
              "name"
            ],
            "properties": {
              "name": {
                "type": "string",
                "minLength": 1
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/dataElements/cookie.js",
          "viewPath": "dataElements/cookie.html",
          "displayName": "Cookie"
        }
      ],
      "description": "Provides default event, condition, and data element types available to all tags users.",
      "discontinued": false,
      "display_name": "Kessel Test",
      "events": [
        {
          "id": "kessel-test::events::blur",
          "name": "blur",
          "schema": {
            "type": "object",
            "$schema": "http://json-schema.org/draft-04/schema#",
            "properties": {
              "bubbleStop": {
                "type": "boolean"
              },
              "elementSelector": {
                "type": "string",
                "minLength": 1
              },
              "elementProperties": {
                "type": "array",
                "items": {
                  "type": "object",
                  "required": [
                    "name",
                    "value"
                  ],
                  "properties": {
                    "name": {
                      "type": "string",
                      "minLength": 1
                    },
                    "value": {
                      "type": "string"
                    },
                    "valueIsRegex": {
                      "type": "boolean"
                    }
                  },
                  "additionalProperties": false
                }
              },
              "bubbleFireIfParent": {
                "type": "boolean"
              },
              "bubbleFireIfChildFired": {
                "type": "boolean"
              }
            },
            "additionalProperties": false
          },
          "libPath": "src/lib/events/blur.js",
          "viewPath": "events/blur.html",
          "displayName": "Blur",
          "categoryName": "Form"
        }
      ],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": null,
      "name": "kessel-test",
      "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2020-11-09T17:54:01.487Z",
      "version": "1.2.0",
      "view_base_path": "dist/"
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    }
  }
}
```

## Beenden eines Erweiterungspakets {#discontinue}

Sie können ein Erweiterungspaket beenden, indem Sie das Attribut `discontinued` über eine PATCH-Anfrage auf `true` setzen.

**API-Format**

```http
PATCH /extension_packages/{EXTENSION_PACKAGE_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | Die `id` des Erweiterungspakets, das Sie beenden möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Eine private Veröffentlichung wird erreicht, indem eine `action` mit dem Wert `release_private` in den `meta` der Anfragedaten bereitgestellt wird.

```shell
curl -X PATCH \
  https://reactor.adobe.io/extension_packages/EP10bb503178694d73bc0cd84387b82172 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "discontinued": true
          },
          "id": "EP5705a5d99aba406692e0ac666fcab160",
          "type": "extension_packages"
        }
      }'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details des Erweiterungspakets zurück.

```json
{
  "data": {
    "id": "EP5705a5d99aba406692e0ac666fcab160",
    "type": "extension_packages",
    "attributes": {
      "actions": [

      ],
      "author": {
        "url": "http://adobe.com",
        "name": "Adobe Systems",
        "email": "reactor@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP5705a5d99aba406692e0ac666fcab160",
      "conditions": [

      ],
      "configuration": null,
      "created_at": "2020-12-14T17:39:36.932Z",
      "data_elements": [

      ],
      "description": "Provides nothing.",
      "discontinued": true,
      "display_name": "Kessel Template Test",
      "events": [

      ],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": null,
      "name": "test-1607967575",
      "owner_org_id": "08364A825824E04F0A494115@AdobeOrg",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2020-12-14T17:39:43.883Z",
      "version": "1.0.0",
      "view_base_path": "dist/"
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP5705a5d99aba406692e0ac666fcab160"
    }
  }
}
```

## Auflisten der Versionen für ein Erweiterungspaket

Sie können die Versionen eines Erweiterungspakets auflisten, indem Sie `/versions` an den Pfad einer Suchanfrage anhängen.

**API-Format**

```http
GET /extension_packages/{EXTENSION_PACKAGE_ID}/versions
```

| Parameter | Beschreibung |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | Die `id` des Erweiterungspakets, dessen Versionen Sie auflisten möchten. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_packages/EP10bb503178694d73bc0cd84387b82172/versions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwort**

Eine erfolgreiche Antwort gibt ein Array früherer Versionen des Erweiterungspakets zurück. Eine Beispielantwort wurde aus Platzgründen weggelassen.
