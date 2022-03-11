---
keywords: Experience Platform; Startseite; beliebte Themen; Marketing Automation Connector
solution: Experience Platform
title: Erstellen eines Datenflusses mithilfe einer Marketing-Automatisierungsquelle in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Ein Datenfluss ist eine geplante Aufgabe, die Daten aus einer Quelle abruft und in einen Platform-Datensatz aufnimmt. In diesem Tutorial erfahren Sie, wie Sie einen Datenfluss für eine Marketing-Automatisierungsquelle mithilfe der Platform-Benutzeroberfläche erstellen.
exl-id: 8d31fc2d-b952-44f7-98e7-f51b0acc19ed
source-git-commit: a9a443eda060606be4394dfc2e2707fe18618160
workflow-type: tm+mt
source-wordcount: '1395'
ht-degree: 12%

---

# Erstellen eines Datenflusses mithilfe einer Marketing-Automatisierungsquelle in der Benutzeroberfläche

Ein Datenfluss ist eine geplante Aufgabe, die Daten aus einer Quelle abruft und in einen Datensatz in Adobe Experience Platform aufnimmt. In diesem Tutorial erfahren Sie, wie Sie mithilfe der Platform-Benutzeroberfläche einen Datenfluss für eine Marketing-Automatisierungsquelle erstellen.

>[!NOTE]
>
>Um einen Datenfluss zu erstellen, müssen Sie bereits über ein authentifiziertes Konto mit einer Marketing-Automatisierungsquelle verfügen. Eine Liste der Tutorials zum Erstellen verschiedener Quell-Konten für die Marketing-Automatisierung in der Benutzeroberfläche finden Sie im [Quellen - Übersicht](../../../home.md#marketing-automation).

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Platform voraus:

* [Quellen](../../../home.md): Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten zu strukturieren, zu beschriften und zu erweitern, indem [!DNL Platform] Dienste.
* [[!DNL Experience Data Model (XDM)] System](../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemas vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-time Customer Profile]](../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
* [[!DNL Data Prep]](../../../../data-prep/home.md): Ermöglicht es Dateningenieuren, Daten dem Experience-Datenmodell (XDM) zuzuordnen, umzuwandeln und zu validieren.

## Hinzufügen von Daten

Nach der Erstellung Ihres Quell-Kontos für die Marketing-Automatisierung muss die **[!UICONTROL Daten hinzufügen]** angezeigt. Dieser Schritt bietet eine Oberfläche, über die Sie die Tabellenhierarchie Ihres Kontos für die Marketing-Automatisierungsquelle ermitteln können.

* In der linken Hälfte der Benutzeroberfläche befindet sich ein Browser, der eine Liste der in Ihrem Konto enthaltenen Datentabellen anzeigt. Die Benutzeroberfläche enthält außerdem eine Suchoption, mit der Sie die Quelldaten, die Sie verwenden möchten, schnell identifizieren können.
* Die rechte Hälfte der Benutzeroberfläche ist ein Vorschaufenster, mit dem Sie bis zu 100 Datenzeilen in der Vorschau anzeigen können.

>[!NOTE]
>
>Die Option &quot;Suchquellendaten&quot;steht allen tabellenbasierten Quellen außer der Adobe Analytics zur Verfügung. [!DNL Amazon Kinesis]und [!DNL Azure Event Hubs].

Nachdem Sie die Quelldaten gefunden haben, wählen Sie die Tabelle aus und klicken Sie auf **[!UICONTROL Nächste]**.

![select-data](../../../images/tutorials/dataflow/table-based/select-data.png)

## Datenflussdetails angeben

Die [!UICONTROL Datenflussdetails] -Seite können Sie auswählen, ob Sie einen vorhandenen Datensatz oder einen neuen Datensatz verwenden möchten. Während dieses Vorgangs können Sie auch Einstellungen für [!UICONTROL Profildatensatz], [!UICONTROL Fehlerdiagnose], [!UICONTROL Partielle Erfassung]und [!UICONTROL Warnhinweise].

![dataflow-detail](../../../images/tutorials/dataflow/table-based/dataflow-detail.png)

### Vorhandenen Datensatz verwenden

Um Daten in einen vorhandenen Datensatz zu erfassen, wählen Sie **[!UICONTROL Vorhandener Datensatz]**. Sie können einen vorhandenen Datensatz entweder über die Option [!UICONTROL Erweiterte Suche] oder durch Scrollen durch die Liste der vorhandenen Datensätze im Dropdown-Menü abrufen. Nachdem Sie einen Datensatz ausgewählt haben, geben Sie einen Namen und eine Beschreibung für Ihren Datenfluss ein.

![existing-dataset](../../../images/tutorials/dataflow/table-based/existing-dataset.png)

### Verwenden eines neuen Datensatzes

Um einen neuen Datensatz zu erfassen, wählen Sie **[!UICONTROL Neuer Datensatz]** und geben Sie dann einen Namen für den Ausgabedatensatz und eine optionale Beschreibung an. Wählen Sie als Nächstes mithilfe der Option [!UICONTROL Erweiterte Suche] oder durch Scrollen durch die Liste der vorhandenen Schemas im Dropdown-Menü ein Schema zum Zuordnen aus. Geben Sie nach Auswahl eines Schemas einen Namen und eine Beschreibung für Ihren Datenfluss ein.

![new-dataset](../../../images/tutorials/dataflow/table-based/new-dataset.png)

### Aktivieren [!DNL Profile] und Fehlerdiagnose

Wählen Sie als Nächstes die **[!UICONTROL Profildatensatz]** Umschalten auf die Aktivierung Ihres Datensatzes für [!DNL Profile]. Auf diese Weise können Sie eine ganzheitliche Ansicht der Attribute und Verhaltensweisen einer Entität erstellen. Daten aus allen [!DNL Profile]-aktivierte Datensätze werden in [!DNL Profile] und Änderungen werden angewendet, wenn Sie Ihren Datenfluss speichern.

[!UICONTROL Fehlerdiagnose] ermöglicht eine detaillierte Erstellung von Fehlermeldungen für alle fehlerhaften Datensätze, die in Ihrem Datenfluss auftreten, während [!UICONTROL Partielle Aufnahme] die Aufnahme von fehlerhaften Daten bis zu einem gewissen Schwellenwert, den Sie manuell definieren, ermöglicht. Weitere Informationen finden Sie in der [Übersicht zur partiellen Batch-Aufnahme](../../../../ingestion/batch-ingestion/partial.md).

![profile-and-errors](../../../images/tutorials/dataflow/table-based/profile-and-errors.png)

### Warnhinweise aktivieren

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status Ihres Datenflusses zu erhalten. Wählen Sie einen Warnhinweis aus der Liste aus, um Benachrichtigungen zum Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnungen finden Sie im Handbuch zu [Abrufen von Warnhinweisen zu Quellen über die Benutzeroberfläche](../alerts.md).

Wenn Sie mit der Bereitstellung von Details für Ihren Datenfluss fertig sind, wählen Sie **[!UICONTROL Nächste]**.

![Warnungen](../../../images/tutorials/dataflow/table-based/alerts.png)

## Zuordnen von Datenfeldern zu einem XDM-Schema

Die [!UICONTROL Zuordnung] -Schritt angezeigt werden. Sie erhalten eine Schnittstelle, über die Sie die Quellfelder aus Ihrem Quellschema den entsprechenden Ziel-XDM-Feldern im Zielschema zuordnen können.

Platform bietet intelligente Empfehlungen für automatisch zugeordnete Felder, die auf dem von Ihnen ausgewählten Zielschema oder Datensatz basieren. Sie können die Zuordnungsregeln manuell an Ihre Anwendungsfälle anpassen. Je nach Bedarf können Sie Felder direkt zuordnen oder mithilfe von Datenvorbereitungsfunktionen Quelldaten transformieren, um berechnete oder berechnete Werte abzuleiten. Umfassende Schritte zur Verwendung der Mapper-Oberfläche und der berechneten Felder finden Sie im Abschnitt [Handbuch zur Datenvorbereitung-Benutzeroberfläche](../../../../data-prep/ui/mapping.md).

Nachdem die Quelldaten erfolgreich zugeordnet wurden, wählen Sie **[!UICONTROL Nächste]**.

![Mapping](../../../images/tutorials/dataflow/table-based/mapping.png)

## Erfassungsläufe planen

Die [!UICONTROL Planung] angezeigt, sodass Sie einen Aufnahmezeitplan konfigurieren können, um die ausgewählten Quelldaten mithilfe der konfigurierten Zuordnungen automatisch zu erfassen. Standardmäßig ist die Planung auf `Once`. Um die Aufnahmefrequenz anzupassen, wählen Sie **[!UICONTROL Häufigkeit]** und wählen Sie dann eine Option aus dem Dropdown-Menü aus.

>[!TIP]
>
>Während einer einmaligen Erfassung sind Intervall und Aufstockung nicht sichtbar.

![scheduling](../../../images/tutorials/dataflow/table-based/scheduling.png)

Wenn Sie die Aufnahmefrequenz auf `Minute`, `Hour`, `Day`oder `Week`, müssen Sie ein Intervall festlegen, um einen bestimmten Zeitrahmen zwischen jeder Aufnahme festzulegen. Eine Erfassungsfrequenz, die beispielsweise auf `Day` und ein Intervall, das auf `15` bedeutet, dass Ihr Datenfluss alle 15 Tage Daten aufnehmen soll.

Während dieses Schritts können Sie auch **Aufstockung** und definieren eine Spalte für die inkrementelle Datenaufnahme. Die Aufstockung wird verwendet, um historische Daten zu erfassen, während die Spalte, die Sie für die inkrementelle Erfassung definieren, es ermöglicht, neue Daten von vorhandenen Daten zu unterscheiden.

Weitere Informationen zu Planungskonfigurationen finden Sie in der Tabelle unten.

| Feld | Beschreibung |
| --- | --- |
| Häufigkeit | Die Häufigkeit, mit der eine Aufnahme erfolgt. Selektive Häufigkeiten beinhalten `Once`, `Minute`, `Hour`, `Day`und `Week`. |
| Intervall | Eine Ganzzahl, die das Intervall für die ausgewählte Häufigkeit festlegt. Der Wert des Intervalls sollte eine Ganzzahl ungleich null sein und auf größer oder gleich 15 gesetzt werden. |
| Startzeit | Ein UTC-Zeitstempel, der angibt, wann die erste Aufnahme erfolgen soll. Die Startzeit muss größer oder gleich der aktuellen UTC-Zeit sein. |
| Aufstockung | Ein boolean -Wert, der bestimmt, welche Daten ursprünglich erfasst werden. Wenn die Aufstockung aktiviert ist, werden alle aktuellen Dateien im angegebenen Pfad während der ersten geplanten Erfassung erfasst. Wenn die Aufstockung deaktiviert ist, werden nur die Dateien erfasst, die zwischen der ersten Ausführung der Aufnahme und der Startzeit geladen werden. Dateien, die vor der Startzeit geladen wurden, werden nicht erfasst. |
| Inkrementelle Daten laden nach | Eine Option mit einem gefilterten Satz von Quellschemafeldern vom Typ, Datum oder Uhrzeit. Dieses Feld wird verwendet, um zwischen neuen und vorhandenen Daten zu unterscheiden. Inkrementelle Daten werden basierend auf dem Zeitstempel der ausgewählten Spalte erfasst. |

![Aufstockung](../../../images/tutorials/dataflow/table-based/backfill.png)

## Überprüfen Sie Ihren Datenfluss.

Die **[!UICONTROL Überprüfen]** angezeigt, sodass Sie Ihren neuen Datenfluss überprüfen können, bevor er erstellt wird. Details werden in die folgenden Kategorien eingeteilt:

* **[!UICONTROL Verbindung]**: Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quelldatei und die Anzahl der Spalten in dieser Quelldatei an.
* **[!UICONTROL Datensatz- und Zuordnungsfelder zuweisen]**: Zeigt, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, dem der Datensatz entspricht.
* **[!UICONTROL Planung]**: Zeigt den aktiven Zeitraum, die Häufigkeit und das Intervall des Aufnahmezeitplans an.

Nachdem Sie Ihren Datenfluss überprüft haben, wählen Sie **[!UICONTROL Beenden]** und lassen Sie etwas Zeit für die Erstellung des Datenflusses zu.

![Überprüfung](../../../images/tutorials/dataflow/table-based/review.png)

## Überwachen Ihres Datenflusses

Nachdem Ihr Datenfluss erstellt wurde, können Sie die erfassten Daten überwachen, um Informationen zu Erfassungsraten, Erfolg und Fehlern zu erhalten. Weitere Informationen zum Überwachen des Datenflusses finden Sie im Tutorial zu [Überwachen von Konten und Datenflüssen in der Benutzeroberfläche](../monitor.md).

## Datenfluss löschen

Sie können Datenflüsse löschen, die nicht mehr erforderlich sind oder falsch erstellt wurden, indem Sie die Variable **[!UICONTROL Löschen]** -Funktion im **[!UICONTROL Datenflüsse]** Arbeitsbereich. Weitere Informationen zum Löschen von Datenflüssen finden Sie im Tutorial zu [Löschen von Datenflüssen in der Benutzeroberfläche](../delete.md).

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich einen Datenfluss erstellt, um Daten aus Ihrer Marketing-Automatisierungsquelle an Platform zu übertragen. Eingehende Daten können jetzt von nachgelagerten Systemen verwendet werden [!DNL Platform] Dienste wie [!DNL Real-time Customer Profile] und [!DNL Data Science Workspace]. Weitere Informationen finden Sie in den folgenden Dokumenten:

* [[!DNL Real-time Customer Profile] – Übersicht](../../../../profile/home.md)
* [[!DNL Data Science Workspace] – Übersicht](../../../../data-science-workspace/home.md)


>[!WARNING]
>
> Die im folgenden Video dargestellte Platform-Benutzeroberfläche ist veraltet. In der obigen Dokumentation finden Sie die neuesten Screenshots und Funktionen der Benutzeroberfläche.
>
>[!VIDEO](https://video.tv.adobe.com/v/29711?quality=12&learn=on)