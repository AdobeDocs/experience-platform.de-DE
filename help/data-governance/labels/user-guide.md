---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Benutzerhandbuch zur Datenverwendung
topic: labels
translation-type: tm+mt
source-git-commit: 475e774d5e7ebac036b42aa94736ba8e22c7185f

---


# Benutzerhandbuch zur Datenverwendung

Dieses Benutzerhandbuch beschreibt die Schritte zum Arbeiten mit Datenverwendungsbeschriftungen (auch als DULE-Beschriftungen bezeichnet) in der Benutzeroberfläche von Experience Platform. Bevor Sie den Leitfaden verwenden, lesen Sie bitte die Übersicht über die [Datenverwaltung](../home.md) , um eine solidere Einführung in das DUL-Framework zu erhalten.

## Verwalten von Datenverwendungsbeschriftungen auf der Datensatzebene

Zur Verwaltung der Datenverwendungsbeschriftungen auf Datensatzebene müssen Sie einen vorhandenen Datensatz auswählen oder einen neuen erstellen. Nach der Anmeldung bei Adobe Experience Platform wählen Sie **[!UICONTROL Datasets]** im linken Navigationsbereich die Option, um den Arbeitsbereich &quot; _Datasets_ &quot;zu öffnen. Auf dieser Seite werden alle erstellten Datensätze, die zu Ihrem Unternehmen gehören, sowie nützliche Details zu jedem Datensatz Liste.

![Registerkarte &quot;Datenbestand&quot;im Datenbereich](../images/labels/datasets.png)

Im nächsten Abschnitt finden Sie Schritte zum Erstellen eines neuen Datensatzes, auf den Beschriftungen angewendet werden sollen. Wenn Sie die Beschriftungen eines vorhandenen Datensatzes bearbeiten möchten, wählen Sie den Datensatz aus der Liste und überspringen Sie mit dem [Hinzufügen von Beschriftungen für die Datenverwendung zum Datensatz](#add-labels).

### Erstellen eines neuen Datensatzes

>[!NOTE] In diesem Beispiel wird ein Datensatz mit einem vorkonfigurierten XDM-Schema (Experience Data Model) erstellt. Weitere Informationen zu XDM-Schemas finden Sie in der [XDM-Systemübersicht](../../xdm/home.md) und den [Grundlagen der Schema-Komposition](../../xdm/schema/composition.md).

Um einen neuen Datensatz zu erstellen, klicken Sie **[!UICONTROL Create Dataset]** in der oberen rechten Ecke des _[!UICONTROL Datasets]_Arbeitsbereichs.

![](../images/labels/create_dataset.png)

Der _[!UICONTROL Create Dataset]_Bildschirm wird angezeigt. Klicken Sie von hier auf **[!UICONTROL Create Dataset from Schema]**.

![Datensatz aus Schema erstellen](../images/labels/dataset_create.png)

Der _[!UICONTROL Select Schema]_Bildschirm zeigt alle verfügbaren Schema an, die Sie zum Erstellen eines Datensatzes verwenden können. Klicken Sie auf das Optionsfeld neben einem Schema, um es auszuwählen. Im_[!UICONTROL Schemas]_ Bereich auf der rechten Seite werden weitere Details zum ausgewählten Schema angezeigt. Nachdem Sie ein Schema ausgewählt haben, klicken Sie auf **[!UICONTROL Next]**.

![Datenbestand-Schema auswählen](../images/labels/dataset_schema.png)

Der Bildschirm &quot;Datensatz _konfigurieren&quot;_ wird angezeigt. Geben Sie einen **Namen** (erforderlich) und eine **Beschreibung** (optional, aber empfohlen) für den neuen Datensatz ein und klicken Sie dann auf **[!UICONTROL Finish]**.

![Datensatz mit Namen und Beschreibung konfigurieren](../images/labels/dataset_configure.png)

Die _[!UICONTROL Dataset Activity]_Seite wird mit Informationen zum neu erstellten Datensatz angezeigt. In diesem Beispiel heißt der Datensatz &quot;Treuemitglieder&quot;, daher zeigt die oberste Navigation_ Datasets > Treuemitglieder _.

![Aktivität des Datensatzes](../images/labels/dataset_activity.png)

### Hinzufügen der Datenverwendungsbeschriftungen mit dem Datensatz {#add-labels}

Nachdem Sie einen neuen Datensatz erstellt oder einen vorhandenen Datensatz aus der Liste im _[!UICONTROL Datasets]_Arbeitsbereich ausgewählt haben, klicken Sie auf **[!UICONTROL Data Governance]**, um den_[!UICONTROL Data Governance]_ Arbeitsbereich zu öffnen. Der Arbeitsbereich ermöglicht Ihnen die Verwaltung von Beschriftungen für die Datenverwendung auf Datensatzebene und Feldebene.

![Registerkarte &quot;Datenverwaltung&quot;](../images/labels/dataset_data_governance.png)

Um die Beschriftungen für die Datenverwendung auf Datensatzebene zu bearbeiten, klicken Sie auf das Stiftsymbol neben dem Dataset-Namen.

![Bezeichnungen auf Datensatzebene bearbeiten](../images/labels/dataset_labels_edit_button.png)

Das _[!UICONTROL Edit Governance Labels]_Dialogfeld wird geöffnet. Aktivieren Sie im Dialogfeld die Kontrollkästchen neben den Beschriftungen, die Sie auf den Datensatz anwenden möchten. Denken Sie daran, dass diese Beschriftungen von allen Feldern im Datensatz übernommen werden. Die_[!UICONTROL Applied Labels]_ Kopfzeile wird aktualisiert, wenn Sie die einzelnen Felder markieren und die ausgewählten Beschriftungen anzeigen. Klicken Sie nach Auswahl der gewünschten Beschriftungen auf **[!UICONTROL Save Changes]**.

<img alt="Governance-Bezeichnungen auf Datenaset-Ebene anwenden" src="../images/labels/apply-labels-dataset.png" width="700"><br>

Der _[!UICONTROL Data Governance]_Arbeitsbereich wird wieder angezeigt und zeigt die Beschriftungen an, die Sie auf Datensatzebene angewendet haben. Sie können auch sehen, dass die Beschriftungen bis zu den einzelnen Feldern im Datensatz geerbt werden.

![Von Feldern geerbte Datenbezeichnungen](../images/labels/dataset_inherited_labels.png)

Beachten Sie, dass neben den Beschriftungen auf Datensatzebene ein &quot;x&quot;angezeigt wird, sodass Sie die Beschriftungen entfernen können. Die geerbten Beschriftungen neben jedem Feld haben kein &quot;x&quot; neben ihnen und erscheinen als &quot;grau ausgegraut&quot;, ohne dass sie entfernt oder bearbeitet werden können. Dies liegt daran, dass **geerbte Felder schreibgeschützt** sind, d. h. sie können nicht auf Feldebene entfernt werden.

Der **[!UICONTROL Show Inherited Labels]** Umschalter ist standardmäßig aktiviert, sodass Sie alle vom Datensatz bis zu seinen Feldern geerbten Bezeichnungen sehen können. Wenn Sie den Umschalter deaktivieren, werden alle geerbten Beschriftungen im Datensatz ausgeblendet.

![Vererbte Beschriftungen ausblenden](../images/labels/hide_inherited_labels.png)

## Verwalten von Datenverwendungsbeschriftungen auf der Ebene des Datensatzfelds

Wenn Sie den Arbeitsablauf für das [Hinzufügen und Bearbeiten von Beschriftungen für die Datenverwendung auf Datensatzebene](#add-labels)fortsetzen, können Sie auch Beschriftungen auf Feldebene innerhalb des Arbeitsbereichs für diesen Datensatz verwalten _[!UICONTROL Data Governance]_.

Um die Beschriftungen für die Datenverwendung auf ein einzelnes Feld anzuwenden, aktivieren Sie das Kontrollkästchen neben dem Feldnamen und klicken Sie dann auf **[!UICONTROL Edit Governance Labels]**.

![Feldbezeichnungen bearbeiten](../images/labels/fields_single_field.png)

Das _[!UICONTROL Edit Governance Labels]_Dialogfeld wird angezeigt. Im Dialogfeld werden Kopfzeilen mit ausgewählten Feldern, angewendeten Beschriftungen und geerbten Beschriftungen angezeigt. Beachten Sie, dass die geerbten Beschriftungen (C2 und C5) im Dialogfeld grau dargestellt werden. Es handelt sich um schreibgeschützte Bezeichnungen, die von der Datensatzebene übernommen werden und daher nur auf Datensatzebene bearbeitet werden können.

<img alt="Bearbeiten von Governance-Beschriftungen für ein einzelnes Feld" src="../images/labels/field-label-inheritance.png" width="700"><br>

Wählen Sie Beschriftungen auf Feldebene aus, indem Sie auf das Kontrollkästchen neben der jeweiligen Bezeichnung klicken, die Sie verwenden möchten. Während Sie Beschriftungen auswählen, wird die _[!UICONTROL Applied Labels]_Kopfzeile aktualisiert und zeigt Beschriftungen an, die auf die in der_[!UICONTROL Selected Fields]_ Kopfzeile angezeigten Felder angewendet werden. Nachdem Sie die Feldbezeichnungen ausgewählt haben, klicken Sie auf **[!UICONTROL Save Changes]**.

<img alt="Anwenden von Beschriftungen auf Feldebene" src="../images/labels/apply-labels-field.png" width="700"><br>

Der _[!UICONTROL Data Governance]_Arbeitsbereich wird wieder angezeigt. Die ausgewählten Beschriftungen auf Feldebene werden nun in der Zeile neben dem Feldnamen angezeigt. Beachten Sie, dass neben der Beschriftung auf Feldebene ein &quot;x&quot;steht, sodass Sie die Beschriftung entfernen können.

![Feld mit Beschriftungen auf Feldebene](../images/labels/fields_show_field_level_labels.png)

Sie können diese Schritte wiederholen, um weiterhin Beschriftungen auf Feldebene für zusätzliche Felder hinzuzufügen und zu bearbeiten, einschließlich der Auswahl mehrerer Felder, um Beschriftungen auf Feldebene gleichzeitig anzuwenden.

![Wählen Sie mehrere Felder aus, um Beschriftungen auf Feldebene gleichzeitig anzuwenden.](../images/labels/fields_select_multiple.png)

Es ist wichtig, sich zu merken, dass die Vererbung nur von der obersten Ebene nach unten verschoben wird (Dataset → Felder), d. h. dass auf Feldebene angewendete Beschriftungen nicht in andere Felder oder Datensätze übertragen werden.

## Nächste Schritte

Nachdem Sie nun Datenverwendungsbeschriftungen auf der Dataset- und Feldebene hinzugefügt haben, können Sie beginnen, Daten in Experience Platform zu erfassen. Weitere Informationen erhalten Sie im Beginn in der [Datenerhebungsdokumentation](../../ingestion/home.md).

Sie können jetzt auch Datenverwendungsrichtlinien auf Basis der von Ihnen angewendeten Beschriftungen definieren. Weitere Informationen finden Sie in der Übersicht über die [Datenverwendungsrichtlinien](../policies/overview.md).

## Zusätzliche Ressourcen

Das folgende Video soll Ihr Verständnis von Data Governance unterstützen und beschreibt, wie Sie Beschriftungen auf einen Datensatz und einzelne Felder anwenden.

>[!VIDEO](https://video.tv.adobe.com/v/29709?quality=12&enable10seconds=on&speedcontrol=on)
