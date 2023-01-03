---
title: Anwendungsfall für auf Entscheidungen basierende abgeleitete Attribute
description: In diesem Handbuch werden die Schritte erläutert, die zur Verwendung von Query Service zum Erstellen von dezimalbasierten abgeleiteten Attributen für die Verwendung mit Ihren Profildaten erforderlich sind.
exl-id: 0ec6b511-b9fd-4447-b63d-85aa1f235436
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1508'
ht-degree: 3%

---

# Anwendungsfall für dezimalbasierte abgeleitete Attribute

Abgeleitete Attribute erleichtern komplexe Anwendungsfälle für die Analyse von Daten aus dem Data Lake, die mit anderen nachgelagerten Platform-Diensten verwendet oder in Ihren Echtzeit-Kundenprofildaten veröffentlicht werden können.

In diesem Anwendungsbeispiel wird gezeigt, wie Sie dezimalbasierte abgeleitete Attribute für die Verwendung mit Ihren Echtzeit-Kundenprofildaten erstellen. Anhand eines Beispielszenarios zur Treue von Fluggesellschaften erfahren Sie in diesem Handbuch, wie Sie einen Datensatz erstellen, der kategorische Dezile verwendet, um Zielgruppen basierend auf Rangattributen zu segmentieren und zu erstellen.

Die folgenden Schlüsselkonzepte werden veranschaulicht:

* Schemaerstellung für das Dezimalbucketing.
* Kategorische Dezimalerstellung.
* Erstellung komplexer abgeleiteter Attribute.
* Berechnung der Dezimalzahlen über einen Lookback-Zeitraum.
* Eine Beispielabfrage, die die Aggregation, Rangfolge und das Hinzufügen eindeutiger Identitäten demonstriert, um die Erstellung von Zielgruppen auf der Grundlage dieser Dezimalgruppen zu ermöglichen.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der [Abfrageausführung in Query Service](../best-practices/writing-queries.md) und die folgenden Komponenten von Adobe Experience Platform:

* [Übersicht über das Echtzeit-Kundenprofil](../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus mehreren Quellen basiert.
* [Grundlagen der Schemakomposition](../../xdm/schema/composition.md): Eine Einführung in Experience-Datenmodell (XDM)-Schemas und die Bausteine, Grundsätze und Best Practices zum Erstellen von Schemas.
* [Aktivieren eines Schemas für das Echtzeit-Kundenprofil](../../profile/tutorials/add-profile-data.md): In diesem Tutorial werden die Schritte beschrieben, die zum Hinzufügen von Daten zum Echtzeit-Kundenprofil erforderlich sind.
* [So definieren Sie einen benutzerdefinierten Datentyp](../../xdm/api/data-types.md): Datentypen werden als Referenzfeldtypen in Klassen oder Schemafeldgruppen verwendet und ermöglichen die konsistente Verwendung einer Mehrfeldstruktur, die an einer beliebigen Stelle im Schema enthalten sein kann.

## Ziele

Das in diesem Dokument angegebene Beispiel verwendet Dezimalstellen, um abgeleitete Attribute für die Rangdaten aus einem Treueschema einer Fluglinie zu erstellen. Abgeleitete Attribute ermöglichen es Ihnen, den Nutzwert Ihrer Daten zu maximieren, indem Sie eine Zielgruppe anhand der höchsten &#39;n&#39; % für eine bestimmte Kategorie identifizieren.

## Erstellen von dezimalbasierten abgeleiteten Attributen

Um die Rangfolge von Dezimalstellen basierend auf einer bestimmten Dimension und einer entsprechenden Metrik zu definieren, muss ein Schema so konzipiert sein, dass eine Dezimalzusammenfassung möglich ist.

In diesem Handbuch wird mithilfe eines Datensatzes zur Treueprogramm von Fluggesellschaften gezeigt, wie mithilfe von Query Service anhand der über verschiedene Lookback-Zeiträume hinweg zurückgelegten Meilen Dezile erstellt werden können.

## Verwenden von Query Service zum Erstellen von Dezimalstellen

Mithilfe von Query Service können Sie einen Datensatz erstellen, der kategorische Dezimalzahlen enthält, die dann segmentiert werden können, um Zielgruppen basierend auf der Attributranking zu erstellen. Die in den folgenden Beispielen angezeigten Konzepte können angewendet werden, um andere Dezimalgruppen-Datensätze zu erstellen, sofern eine Kategorie definiert und eine Metrik verfügbar ist.

Die Beispieldaten zur Treue von Fluglinien verwenden eine [XDM ExperienceEvents-Klasse](../../xdm/classes/experienceevent.md). Jedes Ereignis ist ein Datensatz über eine geschäftliche Transaktion für Meilen, entweder gutgeschrieben oder belastet, und der Status der Mitgliedschaftsloyalität von &quot;Flyer&quot;, &quot;Frequent&quot;, &quot;Silver&quot;oder &quot;Gold&quot;. Das primäre Identitätsfeld lautet `membershipNumber`.

### Beispieldatensätze

Der ursprüngliche Datensatz zur Treueprogramm von Fluggesellschaften für dieses Beispiel ist &quot;Daten zum Treueprogramm für Fluglinien&quot;und weist das folgende Schema auf. Beachten Sie, dass die primäre Identität für das Schema lautet `_profilefoundationreportingstg.membershipNumber`.

![Ein Diagramm des &quot;Airline Loyalty Data&quot;-Schemas.](../images/derived-attributes/deciles-use-case/airline-loyalty-data.png)

**Beispieldaten**

Die folgende Tabelle zeigt die Beispieldaten im `_profilefoundationreportingstg` -Objekt, das für dieses Beispiel verwendet wird. Es bietet Kontext für die Verwendung von Dezimalbuckets zum Erstellen komplexer abgeleiteter Attribute.

>[!NOTE]
>
>Für Kürze wird die Mandanten-ID `_profilefoundationreportingstg` wurde am Anfang des Namespace in den Spaltentiteln und nachfolgenden Erwähnungen im gesamten Dokument weggelassen.

| `.membershipNumber` | `.emailAddress.address` | `.transactionDate` | `.transactionType` | `.transactionDetails` | `.mileage` | `.loyaltyStatus` |
|---|---|---|---|---|---|---|
| C435678623 | sfeldmark1vr@studiopress.com | 2022-01-01 | STATUS_MILES | Neues Mitglied | 5.000 | FLYER |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-01 | AWARD_MILES | JFK-FRA | 7500 | SILBER |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-01 | STATUS_MILES | JFK-FRA | 7500 | SILBER |
| B789279247 | pgalton32n@barnesandnoble.com | 2022-02-10 | AWARD_MILES | FRA-JFK | 5.000 | SILBER |
| A123487284 | rritson1zn@sciencedaily.com | 2022-01-07 | STATUS_MILES | Neue Kreditkarte | 10000 | FLYER |

{style=&quot;table-layout:auto&quot;}

## Dezimaldatensätze generieren

In den oben aufgeführten Daten zur Treueprogramm der Fluggesellschaft wird die Variable `.mileage` Der Wert enthält die Anzahl der Meilen, die ein Mitglied für jeden einzelnen Flug zurücklegt. Diese Daten werden verwendet, um Dezimalstellen für die Anzahl der Meilen zu erstellen, die über Lebenszeit-Lookbacks und verschiedene Lookback-Zeiträume geflogen sind. Zu diesem Zweck wird ein Datensatz erstellt, der Dezimalstellen in einem Zuordnungs-Datentyp für jeden Lookback-Zeitraum und eine entsprechende Dezimalzahl für jeden Lookback-Zeitraum enthält, der unter `membershipNumber`.

Erstellen Sie ein &quot;Airline Loyalty Decile Schema&quot;, um mithilfe von Query Service einen Dezimaldatensatz zu erstellen.

![Ein Diagramm des &quot;Airline Loyalty Decile Schemas&quot;.](../images/derived-attributes/deciles-use-case/airline-loyalty-decile-schema.png)

### Aktivieren des Schemas für das Echtzeit-Kundenprofil

Daten, die zur Verwendung durch das Echtzeit-Kundenprofil in Experience Platform aufgenommen werden, müssen [ein Experience-Datenmodell (XDM)-Schema, das für Profil aktiviert ist](../../xdm/ui/resources/schemas.md). Damit ein Schema für Profile aktiviert werden kann, muss es entweder die XDM Individual Profile- oder die XDM ExperienceEvent-Klasse implementieren.

[Aktivieren Sie Ihr Schema zur Verwendung im Echtzeit-Kundenprofil mithilfe der Schema Registry-API.](../../xdm/tutorials/create-schema-api.md) oder [Benutzeroberfläche des Schema-Editors](../../xdm/tutorials/create-schema-ui.md).  Detaillierte Anweisungen zum Aktivieren eines Schemas für Profile finden Sie in der entsprechenden Dokumentation.

Erstellen Sie anschließend einen Datentyp, der für alle dezimalbezogenen Feldergruppen wiederverwendet werden soll. Die Erstellung der Dezimalfeldgruppe ist ein einmaliger Schritt pro Sandbox. Sie kann auch für alle dezimalbezogenen Schemas wiederverwendet werden.

### Erstellen Sie einen Identitäts-Namespace und markieren Sie ihn als primäre Kennung {#identity-namespace}

Jedes Schema, das für die Verwendung mit Dezimalstellen erstellt wurde, muss eine primäre Identität aufweisen. Sie können [Identitätsfeld in der Benutzeroberfläche von Adobe Experience Platform-Schemas definieren](../../xdm/ui/fields/identity.md#define-an-identity-field)oder durch [Schema Registry-API](../../xdm/api/descriptors.md#create).

Mit Query Service können Sie auch direkt über SQL eine Identität oder eine primäre Identität für Ad-hoc-Schema-Datensatzfelder festlegen. Weitere Informationen finden Sie in der Dokumentation unter [Festlegen einer sekundären Identität und primären Identität in Ad-hoc-Schemaidentitäten](../data-governance/ad-hoc-schema-identities.md) für weitere Informationen.

### Erstellen einer Abfrage zur Berechnung von Dezimalzahlen über einen Lookback-Zeitraum {#create-a-query}

Das folgende Beispiel zeigt die SQL-Abfrage zur Berechnung einer Dezimalzahl über einen Lookback-Zeitraum.

Eine Vorlage kann entweder mit dem Abfrage-Editor in der Benutzeroberfläche oder über die [Query Service-API](../api/query-templates.md#create-a-query-template).

```sql
CREATE TABLE AS airline_loyality_decile 
{  WITH summed_miles_1 AS (
        SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
            _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
            SUM(_profilefoundationreportingstg.mileage) AS totalMiles
        FROM airline_loyalty_data
        WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 0))
    GROUP BY 1,2
    ),
    summed_miles_3 AS (
        SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
            _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
            SUM(_profilefoundationreportingstg.mileage) AS totalMiles
        FROM airline_loyalty_data
        WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 1))
    GROUP BY 1,2
    ),
    summed_miles_6 AS (
        SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
            _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
            SUM(_profilefoundationreportingstg.mileage) AS totalMiles
        FROM airline_loyalty_data
        WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 4))
    GROUP BY 1,2
    ),
    rankings_1 AS (
        SELECT membershipNumber,
            loyaltyStatus,
            totalMiles,
            NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
        FROM summed_miles_1
    ),
    rankings_3 AS (
        SELECT membershipNumber,
            loyaltyStatus,
            totalMiles,
            NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
        FROM summed_miles_3
    ),
    rankings_6 AS (
        SELECT membershipNumber,
            loyaltyStatus,
            totalMiles,
            NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
        FROM summed_miles_6
    ),
    map_1 AS (
        SELECT membershipNumber,
            MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth1
        FROM rankings_1
        GROUP BY membershipNumber
    ),
    map_3 AS (
        SELECT membershipNumber,
            MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth3
        FROM rankings_3
        GROUP BY membershipNumber
    ),
    map_6 AS (
        SELECT membershipNumber,
            MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth6
        FROM rankings_6
        GROUP BY membershipNumber
    ),
    all_memberships AS (
        SELECT DISTINCT _profilefoundationreportingstg.membershipNumber AS membershipNumber FROM airline_loyalty_data
    )
    SELECT STRUCT(
            all_memberships.membershipNumber AS membershipNumber,
            STRUCT(
                    map_1.decileMonth1 AS decileMonth1,
                    map_3.decileMonth3 AS decileMonth3,
                    map_6.decileMonth6 AS decileMonth6
            ) AS decilesMileage
        ) AS _profilefoundationreportingstg
    FROM all_memberships
        LEFT JOIN map_1 ON  (all_memberships.membershipNumber = map_1.membershipNumber)
        LEFT JOIN map_3 ON  (all_memberships.membershipNumber = map_3.membershipNumber)
        LEFT JOIN map_6 ON  (all_memberships.membershipNumber = map_6.membershipNumber)
    }
```

### Abfrage überprüfen

Die Abschnitte der Beispielabfrage werden im Folgenden detaillierter behandelt.

#### Lookback-Zeiträume

Der Dezimaldatentyp enthält einen Behälter für 1, 3, 6, 9, 12 und Lebenszeit-Lookbacks. Die Abfrage nutzt die Lookback-Zeiträume von 1, 3 und 6 Monaten, sodass jeder Abschnitt einige &quot;wiederholte&quot;Abfragen enthält, um temporäre Tabellen für jeden Lookback-Zeitraum zu erstellen.

>[!NOTE]
>
>Wenn die Quelldaten nicht über eine Spalte verfügen, die zur Bestimmung eines Lookback-Zeitraums verwendet werden kann, werden alle Rangfolgen der Dezimalklasse unter `decileMonthAll`.

#### Aggregation

Verwenden Sie gemeinsame Tabellenausdrücke (CTE), um die Meilensteine vor der Erstellung von Dezimalbuckets zu aggregieren. Dadurch werden die Gesamtmeilen für einen bestimmten Lookback-Zeitraum bereitgestellt. CTEs existieren temporär und können nur im Rahmen der größeren Abfrage verwendet werden.

```sql
summed_miles_1 AS (
    SELECT _profilefoundationreportingstg.membershipNumber AS membershipNumber,
           _profilefoundationreportingstg.loyaltyStatus AS loyaltyStatus,
           SUM(_profilefoundationreportingstg.mileage) AS totalMiles
    FROM airline_loyalty_data
    WHERE _profilefoundationreportingstg.transactionDate < (MAKE_DATE(YEAR(CURRENT_DATE), MONTH(CURRENT_DATE), 1) - MAKE_YM_INTERVAL(0, 0))
    GROUP BY 1,2
)
```

Der Block wird in der Vorlage zweimal wiederholt (`summed_miles_3` und `summed_miles_6`), um die Daten für die anderen Lookback-Zeiträume zu generieren.

Es ist wichtig, die Identitäts-, Dimensions- und Metrikspalten für die Abfrage (`membershipNumber`, `loyaltyStatus` und `totalMiles` ).

#### Ranking

Dekore ermöglichen kategorische Bucketings. Um die Rangnummer zu erstellen, muss die `NTILE` -Funktion mit einem Parameter von `10` innerhalb eines FENSTERS, gruppiert nach `loyaltyStatus` -Feld. Dies führt zu einer Rangfolge von 1 bis 10. Legen Sie die `ORDER BY` -Klausel `WINDOW` nach `DESC` , um sicherzustellen, dass der Rangwert von `1` wird dem **größte** Metrik innerhalb der Dimension.

```sql
rankings_1 AS (
    SELECT membershipNumber,
           loyaltyStatus,
           totalMiles,
           NTILE(10) OVER (PARTITION BY loyaltyStatus ORDER BY totalMiles DESC) AS decileBucket
    FROM summed_miles_1
)
```

#### Zuordnungsaggregation

Bei mehreren Lookback-Zeiträumen müssen Sie die dezimalen Behälterzuordnungen im Voraus mithilfe des `MAP_FROM_ARRAYS` und `COLLECT_LIST` Funktionen. Im Beispielausschnitt `MAP_FROM_ARRAYS` erstellt eine Zuordnung mit einem Schlüsselpaar (`loyaltyStatus`) und -Werten (`decileBucket`) Arrays. `COLLECT_LIST` gibt ein Array mit allen Werten in der angegebenen Spalte zurück.

```sql
map_1 AS (
    SELECT membershipNumber,
           MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonth1
    FROM rankings_1
    GROUP BY membershipNumber
)
```

>[!NOTE]
>
>Die Zuordnungsaggregation ist nicht erforderlich, wenn die Dezimaltrennung nur für einen Lebenszeitzeitraum erforderlich ist.

#### Eindeutige Identitäten

Die Liste der eindeutigen Identitäten (`membershipNumber`) ist erforderlich, um eine eindeutige Liste aller Mitgliedschaften zu erstellen.

```sql
all_memberships AS (
    SELECT DISTINCT _profilefoundationreportingstg.membershipNumber AS membershipNumber FROM airline_loyalty_data
)
```

>[!NOTE]
>
>Wenn die Dezimaltrennung nur für einen Lebenszeitzeitraum erforderlich ist, kann dieser Schritt weggelassen und die Aggregation nach `membershipNumber` kann im letzten Schritt durchgeführt werden.

#### Alle temporären Daten zusammenführen

Der letzte Schritt besteht darin, alle temporären Daten in einem Formular zusammenzufügen, das mit der Struktur der Dezimalstellen in der Feldergruppe identisch ist.

```sql
SELECT STRUCT(
           all_memberships.membershipNumber AS membershipNumber,
           STRUCT(
                map_1.decileMonth1 AS decileMonth1,
                map_3.decileMonth3 AS decileMonth3,
                map_6.decileMonth6 AS decileMonth6
           ) AS decilesMileage
       ) AS _profilefoundationreportingstg
FROM all_memberships
    LEFT JOIN map_1 ON  (all_memberships.membershipNumber = map_1.membershipNumber)
    LEFT JOIN map_3 ON  (all_memberships.membershipNumber = map_3.membershipNumber)
    LEFT JOIN map_6 ON  (all_memberships.membershipNumber = map_6.membershipNumber)
```

Wenn nur Lebenszeitdaten verfügbar sind, würde Ihre Abfrage wie folgt aussehen:

```sql
SELECT STRUCT(
           rankings.membershipNumber AS membershipNumber,
           STRUCT(
                MAP_FROM_ARRAYS(COLLECT_LIST(loyaltyStatus), COLLECT_LIST(decileBucket)) AS decileMonthAll
           ) AS decilesMileage
       ) AS _profilefoundationreportingstg
FROM rankings
GROUP BY rankings.membershipNumber
```

Eine Korrelation zwischen der Rangnummer und dem Perzentil ist in den Abfrageergebnissen aufgrund der Verwendung von Dezimalstellen garantiert. Jeder Rang entspricht 10 %, sodass die Ermittlung einer Zielgruppe, die auf den oberen 30 % basiert, nur die Ränge 1, 2 und 3 erreichen muss.

### Ausführen der Abfragevorlage

Führen Sie die Abfrage aus, um den Dezimaldatensatz zu füllen. Sie können die Abfrage auch als Vorlage speichern und planen, dass sie in einem Cadence ausgeführt wird. Wenn die Abfrage als Vorlage gespeichert wird, kann sie auch aktualisiert werden, um das Muster zum Erstellen und Einfügen zu verwenden, das auf die `table_exists` Befehl. Weitere Informationen zur Verwendung der `table_exists`-Befehl finden Sie im [SQL-Syntaxhandbuch](../sql/syntax.md#table-exists).

## Nächste Schritte

Im oben genannten Anwendungsbeispiel werden die Schritte erläutert, um Dezimalattribute im Echtzeit-Kundenprofil verfügbar zu machen. Dadurch kann Segmentation Service über eine Benutzeroberfläche oder eine RESTful-API Zielgruppen basierend auf diesen Dezimalgruppen generieren. Siehe [Übersicht über den Segmentierungsdienst](../../segmentation/home.md) für Informationen zum Erstellen, Auswerten und Zugreifen auf Segmente.
