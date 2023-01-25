---
keywords: Experience Platform; Startseite; beliebte Themen; API; XDM; XDM; XDM-System; Experience-Datenmodell; Datenmodell; ui; Workspace; Enum; Feld;
solution: Experience Platform
title: Definieren von Enum-Feldern und vorgeschlagenen Werten in der Benutzeroberfläche
description: Erfahren Sie, wie Sie in der Experience Platform-Benutzeroberfläche Auflistungen und empfohlene Werte für Zeichenfolgenfelder definieren.
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
source-git-commit: f770ba8668c5154b2cf5a57ba61d771ca34ab2d8
workflow-type: tm+mt
source-wordcount: '1358'
ht-degree: 0%

---

# Definieren von Auflistungen und vorgeschlagenen Werten in der Benutzeroberfläche {#enums-and-suggested-values}

>[!CONTEXTUALHELP]
>id="platform_xdm_enum_suggestedvalue"
>title="Auflistungen und empfohlene Werte"
>abstract="Ein **Enum** beschränkt ein Zeichenfolgenfeld so, dass nur Daten erfasst werden können, die mit einem vordefinierten Satz von Werten übereinstimmen. Jeder Enum-Einschränkung kann ein **Anzeigename** die Dropdown-Listen mit Attributen in der Segmentierungsbenutzeroberfläche füllt. **Vorgeschlagene Werte** für ein Feld die Erfassung nicht einschränken und nur die in der Segmentierung angezeigten Anzeigenamen bestimmen. Wenn Sie mehrere Schemas haben, die ein Feld teilen, das zu einer gemeinsamen Klasse oder Feldergruppe gehört, und Sie verschiedene Auflistungen oder vorgeschlagene Werte für dieses Feld zwischen den einzelnen Schemas definieren, werden diese Werte zusammengeführt und im Vereinigungsschema angehängt."

Im Experience-Datenmodell (XDM) kann einem Zeichenfolgenfeld ein vordefinierter Satz von akzeptierten oder vorgeschlagenen Werten zugewiesen werden, um besser steuern zu können, welche Werte in dieses Feld aufgenommen werden oder wie es sich bei der Segmentierung verhalten wird.

**[!UICONTROL Enums]** beschränken Sie die Werte, die für ein Zeichenfolgenfeld erfasst werden können, auf einen vordefinierten Satz. Wenn Sie versuchen, Daten in ein Enum-Feld zu erfassen und der Wert mit keinem der in der Konfiguration definierten Werte übereinstimmt, wird die Aufnahme verweigert.

Im Gegensatz zu Auflistungen wird die **[!UICONTROL Vorgeschlagene Werte]** -Option ermöglicht es, einen Satz empfohlener Werte für ein Zeichenfolgenfeld zu kennzeichnen, das die erfassten Werte nicht einschränkt. Stattdessen wirken sich die vorgeschlagenen Werte darauf aus, welche vordefinierten Werte im [Segmentierungsbenutzeroberfläche](../../../segmentation/ui/overview.md) , wenn das Zeichenfolgenfeld als Attribut eingefügt wird.

Wann [Definieren eines neuen Felds](./overview.md#define) in der Adobe Experience Platform-Benutzeroberfläche und legen Sie den Typ auf [!UICONTROL Zeichenfolge], erhalten Sie die Möglichkeit, eine [enum](#enum) oder [empfohlene Werte](#suggested-values) für dieses Feld.

![Die Option Aufzählung und Vorgeschlagene Werte ist für ein Zeichenfolgenfeld in der Benutzeroberfläche aktiviert.](../../images/ui/fields/enum/enum-options-selected.png)

In diesem Dokument wird beschrieben, wie Sie Auflistungen und empfohlene Werte im [!UICONTROL Schemas] UI-Arbeitsbereich. Ein kurzer Überblick über Auflistungen und empfohlene Werte, einschließlich ihrer Konfiguration in der Benutzeroberfläche und deren nachgelagerten Effekten, erhalten Sie im folgenden Video:

>[!VIDEO](https://video.tv.adobe.com/v/3409501/?quality=12&learn=on)

## Definieren einer Enumeration {#enum}

Auswählen **[!UICONTROL Auflistungen und empfohlene Werte]**, wählen Sie **[!UICONTROL Enums]**. Es werden zusätzliche Steuerelemente angezeigt, mit denen Sie die Wertbegrenzungen für die Enumeration angeben können. Um eine Einschränkung hinzuzufügen, wählen Sie **[!UICONTROL Zeile hinzufügen]**.

![Die in der Benutzeroberfläche ausgewählte Option Auflistungen .](../../images/ui/fields/enum/enum-add-row.png)

Unter dem **[!UICONTROL Wert]** -Spalte müssen Sie den genauen Wert angeben, auf den Sie das Feld beschränken möchten. Sie können optional eine benutzerfreundliche **[!UICONTROL Anzeigename]** auch für die Beschränkung, was sich auf die Darstellung des Werts in der Segmentierung auswirkt.

Weitere Verwendung **[!UICONTROL Zeile hinzufügen]** , um die gewünschten Einschränkungen und optionalen Beschriftungen zur Enumeration hinzuzufügen, oder wählen Sie das Löschsymbol (![Bild des Löschsymbols](../../images/ui/fields/enum/remove-icon.png)) neben einer zuvor hinzugefügten Zeile, um sie zu entfernen. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Anwenden]** , um die Änderungen auf das Schema anzuwenden.

![Die Aufzählungswerte und Anzeigenamen, die für das Zeichenfolgenfeld in der Benutzeroberfläche ausgefüllt wurden.](../../images/ui/fields/enum/enum-confirm.png)

Die Arbeitsfläche wird entsprechend den Änderungen aktualisiert. Wenn Sie dieses Schema zukünftig untersuchen, können Sie die Begrenzungen für das Enum-Feld in der rechten Leiste anzeigen und bearbeiten.

## Definieren empfohlener Werte {#suggested-values}

Auswählen **[!UICONTROL Auflistungen und empfohlene Werte]**, wählen Sie **[!UICONTROL Vorgeschlagene Werte]** um zusätzliche Steuerelemente anzuzeigen. Wählen Sie von hier aus **[!UICONTROL Zeile hinzufügen]** , um die vorgeschlagenen Werte hinzuzufügen.

![Die Option Empfohlene Werte wurde in der Benutzeroberfläche ausgewählt.](../../images/ui/fields/enum/suggested-add-row.png)

Unter dem **[!UICONTROL Anzeigename]** geben Sie einen benutzerfreundlichen Namen für den Wert ein, wie er in der Segmentierungsbenutzeroberfläche angezeigt werden soll. Um weitere empfohlene Werte hinzuzufügen, wählen Sie **[!UICONTROL Zeile hinzufügen]** und wiederholen Sie den Vorgang nach Bedarf. Um eine zuvor hinzugefügte Zeile zu entfernen, wählen Sie ![Löschsymbol](../../images/ui/fields/enum/remove-icon.png) neben der betreffenden Zeile.

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Anwenden]** , um die Änderungen auf das Schema anzuwenden.

![Die Aufzählungswerte und Anzeigenamen, die für das Zeichenfolgenfeld in der Benutzeroberfläche ausgefüllt wurden.](../../images/ui/fields/enum/suggested-confirm.png)

>[!NOTE]
>
>Es gibt eine ungefähre Verzögerung von fünf Minuten, bis die aktualisierten vorgeschlagenen Werte eines Felds in der Segmentierungsbenutzeroberfläche angezeigt werden.

### Verwalten von vorgeschlagenen Werten für Standardfelder {#standard-fields}

Einige Felder aus Standard-XDM-Komponenten enthalten ihre eigenen empfohlenen Werte, z. B. `eventType` von [[!UICONTROL XDM ExperienceEvent] class](../../classes/experienceevent.md) und Sie können zusätzliche empfohlene Werte für diese Standardfelder auf die gleiche Weise wie für benutzerdefinierte Felder erstellen. Sie können auch jeden der vorgeschlagenen Standardwerte deaktivieren, der Ihren Anwendungsfällen nicht entspricht, aber nicht vollständig aus der Felddefinition entfernt werden kann.

>[!IMPORTANT]
>
>Sie können die vorgeschlagenen Werte nur für Standardfelder deaktivieren, die keine entsprechende Enum-Einschränkung aufweisen. Mit anderen Worten, wenn die Variable **[!UICONTROL Enums]** -Option anstelle von **[!UICONTROL Vorgeschlagene Werte]** festgelegt ist, wird das Feld als Enum eingeschränkt und diese Begrenzungen können nicht deaktiviert werden.
>
>Siehe [Abschnitt unten](#evolution) für weitere Informationen zu den Regeln zum Aktualisieren von Auflistungen und vorgeschlagenen Werten für vorhandene Schemafelder.

Um einen vorgeschlagenen Standardwert zu deaktivieren, wählen Sie den Umschalter neben dem betreffenden Wert aus. Sie können jede beliebige Kombination von vorgeschlagenen Werten deaktivieren, einschließlich aller Werte.

![Einige der vorgeschlagenen Standardwerte für die [!UICONTROL Ereignistyp] -Feld in der Benutzeroberfläche deaktiviert.](../../images/ui/fields/enum/suggested-standard.png)

Um neue empfohlene Werte für ein Standardfeld hinzuzufügen, wählen Sie **[!UICONTROL Zeile hinzufügen]**. Um einen vorgeschlagenen Wert zu entfernen, der zuvor von Ihrer Organisation hinzugefügt wurde, wählen Sie ![Löschsymbol](../../images/ui/fields/enum/remove-icon.png) neben der betreffenden Zeile.

![Benutzerdefinierte empfohlene Werte werden zu einem Standardzeichenfolgenfeld in der Benutzeroberfläche hinzugefügt.](../../images/ui/fields/enum/suggested-standard-add.png)

## Evolutionsregeln für Auflistungen und empfohlene Werte {#evolution}

Nachdem ein Schema mit einem Enum-Feld verwendet wurde, um Daten in Platform aufzunehmen, müssen alle weiteren Änderungen an der Schemadefinition den bereits im System vorhandenen Daten entsprechen. Im Allgemeinen können Änderungen an einem vorhandenen Feld nur dieses Feld betreffen **less** restriktiv sein. Ein Feld kann nicht restriktiver gestaltet werden als es bereits ist.

Bei Auflistungen und vorgeschlagenen Werten gelten die folgenden Regeln für die Nachaufnahme:

* You **CAN** Fügen Sie vorgeschlagenen Werten zu jedem Feld mit vorhandenen vorgeschlagenen Werten hinzu.
* You **CAN** Entfernen Sie benutzerdefinierte empfohlene Werte aus Feldern mit vorhandenen vorgeschlagenen Werten.
* You **CAN** Deaktivieren Sie empfohlene Standardwerte aus Feldern, die nur empfohlene Werte und keine Enum-Begrenzungen enthalten.
* You **CAN** Fügen Sie neue Enum-Werte für ein vorhandenes benutzerdefiniertes Enum-Feld hinzu.
* You **CAN** Ändern Sie die Enum-Werte eines benutzerdefinierten Felds in empfohlene Werte oder konvertieren Sie sie in eine Zeichenfolge ohne Enum oder vorgeschlagene Werte. **Dieser Schalter kann nach der Anwendung nicht mehr rückgängig gemacht werden.**
* You **CANNOT** Hinzufügen oder Entfernen von Enum-Begrenzungen aus Standardfeldern.
* You **CANNOT** Entfernen Sie vorgeschlagene Werte aus Standardfeldern (nur deaktivieren).
* You **CANNOT** Fügen Sie Enum-Begrenzungen zu Feldern ohne vorhandene Enumeration hinzu.
* You **CANNOT** weniger als alle vorhandenen Enum-Einschränkungen für ein benutzerdefiniertes Feld entfernen.
* You **CANNOT** Wechsel von vorgeschlagenen Werten zu einer Enumeration.

## Zusammenführen von Regeln für Auflistungen und empfohlene Werte {#merging}

Wenn mehrere Schemas dasselbe Enum-Feld mit unterschiedlichen Konfigurationen verwenden und diese Schemas in einer Vereinigung enthalten sind, gelten bestimmte Regeln für die Abstimmung von Enum-Unterschieden. Die genauen Regeln hängen davon ab, ob die Schemas, die auf dasselbe Standardfeld verweisen (wie `eventType`) oder wenn sie in verschiedenen Feldergruppen auf denselben benutzerdefinierten Feldpfad verweisen.

Wenn auf dasselbe Standardfeld verwiesen wird:

* Alle weiteren empfohlenen Werte sind **ANGEHÄNGT** in der Union.
* An den vorgeschlagenen Werten für denselben Enum-Schlüssel werden folgende Aktualisierungen vorgenommen: **AKTUALISIERT** in der Union.

Wenn Sie in verschiedenen Feldgruppen auf denselben benutzerdefinierten Feldpfad verweisen:

* Alle weiteren empfohlenen Werte sind **ANGEHÄNGT** in der Union.
* Wenn derselbe zusätzliche empfohlene Wert in mehr als einem Schema definiert ist, werden diese Werte **ZUSAMMENGED** in der Union. Mit anderen Worten, derselbe vorgeschlagene Wert wird nach dem Zusammenführen nicht zweimal angezeigt.

## Validierungsbeschränkungen

Aufgrund der aktuellen Systembeschränkungen gibt es zwei Fälle, in denen eine Enumeration vom System während der Erfassung nicht validiert wird:

1. Die Enumeration wird auf einer [Array-Feld](./array.md).
1. Der Enum ist in der Schemahierarchie auf mehr als einer Ebene definiert.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie Auflistungen und empfohlene Werte für Zeichenfolgenfelder in der Benutzeroberfläche definieren. Informationen zum Verwalten von Auflistungen und empfohlenen Werten mithilfe der Schema Registry-API finden Sie in den folgenden [Tutorial](../../tutorials/suggested-values.md).

Erfahren Sie, wie Sie andere XDM-Feldtypen im [!DNL Schema Editor], siehe Übersicht unter [Definieren von Feldern in der Benutzeroberfläche.](./overview.md#special).
