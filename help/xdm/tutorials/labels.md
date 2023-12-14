---
title: Verwalten von Datennutzungsbezeichnungen für ein Schema
description: Erfahren Sie, wie Sie in der Adobe Experience Platform-Benutzeroberfläche Schemafeldern des Experience-Datenmodell (XDM) Datennutzungsbezeichnungen hinzufügen.
exl-id: 92284bf7-f034-46cc-b905-bdfb9fcd608a
source-git-commit: 6fe11b909369797e96d8fa52542ebd5761a27b03
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 10%

---

# Verwalten von Datennutzungskennzeichnungen für ein Schema

>[!IMPORTANT]
>
>Die schemabasierte Beschriftung ist Teil von [attributbasierte Zugriffssteuerung](../../access-control/abac/overview.md), die derzeit in einer begrenzten Version für Kunden von Gesundheitsdienstleistungen in den USA verfügbar ist. Diese Funktion steht allen Adobe Real-time Customer Data Platform-Kunden nach der vollständigen Veröffentlichung zur Verfügung.

Alle Daten, die in Adobe Experience Platform importiert werden, sind durch Experience-Datenmodell (XDM)-Schemas eingeschränkt. Diese Daten können Nutzungsbeschränkungen unterliegen, die von Ihrem Unternehmen oder durch gesetzliche Bestimmungen festgelegt werden. Um dies zu berücksichtigen, können Sie mit Platform die Verwendung bestimmter Datensätze und Felder durch die Verwendung von [Datennutzungsbezeichnungen](../../data-governance/labels/overview.md).

Eine auf ein Schemafeld angewendete Beschriftung zeigt die Nutzungsrichtlinien an, die für die in diesem spezifischen Feld enthaltenen Daten gelten.

Beschriftungen können auf einzelne Schemata und Felder innerhalb dieser Schemas angewendet werden. Wenn Beschriftungen direkt auf ein Schema angewendet werden, werden diese Beschriftungen auf alle vorhandenen und zukünftigen Datensätze übertragen, die auf diesem Schema basieren.

Darüber hinaus werden alle Feldbeschriftungen, die Sie in einem Schema hinzufügen, zu allen anderen Schemas weitergeleitet, die dasselbe Feld aus einer freigegebenen Klasse oder Feldergruppe verwenden. So können Sie sicherstellen, dass die Nutzungsregeln für ähnliche Felder im gesamten Datenmodell einheitlich sind.

In diesem Tutorial werden die Schritte zum Hinzufügen von Bezeichnungen zu einem Schema mithilfe des Schema-Editors in der Platform-Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM) System]](../home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten von [!DNL Experience Platform] organisiert werden.
   * [Schema Editor](../ui/overview.md): Erfahren Sie, wie Sie Schemas und andere Ressourcen in der Platform-Benutzeroberfläche erstellen und verwalten.
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md): Bietet die Infrastruktur zum Durchsetzen von Datennutzungsbeschränkungen für Platform-Vorgänge mithilfe von Richtlinien, die definieren, welche Marketing-Aktionen für gekennzeichnete Daten ausgeführt werden können (oder nicht).

## Auswählen eines Schemas oder Felds, dem Beschriftungen hinzugefügt werden sollen {#select-schema-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_editgovernancelabels"
>title="Governance-Kennzeichnungen bearbeiten"
>abstract="Wenden Sie eine Kennzeichnung auf ein Schemafeld an, um die Nutzungsrichtlinien festzulegen, die für die in diesem Feld enthaltenen Daten gelten."

Um Beschriftungen hinzuzufügen, müssen Sie zunächst [ein vorhandenes Schema zur Bearbeitung auswählen](../ui/resources/schemas.md#edit) oder [Erstellen eines neuen Schemas](../ui/resources/schemas.md#create) , um die Struktur im Schema-Editor anzuzeigen.

Um die Beschriftungen für ein einzelnes Feld zu bearbeiten, können Sie das Feld auf der Arbeitsfläche auswählen und dann **[!UICONTROL Zugriff verwalten]** in der rechten Leiste.

>[!IMPORTANT]
>
>Auf jedes Schema können maximal 300 Bezeichnungen angewendet werden.

![Wählen Sie ein Feld aus der Arbeitsfläche des Schema-Editors aus](../images/tutorials/labels/manage-access.png)

Sie können auch die **[!UICONTROL Bezeichnungen]** , wählen Sie das gewünschte Feld aus der Liste aus und wählen Sie **[!UICONTROL Anwenden von Zugriffs- und Data Governance-Beschriftungen]** in der rechten Leiste.

![Wählen Sie ein Feld aus dem [!UICONTROL Bezeichnungen] tab](../images/tutorials/labels/select-field-on-labels-tab.png)

Um die Beschriftungen für das gesamte Schema zu bearbeiten, wählen Sie im **[!UICONTROL Bezeichnungen]** aktivieren, aktivieren Sie das Kontrollkästchen unter dem Filtersymbol. Dadurch werden alle verfügbaren Felder im Schema ausgewählt. Wählen Sie als Nächstes **[!UICONTROL Anwenden von Zugriffs- und Data Governance-Beschriftungen]** in der rechten Leiste.

![Wählen Sie den Schemanamen aus der [!UICONTROL Bezeichnungen] tab](../images/tutorials/labels/select-schema-on-labels-tab.png)

>[!NOTE]
>
>Wenn Sie zum ersten Mal versuchen, die Beschriftungen für ein Schema oder ein Feld zu bearbeiten, wird eine Haftungsausschlussmeldung angezeigt, die erklärt, wie sich die Beschriftungsnutzung je nach Richtlinien Ihres Unternehmens auf nachgelagerte Vorgänge auswirkt. Auswählen **[!UICONTROL Fortfahren]** , um die Bearbeitung fortzusetzen.
>
>![Haftungsausschluss für Beschriftung](../images/tutorials/labels/disclaimer.png)

## Bearbeiten der Beschriftungen für das Schema oder Feld {#edit-labels}

Es wird ein Dialogfeld angezeigt, in dem Sie die Beschriftungen für das ausgewählte Feld bearbeiten können. Wenn Sie ein einzelnes Feld vom Typ Objekt ausgewählt haben, werden in der rechten Leiste die Unterfelder aufgelistet, in die die angewendeten Beschriftungen propagiert werden.

![Die ausgewählten Felder werden im Dialogfeld Zugriff anwenden und Data Governance-Beschriftungen hervorgehoben.](../images/tutorials/labels/edit-labels.png)

>[!NOTE]
>
>Wenn Sie Felder für das gesamte Schema bearbeiten, werden in der rechten Leiste die entsprechenden Felder nicht aufgelistet und stattdessen der Schemaname angezeigt.

Verwenden Sie die angezeigte Liste, um die Titel auszuwählen, die Sie dem Schema oder Feld hinzufügen möchten. Wenn Beschriftungen ausgewählt werden, wird die **[!UICONTROL Angewandte Beschriftungen]** -Abschnitt aktualisiert, um die bisher ausgewählten Bezeichnungen anzuzeigen.

![Das Dialogfeld Zugriff anwenden und Beschriftungen für Data Governance mit hervorgehobenen angewendeten Beschriftungen.](../images/tutorials/labels/applied-labels.png)

Um die angezeigten Beschriftungen nach Typ zu filtern, wählen Sie in der linken Leiste die gewünschte Kategorie aus. Um eine neue benutzerdefinierte Bezeichnung zu erstellen, wählen Sie **[!UICONTROL Titel erstellen]**.

![Das Dialogfeld Zugriff auf Data Governance-Beschriftungen anwenden mit angewendetem Filter für Beschriftungstypen und hervorgehobener Beschriftung Erstellen .](../images/tutorials/labels/filter-and-create-custom.png)

Wenn Sie mit den ausgewählten Bezeichnungen zufrieden sind, wählen Sie **[!UICONTROL Speichern]** , um sie auf das Feld oder Schema anzuwenden.

![Das Dialogfeld Zugriff anwenden und Beschriftungen für Data Governance mit hervorgehobener Option Speichern .](../images/tutorials/labels/save-labels.png)

Die **[!UICONTROL Bezeichnungen]** wird erneut angezeigt und zeigt die angewendeten Bezeichnungen für das Schema an.

![Die Registerkarte &quot;Bezeichnungen&quot;im Arbeitsbereich &quot;Schemas&quot;mit hervorgehobenen Feldbezeichnungen.](../images/tutorials/labels/field-labels-added.png)

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Datennutzungsbezeichnungen für Schemas und Felder verwaltet werden. Informationen zum Verwalten von Datennutzungsbezeichnungen, einschließlich des Hinzufügens zu bestimmten Datensätzen anstelle von auf Schemaebene finden Sie in der [Benutzerhandbuch zu den Datennutzungsbezeichnungen](../../data-governance/labels/user-guide.md).
