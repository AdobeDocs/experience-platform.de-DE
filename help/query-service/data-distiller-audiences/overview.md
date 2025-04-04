---
title: Erstellen von Zielgruppen mithilfe von SQL
description: Erfahren Sie, wie Sie mit der SQL-Zielgruppenerweiterung in Adobe Experience Platform Data Distiller Zielgruppen mithilfe von SQL-Befehlen erstellen, verwalten und veröffentlichen können. Dieses Handbuch behandelt alle Aspekte des Zielgruppen-Lebenszyklus, einschließlich der Erstellung, Aktualisierung und Löschung von Profilen und der Verwendung datengesteuerter Zielgruppendefinitionen für dateibasierte Ziele.
exl-id: c35757c1-898e-4d65-aeca-4f7113173473
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1485'
ht-degree: 1%

---

# Erstellen von Zielgruppen mithilfe von SQL

Verwenden Sie die SQL-Audience-Erweiterung, um Zielgruppen mit Daten aus dem Data Lake zu erstellen, einschließlich vorhandener Dimensionsentitäten (z. B. Kundenattribute oder Produktinformationen).

Durch die Verwendung dieser SQL-Erweiterung können Sie besser Zielgruppen erstellen, da Sie beim Definieren von Zielgruppensegmenten keine Rohdaten in Ihren Profilen benötigen. Zielgruppen, die mit dieser Methode erstellt wurden, werden automatisch im Zielgruppen-Arbeitsbereich registriert, wo Sie sie weiter an dateibasierte Ziele anpassen können.

![Infografik mit dem Workflow der SQL-Zielgruppenerweiterung. Zu den Phasen gehören das Erstellen von Zielgruppen mit dem Abfrage-Service mithilfe von SQL-Befehlen, das Verwalten dieser Zielgruppen in der Experience Platform-Benutzeroberfläche und das Aktivieren dieser Zielgruppen in dateibasierten Zielen.](../images/data-distiller/sql-audiences/sql-audience-extension-workflow.png)

In diesem Dokument wird die Verwendung der SQL-Zielgruppenerweiterung in Adobe Experience Platform Data Distiller zum Erstellen, Verwalten und Veröffentlichen von Zielgruppen mithilfe von SQL-Befehlen beschrieben.

## Lebenszyklus der Zielgruppenerstellung in Data Distiller {#audience-creation-lifecycle}

Führen Sie diese Schritte aus, um Ihre Zielgruppen zu erstellen, zu verwalten und zu aktivieren. Erstellte Zielgruppen lassen sich nahtlos in den Zielgruppenfluss integrieren, sodass Sie Segmente aus Basiszielgruppen und dateibasierten Zielen (z. B. CSV-Uploads oder Cloud-Speicherorte) für die Kundenkontakte erstellen können. „Zielgruppenfluss“ bezieht sich auf den vollständigen Prozess der Erstellung, Verwaltung und Aktivierung von Zielgruppen, um eine nahtlose Integration über Ziele hinweg sicherzustellen.

Adobe Experience Platform Verwenden Sie im Rahmen Ihres „Zielgruppen-Flusses“ die folgenden SQL-Befehle[ um Zielgruppen in zu erstellen](#create-audience) zu [](#add-profiles-to-audience) und [löschen](#delete-audience).

### Erstellen einer Zielgruppe {#create-audience}

Verwenden Sie den Befehl `CREATE AUDIENCE AS SELECT` , um eine neue Audience zu definieren. Die erstellte Zielgruppe wird in einem Datensatz gespeichert und im Arbeitsbereich [!UICONTROL Zielgruppen] unter Data Distiller registriert.

```sql
CREATE AUDIENCE table_name  
WITH (primary_identity='IdentitycolName', identity_namespace='Namespace for the identity used', [schema='target_schema_title'])
AS (select_query)
```

**Parameter**

Verwenden Sie diese Parameter, um Ihre SQL-Zielgruppenerstellungsabfrage zu definieren:

| Parameter | Beschreibung |
|--------------------|------------------------------------------------------------------|
| `schema` | Optional. Definiert das XDM-Schema für den von der Abfrage erstellten Datensatz. |
| `table_name` | Name der Tabelle und Zielgruppe. |
| `primary_identity` | Gibt die primäre Identitätsspalte für die Zielgruppe an. |
| `identity_namespace` | Namespace der Identität. Sie können einen vorhandenen Namespace verwenden oder einen neuen erstellen. Um verfügbare Namespaces anzuzeigen, verwenden Sie den Befehl `SHOW NAMESPACES` . Um einen neuen Namespace zu erstellen, verwenden Sie `CREATE NAMESPACE`. Beispiel: `CREATE NAMESPACE lumaCrmId WITH (code='testns', TYPE='Email')`. |
| `select_query` | Eine SELECT-Anweisung, die die Audience definiert. Die Syntax der SELECT-Abfrage finden Sie im Abschnitt [SELECT](../sql/syntax.md#select-queries)Abfragen. |

{style="table-layout:auto"}

>[!NOTE]
>
>Um eine größere Flexibilität für komplexe Datenstrukturen zu bieten, können Sie beim Definieren von Zielgruppen angereicherte Attribute verschachteln. Angereicherte Attribute wie `orders`, `total_revenue`, `recency`, `frequency` und `monetization` können verwendet werden, um Zielgruppen nach Bedarf zu filtern.

**Beispiel:**

Das folgende Beispiel zeigt, wie Sie Ihre SQL-Zielgruppenerstellungsabfrage strukturieren:

```sql
CREATE Audience aud_test
WITH (primary_identity=userId, identity_namespace=lumaCrmId)
AS SELECT userId, orders, total_revenue, recency, frequency, monetization FROM profile_dim_customer;
```

In diesem Beispiel wird die Spalte `userId` als Identitätsspalte identifiziert und ein entsprechender Namespace (`lumaCrmId`) zugewiesen. Die übrigen Spalten (`orders`, `total_revenue`, `recency`, `frequency` und `monetization`) sind angereicherte Attribute, die zusätzlichen Kontext für die Zielgruppe bieten.

**Einschränkungen:**

Beachten Sie die folgenden Einschränkungen bei der Verwendung von SQL zur Erstellung von Zielgruppen:

- Die primäre Identitätsspalte **muss** auf der höchsten Ebene des Datensatzes sein, ohne in anderen Attributen oder Kategorien verschachtelt zu sein.
- Externe Zielgruppen, die mit SQL-Befehlen erstellt wurden, haben eine Aufbewahrungsfrist von 30 Tagen. Nach 30 Tagen werden diese Zielgruppen automatisch gelöscht, was eine wichtige Überlegung für die Planung von Zielgruppen-Management-Strategien ist.

### Hinzufügen von Profilen zu einer bestehenden Audience {#add-profiles-to-audience}

Mit dem Befehl `INSERT INTO` können Sie Profile (oder ganze Zielgruppen) zu einer bestehenden Zielgruppe hinzufügen.

```sql
INSERT INTO table_name
SELECT select_query
```

**Parameter**

In der folgenden Tabelle werden die für den `INSERT INTO`-Befehl erforderlichen Parameter erläutert:

| Parameter | Beschreibung |
|----------------|--------------------------------------------------------------------------------|
| `table_name` | Der Name der Tabelle, die im Rahmen des Befehls Zielgruppe erstellen erstellt wurde. |
| `select_query` | Eine SELECT-Anweisung. Die Syntax der SELECT-Abfrage finden Sie im Abschnitt SELECT-Abfragen . |

{style="table-layout:auto"}

**Beispiel:**

Das folgende Beispiel zeigt, wie Sie mit dem Befehl `INSERT INTO` Profile zu einer bestehenden Audience hinzufügen:

```sql
INSERT INTO Audience aud_test
SELECT userId, orders, total_revenue, recency, frequency, monetization FROM customer_ds;
```

### Beispiel für eine RFM-Modell-Zielgruppe {#rfm-model-audience-example}

Das folgende Beispiel zeigt, wie Sie eine Zielgruppe mithilfe des Modells „Neuigkeit“, „Häufigkeit“ und „Monetarisierung“ (RFM) erstellen. In diesem Beispiel werden Kunden anhand ihrer Aktualität, Häufigkeit und Monetarisierungswerte segmentiert, um Schlüsselgruppen wie treue Kunden, neue Kunden und hochwertige Kunden zu identifizieren.

<!--  Q) Since the focus of this document is on external audiences, or should I just include this temporarily? We could simply provide a link to the separate RFM modeling documentation rather than including the full example here. (Add link to new RFM document when it is published) -->

Die folgende Abfrage erstellt ein Schema für die RFM-Zielgruppe. Die Anweisung richtet Felder ein, in denen Kundeninformationen wie `userId`, `days_since_last_purchase`, `orders`, `total_revenue` usw. gespeichert werden.

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

Füllen Sie die Zielgruppe nach der Erstellung mit Kundendaten und segmentieren Sie die Profile anhand ihrer RFM-Bewertungen. Die folgende SQL-Anweisung verwendet die `NTILE(4)`-Funktion, um Kundinnen und Kunden basierend auf ihren RFM-Werten (Neuigkeit, Häufigkeit, Monetarisierung) in Quartile zu ordnen. Diese Werte kategorisieren Kundinnen und Kunden in sechs Segmente, z. B. „Core“, „Treu“ und „Wale“. Die segmentierten Kundendaten werden dann in die Tabelle der Zielgruppen-`adls_rfm_profile` eingefügt.“

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

### Löschen einer Zielgruppe (ZIELGRUPPE ABLEGEN) {#delete-audience}

Verwenden Sie den Befehl `DROP AUDIENCE` , um eine vorhandene Zielgruppe zu löschen. Wenn die Zielgruppe nicht vorhanden ist, tritt eine Ausnahme auf, es sei denn, `IF EXISTS` wird angegeben.

```sql
DROP AUDIENCE [IF EXISTS] [db_name.]table_name
```

**Parameter**

Die Tabelle enthält die für den `DROP AUDIENCE`-Befehl erforderlichen Parameter:

| Parameter | Beschreibung |
|----------------|----------------------------------------------------------------------------------------|
| `IF EXISTS` | Optional. Wenn angegeben, wird für den Fall, dass die Tabelle nicht gefunden wird, keine Ausnahme ausgelöst. |
| `db_name` | Gibt die Datengruppe an, die zum Qualifizieren des Zielgruppen-Datensatzes verwendet wird. |
| `table_name` | Der Name der Tabelle, die im Rahmen des Befehls Zielgruppe erstellen erstellt wurde. |

{style="table-layout:auto"}

**Beispiel:**

Das folgende Beispiel zeigt, wie Sie eine Zielgruppe mithilfe des Befehls ZIELGRUPPE ABLEGEN löschen:

```sql
DROP AUDIENCE IF EXISTS aud_test;
```

### Automatische Zielgruppenregistrierung und -verfügbarkeit {#registration-and-availability}

Audiences, die mit der SQL-Erweiterung erstellt wurden, werden automatisch unter der Data Distiller [!UICONTROL Origin] im Audience-Arbeitsbereich registriert. Nach der Registrierung stehen diese Zielgruppen für die Zielgruppenbestimmung in dateibasierten Zielen zur Verfügung, wodurch die Segmentierung und Zielgruppenbestimmungsstrategien verbessert werden. Dieser Prozess erfordert keine zusätzliche Konfiguration, wodurch die Zielgruppen-Verwaltung optimiert wird. Weitere Informationen zum Anzeigen, Verwalten und Erstellen von Zielgruppen in der Experience Platform-Benutzeroberfläche finden Sie in der [Zielgruppenportal - Übersicht](../../segmentation/ui/audience-portal.md).

<!-- Q) Do you know how long it takes for the audience to register? This info would help manage user expectations. -->

![Der Zielgruppen-Arbeitsbereich in Adobe Experience Platform mit automatisch veröffentlichten und einsatzbereiten Data Distiller-Zielgruppen.](../images/data-distiller/sql-audiences/audiences.png)

## Zielgruppen für Ziele aktivieren {#activate-audiences}

Aktivieren Sie Ihre Zielgruppen, indem Sie sie auf ein beliebiges dateibasiertes Ziel ausrichten, z. B. [!DNL Amazon S3], [!DNL SFTP] oder [!DNL Azure Blob]. Die angereicherten Zielgruppenattribute stehen bei Bedarf zur weiteren Verfeinerung und Filterung zur Verfügung.

![Flussdiagramm der Adobe Experience Platform-Zieltypen, in dem öffentliche und private/benutzerdefinierte Ziele angezeigt werden, einschließlich Batch- und Streaming-Optionen.](../images/data-distiller/sql-audiences/destination-types.png)

## Funktionserläuterungen {#faqs}

In diesem Abschnitt werden häufig gestellte Fragen zur Erstellung und Verwaltung externer Zielgruppen mithilfe von SQL-Daten in Distiller behandelt.

**Fragen**:

- Wird die Erstellung von Zielgruppen nur für flache Datensätze unterstützt?

+++Antwort

Derzeit ist die Erstellung von Zielgruppen bei der Definition der Zielgruppe auf einfache Attribute (Stammebenen) beschränkt.

+++

- Führt die Erstellung einer Zielgruppe zu einem einzelnen Datensatz oder mehreren Datensätzen oder variiert sie je nach Konfiguration?

+++Antwort

Es gibt eine Eins-zu-eins-Zuordnung zwischen einer Zielgruppe und einem Datensatz.

+++

- Ist der Datensatz, der während der Erstellung der Zielgruppe erstellt wurde, für das Profil markiert?

+++Antwort

Nein, der bei der Erstellung der Zielgruppe erstellte Datensatz ist nicht für das Profil markiert.

+++

- Wird der Datensatz im Data Lake erstellt?

+++Antwort

Ja, der mit der Zielgruppe verknüpfte Datensatz wird im Data Lake erstellt. Die Attribute aus diesem Datensatz sind im Audience Composer und im Zielfluss als angereicherte Attribute verfügbar.

+++

- Sind Attribute in der Zielgruppe auf Enterprise-Batch-dateibasierte Ziele beschränkt? (Ja oder Nein)

+++Antwort

Nein. Angereicherte Attribute in der Zielgruppe sind sowohl für Unternehmens-Batch- als auch für dateibasierte Ziele verfügbar. Wenn ein Fehler wie „Die folgenden Segment-IDs haben Namespaces, die für dieses Ziel nicht zulässig sind: e917f626-a038-42f7-944c-xyxyxyxyx“ auftritt, erstellen Sie ein neues Segment in Data Distiller und verwenden Sie es mit einem beliebigen verfügbaren Ziel.

+++

- Kann ich eine Zielgruppe erstellen, die eine Data Distiller-Zielgruppe verwendet?

+++Antwort

Ja, Sie können eine Zielgruppe erstellen, die eine Data Distiller-Zielgruppe verwendet.

+++

- Werden diese Zielgruppen in Adobe Journey Optimizer angezeigt? Wenn nicht, was passiert, wenn ich eine neue Zielgruppe im Regel-Builder erstelle, die alle Mitglieder dieser Zielgruppe enthält?

+++Antwort

Daten-Distiller-Zielgruppen sind auch in Adobe Journey Optimizer verfügbar. Sie können Daten-Distiller-Zielgruppen in Adobe Journey Optimizer verwenden und die Ergebnisse anhand der angereicherten Attribute filtern.

+++

- Werden Data Distiller-Zielgruppen alle 30 Tage gelöscht, da es sich um externe Zielgruppen handelt?

+++Antwort

Ja, Data Distiller-Zielgruppen werden alle 30 Tage gelöscht, da es sich um externe Zielgruppen handelt.

+++

## Nächste Schritte

Nach dem Lesen dieses Dokuments haben Sie gelernt, wie Sie mit der SQL-Zielgruppenerweiterung in Data Distiller Zielgruppen mithilfe von SQL-Befehlen effektiv erstellen, verwalten und veröffentlichen können. Sie können jetzt Zielgruppendefinitionen auf der Grundlage Ihrer individuellen Geschäftsanforderungen anpassen und über verschiedene Ziele hinweg aktivieren, indem Sie Ihre Marketing-Strategien und datengestützten Entscheidungen optimieren.

Als Nächstes können Sie die folgende Dokumentation lesen, um Ihre Zielgruppen-Management-Strategien für Experience Platform weiter zu entwickeln und zu optimieren:

- **Erkunden der Zielgruppenauswertung**: Erfahren Sie mehr über die [Zielgruppenauswertungsmethoden in Adobe Experience Platform](../../segmentation/home.md#evaluate-segments): Streaming-Segmentierung für Echtzeit-Updates, Batch-Segmentierung für die geplante oder bedarfsgesteuerte Verarbeitung und Edge-Segmentierung für die sofortige Auswertung auf der Edge Network.
- **Mit Zielen integrieren**: Lesen Sie das Handbuch zum [ von Dateien bei Bedarf in Batch-Ziele ](../../destinations/ui/export-file-now.md) der Benutzeroberfläche von Experience Platform-Zielen.
- **Leistung der Zielgruppe überprüfen** Analysieren Sie, wie Ihre SQL-definierten Zielgruppen auf verschiedenen Kanälen funktionieren. Verwenden Sie Dateneinblicke, um Ihre Zielgruppendefinitionen und Zielgruppenbestimmungsstrategien anzupassen und zu verbessern. Lesen Sie das Dokument unter [Zielgruppeneinblicke](../../dashboards/insights/audiences.md), um zu erfahren, wie Sie in Adobe Real-Time CDP auf die SQL-Abfragen für Zielgruppeneinblicke zugreifen und diese anpassen können. Anschließend können Sie eigene Einblicke erstellen und Rohdaten in umsetzbare Informationen umwandeln, indem Sie das Zielgruppen-Dashboard anpassen, um diese Einblicke effektiv zu visualisieren und für eine bessere Entscheidungsfindung zu verwenden.

