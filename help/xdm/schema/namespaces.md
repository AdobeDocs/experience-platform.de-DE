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
>In XDM wird der Namespace (das Thema dieser Seite) verwendet, um Felder in einem Schema zu unterscheiden. Dies unterscheidet sich vom Konzept des Identitäts-Namespace im Identity Service, bei dem Namespace zur Unterscheidung von Identitätswerten verwendet wird. Weitere Informationen finden Sie in der Dokumentation zu [namespace in Identity Service](../../identity-service/features/namespaces.md) .

Alle Felder in Experience-Datenmodell (XDM)-Schemas haben einen zugehörigen Namespace. Mit diesen Namespaces können Sie Ihre Schemas erweitern und Feldkollisionen verhindern, da verschiedene Schemakomponenten zusammengeführt werden. Dieses Dokument bietet einen Überblick über Namespaces in XDM und deren Darstellung in der [Schema Registry-API](../api/overview.md).

Mithilfe von Namespacing können Sie ein Feld in einem Namespace definieren, das etwas Anderes als dasselbe Feld in einem anderen Namespace bedeutet. In der Praxis zeigt der Namespace eines Felds an, wer das Feld erstellt hat (z. B. Standard-XDM (Adobe), Anbieter oder Unternehmen).

Betrachten Sie beispielsweise ein XDM-Schema, das die Feldergruppe [[!UICONTROL Persönliche Kontaktdetails] ](../field-groups/profile/demographic-details.md) verwendet, die über ein standardmäßiges Feld `mobilePhone` verfügt, das im Namespace `xdm` vorhanden ist. Im selben Schema können Sie auch ein separates `mobilePhone` -Feld unter einem anderen Namespace erstellen (Ihre [Mandanten-ID](../api/getting-started.md#know-your-tenant_id)). Beide Felder können zusammen vorhanden sein und gleichzeitig unterschiedliche zugrunde liegende Bedeutungen oder Begrenzungen haben.

## Namespace-Syntax

Die folgenden Abschnitte zeigen, wie Namespaces in der XDM-Syntax zugewiesen werden.

### Standard-XDM {#standard}

Die standardmäßige XDM-Syntax bietet Einblicke in die Darstellung von Namespaces in Schemas (einschließlich [deren Übersetzung in Adobe Experience Platform](#compatibility)).

Standard-XDM verwendet die Syntax [JSON-LD](https://www.w3.org/TR/json-ld11/#basic-concepts) , um Feldern Namespaces zuzuweisen. Dieser Namespace wird in Form eines URI (z. B. `https://ns.adobe.com/xdm` für den Namespace `xdm`) oder als Kurzpräfix bereitgestellt, das im Attribut `@context` eines Schemas konfiguriert ist.

Im Folgenden finden Sie ein Beispielschema für ein Produkt mit standardmäßiger XDM-Syntax. Mit Ausnahme von `@id` (der eindeutigen Kennung, wie sie durch die JSON-LD-Spezifikation definiert ist) beginnt jedes Feld unter `properties` mit einem Namespace und endet mit dem Feldnamen. Wenn Sie ein Shorthand-Präfix verwenden, das unter `@context` definiert ist, werden der Namespace und der Feldname durch einen Doppelpunkt (`:`) getrennt. Wenn Sie kein Präfix verwenden, werden der Namespace und der Feldname durch einen Schrägstrich (`/`) getrennt.

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
| `@context` | Ein Objekt, das die Kurzschreibpräfixe definiert, die anstelle eines vollständigen Namespace-URI unter `properties` verwendet werden können. |
| `@id` | Eine eindeutige Kennung für den Datensatz, wie durch den [JSON-LD spec](https://www.w3.org/TR/json-ld11/#node-identifiers) definiert. |
| `xdm:sku` | Ein Beispiel für ein Feld, in dem ein Namespace mit einem Shorthand-Präfix gekennzeichnet wird. In diesem Fall ist `xdm` der Namespace (`https://ns.adobe.com/xdm`) und `sku` der Feldname. |
| `https://ns.adobe.com/xdm/channels/application` | Ein Beispiel für ein Feld, das den vollständigen Namespace-URI verwendet. In diesem Fall ist `https://ns.adobe.com/xdm/channels` der Namespace und `application` der Feldname. |
| `https://ns.adobe.com/vendorA/product/stockNumber` | Felder, die von Ressourcen des Anbieters bereitgestellt werden, verwenden ihre eigenen eindeutigen Namespaces. In diesem Beispiel ist `https://ns.adobe.com/vendorA/product` der Namespace des Anbieters und `stockNumber` der Feldname. |
| `tenantId:internalSku` | Von Ihrem Unternehmen definierte Felder verwenden Ihre eindeutige Mandantenkennung als Namespace. In diesem Beispiel ist `tenantId` der Mandanten-Namespace (`https://ns.adobe.com/tenantId`) und `internalSku` der Feldname. |

{style="table-layout:auto"}

### Kompatibilitätsmodus {#compatibility}

In Adobe Experience Platform werden XDM-Schemas in der Syntax [Kompatibilitätsmodus](../api/appendix.md#compatibility) dargestellt, die die JSON-LD-Syntax nicht zur Darstellung von Namespaces verwendet. Stattdessen konvertiert Platform den Namespace in ein übergeordnetes Feld (beginnend mit einem Unterstrich) und verschachtelt die Felder darunter.

Beispielsweise wird das Standard-XDM `repo:createdDate` in `_repo.createdDate` konvertiert und würde unter der folgenden Struktur im Kompatibilitätsmodus angezeigt:

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

Felder, die den Namespace `xdm` verwenden, werden als Stammfelder unter `properties` angezeigt und legen Sie das Präfix `xdm:` ab, das in [Standard-XDM-Syntax](#standard) angezeigt wird. Beispielsweise wird `xdm:sku` einfach als `sku` aufgeführt.

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

Dieses Handbuch bietet einen Überblick über XDM-Namespaces und deren Darstellung in JSON. Weitere Informationen zum Konfigurieren von XDM-Schemas mithilfe der API finden Sie im [Handbuch zur Schema Registry-API](../api/overview.md).
