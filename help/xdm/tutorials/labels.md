---
title: Verwalten von Datennutzungsbeschriftungen für ein Schema
description: Erfahren Sie, wie Sie in der Adobe Experience Platform-Benutzeroberfläche Datennutzungsbeschriftungen zu Schemafeldern des Experience-Datenmodells (XDM) hinzufügen.
exl-id: 92284bf7-f034-46cc-b905-bdfb9fcd608a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 11%

---

# Verwalten von Datennutzungs-Labels für ein Schema

Alle Daten, die in Adobe Experience Platform importiert werden, sind durch Experience-Datenmodell(XDM)-Schemata eingeschränkt. Diese Daten können Nutzungsbeschränkungen unterliegen, die von Ihrem Unternehmen oder durch gesetzliche Bestimmungen festgelegt werden. Aus diesem Grund ermöglicht Ihnen Experience Platform, die Verwendung bestimmter Datensätze und Felder durch die Verwendung von [Datennutzungskennzeichnungen“ ](../../data-governance/labels/overview.md) beschränken.

Eine Kennzeichnung, die auf ein Schemafeld angewendet wird, gibt die Nutzungsrichtlinien an, die für die in diesem bestimmten Feld enthaltenen Daten gelten.

Kennzeichnungen können auf einzelne Schemata und Felder innerhalb dieser Schemata angewendet werden. Wenn Kennzeichnungen direkt auf ein Schema angewendet werden, werden diese Kennzeichnungen auf alle vorhandenen und zukünftigen Datensätze übertragen, die auf diesem Schema basieren.

Darüber hinaus wird jede Feldbezeichnung, die Sie in einem Schema hinzufügen, an alle anderen Schemata übertragen, die dasselbe Feld aus einer freigegebenen Klasse oder Feldergruppe verwenden. Dadurch wird sichergestellt, dass die Nutzungsregeln für ähnliche Felder in Ihrem gesamten Datenmodell konsistent sind.

In diesem Tutorial werden die Schritte zum Hinzufügen von Kennzeichnungen zu einem Schema mithilfe des Schema-Editors in der Experience Platform-Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM) System]](../home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten von [!DNL Experience Platform] organisiert werden.
   * [Schema-Editor](../ui/overview.md): Erfahren Sie, wie Sie Schemas und andere Ressourcen in der Experience Platform-Benutzeroberfläche erstellen und verwalten.
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md): Bietet die Infrastruktur zum Durchsetzen von Datennutzungsbeschränkungen für Experience Platform-Vorgänge mithilfe von Richtlinien, die definieren, welche Marketing-Aktionen für gekennzeichnete Daten ausgeführt werden können (oder nicht).

## Auswählen eines Schemas oder Felds, dem Beschriftungen hinzugefügt werden sollen {#select-schema-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_editgovernancelabels"
>title="Governance-Kennzeichnungen bearbeiten"
>abstract="Wenden Sie eine Kennzeichnung auf ein Schemafeld an, um die Nutzungsrichtlinien festzulegen, die für die in diesem Feld enthaltenen Daten gelten."

Um mit dem Hinzufügen von Kennzeichnungen zu beginnen, müssen Sie zunächst [ein vorhandenes Schema zum Bearbeiten auswählen](../ui/resources/schemas.md#edit) oder [ein neues Schema erstellen](../ui/resources/schemas.md#create) um dessen Struktur im Schema-Editor anzuzeigen.

Um die Beschriftungen für ein einzelnes Feld zu bearbeiten, können Sie das Feld auf der Arbeitsfläche und dann **[!UICONTROL Manage access]** in der rechten Leiste auswählen.

>[!IMPORTANT]
>
>Auf jedes Schema können maximal 300 Kennzeichnungen angewendet werden.

![Wählen Sie ein Feld auf der Arbeitsfläche des Schema-Editors aus](../images/tutorials/labels/manage-access.png)

Sie können auch die Registerkarte **[!UICONTROL Labels]** auswählen, das gewünschte Feld aus der Liste auswählen und in der rechten Leiste **[!UICONTROL Apply Access and Data Governance Labels]** auswählen.

![Wählen Sie ein Feld auf der Registerkarte [!UICONTROL Labels] aus](../images/tutorials/labels/select-field-on-labels-tab.png)

Um die Kennzeichnungen für das gesamte Schema zu bearbeiten, aktivieren Sie auf der Registerkarte **[!UICONTROL Labels]** das Kontrollkästchen unter dem Filtersymbol. Dadurch werden alle verfügbaren Felder im Schema ausgewählt. Wählen Sie anschließend **[!UICONTROL Apply Access and Data Governance Labels]** in der rechten Leiste aus.

![Wählen Sie den Schemanamen auf der Registerkarte [!UICONTROL Labels] aus](../images/tutorials/labels/select-schema-on-labels-tab.png)

>[!NOTE]
>
>Wenn Sie zum ersten Mal versuchen, die Kennzeichnungen für ein Schema oder Feld zu bearbeiten, wird eine Haftungsausschlussmeldung angezeigt, die erklärt, wie sich die Verwendung von Kennzeichnungen auf nachgelagerte Vorgänge je nach den Richtlinien Ihrer Organisation auswirkt. Wählen Sie **[!UICONTROL Proceed]** aus, um mit der Bearbeitung fortzufahren.
>
>![Haftungsausschluss für die Verwendung von Bezeichnungen](../images/tutorials/labels/disclaimer.png)

## Bearbeiten der Kennzeichnungen für das Schema oder Feld {#edit-labels}

Es wird ein Dialogfeld angezeigt, in dem Sie die Beschriftungen für das ausgewählte Feld bearbeiten können. Wenn Sie ein einzelnes Feld vom Typ „Objekt“ ausgewählt haben, werden in der rechten Leiste die Unterfelder aufgelistet, in die die angewendeten Kennzeichnungen weitergegeben werden.

![Das Dialogfeld „Zugriff anwenden“ und „Data Governance-Kennzeichnungen“ mit hervorgehobenen ausgewählten Feldern.](../images/tutorials/labels/edit-labels.png)

>[!NOTE]
>
>Wenn Sie Felder für das gesamte Schema bearbeiten, werden in der rechten Leiste die entsprechenden Felder nicht aufgelistet und stattdessen der Schemaname angezeigt.

Verwenden Sie die angezeigte Liste, um die Kennzeichnungen auszuwählen, die Sie dem Schema oder Feld hinzufügen möchten. Wenn Kennzeichnungen ausgewählt werden, wird der Abschnitt **[!UICONTROL Applied labels]** aktualisiert und zeigt die Kennzeichnungen an, die bisher ausgewählt wurden.

![Das Dialogfeld „Zugriff anwenden“ und „Data Governance-Beschriftungen“ mit hervorgehobenen angewendeten Beschriftungen.](../images/tutorials/labels/applied-labels.png)

Um die angezeigten Beschriftungen nach Typ zu filtern, wählen Sie die gewünschte Kategorie in der linken Leiste aus. Um eine neue benutzerdefinierte Beschriftung zu erstellen, wählen Sie **[!UICONTROL Create label]** aus.

![Das Dialogfeld „Zugriffs- und Data Governance-Kennzeichnungen anwenden“ mit einem Filter vom Typ „Kennzeichnung“ und hervorgehobener Option „Kennzeichnung erstellen“.](../images/tutorials/labels/filter-and-create-custom.png)

Wenn Sie mit den ausgewählten Kennzeichnungen zufrieden sind, wählen Sie **[!UICONTROL Save]** aus, um sie auf das Feld oder Schema anzuwenden.

![Das Dialogfeld „Zugriff anwenden“ und „Data Governance-Kennzeichnungen“ mit hervorgehobener Option „Speichern“.](../images/tutorials/labels/save-labels.png)

Die Registerkarte **[!UICONTROL Labels]** wird erneut mit den angewendeten Kennzeichnungen für das Schema angezeigt.

![Die Registerkarte „Kennzeichnungen“ des Arbeitsbereichs „Schemata“ mit hervorgehobenen angewendeten Feldkennzeichnungen.](../images/tutorials/labels/field-labels-added.png)

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie Datennutzungsbeschriftungen für Schemata und Felder verwalten. Informationen zur Verwaltung von Datennutzungskennzeichnungen, einschließlich ihrer Hinzufügung zu bestimmten Datensätzen anstatt auf Schemaebene, finden Sie im [Handbuch zur Benutzeroberfläche von Datennutzungskennzeichnungen](../../data-governance/labels/user-guide.md).
