---
title: Beziehungen in der Reactor-API
description: Erfahren Sie, wie Ressourcenbeziehungen in der Reactor-API hergestellt werden, einschließlich der Beziehungsanforderungen für jede Ressource.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 10%

---

# Beziehungen in der Reactor-API

Ressourcen in der Reactor-API sind häufig miteinander verbunden. Dieses Dokument bietet einen Überblick darüber, wie Ressourcenbeziehungen in der API hergestellt werden, und über die Beziehungsanforderungen der einzelnen Ressourcentypen.

Je nach Ressourcentyp sind einige Beziehungen erforderlich. Eine erforderliche Beziehung bedeutet, dass die übergeordnete Ressource nicht ohne die Beziehung vorhanden sein kann. Alle anderen Beziehungen sind optional.

Unabhängig davon, ob sie erforderlich oder optional sind, werden Beziehungen entweder automatisch vom System bei der Erstellung relevanter Ressourcen hergestellt oder müssen manuell erstellt werden. Bei manueller Erstellung von Beziehungen gibt es je nach Ressource zwei Möglichkeiten:

* [Erstellen nach Nutzlast](#payload)
* [Erstellen nach URL](#url)  (nur für Bibliotheken)

Eine Liste der kompatiblen Beziehungen für jeden Ressourcentyp und gegebenenfalls die erforderlichen Methoden zur Herstellung dieser Beziehungen finden Sie im Abschnitt [Beziehungsanforderungen](#requirements) .

## Erstellen einer Beziehung anhand der Payload {#payload}

Einige Beziehungen müssen bei der anfänglichen Erstellung einer Ressource manuell hergestellt werden. Dazu müssen Sie beim ersten Erstellen der übergeordneten Ressource ein `relationship` -Objekt in der Anfrage-Payload angeben. Beispiele für diese Beziehungen sind:

* [Erstellen eines Datenelements ](../endpoints/data-elements.md#create) mit den erforderlichen Erweiterungen
* [Erstellen einer ](../endpoints/environments.md#create) Umgebung mit der erforderlichen Hostbeziehung

**API-Format**

```http
POST /properties/{PROPERTY_ID}/{RESOURCE_TYPE}
```

| Parameter | Beschreibung |
| --- | --- |
| `{PROPERTY_ID}` | Die ID der Eigenschaft, zu der die Ressource gehört. |
| `{RESOURCE_TYPE}` | Der Typ der zu erstellenden Ressource. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Die folgende Anfrage erstellt ein neues `rule_component`, das Beziehungen zu `rules` und einem `extension` herstellt.

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
| `relationships` | Ein Objekt, das beim Erstellen von Beziehungen durch Payload bereitgestellt werden muss. Jeder Schlüssel in diesem Objekt stellt einen bestimmten Beziehungstyp dar. Im obigen Beispiel werden `extension` und `rules` Beziehungen hergestellt, die speziell für `rule_components` gelten. Weitere Informationen zu kompatiblen Beziehungstypen für verschiedene Ressourcen finden Sie im Abschnitt zu [Beziehungsanforderungen nach Ressource](#relationship-requirements-by-resource). |
| `data` | Jeder Beziehungstyp, der unter dem `relationship`-Objekt bereitgestellt wird, muss eine `data`-Eigenschaft enthalten, die auf die `id`- und `type`-Eigenschaft der Ressource verweist, mit der eine Beziehung hergestellt wird. Sie können eine Beziehung mit mehreren Ressourcen desselben Typs erstellen, indem Sie die `data` -Eigenschaft als Array von Objekten formatieren, wobei jedes Objekt die `id` und `type` einer entsprechenden Ressource enthält. |
| `id` | Die eindeutige Kennung einer Ressource. Jeder `id` muss eine gleichrangige `type` -Eigenschaft hinzugefügt werden, die den Typ der betreffenden Ressource angibt. |
| `type` | Der Ressourcentyp, der durch ein gleichrangiges `id` -Feld referenziert wird. Zu den zulässigen Werten gehören `data_elements`, `rules`, `extensions` und `environments`. |

{style=&quot;table-layout:auto&quot;}

## Erstellen einer Beziehung nach URL {#url}

Im Gegensatz zu anderen Ressourcen erstellen Bibliotheken Beziehungen über ihre eigenen dedizierten `/relationship`-Endpunkte. Zu den Beispielen gehören:

* [Hinzufügen von Erweiterungen, Datenelementen und Regeln zu einer Bibliothek](../endpoints/libraries.md#add-resources)
* [Zuweisen einer Bibliothek zu einer Umgebung](../endpoints/libraries.md#environment)

**API-Format**

```http
POST /properties/{PROPERTY_ID}/libraries/{LIBRARY_ID}/relationships/{RESOURCE_TYPE}
```

| Parameter | Beschreibung |
| --- | --- |
| `{PROPERTY_ID}` | Die ID der Eigenschaft, zu der die Bibliothek gehört. |
| `{LIBRARY_ID}` | Die ID der Bibliothek, für die Sie eine Beziehung erstellen möchten. |
| `{RESOURCE_TYPE}` | Der Ressourcentyp, auf den sich die Beziehung bezieht. Zu den verfügbaren Werten gehören `environment`, `data_elements`, `extensions` und `rules`. |

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
| `data` | Ein Objekt, das die `id` und `type` der Zielressource für die Beziehung referenziert. Wenn Sie eine Beziehung mit mehreren Ressourcen desselben Typs erstellen (z. B. `extensions` und `rules`), muss die `data`-Eigenschaft als Array von Objekten formatiert sein, wobei jedes Objekt die `id` und `type` einer entsprechenden Ressource enthält. |
| `id` | Die eindeutige Kennung einer Ressource. Jeder `id` muss eine gleichrangige `type` -Eigenschaft hinzugefügt werden, die den Typ der betreffenden Ressource angibt. |
| `type` | Der Ressourcentyp, der durch ein gleichrangiges `id` -Feld referenziert wird. Zu den zulässigen Werten gehören `data_elements`, `rules`, `extensions` und `environments`. |

{style=&quot;table-layout:auto&quot;}

## Beziehungsanforderungen nach Ressource {#requirements}

In den folgenden Tabellen werden die verfügbaren Beziehungen für jeden Ressourcentyp beschrieben, unabhängig davon, ob diese Beziehungen erforderlich sind oder nicht, und die akzeptierte Methode zum manuellen Erstellen der Beziehung, sofern zutreffend.

>[!NOTE]
>
>Wenn eine Beziehung nicht als von Payload oder URL erstellt aufgeführt wird, wird sie automatisch vom System zugewiesen.

### Prüfereignisse

| Beziehung | Erforderlich | Erstellen nach Nutzlast | Erstellen nach URL |
| :--- | :---: | :---: | :---: |
| `property` | verwalten |  |  |
| `entity` | verwalten |  |  |

{style=&quot;table-layout:auto&quot;}

### Builds

| Beziehung | Erforderlich | Erstellen nach Nutzlast | Erstellen nach URL |
| :--- | :---: | :---: | :---: |
| `data_elements` |  |  |  |
| `extensions` |  |  |  |
| `rules` |  |  |  |
| `environment` | verwalten |  |  |
| `library` | verwalten |  |  |
| `property` | verwalten |  |  |

{style=&quot;table-layout:auto&quot;}

### Rückrufe

| Beziehung | Erforderlich | Erstellen nach Nutzlast | Erstellen nach URL |
| :--- | :---: | :---: | :---: |
| `property` | verwalten |  |  |

{style=&quot;table-layout:auto&quot;}

### Firmen

| Beziehung | Erforderlich | Erstellen nach Nutzlast | Erstellen nach URL |
| :--- | :---: | :---: | :---: |
| `properties` |  |  |  |

{style=&quot;table-layout:auto&quot;}

### Datenelemente

| Beziehung | Erforderlich | Erstellen nach Nutzlast | Erstellen nach URL |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | verwalten |  |  |
| `notes` |  |  |  |
| `property` | verwalten |  |  |
| `origin` | verwalten |  |  |
| `extension` | verwalten | verwalten |  |
| `updated_with_extension` | verwalten |  |  |
| `updated_with_extension_package` | verwalten |  |  |

{style=&quot;table-layout:auto&quot;}

### Umgebungen

| Beziehung | Erforderlich | Erstellen nach Nutzlast | Erstellen nach URL |
| :--- | :---: | :---: | :---: |
| `library` |  |  |  |
| `builds` |  |  |  |
| `host` | verwalten | verwalten |  |
| `property` | verwalten |  |  |

{style=&quot;table-layout:auto&quot;}

### Erweiterungen

| Beziehung | Erforderlich | Erstellen nach Nutzlast | Erstellen nach URL |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | verwalten |  |  |
| `notes` |  |  |  |
| `property` | verwalten |  |  |
| `origin` | verwalten |  |  |
| `extension_package` | verwalten | verwalten |  |
| `updated_with_extension_package` | verwalten |  |  |

{style=&quot;table-layout:auto&quot;}

### Hosts

| Beziehung | Erforderlich | Erstellen nach Nutzlast | Erstellen nach URL |
| :--- | :---: | :---: | :---: |
| `property` | verwalten |  |  |

{style=&quot;table-layout:auto&quot;}

### Bibliotheken

| Beziehung | Erforderlich | Erstellen nach Nutzlast | Erstellen nach URL |
| :--- | :---: | :---: | :---: |
| `builds` |  |  |  |
| `environment` |  |  | verwalten |
| `data_elements` |  |  | verwalten |
| `extensions` |  |  | verwalten |
| `rules` |  |  | verwalten |
| `notes` |  |  |  |
| `upstream_library` | verwalten |  |  |
| `property` | verwalten |  |  |
| `last_build` |  |  |  |

{style=&quot;table-layout:auto&quot;}

### Anmerkungen

| Beziehung | Erforderlich | Erstellen nach Nutzlast | Erstellen nach URL |
| :--- | :---: | :---: | :---: |
| `resource` | verwalten |  |  |

{style=&quot;table-layout:auto&quot;}

### Eigenschaften

| Beziehung | Erforderlich | Erstellen nach Nutzlast | Erstellen nach URL |
| :--- | :---: | :---: | :---: |
| `company` | verwalten |  |  |
| `callbacks` |  |  |  |
| `environments` |  |  |  |
| `libraries` |  |  |  |
| `data_elements` |  |  |  |
| `extensions` |  |  |  |
| `extensions` |  |  |  |

{style=&quot;table-layout:auto&quot;}

### Regel Komponenten

| Beziehung | Erforderlich | Erstellen nach Nutzlast | Erstellen nach URL |
| :--- | :---: | :---: | :---: |
| `updated_with_extensions_package` | verwalten |  |  |
| `updated_with_extension` | verwalten |  |  |
| `extension` | verwalten | verwalten |  |
| `notes` |  |  |  |
| `origin` | verwalten |  |  |
| `property` | verwalten |  |  |
| `rules` | verwalten | verwalten |  |
| `revisions` | verwalten |  |  |

{style=&quot;table-layout:auto&quot;}

### Regeln

| Beziehung | Erforderlich | Erstellen nach Nutzlast | Erstellen nach URL |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | verwalten |  |  |
| `notes` |  |  |  |
| `property` | verwalten |  |  |
| `origin` | verwalten |  |  |
| `rule_components` |  |  |  |
