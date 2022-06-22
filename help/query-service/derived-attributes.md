---
title: Abgeleitete Attribute
description: Abgeleitete Attribute ermöglichen es Ihnen, Attribute auf einer regulären Platzierung zu berechnen und diese abgeleiteten Attribute optional als Profilattribute in das Echtzeit-Kundenprofil zu veröffentlichen. Dieses Dokument bietet einen Überblick darüber, wie Sie mit Query Service abgeleitete Attribute zur Verwendung mit Ihren Profildaten erstellen können.
source-git-commit: 72e157e0a6310ebf2f55205b03b60600a56e3cf6
workflow-type: tm+mt
source-wordcount: '1650'
ht-degree: 7%

---

# Abgeleitete Attribute

Abgeleitete Attribute ermöglichen es Ihnen, Attribute auf einer regulären Platzierung zu berechnen und diese abgeleiteten Attribute optional als Profilattribute in das Echtzeit-Kundenprofil zu veröffentlichen.

Abgeleitete Attribute, z. B. mit Dezimaldaten erstellte Attribute, sind für eine Vielzahl von Anwendungsfällen erforderlich, die Profildaten analysieren. Mithilfe von Dezimaldaten können Sie Zielgruppen aus Segmenten basierend auf ihrem Perzentil oder ihrer Rangfolge eines bestimmten Attributs erstellen. Mögliche Anwendungsfälle sind beispielsweise:

* Identifizieren der niedrigsten 10 % der Abonnenten basierend auf der Kanalanzeige. Dadurch können Marketing-Experten eine bestimmte Zielgruppe ansprechen und ein neues Abonnentenpaket verkaufen.
* Identifizieren einer Zielgruppe, die zu den 10 % der Flugzeuge gehört, basierend auf ihrer Gesamtzahl der Flugmeilen, die sie zurückgelegt haben, und deren Status &quot;Flyer&quot; lautet. Diese Zielgruppe kann verwendet werden, um gezielt den Verkauf eines neuen Kreditkartenangebots anzusprechen.

## Erste Schritte

Diese Übersicht setzt ein Verständnis der [Platform-API-Aufrufe](../landing/api-guide.md) und die folgenden Komponenten von Adobe Experience Platform:

* [Übersicht über das Echtzeit-Kundenprofil](../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus mehreren Quellen basiert.
* [Grundlagen der Schemakomposition](../xdm/schema/composition.md): Eine Einführung in Experience-Datenmodell (XDM)-Schemas und die Bausteine, Grundsätze und Best Practices zum Erstellen von Schemas.
* [Aktivieren eines Schemas für das Echtzeit-Kundenprofil](../profile/tutorials/add-profile-data.md): In diesem Tutorial werden die Schritte beschrieben, die zum Hinzufügen von Daten zum Echtzeit-Kundenprofil erforderlich sind.

## SQL-Unterstützung für abgeleitete Attribute

Um die Rangfolge von Dezimalstellen basierend auf einer bestimmten Dimension (Kategorie) und einer entsprechenden Metrik (Umsatz, Punkte, Dauer der Anzeige usw.) zu definieren, muss ein Schema so konzipiert sein, dass eine Dezile-Zusammenfassung möglich ist. Dieses Schema kann als Teil des größeren Profilschemas verwendet werden.

### Erstellen eines Identitäts-Namespace für das Profilschema {#identity-namespace}

Identitäts-Namespaces sind eine Komponente des [Identity Service](../identity-service/home.md), die als Indikatoren für den Kontext dient, auf den sich eine Identität bezieht. Eine vollqualifizierte Identität umfasst einen ID-Wert und einen Namespace. Beim Abgleichen und Zusammenführen von Datensatzdaten über Profilfragmente hinweg müssen sowohl der Identitätswert als auch der Namespace übereinstimmen.

Datensätze, die im Zusammenhang mit der Identität erstellt wurden, können als Datengruppe gruppiert werden, was zur Beibehaltung des Lebenszyklus der Daten beiträgt. Benutzerdefinierte Namespaces können mit der [Identity Service-API](../identity-service/api/create-custom-namespace.md) oder über die Benutzeroberfläche. Siehe [Dokumentation zu benutzerdefinierten Namespaces verwalten](../identity-service/namespaces.md#manage-namespaces) für Anleitungen dazu, wie Sie dies über die Benutzeroberfläche durchführen können.

Der primäre Identitätsdeskriptor kann entweder einem Feld in der Schema-Benutzeroberfläche zugewiesen oder mithilfe der Schema Registry-API erstellt werden. Anweisungen dazu finden Sie in der Dokumentation . [Identitätsfeld in der Adobe Experience Platform-Benutzeroberfläche definieren](../xdm/ui/fields/identity.md#define-an-identity-field)oder durch [Schema Registry-API](../xdm/api/descriptors.md#create).

Mit Query Service können Sie auch direkt über SQL eine Identität oder eine primäre Identität für Ad-hoc-Schema-Datensatzfelder festlegen. Weitere Informationen finden Sie in der Dokumentation unter [Festlegen einer sekundären Identität und primären Identität in Ad-hoc-Schemaidentitäten](./data-governance/ad-hoc-schema-identities.md) für weitere Informationen.

## Erstellen abgeleiteter Attribute

Die in diesem Dokument bereitgestellte Beispielabfrage konzentriert sich auf Dezimalstellen, um große Datensätze zu kategorisieren, die Daten von den höchsten zu den niedrigsten Werten zu ordnen (oder umgekehrt) und nach Zeiträumen zu filtern.

### Deciles {#deciles}

Eine Dezimalzahl ist eine Methode, einen Satz von Rangdaten in 10 gleiche Teile aufzuteilen. Wenn die Daten in Dezimalzahlen unterteilt sind, wird jeder Zeile des Datensatzes ein Dezimalrang zugewiesen. Dadurch können die Daten in absteigender oder aufsteigender Reihenfolge sortiert werden.

Ein Dezimalrang ordnet die Daten in der Reihenfolge von unten nach oben an und erfolgt auf einer Skala von 1 bis 10, wobei jede aufeinander folgende Zahl einer Steigerung von 10 Prozentpunkten entspricht.

Decile Buckets stellen die Anzahl der Ranggruppen dar und werden verwendet, um einer Dimension (Kategorie) im Datensatz eine Rangfolge zuzuweisen. Der Bucket kann eine Zahl oder ein Ausdruck sein, der als positiver ganzzahliger Wert für jede Partition ausgewertet wird. Die Behälter dürfen keinen Nullwert haben.

Quartile werden verwendet, um die Verteilung durch vier und Perzentile durch 100 zu teilen.

### Erstellen des Schemas für Dezimalspannen {#create-schema}

Das für Dezimalgruppen erstellte Schema besteht aus drei integralen Teilen: einen Datentyp, eine Feldergruppe für den Datentyp (pro Quelldatensatz) und ein primäres Identitätsfeld.

>[!NOTE]
>
>Bevor das Schema erstellt werden kann, muss ein Identitäts-Namespace erstellt werden. Siehe [Identitäts-Namespace](#identity-namespace) für weitere Details.

Adobe bietet mehrere Standard-XDM-Klassen (&quot;Core&quot;), darunter &quot;XDM Individual Profile&quot;und &quot;XDM ExperienceEvent&quot;. Zusätzlich zu diesen Core-Klassen können Sie auch eigene benutzerdefinierte Klassen erstellen, um spezifischere Anwendungsfälle für Ihr Unternehmen zu beschreiben. Informationen dazu finden Sie in den Handbüchern [Erstellen und Bearbeiten von Schemata in der Benutzeroberfläche](../xdm/ui/resources/schemas.md#create) oder mithilfe der [Schemas-Endpunkt in der Schema Registry-API](../xdm/api/schemas.md#create) für weitere Details.

Daten, die zur Verwendung durch Echtzeit-Kundenprofile in die Experience Platform eingegeben werden, müssen einem XDM-Schema (Experience Data Model) entsprechen, das für Profile aktiviert ist. Damit ein Schema für Profile aktiviert werden kann, muss es entweder die XDM Individual Profile- oder die XDM ExperienceEvent-Klasse implementieren.

Sie können [Aktivieren eines Schemas zur Verwendung im Echtzeit-Kundenprofil mithilfe der Schema Registry-API](../xdm/tutorials/create-schema-api.md) oder [Benutzeroberfläche des Schema-Editors](../xdm/tutorials/create-schema-ui.md).  Detaillierte Anweisungen zum Aktivieren eines Schemas für Profile finden Sie in der entsprechenden Dokumentation.

### Erstellen eines Datentyps {#create-data-type}

Datentypen werden als Referenzfeldtypen in Klassen oder Schemafeldgruppen verwendet und ermöglichen die konsistente Verwendung einer Mehrfeldstruktur, die an einer beliebigen Stelle im Schema enthalten sein kann. Die Erstellung des Datentyps ist ein einmaliger Schritt pro Sandbox, da er für alle dezimalbezogenen Feldergruppen wiederverwendet werden kann.

Anweisungen dazu finden Sie in der Dokumentation . [benutzerdefinierten Datentyp definieren](../xdm/api/data-types.md) mithilfe der [Schema Registry-API](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

### Erstellen der Dezimalfeldgruppe {#create-field-group}

Die Erstellung der Feldergruppe ist ein einmaliger Schritt pro Sandbox. Sie kann auch für alle dezimalbezogenen Schemas wiederverwendet werden.

Anweisungen dazu finden Sie in der Dokumentation . [Erstellen von Feldergruppen über die Benutzeroberfläche](../xdm/ui/resources/field-groups.md#create)

## Verwenden von Query Service zum Erstellen von Dezimalstellen

Query Service bietet eine ideale Möglichkeit, einen Datensatz mit kategorischen Dezimalstellen zu erstellen. Dies kann dann in Verbindung mit dem Segmentierungsdienst verwendet werden, um Zielgruppen basierend auf dem Attribut-Ranking zu erstellen.

Die in den folgenden Beispielen angezeigten Konzepte können angewendet werden, um andere Dezimalgruppen-Datensätze zu erstellen, sofern eine Kategorie (Dimension) definiert und eine Metrik verfügbar ist. Die Beispiele basieren auf Daten für ein Treueprogramm von Fluggesellschaften. Die Treuedaten der Fluggesellschaften verwenden die Experience Events-Klasse, bei der jedes Ereignis einen Datensatz einer Geschäftstransaktion für **Kilometerstand**, entweder gutgeschrieben oder belastet, und die Mitgliedschaft **Treuestatus** entweder &quot;Flyer&quot;, &quot;Frequent&quot;, &quot;Silber&quot;oder &quot;Gold&quot;. Das primäre Identitätsfeld lautet `membershipNumber`.

### Abfragevorlage erstellen {#create-a-query-template}

Die Vorlage kann entweder mit dem Abfrage-Editor in der Benutzeroberfläche oder über die [Query Service-API](./api/query-templates.md#create-a-query-template).

Die im Folgenden dargestellten Abschnitte der Abfragevorlage werden ausführlicher behandelt.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/query/query-templates \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
         "name": "Airline Loyalty Deciles Insert into profile",
         "sql":
            "WITH summed_miles_1 AS (
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
                LEFT JOIN map_6 ON  (all_memberships.membershipNumber = map_6.membershipNumber)"
        }'
```

#### Rückblickszeiträume

Der Dezimaldatentyp enthält einen Behälter für 1, 3, 6, 9, 12 und Lebenszeit-Rückblicke. Die Abfrage nutzt die Rückblickszeiträume von 1, 3 und 6 Monaten, sodass jeder Abschnitt einige &quot;wiederholte&quot;Abfragen enthält, um temporäre Tabellen für jeden Rückblickzeitraum zu erstellen.

>[!NOTE]
>
>Wenn die Quelldaten nicht über eine Spalte verfügen, die zur Bestimmung eines Rückblickzeitraums verwendet werden kann, werden alle Rangfolgen der Dezimalklasse unter `decileMonthAll`.

#### Aggregation

Verwenden Sie gemeinsame Tabellenausdrücke (CTE), um die Meilensteine vor der Erstellung von Dezimalbuckets zu aggregieren. Dadurch werden die Gesamtmeilen für einen bestimmten Rückblickzeitraum bereitgestellt. CTEs existieren temporär und können nur im Rahmen der größeren Abfrage verwendet werden.

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

Der Block wird in der Vorlage zweimal wiederholt (`summed_miles_3` und `summed_miles_6`), um die Daten für die anderen Rückblickperioden zu generieren.

Beachten Sie die Identitäts-, Dimensions- und Metrikspalten für die Abfrage (`membershipNumber`, `loyaltyStatus` und `totalMiles` ).

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

Bei mehreren Rückblickszeiträumen müssen Sie die dezimalen Behälterzuordnungen im Voraus mithilfe des `MAP_FROM_ARRAYS` und `COLLECT_LIST` Funktionen. Im Beispielausschnitt `MAP_FROM_ARRAYS` erstellt eine Zuordnung mit einem Schlüsselpaar (`loyaltyStatus`) und -Werten (`decileBucket`) Arrays. `COLLECT_LIST` gibt ein Array mit allen Werten in der angegebenen Spalte zurück.

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

### Ausführen der Abfragevorlage

Abfragen können [entweder über die Benutzeroberfläche ausgeführt](./ui/user-guide.md#executing-queries) oder [Query Service-API](./api/queries.md#create-a-query).

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/query/queries \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "dbName": "prod:all",
    "templateId": "{{airline_decile_query_template_id}}",
    "insertIntoParameters": {
        "datasetName": "airline_loyalty_decile"
    }
}'
```

Eine Korrelation zwischen der Rangnummer und dem Perzentil ist in den Abfrageergebnissen aufgrund der Verwendung von Dezimalstellen garantiert. Jeder Rang entspricht 10 %, sodass die Ermittlung einer Zielgruppe, die auf den oberen 30 % basiert, nur die Ränge 1, 2 und 3 erreichen muss.

## Nächste Schritte

Der Segmentation Service bietet eine Benutzeroberfläche und eine RESTful-API, mit der Sie Zielgruppen basierend auf diesen Dezimalgruppen erstellen können. Siehe [Übersicht über den Segmentierungsdienst](../segmentation/home.md) für Informationen zum Erstellen, Auswerten und Zugreifen auf Segmente.

Detaillierte Informationen zum Erstellen und Verwenden von Segmenten im Segment Builder (der Benutzeroberflächenimplementierung des Segmentation Service) finden Sie in der [Segment Builder-Handbuch](../segmentation/ui/overview.md).

Informationen zum Erstellen von Segmentdefinitionen mithilfe der API finden Sie im Tutorial zum [Erstellen von Zielgruppensegmenten mithilfe der API](../segmentation/tutorials/create-a-segment.md).
