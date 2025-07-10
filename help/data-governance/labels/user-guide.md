---
keywords: Experience Platform;Startseite;beliebte Themen;Data Governance;Datennutzungsbeschriftung;Policy Service;Benutzerhandbuch zu Datennutzungsbeschriftungen
solution: Experience Platform
title: Verwalten von Datennutzungs-Labels in der Benutzeroberfläche
description: Dieses Handbuch beschreibt die Schritte zum Arbeiten mit Datennutzungs-Labels in der Benutzeroberfläche von Adobe Experience Platform.
exl-id: aa44d5cc-416a-4ef2-be14-b4f32aec162c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1552'
ht-degree: 90%

---

# Verwalten von Datennutzungs-Labels in der Benutzeroberfläche {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataGovernance_description"
>title="Steuerung der Datennutzung in Experience Platform"
>abstract="<h2>Beschreibung</h2><p>Mit dem Data-Governance-Framework in Experience Platform können Sie Attribute und Schemata anhand von Datennutzungsbeschränkungen kennzeichnen und Richtlinien einrichten, die diese Einschränkungen für bestimmte Marketing-Aktionen identifizieren und berücksichtigen.</p>"

Dieses Benutzerhandbuch beschreibt die Schritte zum Arbeiten mit Datennutzungs-Labels in der Benutzeroberfläche von [!DNL Experience Platform].

## Verwalten von Labels {#manage-labels}

Um Labels auf Ihre Daten anzuwenden, benötigen Sie die Berechtigung **[!UICONTROL Nutzungs-Labels verwalten]** für die Verwendung in der standardmäßigen Produktions-Sandbox „prod“. Um ein benutzerdefinierts Label zu erstellen, müssen Sie ebenfalls über Administratorrechte für das Produktprofil verfügen. Jede Organisation verfügt nur über eine Liste von anwendbaren Kennzeichnungen. Kennzeichnungen **nicht** werden. Stattdessen können Sie sie aus den Datensätzen oder Feldern entfernen, auf die sie angewendet werden.

Weitere Informationen zum Zuweisen einer Berechtigung finden Sie im Handbuch zum [Konfigurieren von Berechtigungen](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html?lang=de) oder im Abschnitt [Zugriffssteuerung – Übersicht](../../access-control/home.md). Wenn Sie keinen Zugriff auf Admin Console für Ihr Unternehmen haben, wenden Sie sich an das Admin-Team Ihres Unternehmens.

## Verwalten von Labels auf Schemaebene

Sie können Labels direkt zu einem Schema oder zu Feldern innerhalb dieses Schemas hinzufügen. Alle Felder, die auf der Schemaebene angewendet werden, werden auf alle Datensätze übertragen, die auf diesem Schema basieren.

>[!NOTE]
>
>Wenn Ihre Datennutzungsrichtlinien erstellt wurden, bevor Sie Ihr Feld beschriftet haben, kann ein Dialogfeld für einen Verstoß gegen Governance-Richtlinien angezeigt werden, wenn Sie Kennzeichnungen auf Ihr neues Schema anwenden. Dieses Dialogfeld zeigt an, dass die Anwendung dieser Kennzeichnung gegen eine bestehende Nutzungsrichtlinie verstößt. Verwenden Sie das Datenherkunftsdiagramm, um zu verstehen, welche anderen Konfigurationsänderungen vorgenommen werden müssen, bevor Sie den Titel zu Ihrem Schemafeld hinzufügen können.
>
>![Das Dialogfeld „Verletzung der Data Governance-Richtlinie erkannt“ mit Hervorhebung der Zusammenfassung der Verletzung und des Diagramms der Datenherkunft.](../images/labels/policy-violation-dialog.png)
>
>Weitere [ zu Richtlinienverletzungen finden Sie in der Dokumentation ](../enforcement/auto-enforcement.md#data-usage-violation)Verletzung von Datennutzungsrichtlinien“.

Zum Verwalten der Datennutzungs-Labels auf Schemaebene müssen Sie ein vorhandenes Schema auswählen oder ein neues erstellen. Wählen Sie nach der Anmeldung bei Adobe Experience Platform im linken Navigationsbereich die Option **[!UICONTROL Schemata]** aus, um den Arbeitsbereich **[!UICONTROL Schemata]** zu öffnen. Auf dieser Seite werden alle erstellten Schemata, die zu Ihrem Unternehmen gehören, sowie nützliche Details zu jedem Schema angezeigt.

![Die Adobe Experience Platform-Benutzeroberfläche mit hervorgehobener Schema-Registerkarte.](../images/labels/schema-tab.png)

Im nächsten Abschnitt finden Sie Schritte zum Erstellen eines neuen Schemas, auf das Labels angewendet werden sollen. Wenn Sie Labels für ein vorhandenes Schema bearbeiten möchten, wählen Sie das Schema aus der Liste aus und fahren Sie mit dem Punkt [Hinzufügen von Datennutzungs-Labels zum Schema](#add-labels) fort.

### Erstellen eines neuen Schemas

Um ein neues Schema zu erstellen, wählen Sie oben rechts im Arbeitsbereich **[!UICONTROL Schemata]** die Option **[!UICONTROL Schema erstellen]** aus. Vollständige Anweisungen finden Sie im Handbuch zum [Erstellen eines Schemas mit dem Schema-Editor](../../xdm/tutorials/create-schema-ui.md#create). Sie können auch ein [Schema mithilfe der Schema Registry-API erstellen](../../xdm/tutorials/create-schema-api.md), falls erforderlich.

### Hinzufügen von Datennutzungs-Labels zu einem Schema {#add-labels-to-schema}

Wählen Sie nach Erstellen eines neuen Schemas oder Auswählen eines vorhandenen Schemas aus der Liste auf der Registerkarte [!UICONTROL Durchsuchen] des Arbeitsbereichs [!UICONTROL Schemata] ein Feld aus Ihrem Schema im Schema-Editor aus. Wählen Sie in der Seitenleiste [!UICONTROL Feldeigenschaften] die Option **[!UICONTROL Zugriffs- und Data-Governance-Labels anwenden]** aus.

![Die Registerkarte „Struktur“ des Arbeitsbereichs „Schemata“ mit Visualisierung Ihres Schemas bei hervorgehobener Option „Zugriffs- und Data-Governance-Labels anwenden“.](../images/labels/schema-label-governance.png)

Es wird ein Dialogfeld angezeigt, in dem Sie Datennutzungs-Labels auf Schema- und Feldebene anwenden und verwalten können. Im XDM-Tutorial finden Sie vollständige Anweisungen zum [Hinzufügen oder Bearbeiten von Datennutzungs-Labels für XDM-Schemata](../../xdm/tutorials/labels.md#select-schema-field).

### Hinzufügen von Datennutzungs-Labels zu einem bestimmten Datensatz {#add-labels-to-dataset}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataGovernance_instructions"
>title="Anweisungen"
>abstract="<ol><li>Wählen Sie im linken Navigationsbereich die Option <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/user-guide.html?lang=de">Datensätze</a> und dann den Datensatz aus, den Sie beschränken möchten.</li><li>Wählen Sie in der Ansicht „Datensatzdetails“ die Registerkarte <b>Data Governance</b> aus.</li><li>Wählen Sie die Datensatzfelder aus, die Sie beschränken möchten, und wählen Sie dann <b>Governance-Kennzeichnungen bearbeiten</b> aus, um die Daten anhand von Nutzungsbeschränkungen zu kennzeichnen.</li><li>Wählen Sie nach der Kennzeichnung Ihrer Daten im linken Navigationsbereich die Option <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html?lang=de">Richtlinien</a> und dann die Option <b>Richtlinie erstellen</b> aus.</li><li>Erstellen Sie eine <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/user-guide.html?lang=de#create-governance-policy">Data Governance-Richtlinie</a> und wählen Sie dann die Datennutzungskennzeichnungen aus, auf die die Richtlinie angewendet werden soll.</li><li>Wählen Sie die Marketing-Aktion(en) aus, die die Richtlinie für alle Daten mit diesen Labels verweigern soll. Nachdem die Richtlinie erstellt wurde, wählen Sie sie aus der Liste aus und aktivieren Sie sie mithilfe des Umschalters in der rechten Leiste.</li><li>Für jede aktivierte Richtlinie verhindert Experience Platform, dass Daten mit den angegebenen Labels für die definierte(n) Marketing-Aktion(en) verwendet werden. Diese Durchsetzung erfolgt automatisch, wenn Sie versuchen, gekennzeichnete Daten für ein Ziel mit zugehörigen Marketing-Aktionen zu aktivieren (Anwendungsfälle).</li></ol>"

>[!IMPORTANT]
>
>Labels können auf Datensatzebene nicht mehr auf Felder angewendet werden. Dieser Workflow wurde zugunsten von Labels auf Schemaebene aufgegeben. Alle Kennzeichnungen, die zuvor auf der Datensatzobjektebene angewendet wurden, werden bis zum 31. Mai 2024 weiterhin über die Experience Platform-Benutzeroberfläche unterstützt. Damit Ihre Labels schemaübergreifend konsistent sind, müssen alle Labels, die zuvor auf Felder auf Datensatzebene angewendet wurden, von Ihnen im Laufe des kommenden Jahres auf Schemaebene migriert werden. In der Dokumentation finden Sie Anweisungen zum [Migrieren von zuvor angewendeten Labels von der Datensatz- auf die Schemaebene](../e2e.md#migrate-labels).

Labels können über die Registerkarte **[!UICONTROL Data Governance]** des Arbeitsbereichs **[!UICONTROL Datensätze]** auf den kompletten Datensatz angewendet werden. Der Arbeitsbereich ermöglicht Ihnen das Verwalten von Datennutzungs-Labels auf Datensatzebene.

![Die Registerkarte[!UICONTROL Data Governance] des Arbeitsbereichs [!UICONTROL Datensätze] mit hervorgehobener Registerkarte „Data Governance“.](../images/labels/dataset-governance.png)

Um Datennutzungs-Labels auf Datensatzebene zu bearbeiten, wählen Sie zunächst das Stiftsymbol (![Stiftsymbol.](/help/images/icons/edit.png)) in der Zeile des Datensatznamens aus.

![Die Registerkarte [!UICONTROL Data Governance] des Arbeitsbereichs [!UICONTROL Datensätze] mit hervorgehobenem Stiftsymbol zum Bearbeiten.](../images/labels/dataset-level-edit.png)

Der Dialog **[!UICONTROL Governance-Beschriftungen bearbeiten]** wird geöffnet. Aktivieren Sie im Dialogfeld die Kontrollkästchen neben den Labels, die Sie auf den Datensatz anwenden möchten. Denken Sie daran, dass diese Labels von allen Feldern im Datensatz übernommen werden. Während Sie die einzelnen Kontrollkästchen auswählen, wird die Kopfzeile **[!UICONTROL Angewandte Labels]** aktualisiert, sodass sie die ausgewählten Labels anzeigt. Nachdem Sie die gewünschten Labels ausgewählt haben, wählen Sie **[!UICONTROL Änderungen speichern]**.

![Das Dialogfeld „Governance-Beschriftungen bearbeiten“ mit hervorgehobenen Kontrollkästchen für Kennzeichnungen und markierter Schaltfläche „Änderungen speichern“.](../images/labels/apply-labels-dataset.png)

Der Arbeitsbereich **[!UICONTROL Data Governance]** wird wieder angezeigt und zeigt die Kennzeichnungen an, die Sie auf Datensatzebene in der ersten Zeile der Tabelle angewendet haben. Es sind auch die durch einzelne Karten angezeigten Labels zu sehen, die von jedem Feld im Datensatz übernommen werden.

![Die Registerkarte [!UICONTROL Data Governance] des Arbeitsbereichs [!UICONTROL Datensätze] mit hervorgehobenen angewendeten Kennzeichnungen auf Datensatzebene und übernommenen Kennzeichnungen für Datensatzfelder.](../images/labels/applied-dataset-labels.png)

### Entfernen von Labels aus einem Datensatz {#remove-labels-from-a-dataset}

Auf Datensatzebene hinzugefügte Labels weisen neben ihrer Karte ein „x“ auf. Dadurch können Sie die Labels aus dem kompletten Datensatz entfernen. Bei übernommenen Labels wird nicht neben jedem Feld ein „x“ angezeigt. Sie werden abgeblendet, also ausgegraut dargestellt. Diese **übernommenen Labels sind schreibgeschützt**, d. h., sie können nicht auf Feldebene entfernt oder bearbeitet werden.

<!-- ## View labels at the dataset field level {#view-labels-at-dataset-field-level} -->

<!-- To view labels inherited by the dataset from the schema level, select **[!UICONTROL Datasets]** to navigate to the datasets workspace and select the relevant dataset from the list. 

![The Browse tab of the Datasets workspace with Datasets highlighted in the left sidebar.](../images/labels/dataset-navigation.png)

Next, select the **[!UICONTROL Data Governance]** tab to show the labels that have been applied to the dataset. You can also see that the labels are inherited down to each of the fields within the dataset.

![Dataset Labels inherited by fields](../images/labels/dataset-labels-applied.png)

The inherited labels beside each field do not have an "x" next to them and appear "greyed out" with no ability to remove or edit. This is because **inherited fields are read-only**, meaning they cannot be removed at the field level. -->

<!--Beleive can cut above here  -->

Der Umschalter **[!UICONTROL Übernommene Kennzeichnung anzeigen]** ist standardmäßig aktiviert. Dadurch können Sie alle Labels sehen, die die zugehörigen Felder vom Schema übernommen haben. Wenn Sie den Umschalter deaktivieren, werden alle übernommenen Labels im Datensatz ausgeblendet.

![Die Registerkarte „Data Governance“ des Arbeitsbereichs „Datensätze“ mit hervorgehobenem Umschalter „Übernommene Kennzeichnung anzeigen“.](../images/labels/inherited-labels.png)

<!-- Labels applied to the dataset appear in read-only form within the **[!UICONTROL Data Governance]** view for that dataset. 

![The Data Governance tab of the Datasets workspace with labels highlighted.](../images/labels/read-only-governance-labels.png) -->

>[!NOTE]
>
>Labels, die angewendet wurden, bevor die Funktion zur Kennzeichnung von Datensätzen eingestellt wurde, können aus dem Datensatz entfernt werden, indem Sie den relevanten Datensatz suchen und das Symbol „Abbrechen“ auf der Kennzeichnung auswählen.
>>![Die Registerkarte „Data Governance“ im Arbeitsbereich „Datensätze“ mit hervorgehobener löschbarer Kennzeichnung.](../images/labels/remove-governance-labels.png)
>>In der Dokumentation finden Sie Anweisungen zum [Migrieren von zuvor angewendeten Labels von der Datensatz- auf die Schemaebene](../e2e.md#migrate-labels).

## Verwalten von benutzerdefinierten Labels {#manage-custom-labels}

>[!CONTEXTUALHELP]
>id="platform_governance_createlabels"
>title="Erstellen von Labels"
>abstract="Mit Labels können Sie Datensätze und Felder entsprechend den für diese Daten geltenden Nutzungsrichtlinien kategorisieren. Experience Platform bietet einen Standardsatz von Labels, die Sie verwenden können. Sie können aber auch benutzerdefinierte Labels erstellen, die für Ihr Unternehmen spezifisch sind."

Sie können Ihre eigenen benutzerspezifischen Nutzungs-Labels im Arbeitsbereich **[!UICONTROL Richtlinien]** in der Benutzeroberfläche von [!DNL Experience Platform] erstellen. Wählen Sie **[!UICONTROL Richtlinien]** in der linken Navigation und anschließend **[!UICONTROL Labels]**, um eine Liste der vorhandenen Labels zu sehen. Wählen Sie dort **[!UICONTROL Label erstellen]**.

![Der Arbeitsbereich „Richtlinien“ mit hervorgehobener Option „Kennzeichnung erstellen“.](../images/labels/create-label-btn.png)

Das Dialogfeld **[!UICONTROL Label erstellen]** wird angezeigt. Geben Sie nun die folgenden Informationen für das neue Label ein:

* **[!UICONTROL Name]**: Eine eindeutige Kennung für das Label. Dieser Wert wird für Suchen verwendet und sollte daher kurz und knapp sein.
* **[!UICONTROL Benutzerfreundlicher Name]**: Ein benutzerfreundlicher Anzeigename für das Label.
* **[!UICONTROL Beschreibung]**: (Optional) Eine Beschreibung für das Label, um mehr Kontext bereitzustellen.

Klicken Sie abschließend auf **[!UICONTROL Erstellen]**.

![Das Dialogfeld „Label erstellen“ des Arbeitsbereichs „Richtlinien“ mit hervorgehobener Schaltfläche „Erstellen“.](../images/labels/create-label-dialog.png)

Das Dialogfeld wird geschlossen und die neu erstellte benutzerdefinierte Kennzeichnung wird in der Liste unter der Registerkarte **[!UICONTROL Labels]** angezeigt.

![Die Registerkarte „Labels“ des Arbeitsbereichs „Richtlinien“ mit der hervorgehobenen neuen benutzerdefinierten Kennzeichnung.](../images/labels/label-created.png)

Die Kennzeichnung kann jetzt unter **[!UICONTROL Benutzerdefinierte Labels]** ausgewählt werden, wenn Labels für Datensätze und Felder bearbeitet oder Datennutzungsrichtlinien erstellt werden.

![Das Dialogfeld „Zugriffs- und Data-Governance-Labels anwenden“ mit hervorgehobenen benutzerdefinierten Kennzeichnungen.](../images/labels/add-custom-label.png)

## Nächste Schritte

Nachdem Sie Datennutzungs-Labels auf Datensatz- und Feldebene hinzugefügt haben, können Sie damit beginnen, Daten in [!DNL Experience Platform] zu erfassen. Weitere Informationen erhalten Sie in der [Dokumentation zur Datenaufnahme](../../ingestion/home.md).

Sie können jetzt auch Datennutzungsrichtlinien auf Basis der von Ihnen angewendeten Labels definieren. Weitere Informationen finden Sie unter [Datennutzungsrichtlinien – Übersicht](../policies/overview.md).

<!-- The workflow of this video is now outdated. This can be enabled once the video has been updated

## Additional resources

The following video is intended to support your understanding of Data Governance, and outlines how to apply labels to a dataset and individual fields.

>[!VIDEO](https://video.tv.adobe.com/v/29709?quality=12&enable10seconds=on&speedcontrol=on) -->
