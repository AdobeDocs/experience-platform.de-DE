---
keywords: Experience Platform;home;popular topics;schema;Schema;xdm;experience data model;namespace;Namespaces;Kompatibilitätsmodus;xed
solution: Experience Platform
title: Namespace im Experience-Datenmodell (XDM)
description: Erfahren Sie, wie Sie mit Namespacing im Experience-Datenmodell (XDM) Ihre Schemas erweitern und Feldkollisionen verhindern können, da verschiedene Schemakomponenten zusammengeführt werden.
exl-id: b351dfaf-5219-4750-a7a9-cf4689a5b736
source-git-commit: d26a0586a992948e1b278bae91a985fe3d9f1ee8
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 1%

---

# Namespace im Experience-Datenmodell (XDM)

>[!IMPORTANT]
>
>In XDM wird der Namespace (das Thema dieser Seite) verwendet, um Felder in einem Schema zu unterscheiden. Dies unterscheidet sich vom Konzept des Identitäts-Namespace im Identity Service, bei dem Namespace zur Unterscheidung von Identitätswerten verwendet wird. Lesen Sie die Dokumentation unter [Namespace in Identity Service](../../identity-service/features/namespaces.md) für weitere Informationen.

Alle Felder in Experience-Datenmodell (XDM)-Schemas haben einen zugehörigen Namespace. Mit diesen Namespaces können Sie Ihre Schemas erweitern und Feldkollisionen verhindern, da verschiedene Schemakomponenten zusammengeführt werden. Dieses Dokument bietet einen Überblick über Namespaces in XDM und darüber, wie sie im [Schema Registry-API](../api/overview.md).

Mithilfe von Namespacing können Sie ein Feld in einem Namespace definieren, das etwas Anderes als dasselbe Feld in einem anderen Namespace bedeutet. In der Praxis zeigt der Namespace eines Felds an, wer das Feld erstellt hat (z. B. Standard-XDM (Adobe), Anbieter oder Unternehmen).

Betrachten Sie beispielsweise ein XDM-Schema, das die [[!UICONTROL Persönliche Kontaktangaben] Feldergruppe](../field-groups/profile/demographic-details.md), die über einen Standard verfügt `mobilePhone` -Feld, das in der `xdm` Namespace. Im selben Schema können Sie auch eine separate `mobilePhone` Feld unter einem anderen Namespace (Ihre [Mandanten-ID](../api/getting-started.md#know-your-tenant_id)). Beide Felder können zusammen vorhanden sein und gleichzeitig unterschiedliche zugrunde liegende Bedeutungen oder Begrenzungen haben.

## Namespace-Syntax

Die folgenden Abschnitte zeigen, wie Namespaces in der XDM-Syntax zugewiesen werden.

### Standard-XDM {#standard}

Die standardmäßige XDM-Syntax bietet Einblicke in die Darstellung von Namespaces in Schemas (einschließlich [Übersetzungen in Adobe Experience Platform](#compatibility)).

Standard-XDM-Verwendung [JSON-LD](https://www.w3.org/TR/json-ld11/#basic-concepts) -Syntax, um Feldern Namespaces zuzuweisen. Dieser Namespace wird in Form eines URI (z. B. `https://ns.adobe.com/xdm` für die `xdm` -Namespace) oder als Shorthand-Präfix, das im `@context` -Attribut eines Schemas.

Im Folgenden finden Sie ein Beispielschema für ein Produkt mit standardmäßiger XDM-Syntax. Mit Ausnahme von `@id` (die eindeutige Kennung, wie durch die JSON-LD-Spezifikation definiert), jedes Feld unter `properties` beginnt mit einem Namespace und endet mit dem Feldnamen. Wenn Sie ein Shorthand-Präfix verwenden, das unter `@context`, werden der Namespace und der Feldname durch einen Doppelpunkt (`:`). Wenn Sie kein Präfix verwenden, werden der Namespace und der Feldname durch einen Schrägstrich (`/`).

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
| `@context` | Ein Objekt, das die Kurzschreibpräfixe definiert, die anstelle eines vollständigen Namespace-URI unter verwendet werden können. `properties`. |
| `@id` | Eine eindeutige Kennung für den Datensatz, wie durch die [JSON-LD spec](https://www.w3.org/TR/json-ld11/#node-identifiers). |
| `xdm:sku` | Ein Beispiel für ein Feld, in dem ein Namespace mit einem Shorthand-Präfix gekennzeichnet wird. In diesem Fall `xdm` ist der Namespace (`https://ns.adobe.com/xdm`) und `sku` ist der Feldname. |
| `https://ns.adobe.com/xdm/channels/application` | Ein Beispiel für ein Feld, das den vollständigen Namespace-URI verwendet. In diesem Fall `https://ns.adobe.com/xdm/channels` ist der Namespace und `application` ist der Feldname. |
| `https://ns.adobe.com/vendorA/product/stockNumber` | Felder, die von Ressourcen des Anbieters bereitgestellt werden, verwenden ihre eigenen eindeutigen Namespaces. In diesem Beispiel `https://ns.adobe.com/vendorA/product` ist der Namespace des Anbieters und `stockNumber` ist der Feldname. |
| `tenantId:internalSku` | Von Ihrem Unternehmen definierte Felder verwenden Ihre eindeutige Mandantenkennung als Namespace. In diesem Beispiel `tenantId` ist der Mandanten-Namespace (`https://ns.adobe.com/tenantId`) und `internalSku` ist der Feldname. |

{style="table-layout:auto"}

### Kompatibilitätsmodus {#compatibility}

In Adobe Experience Platform werden XDM-Schemata in [Kompatibilitätsmodus](../api/appendix.md#compatibility) -Syntax, die nicht die JSON-LD-Syntax verwendet, um Namespaces darzustellen. Stattdessen konvertiert Platform den Namespace in ein übergeordnetes Feld (beginnend mit einem Unterstrich) und verschachtelt die Felder darunter.

Beispielsweise das Standard-XDM `repo:createdDate` konvertiert in `_repo.createdDate` und würde unter der folgenden Struktur im Kompatibilitätsmodus angezeigt werden:

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

Felder, die die `xdm` Namespace erscheint als Stammfelder unter `properties` und legen Sie die `xdm:` Präfix, das in [Standard-XDM-Syntax](#standard). Beispiel: `xdm:sku` ist einfach aufgeführt als `sku` anstatt.

Die folgende JSON-Datei stellt dar, wie das oben gezeigte Beispiel der standardmäßigen XDM-Syntax in den Kompatibilitätsmodus übersetzt wird.

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

Dieses Handbuch bietet einen Überblick über XDM-Namespaces und deren Darstellung in JSON. Weitere Informationen zum Konfigurieren von XDM-Schemas mithilfe der API finden Sie unter [Handbuch zur Schema Registry-API](../api/overview.md).
