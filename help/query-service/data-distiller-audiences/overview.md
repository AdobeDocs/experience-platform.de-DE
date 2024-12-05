---
title: Erstellen von Zielgruppen mit SQL
description: Erfahren Sie, wie Sie mit der SQL-Zielgruppenerweiterung in Adobe Experience Platform Data Distiller Zielgruppen mit SQL-Befehlen erstellen, verwalten und veröffentlichen können. In diesem Handbuch werden alle Aspekte des Zielgruppen-Lebenszyklus behandelt, einschließlich Erstellung, Aktualisierung und Löschung von Profilen und Verwendung datengesteuerter Zielgruppendefinitionen für dateibasierte Ziele.
exl-id: c35757c1-898e-4d65-aeca-4f7113173473
source-git-commit: 7db055f598e3fa7d5a50214a0cfa86e28e5bfe47
workflow-type: tm+mt
source-wordcount: '1481'
ht-degree: 1%

---

# Erstellen von Zielgruppen mit SQL

Verwenden Sie die SQL-Zielgruppenerweiterung, um Zielgruppen mit Daten aus dem Data Lake zu erstellen, einschließlich vorhandener Dimensionselemente (z. B. Kundenattribute oder Produktinformationen).

Die Verwendung dieser SQL-Erweiterung verbessert Ihre Fähigkeit, Zielgruppen zu erstellen, da Sie beim Definieren von Zielgruppensegmenten keine Rohdaten in Ihren Profilen benötigen. Mit dieser Methode erstellte Zielgruppen werden automatisch im Arbeitsbereich &quot;Zielgruppe&quot;registriert, wo Sie sie weiter an dateibasierte Ziele ausrichten können.

![Infografik, die den Workflow für die SQL-Zielgruppenerweiterung anzeigt. Zu den Phasen gehören das Erstellen von Zielgruppen mit dem Query Service mithilfe von SQL-Befehlen, deren Verwaltung in der Platform-Benutzeroberfläche, das Aktivieren dieser Zielgruppen in dateibasierten Zielen.](../images/data-distiller/sql-audiences/sql-audience-extension-workflow.png)

In diesem Dokument wird beschrieben, wie Sie die SQL-Zielgruppenerweiterung in Adobe Experience Platform Data Distiller verwenden, um Zielgruppen mit SQL-Befehlen zu erstellen, zu verwalten und zu veröffentlichen.

## Lebenszyklus der Zielgruppenerstellung in Data Distiller {#audience-creation-lifecycle}

Führen Sie diese Schritte aus, um Zielgruppen zu erstellen, zu verwalten und zu aktivieren. Die erstellten Zielgruppen werden nahtlos in den &quot;Zielgruppenfluss&quot;integriert, sodass Sie Segmente aus Basiszielgruppen und dateibasierten Zielen (z. B. CSV-Uploads oder Cloud-Speicher-Standorte) erstellen können, um Kundenkontakte zu ermöglichen. &quot;Zielgruppenfluss&quot;bezieht sich auf den gesamten Prozess der Erstellung, Verwaltung und Aktivierung von Zielgruppen, um eine nahtlose Integration über Ziele hinweg sicherzustellen.

Verwenden Sie als Teil Ihres &quot;Zielgruppenflusses&quot;die folgenden SQL-Befehle für die Zielgruppen [create](#create-audience), [modify](#add-profiles-to-audience) und [delete](#delete-audience) in Adobe Experience Platform.

### Erstellen einer Zielgruppe {#create-audience}

Verwenden Sie den Befehl `CREATE AUDIENCE AS SELECT` , um eine neue Zielgruppe zu definieren. Die erstellte Zielgruppe wird in einem Datensatz gespeichert und im Arbeitsbereich [!UICONTROL Zielgruppen] unter Data Distiller registriert.

```sql
CREATE AUDIENCE table_name  
WITH (primary_identity='IdentitycolName', identity_namespace='Namespace for the identity used', [schema='target_schema_title'])
AS (select_query)
```

**Parameter**

Verwenden Sie diese Parameter, um Ihre SQL-Zielgruppen-Erstellungsabfrage zu definieren:

| Parameter | Beschreibung |
|--------------------|------------------------------------------------------------------|
| `schema` | Optional. Definiert das XDM-Schema für den Datensatz, der von der Abfrage erstellt wird. |
| `table_name` | Name der Tabelle und Zielgruppe. |
| `primary_identity` | Gibt die primäre Identitätsspalte für die Zielgruppe an. |
| `identity_namespace` | Namespace der Identität. Sie können einen vorhandenen Namespace verwenden oder einen neuen erstellen. Verwenden Sie den Befehl `SHOW NAMESPACE` , um verfügbare Namespaces anzuzeigen. Verwenden Sie `CREATE NAMESPACE`, um einen neuen Namespace zu erstellen. Beispiel: `CREATE NAMESPACE lumaCrmId WITH (code='testns', TYPE='Email')`. |
| `select_query` | Eine SELECT-Anweisung, die die Audience definiert. Die Syntax der SELECT-Abfrage finden Sie im Abschnitt [SELECT-Abfragen](../sql/syntax.md#select-queries) . |

{style="table-layout:auto"}

>[!NOTE]
>
>Um komplexe Datenstrukturen flexibler zu gestalten, können Sie beim Definieren von Zielgruppen angereicherte Attribute verschachteln. Angereicherte Attribute wie `orders`, `total_revenue`, `recency`, `frequency` und `monetization` können verwendet werden, um Zielgruppen nach Bedarf zu filtern.

**Beispiel:**

Das folgende Beispiel zeigt, wie Sie Ihre SQL-Zielgruppen-Erstellungsabfrage strukturieren:

```sql
CREATE Audience aud_test
WITH (primary_identity=userId, identity_namespace=lumaCrmId)
AS SELECT userId, orders, total_revenue, recency, frequency, monetization FROM profile_dim_customer;
```

In diesem Beispiel wird die Spalte `userId` als Identitätsspalte identifiziert und ein entsprechender Namespace (`lumaCrmId`) zugewiesen. Die verbleibenden Spalten (`orders`, `total_revenue`, `recency`, `frequency` und `monetization`) sind angereicherte Attribute, die zusätzlichen Kontext für die Zielgruppe bieten.

**Einschränkungen:**

Beachten Sie die folgenden Einschränkungen bei der Verwendung von SQL für die Erstellung von Zielgruppen:

- Die primäre Identitätsspalte **muss** auf der obersten Ebene des Datensatzes liegen, ohne in andere Attribute oder Kategorien verschachtelt zu sein.
- Externe Zielgruppen, die mit SQL-Befehlen erstellt wurden, haben eine Aufbewahrungsfrist von 30 Tagen. Nach 30 Tagen werden diese Zielgruppen automatisch gelöscht, was eine wichtige Überlegung bei der Planung von Zielgruppen-Management-Strategien ist.

### Profile zu einer existierenden Zielgruppe hinzufügen {#add-profiles-to-audience}

Verwenden Sie den Befehl `INSERT INTO` , um einer vorhandenen Zielgruppe Profile (oder ganze Zielgruppen) hinzuzufügen.

```sql
INSERT INTO table_name
SELECT select_query
```

**Parameter**

In der folgenden Tabelle werden die Parameter erläutert, die für den Befehl `INSERT INTO` erforderlich sind:

| Parameter | Beschreibung |
|----------------|--------------------------------------------------------------------------------|
| `table_name` | Der Name der Tabelle, die im Rahmen des Befehls Zielgruppe erstellen erstellt wurde. |
| `select_query` | Eine SELECT-Anweisung. Die Syntax der SELECT-Abfrage finden Sie im Abschnitt SELECT-Abfragen . |

{style="table-layout:auto"}

**Beispiel:**

Im folgenden Beispiel wird gezeigt, wie mit dem Befehl `INSERT INTO` Profile zu einer vorhandenen Zielgruppe hinzugefügt werden:

```sql
INSERT INTO Audience aud_test
SELECT userId, orders, total_revenue, recency, frequency, monetization FROM customer_ds;
```

### Beispiel einer RFM-Modell-Audience {#rfm-model-audience-example}

Das folgende Beispiel zeigt, wie eine Zielgruppe mithilfe des Modells Neuigkeit, Häufigkeit und Monetarisierung (RFM) erstellt wird. In diesem Beispiel werden Kunden anhand ihrer Neuigkeits-, Häufigkeits- und Monetarisierungsbewertungen segmentiert, um wichtige Gruppen wie treue Kunden, neue Kunden und hochwertige Kunden zu identifizieren.

<!--  Q) Since the focus of this document is on external audiences, or should I just include this temporarily? We could simply provide a link to the separate RFM modeling documentation rather than including the full example here. (Add link to new RFM document when it is published) -->

Die folgende Abfrage erstellt ein Schema für die RFM-Audience. Die Anweisung richtet Felder ein, die Kundeninformationen wie `userId`, `days_since_last_purchase`, `orders`, `total_revenue` usw. enthalten.

```sql
CREATE Audience adls_rfm_profile
WITH (primary_identity=userId, identity_namespace=lumaCrmId) AS
SELECT
    cast(NULL AS string) userId,
    cast(NULL AS integer) days_since_last_purchase,
    cast(NULL AS integer) orders,
    cast(NULL AS decimal(18,2)) total_revenue,
    cast(NULL AS integer) recency,
    cast(NULL AS integer) frequency,
    cast(NULL AS integer) monetization,
    cast(NULL AS string) rfm_model
WHERE false;
```

Nachdem Sie die Audience erstellt haben, füllen Sie sie mit Kundendaten aus und segmentieren Sie die Profile anhand ihrer RFM-Bewertungen. Die folgende SQL-Anweisung verwendet die Funktion &quot;`NTILE(4)`&quot;, um Kunden anhand ihrer RFM-Werte (Neuigkeit, Häufigkeit, Monetarisierung) in Quartilen einzuordnen. Diese Bewertungen kategorisieren Kunden in sechs Segmente, z. B. &quot;Core&quot;, &quot;Loyal&quot;und &quot;Wale&quot;. Die segmentierten Kundendaten werden dann in die Audience `adls_rfm_profile` -Tabelle eingefügt.&quot;

```sql
INSERT INTO Audience adls_rfm_profile
SELECT
    userId,
    days_since_last_purchase,
    orders,
    total_revenue,
    recency,
    frequency,
    monetization,
    CASE
        WHEN Recency=1 AND Frequency=1 AND Monetization=1 THEN '1. Core - Your Best Customers'
        WHEN Recency IN(1,2,3,4) AND Frequency=1 AND Monetization IN (1,2,3,4) THEN '2. Loyal - Your Most Loyal Customers'
        WHEN Recency IN(1,2,3,4) AND Frequency IN (1,2,3,4) AND Monetization=1 THEN '3. Whales - Your Highest Paying Customers'
        WHEN Recency IN(1,2,3,4) AND Frequency IN(1,2,3) AND Monetization IN(2,3,4) THEN '4. Promising - Faithful Customers'
        WHEN Recency=1 AND Frequency=4 AND Monetization IN (1,2,3,4) THEN '5. Rookies - Your Newest Customers'
        WHEN Recency IN (2,3,4) AND Frequency=4 AND Monetization IN (1,2,3,4) THEN '6. Slipping - Once Loyal, Now Gone'
    END AS rfm_model
FROM (
    SELECT
        userId,
        days_since_last_purchase,
        orders,
        total_revenue,
        NTILE(4) OVER (ORDER BY days_since_last_purchase) AS recency,
        NTILE(4) OVER (ORDER BY orders DESC) AS frequency,
        NTILE(4) OVER (ORDER BY total_revenue DESC) AS monetization
    FROM (
        SELECT
            userid,
            DATEDIFF(current_date, MAX(purchase_date)) AS days_since_last_purchase,
            COUNT(purchaseid) AS orders,
            CAST(SUM(total_revenue) AS double) AS total_revenue
        FROM (
            SELECT DISTINCT
                ENDUSERIDS._EXPERIENCE.EMAILID.ID AS userid,
                commerce.`ORDER`.purchaseid AS purchaseid,
                commerce.`ORDER`.pricetotal AS total_revenue,
                TO_DATE(timestamp) AS purchase_date
            FROM sample_data_for_ootb_templates
            WHERE commerce.`ORDER`.purchaseid IS NOT NULL
        ) AS b
        GROUP BY userId
    )
);
```

### Löschen einer Zielgruppe (DROP-ZIELGRUPPE) {#delete-audience}

Verwenden Sie den Befehl `DROP AUDIENCE` , um eine vorhandene Zielgruppe zu löschen. Wenn die Zielgruppe nicht vorhanden ist, tritt eine Ausnahme auf, es sei denn, `IF EXISTS` ist angegeben.

```sql
DROP AUDIENCE [IF EXISTS] [db_name.]table_name
```

**Parameter**

Die Tabelle enthält die Parameter, die für den Befehl `DROP AUDIENCE` erforderlich sind:

| Parameter | Beschreibung |
|----------------|----------------------------------------------------------------------------------------|
| `IF EXISTS` | Optional. Wenn angegeben, wird für den Fall, dass die Tabelle nicht gefunden wird, keine Ausnahme ausgelöst. |
| `db_name` | Gibt die Datengruppe an, die zur Qualifizierung des Zielgruppendatensatzes verwendet wird. |
| `table_name` | Der Name der Tabelle, die im Rahmen des Befehls Zielgruppe erstellen erstellt wurde. |

{style="table-layout:auto"}

**Beispiel:**

Das folgende Beispiel zeigt, wie Sie eine Zielgruppe mithilfe des Befehls DROP AUDIENCE löschen:

```sql
DROP AUDIENCE IF EXISTS aud_test;
```

### Automatische Zielgruppenregistrierung und -verfügbarkeit {#registration-and-availability}

Mit der SQL-Erweiterung erstellte Zielgruppen werden automatisch unter Data Distiller [!UICONTROL Origin] im Audience Workspace registriert. Nach der Registrierung sind diese Zielgruppen für das Targeting in dateibasierten Zielen verfügbar, wodurch die Segmentierungs- und Targeting-Strategien verbessert werden. Dieser Prozess erfordert keine zusätzliche Konfiguration, die das Zielgruppen-Management optimiert. Weitere Informationen zum Anzeigen, Verwalten und Erstellen von Zielgruppen in der Platform-Benutzeroberfläche finden Sie in der [Übersicht über Audience Portal](../../segmentation/ui/audience-portal.md).

<!-- Q) Do you know how long it takes for the audience to register? This info would help manage user expectations. -->

![Der Arbeitsbereich &quot;Zielgruppe&quot;in Adobe Experience Platform, in dem Data Distiller-Zielgruppen automatisch veröffentlicht und einsatzbereit angezeigt werden.](../images/data-distiller/sql-audiences/audiences.png)

## Zielgruppen für Ziele aktivieren {#activate-audiences}

Aktivieren Sie Ihre Zielgruppen, indem Sie sie an ein beliebiges dateibasiertes Ziel wie [!DNL Amazon S3], [!DNL SFTP] oder [!DNL Azure Blob] richten. Die angereicherten Zielgruppenattribute stehen bei Bedarf zur weiteren Verfeinerung und Filterung zur Verfügung.

![Flussdiagramm der Adobe Experience Platform-Zieltypen mit öffentlichen und privaten/benutzerdefinierten Zielen, einschließlich Batch- und Streaming-Optionen.](../images/data-distiller/sql-audiences/destination-types.png)

## Funktionsklarationen {#faqs}

In diesem Abschnitt werden häufig gestellte Fragen zum Erstellen und Verwalten externer Zielgruppen mit SQL in Data Distiller behandelt.

**Fragen**:

- Wird die Zielgruppenerstellung nur für flache Datensätze unterstützt?

+++Antwort

Derzeit ist die Erstellung von Zielgruppen bei der Definition der Zielgruppe auf einfache Attribute (auf Stammebene) beschränkt.

+++

- Führt die Erstellung von Zielgruppen zu einem einzelnen Datensatz oder mehreren Datensätzen oder variiert die Erstellung je nach Konfiguration?

+++Antwort

Es gibt eine Eins-zu-Eins-Zuordnung zwischen einer Zielgruppe und einem Datensatz.

+++

- Ist der bei der Zielgruppenerstellung erstellte Datensatz für Profil markiert?

+++Antwort

Nein, der bei der Zielgruppenerstellung erstellte Datensatz ist nicht für Profil markiert.

+++

- Wird der Datensatz im Data Lake erstellt?

+++Antwort

Ja, der mit der Zielgruppe verknüpfte Datensatz wird im Data Lake erstellt. Die Attribute aus diesem Datensatz sind im Audience Composer und im Zielfluss als angereicherte Attribute verfügbar.

+++

- Sind Attribute in der Zielgruppe auf dateibasierte Enterprise-Batch-Ziele beschränkt? (Ja oder Nein)

+++Antwort

Nein. Angereicherte Attribute in der Zielgruppe stehen sowohl für Enterprise-Batch- als auch für dateibasierte Ziele zur Verfügung. Wenn ein Fehler wie &quot;Die folgenden Segment-IDs haben Namespaces, die für dieses Ziel nicht zulässig sind: e917f626-a038-42f7-944c-xyxyxyx&quot;auftritt, erstellen Sie ein neues Segment in Data Distiller und verwenden Sie es mit einem beliebigen verfügbaren Ziel.

+++

- Kann ich eine Audience von Zielgruppen erstellen, die eine Data Distiller-Audience verwenden?

+++Antwort

Ja, Sie können eine Audience von Audiences erstellen, die eine Data Distiller-Audience verwendet.

+++

- Werden diese Zielgruppen in Adobe Journey Optimizer angezeigt? Wenn nicht, was passiert, wenn ich im Regel-Builder eine neue Zielgruppe erstelle, die alle Mitglieder dieser Zielgruppe enthält?

+++Antwort

Data Distiller-Zielgruppen sind auch in Adobe Journey Optimizer verfügbar. Sie können Data Distiller-Zielgruppen in Adobe Journey Optimizer verwenden und die Ergebnisse anhand der angereicherten Attribute filtern.

+++

- Werden Data Distiller-Zielgruppen alle 30 Tage gelöscht, da es sich um externe Zielgruppen handelt?

+++Antwort

Ja, Data Distiller-Zielgruppen werden alle 30 Tage gelöscht, da es sich um externe Zielgruppen handelt.

+++

## Nächste Schritte

Nach dem Lesen dieses Dokuments haben Sie gelernt, wie Sie mit der SQL-Zielgruppenerweiterung in Data Distiller Zielgruppen mit SQL-Befehlen effektiv erstellen, verwalten und veröffentlichen können. Sie können jetzt Zielgruppendefinitionen auf Grundlage Ihrer individuellen Geschäftsanforderungen anpassen und sie über verschiedene Ziele hinweg aktivieren, um Ihre Marketing-Strategien und datengesteuerten Entscheidungen zu optimieren.

Als Nächstes können Sie die folgende Dokumentation lesen, um Ihre Zielgruppen-Management-Strategien für Platform weiter zu entwickeln und zu optimieren:

- **Zielgruppenbewertung durchsuchen**: Erfahren Sie mehr über die [Zielgruppenbewertungsmethoden in Adobe Experience Platform](../../segmentation/home.md#evaluate-segments): Streaming-Segmentierung für Echtzeitaktualisierungen, Batch-Segmentierung für geplante oder On-Demand-Verarbeitung und Kantensegmentierung für die sofortige Auswertung des Edge Networks.
- **Integrieren mit Zielen**: Lesen Sie das Handbuch zum [Exportieren von Dateien On-Demand an Batch-Ziele](../../destinations/ui/export-file-now.md) mithilfe der Benutzeroberfläche &quot;Platform Destinations&quot;.
- **Audience Performance überprüfen**: Analysieren Sie, wie Ihre SQL-definierten Zielgruppen über verschiedene Kanäle hinweg funktionieren. Verwenden Sie Dateneinblicke, um Ihre Zielgruppendefinitionen und Zielgruppenstrategien anzupassen und zu verbessern. Lesen Sie das Dokument zu [Zielgruppeneinblicken](../../dashboards/insights/audiences.md) , um zu erfahren, wie Sie auf die SQL-Abfragen für Zielgruppeneinblicke in Adobe Real-Time CDP zugreifen und diese anpassen können. Anschließend können Sie eigene Einblicke erstellen und Rohdaten in umsetzbare Informationen umwandeln, indem Sie das Zielgruppen-Dashboard anpassen, um diese Einblicke effektiv zu visualisieren und für eine bessere Entscheidungsfindung zu verwenden.

