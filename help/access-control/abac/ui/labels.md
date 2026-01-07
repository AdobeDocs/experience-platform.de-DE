---
keywords: Experience Platform;Startseite;beliebte Themen;Zugriffssteuerung;attributbasierte Zugriffssteuerung
title: Attributbasierte Zugriffssteuerung - Kennzeichnungen verwalten
description: Verwalten von Kennzeichnungen über die Benutzeroberfläche „Berechtigungen“ in Adobe Experience Cloud.
exl-id: c790f09c-fda6-48bf-95db-3f5053cd882e
source-git-commit: 855f0a1384f658d39aa9d4fbb6bcb032933e59db
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 13%

---

# Verwalten von Labels

Mit Beschriftungen können Sie Datensätze und Felder entsprechend den Richtlinien für die Datennutzung und die attributbasierte Zugriffssteuerung kategorisieren. Labels können jederzeit angewendet werden, was eine flexible Handhabung der Daten ermöglicht. Best Practices legen nahe, Daten direkt bei ihrer Aufnahme in Adobe Experience Platform oder ab dem Zeitpunkt ihrer Nutzbarkeit mit einer Beschriftung zu versehen. Lesen Sie dieses Dokument, um zu erfahren, wie Sie Beschriftungen in der Benutzeroberfläche „Berechtigungen“ verwalten können.

Eine umfassende Liste der Kennzeichnungen und der entsprechenden Governance-Richtlinien finden Sie im Handbuch [Core-Datennutzungskennzeichnungen](../../../data-governance/labels/reference.md){target="_blank"}.

>[!NOTE]
>
>Zum Erstellen oder Anzeigen [berechneten Attribute](../../../profile/computed-attributes/overview.md){target="_blank"} mit Feldern, die eine bestimmte Kennzeichnung enthalten, benötigen Sie Zugriff auf diese Kennzeichnung.

## Kennzeichnungen erkunden {#explore-labels}

Um alle verfügbaren Bezeichnungen anzuzeigen, navigieren Sie zu **[!UICONTROL Permissions]** in [Adobe Experience Cloud](https://experience.adobe.com/){target="_blank"}. Wählen Sie **[!UICONTROL Labels]** im linken Bedienfeld aus.

![Der Arbeitsbereich „Kennzeichnungen“ in „Berechtigungen“ mit hervorgehobenen Kennzeichnungen im linken Bereich.](../../images/ui/labels/labels-home.png){zoomable="yes"}

Kennzeichnungen werden nach Typ kategorisiert und gehören zu einer der folgenden Kategorien:

| Typ | Beschreibung |
| --- | --- |
| [Vertrag](../../../data-governance/labels/reference.md#contract){target="_blank"} | Diese Kategorie wird verwendet, um Daten zu kategorisieren, für die vertragliche Verpflichtungen bestehen oder die mit den Data-Governance-Richtlinien Ihres Unternehmens in Zusammenhang stehen. |
| [Identität](../../../data-governance/labels/reference.md#identity){target="_blank"} | Diese Kategorie wird verwendet, um Daten zu kategorisieren, mit denen eine Person direkt oder indirekt identifiziert werden kann. |
| [sensitiv](../../../data-governance/labels/reference.md#sensitive){target="_blank"} | Diese Kategorie wird verwendet, um Daten zu kategorisieren, die Ihr Unternehmen als sensibel erachtet. |
| [Partner-Ökosystem](../../../data-governance/labels/reference.md#partner){target="_blank"} | Diese Kategorie wird verwendet, um Daten zu kategorisieren, die aus externen Quellen Ihrer Organisation bezogen werden. |
| Verantwortungsvolle Interaktion | Diese Kategorie enthält eine einzige Beschriftung, **[!UICONTROL Potential for Bias]**, die Daten widerspiegelt, die möglicherweise verzerrend wirken. |
| Benutzerspezifisch | Diese Kategorie enthält Beschriftungen, die von Ihrer Organisation erstellt wurden. |

Um Kennzeichnungen zu filtern, wählen Sie das Filtersymbol (![Filtersymbol](/help/images/icons/filter.png)) und dann den gewünschten Kennzeichnungstyp aus der **[!UICONTROL Type]** Dropdown-Liste aus.

![Der Arbeitsbereich „Kennzeichnungen“ mit erweiterter Filteroption und hervorgehobener Dropdown-Liste „Typ“.](../../images/ui/labels/label-filter.png){zoomable="yes"}

Um eine einzelne Kennzeichnung anzuzeigen, wählen Sie den Namen der Kennzeichnung aus der Liste aus. Die Detailseite des Titels wird angezeigt. Die Kernkennzeichnungen von Adobe **nicht** bearbeitbar.

![Die Detailseite einer einzelnen Kennzeichnung.](../../images/ui/labels/label-details.png){zoomable="yes"}

## Erstellen einer benutzerdefinierten Beschriftung {#create-custom-label}

>[!CONTEXTUALHELP]
>id="platform_abac_labelusage"
>title="Verwendung von Kennzeichnungen"
>abstract="Sie können benutzerdefinierte Kennzeichnungen verwenden, um Data-Governance- und Zugriffssteuerungs-Konfigurationen auf Ihre Daten anzuwenden."

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about_create"
>title="Erstellen neuer Kennzeichnungen"
>abstract="Sie können eigene Kennzeichnungen entsprechend den Anforderungen Ihres Unternehmens definieren. Mithilfe benutzerdefinierter Kennzeichnungen können Sie auf Ihre Daten Konfigurationen für Data Governance und Zugriffssteuerung anwenden."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=de#manage-labels" text="Verwalten von benutzerdefinierten Labels"

>[!NOTE]
>
>Um eine benutzerdefinierte Kennzeichnung zu erstellen, benötigen Sie eine Rolle, die die **[!UICONTROL Manage Usage Labels]** Berechtigungen und die `Prod`-Sandbox enthält.

Um eine neue Beschriftung zu erstellen, wählen Sie im linken Bereich des Arbeitsbereichs **[!UICONTROL Labels]** die Option **[!UICONTROL Permissions]** und dann **[!UICONTROL Create label]** aus.

![Der Arbeitsbereich „Kennzeichnungen“ mit hervorgehobener Option „Kennzeichnung erstellen“.](../../images/ui/labels/create-label.png){zoomable="yes"}

Das **[!UICONTROL Create new label]** Dialogfeld wird angezeigt und fordert Sie zur Eingabe eines **[!UICONTROL Name]**, eines **[!UICONTROL Friendly name]** und einer **[!UICONTROL Description]** auf.

>[!IMPORTANT]
>
> Die [!UICONTROL Name] der Kennzeichnung kann nach der Erstellung der Kennzeichnung nicht mehr geändert werden und das Löschen der Kennzeichnung wird derzeit nicht unterstützt.

Wählen Sie **[!UICONTROL Confirm]** aus, um die Erstellung Ihrer Bezeichnung abzuschließen.

![Das Dialogfeld „Neue Kennzeichnung erstellen“ mit hervorgehobenem Namen, Anzeigenamen und Beschreibung und hervorgehobener Option „Bestätigen“.](../../images/ui/labels/create-new-label.png){zoomable="yes"}

## Bearbeiten einer benutzerdefinierten Beschriftung {#edit-custom-label}

Sie können zwar nicht die **[!UICONTROL Name]** einer benutzerdefinierten Beschriftung bearbeiten, aber Sie können die **[!UICONTROL Friendly name]** und **[!UICONTROL Description]** bearbeiten. Um eine benutzerdefinierte Beschriftung zu bearbeiten, wählen Sie die Beschriftung aus der Liste im **[!UICONTROL Labels]** Arbeitsbereich aus.

![Der Arbeitsbereich „Kennzeichnungen“ mit hervorgehobener Kennzeichnung.](../../images/ui/labels/select-label.png){zoomable="yes"}

Bearbeiten Sie eines der Felder und klicken Sie dann auf eine beliebige Stelle außerhalb des Textfelds, um Ihre Änderungen zu speichern. Auf dem Bildschirm wird eine Bestätigungsmeldung angezeigt, und der **[!UICONTROL Modified by]** und das **[!UICONTROL Modified]** werden geändert.

![Die Detailseite der Kennzeichnung mit der Meldung „Erfolgreich aktualisiert“ wird angezeigt.](../../images/ui/labels/edit-label.png){zoomable="yes"}

## Nächste Schritte

Jetzt, da Sie ein tieferes Verständnis von Kennzeichnungen haben, können Sie beginnen, [sie auf Schemata anzuwenden](../../../xdm/tutorials/labels.md).
