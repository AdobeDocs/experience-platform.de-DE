---
title: Streamen von Daten aus Ihrer Snowflake-Datenbank an Experience Platform mithilfe der Benutzeroberfläche
description: Erfahren Sie, wie Sie Daten aus Ihrer Snowflake-Datenbank an Experience Platform streamen.
exl-id: 49d488f1-90d8-452a-9f3e-02afdcc79b09
source-git-commit: 04a1cecbacdaf0b701d3ef18d03497973a8f3263
workflow-type: tm+mt
source-wordcount: '1648'
ht-degree: 16%

---

# Streamen von Daten aus Ihrer [!DNL Snowflake]-Datenbank an Experience Platform mithilfe der Benutzeroberfläche

In diesem Handbuch erfahren Sie, wie Sie die Benutzeroberfläche verwenden, um Daten aus Ihrer [!DNL Snowflake] an Adobe Experience Platform zu streamen.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

### Authentifizierung

Lesen Sie das Handbuch unter [Vorausgesetzte Einrichtung für  [!DNL Snowflake] -Streaming](../../../../connectors/databases/snowflake-streaming.md), um Informationen zu den Schritten zu erhalten, die Sie durchführen müssen, bevor Sie Streaming-Daten von [!DNL Snowflake] in Experience Platform aufnehmen können.

## Verwenden der [!DNL Snowflake Streaming] zum Streamen [!DNL Snowflake] Daten an Experience Platform

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter *Kategorie* die Option **[!DNL Snowflake Streaming]** und dann die Option **[!UICONTROL Daten hinzufügen]** aus.

>[!TIP]
>
>Für Quellen, die im Quellkatalog kein authentifiziertes Konto haben, wird die Option **[!UICONTROL Einrichten]** angezeigt. Sobald ein authentifiziertes Konto vorhanden ist, ändert sich diese Option in **[!UICONTROL Daten hinzufügen]**.

![Der Quellkatalog in der Experience Platform-Benutzeroberfläche mit ausgewählter Snowflake Streaming-Quellkarte.](../../../../images/tutorials/create/snowflake-streaming/catalog.png)

Die **[!UICONTROL Snowflake Streaming-Konto verbinden]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

>[!BEGINTABS]

>[!TAB Neues Konto erstellen]

Um ein neues Konto zu erstellen, wählen **[!UICONTROL Neues Konto]** und geben Sie einen Namen, eine optionale Beschreibung und Ihre -Anmeldeinformationen an.

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![Die neue Benutzeroberfläche zur Kontoerstellung des Quell-Workflows.](../../../../images/tutorials/create/snowflake-streaming/new.png)

| Anmeldedaten | Beschreibung |
| --- | --- |
| Konto | Der Name Ihres [!DNL Snowflake]. Konventionen zu Kontonamen finden Sie im [[!DNL Snowflake Streaming] Authentifizierungshandbuch](../../../../connectors/databases/snowflake-streaming.md#gather-required-credentials). |
| Warehouse | Der Name Ihres [!DNL Snowflake]. Warehouses verwalten die Ausführung von Abfragen in [!DNL Snowflake]. Jedes [!DNL Snowflake] Warehouse ist unabhängig voneinander und muss einzeln aufgerufen werden, um Daten in Experience Platform zu bringen. |
| Datenbank | Der Name Ihrer [!DNL Snowflake]. Die -Datenbank enthält die Daten, die Sie an Experience Platform übermitteln möchten. |
| Schema | (Optional) Das mit Ihrem [!DNL Snowflake] verknüpfte Datenbankschema. |
| Benutzername | Der Benutzername Ihres [!DNL Snowflake]. |
| Kennwort | Das Kennwort für Ihr [!DNL Snowflake]. |
| Rolle | (Optional) Eine benutzerdefinierte Rolle, die einem Benutzer für eine bestimmte Verbindung bereitgestellt werden kann. Wenn kein Wert angegeben wird, ist dieser Standardwert `public`. |

Weiterführende Informationen zur Kontoerstellung finden Sie im Abschnitt [Konfigurieren von Rolleneinstellungen](../../../../connectors/databases/snowflake-streaming.md#configure-role-settings) in der [!DNL Snowflake Streaming].

>[!TAB Vorhandenes Konto verwenden]

Um ein vorhandenes Konto zu verwenden, wählen Sie **[!UICONTROL Vorhandenes Konto]** und dann das gewünschte Konto aus dem vorhandenen Kontokatalog aus.

Klicken Sie auf **[!UICONTROL Weiter]**, um fortzufahren.

![Die vorhandene Kontoauswahlseite des Quellkatalogs.](../../../../images/tutorials/create/snowflake-streaming/existing.png)

>[!ENDTABS]

## Daten auswählen {#select-data}

>[!IMPORTANT]
>
>* Eine Zeitstempelspalte muss in Ihrer Quelltabelle vorhanden sein, damit ein Streaming-Datenfluss erstellt werden kann. Der Zeitstempel ist erforderlich, damit Experience Platform weiß, wann Daten aufgenommen werden und wann inkrementelle Daten gestreamt werden. Sie können nachträglich eine Zeitstempelspalte für eine bestehende Verbindung hinzufügen und einen neuen Datenfluss erstellen.
>
>* Stellen Sie sicher, dass die Groß-/Kleinschreibung der Datenfelder in Ihrer Beispiel-Quelldatendatei mit der Anleitung von [!DNL Snowflake] zur Groß-/Kleinschreibung für Kennungen übereinstimmt. Weitere Informationen finden [[!DNL Snowflake]  im Dokument zur Groß](https://docs.snowflake.com/en/sql-reference/identifiers-syntax#label-identifier-casing) und Kleinschreibung von Bezeichnern .

Der Schritt [!UICONTROL Daten auswählen] wird angezeigt. In diesem Schritt müssen Sie die Daten auswählen, die Sie in Experience Platform importieren möchten, Zeitstempel und Zeitzonen konfigurieren und eine Beispieldatendatei für die Aufnahme von Rohdaten bereitstellen.

Verwenden Sie das Datenbankverzeichnis auf der linken Bildschirmseite und wählen Sie die Tabelle aus, die Sie in Experience Platform importieren möchten.

![Die ausgewählte Datenschnittstelle mit ausgewählter Datenbanktabelle.](../../../../images/tutorials/create/snowflake-streaming/select-table.png)

Wählen Sie als Nächstes den Zeitstempel-Spaltentyp Ihrer Tabelle aus. Sie können zwischen zwei Arten von Zeitstempelspalten wählen: `TIMESTAMP_NTZ` oder `TIMESTAMP_LTZ`. Wenn Sie den Spaltentyp `TIMESTAMP_NTZ` auswählen, müssen Sie auch eine Zeitzone angeben. Die Spalten sollten eine NOT NULL-Einschränkung aufweisen. Weitere Informationen finden Sie im Abschnitt zu [Einschränkungen und häufig gestellte Fragen](../../../../connectors/databases/snowflake-streaming.md#limitations-and-frequently-asked-questions).

In diesem Schritt können Sie auch Aufstockungseinstellungen konfigurieren. Die Aufstockung bestimmt, welche Daten anfänglich aufgenommen werden. Wenn die Aufstockung aktiviert ist, werden alle aktuellen Dateien im angegebenen Pfad während der ersten geplanten Aufnahme aufgenommen. Andernfalls werden nur die Dateien aufgenommen, die zwischen dem ersten Aufnahmevorgang und der Startzeit geladen werden. Dateien, die vor der Startzeit geladen wurden, werden nicht aufgenommen.

Wählen Sie den Umschalter **[!UICONTROL Aufstockung]** aus, um die Aufstockung zu aktivieren.

![Die Konfigurationsschritte Zeitstempel, Zeitzone und Aufstockung.](../../../../images/tutorials/create/snowflake-streaming/timezone.png)

Wählen Sie abschließend **[!UICONTROL Datei auswählen]** aus, um ein Beispiel für Quelldaten hochzuladen und so den Zuordnungssatz zu erstellen. Dieser wird in einem späteren Schritt verwendet, um Ihre Originaldaten dem Experience-Datenmodell (XDM) zuzuordnen.

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Weiter]** aus, um fortzufahren.

![Die Vorschau der Quellbeispieldaten.](../../../../images/tutorials/create/snowflake-streaming/preview.png)

## Datensatz- und Datenflussdetails angeben {#provide-dataset-and-dataflow-details}

Als Nächstes müssen Sie Informationen zu Ihrem Datensatz und Ihrem Datenfluss angeben.

### Datensatz-Details {#dataset-details}

Ein Datensatz ist ein Konstrukt zur Datenspeicherung und -verwaltung, in dem Daten (in der Regel) in einer Tabelle erfasst werden, die ein Schema (Spalten) und Felder (Zeilen) beinhaltet. Daten, die erfolgreich in Experience Platform aufgenommen werden, bleiben als Datensätze im Data Lake erhalten. In diesem Schritt können Sie einen neuen Datensatz erstellen oder einen vorhandenen Datensatz verwenden.

>[!BEGINTABS]

>[!TAB Verwenden eines neuen Datensatzes]

Um einen neuen Datensatz zu verwenden, wählen **[!UICONTROL Neuer Datensatz]** und geben Sie dann einen Namen und eine optionale Beschreibung für Ihren Datensatz an. Sie müssen auch ein Experience-Datenmodell-Schema (XDM) auswählen, dem Ihr Datensatz entspricht.

![Die neue Oberfläche zur Datensatzauswahl.](../../../../images/tutorials/create/snowflake-streaming/new-dataset.png)

| Neue Datensatzdetails | Beschreibung |
| --- | --- |
| Name des Ausgabe-Datensatzes | Der Name Ihres neuen Datensatzes. |
| Beschreibung | (Optional) Ein kurzer Überblick über den neuen Datensatz. |
| Schema | Eine Dropdown-Liste mit Schemata, die in Ihrer Organisation vorhanden sind. Sie können auch vor dem Prozess der Quellkonfiguration Ihr eigenes Schema erstellen. Weitere Informationen finden Sie im Handbuch unter [Erstellen eines XDM-Schemas in der Benutzeroberfläche](../../../../../xdm/tutorials/create-schema-ui.md). |

>[!TAB Verwenden eines vorhandenen Datensatzes]

Wenn Sie bereits über einen vorhandenen Datensatz verfügen, wählen Sie **[!UICONTROL Vorhandener Datensatz]** und verwenden Sie dann die Option **[!UICONTROL Erweiterte Suche]**, um ein Fenster aller Datensätze in Ihrer Organisation anzuzeigen, einschließlich der entsprechenden Details, z. B. ob sie für die Aufnahme in das Echtzeit-Kundenprofil aktiviert sind.

![Die vorhandene Oberfläche zur Datensatzauswahl.](../../../../images/tutorials/create/snowflake-streaming/existing-dataset.png)

>[!ENDTABS]

+++Wählen Sie Schritte aus, um die Profilaufnahme, Fehlerdiagnose und partielle Aufnahme zu aktivieren.

Wenn Ihr Datensatz für das Echtzeit-Kundenprofil aktiviert ist, können Sie in diesem Schritt **[!UICONTROL Profildatensatz]** umschalten, um Ihre Daten für die Profilaufnahme zu aktivieren. Sie können diesen Schritt auch verwenden, um **[!UICONTROL Fehlerdiagnose]** und **[!UICONTROL Partielle Aufnahme]** zu aktivieren.

* **[!UICONTROL Fehlerdiagnose]**: Wählen Sie **[!UICONTROL Fehlerdiagnose]** aus, um die Quelle anzuweisen, Fehlerdiagnosen zu erstellen, auf die Sie später bei der Überwachung Ihrer Datensatzaktivität und des Datenflussstatus verweisen können.
* **[!UICONTROL Partielle Aufnahme]** Bei der partiellen Batch-Aufnahme werden Daten mit Fehlern bis zu einem bestimmten konfigurierbaren Schwellenwert aufgenommen. Mit dieser Funktion können Sie alle Ihre korrekten Daten erfolgreich in Experience Platform aufnehmen, während alle Ihre falschen Daten separat mit Informationen darüber, warum sie ungültig sind, in Batches erfasst werden.

+++

### Datenflussdetails {#dataflow-details}

Nachdem Ihr Datensatz konfiguriert wurde, müssen Sie Details zu Ihrem Datenfluss angeben, einschließlich eines Namens, einer optionalen Beschreibung und Warnhinweiskonfigurationen.

![Der Konfigurationsschritt „Datenflussdetails“.](../../../../images/tutorials/create/snowflake-streaming/dataflow-details.png)

| Datenflusskonfigurationen | Beschreibung |
| --- | --- |
| Datenflussname | Der Name des Datenflusses.  Standardmäßig wird dabei der Name der zu importierenden Datei verwendet. |
| Beschreibung | (Optional) Eine kurze Beschreibung Ihres Datenflusses. |
| Warnhinweise | Experience Platform kann ereignisbasierte Warnhinweise erstellen, die Benutzende abonnieren können. Für diese Optionen ist ein laufender Datenfluss erforderlich, um sie im Trigger zu halten. Weitere Informationen finden Sie unter [Warnhinweise - Übersicht](../../alerts.md) <ul><li>**Start der Ausführung des Quelldatenflusses**: Wählen Sie diesen Warnhinweis aus, um eine Benachrichtigung zu erhalten, wenn die Ausführung des Datenflusses beginnt.</li><li>**Erfolgreiche Ausführung des Quelldatenflusses**: Wählen Sie diesen Warnhinweis aus, um eine Benachrichtigung zu erhalten, wenn Ihr Datenfluss fehlerfrei endet.</li><li>**Fehler bei der Ausführung des Datenflusses an Quellen**: Wählen Sie diesen Warnhinweis aus, um eine Benachrichtigung zu erhalten, wenn die Ausführung des Datenflusses mit Fehlern endet.</li></ul> |

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Weiter]** aus, um fortzufahren.

## Zuordnen von Feldern zu einem XDM-Schema {#mapping}

Der Schritt [!UICONTROL Zuordnung] wird angezeigt. Verwenden Sie die Zuordnungsschnittstelle, um Ihre Quelldaten den entsprechenden Schemafeldern zuzuordnen, bevor Sie diese Daten in Experience Platform aufnehmen, und wählen Sie dann **[!UICONTROL Weiter]**. Eine ausführliche Anleitung zur Verwendung der Zuordnungsschnittstelle finden Sie im [Handbuch zur Datenvorbereitungs-](../../../../../data-prep/ui/mapping.md)).

![Die Zuordnungsschnittstelle des Quell-Workflows.](../../../../images/tutorials/create/snowflake-streaming/mapping.png)

## Überprüfen des Datenflusses {#review}

Der letzte Schritt im Prozess zur Erstellung eines Datenflusses besteht darin, Ihren Datenfluss zu überprüfen, bevor er ausgeführt wird. Verwenden Sie den **[!UICONTROL Überprüfen]** Schritt, um die Details Ihres neuen Datenflusses zu überprüfen, bevor er ausgeführt wird. Die Details sind in die folgenden Kategorien unterteilt:

* **Verbindung**: Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quelldatei und die Anzahl der Spalten innerhalb dieser Quelldatei an.
* **Datensatz- und Zuordnungsfelder zuweisen**: Zeigt an, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, dem der Datensatz entspricht.

Nachdem Sie Ihren Datenfluss überprüft haben, klicken Sie auf **[!UICONTROL Beenden]** und gewähren Sie etwas Zeit für die Erstellung des Datenflusses.

![Der Schritt Überprüfen des Quell-Workflows.](../../../../images/tutorials/create/snowflake-streaming/review.png)

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich einen Streaming-Datenfluss für [!DNL Snowflake] erstellt. Weitere Ressourcen finden Sie in der Dokumentation unten.

### Überwachen Ihres Datenflusses

Nachdem Ihr Datenfluss erstellt wurde, können Sie die Daten überwachen, die über ihn aufgenommen werden, um Informationen zu Aufnahmegeschwindigkeiten, Erfolg und Fehlern anzuzeigen. Weitere Informationen zum Überwachen von Streaming-Datenflüssen finden Sie im Tutorial [Überwachen von Streaming-Datenflüssen in der Benutzeroberfläche](../../monitor-streaming.md).

### Aktualisieren des Datenflusses

Um Konfigurationen für die Planung, Zuordnung und allgemeine Informationen Ihrer Datenflüsse zu aktualisieren, besuchen Sie das Tutorial [Aktualisieren von Quelldatenflüssen in der Benutzeroberfläche](../../update-dataflows.md).

### Löschen des Datenflusses

Datenflüsse, die nicht mehr erforderlich sind oder nicht korrekt erstellt wurden, können Sie löschen, indem Sie dazu die Funktion **[!UICONTROL Löschen]** im Arbeitsbereich **[!UICONTROL Datenflüsse]** verwenden. Weitere Informationen zum Löschen von Datenflüssen finden Sie im Tutorial [Löschen von Datenflüssen in der Benutzeroberfläche](../../delete.md).
