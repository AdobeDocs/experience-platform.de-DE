---
title: Anleitung zu Query Accelerated Store Reporting Insights
description: Erfahren Sie, wie Sie mit dem Abfrage-Service ein Reporting-Insights-Datenmodell zur Verwendung mit beschleunigten Speicherdaten und benutzerdefinierten Dashboards erstellen.
exl-id: 216d76a3-9ea3-43d3-ab6f-23d561831048
source-git-commit: 037ea8d11bb94e3b4f71ea301a535677b3cccdbd
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 84%

---

# Reporting-Insights des abfragebeschleunigten Speichers Handbuch

Mit dem abfragebeschleunigten Speicher können Sie die Zeit und die Verarbeitungsleistung reduzieren, die erforderlich sind, um entscheidende Erkenntnisse aus Ihren Daten zu gewinnen. Normalerweise werden die Daten in regelmäßigen Abständen (beipielsweise stündlich oder täglich) verarbeitet, wobei aggregierte Ansichten erstellt und in Berichten wiedergegeben werden. Die Analyse dieser aus den aggregierten Daten erstellten Berichte führt zu Insights, die zur Verbesserung der Unternehmensleistung beitragen sollen. Der abfragebeschleunigte Speicher bietet einen Cache-Service, Gleichzeitigkeit, Interaktivität und eine zustandslose API. Es wird jedoch davon ausgegangen, dass die Daten vorverarbeitet und für aggregierte Abfragen optimiert sind und nicht für die Abfrage von Rohdaten.

Mit dem Abfrage-beschleunigten Speicher können Sie ein benutzerdefiniertes Datenmodell erstellen und/oder ein vorhandenes Adobe Real-time Customer Data Platform-Datenmodell erweitern. Die gewonnenen Reporting-Insights können Sie dann in ein Reporting-/Visualisierungs-Framework Ihrer Wahl einbetten. Siehe die Dokumentation zum Real-time Customer Data Platform Insights-Datenmodell, um zu erfahren, wie Sie [Ihre SQL-Abfragevorlagen anpassen können, um Real-Time CDP-Berichte für Ihre Marketing- und KPI-Anwendungsfälle zu erstellen.](../../../dashboards/cdp-insights-data-model.md).

Das Real-Time CDP-Datenmodell von Adobe Experience Platform bietet Einblicke in Profile, Zielgruppen und Ziele und ermöglicht die Real-Time CDP-Insight-Dashboards. Dieses Dokument führt Sie durch den Prozess der Erstellung Ihres Reporting-Insights-Datenmodells und zeigt Ihnen, wie Sie Real-Time CDP-Datenmodelle bei Bedarf erweitern können.

## Voraussetzungen

In diesem Tutorial werden benutzerdefinierte Dashboards verwendet, um Daten aus Ihrem benutzerdefinierten Datenmodell innerhalb der Platform-Benutzeroberfläche zu visualisieren. Weitere Informationen zu dieser Funktion finden Sie in der [Dokumentation zu benutzerdefinierten Dashboards](../../../dashboards/user-defined-dashboards.md).

## Erste Schritte

Die Data Distiller SKU ist erforderlich, um ein benutzerdefiniertes Datenmodell für Ihre Reporting-Insights zu erstellen und um die Real-Time CDP-Datenmodelle zu erweitern, die angereicherte Platform-Daten enthalten. Bitte beachten Sie die Dokumentation zu [Packaging](../../packaging.md), [Leitplanken](../../guardrails.md#query-accelerated-store) und [Lizenzierung](../../data-distiller/license-usage.md), die sich auf die Data Distiller SKU bezieht. Wenn Sie nicht über die Data Distiller SKU verfügen, wenden Sie sich bitte an den Adobe-Support, um weitere Informationen zu erhalten.

## Erstellen eines Reporting-Insights-Datenmodells

In diesem Tutorial wird ein Beispiel für den Aufbau eines Audience-Insight-Datenmodells verwendet. Wenn Sie eine oder mehrere Advertiser-Plattformen verwenden, um Ihre Audience zu erreichen, können Sie die API des Advertisers verwenden, um eine ungefähre Anzahl von Übereinstimmungen mit Ihrer Audience zu erhalten.

Zu Beginn verfügen Sie über ein erstes Datenmodell aus Ihren Quellen (möglicherweise aus Ihrer Advertiser-Plattform-API). Um eine aggregierte Ansicht Ihrer Rohdaten zu erhalten, erstellen Sie ein Reporting-Insights-Modell wie in der folgenden Abbildung beschrieben. So kann ein Datensatz die oberen und unteren Grenzen der Audience-Übereinstimmung ermitteln.

![Ein Entitäts-Relations-Diagramm (ERD) des Audience-Insight-Benutzermodells.](../../images/query-accelerated-store/audience-insight-user-model.png)

In diesem Beispiel basiert die Tabelle/der Datensatz `externalaudiencereach` auf einer ID und verfolgt die unteren und oberen Grenzen für die Anzahl der Treffer. Die `externalaudiencemapping` -Dimensionstabelle/-datensatz ordnet die externe ID einem Ziel und einer Zielgruppe in Platform zu.

## Erstellen eines Modells für Reporting-Insights mit Data Distiller

Als Nächstes erstellen Sie ein Reporting-Insights-Modell (in diesem Beispiel `audienceinsight`) und verwenden den SQL-Befehl `ACCOUNT=acp_query_batch and TYPE=QSACCEL`, um sicherzustellen, dass es in dem beschleunigten Speicher erstellt wird. Verwenden Sie dann den Abfrage-Service, um ein Schema `audienceinsight.audiencemodel` für die `audienceinsight`-Datenbank zu erstellen.

>[!NOTE]
>
>Die Data Distiller SKU ist für den Befehl `ACCOUNT=acp_query_batch` erforderlich. Ohne sie wird ein reguläres Datenmodell auf dem Data Lake erstellt.

```sql
CREATE database audienceinsight WITH (TYPE=QSACCEL, ACCOUNT=acp_query_batch);
 
CREATE schema audienceinsight.audiencemodel;
```

## Erstellen von Tabellen und Beziehungen und Auffüllen von Daten

Nachdem Sie nun Ihr Reporting-Insights-Modell `audienceinsight` erstellt haben, erstellen Sie die Tabellen `externalaudiencereach` und `externalaudiencemapping` und legen Beziehungen zwischen ihnen fest. Als Nächstes verwenden Sie den Befehl `ALTER TABLE`, um eine Fremdschlüssel-Begrenzung zwischen den Tabellen hinzuzufügen und eine Beziehung zu definieren. Das folgende SQL-Beispiel veranschaulicht, wie dies funktioniert.

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
SELECT cast(null as int) audience_id,
       cast(null as int) destination_id,
       cast(null as int) ext_custom_audience_id
 WHERE false;
 
ALTER TABLE externalaudiencereach ADD  CONSTRAINT FOREIGN KEY (ext_custom_audience_id) REFERENCES externalaudiencemapping (ext_custom_audience_id) NOT enforced;
```

Nach erfolgreicher Ausführung der beiden `ALTER TABLE`-Befehle ist die Beziehung zwischen den Fakten- und Dimensionstabellen hergestellt.

Sobald die Anweisungen ausgeführt wurden, verwenden Sie den Befehl `SHOW datagroups;`, um eine Liste der verfügbaren Datensätze im beschleunigten Speicher von `audienceinsight.audiencemodel` anzuzeigen. Ihre tabellarischen Ergebnisse sollten dem unten angegebenen Beispiel ähneln.

>[!IMPORTANT]
>
>Über den zustandslosen API-Endpunkt `POST /data/foundation/query/accelerated-queries` des Abfrage-Services ist nur der Zugriff auf Daten im beschleunigten Speicher möglich.

```console
    Database     |    Schema     | GroupType |      ChildType       |        ChildName        | PhysicalParent |               ChildId               
-----------------+---------------+-----------+----------------------+-------------------------+----------------+--------------------------------------
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencemapping | true           | 9155d3b4-889d-41da-9014-5b174f6fa572
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencereach   | true           | 1b941a6d-6214-4810-815c-81c497a0b636
```

## Abfrage des Reporting-Insights-Datenmodells

Verwenden Sie den Abfrage-Service, um die Dimensionstabelle `audiencemodel.externalaudiencereach` abzufragen. Nachfolgend finden Sie eine Beispielabfrage.

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

Die tabellarischen Ergebnisse enthalten eine Anzahl und eine ID.

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

## Erweitern Ihres Datenmodells mit dem Real-Time CDP Insights-Datenmodell

Sie können Ihr Zielgruppenmodell mit zusätzlichen Details erweitern, um eine umfangreichere Dimensionstabelle zu erstellen. Sie können beispielsweise den Zielgruppennamen und Zielnamen der externen Zielgruppenkennung zuordnen. Verwenden Sie dazu Query Service , um einen neuen Datensatz zu erstellen oder zu aktualisieren und ihn zum Zielgruppenmodell hinzuzufügen, das Zielgruppen und Ziele mit einer externen Identität kombiniert. Das folgende Diagramm veranschaulicht das Konzept dieser Datenmodellerweiterung.

![Ein ERD-Diagramm, das das Real-Time CDP-Insight-Datenmodell und das abfragebeschleunigte Speichermodell verbindet.](../../images/query-accelerated-store/updatingAudienceInsightUserModel.png)

## Erstellen von Dimensionstabellen, um Ihr Reporting-Insights-Modell zu erweitern

Verwenden Sie den Abfrage-Service, um wichtige beschreibende Attribute aus den angereicherten Real-Time CDP-Dimensions-Datensätzen zum `audienceinsight`-Datenmodell hinzuzufügen und eine Beziehung zwischen Ihrer Faktentabelle und der neuen Dimensionstabelle herzustellen. Die folgende SQL-Anweisung zeigt, wie Sie bestehende Dimensionstabellen in Ihr Reporting-Insights-Datenmodell integrieren können.

```sql
CREATE TABLE audienceinsight.audiencemodel.external_seg_dest_map AS
  SELECT ext_custom_audience_id,
         destination_name,
         audience_name,
         destination_status,
         a.destination_id,
         a.audience_id
  FROM   externalaudiencemapping AS a
         LEFT OUTER JOIN adwh_dim_audiences AS b
                      ON ( ( a.audience_id ) = ( b.audience_id ) )
         LEFT OUTER JOIN adwh_dim_destination AS c
                      ON ( ( a.destination_id ) = ( c.destination_id ) );
 
ALTER TABLE externalaudiencereach  ADD  CONSTRAINT FOREIGN KEY (ext_custom_audience_id) REFERENCES external_seg_dest_map (ext_custom_audience_id) NOT enforced;
```

Verwenden Sie den Befehl `SHOW datagroups;`, um die Erstellung der zusätzlichen Dimensionstabelle `external_seg_dest_map` zu bestätigen.

```console
    Database     |     Schema     | GroupType |      ChildType       |                ChildName  | PhysicalParent |               ChildId               
-----------------+----------------+-----------+----------------------+----------------------------------------------------+----------------+--------------------------------------
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | external_seg_dest_map      | true           | 4b4b86b7-2db7-48ee-a67e-4b28cb900810
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencemapping    | true           | b0302c05-28c3-488b-a048-1c635d88dca9
 audienceinsight | audiencemodel | QSACCEL   | Data Warehouse Table | externalaudiencereach      | true           | 4485c610-7424-4ed6-8317-eed0991b9727
```

## Abfragen Ihres erweiterten Reporting-Insights-Datenmodells mit beschleunigtem Speicher

Nachdem das `audienceinsight`-Datenmodell erweitert wurde, kann es nun abgefragt werden. Die folgende SQL-Tabelle zeigt die Liste der zugeordneten Ziele und Zielgruppen.

```sql
SELECT a.ext_custom_audience_id,
       b.destination_name,
       b.audience_name,
       b.destination_status,
       b.destination_id,
       b.audience_id
FROM   audiencemodel.externalaudiencereach1 AS a
       LEFT OUTER JOIN audiencemodel.external_seg_dest_map AS b
                    ON ( ( a.ext_custom_audience_id ) = (
                         b.ext_custom_audience_id ) )
LIMIT  25; 
```

Die Abfrage gibt alle Datensätze des abfragebeschleunigten Speichers zurück:

```console
ext_custom_audience_id | destination_name |       audience_name        | destination_status | destination_id | audience_id 
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

## Visualisieren Ihrer Daten mit benutzerdefinierten Dashboards

Nachdem Sie Ihr benutzerdefiniertes Datenmodell erstellt haben, können Sie Ihre Daten mit benutzerdefinierten Abfragen und benutzerdefinierten Dashboards visualisieren.

Die folgende SQL-Tabelle enthält eine Aufschlüsselung der Übereinstimmungsanzahl nach Zielgruppen in einem Ziel und eine Aufschlüsselung der einzelnen Zielgruppen nach Zielgruppen.

```sql
SELECT b.destination_name,
       a.approximate_count_upper_bound,
       b.audience_name
FROM   audiencemodel.externalaudiencereach AS a
       LEFT OUTER JOIN audiencemodel.external_seg_dest_map AS b
                    ON ( ( a.ext_custom_audience_id ) = (
                         b.ext_custom_audience_id ) )
GROUP  BY b.destination_name,
          a.approximate_count_upper_bound,
          b.audience_name
ORDER BY b.destination_name
LIMIT  5000
```

Die folgende Abbildung zeigt ein Beispiel für die möglichen benutzerdefinierten Visualisierungen unter Verwendung Ihres Reporting-Insights-Datenmodells.

![Eine Übereinstimmungszählung nach Ziel und Zielgruppen-Widget, das aus dem neuen Datenmodell der Berichtseinblicke erstellt wurde.](../../images/query-accelerated-store/user-defined-dashboard-widget.png)

Ihr benutzerdefiniertes Datenmodell ist in der Liste der verfügbaren Datenmodelle im benutzerdefinierten Dashboard-Arbeitsbereich zu finden. Eine Anleitung zur Verwendung Ihres benutzerdefinierten Datenmodells finden Sie im [Handbuch zum benutzerdefinierten Dashboard](../../../dashboards/user-defined-dashboards.md).
