---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Auflisten von Ressourcen
topic: developer guide
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 32%

---


# Auflisten von Ressourcen

Sie können eine Liste aller [!DNL Schema Registry] Ressourcen eines bestimmten Typs (Klassen, Mixins, Schema, Datentypen oder Deskriptoren) in einem Container durch eine GET-Anforderung erstellen.

>[!NOTE]
>
>Bei der Auflistung der Ressourcen werden die Ergebnisse auf 300 Elemente [!DNL Schema Registry] begrenzt. Um Ressourcen über diese Grenze hinaus zurückzugeben, müssen Sie [Seitenparameter](#paging)verwenden. Es wird außerdem empfohlen, Abfrage-Parameter zum [Filtern der Ergebnisse](#filtering) und zur Reduzierung der zurückgegebenen Ressourcen zu verwenden.

**API-Format**

```http
GET /{CONTAINER_ID}/{RESOURCE_TYPE}
GET /{CONTAINER_ID}/{RESOURCE_TYPE}?{QUERY_PARAMS}
```

| Parameter | Beschreibung |
| --- | --- |
| `{CONTAINER_ID}` | Der Container, in dem sich die Ressourcen befinden („global“oder „tenant“). |
| `{RESOURCE_TYPE}` | The type of resource to retrieve from the [!DNL Schema Library]. Valid types are `classes`, `mixins`, `schemas`, `datatypes`, and `descriptors`. |
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

Das Antwortformat hängt von der Accept-Kopfzeile ab, die in der Anfrage gesendet wird. Die folgenden Accept-Kopfzeilen stehen zur Auflistung von Ressourcen zur Verfügung:

| Accept-Kopfzeile | Beschreibung |
| ------- | ------------ |
| application/vnd.adobe.xed-id+json | Gibt eine kurze Zusammenfassung der einzelnen Ressourcen zurück. Dies ist die empfohlene Kopfzeile für die Auflistung der Ressourcen. (Maximal: 300) |
| application/vnd.adobe.xed+json | Gibt für jede Ressource das vollständige JSON-Schema zurück, einschließlich der Originale `$ref` und `allOf`. (Maximal: 300) |
| application/vnd.adobe.xdm-v2+json | Bei Verwendung des `/descriptors` Endpunkts muss dieser Accept-Header verwendet werden, um Paging-Funktionen zu nutzen. |

**Antwort**

In der obigen Anfrage wird die Accept-Kopfzeile `application/vnd.adobe.xed-id+json` verwendet. Daher enthält die Antwort lediglich die Attribute `title`, `$id`, `meta:altId` und `version` für die jeweilige Ressource. Wenn `full` als Ersatz in die Accept-Kopfzeile eingefügt wird, werden alle Attribute jeder Ressource zurückgegeben. Wählen Sie je nach den Informationen, die in Ihrer Antwort enthalten sein sollen, die geeignete Accept-Kopfzeile aus.

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

Die [!DNL Schema Registry] unterstützt die Verwendung von Abfrage-Parametern zum Anzeigen von Seiten- und Filterergebnissen bei der Auflistung von Ressourcen.

>[!NOTE]
>
>Wenn mehrere Abfrageparameter kombiniert werden, müssen diese durch Und-Zeichen (`&`) getrennt werden.

### Paging {#paging}

Zu den gebräuchlichsten Parametern für die Abfrage von Paging gehören:

| Parameter | Beschreibung |
| --- | --- |
| `start` | Geben Sie an, wo die aufgelisteten Ergebnisse beginnen sollen. Dieser Wert kann aus dem `_page.next` Attribut einer Liste-Antwort abgerufen und für den Zugriff auf die nächste Ergebnisseite verwendet werden. Wenn der `_page.next` Wert null ist, ist keine zusätzliche Seite verfügbar. |
| `limit` | Beschränken Sie die Anzahl der zurückgegebenen Ressourcen. Beispiel: `limit=5` gibt eine Liste von fünf Ressourcen zurück. |
| `orderby` | Sortieren Sie die Ergebnisse nach einer bestimmten Eigenschaft. Beispiel: `orderby=title` sortiert die Ergebnisse in aufsteigender Reihenfolge (A-Z) nach Titel. Das Hinzufügen von `-` vor dem Titel (`orderby=-title`) sortiert die Ergebnisse nach Titel in absteigender Reihenfolge (Z-A). |

### Filter {#filtering}

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

>[!TIP]
>
>Sie können den `property` Parameter verwenden, um Mixins nach ihrer kompatiblen Klasse zu filtern. For example, `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` returns only mixins that are compatible with the [!DNL XDM Individual Profile] class.
