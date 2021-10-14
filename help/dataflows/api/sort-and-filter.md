---
title: Sortieren und Filtern von Antworten in der Flow Service-API
description: In diesem Tutorial wird die Syntax für das Sortieren und Filtern mithilfe von Abfrageparametern in der Flow Service-API behandelt, einschließlich einiger erweiterter Anwendungsfälle.
source-git-commit: ccca81357bd7d7083abd3f395aa547c85ebf65fd
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 7%

---

# Sortieren und Filtern von Antworten in der Flow Service-API

Bei der Ausführung von Auflistungsanforderungen (GET) in der [Flow Service-API](https://www.adobe.io/experience-platform-apis/references/flow-service/) können Sie Abfrageparameter verwenden, um Antworten zu sortieren und zu filtern. Dieses Handbuch enthält eine Referenz zur Verwendung dieser Parameter für verschiedene Anwendungsfälle.

## Sortieren

Sie können Antworten mithilfe eines `orderby`-Abfrageparameters sortieren. Die folgenden Ressourcen können in der API sortiert werden:

* [Verbindungen](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Connections)
* [Quellverbindungen](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Source-connections)
* [Zielverbindungen](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Target-connections)
* [Flüsse](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Flows)
* [Ausführungen](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Runs)

Um den Parameter zu verwenden, müssen Sie seinen Wert auf die spezifische Eigenschaft festlegen, nach der Sie sortieren möchten (z. B. `?orderby=name`). Sie können dem Wert ein Pluszeichen (`+`) für aufsteigende Reihenfolge oder ein Minuszeichen (`-`) für absteigende Reihenfolge voranstellen. Wenn kein Bestellpräfix angegeben wird, wird die Liste standardmäßig in aufsteigender Reihenfolge sortiert.

```http
GET /flows?orderby=name
GET /flows?orderby=-name
```

Sie können einen Sortierparameter auch mit einem Filterparameter kombinieren, indem Sie ein &quot;Und&quot;-Symbol (`&`) verwenden.

```http
GET /flows?property=state==enabled&orderby=createdAt
```

## Filtern

Sie können Antworten filtern, indem Sie einen `property`-Parameter mit einem Schlüssel-Wert-Ausdruck verwenden. Beispielsweise gibt `?property=id==12345` nur Ressourcen zurück, deren `id`-Eigenschaft genau `12345` entspricht.

Die Filterung kann im Allgemeinen auf jede Eigenschaft in einer Entität angewendet werden, solange der gültige Pfad zu dieser Eigenschaft bekannt ist.

>[!NOTE]
>
>Wenn eine Eigenschaft in einem Array-Element verschachtelt ist, müssen Sie eckige Klammern (`[]`) an das Array im Pfad anhängen. Beispiele finden Sie im Abschnitt [Filtern nach Array-Eigenschaften](#arrays) .

**Gibt alle Quellverbindungen zurück, bei denen der Name der Quelltabelle  `lead`lautet:**

```http
GET /sourceConnections?property=params.tableName==lead
```

**Gibt alle Flüsse für eine bestimmte Segment-ID zurück:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

### Filter kombinieren

Mehrere `property`-Filter können in eine Abfrage einbezogen werden, vorausgesetzt sie werden durch die Zeichen &quot;und&quot;(`&`) getrennt. Beim Kombinieren von Filtern wird von einer UND-Beziehung ausgegangen. Das bedeutet, dass eine Entität alle Filter erfüllen muss, damit sie in die Antwort aufgenommen wird.

**Gibt alle aktivierten Flüsse für eine Segment-ID zurück:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a&property=state==enabled
```

### Filtern nach Array-Eigenschaften {#arrays}

Sie können nach den Eigenschaften von Elementen in Arrays filtern, indem Sie `[]` an den Namen der Array-Eigenschaft anhängen.

**Rückkehrflüsse, die bestimmten Quellverbindungen zugeordnet sind:**

```http
GET /flows?property=sourceConnectionIds[]==9874984,6980696
```

**Rückkehrflüsse mit einer Transformation, die eine bestimmte Selektorwert-ID enthält:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

**Gibt Quellverbindungen zurück, die eine Spalte mit einem bestimmten  `name` Wert aufweisen:**

```http
GET /sourceConnections?property=params.columns[].name==firstName
```

**Suchen Sie nach der Flusslaufs-ID für ein Ziel, indem Sie nach Segment-ID filtern:**

```http
GET /runs?property=metrics.recordSummary.targetSummaries[].entitySummaries[].id==segment:068d6e2c-b546-4c73-bfb7-9a9d33375659
```

### `count`

Jede Filterabfrage kann mit dem Abfrageparameter `count` mit dem Wert `true` angehängt werden, um die Anzahl der Ergebnisse zurückzugeben. Die API-Antwort enthält eine `count` -Eigenschaft, deren Wert die Anzahl der insgesamt gefilterten Elemente darstellt. Die tatsächlichen gefilterten Elemente werden in diesem Aufruf nicht zurückgegeben.

**Gibt die Anzahl der aktivierten Flüsse im System zurück:**

```http
GET /flows?property=state==enabled&count=true
```

Die Antwort auf die obige Abfrage würde wie folgt aussehen:

```json
{
  "count": 95
}
```

### Gefilterte Eigenschaften nach Ressource

Je nachdem, welche Flow Service-Entität Sie abrufen, können für die Filterung verschiedene Eigenschaften verwendet werden. Die folgenden Tabellen enthalten die Felder der Stammebene für jede Ressource, die häufig bei der Filterung von Anwendungsfällen verwendet wird.

**`connectionSpec`**

| Eigenschaft | Beispiel |
| --- | --- |
| `id` | `/connectionSpecs?property=id==736873,9485095` |
| `name` | `/connectionSpecs?property=name==TestConn` |
| `providerId` | `/connectionSpecs?property=providerId==3897933` |
| `attributes.{ATTRIBUTE_NAME}` | `/connectionSpecs?property=attributes.sampleAttribute="abc"` |

{style=&quot;table-layout:auto&quot;}

**`flowSpec`**

| Eigenschaft | Beispiel |
| --- | --- |
| `id` | `/flowSpecs?property=id==736873,9485095` |
| `name` | `/flowSpecs?property=name==TestConn` |
| `providerId` | `/flowSpecs?property=providerId==3897933` |

{style=&quot;table-layout:auto&quot;}

**`connection`**

| Eigenschaft | Beispiel |
| --- | --- |
| `id` | `/connections?property=id==736873,9485095` |
| `name` | `/connections?property=name==TestConn` |
| `description` | `/connections?property=description==Test%20description` |
| `connectionSpec.id` | `/connections?property=connectionSpec.id==938903,849048` |
| `state` | `/connections?property=state==enabled` |

{style=&quot;table-layout:auto&quot;}

**`sourceConnection`**

| Eigenschaft | Beispiel |
| --- | --- |
| `id` | `/sourceConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/sourceConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/sourceConnections?property=baseConnectionId==983908,4908095` |

{style=&quot;table-layout:auto&quot;}

**`targetConnection`**

| Eigenschaft | Beispiel |
| --- | --- |
| `id` | `/targetConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/targetConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/targetConnections?property=baseConnectionId==983908,4908095` |

{style=&quot;table-layout:auto&quot;}

**`flow`**

| Eigenschaft | Beispiel |
| --- | --- |
| `id` | `/flows?property=id==736873,9485095` |
| `name` | `/flows?property=name==TestFlow` |
| `description` | `/flows?property=description==Test%20description` |
| `flowSpec.id` | `/flows?property=flowSpec.id==938903,849048` |
| `state` | `/flows?property=state==enabled` |
| `sourceConnectionIds` | `/flows?property=sourceConnectionIds[]==9874984,6980696` |
| `targetConnectionIds` | `/flows?property=targetConnectionIds[]==598590,690666` |

{style=&quot;table-layout:auto&quot;}

**`run`**

| Eigenschaft | Beispiel |
| --- | --- |
| `id` | `/runs?property=id==736873,9485095` |
| `flowId` | `/runs?property=flowId==8749844` |
| `state` | `/runs?property=state==inProgress` |

{style=&quot;table-layout:auto&quot;}

## Nächste Schritte

In diesem Handbuch wurde die Verwendung der Abfrageparameter `orderby` und `property` zum Sortieren und Filtern von Antworten in der Flow Service-API beschrieben. Eine schrittweise Anleitung zur Verwendung der API für allgemeine Workflows in Platform finden Sie in den API-Tutorials in der Dokumentation [sources](../../sources/home.md) und [destinations](../../destinations/home.md) .
