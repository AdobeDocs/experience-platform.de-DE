---
title: Abfrage Accelerated Store Reporting Insights
description: Erfahren Sie, wie Sie über Query Service ein Berichtseinblicke-Datenmodell für die Verwendung mit beschleunigten Store-Daten und benutzerdefinierten Dashboards erstellen.
source-git-commit: 16ae8a16d8c4f7ec68a054e8d15a518f453a05c7
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 0%

---

# Einblicke in die Abfrage-Berichtserstellung

Der Abfrage-beschleunigte Speicher ermöglicht Ihnen, die Zeit und Verarbeitungsleistung zu reduzieren, die erforderlich ist, um kritische Einblicke aus Ihren Daten zu gewinnen. In der Regel werden Daten in regelmäßigen Abständen verarbeitet (z. B. stündlich oder täglich), wobei aggregierte Ansichten erstellt und in Berichten verwendet werden. Die Analyse dieser Berichte, die aus aggregierten Daten generiert werden, liefert Einblicke, die die Geschäftsleistung verbessern sollen. Der Abfrage-beschleunigte Speicher bietet einen Cache-Dienst, eine gleichzeitige Nutzung, ein interaktives Erlebnis und eine zustandlose API. Es wird jedoch davon ausgegangen, dass die Daten vorverarbeitet und für aggregierte Abfragen optimiert sind und nicht für die Rohdatenabfrage.

Mit dem Abfrage-beschleunigten Speicher können Sie ein benutzerdefiniertes Datenmodell erstellen und/oder vorhandene Real-time Customer Data Platform-Datenmodelle erweitern. Anschließend können Sie mit Ihren Berichterstellungseinblicken interagieren oder sie in ein Berichts-/Visualisierungsframework Ihrer Wahl einbetten. Weitere Informationen finden Sie in der Dokumentation zum Real-time Customer Data Platform Insights-Datenmodell . [Passen Sie Ihre SQL-Abfragevorlagen an, um Real-Time CDP-Berichte für Ihre Marketing- und KPI-Anwendungsfälle (Key Performance Indicators) zu erstellen.](../../dashboards/cdp-insights-data-model.md).

Das Real-Time CDP-Datenmodell von Adobe Experience Platform bietet Einblicke in Profile, Segmente und Ziele und ermöglicht die Real-Time CDP-Insight-Dashboards. Dieses Dokument führt Sie durch den Prozess der Erstellung Ihres Berichtseinblicke-Datenmodells und darüber, wie Sie Real-Time CDP-Datenmodelle nach Bedarf erweitern.

## Voraussetzungen

In diesem Tutorial werden benutzerdefinierte Dashboards verwendet, um Daten aus Ihrem benutzerdefinierten Datenmodell in der Platform-Benutzeroberfläche zu visualisieren. Siehe [Dokumentation zu benutzerdefinierten Dashboards](../../dashboards/user-defined-dashboards.md) , um mehr über diese Funktion zu erfahren.

## Erste Schritte

Die Data Distiller-SKU ist erforderlich, um ein benutzerdefiniertes Datenmodell für Ihre Berichtseinblicke zu erstellen und die Real-Time CDP-Datenmodelle zu erweitern, die angereicherte Platform-Daten enthalten. Siehe [Verpackung](../packages.md), [Limits](../guardrails.md#query-accelerated-store)und [Lizenz](../data-distiller/licence-usage.md) Dokumentation, die sich auf die Data Distiller SKU bezieht. Wenn Sie nicht über die Data Distiller-SKU verfügen, wenden Sie sich für weitere Informationen an Ihren Adobe-Kundenbetreuer.

## Erstellen eines Berichtseinblicke-Datenmodells

In diesem Tutorial wird ein Beispiel für das Erstellen eines Audience Insight-Datenmodells verwendet. Wenn Sie eine oder mehrere Advertiser-Plattformen verwenden, um Ihre Zielgruppe zu erreichen, können Sie die API des Advertisers verwenden, um eine ungefähre Übereinstimmungsanzahl Ihrer Zielgruppe zu erhalten.

Zunächst verfügen Sie über ein anfängliches Datenmodell aus Ihren Quellen (möglicherweise aus Ihrer Advertiser-Plattform-API). Um eine aggregierte Ansicht Ihrer Rohdaten zu erhalten, erstellen Sie ein Berichtseinblicke-Modell, wie in der Abbildung unten beschrieben. Dadurch kann ein Datensatz die oberen und unteren Grenzen der Zielgruppenübereinstimmung abrufen.

![Ein Entitäts-relationales Diagramm (ERD) des Zielgruppen-Insight-Benutzermodells.](../images/query-accelerated-store/audience-insight-user-model.png)

In diesem Beispiel wird die `externalaudiencereach` -Tabelle/Datensatz basiert auf einer ID und verfolgt die unteren und oberen Grenzen für die Anzahl der Treffer. Die `externalaudiencemapping` -Dimensionstabelle/-datensatz ordnet die externe ID einem Ziel und Segment in Platform zu.

## Erstellen eines Modells für die Berichterstellung von Einblicken mit Data Distiller

Erstellen Sie anschließend ein Insight-Berichtsmodell (`audienceinsight` in diesem Beispiel) und verwenden Sie den SQL-Befehl `ACCOUNT=acp_query_batch and TYPE=QSACCEL` , um sicherzustellen, dass sie im beschleunigten Speicher erstellt wird. Erstellen Sie dann mit Query Service eine `audienceinsight.audiencemodel` -Schema für `audienceinsight` Datenbank.

>[!NOTE]
>
>Die Data Distiller-SKU ist für die `ACCOUNT=acp_query_batch` Befehl. Andernfalls wird ein reguläres Datenmodell auf dem Data Lake erstellt.

```sql
CREATE database audienceinsight WITH (TYPE=QSACCEL, ACCOUNT=acp_query_batch);
 
CREATE schema audienceinsight.audiencemodel;
```

## Tabellen, Beziehungen und Daten erstellen

Nachdem Sie Ihre `audienceinsight` Reporting-Insight-Modell, erstellen Sie die `externalaudiencereach` und `externalaudiencemapping` Tabellen erstellen und Beziehungen zwischen ihnen herstellen. Verwenden Sie als Nächstes das `ALTER TABLE` -Befehl, um eine Fremdschlüsseleinschränkung zwischen den Tabellen hinzuzufügen und eine Beziehung zu definieren. Das folgende SQL-Beispiel zeigt, wie dies funktioniert.

```sql
CREATE TABLE IF NOT exists audienceinsight.audiencemodel.externalaudiencereach
WITH ( DISTRIBUTION = REPLICATE ) AS
  SELECT cast(null as int) approximate_count_upper_bound,
         cast(null as string) deliverystatusdescription,
         cast(null as timestamp)  timeupdated ,
         cast(null as int) operationstatuscode ,
         cast(null as string) operationstatusdescription,
         cast(null as int) approximate_count_lower_bound,
         cast(null as timestamp)timecreated ,
         cast(null as timestamp)timecontentupdated ,
         cast(null as int) deliverystatuscode ,
         cast(null as int)  ext_custom_audience_id
   WHERE false;
 
CREATE TABLE IF NOT exists audienceinsight.audiencemodel.externalaudiencemapping
WITH ( DISTRIBUTION = REPLICATE ) AS
SELECT cast(null as int) segment_id,
       cast(null as int) destination_id,
       cast(null as int) ext_custom_audience_id
 WHERE false;
 
ALTER TABLE externalaudiencereach ADD  CONSTRAINT FOREIGN KEY (ext_custom_audience_id) REFERENCES externalaudiencemapping (ext_custom_audience_id) NOT enforced;
```

Nach erfolgreicher Ausführung beider `ALTER TABLE` -Befehle, wird die Beziehung zwischen den Fakt- und den Dimensionstabellen gebildet.

Sobald die Anweisungen ausgeführt wurden, verwenden Sie die `SHOW datagroups;` -Befehl, um eine Liste der verfügbaren Datensätze im beschleunigten Speicher aus dem `audienceinsight.audiencemodel`. Ihre tabellarischen Ergebnisse sollten dem unten angegebenen Beispiel ähneln.

>[!IMPORTANT]
>
>Über den API-Endpunkt &quot;Zustandslos&quot;von Query Service können nur Daten im beschleunigten Speicher aufgerufen werden `POST /data/foundation/query/accelerated-queries`.

```console
    Database     |    Schema     | GroupType |      ChildType       |        ChildName        | PhysicalParent |               ChildId               
-----------------+---------------+-----------+----------------------+-------------------------+----------------+--------------------------------------
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencemapping | true           | 9155d3b4-889d-41da-9014-5b174f6fa572
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencereach   | true           | 1b941a6d-6214-4810-815c-81c497a0b636
```

## Abfragen des Reporting-Insight-Datenmodells

Query Service zum Abfragen der `audiencemodel.externalaudiencereach` Dimensionstabelle. Nachfolgend finden Sie eine Beispielabfrage.

```sql
SELECT a.ext_custom_audience_id,
       a.approximate_count_upper_bound
FROM   audiencemodel.externalaudiencereach AS a
       LEFT OUTER JOIN audiencemodel.externalaudiencemapping AS b
                    ON ( ( a.ext_custom_audience_id ) =
                         ( b.ext_custom_audience_id ) )
GROUP  BY a.ext_custom_audience_id,
          a.approximate_count_upper_bound
LIMIT  5000 ;
```

Die tabellarischen Ergebnisse umfassen eine Zählung und eine ID.

```console
ext_custom_audience_id | approximate_count_upper_bound
------------------------+-------------------------------
 23850912218170554      |                          1000
 23850808585120554      |                       1012000
 23850808585220554      |                        100000
 23850814978560554      |                          1000
 23850808585180554      |                        421000
 23850814978510554      |                       3001000
 23850814978530554      |                        300000
 23850912218160554      |                        105000
 23850808584990554      |                          1000
 23850809520110554      |                          1000
(10 rows)
```

## Erweitern Ihres Datenmodells mit dem Real-Time CDP Insight-Datenmodell

Sie können Ihr Zielgruppenmodell um zusätzliche Details erweitern, um eine reichere Dimensionstabelle zu erstellen. Sie können beispielsweise den Segmentnamen und den Zielnamen der externen Zielgruppenkennung zuordnen. Verwenden Sie dazu Query Service , um einen neuen Datensatz zu erstellen oder zu aktualisieren und ihn zum Zielgruppenmodell hinzuzufügen, das Segmente und Ziele mit einer externen Identität kombiniert. Das folgende Diagramm zeigt das Konzept dieser Datenmodellerweiterung.

![Ein ERD-Diagramm, das das Real-Time CDP Insight-Datenmodell mit dem Query Accelerated Store-Modell verknüpft.](../images/query-accelerated-store/updatingAudienceInsightUserModel.png)

## Erstellen von Dimensionstabellen zur Erweiterung Ihres Berichtseinblicke-Modells

Verwenden Sie Query Service, um wichtige beschreibende Attribute aus den angereicherten Real-Time CDP-Dimensionsdatensätzen zum `audienceinsight` Datenmodell erstellen und eine Beziehung zwischen Ihrer Faktentabelle und der neuen Dimensionstabelle herstellen. Die folgende SQL zeigt, wie Sie vorhandene Dimensionstabellen in Ihr Berichtseinblicke-Datenmodell integrieren.

```sql
CREATE TABLE audienceinsight.audiencemodel.external_seg_dest_map AS
  SELECT ext_custom_audience_id,
         destination_name,
         segment_name,
         destination_status,
         a.destination_id,
         a.segment_id
  FROM   externalaudiencemapping AS a
         LEFT OUTER JOIN adwh_dim_segments AS b
                      ON ( ( a.segment_id ) = ( b.segment_id ) )
         LEFT OUTER JOIN adwh_dim_destination AS c
                      ON ( ( a.destination_id ) = ( c.destination_id ) );
 
ALTER TABLE externalaudiencereach  ADD  CONSTRAINT FOREIGN KEY (ext_custom_audience_id) REFERENCES external_seg_dest_map (ext_custom_audience_id) NOT enforced;
```

Verwenden Sie die `SHOW datagroups;` -Befehl, um die Erstellung des zusätzlichen `external_seg_dest_map` Dimensionstabelle.

```console
    Database     |     Schema     | GroupType |      ChildType       |                ChildName  | PhysicalParent |               ChildId               
-----------------+----------------+-----------+----------------------+----------------------------------------------------+----------------+--------------------------------------
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | external_seg_dest_map      | true           | 4b4b86b7-2db7-48ee-a67e-4b28cb900810
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencemapping    | true           | b0302c05-28c3-488b-a048-1c635d88dca9
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencereach      | true           | 4485c610-7424-4ed6-8317-eed0991b9727
```

## Abfragen Ihres erweiterten Datenmodells für die schnelleren Speicherberichterstellung

Nun, dass `audienceinsight` Das Datenmodell wurde erweitert und kann abgefragt werden. Die folgende SQL-Tabelle zeigt die Liste der zugeordneten Ziele und Segmente.

```sql
SELECT a.ext_custom_audience_id,
       b.destination_name,
       b.segment_name,
       b.destination_status,
       b.destination_id,
       b.segment_id
FROM   audiencemodel.externalaudiencereach1 AS a
       LEFT OUTER JOIN audiencemodel.external_seg_dest_map AS b
                    ON ( ( a.ext_custom_audience_id ) = (
                         b.ext_custom_audience_id ) )
LIMIT  25; 
```

Die Abfrage gibt alle Datensätze im Abfrage-beschleunigten Speicher zurück:

```console
ext_custom_audience_id | destination_name |       segment_name        | destination_status | destination_id | segment_id 
------------------------+------------------+---------------------------+--------------------+----------------+-------------
 23850808595110554      | FCA_Test2        | United States             | enabled            |     -605911558 | -1357046572
 23850799115800554      | FCA_Test2        | Born in 1980s             | enabled            |     -605911558 | -1224554872
 23850799115790554      | FCA_Test2        | Born in 1970s             | enabled            |     -605911558 |  1899603869
 23850798177620554      | FCA_Test1        | Billionaires              | enabled            |      321720439 |  1401872665
 23850814978560554      | FCA_Test3        | Canada - Saskatchewan     | enabled            |     1182494936 | -1917996562
 23850808585180554      | FCA_Test3        | United States             | enabled            |     1182494936 | -1357046572
 23850814978530554      | FCA_Test3        | Canada - British Columbia | enabled            |     1182494936 |  -652840507
 23850808585120554      | FCA_Test3        | Canada - Quebec           | enabled            |     1182494936 |  -519557860
 23850809520110554      | FCA_Test3        | Born in 1960s             | enabled            |     1182494936 |   237824266
 23850808585220554      | FCA_Test3        | Western Canada            | enabled            |     1182494936 |  1075937528
 23850808584990554      | FCA_Test3        | Canada - Ontario          | enabled            |     1182494936 |  1593438041
 23850814978510554      | FCA_Test3        | Canada - Alberta          | enabled            |     1182494936 |  1862946783
 23850912218170554      | FCA_Test4        | Canada - Alberta          | enabled            |     1549248886 |  1862946783
 23850912218160554      | FCA_Test4        | Born in 1970s             | enabled            |     1549248886 |  1899603869
```

## Daten mit benutzerdefinierten Dashboards visualisieren

Nachdem Sie Ihr benutzerdefiniertes Datenmodell erstellt haben, können Sie Ihre Daten mit benutzerdefinierten Abfragen und benutzerdefinierten Dashboards visualisieren.

Die folgende SQL-Tabelle enthält eine Aufschlüsselung der Übereinstimmungsanzahl nach Zielgruppen in einem Ziel und eine Aufschlüsselung der einzelnen Zielgruppen nach Segment.

```sql
SELECT b.destination_name,
       a.approximate_count_upper_bound,
       b.segment_name
FROM   audiencemodel.externalaudiencereach AS a
       LEFT OUTER JOIN audiencemodel.external_seg_dest_map AS b
                    ON ( ( a.ext_custom_audience_id ) = (
                         b.ext_custom_audience_id ) )
GROUP  BY b.destination_name,
          a.approximate_count_upper_bound,
          b.segment_name
ORDER BY b.destination_name
LIMIT  5000
```

Das folgende Bild bietet ein Beispiel für mögliche benutzerdefinierte Visualisierungen mithilfe Ihres Berichtseinblicke-Datenmodells.

![Eine Übereinstimmungszählung nach Ziel und Segment-Widget, das aus dem neuen Berichtseinblicke-Datenmodell erstellt wurde.](../images/query-accelerated-store/user-defined-dashboard-widget.png)

Ihr benutzerdefiniertes Datenmodell finden Sie in der Liste der verfügbaren Datenmodelle im benutzerdefinierten Dashboard-Arbeitsbereich. Siehe [Benutzerhandbuch zu benutzerdefinierten Dashboards](../../dashboards/user-defined-dashboards.md) für Anleitungen zur Verwendung Ihres benutzerdefinierten Datenmodells.
