---
title: Filtern von Antworten in der Reactor-API
description: Hier erfahren Sie, wie Sie bei der Auflistung von Ressourcen in der Reactor-API Ergebnisse filtern können.
exl-id: 8a91f3dd-4ead-4a10-abb1-e71acb0d73b6
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 100%

---

# Filtern von Antworten in der Reactor-API

Bei Verwendung von Listenendpunkten (GET) in der Reactor-API kann es erforderlich sein, die zurückgegebenen Ergebnisse auf eine Untergruppe von Datensätzen zu beschränken. Zu diesem Zweck unterstützen viele Listenendpunkte der API die Möglichkeit, nach bestimmten Attributen zu filtern. Wenn Sie stattdessen strukturierte Abfragen an die API richten möchten, finden Sie weitere Informationen im Benutzerhandbuch zum Thema [Suchen](./search.md).

## Filter-Syntax

Das folgende Beispiel erläutert, wie Sie Filter für Ihre GET-Anfragen implementieren.

**API-Format**

Um die Antwort nach einem bestimmten Listenendpunkt zu filtern, müssen Sie einen `filter`-Abfrageparameter im Anfragepfad angeben.

>[!NOTE]
>
>Die folgende Vorlage verwendet eckige Klammern (`[]`) und Leerzeichen für bessere Lesbarkeit. In der Praxis müssen diese Zeichen URI-kodiert sein, wie in [RFC 3986](https://tools.ietf.org/html/rfc3986) beschrieben. Ein Beispiel für einen ordnungsgemäß kodierten Anfragepfad finden Sie weiter unten in diesem Handbuch.
>
>Beachten Sie, dass bei falscher Filterstruktur keine Filter angewendet werden und der vollständige Ergebnissatz zurückgegeben wird.

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME}]={OPERATOR} {VALUE}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `{ENDPOINT}` | Ein Auflistungsendpunkt in der Reactor-API, der Filterparameter unterstützt. |
| `{ATTRIBUTE_NAME}` | Der Name eines bestimmten Attributs, nach dem Ergebnisse gefiltert werden sollen. Beachten Sie, dass verschiedene Endpunkte unterschiedliche Attribute für die Filterung unterstützen. Eine Liste der verfügbaren Filterattribute finden Sie im Referenzhandbuch für den Endpunkt, mit dem Sie arbeiten. |
| `{OPERATOR}` | Der Operator, der bestimmt, wie die Ergebnisse anhand des bereitgestellten `{VALUE}` ausgewertet werden. Die unterstützten Operatoren sind im [Anhang](#supported-operators) aufgeführt. |
| `{VALUE}` | Der Wert, mit dem die zurückgegebenen Ergebnisse verglichen werden sollen. Beim Vergleich auf Gleichheit mit dem Operator `EQ` muss der Wert eine exakte Übereinstimmung sein, bei der Groß- und Kleinschreibung berücksichtigt werden, damit er in die Antwort aufgenommen werden kann. |

{style=&quot;table-layout:auto&quot;}

**Anfrage**

Die folgende Beispielanfrage ruft eine Liste der veröffentlichten Bibliotheken ab, indem ein Filter angewendet wird, für den das Attribut `state` der Bibliothek `published` entsprechen muss.

Vor der URI-Kodierung würde die Syntax für diesen Filter im Anfragepfad wie folgt aussehen:

`https://reactor.adobe.io/properties/PR906238a59bbf4262bcedba248f483600/libraries?filter[state]=EQ published`

Sobald der Pfad und die Abfrageparameter URI-kodiert wurden, können sie in API-Anfragen wie der folgenden verwendet werden:

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR906238a59bbf4262bcedba248f483600/libraries?filter%5Bstate%5D=EQ%20published \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

## Filtern nach mehreren Werten {#multiple-values}

Um für ein einzelnes Attribut nach mehreren Werten zu filtern, geben Sie die Werte als kommagetrennte Liste an.

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME}]={OPERATOR} {VALUE_1},{VALUE_2}
```

## Verwenden mehrerer Filter

Um Filter für mehrere Attribute anzuwenden, geben Sie für jedes Attribut einen `filter`-Parameter an. Die Parameter müssen durch kaufmännische Und-Zeichen (`&`) getrennt werden.

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME_1}]={OPERATOR} {VALUE}&filter[{ATTRIBUTE_NAME_2}]={OPERATOR} {VALUE}
```

>[!NOTE]
>
>Wenn Sie dasselbe Attribut in mehreren Filtern für dieselbe Anfrage angeben, wird nur der zuletzt angegebene Filter für dieses Attribut angewendet.

## Anhang

Der folgende Abschnitt enthält eine zusätzliche Information für die Arbeit mit Filtern in der Reactor-API.

### Unterstützte Filteroperatoren {#operators}

In der folgenden Tabelle sind die unterstützten Operatorwerte für Filterparameter aufgeführt. Beachten Sie, dass je nach Attribut, nach dem Sie filtern, nicht alle verfügbaren Filteroperatoren anwendbar sind, wie die Verwendung der Operatoren „kleiner als“ oder „größer als“ für Zeichenfolgenattribute.

| Operator | Beschreibung |
| --- | --- |
| `EQ` | Das Attribut muss dem bereitgestellten Wert entsprechen. |
| `NOT` | Das Attribut darf dem bereitgestellten Wert nicht entsprechen. |
| `LT` | Das Attribut muss kleiner als der angegebene Wert sein. |
| `GT` | Das Attribut muss größer als der angegebene Wert sein. |
| `BETWEEN` | Das Attribut muss innerhalb eines bestimmten Wertebereichs liegen. Bei Verwendung dieses Operators müssen [zwei Werte](#multiple-values) angegeben werden, um die Mindest- und Höchstwerte für den gewünschten Bereich anzugeben. |
| `CONTAINS` | Das Attribut muss den angegebenen Wert enthalten, wie einen Zeichensatz innerhalb eines Zeichenfolgenattributs. |
