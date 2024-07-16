---
keywords: Experience Platform; home; beliebte Themen; API; XDM; XDM; XDM-System; Experience-Datenmodell; Datenmodell; ui; workspace; enum; field;
solution: Experience Platform
title: Definieren von Enum-Feldern und vorgeschlagenen Werten in der Benutzeroberfläche
description: Erfahren Sie, wie Sie in der Experience Platform-Benutzeroberfläche Auflistungen und empfohlene Werte für Zeichenfolgenfelder definieren.
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 8%

---

# Definieren von Auflistungen und vorgeschlagenen Werten in der Benutzeroberfläche {#enums-and-suggested-values}

>[!CONTEXTUALHELP]
>id="platform_xdm_enum_suggestedvalue"
>title="Aufzählungen und empfohlene Werte"
>abstract="Eine **Aufzählung** beschränkt ein Zeichenfolgen-Feld so, dass nur Daten aufgenommen werden können, die mit einem vordefinierten Satz von Werten übereinstimmen. Jeder Aufzählungs-Beschränkung kann ein **Anzeigename** zugewiesen werden, mit dem in der Segmentierungs-Benutzeroberfläche Attribut-Dropdown-Listen befüllt werden. **Vorgeschlagene Werte** für ein Feld schränken die Aufnahme nicht ein, sondern bestimmen nur die in der Segmentierung dargestellten Anzeigenamen. Wenn Sie mehrere Schemata haben, die ein Feld gemeinsam nutzen, das zu einer gemeinsamen Klasse oder Feldergruppe gehört, und Sie zwischen den einzelnen Schemata unterschiedliche Aufzählungen oder vorgeschlagene Werte für dieses Feld definieren, werden diese Werte zusammengeführt und im Vereinigungsschema angefügt."

Im Experience-Datenmodell (XDM) kann einem Zeichenfolgenfeld ein vordefinierter Satz von akzeptierten oder vorgeschlagenen Werten zugewiesen werden, um besser steuern zu können, welche Werte in dieses Feld aufgenommen werden oder wie es sich bei der Segmentierung verhalten wird.

**[!UICONTROL Enums]** begrenzt die Werte, die für ein Zeichenfolgenfeld erfasst werden können, auf einen vordefinierten Satz. Wenn Sie versuchen, Daten in ein Enum-Feld zu erfassen und der Wert mit keinem der in der Konfiguration definierten Werte übereinstimmt, wird die Aufnahme verweigert.

Im Gegensatz zu Auflistungen ermöglicht die Option **[!UICONTROL Vorgeschlagene Werte]** die Angabe eines Satzes empfohlener Werte für ein Zeichenfolgenfeld, das die Werte, die aufgenommen werden können, nicht einschränkt. Stattdessen wirken sich die vorgeschlagenen Werte darauf aus, welche vordefinierten Werte in der [Segmentierungsbenutzeroberfläche](../../../segmentation/ui/overview.md) verfügbar sind, wenn das Zeichenfolgenfeld als Attribut eingefügt wird.

Wenn [ein neues Feld ](./overview.md#define) in der Adobe Experience Platform-Benutzeroberfläche definiert und der Typ auf [!UICONTROL String] gesetzt wird, erhalten Sie die Möglichkeit, für dieses Feld die Werte [enum](#enum) oder [empfohlen](#suggested-values) zu definieren.

![Bild, das die Option &quot;Aufzählung und empfohlene Werte&quot;für ein Zeichenfolgenfeld in der Benutzeroberfläche aktiviert hat](../../images/ui/fields/enum/enum-options-selected.png)

In diesem Dokument wird beschrieben, wie Sie Auflistungen und vorgeschlagene Werte im Arbeitsbereich der Benutzeroberfläche von [!UICONTROL Schemas] definieren. Ein kurzer Überblick über Auflistungen und empfohlene Werte, einschließlich ihrer Konfiguration in der Benutzeroberfläche und deren nachgelagerten Effekten, erhalten Sie im folgenden Video:

>[!VIDEO](https://video.tv.adobe.com/v/3409501/?quality=12&learn=on)

## Definieren einer Enumeration {#enum}

Wählen Sie **[!UICONTROL Auflistungen und Vorgeschlagene Werte]** und dann **[!UICONTROL Auflistungen]** aus. Es werden zusätzliche Steuerelemente angezeigt, mit denen Sie die Wertbegrenzungen für die Enumeration angeben können. Um eine Einschränkung hinzuzufügen, wählen Sie **[!UICONTROL Zeile hinzufügen]** aus.

![Bild mit der in der Benutzeroberfläche ausgewählten Option &quot;Auflistungen&quot;](../../images/ui/fields/enum/enum-add-row.png)

Unter der Spalte **[!UICONTROL Wert]** müssen Sie den genauen Wert angeben, auf den Sie das Feld beschränken möchten. Sie können optional auch einen benutzerfreundlichen **[!UICONTROL Anzeigenamen]** für die Begrenzung angeben, der sich auf die Darstellung des Werts in der Segmentierung auswirkt.

Verwenden Sie weiterhin &quot;**[!UICONTROL Zeile hinzufügen]**&quot;, um die gewünschten Einschränkungen und optionalen Beschriftungen zur Aufzählung hinzuzufügen, oder wählen Sie das Löschsymbol (![Bild des Löschsymbols](../../images/ui/fields/enum/remove-icon.png)) neben einer zuvor hinzugefügten Zeile aus, um sie zu entfernen. Wählen Sie abschließend **[!UICONTROL Anwenden]** aus, um die Änderungen auf das Schema anzuwenden.

![Bild, das die Aufzählungswerte und Anzeigenamen anzeigt, die für das Zeichenfolgenfeld in der Benutzeroberfläche ausgefüllt wurden](../../images/ui/fields/enum/enum-confirm.png)

Die Arbeitsfläche wird entsprechend den Änderungen aktualisiert. Wenn Sie dieses Schema zukünftig untersuchen, können Sie die Begrenzungen für das Enum-Feld in der rechten Leiste anzeigen und bearbeiten.

## Definieren empfohlener Werte {#suggested-values}

Wählen Sie **[!UICONTROL Auflistungen und Vorgeschlagene Werte]** und dann **[!UICONTROL Vorgeschlagene Werte]** aus, um zusätzliche Steuerelemente anzuzeigen. Wählen Sie hier **[!UICONTROL Zeile hinzufügen]** aus, um die vorgeschlagenen Werte hinzuzufügen.

![Bild, das die in der Benutzeroberfläche ausgewählte Option &quot;Vorgeschlagene Werte&quot;anzeigt](../../images/ui/fields/enum/suggested-add-row.png)

Geben Sie unter der Spalte **[!UICONTROL Anzeigename]** einen benutzerfreundlichen Namen für den Wert ein, wie er in der Segmentierungsbenutzeroberfläche angezeigt werden soll. Um weitere empfohlene Werte hinzuzufügen, wählen Sie erneut **[!UICONTROL Zeile hinzufügen]** und wiederholen Sie den Vorgang nach Bedarf. Um eine zuvor hinzugefügte Zeile zu entfernen, wählen Sie ![das Löschsymbol](../../images/ui/fields/enum/remove-icon.png) neben der betreffenden Zeile aus.

Wählen Sie abschließend **[!UICONTROL Anwenden]** aus, um die Änderungen auf das Schema anzuwenden.

![Bild, das die Aufzählungswerte und Anzeigenamen anzeigt, die für das Zeichenfolgenfeld in der Benutzeroberfläche ausgefüllt wurden](../../images/ui/fields/enum/suggested-confirm.png)

>[!NOTE]
>
>Es gibt eine ungefähre Verzögerung von fünf Minuten, bis die aktualisierten vorgeschlagenen Werte eines Felds in der Segmentierungsbenutzeroberfläche angezeigt werden.

### Verwalten von vorgeschlagenen Werten für Standardfelder

Einige Felder aus Standard-XDM-Komponenten enthalten ihre eigenen empfohlenen Werte, z. B. `eventType` aus der [[!UICONTROL XDM ExperienceEvent]-Klasse](../../classes/experienceevent.md). Sie können zwar zusätzliche empfohlene Werte für ein Standardfeld erstellen, jedoch keine von Ihrem Unternehmen nicht definierten vorgeschlagenen Werte ändern oder entfernen. Bei der Anzeige eines Standardfelds in der Benutzeroberfläche werden die vorgeschlagenen Werte angezeigt, sind jedoch schreibgeschützt.

![Bild, das die Aufzählungswerte und Anzeigenamen anzeigt, die für das Zeichenfolgenfeld in der Benutzeroberfläche ausgefüllt wurden](../../images/ui/fields/enum/suggested-standard.png)

Um neue empfohlene Werte für ein Standardfeld hinzuzufügen, wählen Sie **[!UICONTROL Zeile hinzufügen]** aus. Um einen vorgeschlagenen Wert zu entfernen, der zuvor von Ihrer Organisation hinzugefügt wurde, wählen Sie ![das Löschsymbol](../../images/ui/fields/enum/remove-icon.png) neben der betreffenden Zeile aus.

![Bild, das die Aufzählungswerte und Anzeigenamen anzeigt, die für das Zeichenfolgenfeld in der Benutzeroberfläche ausgefüllt wurden](../../images/ui/fields/enum/suggested-standard-add.png)

<!-- ### Removing suggested values for standard fields

Only suggested values that you define can be removed from a standard field. Existing suggested values can be disabled so that they no longer appear in the segmentation dropdown, but they cannot be removed outright.

For example, consider a profile schema where the a suggested value for the standard `person.gender` field is disabled:

![Image showing the enum values and display names filled out for the string field in the UI](../../images/ui/fields/enum/standard-enum-disabled.png)

In this example, the display name "[!UICONTROL Non-specific]" is now disabled from being shown in the segmentation dropdown list. However, the value `non_specific` is still part of the list of enumerated fields and is therefore still allowed on ingestion. In other words, you cannot disable the actual enum value for the standard field as it would go against the principle of only allowing changes that make a field less restrictive.

See the [section below](#evolution) for more information on the rules for updating enums and suggested values for existing schema fields. -->

## Evolutionsregeln für Auflistungen und empfohlene Werte {#evolution}

Nachdem ein Schema mit einem Enum-Feld verwendet wurde, um Daten in Platform aufzunehmen, müssen alle weiteren Änderungen an der Schemadefinition den bereits im System vorhandenen Daten entsprechen. Im Allgemeinen können Änderungen an einem vorhandenen Feld nur das Feld **less** einschränken. Ein Feld kann nicht restriktiver gestaltet werden als es bereits ist.

Bei Auflistungen und vorgeschlagenen Werten gelten die folgenden Regeln für die Nachaufnahme:

* Sie **CAN** können vorgeschlagene Werte für Standard- und benutzerdefinierte Felder mit vorhandenen vorgeschlagenen Werten hinzufügen.
* Sie **CAN** entfernen vorgeschlagene Werte aus benutzerdefinierten Feldern mit vorhandenen vorgeschlagenen Werten.
* Sie **CAN** können neue Enum-Werte für ein vorhandenes benutzerdefiniertes Enum-Feld hinzufügen.
* Sie können **CAN** die Enum-Werte eines benutzerdefinierten Felds in empfohlene Werte umschalten oder sie in eine Zeichenfolge ohne Enum oder vorgeschlagene Werte konvertieren. **Dieser Schalter kann nicht rückgängig gemacht werden, sobald er angewendet wurde.**
* Sie **KÖNNEN NICHT** Auflistungen oder vorgeschlagene Werte aus Standardfeldern entfernen.
* Sie **KÖNNEN NICHT** Enum-Werte zu einem Feld ohne vorhandene Enumeration hinzufügen.
* Sie **KÖNNEN NICHT** weniger als alle vorhandenen Enum-Werte für ein benutzerdefiniertes Feld entfernen.
* Sie **KÖNNEN NICHT** von vorgeschlagenen Werten zu einer Enumeration wechseln.

## Zusammenführen von Regeln für Auflistungen und empfohlene Werte {#merging}

Wenn mehrere Schemas dasselbe Enum-Feld mit unterschiedlichen Konfigurationen verwenden und diese Schemas in einer Vereinigung enthalten sind, gelten bestimmte Regeln für die Abstimmung von Enum-Unterschieden. Die genauen Regeln hängen davon ab, ob die Schemas, die auf dasselbe Standardfeld verweisen (z. B. `eventType`) oder ob sie in verschiedenen Feldgruppen auf denselben benutzerdefinierten Feldpfad verweisen.

Wenn auf dasselbe Standardfeld verwiesen wird:

* Alle weiteren vorgeschlagenen Werte sind **ANGEHÄNGT** in der Vereinigung.
* Aktualisierungen, die an den vorgeschlagenen Werten für denselben Enum-Schlüssel vorgenommen werden, sind **UPDATED** in der Vereinigung.

Wenn Sie in verschiedenen Feldgruppen auf denselben benutzerdefinierten Feldpfad verweisen:

* Alle weiteren vorgeschlagenen Werte sind **ANGEHÄNGT** in der Vereinigung.
* Wenn derselbe zusätzliche empfohlene Wert in mehr als einem Schema definiert ist, sind diese Werte **ZUSAMMENGED** in der Vereinigung. Mit anderen Worten, derselbe empfohlene Wert wird nach dem Zusammenführen nicht zweimal angezeigt.

## Validierungsbeschränkungen

Aufgrund der aktuellen Systembeschränkungen gibt es zwei Fälle, in denen eine Enumeration vom System während der Erfassung nicht validiert wird:

1. Der Enum wird in einem [Array-Feld](./array.md) definiert.
1. Der Enum ist in der Schemahierarchie auf mehr als einer Ebene definiert.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie Auflistungen und empfohlene Werte für Zeichenfolgenfelder in der Benutzeroberfläche definieren. Informationen zum Verwalten von Auflistungen und vorgeschlagenen Werten mithilfe der Schema Registry-API finden Sie im folgenden [Tutorial](../../tutorials/suggested-values.md).

Informationen zum Definieren anderer XDM-Feldtypen in der [!DNL Schema Editor] finden Sie in der Übersicht zum Definieren von Feldern in der Benutzeroberfläche [2}.](./overview.md#special)
