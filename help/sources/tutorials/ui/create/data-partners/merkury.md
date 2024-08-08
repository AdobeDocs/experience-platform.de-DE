---
title: Erstellen Sie eine Source-Verbindung mit einer Enterprise Identity-Lösung für Merkury und einen Datenfluss in der Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Quellverbindung zur Enterprise Identity-Lösung für Merkury erstellen.
last-substantial-update: 2023-12=12
badge: Beta
exl-id: 2af48c18-76f9-4615-8e76-8f030a312a8f
source-git-commit: d048109141168b33795753c4706dac64cdf29ca5
workflow-type: tm+mt
source-wordcount: '2143'
ht-degree: 29%

---

# Erstellen einer [!DNL Merkury Enterprise Identity Resolution]-Quellverbindung und eines Datenflusses in der Benutzeroberfläche

>[!NOTE]
>
>Die [!DNL Merkury Enterprise Identity Resolution]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta-beschrifteten Quellen finden Sie in der [Quellenübersicht](../../../../home.md#terms-and-conditions) .

In diesem Tutorial erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine [!DNL Merkury Enterprise Identity Resolution]-Quellverbindung und einen Datenfluss erstellen.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

### Sammeln erforderlicher Anmeldedaten

Um auf Ihren Bucket auf dem Experience Platform zuzugreifen, müssen Sie gültige Werte für die folgenden Anmeldedaten angeben:

| Anmeldedaten | Beschreibung |
| --- | --- |
| Zugriffsschlüssel | Die Zugriffsschlüssel-ID für Ihren Behälter. Sie können diesen Wert aus Ihrem [!DNL Merkury]-Team abrufen. |
| Geheimer Schlüssel | Die geheime Schlüssel-ID für Ihren Bucket. Sie können diesen Wert aus Ihrem [!DNL Merkury]-Team abrufen. |
| Behältername | Dies ist Ihr Merkury-Bucket, in dem Dateien freigegeben werden. Sie können diesen Wert aus Ihrem [!DNL Merkury]-Team abrufen. |

Weitere Informationen zum Einrichten für [!DNL Merkury] und andere Voraussetzungen finden Sie in der [[!DNL Merkury] Quellübersicht](../../../../connectors/data-partners/merkury.md).

## Ihr Merkur-Konto verbinden

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Quellen]** in der linken Navigationsleiste, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie **[!UICONTROL Datenpartner]** die Option **[!UICONTROL Merkury]** und dann **[!UICONTROL Einrichten]** aus.

![Der Quellkatalog mit der ausgewählten Merkury-Quelle.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/catalog.png)

Die Seite **[!UICONTROL Verbindung zu Merkury herstellen]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Neues Konto erstellen

Wenn Sie neue Anmeldedaten verwenden, wählen Sie **[!UICONTROL Neues Konto]** aus. Geben Sie im angezeigten Formular einen Namen, eine optionale Beschreibung und Ihre [!DNL Merkury]-Anmeldedaten ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und lassen Sie dann etwas Zeit, bis die neue Verbindung hergestellt ist.

![Die neue Kontoschnittstelle für Merkury](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/new-account.png).

### Vorhandenes Konto verwenden

Um ein vorhandenes Konto zu verwenden, wählen Sie **[!UICONTROL Vorhandenes Konto]** und dann das gewünschte [!DNL Merkury]-Konto aus. Klicken Sie auf **[!UICONTROL Weiter]**, um fortzufahren.

![Die vorhandene Kontoschnittstelle für Merkury.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/existing-account.png)

>[!BEGINSHADEBOX]

**Unterstützte Dateiformate**

Sie können die folgenden Dateiformate mit der Quelle [!DNL Merkury] erfassen:

* Trennzeichen-Werte (DSV): Jeder einzelne Wert kann als Trennzeichen für DSV-formatierte Datendateien verwendet werden.
* [!DNL JavaScript Object Notation] (JSON): JSON-formatierte Datendateien müssen XDM-konform sein.
* [!DNL Apache Parquet]: Parquet-formatierte Datendateien müssen XDM-konform sein.
* Komprimierte Dateien: JSON- und durch Trennzeichen getrennte Dateien können wie folgt komprimiert werden: `bzip2`, `gzip`, `deflate`, `zipDeflate`, `tarGzip` und `tar`.

>[!ENDSHADEBOX]

## Daten hinzufügen

Nachdem Sie Ihr [!DNL Merkury] -Konto erstellt haben, wird der Schritt **[!UICONTROL Daten hinzufügen]** angezeigt, der eine Oberfläche bereitstellt, über die Sie Ihre [!DNL Merkury]-Dateihierarchie durchsuchen und den Ordner bzw. die Datei auswählen können, den bzw. die Sie auf Experience Platform bringen möchten.

* Der linke Teil der Benutzeroberfläche ist ein Verzeichnisbrowser, der Ihre [!DNL Merkury] -Dateihierarchie anzeigt.
* Im rechten Bereich der Benutzeroberfläche können Sie eine Vorschau von bis zu 100 Zeilen mit Daten aus einem kompatiblen Ordner oder einer kompatiblen Datei anzeigen.

![Das Datei- und Ordnerverzeichnis des Ursprungs-Workflows, in dem Sie die zu erfassenden Daten auswählen können.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/add-data.png)

Wählen Sie den Stammordner aus, um auf Ihre Ordnerhierarchie zuzugreifen. Von hier aus können Sie einen einzelnen Ordner auswählen, um alle Dateien rekursiv in den Ordner aufzunehmen. Beim Erfassen eines ganzen Ordners müssen Sie sicherstellen, dass alle Dateien in diesem Ordner dasselbe Datenformat und Schema aufweisen.

Nachdem Sie einen Ordner ausgewählt haben, wird die richtige Oberfläche aktualisiert, um eine Vorschau des Inhalts und der Struktur der ersten Datei im ausgewählten Ordner anzuzeigen.

![Die für die Aufnahme und die Dateivorschau ausgewählten Daten.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/selected-data.png)


Während dieses Schritts können Sie mehrere Konfigurationen an Ihren Daten vornehmen, bevor Sie fortfahren. Wählen Sie zunächst **[!UICONTROL Datenformat]** und dann im angezeigten Dropdown-Bedienfeld das entsprechende Datenformat für Ihre Datei aus.

In der folgenden Tabelle werden die entsprechenden Datenformate für die unterstützten Dateitypen angezeigt:

| Dateityp | Datenformat |
| --- | --- |
| CSV | [!UICONTROL Getrennt] |
| JSON | [!UICONTROL JSON] |
| Parquet | [!UICONTROL XDM Parquet] |

### Spaltentrennzeichen auswählen

+++Auswählen , um Schritte zum Festlegen eines Trennzeichens anzuzeigen

Nach der Konfiguration Ihres Datenformats können Sie beim Erfassen von durch Trennzeichen getrennten Dateien ein Spaltentrennzeichen festlegen. Wählen Sie die Option **[!UICONTROL Trennzeichen]** und dann ein Trennzeichen aus dem Dropdown-Menü aus. Im Menü werden die am häufigsten verwendeten Optionen für Trennzeichen angezeigt, darunter ein Komma (`,`), eine Registerkarte (`\t`) und ein senkrechter Strich (`|`).

Wenn Sie lieber ein benutzerdefiniertes Trennzeichen verwenden möchten, wählen Sie &quot;**[!UICONTROL Benutzerdefiniert]**&quot;und geben Sie in die Popup-Eingabeleiste ein Trennzeichen mit einem einzelnen Zeichen Ihrer Wahl ein.

+++

### Komprimierte Dateien erfassen

+++ Wählen Sie diese Option, um die Schritte zum Erfassen komprimierter Dateien anzuzeigen.

Sie können auch komprimierte JSON- oder durch Trennzeichen getrennte Dateien erfassen, indem Sie deren Komprimierungstyp angeben.

Wählen Sie im Schritt [!UICONTROL Daten auswählen] eine komprimierte Datei für die Aufnahme aus und wählen Sie dann den entsprechenden Dateityp aus und ob er XDM-kompatibel ist oder nicht. Wählen Sie als Nächstes **[!UICONTROL Komprimierungstyp]** und dann den entsprechenden komprimierten Dateityp für die Quelldaten aus.

Um eine bestimmte Datei in Platform zu laden, wählen Sie einen Ordner aus und wählen Sie dann die Datei aus, die Sie aufnehmen möchten. Während dieses Schritts können Sie auch eine Vorschau des Dateiinhalts anderer Dateien in einem bestimmten Ordner anzeigen, indem Sie das Vorschausymbol neben einem Dateinamen verwenden.

Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

+++

## Angeben von Datenflussdetails

Auf der Seite [!UICONTROL Datenflussdetails] können Sie auswählen, ob Sie einen vorhandenen Datensatz oder einen neuen Datensatz verwenden möchten. Während dieses Vorgangs können Sie Ihre Daten auch so konfigurieren, dass sie in das Profil aufgenommen werden, und Einstellungen wie [!UICONTROL Fehlerdiagnose], [!UICONTROL Partielle Erfassung] und [!UICONTROL Warnhinweise] aktivieren.

### Verwenden eines vorhandenen Datensatzes

Um Daten in einen vorhandenen Datensatz aufzunehmen, wählen Sie **[!UICONTROL Vorhandener Datensatz]**. Sie können einen vorhandenen Datensatz entweder über die Option [!UICONTROL Erweiterte Suche] oder durch Scrollen durch die Liste der vorhandenen Datensätze im Dropdown-Menü abrufen. Nachdem Sie einen Datensatz ausgewählt haben, geben Sie einen Namen und eine Beschreibung für Ihren Datenfluss ein.

![ Die vorhandene Datensatzschnittstelle.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/existing-dataset.png)

### Verwenden eines neuen Datensatzes

Für ein Aufnehmen in einen neuen Datensatz wählen Sie **[!UICONTROL Neuer Datensatz]** aus und geben Sie einen Namen für den Ausgabedatensatz und eine optionale Beschreibung an. Wählen Sie als Nächstes mithilfe der Option [!UICONTROL Erweiterte Suche] oder durch Scrollen durch die Liste der vorhandenen Schemata im Dropdown-Menü ein Schema zum Zuordnen aus. Nachdem Sie ein Schema ausgewählt haben, geben Sie einen Namen und eine Beschreibung für Ihren Datenfluss ein.

![Die neue Datensatzschnittstelle.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/new-dataset.png)

### Profil- und Fehlerdiagnose aktivieren

++ + Auswählen, um Schritte zur Aktivierung der Fehlerdiagnose und Profilaufnahme anzuzeigen

Wählen Sie als Nächstes den Umschalter **[!UICONTROL Profildatensatz]** aus, um Ihren Datensatz für das Echtzeit-Kundenprofil zu aktivieren. Auf diese Weise können Sie eine ganzheitliche Ansicht der Attribute und Verhaltensweisen einer Entität erstellen. Daten aus allen profilaktivierten Datensätzen werden in das Profil aufgenommen und Änderungen werden angewendet, wenn Sie Ihren Datenfluss speichern.

[!UICONTROL Fehlerdiagnose] ermöglicht eine detaillierte Erstellung von Fehlermeldungen für alle fehlerhaften Datensätze, die in Ihrem Datenfluss auftreten, während [!UICONTROL Partielle Aufnahme] die Aufnahme von fehlerhaften Daten bis zu einem gewissen Schwellenwert, den Sie manuell definieren, ermöglicht. Weitere Informationen finden Sie in der [Übersicht zur partiellen Batch-Aufnahme](../../../../../ingestion/batch-ingestion/partial.md).

+++

### Aktivieren von Warnhinweisen

+++Auswählen, um Schritte zum Aktivieren von Warnhinweisen anzuzeigen

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status Ihres Datenflusses zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Warnhinweisen zu Quellen über die Benutzeroberfläche](../../alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihren Datenfluss fertig sind, klicken Sie auf **[!UICONTROL Weiter]**.

+++

## Zuordnen von Datenfeldern zu einem XDM-Schema

Es erfolgt der Schritt der [!UICONTROL Zuordnung], in dem Ihnen eine Schnittstelle zum Zuordnen der Quellfelder aus Ihrem Quellschema zu den entsprechenden XDM-Zielfeldern im Zielschema bereitgestellt wird.

Platform bietet intelligente Empfehlungen für automatisch zugeordnete Felder, die auf dem ausgewählten Zielschema oder Datensatz basieren. Sie können die Zuordnungsregeln manuell an Ihre Anwendungsfälle anpassen. Je nach Bedarf können Sie wahlweise Felder direkt zuordnen oder mithilfe von Datenvorbereitungsfunktionen Quelldaten transformieren, um berechnete oder anderweitig ermittelte Werte abzuleiten. Umfassende Schritte zur Verwendung der Zuordnungsoberfläche und der berechneten Felder finden Sie im Handbuch [Data Prep UI guide](../../../../../data-prep/ui/mapping.md).

Nachdem die Quelldaten erfolgreich zugeordnet wurden, wählen Sie **[!UICONTROL Weiter]** aus.

![ Die Zuordnungsschnittstelle.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/mapping.png)

## Erfassungsläufe planen

Der Schritt [!UICONTROL Planung] wird angezeigt, in dem Sie einen Aufnahmeplan konfigurieren können, um die ausgewählten Quelldaten mithilfe der konfigurierten Zuordnungen automatisch zu erfassen. Standardmäßig ist die Planung auf `Once` eingestellt. Um die Aufnahmefrequenz anzupassen, wählen Sie **[!UICONTROL Häufigkeit]** und dann eine Option aus dem Dropdown-Menü aus.

>[!TIP]
>
>Während einer einmaligen Erfassung sind Intervall und Aufstockung nicht sichtbar.

![Die Planungsschnittstelle](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/schedule.png)

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

## Überprüfen des Datenflusses

Der Schritt **[!UICONTROL Überprüfung]** wird angezeigt, sodass Sie Ihren neuen Datenfluss überprüfen können, bevor er hergestellt wird. Die Details lassen sich wie folgt kategorisieren:

* **[!UICONTROL Verbindung]**: Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quelldatei und die Anzahl der Spalten innerhalb dieser Quelldatei an.
* **[!UICONTROL Datensatz- und Zuordnungsfelder zuweisen]**: Zeigt an, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, dem der Datensatz entspricht.
* **[!UICONTROL Planung]**: Zeigt den aktiven Zeitraum, die Häufigkeit und das Intervall des Aufnahmezeitplans an.

Nachdem Sie Ihren Datenfluss überprüft haben, klicken Sie auf **[!UICONTROL Beenden]** und lassen Sie die Erstellung des Datenflusses etwas Zeit zu.

![ Die Überprüfungsseite.](../../../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/review.png)

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich einen Datenfluss erstellt, um Batch-Daten aus Ihrer [!DNL Merkury] -Quelle an Experience Platform zu übertragen. Weitere Ressourcen finden Sie in der unten beschriebenen Dokumentation.

### Überwachen Ihres Datenflusses

Nachdem Ihr Datenfluss erstellt wurde, können Sie die erfassten Daten überwachen, um Informationen zu Erfassungsraten, Erfolg und Fehlern anzuzeigen. Weitere Informationen zum Überwachen des Datenflusses finden Sie im Tutorial zum [Überwachen von Konten und Datenflüssen in der Benutzeroberfläche](../../monitor.md).

### Aktualisieren des Datenflusses

Um Konfigurationen für die Planung, Zuordnung und allgemeine Informationen Ihrer Datenflüsse zu aktualisieren, besuchen Sie das Tutorial zum Aktualisieren der Datenflüsse für Quellen in der Benutzeroberfläche ](../../update-dataflows.md) .[

### Löschen des Datenflusses

Datenflüsse, die nicht mehr erforderlich sind oder nicht korrekt erstellt wurden, können Sie löschen, indem Sie dazu die Funktion **[!UICONTROL Löschen]** im Arbeitsbereich **[!UICONTROL Datenflüsse]** verwenden. Weitere Informationen zum Löschen von Datenflüssen finden Sie im Tutorial zum Löschen von Datenflüssen in der Benutzeroberfläche ](../../delete.md).[
