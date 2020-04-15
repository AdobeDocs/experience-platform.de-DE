---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Listen
topic: developer guide
translation-type: tm+mt
source-git-commit: fe7b6acf86ebf39da728bb091334785a24d86b49

---


# Listen

Sie können eine Liste aller Ressourcen (Schema, Klassen, Mixins oder Datentypen) in einem Container durch eine einzelne GET-Anforderung Ansicht.

**API-Format**

```http
GET /{CONTAINER_ID}/{RESOURCE_TYPE}
GET /{CONTAINER_ID}/{RESOURCE_TYPE}?{QUERY_PARAMS}
```

| Parameter | Beschreibung |
| --- | --- |
| `{CONTAINER_ID}` | Der Container, in dem sich die Ressourcen befinden (&quot;global&quot;oder &quot;mieter&quot;). |
| `{RESOURCE_TYPE}` | Der Typ der Ressource, die aus der Schema-Bibliothek abgerufen werden soll. Gültige Typen sind `datatypes`, `mixins`, `schemas`und `classes`. |
| `{QUERY_PARAMS`} | Optionale Abfrage-Parameter zum Filtern der Ergebnisse. Weitere Informationen finden Sie im Abschnitt zu den Parametern für die [Abfrage](#query) . |

**Anfrage**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/classes&limit=2 \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Das Antwortformat hängt vom Accept-Header ab, der in der Anforderung gesendet wird. Die folgenden Accept-Header stehen zur Auflistung von Ressourcen zur Verfügung:

| Kopfzeile akzeptieren | Beschreibung |
| ------- | ------------ |
| application/vnd.adobe.xed-id+json | Gibt eine kurze Zusammenfassung jeder Ressource zurück, im Allgemeinen die bevorzugte Kopfzeile für die Auflistung |
| application/vnd.adobe.xed+json | Gibt für jede Ressource das vollständige JSON-Schema zurück, wobei das Original `$ref` und `allOf` |

**Antwort**

In der obigen Anforderung wurde der Header `application/vnd.adobe.xed-id+json` &quot;Akzeptieren&quot;verwendet. Daher enthält die Antwort nur die Attribute `title`, `$id`, `meta:altId`und `version` für jede Ressource. Wenn Sie `full` in den Accept-Header wechseln, werden alle Attribute jeder Ressource zurückgegeben. Wählen Sie den entsprechenden Accept-Header je nach den Informationen, die Sie in Ihrer Antwort benötigen.

```JSON
{
  "results": [
    {
        "title": "XDM ExperienceEvent",
        "$id": "https://ns.adobe.com/xdm/context/experienceevent",
        "meta:altId": "_xdm.context.experienceevent",
        "version": "1"
    },
    {
        "title": "XDM Individual Profile",
        "$id": "https://ns.adobe.com/xdm/context/profile",
        "meta:altId": "_xdm.context.profile",
        "version": "1"
    }
  ]
}
```

## Verwenden von Abfrage-Parametern {#query}

Die Schema Registry unterstützt die Verwendung von Abfrage-Parametern zum Anzeigen von  und Filtern von Ergebnissen bei der Auflistung von Ressourcen.

>[!NOTE] Bei der Kombination mehrerer Parameter für die Abfrage müssen diese durch das kaufmännische Und (`&`) getrennt werden.

### Seite

Zu den gebräuchlichsten Parametern für die Abfrage von Paging gehören:

| Parameter | Beschreibung |
| --- | --- |
| `start` | Geben Sie an, wo die aufgelisteten Ergebnisse angezeigt werden sollen. Beispiel: Die Liste `start=2` resultiert aus dem dritten zurückgegebenen Element. |
| `limit` | Schränken Sie die Anzahl der zurückgegebenen Ressourcen ein. Beispiel: `limit=5` gibt eine Liste von fünf Mitteln zurück. |
| `orderby` | Sortieren Sie die Ergebnisse nach einer bestimmten Eigenschaft. Beispiel: Die Ergebnisse `orderby=title` werden in aufsteigender Reihenfolge (A-Z) nach Titel sortiert. Durch Hinzufügen eines `-` Vor-Titels (`orderby=-title`) werden Elemente in absteigender Reihenfolge nach Titel sortiert (Z-A). |

### Filter

Sie können die Ergebnisse mithilfe des `property` Parameters filtern, der verwendet wird, um einen bestimmten Operator auf eine bestimmte JSON-Eigenschaft in den abgerufenen Ressourcen anzuwenden. Zu den unterstützten Operatoren gehören:

| Operator | Beschreibung | Beispiel |
| --- | --- | --- |
| `==` | Filter, ob die Eigenschaft dem bereitgestellten Wert entspricht. | `property=title==test` |
| `!=` | Filter, ob die Eigenschaft nicht mit dem bereitgestellten Wert übereinstimmt. | `property=title!=test` |
| `<` | Filter, ob die Eigenschaft kleiner als der angegebene Wert ist. | `property=version<5` |
| `>` | Filter, ob die Eigenschaft größer als der angegebene Wert ist. | `property=version>5` |
| `<=` | Filter, ob die Eigenschaft kleiner als oder gleich dem bereitgestellten Wert ist. | `property=version<=5` |
| `>=` | Filter, ob die Eigenschaft größer oder gleich dem bereitgestellten Wert ist. | `property=version>=5` |
| `~` | Filter, ob die Eigenschaft mit einem bereitgestellten regulären Ausdruck übereinstimmt. | `property=title~test$` |
| (Keine) | Wenn nur der Eigenschaftsname angegeben wird, werden nur Einträge zurückgegeben, bei denen die Eigenschaft vorhanden ist. | `property=title` |

>[!TIP] Sie können den `property` Parameter verwenden, um Mixins nach ihrer kompatiblen Klasse zu filtern. Gibt beispielsweise `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` nur Mixins zurück, die mit der XDM Individual Profil-Klasse kompatibel sind.
