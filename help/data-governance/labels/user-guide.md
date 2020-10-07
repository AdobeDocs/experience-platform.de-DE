---
keywords: Experience Platform;home;popular topics;data governance;data usage label;policy service;data usage labels user guide
solution: Experience Platform
title: Benutzerhandbuch zu den Datennutzungsbezeichnungen
topic: labels
description: In diesem Benutzerhandbuch werden die Schritte zum Arbeiten mit Datenverwendungsbeschriftungen in der Adobe Experience Platform-Benutzeroberfläche beschrieben.
translation-type: tm+mt
source-git-commit: 259c26a9d3b6ef397acd552e255f68ecb25b2dd1
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 1%

---


# Benutzerhandbuch zu den Datennutzungsbezeichnungen

Dieses Benutzerhandbuch beschreibt die Schritte zum Arbeiten mit Beschriftungen für die Datenverwendung in der [!DNL Experience Platform] Benutzeroberfläche. Bevor Sie das Handbuch verwenden, lesen Sie bitte die [[!DNL Data Governance] Übersicht](../home.md) für eine stabilere Einführung in das [!DNL Data Governance] Framework.

## Verwalten von Datenverwendungsbeschriftungen auf der Datensatzebene

Zur Verwaltung der Datenverwendungsbeschriftungen auf Datensatzebene müssen Sie einen vorhandenen Datensatz auswählen oder einen neuen erstellen. Wählen Sie nach der Anmeldung bei Adobe Experience Platform im linken Navigationsbereich die Option **[!UICONTROL Datasets]** , um den Arbeitsbereich &quot; **[!UICONTROL Datasets]** &quot;zu öffnen. Auf dieser Seite werden alle erstellten Datensätze, die zu Ihrem Unternehmen gehören, sowie nützliche Details zu jedem Datensatz Liste.

![Registerkarte &quot;Datenbestand&quot;im Datenbereich](../images/labels/datasets.png)

Im nächsten Abschnitt finden Sie Schritte zum Erstellen eines neuen Datensatzes, auf den Beschriftungen angewendet werden sollen. Wenn Sie die Beschriftungen eines vorhandenen Datensatzes bearbeiten möchten, wählen Sie den Datensatz aus der Liste und überspringen Sie mit dem [Hinzufügen von Beschriftungen für die Datenverwendung zum Datensatz](#add-labels).

### Neuen Datensatz erstellen

>[!NOTE]
>
>In diesem Beispiel wird ein Datensatz mit einem vorkonfigurierten [!DNL Experience Data Model] (XDM-)Schema erstellt. Weitere Informationen zu XDM-Schemas finden Sie in der [XDM-Systemübersicht](../../xdm/home.md) und den [Grundlagen der Schema-Komposition](../../xdm/schema/composition.md).

To create a new dataset, click **[!UICONTROL Create Dataset]** in the top-right corner of the **[!UICONTROL Datasets]** workspace.

![](../images/labels/create_dataset.png)

Der Bildschirm &quot; **[!UICONTROL Datensatz]** erstellen&quot;wird angezeigt. Klicken Sie von hier auf Dataset aus Schema **[!UICONTROL erstellen]**.

![Datensatz aus Schema erstellen](../images/labels/dataset_create.png)

Der Bildschirm &quot;Schema **** auswählen&quot;wird angezeigt, in dem alle verfügbaren Schema Liste werden, die Sie zum Erstellen eines Datensatzes verwenden können. Klicken Sie auf das Optionsfeld neben einem Schema, um es auszuwählen. Im Bereich &quot; **[!UICONTROL Schema]** &quot;auf der rechten Seite werden weitere Details zum ausgewählten Schema angezeigt. Once you have selected a schema, click **[!UICONTROL Next]**.

![Datenbestand-Schema auswählen](../images/labels/dataset_schema.png)

The **[!UICONTROL Configure Dataset]** screen appears. Geben Sie einen Namen (erforderlich) und eine Beschreibung (optional, jedoch empfohlen) für Ihren neuen Datensatz ein und klicken Sie dann auf **[!UICONTROL Fertig stellen]**.

![Datensatz mit Namen und Beschreibung konfigurieren](../images/labels/dataset_configure.png)

Die Aktivität **[!UICONTROL des]** Datensatzes wird mit Informationen zum neu erstellten Datensatz angezeigt. In diesem Beispiel heißt der Datensatz &quot;Treuemitglieder&quot;, daher zeigt die oberste Navigation **Datasets > Treuemitglieder**.

![Aktivität des Datensatzes](../images/labels/dataset_activity.png)

### hinzufügen der Datenverwendungsbeschriftungen mit dem Datensatz {#add-labels}

Nachdem Sie einen neuen Datensatz erstellt oder einen vorhandenen Datensatz aus der Liste im Arbeitsbereich &quot; **[!UICONTROL Datensätze]** &quot;ausgewählt haben, klicken Sie auf **[!UICONTROL Datenverwaltung]** , um den Arbeitsbereich &quot; **[!UICONTROL Datenverwaltung]** &quot;zu öffnen. Der Arbeitsbereich ermöglicht Ihnen die Verwaltung von Beschriftungen für die Datenverwendung auf Datensatzebene und Feldebene.

![Registerkarte &quot;Datenverwaltung&quot;](../images/labels/dataset_data_governance.png)

Um die Beschriftungen für die Datenverwendung auf Datensatzebene zu bearbeiten, klicken Sie auf das Stiftsymbol neben dem Dataset-Namen.

![Bezeichnungen auf Datensatzebene bearbeiten](../images/labels/dataset_labels_edit_button.png)

Das Dialogfeld &quot; **[!UICONTROL Governance-Bezeichnungen]** bearbeiten&quot;wird geöffnet. Aktivieren Sie im Dialogfeld die Kontrollkästchen neben den Beschriftungen, die Sie auf den Datensatz anwenden möchten. Denken Sie daran, dass diese Beschriftungen von allen Feldern im Datensatz übernommen werden. Die Kopfzeile &quot; **[!UICONTROL Angewandte Bezeichnungen]** &quot;wird aktualisiert, wenn Sie die einzelnen Felder markieren und die ausgewählten Bezeichnungen anzeigen. Nachdem Sie die gewünschten Beschriftungen ausgewählt haben, klicken Sie auf Änderungen **[!UICONTROL speichern]**.

<img alt="Governance-Bezeichnungen auf Datenaset-Ebene anwenden" src="../images/labels/apply-labels-dataset.png" width="700"><br>

Der Arbeitsbereich **[!UICONTROL Datenverwaltung]** wird wieder angezeigt und zeigt die Beschriftungen an, die Sie auf Datensatzebene angewendet haben. Sie können auch sehen, dass die Beschriftungen bis zu den einzelnen Feldern im Datensatz geerbt werden.

![Von Feldern geerbte Datenbezeichnungen](../images/labels/dataset_inherited_labels.png)

Beachten Sie, dass neben den Beschriftungen auf Datensatzebene ein &quot;x&quot;angezeigt wird, sodass Sie die Beschriftungen entfernen können. Die geerbten Beschriftungen neben jedem Feld haben kein &quot;x&quot; neben ihnen und erscheinen als &quot;grau ausgegraut&quot;, ohne dass sie entfernt oder bearbeitet werden können. Dies liegt daran, dass **geerbte Felder schreibgeschützt** sind, d. h. sie können nicht auf Feldebene entfernt werden.

Der Umschalter &quot; **[!UICONTROL Vererbte Bezeichnungen]** anzeigen&quot;ist standardmäßig aktiviert, sodass Sie alle Bezeichnungen sehen können, die vom Datensatz bis zu seinen Feldern vererbt wurden. Wenn Sie den Umschalter deaktivieren, werden alle geerbten Beschriftungen im Datensatz ausgeblendet.

![Vererbte Beschriftungen ausblenden](../images/labels/hide_inherited_labels.png)

## Verwalten von Datenverwendungsbeschriftungen auf der Ebene des Datensatzfelds

Wenn Sie den Arbeitsablauf für das [Hinzufügen und Bearbeiten von Datenverwendungsbeschriftungen auf Datensatzebene](#add-labels)fortsetzen, können Sie auch Beschriftungen auf Feldebene im Arbeitsbereich **[!UICONTROL Datenverwaltung]** für diesen Datensatz verwalten.

Um die Beschriftungen für die Datenverwendung auf ein einzelnes Feld anzuwenden, aktivieren Sie das Kontrollkästchen neben dem Feldnamen und klicken Sie dann auf Governance-Beschriftungen **[!UICONTROL bearbeiten]**.

![Feldbezeichnungen bearbeiten](../images/labels/fields_single_field.png)

Das Dialogfeld &quot;Governance-Bezeichnungen **[!UICONTROL bearbeiten&quot;]** wird angezeigt. Im Dialogfeld werden Kopfzeilen mit ausgewählten Feldern, angewendeten Beschriftungen und geerbten Beschriftungen angezeigt. Beachten Sie, dass die geerbten Beschriftungen (C2 und C5) im Dialogfeld grau dargestellt werden. Es handelt sich um schreibgeschützte Bezeichnungen, die von der Datensatzebene übernommen werden und daher nur auf Datensatzebene bearbeitet werden können.

<img alt="Bearbeiten von Governance-Beschriftungen für ein einzelnes Feld" src="../images/labels/field-label-inheritance.png" width="700"><br>

Wählen Sie Beschriftungen auf Feldebene aus, indem Sie auf das Kontrollkästchen neben der jeweiligen Bezeichnung klicken, die Sie verwenden möchten. Während Sie Beschriftungen auswählen, wird die Kopfzeile &quot; **[!UICONTROL Angewandte Bezeichnungen]** &quot;aktualisiert und zeigt Beschriftungen an, die auf die Felder angewendet wurden, die in der Kopfzeile &quot; **[!UICONTROL Ausgewählte Felder]** &quot;angezeigt werden. Nachdem Sie die Feldbezeichnungen ausgewählt haben, klicken Sie auf Änderungen **[!UICONTROL speichern]**.

<img alt="Anwenden von Beschriftungen auf Feldebene" src="../images/labels/apply-labels-field.png" width="700"><br>

Der **[!UICONTROL Arbeitsbereich &quot;Datenverwaltung]** &quot;wird wieder angezeigt, in dem nun die ausgewählten Beschriftungen auf Feldebene in der Zeile neben dem Feldnamen angezeigt werden. Beachten Sie, dass neben der Beschriftung auf Feldebene ein &quot;x&quot;steht, sodass Sie die Beschriftung entfernen können.

![Feld mit Beschriftungen auf Feldebene](../images/labels/fields_show_field_level_labels.png)

Sie können diese Schritte wiederholen, um weiterhin Beschriftungen auf Feldebene für zusätzliche Felder hinzuzufügen und zu bearbeiten, einschließlich der Auswahl mehrerer Felder, um Beschriftungen auf Feldebene gleichzeitig anzuwenden.

![Wählen Sie mehrere Felder aus, um Beschriftungen auf Feldebene gleichzeitig anzuwenden.](../images/labels/fields_select_multiple.png)

Es ist wichtig, sich zu merken, dass die Vererbung nur von der obersten Ebene nach unten verschoben wird (Dataset → Felder), d. h. dass auf Feldebene angewendete Beschriftungen nicht in andere Felder oder Datensätze übertragen werden.

## Verwalten benutzerdefinierter Beschriftungen

Sie können Ihre eigenen benutzerdefinierten Nutzungsbezeichnungen im Arbeitsbereich &quot; **[!UICONTROL Richtlinien]** &quot;in der [!DNL Experience Platform] Benutzeroberfläche erstellen. Klicken Sie im linken Navigationsbereich auf **[!UICONTROL Richtlinien]** und dann auf **[!UICONTROL Bezeichnungen]** , um eine Liste der vorhandenen Bezeichnungen Ansicht. Klicken Sie von hier auf Bezeichnung **[!UICONTROL erstellen]**.

![](../images/labels/create-label-btn.png)

Das Dialogfeld &quot;Beschriftung **[!UICONTROL erstellen]** &quot;wird angezeigt. Geben Sie von hier aus die folgenden Informationen für die neue Beschriftung ein:

* **[!UICONTROL Bezeichner]**: Eine eindeutige Kennung für die Bezeichnung. Dieser Wert wird für Nachschlagezwecke verwendet und sollte daher kurz und knapp sein.
* **[!UICONTROL Name]**: Ein Anzeigename für die Beschriftung.
* **[!UICONTROL Beschreibung]**: (Optional) Eine Beschreibung für die Bezeichnung, um weiteren Kontext bereitzustellen.

Klicken Sie abschließend auf **[!UICONTROL Erstellen]**.

![](../images/labels/create-label.png)

Das Dialogfeld wird geschlossen und die neu erstellte benutzerdefinierte Bezeichnung wird in der Liste auf der Registerkarte &quot; **[!UICONTROL Bezeichnungen]** &quot;angezeigt.

![](../images/labels/label-created.png)

Die Beschriftung kann jetzt unter &quot; **[!UICONTROL Benutzerdefinierte Beschriftungen]** &quot;ausgewählt werden, wenn die Beschriftungen für Datensätze und Felder bearbeitet oder Datenverwendungsrichtlinien erstellt werden.

<img src="../images/labels/add-custom-label.png" width="600" /><br>

## Nächste Schritte

Nachdem Sie nun Bezeichnungen zur Datenverwendung auf der Ebene des Datensatzes und der Felder hinzugefügt haben, können Sie beginnen, Daten zu erfassen [!DNL Experience Platform]. Weitere Informationen erhalten Sie im Beginn in der [Datenerhebungsdokumentation](../../ingestion/home.md).

Sie können jetzt auch Datenverwendungsrichtlinien auf Basis der von Ihnen angewendeten Beschriftungen definieren. Weitere Informationen finden Sie in der Übersicht über die [Datenverwendungsrichtlinien](../policies/overview.md).

## Zusätzliche Ressourcen

Das folgende Video soll Ihnen dabei helfen, Beschreibungen zu verstehen [!DNL Data Governance]und beschreibt, wie Sie Beschriftungen auf einen Datensatz und einzelne Felder anwenden.

>[!VIDEO](https://video.tv.adobe.com/v/29709?quality=12&enable10seconds=on&speedcontrol=on)
