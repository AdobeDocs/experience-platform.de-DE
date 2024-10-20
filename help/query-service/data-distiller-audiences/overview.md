---
title: Erstellen von Zielgruppen mit SQL
description: Erfahren Sie, wie Sie mit der SQL-Zielgruppenerweiterung in Adobe Experience Platform Data Distiller Zielgruppen mit SQL-Befehlen erstellen, verwalten und veröffentlichen können. In diesem Handbuch werden alle Aspekte des Zielgruppen-Lebenszyklus behandelt, einschließlich Erstellung, Aktualisierung und Löschung von Profilen und Verwendung datengesteuerter Zielgruppendefinitionen für dateibasierte Ziele.
source-git-commit: b790dc0a485011022ac637f9d9c55f21c882d5fc
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 1%

---

# Erstellen von Zielgruppen mit SQL

In diesem Dokument wird beschrieben, wie Sie die SQL-Zielgruppenerweiterung in Adobe Experience Platform Data Distiller verwenden, um Zielgruppen mit SQL-Befehlen zu erstellen, zu verwalten und zu veröffentlichen.

Verwenden Sie die SQL-Zielgruppenerweiterung, um Zielgruppen mit Daten aus dem Data Lake zu erstellen, einschließlich vorhandener Dimensionentitäten. Mit dieser Erweiterung können Sie Zielgruppensegmente direkt mit SQL definieren und so Flexibilität bieten, ohne Rohdaten in Ihren Profilen zu benötigen. Mit dieser Methode erstellte Zielgruppen werden automatisch im Arbeitsbereich &quot;Zielgruppe&quot;registriert, wo Sie sie weiter an dateibasierte Ziele ausrichten können.

![Infografik, die den Workflow für die SQL-Zielgruppenerweiterung anzeigt. Zu den Phasen gehören das Erstellen von Zielgruppen mit dem Query Service mithilfe von SQL-Befehlen, deren Verwaltung in der Platform-Benutzeroberfläche, das Aktivieren dieser Zielgruppen in dateibasierten Zielen.](../images/data-distiller/sql-audiences/sql-audience-extension-workflow.png)

## Lebenszyklus der Zielgruppenerstellung in Data Distiller {#audience-creation-lifecycle}

Führen Sie diese Schritte aus, um Ihre Zielgruppen effektiv zu verwalten. Die erstellten Zielgruppen werden nahtlos in den Zielgruppenfluss integriert, sodass Sie Segmente aus diesen Basiszielgruppen erstellen und dateibasierte Ziele für das Kunden-Targeting auswählen können. Verwenden Sie die folgenden SQL-Befehle, um die Zielgruppen [create](#create-audience), [modify](#add-profiles-to-audience) und [delete](#delete-audience) in Adobe Experience Platform zu erstellen.

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
| `identity_namespace` | Namespace der Identität. |
| `select_query` | Eine SELECT-Anweisung, die die Audience definiert. Die Syntax der SELECT-Abfrage finden Sie im Abschnitt [SELECT-Abfragen](../sql/syntax.md#select-queries) . |

{style="table-layout:auto"}

**Beispiel:**

Das folgende Beispiel zeigt, wie Sie Ihre SQL-Zielgruppen-Erstellungsabfrage strukturieren:

```sql
CREATE Audience aud_test 
WITH (primary_identity=month, identity_namespace=queryService) 
AS SELECT month FROM profile_dim_date LIMIT 5;
```

**Einschränkungen:**

Beachten Sie die folgenden Einschränkungen bei der Verwendung von SQL für die Erstellung von Zielgruppen:

- Die primäre Identitätsspalte &quot;**must**&quot; befindet sich auf der Stammebene.
- Neue Batches überschreiben vorhandene Datensätze. Die Anlagenfunktion wird derzeit nicht unterstützt.
- Verschachtelte Attribute werden derzeit nicht unterstützt.

### Profile zu einer vorhandenen Zielgruppe hinzufügen {#add-profiles-to-audience}

Verwenden Sie den Befehl `INSERT INTO` , um einer vorhandenen Zielgruppe Profile hinzuzufügen.

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
SELECT month FROM profile_dim_date LIMIT 10;
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

### Automatische Veröffentlichung von Zielgruppen {#auto-publish-audiences}

Mit der SQL-Erweiterung erstellte Zielgruppen werden automatisch unter Data Distiller im Audience-Arbeitsbereich registriert. Nach der Registrierung sind diese Zielgruppen für das Targeting verfügbar und können in dateibasierten Zielen verwendet werden, um Ihre Segmentierungs- und Targeting-Strategien zu verbessern.

![Der Arbeitsbereich &quot;Zielgruppe&quot;in Adobe Experience Platform, in dem Data Distiller-Zielgruppen automatisch veröffentlicht und einsatzbereit angezeigt werden.](../images/data-distiller/sql-audiences/audiences.png)

## Aktivieren von Zielgruppen für Ziele {#activate-audiences}

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

Datendestiller-Zielgruppen sind derzeit nicht in Adobe Journey Optimizer verfügbar. Sie müssen eine neue Zielgruppe im Adobe Journey Optimizer Rule Builder erstellen, damit sie in Adobe Journey Optimizer verfügbar ist.

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
- **Audience Performance überprüfen**: Analysieren Sie, wie Ihre SQL-definierten Zielgruppen über verschiedene Kanäle hinweg funktionieren. Verwenden Sie Dateneinblicke, um Ihre Zielgruppendefinitionen und Zielgruppenstrategien anzupassen und zu verbessern. Lesen Sie das Dokument zu [Zielgruppeneinblicken](../../dashboards/insights/audiences.md) , um zu erfahren, wie Sie auf die SQL-Abfragen für Zielgruppeneinblicke in Adobe Real-time Customer Data Platform zugreifen und diese anpassen können. Anschließend können Sie eigene Einblicke erstellen und Rohdaten in umsetzbare Informationen umwandeln, indem Sie das Zielgruppen-Dashboard anpassen, um diese Einblicke effektiv zu visualisieren und für eine bessere Entscheidungsfindung zu verwenden.
