---
title: Streamen von Daten aus Ihrer Snowflake-Datenbank auf Experience Platform mithilfe der Benutzeroberfläche
type: Tutorial
description: Erfahren Sie, wie Sie Daten aus Ihrer Snwoflake-Datenbank auf Experience Platform streamen.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 49d488f1-90d8-452a-9f3e-02afdcc79b09
source-git-commit: f39ee3af176e3d9b8ad04bfad81793db0ebe71a7
workflow-type: tm+mt
source-wordcount: '1648'
ht-degree: 17%

---

# Streamen von Daten aus Ihrer [!DNL Snowflake]-Datenbank mithilfe der Benutzeroberfläche an das Experience Platform

In diesem Handbuch erfahren Sie, wie Sie mit der Benutzeroberfläche Daten von Ihrer [!DNL Snowflake] -Datenbank an Adobe Experience Platform streamen können.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

### Authentifizierung

Informationen zu den Schritten, die Sie ausführen müssen, bevor Sie Streaming-Daten von [!DNL Snowflake] auf Experience Platform erfassen können, finden Sie im Handbuch unter [Voraussetzungen für die Einrichtung von  [!DNL Snowflake] Streaming-Daten](../../../../connectors/databases/snowflake-streaming.md) .

## [!DNL Snowflake Streaming]-Quelle verwenden, um [!DNL Snowflake]-Daten an Experience Platform zu streamen

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste die Option **[!UICONTROL Quellen]**, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie *Datenbanken* die Option **[!DNL Snowflake Streaming]** und dann **[!UICONTROL Daten hinzufügen]** aus.

>[!TIP]
>
>Quellen ohne authentifiziertes Konto im Quellkatalog zeigen die Option **[!UICONTROL Einrichten]** an. Sobald ein authentifiziertes Konto vorhanden ist, wird diese Option in **[!UICONTROL Daten hinzufügen]** geändert.

![Der Quellkatalog in der Experience Platform-Benutzeroberfläche, wobei die Snowflake-Streaming-Quellkarte ausgewählt ist.](../../../../images/tutorials/create/snowflake-streaming/catalog.png)

Die Seite **[!UICONTROL Snowflake-Streaming-Konto verbinden]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

>[!BEGINTABS]

>[!TAB Neues Konto erstellen]

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL Neues Konto]** aus und geben Sie einen Namen, eine optionale Beschreibung und Ihre Anmeldeinformationen ein.

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![Die neue Benutzeroberfläche zur Kontoerstellung des Ursprungs-Workflows.](../../../../images/tutorials/create/snowflake-streaming/new.png)

| Anmeldedaten | Beschreibung |
| --- | --- |
| Konto | Der Name Ihres [!DNL Snowflake]-Kontos. Konventionen zu Kontonamen finden Sie im [[!DNL Snowflake Streaming] Authentifizierungshandbuch](../../../../connectors/databases/snowflake-streaming.md#gather-required-credentials). |
| Warehouse | Der Name Ihres [!DNL Snowflake] Warehouse. Warehouse verwaltet die Ausführung von Abfragen in [!DNL Snowflake]. Jedes [!DNL Snowflake]-Warehouse ist unabhängig voneinander und muss einzeln aufgerufen werden, um Daten an Experience Platform zu bringen. |
| Datenbank | Der Name Ihrer [!DNL Snowflake] -Datenbank. Die Datenbank enthält die Daten, die Sie zum Experience Platform mitbringen möchten. |
| Schema | (Optional) Das Datenbankschema, das mit Ihrem [!DNL Snowflake]-Konto verknüpft ist. |
| Benutzername | Der Benutzername Ihres [!DNL Snowflake]-Kontos. |
| Kennwort | Das Kennwort für Ihr [!DNL Snowflake]-Konto. |
| Rolle | (Optional) Eine benutzerdefinierte Rolle, die einem Benutzer für eine bestimmte Verbindung bereitgestellt werden kann. Wenn dieser Wert nicht angegeben wird, wird standardmäßig `public` verwendet. |

Weiterführende Informationen zur Kontoerstellung finden Sie im Abschnitt [Konfigurieren von Rolleneinstellungen](../../../../connectors/databases/snowflake-streaming.md#configure-role-settings) in der [!DNL Snowflake Streaming] -Übersicht.

>[!TAB Vorhandenes Konto verwenden]

Um ein vorhandenes Konto zu verwenden, wählen Sie **[!UICONTROL Vorhandenes Konto]** und dann das gewünschte Konto aus dem vorhandenen Kontokatalog aus.

Klicken Sie auf **[!UICONTROL Weiter]**, um fortzufahren.

![Die vorhandene Kontoauswahlseite des Quellkatalogs.](../../../../images/tutorials/create/snowflake-streaming/existing.png)

>[!ENDTABS]

## Daten auswählen {#select-data}

>[!IMPORTANT]
>
>* In der Quelltabelle muss eine Spalte mit Zeitstempel vorhanden sein, damit ein Streaming-Datenfluss erstellt werden kann. Der Zeitstempel ist erforderlich, damit Experience Platform weiß, wann Daten erfasst und wann inkrementelle Daten gestreamt werden. Sie können rückwirkend eine Zeitstempelspalte für eine bestehende Verbindung hinzufügen und einen neuen Datenfluss erstellen.
>
>* Stellen Sie sicher, dass die Groß-/Kleinschreibung der Datenfelder in Ihrer Beispiel-Quelldatendatei den Anweisungen von [!DNL Snowflake] zur Fallauflösung für Kennungen entspricht. Weitere Informationen finden Sie im Dokument [[!DNL Snowflake] zur Identifizierungsweise](https://docs.snowflake.com/en/sql-reference/identifiers-syntax#label-identifier-casing) .

Der Schritt [!UICONTROL Daten auswählen] wird angezeigt. In diesem Schritt müssen Sie die Daten auswählen, die Sie in Experience Platform importieren möchten, Zeitstempel und Zeitzonen konfigurieren und eine Beispieldatendatei für die Aufnahme von Rohdaten bereitstellen.

Verwenden Sie das Datenbankverzeichnis auf der linken Bildschirmseite und wählen Sie die Tabelle aus, die Sie in Experience Platform importieren möchten.

![Die ausgewählte Datenschnittstelle mit einer ausgewählten Datenbanktabelle.](../../../../images/tutorials/create/snowflake-streaming/select-table.png)

Wählen Sie als Nächstes den Zeitstempelspaltentyp Ihrer Tabelle aus. Sie können zwischen zwei Arten von Zeitstempelspalten wählen: `TIMESTAMP_NTZ` oder `TIMESTAMP_LTZ`. Wenn Sie den Spaltentyp `TIMESTAMP_NTZ` auswählen, müssen Sie auch eine Zeitzone angeben. Ihre Spalten sollten eine Nicht-Null-Einschränkung aufweisen. Weitere Informationen finden Sie im Abschnitt zu [Einschränkungen und häufig gestellten Fragen] .

Sie können während dieses Schritts auch die Einstellungen für die Aufstockung konfigurieren. Die Aufstockung bestimmt, welche Daten ursprünglich erfasst werden. Wenn die Aufstockung aktiviert ist, werden alle aktuellen Dateien im angegebenen Pfad während der ersten geplanten Erfassung erfasst. Andernfalls werden nur die Dateien erfasst, die zwischen der ersten Ausführung der Aufnahme und der Startzeit geladen wurden. Dateien, die vor der Startzeit geladen wurden, werden nicht erfasst.

Wählen Sie den Umschalter **[!UICONTROL Aufstockung]** aus, um die Aufstockung zu aktivieren.

![Die Konfigurationsschritte für Zeitstempel, Zeitzone und Aufstockung.](../../../../images/tutorials/create/snowflake-streaming/timezone.png)

Wählen Sie abschließend **[!UICONTROL Datei auswählen]** aus, um eine Beispiel-Quelldaten hochzuladen und so den Zuordnungssatz zu erstellen. Dieser wird in einem späteren Schritt verwendet, um Ihre ursprünglichen Daten dem Experience-Datenmodell (XDM) zuzuordnen.

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Weiter]** aus, um fortzufahren.

![Die Vorschau der Quellbeispieldaten.](../../../../images/tutorials/create/snowflake-streaming/preview.png)

## Bereitstellen von Datensatz- und Datenflussdetails {#provide-dataset-and-dataflow-details}

Als Nächstes müssen Sie Informationen zu Ihrem Datensatz und Ihrem Datenfluss angeben.

### Datensatz-Details {#dataset-details}

Ein Datensatz ist ein Konstrukt zur Datenspeicherung und -verwaltung, in dem Daten (in der Regel) in einer Tabelle erfasst werden, die ein Schema (Spalten) und Felder (Zeilen) beinhaltet. Daten, die erfolgreich in Experience Platform aufgenommen wurden, werden im Data Lake als Datensätze persistiert. In diesem Schritt können Sie einen neuen Datensatz erstellen oder einen vorhandenen Datensatz verwenden.

>[!BEGINTABS]

>[!TAB Verwenden eines neuen Datensatzes]

Um einen neuen Datensatz zu verwenden, wählen Sie **[!UICONTROL Neuer Datensatz]** aus und geben Sie dann einen Namen und eine optionale Beschreibung für Ihren Datensatz an. Sie müssen auch ein Experience-Datenmodell (XDM)-Schema auswählen, dem Ihr Datensatz entspricht.

![ Die neue Oberfläche zur Datensatzauswahl.](../../../../images/tutorials/create/snowflake-streaming/new-dataset.png)

| Neue Datensatzdetails | Beschreibung |
| --- | --- |
| Name des Ausgabe-Datensatzes | Der Name Ihres neuen Datensatzes. |
| Beschreibung | (Optional) Eine kurze Übersicht über den neuen Datensatz. |
| Schema | Eine Dropdown-Liste mit Schemas, die in Ihrer Organisation vorhanden sind. Sie können auch ein eigenes Schema vor dem Quellkonfigurationsprozess erstellen. Weitere Informationen finden Sie im Handbuch zum Erstellen eines XDM-Schemas in der Benutzeroberfläche ](../../../../../xdm/tutorials/create-schema-ui.md).[ |

>[!TAB Verwenden eines vorhandenen Datensatzes]

Wenn Sie bereits über einen vorhandenen Datensatz verfügen, wählen Sie **[!UICONTROL Vorhandenen Datensatz]** und verwenden Sie dann die Option **[!UICONTROL Erweiterte Suche]** , um ein Fenster mit allen Datensätzen in Ihrer Organisation anzuzeigen, einschließlich der entsprechenden Details, z. B. ob sie für die Aufnahme in das Echtzeit-Kundenprofil aktiviert sind.

![ Die vorhandene Oberfläche zur Datensatzauswahl.](../../../../images/tutorials/create/snowflake-streaming/existing-dataset.png)

>[!ENDTABS]

++ + Wählen Sie Schritte aus, um die Profilaufnahme, Fehlerdiagnose und partielle Erfassung zu aktivieren.

Wenn Ihr Datensatz für das Echtzeit-Kundenprofil aktiviert ist, können Sie während dieses Schritts **[!UICONTROL Profildatensatz]** umschalten, um Ihre Daten für die Profilaufnahme zu aktivieren. Sie können diesen Schritt auch verwenden, um die **[!UICONTROL Fehlerdiagnose]** und die **[!UICONTROL partielle Erfassung]** zu aktivieren.

* **[!UICONTROL Fehlerdiagnose]**: Wählen Sie **[!UICONTROL Fehlerdiagnose]** aus, um die Quelle anzuweisen, Fehlerdiagnosen zu erstellen, die Sie später bei der Überwachung der Datensatzaktivität und des Datenflussstatus referenzieren können.
* **[!UICONTROL Partielle Erfassung]**: Partielle Batch-Erfassung ist die Möglichkeit, Daten mit Fehlern bis zu einem bestimmten konfigurierbaren Schwellenwert zu erfassen. Mit dieser Funktion können Sie alle Ihre präzisen Daten erfolgreich in Experience Platform erfassen, während all Ihre falschen Daten separat mit Informationen darüber gestapelt werden, warum sie ungültig sind.

+++

### Datenflussdetails {#dataflow-details}

Nachdem Ihr Datensatz konfiguriert wurde, müssen Sie Details zu Ihrem Datenfluss angeben, einschließlich eines Namens, einer optionalen Beschreibung und Warnhinweiskonfigurationen.

![ Der Konfigurationsschritt für den Datenfluss detailliert.](../../../../images/tutorials/create/snowflake-streaming/dataflow-details.png)

| Datenflusskonfigurationen | Beschreibung |
| --- | --- |
| Datenflussname | Der Name des Datenflusses.  Standardmäßig wird dabei der Name der Datei verwendet, die importiert wird. |
| Beschreibung | (Optional) Eine kurze Beschreibung Ihres Datenflusses. |
| Warnhinweise | Experience Platform kann ereignisbasierte Warnhinweise erstellen, die Benutzer abonnieren können. Diese Optionen erfordern einen laufenden Datenfluss, um sie Trigger. Weitere Informationen finden Sie in der [Warnhinweise - Übersicht](../../alerts.md) <ul><li>**Start des Datenflusses für Quellen**: Wählen Sie diesen Warnhinweis aus, um eine Benachrichtigung zu erhalten, wenn der Datenfluss beginnt.</li><li>**Erfolg des Datenfluss-Workflows für Quellen**: Wählen Sie diesen Warnhinweis aus, um eine Benachrichtigung zu erhalten, wenn Ihr Datenfluss ohne Fehler beendet wird.</li><li>**Quellen für Fehler beim Ausführen des Datenflusses**: Wählen Sie diesen Warnhinweis aus, um eine Benachrichtigung zu erhalten, wenn die Ausführung des Datenflusses mit Fehlern endet.</li></ul> |

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Weiter]** aus, um fortzufahren.

## Felder einem XDM-Schema zuordnen {#mapping}

Der Schritt [!UICONTROL Zuordnung] wird angezeigt. Verwenden Sie die Zuordnungsschnittstelle, um Ihre Quelldaten den entsprechenden Schemafeldern zuzuordnen, bevor Sie diese Daten in Experience Platform aufnehmen, und wählen Sie dann **[!UICONTROL Weiter]** aus. Eine ausführliche Anleitung zur Verwendung der Zuordnungsschnittstelle finden Sie im [UI-Handbuch zur Datenvorbereitung](../../../../../data-prep/ui/mapping.md) .

![Die Zuordnungsschnittstelle des Ursprungs-Workflows.](../../../../images/tutorials/create/snowflake-streaming/mapping.png)

## Überprüfen des Datenflusses {#review}

Der letzte Schritt im Erstellungsprozess des Datenflusses besteht darin, Ihren Datenfluss zu überprüfen, bevor er ausgeführt wird. Verwenden Sie den Schritt **[!UICONTROL Überprüfen]** , um die Details Ihres neuen Datenflusses zu überprüfen, bevor er ausgeführt wird. Details werden in die folgenden Kategorien eingeteilt:

* **Verbindung**: Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quelldatei und die Anzahl der Spalten in dieser Quelldatei an.
* **Datensatz- und Zuordnungsfelder zuweisen**: Zeigt an, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, dem der Datensatz entspricht.

Nachdem Sie Ihren Datenfluss überprüft haben, klicken Sie auf **[!UICONTROL Beenden]** und gewähren Sie etwas Zeit für die Erstellung des Datenflusses.

![Der Schritt &quot;Überprüfen&quot;des Ursprungs-Workflows.](../../../../images/tutorials/create/snowflake-streaming/review.png)

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich einen Streaming-Datenfluss für [!DNL Snowflake] -Daten erstellt. Weitere Ressourcen finden Sie in der folgenden Dokumentation.

### Überwachen Ihres Datenflusses

Nachdem Ihr Datenfluss erstellt wurde, können Sie die erfassten Daten überwachen, um Informationen zu Erfassungsraten, Erfolg und Fehlern anzuzeigen. Weitere Informationen zum Überwachen von Streaming-Datenflüssen finden Sie im Tutorial zum [Überwachen von Streaming-Datenflüssen in der Benutzeroberfläche](../../monitor-streaming.md).

### Aktualisieren des Datenflusses

Um Konfigurationen für die Planung, Zuordnung und allgemeine Informationen Ihrer Datenflüsse zu aktualisieren, besuchen Sie das Tutorial zum Aktualisieren der Datenflüsse für Quellen in der Benutzeroberfläche ](../../update-dataflows.md).[

### Löschen des Datenflusses

Datenflüsse, die nicht mehr erforderlich sind oder nicht korrekt erstellt wurden, können Sie löschen, indem Sie dazu die Funktion **[!UICONTROL Löschen]** im Arbeitsbereich **[!UICONTROL Datenflüsse]** verwenden. Weitere Informationen zum Löschen von Datenflüssen finden Sie im Tutorial zum Löschen von Datenflüssen in der Benutzeroberfläche ](../../delete.md).[
