---
keywords: Experience Platform;home;popular topics;dataflow;Dataflow
title: Konfigurieren eines Datenflusses zum Aufnehmen von Batch-Daten aus einer Cloud Storage-Source in der Benutzeroberfläche
description: In diesem Tutorial erfahren Sie, wie Sie einen neuen Datenfluss konfigurieren, um Batch-Daten aus einer Cloud-Speicherquelle in der Benutzeroberfläche zu erfassen
exl-id: b327bbea-039d-4c04-afd3-f1d6a5f902a6
source-git-commit: 48aef63cffbdc52a6a96ef69e5db4f54274144b6
workflow-type: tm+mt
source-wordcount: '1926'
ht-degree: 29%

---

# Konfigurieren eines Datenflusses zum Erfassen von Batch-Daten aus einer Cloud-Speicherquelle in der Benutzeroberfläche

In diesem Tutorial erfahren Sie, wie Sie einen Datenfluss konfigurieren, um Batch-Daten von Ihrer Cloud-Speicherquelle an Adobe Experience Platform zu übertragen.

## Erste Schritte

>[!NOTE]
>
>Um einen Datenfluss zu erstellen, der Batch-Daten aus einem Cloud-Speicher bringt, müssen Sie bereits Zugriff auf eine authentifizierte Cloud-Speicherquelle haben. Wenn Sie keinen Zugriff haben, finden Sie in der [Quellenübersicht](../../../../home.md#cloud-storage) eine Liste der Cloud-Speicher-Quellen, mit denen Sie ein Konto erstellen können.

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

### Unterstützte Dateiformate

Cloud-Speicherquellen für Batch-Daten unterstützen die folgenden Dateiformate für die Erfassung:

* Trennzeichen-Werte (DSV): Jeder einzelne Wert kann als Trennzeichen für DSV-formatierte Datendateien verwendet werden.
* [!DNL JavaScript Object Notation] (JSON): JSON-formatierte Datendateien müssen XDM-konform sein.
* [!DNL Apache Parquet]: Parquet-formatierte Datendateien müssen XDM-konform sein.
* Komprimierte Dateien: JSON- und durch Trennzeichen getrennte Dateien können wie folgt komprimiert werden: `bzip2`, `gzip`, `deflate`, `zipDeflate`, `tarGzip` und `tar`.

## Daten hinzufügen

Nachdem Sie Ihr Cloud-Speicherkonto erstellt haben, wird der Schritt **[!UICONTROL Daten hinzufügen]** angezeigt. Dort können Sie Ihre Cloud-Speicher-Dateihierarchie durchsuchen und den Ordner oder die spezifische Datei auswählen, den/die Sie in Platform laden möchten.

* Der linke Teil der Benutzeroberfläche ist ein Ordner-Browser, der Ihre Cloud-Speicher-Dateihierarchie anzeigt.
* Im rechten Bereich der Benutzeroberfläche können Sie eine Vorschau von bis zu 100 Zeilen mit Daten aus einem kompatiblen Ordner oder einer kompatiblen Datei anzeigen.

![](../../../../images/tutorials/dataflow/cloud-batch/select-data.png)

Wählen Sie den Stammordner aus, um auf Ihre Ordnerhierarchie zuzugreifen. Von hier aus können Sie einen einzelnen Ordner auswählen, um alle Dateien rekursiv in den Ordner aufzunehmen. Beim Erfassen eines ganzen Ordners müssen Sie sicherstellen, dass alle Dateien in diesem Ordner dasselbe Datenformat und Schema aufweisen.

![](../../../../images/tutorials/dataflow/cloud-batch/folder-directory.png)

Nachdem Sie einen Ordner ausgewählt haben, wird die richtige Oberfläche aktualisiert, um eine Vorschau des Inhalts und der Struktur der ersten Datei im ausgewählten Ordner anzuzeigen.

![](../../../../images/tutorials/dataflow/cloud-batch/select-folder.png)

Während dieses Schritts können Sie mehrere Konfigurationen an Ihren Daten vornehmen, bevor Sie fortfahren. Wählen Sie zunächst **[!UICONTROL Datenformat]** und dann im angezeigten Dropdown-Bedienfeld das entsprechende Datenformat für Ihre Datei aus.

In der folgenden Tabelle werden die entsprechenden Datenformate für die unterstützten Dateitypen angezeigt:

| Dateityp | Datenformat |
| --- | --- |
| CSV | [!UICONTROL Getrennt] |
| JSON | [!UICONTROL JSON] |
| Parquet | [!UICONTROL XDM Parquet] |

![](../../../../images/tutorials/dataflow/cloud-batch/data-format.png)

### Spaltentrennzeichen auswählen

Nach der Konfiguration Ihres Datenformats können Sie beim Erfassen von durch Trennzeichen getrennten Dateien ein Spaltentrennzeichen festlegen. Wählen Sie die Option **[!UICONTROL Trennzeichen]** und dann ein Trennzeichen aus dem Dropdown-Menü aus. Im Menü werden die am häufigsten verwendeten Optionen für Trennzeichen angezeigt, darunter ein Komma (`,`), eine Registerkarte (`\t`) und ein senkrechter Strich (`|`).

![](../../../../images/tutorials/dataflow/cloud-batch/delimiter.png)

Wenn Sie lieber ein benutzerdefiniertes Trennzeichen verwenden möchten, wählen Sie &quot;**[!UICONTROL Benutzerdefiniert]**&quot;und geben Sie in die Popup-Eingabeleiste ein Trennzeichen mit einem einzelnen Zeichen Ihrer Wahl ein.

![](../../../../images/tutorials/dataflow/cloud-batch/custom.png)

### Komprimierte Dateien erfassen

Sie können auch komprimierte JSON- oder durch Trennzeichen getrennte Dateien erfassen, indem Sie deren Komprimierungstyp angeben.

Wählen Sie im Schritt [!UICONTROL Daten auswählen] eine komprimierte Datei für die Aufnahme aus und wählen Sie dann den entsprechenden Dateityp aus und ob er XDM-kompatibel ist oder nicht. Wählen Sie als Nächstes **[!UICONTROL Komprimierungstyp]** und dann den entsprechenden komprimierten Dateityp für die Quelldaten aus.

![](../../../../images/tutorials/dataflow/cloud-batch/custom.png)

Um eine bestimmte Datei in Platform zu laden, wählen Sie einen Ordner aus und wählen Sie dann die Datei aus, die Sie aufnehmen möchten. Während dieses Schritts können Sie auch eine Vorschau des Dateiinhalts anderer Dateien in einem bestimmten Ordner anzeigen, indem Sie das Vorschausymbol neben einem Dateinamen verwenden.

Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![](../../../../images/tutorials/dataflow/cloud-batch/select-file.png)

## Angeben von Datenflussdetails

Auf der Seite [!UICONTROL Datenflussdetails] können Sie auswählen, ob Sie einen vorhandenen Datensatz oder einen neuen Datensatz verwenden möchten. Während dieses Vorgangs können Sie Ihre Daten auch so konfigurieren, dass sie in das Profil aufgenommen werden, und Einstellungen wie [!UICONTROL Fehlerdiagnose], [!UICONTROL Partielle Erfassung] und [!UICONTROL Warnhinweise] aktivieren.

![](../../../../images/tutorials/dataflow/cloud-batch/dataflow-detail.png)

### Verwenden eines vorhandenen Datensatzes

Um Daten in einen vorhandenen Datensatz aufzunehmen, wählen Sie **[!UICONTROL Vorhandener Datensatz]**. Sie können einen vorhandenen Datensatz entweder über die Option [!UICONTROL Erweiterte Suche] oder durch Scrollen durch die Liste der vorhandenen Datensätze im Dropdown-Menü abrufen. Nachdem Sie einen Datensatz ausgewählt haben, geben Sie einen Namen und eine Beschreibung für Ihren Datenfluss ein.

![](../../../../images/tutorials/dataflow/cloud-batch/existing.png)

### Verwenden eines neuen Datensatzes

Für ein Aufnehmen in einen neuen Datensatz wählen Sie **[!UICONTROL Neuer Datensatz]** aus und geben Sie einen Namen für den Ausgabedatensatz und eine optionale Beschreibung an. Wählen Sie als Nächstes mithilfe der Option [!UICONTROL Erweiterte Suche] oder durch Scrollen durch die Liste der vorhandenen Schemata im Dropdown-Menü ein Schema zum Zuordnen aus. Nachdem Sie ein Schema ausgewählt haben, geben Sie einen Namen und eine Beschreibung für Ihren Datenfluss ein.

![](../../../../images/tutorials/dataflow/cloud-batch/new.png)

### Profil- und Fehlerdiagnose aktivieren

Wählen Sie als Nächstes den Umschalter **[!UICONTROL Profildatensatz]** aus, um Ihren Datensatz für Profil zu aktivieren. Auf diese Weise können Sie eine ganzheitliche Ansicht der Attribute und Verhaltensweisen einer Entität erstellen. Daten aus allen profilaktivierten Datensätzen werden in das Profil aufgenommen und Änderungen werden angewendet, wenn Sie Ihren Datenfluss speichern.

[!UICONTROL Fehlerdiagnose] ermöglicht eine detaillierte Erstellung von Fehlermeldungen für alle fehlerhaften Datensätze, die in Ihrem Datenfluss auftreten, während [!UICONTROL Partielle Aufnahme] die Aufnahme von fehlerhaften Daten bis zu einem gewissen Schwellenwert, den Sie manuell definieren, ermöglicht. Weitere Informationen finden Sie in der [Übersicht zur partiellen Batch-Aufnahme](../../../../../ingestion/batch-ingestion/partial.md).

![](../../../../images/tutorials/dataflow/cloud-batch/ingestion-configs.png)

### Aktivieren von Warnhinweisen

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status Ihres Datenflusses zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Warnhinweisen zu Quellen über die Benutzeroberfläche](../../alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihren Datenfluss fertig sind, klicken Sie auf **[!UICONTROL Weiter]**.

![](../../../../images/tutorials/dataflow/cloud-batch/alerts.png)

## Zuordnen von Datenfeldern zu einem XDM-Schema

Es erfolgt der Schritt der [!UICONTROL Zuordnung], in dem Ihnen eine Schnittstelle zum Zuordnen der Quellfelder aus Ihrem Quellschema zu den entsprechenden XDM-Zielfeldern im Zielschema bereitgestellt wird.

Platform bietet intelligente Empfehlungen für automatisch zugeordnete Felder, die auf dem ausgewählten Zielschema oder Datensatz basieren. Sie können die Zuordnungsregeln manuell an Ihre Anwendungsfälle anpassen. Je nach Bedarf können Sie wahlweise Felder direkt zuordnen oder mithilfe von Datenvorbereitungsfunktionen Quelldaten transformieren, um berechnete oder anderweitig ermittelte Werte abzuleiten. Umfassende Schritte zur Verwendung der Zuordnungsoberfläche und der berechneten Felder finden Sie im Handbuch [Data Prep UI guide](../../../../../data-prep/ui/mapping.md).

Nachdem die Quelldaten erfolgreich zugeordnet wurden, wählen Sie **[!UICONTROL Weiter]** aus.

![](../../../../images/tutorials/dataflow/cloud-batch/mapping.png)

## Erfassungsläufe planen

>[!IMPORTANT]
>
>Es wird dringend empfohlen, Ihren Datenfluss für die einmalige Erfassung bei Verwendung der [FTP-Quelle](../../../../connectors/cloud-storage/ftp.md) zu planen.

Der Schritt [!UICONTROL Planung] wird angezeigt, in dem Sie einen Aufnahmeplan konfigurieren können, um die ausgewählten Quelldaten mithilfe der konfigurierten Zuordnungen automatisch zu erfassen. Standardmäßig ist die Planung auf `Once` eingestellt. Um die Aufnahmefrequenz anzupassen, wählen Sie **[!UICONTROL Häufigkeit]** und dann eine Option aus dem Dropdown-Menü aus.

>[!TIP]
>
>Während einer einmaligen Erfassung sind Intervall und Aufstockung nicht sichtbar.

![ scheduling](../../../../images/tutorials/dataflow/cloud-batch/scheduling.png)

Wenn Sie die Aufnahmefrequenz auf `Minute`, `Hour`, `Day` oder `Week` festlegen, müssen Sie ein Intervall festlegen, um einen bestimmten Zeitrahmen zwischen jeder Aufnahme festzulegen. Beispielsweise bedeutet eine Erfassungsfrequenz, die auf &quot;`Day`&quot;und ein auf &quot;`15`&quot;festgelegtes Intervall, dass Ihr Datenfluss alle 15 Tage Daten aufnehmen soll.

Während dieses Schritts können Sie auch **Aufstockung** aktivieren und eine Spalte für die inkrementelle Aufnahme von Daten definieren. Die Aufstockung wird verwendet, um historische Daten zu erfassen, während die Spalte, die Sie für die inkrementelle Erfassung definieren, es ermöglicht, neue Daten von vorhandenen Daten zu unterscheiden.

Weitere Informationen zu Planungskonfigurationen finden Sie in der Tabelle unten.

| Planungskonfiguration | Beschreibung |
| --- | --- |
| Häufigkeit | Konfigurieren Sie die Häufigkeit, mit der der Datenfluss ausgeführt werden soll. Sie können die Häufigkeit wie folgt einstellen: <ul><li>**Einmal**: Setzen Sie Ihre Häufigkeit auf `once`, um eine einmalige Erfassung zu erstellen. Konfigurationen für Intervall und Aufstockung sind beim Erstellen eines einmaligen Erfassungsdataflods nicht verfügbar. Standardmäßig ist die Planung auf einmal eingestellt.</li><li>**Minute**: Setzen Sie Ihre Häufigkeit auf `minute` , um Ihren Datenfluss so zu planen, dass Daten pro Minute erfasst werden.</li><li>**Stunde**: Setzen Sie Ihre Häufigkeit auf &quot;`hour`&quot;, um Ihren Datenfluss so zu planen, dass er Daten pro Stunde erfasst.</li><li>**Tag**: Setzen Sie Ihre Häufigkeit auf &quot;`day`&quot;, um Ihren Datenfluss so zu planen, dass er Daten pro Tag erfasst.</li><li>**Woche**: Setzen Sie Ihre Häufigkeit auf &quot;`week`&quot;, um Ihren Datenfluss so zu planen, dass er Daten pro Woche erfasst.</li></ul> |
| Intervall | Nachdem Sie eine Frequenz ausgewählt haben, können Sie die Intervalleinstellung konfigurieren, um den Zeitrahmen zwischen jeder Aufnahme festzulegen. Wenn Sie beispielsweise Ihre Häufigkeit auf &quot;Tag&quot;festlegen und das Intervall auf 15 konfigurieren, wird Ihr Datenfluss alle 15 Tage ausgeführt. Sie können das Intervall nicht auf null festlegen. Der akzeptierte Mindestintervallwert für jede Frequenz lautet wie folgt:<ul><li>**Einmal**: nicht zutreffend</li><li>**Minute**: 15</li><li>**Hour**: 1</li><li>**Tag**: 1</li><li>**Woche**: 1</li></ul> |
| Startzeit | Der Zeitstempel für die projizierte Ausführung, dargestellt in UTC-Zeitzone. |
| Aufstockung | Die Aufstockung bestimmt, welche Daten ursprünglich erfasst werden. Wenn die Aufstockung aktiviert ist, werden alle aktuellen Dateien im angegebenen Pfad während der ersten geplanten Erfassung erfasst. Wenn die Aufstockung deaktiviert ist, werden nur die Dateien erfasst, die zwischen der ersten Ausführung der Aufnahme und der Startzeit geladen werden. Dateien, die vor der Startzeit geladen wurden, werden nicht erfasst. |

>[!NOTE]
>
>Bei der Batch-Aufnahme wählt jeder nachfolgende Datenfluss die aufzunehmenden Dateien aus Ihrer Quelle anhand ihres **zuletzt geänderten** Zeitstempels aus. Das bedeutet, dass Batch-Datenflüsse ausgewählte Dateien aus der Quelle auswählen, die neu sind oder seit der letzten Flussausführung geändert wurden. Darüber hinaus müssen Sie sicherstellen, dass zwischen dem Datei-Upload und einem geplanten Ablauf ausreichend Zeit ist, da Dateien, die nicht vollständig in Ihr Cloud-Speicherkonto hochgeladen wurden, bevor die geplante Flusslaufzeit möglicherweise nicht zur Aufnahme abgerufen wird.

Wählen Sie nach Abschluss der Konfiguration Ihres Aufnahmezeitplans **[!UICONTROL Weiter]** aus.

![](../../../../images/tutorials/dataflow/cloud-batch/scheduling-configs.png)

## Überprüfen des Datenflusses

Der Schritt **[!UICONTROL Überprüfung]** wird angezeigt, sodass Sie Ihren neuen Datenfluss überprüfen können, bevor er hergestellt wird. Die Details lassen sich wie folgt kategorisieren:

* **[!UICONTROL Verbindung]**: Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quelldatei und die Anzahl der Spalten innerhalb dieser Quelldatei an.
* **[!UICONTROL Datensatz- und Zuordnungsfelder zuweisen]**: Zeigt an, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, dem der Datensatz entspricht.
* **[!UICONTROL Planung]**: Zeigt den aktiven Zeitraum, die Häufigkeit und das Intervall des Aufnahmezeitplans an.

Nachdem Sie Ihren Datenfluss überprüft haben, klicken Sie auf **[!UICONTROL Beenden]** und lassen Sie die Erstellung des Datenflusses etwas Zeit zu.

![](../../../../images/tutorials/dataflow/cloud-batch/review.png)


## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich einen Datenfluss erstellt, um Daten aus einem externen Cloud-Speicher einzubringen und Einblicke in die Überwachung von Datensätzen zu erhalten. Um mehr über die Erstellung von Datenflüssen zu erfahren, ergänzen Sie Ihr Lernen, indem Sie sich das folgende Video ansehen. Darüber hinaus können eingehende Daten jetzt von nachgelagerten [!DNL Platform]-Diensten wie [!DNL Real-Time Customer Profile] und [!DNL Data Science Workspace] verwendet werden. Weiterführende Informationen finden Sie in folgenden Dokumenten:

* [[!DNL Real-Time Customer Profile] – Übersicht](../../../../../profile/home.md)
* [[!DNL Data Science Workspace] – Übersicht](../../../../../data-science-workspace/home.md)

>[!WARNING]
>
> Die im folgenden Video angezeigte [!DNL Platform]-Benutzeroberfläche ist veraltet. Die neuesten Screenshots und Funktionen der Benutzeroberfläche finden Sie in der obigen Dokumentation.

>[!VIDEO](https://video.tv.adobe.com/v/29695?quality=12&learn=on)

## Anhang

Die folgenden Abschnitte enthalten zusätzliche Informationen zum Arbeiten mit Quell-Connectoren.

## Überwachen Ihres Datenflusses

Nachdem Ihr Datenfluss erstellt wurde, können Sie die erfassten Daten überwachen, um Informationen zu Erfassungsraten, Erfolg und Fehlern anzuzeigen. Weitere Informationen zum Überwachen des Datenflusses finden Sie im Tutorial zum [Überwachen von Konten und Datenflüssen in der Benutzeroberfläche](../../monitor.md).

## Aktualisieren des Datenflusses

Um Konfigurationen für die Planung, Zuordnung und allgemeine Informationen Ihrer Datenflüsse zu aktualisieren, besuchen Sie das Tutorial zum Aktualisieren der Datenflüsse für Quellen in der Benutzeroberfläche ](../../update-dataflows.md) .[

## Löschen des Datenflusses

Datenflüsse, die nicht mehr erforderlich sind oder nicht korrekt erstellt wurden, können Sie löschen, indem Sie dazu die Funktion **[!UICONTROL Löschen]** im Arbeitsbereich **[!UICONTROL Datenflüsse]** verwenden. Weitere Informationen zum Löschen von Datenflüssen finden Sie im Tutorial zum Löschen von Datenflüssen in der Benutzeroberfläche ](../../delete.md).[