---
title: Beziehungen in der Reactor-API
description: Lernen Sie, wie Ressourcenbeziehungen in der Reactor-API hergestellt werden, einschließlich der Beziehungsanforderungen für jede Ressource.
exl-id: 23976978-a639-4eef-91b6-380a29ec1c14
source-git-commit: 7e4bc716e61b33563e0cb8059cb9f1332af7fd36
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 100%

---

# Beziehungen in der Reactor-API

Ressourcen in der Reactor-API stehen häufig in Beziehung zueinander. Dieses Dokument gibt einen Überblick darüber, wie Ressourcenbeziehungen in der API hergestellt werden und welche Anforderungen die einzelnen Ressourcentypen an die Beziehungen stellen.

Je nach Art der betreffenden Ressource sind einige Beziehungen erforderlich. Eine erforderliche Beziehung impliziert, dass die übergeordnete Ressource nicht ohne die Beziehung existieren kann. Alle anderen Beziehungen sind optional.

Unabhängig davon, ob sie erforderlich oder optional sind, werden Beziehungen entweder automatisch vom System erstellt, wenn relevante Ressourcen angelegt werden, oder sie müssen manuell erstellt werden. Beim manuellen Erstellen von Beziehungen gibt es je nach Ressource zwei mögliche Methoden:

* [Erstellen nach Payload](#payload)
* [Erstellen nach URL](#url) (nur für Bibliotheken)

Eine Liste der kompatiblen Beziehungen für jeden Ressourcentyp und gegebenenfalls die erforderlichen Methoden zur Herstellung dieser Beziehungen finden Sie im Abschnitt [Beziehungsanforderungen](#requirements).

## Erstellen einer Beziehung nach Payload {#payload}

Einige Beziehungen müssen beim erstmaligen Erstellen einer Ressource manuell eingerichtet werden. Dazu müssen Sie beim ersten Erstellen der übergeordneten Ressource ein `relationship`-Objekt in der Anfrage-Payload angeben. Beispiele für diese Beziehungen sind:

* [Erstellen eines Datenelements](../endpoints/data-elements.md#create) mit den erforderlichen Erweiterungen
* [Erstellen einer Umgebung](../endpoints/environments.md#create) mit der erforderlichen Host-Beziehung

**API-Format**

```http
POST /properties/{PROPERTY_ID}/{RESOURCE_TYPE}
```

| Parameter | Beschreibung |
| --- | --- |
| `{PROPERTY_ID}` | Die ID der Eigenschaft, zu der die Ressource gehört. |
| `{RESOURCE_TYPE}` | Die Art der zu erstellenden Ressource. |

{style="table-layout:auto"}

**Anfrage**

Die folgende Anfrage erstellt eine neue `rule_component`, die Beziehungen zu `rules` und einer `extension` herstellt.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRf606dbddfbdc44f580fc6f342b5ff9be/rule_components \
  -H 'Authorization: Bearer [TOKEN]' \
  -H 'x-api-key: [KEY]' \
  -H 'x-gw-ims-org-id: [ORG_ID]' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "delegate_descriptor_id": "kessel-test::events::click",
            "name": "My Example Click Event",
            "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":true}"
          },
          "relationships": {
            "extension": {
              "data": {
                "id": "EXa2865f4d14204fa094f247406424371b",
                "type": "extensions"
              }
            },
            "rules": {
              "data": [
                {
                  "id": "RLd53598e3f1884e63bbc8e9c95e463dcf",
                  "type": "rules"
                }
              ]
            }
          },
          "type": "rule_components"
        }
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `relationships` | Ein Objekt, das beim Anlegen von Beziehungen per Payload bereitgestellt werden muss. Jeder Schlüssel in diesem Objekt repräsentiert einen bestimmten Beziehungstyp. Im obigen Beispiel werden `extension`- und `rules`-Beziehungen hergestellt, die speziell für `rule_components` gelten. Weitere Informationen zu kompatiblen Beziehungstypen für verschiedene Ressourcen finden Sie im Abschnitt zu [Beziehungsanforderungen nach Ressource](#relationship-requirements-by-resource). |
| `data` | Jeder Beziehungstyp, der unter dem `relationship`-Objekt bereitgestellt wird, muss eine `data`-Eigenschaft enthalten, die auf die `id`- und `type`-Eigenschaft der Ressource verweist, mit der eine Beziehung hergestellt wird. Sie können eine Beziehung mit mehreren Ressourcen desselben Typs erstellen, indem Sie die `data`-Eigenschaft als Array von Objekten formatieren, wobei jedes Objekt `id` und `type` einer entsprechenden Ressource enthält. |
| `id` | Die eindeutige ID einer Ressource. Jeder `id` muss eine gleichrangige `type`-Eigenschaft hinzugefügt werden, die den Typ der betreffenden Ressource angibt. |
| `type` | Der Ressourcentyp, der durch ein gleichrangiges `id`-Feld referenziert wird. Akzeptierte Werte umfassen `data_elements`, `rules`, `extensions` und `environments`. |

{style="table-layout:auto"}

## Erstellen einer Beziehung nach URL {#url}

Im Gegensatz zu anderen Ressourcen erstellen Bibliotheken Beziehungen über ihre eigenen dedizierten `/relationship`-Endpunkte. Zu den Beispielen gehören:

* [Hinzufügen von Erweiterungen, Datenelementen und Regeln zu einer Bibliothek](../endpoints/libraries.md#add-resources)
* [Zuordnen einer Bibliothek zu einer Umgebung](../endpoints/libraries.md#environment)

**API-Format**

```http
POST /properties/{PROPERTY_ID}/libraries/{LIBRARY_ID}/relationships/{RESOURCE_TYPE}
```

| Parameter | Beschreibung |
| --- | --- |
| `{PROPERTY_ID}` | Die ID der Eigenschaft, zu der die Bibliothek gehört. |
| `{LIBRARY_ID}` | Die ID der Bibliothek, für die Sie eine Beziehung erstellen möchten. |
| `{RESOURCE_TYPE}` | Der Typ der Ressource, auf die die Beziehung abzielt. Zu den verfügbaren Werten gehören `environment`, `data_elements`, `extensions` und `rules`. |

**Anfrage**

Die folgende Anfrage verwendet den Endpunkt `/relationships/environment` für eine Bibliothek, um eine Beziehung zu einer Umgebung zu erstellen.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRf606dbddfbdc44f580fc6f342b5ff9be/libraries/LB10c1fd171cd347f19fcb8659a8d679ef/relationships/environment \
  -H 'Authorization: Bearer [TOKEN]' \
  -H 'x-api-key: [KEY]' \
  -H 'x-gw-ims-org-id: [ORG_ID]' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "id": "ENf395a477d2b24ad696d65b901055b9dc",
          "type": "environments",
        }
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `data` | Ein Objekt, das `id` und `type` der Zielressource für die Beziehung referenziert. Wenn Sie eine Beziehung mit mehreren Ressourcen desselben Typs erstellen (z. B. `extensions` und `rules`), muss die `data`-Eigenschaft als Array von Objekten formatiert sein, wobei jedes Objekt `id` und `type` einer entsprechenden Ressource enthält. |
| `id` | Die eindeutige ID einer Ressource. Jeder `id` muss eine gleichrangige `type`-Eigenschaft hinzugefügt werden, die den Typ der betreffenden Ressource angibt. |
| `type` | Der Ressourcentyp, der durch ein gleichrangiges `id`-Feld referenziert wird. Akzeptierte Werte umfassen `data_elements`, `rules`, `extensions` und `environments`. |

{style="table-layout:auto"}

## Beziehungsanforderungen nach Ressource {#requirements}

In den folgenden Tabellen werden die verfügbaren Beziehungen für jeden Ressourcentyp beschrieben, unabhängig davon, ob diese Beziehungen erforderlich sind oder nicht, und die akzeptierte Methode zum manuellen Erstellen der Beziehung, sofern zutreffend.

>[!NOTE]
>
>Wenn eine Beziehung nicht als von Payload oder URL erstellt aufgeführt wird, wird sie automatisch vom System zugewiesen.

### Audit-Ereignisse

| Beziehung | Erforderlich | Erstellen nach Payload | Erstellen nach URL |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |
| `entity` | ✓ |  |  |

{style="table-layout:auto"}

### Builds

| Beziehung | Erforderlich | Erstellen nach Payload | Erstellen nach URL |
| :--- | :---: | :---: | :---: |
| `data_elements` |  |  |  |
| `extensions` |  |  |  |
| `rules` |  |  |  |
| `environment` | ✓ |  |  |
| `library` | ✓ |  |  |
| `property` | ✓ |  |  |

{style="table-layout:auto"}

### Callbacks

| Beziehung | Erforderlich | Erstellen nach Payload | Erstellen nach URL |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |

{style="table-layout:auto"}

### Firmen

| Beziehung | Erforderlich | Erstellen nach Payload | Erstellen nach URL |
| :--- | :---: | :---: | :---: |
| `properties` |  |  |  |

{style="table-layout:auto"}

### Datenelemente

| Beziehung | Erforderlich | Erstellen nach Payload | Erstellen nach URL |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `extension` | ✓ | ✓ |  |
| `updated_with_extension` | ✓ |  |  |
| `updated_with_extension_package` | ✓ |  |  |

{style="table-layout:auto"}

### Umgebungen

| Beziehung | Erforderlich | Erstellen nach Payload | Erstellen nach URL |
| :--- | :---: | :---: | :---: |
| `library` |  |  |  |
| `builds` |  |  |  |
| `host` | ✓ | ✓ |  |
| `property` | ✓ |  |  |

{style="table-layout:auto"}

### Erweiterungen

| Beziehung | Erforderlich | Erstellen nach Payload | Erstellen nach URL |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `extension_package` | ✓ | ✓ |  |
| `updated_with_extension_package` | ✓ |  |  |

{style="table-layout:auto"}

### Hosts

| Beziehung | Erforderlich | Erstellen nach Payload | Erstellen nach URL |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |

{style="table-layout:auto"}

### Bibliotheken

| Beziehung | Erforderlich | Erstellen nach Payload | Erstellen nach URL |
| :--- | :---: | :---: | :---: |
| `builds` |  |  |  |
| `environment` |  |  | ✓ |
| `data_elements` |  |  | ✓ |
| `extensions` |  |  | ✓ |
| `rules` |  |  | ✓ |
| `notes` |  |  |  |
| `upstream_library` | ✓ |  |  |
| `property` | ✓ |  |  |
| `last_build` |  |  |  |

{style="table-layout:auto"}

### Anmerkungen

| Beziehung | Erforderlich | Erstellen nach Payload | Erstellen nach URL |
| :--- | :---: | :---: | :---: |
| `resource` | ✓ |  |  |

{style="table-layout:auto"}

### Eigenschaften

| Beziehung | Erforderlich | Erstellen nach Payload | Erstellen nach URL |
| :--- | :---: | :---: | :---: |
| `company` | ✓ |  |  |
| `callbacks` |  |  |  |
| `environments` |  |  |  |
| `libraries` |  |  |  |
| `data_elements` |  |  |  |
| `extensions` |  |  |  |
| `extensions` |  |  |  |

{style="table-layout:auto"}

### Regel Komponenten

| Beziehung | Erforderlich | Erstellen nach Payload | Erstellen nach URL |
| :--- | :---: | :---: | :---: |
| `updated_with_extensions_package` | ✓ |  |  |
| `updated_with_extension` | ✓ |  |  |
| `extension` | ✓ | ✓ |  |
| `notes` |  |  |  |
| `origin` | ✓ |  |  |
| `property` | ✓ |  |  |
| `rules` | ✓ | ✓ |  |
| `revisions` | ✓ |  |  |

{style="table-layout:auto"}

### Regeln

| Beziehung | Erforderlich | Erstellen nach Payload | Erstellen nach URL |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `rule_components` |  |  |  |

### Geheime Daten

| Beziehung | Erforderlich | Erstellen nach Payload | Erstellen nach URL |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  | ✓ |
| `environment` | ✓ | ✓ |  |

