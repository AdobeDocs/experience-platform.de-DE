---
title: Sortieren und Filtern von Antworten in der Flow Service-API
description: In diesem Tutorial wird die Syntax für das Sortieren und Filtern mithilfe von Abfrageparametern in der Flow Service-API behandelt, einschließlich einiger erweiterter Anwendungsfälle.
exl-id: 029c3199-946e-4f89-ba7a-dac50cc40c09
source-git-commit: c7ff379b260edeef03f8b47f932ce9040eef3be2
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 3%

---

# Sortieren und Filtern von Antworten in der Flow Service-API

Beim Ausführen von Auflistungsanforderungen (GET) im [Flussdienst-API](https://www.adobe.io/experience-platform-apis/references/flow-service/)können Sie Abfrageparameter verwenden, um Antworten zu sortieren und zu filtern. Dieses Handbuch enthält eine Referenz zur Verwendung dieser Parameter für verschiedene Anwendungsfälle.

## Sortieren

Sie können Antworten mithilfe einer `orderby` Abfrageparameter. Die folgenden Ressourcen können in der API sortiert werden:

* [Verbindungen](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Connections)
* [Quellverbindungen](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Source-connections)
* [Zielverbindungen](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Target-connections)
* [Flüsse](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Flows)
* [Ausführungen](https://www.adobe.io/experience-platform-apis/references/flow-service/#tag/Runs)

Um den Parameter zu verwenden, müssen Sie seinen Wert auf die spezifische Eigenschaft festlegen, nach der Sie sortieren möchten (z. B. `?orderby=name`). Sie können dem Wert ein Pluszeichen (`+`) für aufsteigende Reihenfolge oder Minuszeichen (`-`) in absteigender Reihenfolge. Wenn kein Bestellpräfix angegeben wird, wird die Liste standardmäßig in aufsteigender Reihenfolge sortiert.

```http
GET /flows?orderby=name
GET /flows?orderby=-name
```

Sie können einen Sortierparameter auch mit einem Filterparameter kombinieren, indem Sie ein &quot;Und&quot;-Symbol (`&`).

```http
GET /flows?property=state==enabled&orderby=createdAt
```

## Filtern

Sie können Antworten mithilfe eines `property` -Parameter mit einem Schlüssel-Wert-Ausdruck. Beispiel: `?property=id==12345` gibt nur Ressourcen zurück, die `id` Eigenschaft genau gleich `12345`.

Die Filterung kann im Allgemeinen auf jede Eigenschaft in einer Entität angewendet werden, solange der gültige Pfad zu dieser Eigenschaft bekannt ist.

>[!NOTE]
>
>Wenn eine Eigenschaft in einem Array-Element verschachtelt ist, müssen Sie eckige Klammern (`[]`) zum Array im Pfad hinzu. Siehe Abschnitt zu [Filtern nach Array-Eigenschaften](#arrays) für Beispiele.

**Gibt alle Quellverbindungen zurück, bei denen der Name der Quelltabelle lautet `lead`:**

```http
GET /sourceConnections?property=params.tableName==lead
```

**Gibt alle Flüsse für eine bestimmte Segment-ID zurück:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

### Filter kombinieren

Mehrere `property` Filter können in eine Abfrage einbezogen werden, sofern sie durch &quot;und&quot;-Zeichen (`&`). Beim Kombinieren von Filtern wird von einer UND-Beziehung ausgegangen. Das bedeutet, dass eine Entität alle Filter erfüllen muss, damit sie in die Antwort aufgenommen wird.

**Gibt alle aktivierten Flüsse für eine Segment-ID zurück:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a&property=state==enabled
```

### Filtern nach Array-Eigenschaften {#arrays}

Sie können nach den Eigenschaften von Elementen in Arrays filtern, indem Sie `[]` zum Namen der Array-Eigenschaft.

**Rückkehrflüsse, die bestimmten Quellverbindungen zugeordnet sind:**

```http
GET /flows?property=sourceConnectionIds[]==9874984,6980696
```

**Rückkehrflüsse mit einer Transformation, die eine bestimmte Selektorwert-ID enthält:**

```http
GET /flows?property=transformations[].params.segmentSelectors.selectors[].value.id==5722a16f-5e1f-4732-91b6-3b03943f759a
```

**Quellverbindungen zurückgeben, die eine Spalte mit einer bestimmten `name` Wert:**

```http
GET /sourceConnections?property=params.columns[].name==firstName
```

**Suchen Sie nach der Flusslaufs-ID für ein Ziel, indem Sie nach Segment-ID filtern:**

```http
GET /runs?property=metrics.recordSummary.targetSummaries[].entitySummaries[].id==segment:068d6e2c-b546-4c73-bfb7-9a9d33375659
```

### `count`

Jede Filterabfrage kann mit `count` Abfrageparameter mit dem Wert `true` , um die Anzahl der Ergebnisse zurückzugeben. Die API-Antwort enthält eine `count` -Eigenschaft, deren Wert die Anzahl der insgesamt gefilterten Elemente darstellt. Die tatsächlichen gefilterten Elemente werden in diesem Aufruf nicht zurückgegeben.

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

{style="table-layout:auto"}

**`flowSpec`**

| Eigenschaft | Beispiel |
| --- | --- |
| `id` | `/flowSpecs?property=id==736873,9485095` |
| `name` | `/flowSpecs?property=name==TestConn` |
| `providerId` | `/flowSpecs?property=providerId==3897933` |

{style="table-layout:auto"}

**`connection`**

| Eigenschaft | Beispiel |
| --- | --- |
| `id` | `/connections?property=id==736873,9485095` |
| `name` | `/connections?property=name==TestConn` |
| `description` | `/connections?property=description==Test%20description` |
| `connectionSpec.id` | `/connections?property=connectionSpec.id==938903,849048` |
| `state` | `/connections?property=state==enabled` |

{style="table-layout:auto"}

**`sourceConnection`**

| Eigenschaft | Beispiel |
| --- | --- |
| `id` | `/sourceConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/sourceConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/sourceConnections?property=baseConnectionId==983908,4908095` |

{style="table-layout:auto"}

**`targetConnection`**

| Eigenschaft | Beispiel |
| --- | --- |
| `id` | `/targetConnections?property=id==736873,9485095` |
| `connectionSpec.id` | `/targetConnections?property=connectionSpec.id==938903,849048` |
| `baseConnectionId` | `/targetConnections?property=baseConnectionId==983908,4908095` |

{style="table-layout:auto"}

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

{style="table-layout:auto"}

**`run`**

| Eigenschaft | Beispiel |
| --- | --- |
| `id` | `/runs?property=id==736873,9485095` |
| `flowId` | `/runs?property=flowId==8749844` |
| `state` | `/runs?property=state==inProgress` |

{style="table-layout:auto"}

## Anwendungsfälle {#use-cases}

In diesem Abschnitt finden Sie einige spezifische Beispiele dafür, wie Sie mit Filtern und Sortieren Informationen zu bestimmten Connectoren zurückgeben oder Probleme beheben können. Wenn Sie weitere Anwendungsfälle zum Adobe hinzufügen möchten, verwenden Sie bitte die **[!UICONTROL Detaillierte Feedback-Optionen]** auf der Seite, um eine Anfrage zu senden.

**Filtern, um nur Verbindungen zu einem bestimmten Ziel zurückzugeben**

Sie können Filter verwenden, um nur Verbindungen zu bestimmten Zielen zurückzugeben. Abfragen der `connectionSpecs` Endpunkt wie unten:

```http
GET /connectionSpecs
```

Suchen Sie dann nach Ihrer gewünschten `connectionSpec` durch Kontrolle der `name` -Parameter. Suchen Sie beispielsweise nach Amazon Ads, Pega oder SFTP usw. im `name` -Parameter. Die entsprechende `id` ist die `connectionSpec` , nach dem Sie im nächsten API-Aufruf suchen können.

Filtern Sie beispielsweise Ihre Ziele so, dass nur vorhandene Verbindungen zu Amazon S3-Verbindungen zurückgegeben werden:

```http
GET /connections?property=connectionSpec.id==4890fc95-5a1f-4983-94bb-e060c08e3f81
```

**Filtern, um nur Datenflüsse an Ziele zurückzugeben**

Bei der Abfrage des `/flows` -Endpunkt verwenden, können Sie einen Filter verwenden, um nicht alle Datenflüsse für Quellen und Ziele zurückzugeben, sondern nur Datenflüsse an Ziele. Verwenden Sie dazu `isDestinationFlow` als Abfrageparameter wie folgt:

```http
GET /flows?property=inheritedAttributes.properties.isDestinationFlow==true
```

**Filter zum Zurückgeben von Datenflüssen an eine bestimmte Quelle oder ein bestimmtes Ziel**

Sie können Datenflüsse filtern, um Datenflüsse nur an ein bestimmtes Ziel oder aus einer bestimmten Quelle zurückzugeben. Filtern Sie beispielsweise Ihre Ziele so, dass nur vorhandene Verbindungen zu Amazon S3-Verbindungen zurückgegeben werden:

```http
GET /flows?property=inheritedAttributes.targetConnections[].connectionSpec.id==4890fc95-5a1f-4983-94bb-e060c08e3f81
```

**Filtern, um alle Ausführungen eines Datenflusses für einen bestimmten Zeitraum abzurufen**

Sie können Datenfluss-Ausführungen eines Datenflusses filtern, um nur Ausführungen in einem bestimmten Zeitintervall zu betrachten, wie unten dargestellt:

```
GET /runs?property=flowId==<flow-id>&property=metrics.durationSummary.startedAtUTC>1593134665781&property=metrics.durationSummary.startedAtUTC<1653134665781
```

**Filtern, um nur fehlgeschlagene Datenflüsse zurückzugeben**

Zu Debugging-Zwecken können Sie alle fehlgeschlagenen Datenfluss-Ausführungen für einen bestimmten Quell- oder Ziel-Datenfluss filtern und anzeigen, wie unten dargestellt:

```http
GET /runs?property=flowId==<flow-id>&property=metrics.statusSummary.status==Failed
```

## Nächste Schritte

In diesem Handbuch wurde die Verwendung der `orderby` und `property` Abfrageparameter zum Sortieren und Filtern von Antworten in der Flow Service-API. Eine schrittweise Anleitung zur Verwendung der API für allgemeine Workflows in Platform finden Sie in den API-Tutorials im Abschnitt [sources](../../sources/home.md) und [Ziele](../../destinations/home.md) Dokumentation.
