---
title: Search-Endpunkt
description: Erfahren Sie, wie Sie den /search-Endpunkt in der Reactor-API aufrufen.
exl-id: 14eb8d8a-3b42-42f3-be87-f39e16d616f4
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 100%

---

# Search-Endpunkt

Der `/search`-Endpunkt in der Reactor-API bietet eine Möglichkeit, Ressourcen zu finden, die den gewünschten Kriterien entsprechen, ausgedrückt als Abfrage.

Die folgenden Typen von API-Ressourcen sind durchsuchbar und verwenden dieselbe Datenstruktur wie die ressourcenbasierten Dokumente, die über die API zurückgegeben werden:

* `audit_events`
* `builds`
* `callbacks`
* `data_elements`
* `environments`
* `extension_packages`
* `extensions`
* `hosts`
* `libraries`
* `properties`
* `rule_components`
* `rules`

Alle Abfragen sind auf Ihre aktuelle Firma und die zugänglichen Eigenschaften beschränkt.

>[!IMPORTANT]
>
>Die Suchfunktion hat die folgenden Einschränkungen und Ausnahmen:
>* Meta ist nicht durchsuchbar und wird nicht in den Suchergebnissen zurückgegeben.
>* Schemafelder für Delegaten von Erweiterungspaketen (Aktionen, Bedingungen usw.) sind als Text durchsuchbar, nicht als verschachtelte Datenstruktur.
>* Bereichsabfragen unterstützen derzeit nur Ganzzahlen.


Ausführlichere Informationen zur Verwendung dieser Funktion finden Sie im [Suchleitfaden](../guides/search.md).

## Erste Schritte

Der in diesem Handbuch verwendete Endpunkt ist Teil der [Reactor-API](https://www.adobe.io/experience-platform-apis/references/reactor/). Bevor Sie fortfahren, lesen Sie zunächst das [Erste-Schritte-Handbuch](../getting-started.md), um wichtige Informationen zur Authentifizierung bei der API zu erhalten.

## Durchführen einer Suche {#perform}

Sie können eine Suche durchführen, indem Sie eine POST-Anfrage stellen.

**API-Format**

```http
POST /search
```

**Anfrage**

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "from": 0,
          "size": 25,
          "query": {
            "attributes.name": {
              "value": "Performance"
            },
            "attributes.revision_number": {
              "range": {
                "lte": "2",
                "gt": "0"
              }
            }
          },
          "sort": [
            {
              "attributes.revision_number": "desc"
            }
          ],
          "resource_types": [
            "data_elements",
            "rule_components"
          ]
        }
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `from` | Die Anzahl der Ergebnisse, um die die Antwort verschoben werden soll. |
| `size` | Die maximale Anzahl an zurückzugebenden Ergebnissen. Die Ergebnisse dürfen 100 Elemente nicht überschreiten. |
| `query` | Ein Objekt, das die Suchabfrage darstellt. Für jede Eigenschaft in diesem Objekt muss der Schlüssel einen Feldpfad für die Abfrage darstellen und der Wert muss ein Objekt sein, dessen Untereigenschaften bestimmen, wonach abgefragt werden soll.<br><br>Für jeden Feldpfad können Sie die folgenden Untereigenschaften verwenden:<ul><li>`exists`: Gibt „true“ zurück, wenn das Feld in der Ressource vorhanden ist.</li><li>`value`: Gibt „true“ zurück, wenn der Wert des Felds mit dem Wert dieser Eigenschaft übereinstimmt.</li><li>`value_operator`: Boolesche Logik, die verwendet wird, um zu bestimmen, wie eine `value`-Abfrage verarbeitet werden soll. Die zulässigen Werte sind `AND` und `OR`. Wenn diese Option ausgeschlossen ist, wird von der Logik `AND` ausgegangen. Weitere Informationen finden Sie im Abschnitt [Wertoperator-Logik](#value-operator).</li><li>`range` Gibt „true“ zurück, wenn der Wert des Felds in einen bestimmten numerischen Bereich fällt. Der Bereich selbst wird durch die folgenden Untereigenschaften bestimmt:<ul><li>`gt`: Größer als der angegebene Wert, nicht gleich.</li><li>`gte`: Größer oder gleich dem angegebenen Wert.</li><li>`lt`: Kleiner als der angegebene Wert, nicht gleich.</li><li>`lte`: Kleiner oder gleich dem angegebenen Wert.</li></ul></li></ul> |
| `sort` | Ein Array von Objekten, das die Reihenfolge angibt, in der Ergebnisse sortiert werden sollen. Jedes Objekt muss eine einzelne Eigenschaft enthalten: Der Schlüssel stellt den Feldpfad dar, nach dem sortiert werden soll, und der Wert stellt die Sortierreihenfolge (`asc` für aufsteigende, `desc` für absteigende Werte) dar. |
| `resource_types` | Ein Array von Zeichenfolgen, die die zu suchenden Ressourcentypen angeben. |

{style=&quot;table-layout:auto&quot;}

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste mit übereinstimmenden Ressourcen für die Abfrage zurück. Weitere Informationen dazu, wie die API Übereinstimmungen für bestimmte Werte ermittelt, finden Sie im Anhang zu [Konventionen zum Abgleichen](#conventions).

```json
{
  "data": [
    {
      "id": "DE5d11b3ed301d4ce99b530a5121e392b2",
      "type": "data_elements",
      "attributes": {
        "created_at": "2020-12-14T17:36:09.045Z",
        "deleted_at": null,
        "dirty": true,
        "enabled": true,
        "name": "Performance Indicator",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:36:09.045Z",
        "clean_text": false,
        "default_value": null,
        "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
        "force_lower_case": false,
        "review_status": "unsubmitted",
        "storage_duration": null,
        "settings": "{\"elementProperty\":\"html\",\"elementSelector\":\".target-element\"}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/property"
          },
          "data": {
            "id": "PR97d92a379a5f48758947cdf44f607a0d",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/origin"
          },
          "data": {
            "id": "DE5d11b3ed301d4ce99b530a5121e392b2",
            "type": "data_elements"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/extension"
          },
          "data": {
            "id": "EX0348d463358c4c89afe726245576f112",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/updated_with_extension"
          },
          "data": {
            "id": "EX1cc78b39339242da82a0e0752fa53375",
            "type": "extensions"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d",
        "origin": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2",
        "self": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2",
        "extension": "https://reactor.adobe.io/extensions/EX0348d463358c4c89afe726245576f112"
      },
      "meta": {
        "latest_revision_number": 1
      }
    }
  ],
  "meta": {
    "total_hits": 1
  }
}
```

## Anhang

Der folgende Abschnitt enthält zusätzliche Informationen zur Verwendung des `/search`-Endpunkts.

### Wertoperator-Logik {#value-operator}

Suchabfragewerte werden in Begriffe aufgeteilt, damit sie mit indizierten Dokumenten abgeglichen werden können. Zwischen jedem Begriff wird eine `AND`-Beziehung angenommen.

Bei Verwendung von `AND` als `value_operator` wird der Abfragewert `My Rule Holiday Sale` als Dokumente mit einem Feld interpretiert, das `My AND Rule AND Holiday AND Sale` enthält.

Bei Verwendung von `OR` als `value_operator` wird der Abfragewert `My Rule Holiday Sale` als Dokumente mit einem Feld interpretiert, das `My OR Rule OR Holiday OR Sale` enthält. Je mehr Begriffe übereinstimmen, desto höher ist der `match_score`. Wenn aufgrund der Art der teilweisen Zuordnung nichts dem gewünschten Wert entspricht, können Sie eine Ergebnismenge abrufen, bei der der Wert nur auf einem sehr einfachen Niveau übereinstimmt, z. B. nur einige Textzeichen.

### Konventionen für den Abgleich {#conventions}

Bei einer Suche geht es um die Beantwortung der Frage, wie relevant ein Dokument für eine Abfrage ist. Die Art und Weise, wie Dokumentdaten analysiert und indiziert werden, wirkt sich direkt darauf aus.

In der folgenden Tabelle werden die Konventionen für den Abgleich für allgemeine Feldtypen aufgeschlüsselt:

| Feldtyp | Konventionen für den Abgleich |
| --- | --- |
| Zeichenfolgen | Text mit partieller Begriffsanalyse, ohne Unterscheidung zwischen Groß- und Kleinschreibung |
| Enum-Werte | Exakte Übereinstimmung unter Berücksichtigung von Groß- und Kleinschreibung |
| Ganzzahlen | Exakte Übereinstimmung |
| Fließkommazahlen | Exakte Übereinstimmung |
| Zeitstempel | Exakte Übereinstimmung (DateTime-Format) |
| Anzeigenamen | Text mit partieller Begriffsanalyse, ohne Unterscheidung zwischen Groß- und Kleinschreibung |

Es gibt zusätzliche Konventionen für bestimmte Felder, die in der API angezeigt werden:

| Feld | Konventionen für den Abgleich |
| --- | --- |
| `id` | Exakte Übereinstimmung unter Berücksichtigung von Groß- und Kleinschreibung |
| `delegate_descriptor_id` | Exakte Übereinstimmung unter Berücksichtigung von Groß- und Kleinschreibung, wobei die Begriffe mit `::` aufgeteilt sind |
| `name` | Exakte Übereinstimmung unter Berücksichtigung von Groß- und Kleinschreibung |
| `settings` | Text mit partieller Begriffsanalyse, ohne Unterscheidung zwischen Groß- und Kleinschreibung |
| `type` | Exakte Übereinstimmung unter Berücksichtigung von Groß- und Kleinschreibung |
