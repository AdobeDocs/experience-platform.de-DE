---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;xdm;Erlebnisdatenmodell;Namensraum;Namensraum;Kompatibilitätsmodus;Gemischt
solution: Experience Platform
title: Benennung im Experience Data Model (XDM)
topic-legacy: overviews
description: Erfahren Sie, wie Sie mit der Benennung im Experience Data Model (XDM) Ihre Schema erweitern und Feldkollisionen verhindern können, da verschiedene Schema-Komponenten zusammengeführt werden.
source-git-commit: b4c4f8f7e428d27f389bff5591a03925b6afa6d8
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 1%

---


# Benennung im Experience Data Model (XDM)

Alle Felder im Experience Data Model (XDM)-Schema haben einen zugehörigen Namensraum. Mit diesen Namensräumen können Sie Ihre Schema erweitern und Feldkollisionen verhindern, da verschiedene Schema-Komponenten zusammengeführt werden. Dieses Dokument bietet einen Überblick über die Namensraum in
XDM und wie sie in der [Schema Registry API](../api/overview.md) dargestellt werden.

Die Benennung ermöglicht es Ihnen, ein Feld in einem Namensraum als etwas zu definieren, das sich von demselben Feld in einem anderen Namensraum unterscheidet. In der Praxis gibt der Namensraum eines Felds an, wer das Feld erstellt hat (z. B. XDM (Adobe), Anbieter oder Unternehmen).

Angenommen, ein XDM-Schema verwendet die Feldgruppe [[!UICONTROL Persönliche Kontaktdaten], die ein Standardfeld `mobilePhone` hat, das im Namensraum `xdm` vorhanden ist. ](../field-groups/profile/demographic-details.md) Im selben Schema können Sie auch ein separates `mobilePhone`-Feld unter einem anderen Namensraum erstellen (Ihre [Mandant-ID](../api/getting-started.md#know-your-tenant_id)). Beide Felder können nebeneinander bestehen, während unterschiedliche zugrunde liegende Bedeutungen oder Einschränkungen bestehen.

## Namespacesyntax

Die folgenden Abschnitte zeigen, wie Namensraum in der XDM-Syntax zugewiesen werden.

### Standard-XDM {#standard}

Die standardmäßige XDM-Syntax bietet einen Einblick, wie Namensraum in Schemas dargestellt werden (einschließlich [wie sie in Adobe Experience Platform](#compatibility) übersetzt werden).

Standard-XDM verwendet die Syntax [JSON-LD](https://json-ld.org/), um Felder Namensraum zuzuweisen. Dieser Namensraum wird in Form eines URI (z. B. `https://ns.adobe.com/xdm` für den `xdm`-Namensraum) oder als Kurzschrift-Präfix geliefert, das im `@context`-Attribut eines Schemas konfiguriert ist.

Im Folgenden finden Sie ein Schema für ein Produkt in der standardmäßigen XDM-Syntax. Mit Ausnahme von `@id` (dem eindeutigen Bezeichner gemäß der JSON-LD-Spezifikation) wird jedes Feld unter `properties` mit einem Namensraum und dem Feldnamen beendet. Wenn Sie ein unter `@context` definiertes Shorthand-Präfix verwenden, werden der Namensraum und der Feldname durch einen Doppelpunkt (`:`) getrennt. Wenn Sie kein Präfix verwenden, werden Namensraum und Feldname durch einen Schrägstrich (`/`) getrennt.

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
| `@context` | Ein Objekt, das die Shorthand-Präfixe definiert, die anstelle eines vollständigen Namensraum-URI unter `properties` verwendet werden können. |
| `@id` | Ein eindeutiger Bezeichner für den Datensatz gemäß der Definition in [JSON-LD spec](https://json-ld.org/spec/latest/json-ld/#node-identifiers). |
| `xdm:sku` | Ein Beispiel für ein Feld mit einem Shorthand-Präfix zur Bezeichnung eines Namensraums. In diesem Fall ist `xdm` der Namensraum (`https://ns.adobe.com/xdm`) und `sku` der Feldname. |
| `https://ns.adobe.com/xdm/channels/application` | Ein Beispiel für ein Feld, das den vollständigen Namensraum-URI verwendet. In diesem Fall ist `https://ns.adobe.com/xdm/channels` der Namensraum und `application` der Feldname. |
| `https://ns.adobe.com/vendorA/product/stockNumber` | Felder, die von Anbieterressourcen bereitgestellt werden, verwenden ihre eigenen eindeutigen Namensraum. In diesem Beispiel ist `https://ns.adobe.com/vendorA/product` der Anbieter-Namensraum und `stockNumber` der Feldname. |
| `tenantId:internalSku` | Die von Ihrer Organisation definierten Felder verwenden Ihre eindeutige Mandanten-ID als Namensraum. In diesem Beispiel ist `tenantId` der Pächter-Namensraum (`https://ns.adobe.com/tenantId`) und `internalSku` der Feldname. |

{style=&quot;table-layout:auto&quot;}

### Kompatibilitätsmodus {#compatibility}

In Adobe Experience Platform werden XDM-Schema in der Syntax [Kompatibilitätsmodus](../api/appendix.md#compatibility) dargestellt, die die JSON-LD-Syntax nicht zur Darstellung von Namensräumen verwendet. Stattdessen konvertiert Platform den Namensraum in ein übergeordnetes Feld (beginnend mit einem Unterstrich) und verschachtelt die darunter liegenden Felder.

Beispiel: Der Standard-XDM `repo:createdDate` wird in `_repo.createdDate` konvertiert und erscheint unter der folgenden Struktur im Kompatibilitätsmodus:

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

Felder, die den Namensraum `xdm` verwenden, werden als Stammfelder unter `properties` angezeigt und legen Sie das Präfix `xdm:` ab, das unter [Standard-XDM-Syntax](#standard) angezeigt wird. `xdm:sku` wird beispielsweise einfach als `sku` aufgeführt.

Die folgende JSON stellt dar, wie das oben gezeigte XDM-Syntaxbeispiel in den Kompatibilitätsmodus übersetzt wird.

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

Dieser Leitfaden bietet einen Überblick über XDM-Namensraum und ihre Darstellung in JSON. Weitere Informationen zum Konfigurieren von XDM-Schemas mit der API finden Sie im Handbuch [Schema Registry API guide](../api/overview.md).
