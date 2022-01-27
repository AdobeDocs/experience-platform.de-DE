---
keywords: Experience Platform; Startseite; beliebte Themen; Datenfluss; Datenfluss
solution: Experience Platform
title: Konfigurieren eines Datenflusses für einen Cloud-Speicher-Batch-Connector in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Ein Datenfluss ist eine geplante Aufgabe, die Daten aus einer Quelle abruft und in einen Platform-Datensatz aufnimmt. In diesem Tutorial werden Schritte zum Konfigurieren eines neuen Datenflusses mithilfe Ihres Cloud-Speicherkontos beschrieben.
exl-id: b327bbea-039d-4c04-afd3-f1d6a5f902a6
source-git-commit: 86d8313d7acea41e7b3bcea6554e91ea2190ae69
workflow-type: tm+mt
source-wordcount: '2083'
ht-degree: 3%

---

# Konfigurieren eines Datenflusses für eine Cloud-Speicher-Batch-Verbindung in der Benutzeroberfläche

Ein Datenfluss ist eine geplante Aufgabe, die Daten aus einer Quelle abruft und in eine [!DNL Platform] Datensatz. In diesem Tutorial werden Schritte zum Konfigurieren eines neuen Datenflusses mithilfe Ihres Cloud-Speicherkontos beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Der standardisierte Rahmen, durch den [!DNL Experience Platform] organisiert Kundenerlebnisdaten.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Tutorial zum Schema Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Darüber hinaus erfordert dieses Tutorial, dass Sie über ein eingerichtetes Cloud-Speicher-Konto verfügen. Eine Liste der Tutorials zum Erstellen verschiedener Cloud-Speicher-Konten in der Benutzeroberfläche finden Sie im [Übersicht über Quell-Connectoren](../../../../home.md).

### Unterstützte Dateiformate

[!DNL Experience Platform] unterstützt die folgenden Dateiformate, die aus externen Speichern erfasst werden:

* Trennzeichen (DSV): Jeder einzelne Wert kann als Trennzeichen für Datendateien im DSV-Format verwendet werden.
* [!DNL JavaScript Object Notation] (JSON): JSON-formatierte Datendateien müssen XDM-konform sein.
* [!DNL Apache Parquet]: Parquet-formatierte Datendateien müssen XDM-konform sein.
* Komprimierte Dateien: JSON- und durch Trennzeichen getrennte Dateien können wie folgt komprimiert werden: `bzip2`, `gzip`, `deflate`, `zipDeflate`, `tarGzip`und `tar`.

## Daten auswählen

Nachdem Sie Ihr Cloud-Speicherkonto erstellt haben, wird die **[!UICONTROL Daten auswählen]** angezeigt. Dieser Schritt stellt eine Oberfläche bereit, über die Sie die Hierarchie Ihrer Cloud-Speicher-Dateien durchsuchen können.

* Der linke Teil der Benutzeroberfläche ist ein Verzeichnisbrowser, in dem Ihre Cloud-Speicherdateien und -Verzeichnisse angezeigt werden.
* Im rechten Bereich der Benutzeroberfläche können Sie eine Vorschau von bis zu 100 Datenzeilen aus einer kompatiblen Datei anzeigen.

![Benutzeroberfläche](../../../../images/tutorials/dataflow/cloud-storage/batch/interface.png)

Wenn Sie einen aufgelisteten Ordner auswählen, können Sie die Ordnerhierarchie in tiefere Ordner durchlaufen. Sie können einen einzelnen Ordner auswählen, um alle Dateien rekursiv im Ordner aufzunehmen. Beim Erfassen eines ganzen Ordners müssen Sie sicherstellen, dass alle Dateien im Ordner dasselbe Schema nutzen.

Nachdem Sie eine kompatible Datei oder einen kompatiblen Ordner ausgewählt haben, wählen Sie das entsprechende Datenformat aus der [!UICONTROL Datenformat auswählen] Dropdown-Menü.

Die folgende Tabelle zeigt das geeignete Datenformat für die unterstützten Dateitypen:

| Dateityp | Datenformat |
| --- | --- |
| CSV | [!UICONTROL Getrennt] |
| JSON | [!UICONTROL JSON] |
| Parquet | [!UICONTROL XDM Parquet] |

Auswählen **[!UICONTROL JSON]** und warten Sie einige Sekunden, bis die Vorschaufunktion gefüllt ist.

![select-data](../../../../images/tutorials/dataflow/cloud-storage/batch/select-data.png)

>[!NOTE]
>
>Im Gegensatz zu getrennten und JSON-Dateitypen sind formatierte Parquet-Dateien nicht für die Vorschau verfügbar.

Über die Vorschau-Oberfläche können Sie den Inhalt und die Struktur einer Datei überprüfen. Standardmäßig zeigt die Vorschaufunktion die erste Datei im ausgewählten Ordner an.

Um eine andere Datei in der Vorschau anzuzeigen, wählen Sie das Vorschausymbol neben dem Namen der Datei aus, die Sie überprüfen möchten.

![default-preview](../../../../images/tutorials/dataflow/cloud-storage/batch/default-preview.png)

Nachdem Sie den Inhalt und die Struktur der Dateien in Ihrem Ordner überprüft haben, wählen Sie **[!UICONTROL Nächste]** um alle Dateien rekursiv im Ordner zu erfassen.

![select-folder](../../../../images/tutorials/dataflow/cloud-storage/batch/select-folder.png)

Wenn Sie lieber eine bestimmte Datei auswählen möchten, wählen Sie die gewünschte Datei aus und klicken Sie auf **[!UICONTROL Nächste]**.

![select-file](../../../../images/tutorials/dataflow/cloud-storage/batch/select-file.png)

### Festlegen eines benutzerdefinierten Trennzeichens für durch Trennzeichen getrennte Dateien

Sie können beim Erfassen von durch Trennzeichen getrennten Dateien ein benutzerdefiniertes Trennzeichen festlegen. Wählen Sie die **[!UICONTROL Trennzeichen]** und wählen Sie dann ein Trennzeichen aus dem Dropdown-Menü aus. Im Menü werden die am häufigsten verwendeten Optionen für Trennzeichen angezeigt, darunter ein Komma (`,`), eine Registerkarte (`\t`) und einem senkrechten Strich (`|`). Wenn Sie ein benutzerdefiniertes Trennzeichen bevorzugen, wählen Sie **[!UICONTROL Benutzerdefiniert]** und geben Sie in der Popup-Symbolleiste ein einzelnes Trennzeichen Ihrer Wahl ein.

Nachdem Sie Ihr Datenformat ausgewählt und Ihr Trennzeichen festgelegt haben, wählen Sie **[!UICONTROL Nächste]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/delimiter.png)

### Komprimierte Dateien erfassen

Sie können komprimierte JSON- oder durch Trennzeichen getrennte Dateien erfassen, indem Sie deren Komprimierungstyp angeben.

Im [!UICONTROL Daten auswählen] Schritt, wählen Sie eine komprimierte Datei für die Aufnahme aus und wählen Sie dann den entsprechenden Dateityp und ob sie XDM-kompatibel ist oder nicht. Wählen Sie als Nächstes **[!UICONTROL Komprimierungstyp]** und wählen Sie dann den entsprechenden komprimierten Dateityp für Ihre Quelldaten aus.

Wählen Sie bei identifiziertem komprimierten Dateityp die Option **[!UICONTROL Nächste]** um fortzufahren.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/compressed-files.png)

## Zuordnen von Datenfeldern zu einem XDM-Schema

Die **[!UICONTROL Zuordnung]** wird ein Schritt angezeigt, der eine interaktive Oberfläche bereitstellt, über die die Quelldaten einem [!DNL Platform] Datensatz. Quelldateien, die in Parquet formatiert wurden, müssen XDM-konform sein und müssen die Zuordnung nicht manuell konfigurieren. Bei CSV-Dateien ist es erforderlich, die Zuordnung explizit zu konfigurieren. Sie können jedoch festlegen, welche Quelldatenfelder zugeordnet werden sollen. JSON-Dateien, die als XDM-Beschwerde gekennzeichnet sind, müssen nicht manuell konfiguriert werden. Wenn es jedoch nicht als XDM-kompatibel markiert ist, müssen Sie die Zuordnung explizit konfigurieren.

Wählen Sie einen Datensatz für eingehende Daten aus, die in aufgenommen werden sollen. Sie können entweder einen vorhandenen Datensatz verwenden oder einen neuen erstellen.

**Vorhandenen Datensatz verwenden**

Um Daten in einen vorhandenen Datensatz zu erfassen, wählen Sie **[!UICONTROL Vorhandener Datensatz]** und wählen Sie dann das Datensatzsymbol aus.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/use-existing-data.png)

Die **[!UICONTROL Datensatz auswählen]** angezeigt. Suchen Sie den gewünschten Datensatz, wählen Sie ihn aus und klicken Sie auf **[!UICONTROL Weiter]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-existing-dataset.png)

**Verwenden eines neuen Datensatzes**

Um Daten in einen neuen Datensatz zu erfassen, wählen Sie **[!UICONTROL Neuer Datensatz]** und geben Sie einen Namen und eine Beschreibung für den Datensatz in die entsprechenden Felder ein. Um ein Schema hinzuzufügen, können Sie einen vorhandenen Schemanamen in die **[!UICONTROL Schema auswählen]** Dialogfeld. Alternativ können Sie die **[!UICONTROL Erweiterte Schemasuche]** , um nach einem geeigneten Schema zu suchen.

Während dieses Schritts können Sie Ihren Datensatz für [!DNL Real-time Customer Profile] und erstellen Sie eine ganzheitliche Ansicht der Attribute und Verhaltensweisen einer Entität. Daten aus allen aktivierten Datensätzen werden in [!DNL Profile] und Änderungen werden angewendet, wenn Sie Ihren Datenfluss speichern.

Umschalten zwischen **[!UICONTROL Profildatensatz]** Schaltfläche zum Aktivieren Ihres Zieldatensatzes für [!DNL Profile].

![](../../../../images/tutorials/dataflow/cloud-storage/batch/new-dataset.png)

Die **[!UICONTROL Schema auswählen]** angezeigt. Wählen Sie das Schema aus, das Sie auf den neuen Datensatz anwenden möchten, und wählen Sie dann **[!UICONTROL Fertig]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-schema.png)

Je nach Bedarf können Sie Felder direkt zuordnen oder mithilfe von Datenvorbereitungsfunktionen Quelldaten transformieren, um berechnete oder berechnete Werte abzuleiten. Umfassende Schritte zur Verwendung der Mapper-Oberfläche und der berechneten Felder finden Sie im Abschnitt [Handbuch zur Datenvorbereitung-Benutzeroberfläche](../../../../../data-prep/ui/mapping.md).

![](../../../../images/tutorials/dataflow/cloud-storage/batch/mapping.png)

Bei JSON-Dateien können Sie neben der direkten Zuordnung von Feldern zu anderen Feldern Objekte und Arrays anderen Objekten und Arrays direkt zuordnen. Außerdem können Sie komplexe Datentypen wie Arrays in JSON-Dateien mit einem Cloud-Speicher-Quell-Connector in der Vorschau anzeigen und zuordnen.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/source-field-json.png)

![](../../../../images/tutorials/dataflow/cloud-storage/batch/target-field-json.png)

Beachten Sie, dass Sie keine Zuordnung für verschiedene Typen erstellen können. Sie können beispielsweise kein Objekt einem Array oder einem Feld einem Objekt zuordnen.

>[!TIP]
>
>Platform bietet intelligente Empfehlungen für automatisch zugeordnete Felder, die auf dem von Ihnen ausgewählten Zielschema oder Datensatz basieren. Sie können die Zuordnungsregeln manuell an Ihre Anwendungsfälle anpassen.

Auswählen **[!UICONTROL Datenvorschau]** , um die Zuordnungsergebnisse von bis zu 100 Zeilen mit Beispieldaten aus dem ausgewählten Datensatz anzuzeigen.

Während der Vorschau wird die Identitätsspalte als erstes Feld priorisiert, da dies die wichtigsten Informationen ist, die bei der Validierung der Zuordnungsergebnisse erforderlich sind.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/mapping-preview.png)

Nachdem die Quelldaten zugeordnet wurden, wählen Sie **[!UICONTROL Schließen]**.

## Erfassungsläufe planen

Die **[!UICONTROL Planung]** angezeigt, sodass Sie einen Aufnahmezeitplan konfigurieren können, um die ausgewählten Quelldaten mithilfe der konfigurierten Zuordnungen automatisch zu erfassen. In der folgenden Tabelle sind die verschiedenen konfigurierbaren Felder für die Planung aufgeführt:

| Feld | Beschreibung |
| --- | --- |
| Häufigkeit | Selektive Häufigkeiten beinhalten `Once`, `Minute`, `Hour`, `Day`und `Week`. |
| Intervall | Eine Ganzzahl, die das Intervall für die ausgewählte Häufigkeit festlegt. |
| Startzeit | Ein UTC-Zeitstempel, der angibt, wann die erste Aufnahme erfolgen soll. |
| Aufstockung | Ein boolean -Wert, der bestimmt, welche Daten ursprünglich erfasst werden. Wenn **[!UICONTROL Aufstockung]** aktiviert ist, werden alle aktuellen Dateien im angegebenen Pfad während der ersten geplanten Erfassung erfasst. Wenn **[!UICONTROL Aufstockung]** deaktiviert ist, werden nur die Dateien erfasst, die zwischen der ersten Ausführung der Aufnahme und der Startzeit geladen werden. Dateien, die vor der Startzeit geladen wurden, werden nicht erfasst. |

Datenflüsse dienen dazu, Daten automatisch auf geplanter Basis zu erfassen. Wählen Sie zunächst die Aufnahmefrequenz aus. Legen Sie anschließend das Intervall fest, um den Zeitraum zwischen zwei Durchsatzausführungen festzulegen. Der Wert des Intervalls sollte eine Ganzzahl ungleich null sein und auf größer oder gleich 15 gesetzt werden.

Passen Sie zum Festlegen der Startzeit für die Aufnahme das im Feld Startzeit angezeigte Datum und die Uhrzeit an. Alternativ können Sie das Kalendersymbol auswählen, um den Startzeitwert zu bearbeiten. Die Startzeit muss größer oder gleich der aktuellen Uhrzeit in UTC sein.

Geben Sie Werte für den Zeitplan an und wählen Sie **[!UICONTROL Nächste]**.

>[!NOTE]
>
>Bei der Batch-Erfassung wählt jeder darauf folgende Datenfluss Dateien aus, die basierend auf ihren **letzte Änderung** Zeitstempel. Das bedeutet, dass Batch-Datenflüsse ausgewählte Dateien aus der Quelle auswählen, die neu sind oder seit der letzten Flussausführung geändert wurden. Darüber hinaus müssen Sie sicherstellen, dass zwischen dem Datei-Upload und einem geplanten Ablauf ausreichend Zeit ist, da Dateien, die nicht vollständig in Ihr Cloud-Speicherkonto hochgeladen wurden, bevor die geplante Flusslaufzeit möglicherweise nicht zur Aufnahme abgerufen wird.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/scheduling-interval-on.png)

### Einrichten eines Datenflusses zur einmaligen Erfassung

Um die einmalige Erfassung einzurichten, wählen Sie den Dropdown-Pfeil &quot;Häufigkeit&quot;aus und klicken Sie auf **[!UICONTROL Einmal]**. Sie können einen Datensatz weiterhin für eine einmalige Frequenzaufnahme bearbeiten, solange die Startzeit in der Zukunft bleibt. Nach Ablauf der Startzeit kann der Wert für die einmalige Häufigkeit nicht mehr bearbeitet werden. **[!UICONTROL Intervall]** und **[!UICONTROL Aufstockung]** sind beim Einrichten eines einmaligen Aufnahme-Datenflusses nicht sichtbar.

>[!IMPORTANT]
>
>Es wird dringend empfohlen, Ihren Datenfluss für die einmalige Erfassung zu planen, wenn Sie die [FTP-Connector](../../../../connectors/cloud-storage/ftp.md).

Nachdem Sie die entsprechenden Werte für den Zeitplan angegeben haben, wählen Sie **[!UICONTROL Nächste]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/scheduling-once.png)

## Datenflussdetails angeben

Die **[!UICONTROL Datenflussdetails]** angezeigt, sodass Sie einen Namen eingeben und eine kurze Beschreibung zu Ihrem neuen Datenfluss eingeben können.

Während dieses Vorgangs können Sie auch **[!UICONTROL Partielle Erfassung]** und **[!UICONTROL Fehlerdiagnose]**. Aktivieren **[!UICONTROL Partielle Erfassung]** bietet die Möglichkeit, Daten mit Fehlern bis zu einem bestimmten Schwellenwert zu erfassen, den Sie festlegen können. Aktivieren **[!UICONTROL Fehlerdiagnose]** liefert Details zu allen falschen Daten, die separat gebündelt werden. Weitere Informationen finden Sie unter [partielle Batch-Erfassung - Übersicht](../../../../../ingestion/batch-ingestion/partial.md).

Geben Sie Werte für den Datenfluss an und wählen Sie **[!UICONTROL Nächste]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/dataflow-detail.png)

## Überprüfen Sie Ihren Datenfluss.

Die **[!UICONTROL Überprüfen]** angezeigt, sodass Sie Ihren neuen Datenfluss überprüfen können, bevor er erstellt wird. Details werden in die folgenden Kategorien eingeteilt:

* **[!UICONTROL Verbindung]**: Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quelldatei und die Anzahl der Spalten in dieser Quelldatei an.
* **[!UICONTROL Datensatz- und Zuordnungsfelder zuweisen]**: Zeigt, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, dem der Datensatz entspricht.
* **[!UICONTROL Planung]**: Zeigt den aktiven Zeitraum, die Häufigkeit und das Intervall des Aufnahmezeitplans an.

Nachdem Sie Ihren Datenfluss überprüft haben, klicken Sie auf **[!UICONTROL Beenden]** und lassen Sie etwas Zeit für die Erstellung des Datenflusses zu.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/review.png)

## Überwachen Ihres Datenflusses

Nachdem Ihr Datenfluss erstellt wurde, können Sie die erfassten Daten überwachen, um Informationen zu Erfassungsraten, Erfolg und Fehlern zu erhalten. Weitere Informationen zum Überwachen des Datenflusses finden Sie im Tutorial zu [Überwachen von Konten und Datenflüssen in der Benutzeroberfläche](../../monitor.md).

## Datenfluss löschen

Sie können Datenflüsse löschen, die nicht mehr erforderlich sind oder falsch erstellt wurden, indem Sie die Variable **[!UICONTROL Löschen]** -Funktion im **[!UICONTROL Datenflüsse]** Arbeitsbereich. Weitere Informationen zum Löschen von Datenflüssen finden Sie im Tutorial zu [Löschen von Datenflüssen in der Benutzeroberfläche](../../delete.md).

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich einen Datenfluss erstellt, um Daten aus einem externen Cloud-Speicher einzubringen und Einblicke in die Überwachung von Datensätzen zu erhalten. Um mehr über die Erstellung von Datenflüssen zu erfahren, ergänzen Sie Ihr Lernen, indem Sie sich das folgende Video ansehen. Darüber hinaus können eingehende Daten jetzt von nachgelagerten [!DNL Platform] Dienste wie [!DNL Real-time Customer Profile] und [!DNL Data Science Workspace]. Weitere Informationen finden Sie in den folgenden Dokumenten:

* [[!DNL Real-time Customer Profile] – Übersicht](../../../../../profile/home.md)
* [[!DNL Data Science Workspace] – Übersicht](../../../../../data-science-workspace/home.md)

>[!WARNING]
>
> Die im folgenden Video angezeigte [!DNL Platform]-Benutzeroberfläche ist veraltet. In der obigen Dokumentation finden Sie die neuesten Screenshots und Funktionen der Benutzeroberfläche.

>[!VIDEO](https://video.tv.adobe.com/v/29695?quality=12&learn=on)

## Anhang

Die folgenden Abschnitte enthalten zusätzliche Informationen zum Arbeiten mit Quell-Connectoren.

### Datenfluss deaktivieren

Wenn ein Datenfluss erstellt wird, wird er sofort aktiv und erfasst Daten gemäß dem festgelegten Zeitplan. Sie können einen aktiven Datenfluss jederzeit deaktivieren, indem Sie die unten stehenden Anweisungen befolgen.

Innerhalb der **[!UICONTROL Quellen]** Klicken Sie auf den **[!UICONTROL Durchsuchen]** Registerkarte. Klicken Sie anschließend auf den Namen des Kontos, das dem aktiven Datenfluss zugeordnet ist, den Sie deaktivieren möchten.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

Die **[!UICONTROL Quellaktivität]** angezeigt. Wählen Sie den aktiven Datenfluss aus der Liste aus, um ihn zu öffnen **[!UICONTROL Eigenschaften]** auf der rechten Bildschirmseite, die eine **[!UICONTROL Aktiviert]** Schaltfläche ein/aus. Klicken Sie auf den Umschalter, um den Datenfluss zu deaktivieren. Derselbe Umschalter kann verwendet werden, um einen Datenfluss erneut zu aktivieren, nachdem er deaktiviert wurde.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/disable-source.png)

### Eingehende Daten aktivieren für [!DNL Profile] population

Eingehende Daten aus Ihrem Quell-Connector können zur Anreicherung und zum Ausfüllen Ihrer [!DNL Real-time Customer Profile] Daten. Weitere Informationen zum Ausfüllen der [!DNL Real-time Customer Profile] -Daten, siehe Tutorial zu [Profilpopulation](../../profile.md).
