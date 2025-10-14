---
keywords: Experience Platform;Startseite;beliebte Themen;schema;Schema;xdm;Experience-Datenmodell;namespace;Namespaces;Kompatibilitätsmodus;xed;
solution: Experience Platform
title: Namespace im Experience-Datenmodell (XDM)
description: Erfahren Sie, wie Sie mit dem Namespace im Experience-Datenmodell (XDM) Ihre Schemata erweitern und Feldkollisionen verhindern können, wenn verschiedene Schemakomponenten zusammengeführt werden.
exl-id: b351dfaf-5219-4750-a7a9-cf4689a5b736
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 1%

---

# Namespace im Experience-Datenmodell (XDM)

>[!IMPORTANT]
>
>In XDM wird der Namespace (das Thema dieser Seite) verwendet, um Felder in einem Schema zu unterscheiden. Dies unterscheidet sich vom Konzept des Identity-Namespace in Identity Service, bei dem der Namespace zur Unterscheidung von Identitätswerten verwendet wird. Weitere Informationen finden Sie in der Dokumentation [Namespace im Identity &#x200B;](../../identity-service/features/namespaces.md)).

Alle Felder in Experience-Datenmodell (XDM)-Schemata haben einen zugehörigen Namespace. Mit diesen Namespaces können Sie Ihre Schemata erweitern und Feldkollisionen verhindern, wenn verschiedene Schemakomponenten zusammengeführt werden. Dieses Dokument bietet einen Überblick über Namespaces in XDM und darüber, wie sie in der [Schema Registry-API) dargestellt &#x200B;](../api/overview.md).

Mit dem Namespace können Sie ein Feld in einem Namespace so definieren, dass es etwas Anderes bedeutet als dasselbe Feld in einem anderen Namespace. In der Praxis zeigt der Namespace eines Felds an, wer das Feld erstellt hat (z. B. Standard-XDM (Adobe), ein Anbieter oder Ihr Unternehmen).

Nehmen wir zum Beispiel ein XDM-Schema, das die Feldergruppe [[!UICONTROL Persönliche Kontaktdaten] verwendet](../field-groups/profile/demographic-details.md) die über ein `mobilePhone` verfügt, das im `xdm`-Namespace vorhanden ist. Im selben Schema können Sie auch ein separates `mobilePhone` unter einem anderen Namespace (Ihrer [-ID) &#x200B;](../api/getting-started.md#know-your-tenant_id). Beide Felder können nebeneinander existieren, während sie unterschiedliche zugrunde liegende Bedeutungen oder Einschränkungen haben.

## Namespace-Syntax

Die folgenden Abschnitte zeigen, wie Namespaces in der XDM-Syntax zugewiesen werden.

### Standard-XDM {#standard}

Die standardmäßige XDM-Syntax zeigt in insight, wie Namespaces in Schemata dargestellt werden (einschließlich [wie sie in Adobe Experience Platform übersetzt werden](#compatibility)).

Standard-XDM verwendet [JSON-LD](https://www.w3.org/TR/json-ld11/#basic-concepts)-Syntax, um Feldern Namespaces zuzuweisen. Dieser Namespace wird in Form eines URI (z. B. `https://ns.adobe.com/xdm` für den `xdm`-Namespace) oder als Präfix bereitgestellt, das im `@context` eines Schemas konfiguriert ist.

Im Folgenden finden Sie ein Beispielschema für ein Produkt in der standardmäßigen XDM-Syntax. Mit Ausnahme von `@id` (der eindeutigen Kennung wie in der JSON-LD-Spezifikation definiert) beginnt jedes Feld unter `properties` mit einem Namespace und endet mit dem Feldnamen. Bei Verwendung eines unter `@context` definierten kurzen Präfixes werden der Namespace und der Feldname durch einen Doppelpunkt (`:`) getrennt. Wenn kein Präfix verwendet wird, werden der Namespace und der Feldname durch einen Schrägstrich (`/`) getrennt.

```json
{
  "$id": "https://ns.adobe.com/xdm/schemas/mySchema",
  "title": "Product",
  "description": "Represents the definition of a Project",
  "@context": {
    "xdm": "https://ns.adobe.com/xdm",
    "repo": "http://ns.adobe.com/adobecloud/core/1.0/",
    "schema": "http://schema.org",
    "tenantId": "https://ns.adobe.com/tenantId"
  },
  "properties": {
    "@id": {
      "type": "string"
    },
    "xdm:sku": {
      "type": "string"
    },
    "xdm:name": {
      "type": "string"
    },
    "repo:createdDate": {
      "type": "string",
      "format": "datetime"
    },
    "https://ns.adobe.com/xdm/channels/application": {
      "type": "string"
    },
    "schema:latitude": {
      "type": "number"
    },
    "https://ns.adobe.com/vendorA/product/stockNumber": {
      "type": "string"
    },
    "tenantId:internalSku": {
      "type": "number"
    }
  }
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `@context` | Ein -Objekt, das die Kurzpräfixe definiert, die anstelle eines vollständigen Namespace-URI unter `properties` verwendet werden können. |
| `@id` | Eine eindeutige Kennung für den Datensatz, wie in der [JSON-LD-Spezifikation](https://www.w3.org/TR/json-ld11/#node-identifiers) definiert. |
| `xdm:sku` | Ein Beispiel für ein Feld, das ein kurzes Präfix zur Bezeichnung eines Namespace verwendet. In diesem Fall ist `xdm` der Namespace (`https://ns.adobe.com/xdm`) und `sku` der Feldname. |
| `https://ns.adobe.com/xdm/channels/application` | Beispiel für ein Feld, das den vollständigen Namespace-URI verwendet. In diesem Fall ist `https://ns.adobe.com/xdm/channels` der Namespace und `application` der Feldname. |
| `https://ns.adobe.com/vendorA/product/stockNumber` | Felder, die von Anbieterressourcen bereitgestellt werden, verwenden ihre eigenen eindeutigen Namespaces. In diesem Beispiel ist `https://ns.adobe.com/vendorA/product` der Namespace des Anbieters und `stockNumber` der Feldname. |
| `tenantId:internalSku` | Felder, die von Ihrer Organisation definiert werden, verwenden Ihre eindeutige Mandanten-ID als Namespace. In diesem Beispiel ist `tenantId` der Mandanten-Namespace (`https://ns.adobe.com/tenantId`) und `internalSku` der Feldname. |

{style="table-layout:auto"}

### Kompatibilitätsmodus {#compatibility}

In Adobe Experience Platform werden XDM-Schemata in der Syntax [Kompatibilitätsmodus](../api/appendix.md#compatibility) dargestellt, wobei die JSON-LD-Syntax zur Darstellung von Namespaces nicht verwendet wird. Stattdessen konvertiert Experience Platform den Namespace in ein übergeordnetes Feld (beginnend mit einem Unterstrich) und verschachtelt die Felder darunter.

Beispielsweise wird das standardmäßige XDM-`repo:createdDate` in `_repo.createdDate` konvertiert und würde im Kompatibilitätsmodus unter der folgenden Struktur angezeigt:

```json
"_repo": {
  "type": "object",
  "properties": {
    "createdDate": {
      "type": "string",
      "format": "datetime"
    }
  }
}
```

Felder, die den `xdm`-Namespace verwenden, werden als Stammfelder unter `properties` angezeigt und legen das `xdm:` Präfix ab, das in der ([&#x200B; XDM-Syntax) &#x200B;](#standard) würde. Beispielsweise wird `xdm:sku` stattdessen einfach als `sku` aufgeführt.

Die folgende JSON-Datei zeigt, wie das Beispiel der Standard-XDM-Syntax oben in den Kompatibilitätsmodus übersetzt wird.

```json
{
  "$id": "https://ns.adobe.com/xdm/schemas/mySchema",
  "title": "Product",
  "description": "Represents the definition of a Project",
  "properties": {
    "_id": {
      "type": "string"
    },
    "sku": {
      "type": "string"
    },
    "name": {
      "type": "string"
    },
    "_repo": {
      "type": "object",
      "properties": {
        "createdDate": {
          "type": "string",
          "format": "datetime"
        }
      }
    },
    "_channels": {
      "type": "object",
      "properties": {
        "application": {
          "type": "string"
        }
      }
    },
    "_schema": {
      "type": "object",
      "properties": {
        "application": {
          "type": "string"
        }
      }
    },
    "_vendorA": {
      "type": "object",
      "properties": {
        "product": {
          "type": "object",
          "properties": {
            "stockNumber": {
              "type": "string"
            }
          }
        }
      }
    },
    "_tenantId": {
      "type": "object",
      "properties": {
        "internalSku": {
          "type": "number"
        }
      }
    }
  }
}
```

## Nächste Schritte

Dieses Handbuch bietet einen Überblick über XDM-Namespaces und deren Darstellung in JSON. Weitere Informationen zum Konfigurieren von XDM-Schemata mithilfe der API finden Sie im [Handbuch zur Schema Registry-API](../api/overview.md).
