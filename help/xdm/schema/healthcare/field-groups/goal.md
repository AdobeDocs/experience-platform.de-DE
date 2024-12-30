---
title: Zielschemafeldgruppe
description: Erfahren Sie mehr über die Zielschemafeldgruppe.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 87715274-cc9d-41da-9ca7-1634903b4e8f
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 6%

---

# [!UICONTROL Ziel] Schemafeldgruppe

[!UICONTROL Goal] ist eine standardmäßige Schemafeldgruppe für die [[!DNL XDM Individual Profile] class](../../../classes/individual-profile.md) und die [[!DNL Provider class]](../../../classes/provider.md). Sie bietet ein einzelnes Objekttyp-Feld, `healthcareGoal` das (die) beabsichtigte(n) Ziel(e) für einen Patienten, eine Gruppe oder eine Organisation beschreibt.

![Feldergruppenstruktur](../../../images/healthcare/field-groups/goal/goal.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Leistungsstatus] | `achievementStatus` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Beschreibt den Fortschritt (oder das Fehlen des Fortschritts) in Richtung des Ziels gegenüber dem Ziel. |
| [!UICONTROL Adressen] | `addresses` | Array von [[!UICONTROL Referenz]](../data-types/reference.md) | Die Bedingungen und andere Elemente der Gesundheitsdaten, die durch das Ziel behandelt werden sollen. |
| [!UICONTROL Kategorie] | `category` | Array von [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Gibt eine Kategorie an, in die das Ziel fällt, z. B. Ernährung oder Verhalten. |
| [!UICONTROL Beschreibung] | `description` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Der Code oder Text, der das Ziel beschreibt. |
| [!UICONTROL ID] | `identifier` | Array von [[!UICONTROL Identifier]](../data-types/identifier.md) | Die Geschäftskennungen, die diesem Ziel vom Ausführenden oder anderen Systemen zugewiesen wurden und konstant bleiben, während die Ressource aktualisiert wird und sich von Server zu Server ausbreitet. |
| [!UICONTROL Hinweis] | `note` | Array von [[!UICONTROL Anmerkung]](../data-types/annotation.md) | Kommentare zum Ziel. |
| [!UICONTROL Ergebnis] | `outcome` | Array von [[!UICONTROL Codeable Reference]](../data-types/codeable-reference.md) | kennzeichnet die Änderung (oder das Ausbleiben der Änderung), wenn der Status des Ziels bewertet wird. |
| [!UICONTROL Priorität] | `priority` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | kennzeichnet den einvernehmlich festgelegten Grad der Bedeutung im Zusammenhang mit dem Erreichen oder Aufrechterhalten des Ziels. |
| [!UICONTROL Quelle] | `source` | [[!UICONTROL Referenz]](../data-types/reference.md) | Gibt die Quelle des Ziels an, z. B. den Patienten oder den Arzt. |
| [!UICONTROL Codeable-Konzept starten] | `startCodeableConcept` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Das Ereignis, nach dem das Ziel dann verfolgt werden soll. |
| [!UICONTROL Subject |]`subject` | [[!UICONTROL Referenz]](../data-types/reference.md) | Identifiziert den Patienten, die Gruppe oder die Organisation, für den bzw. die das Ziel festgelegt wird. |
| [!UICONTROL Zielgruppe] | `target` | Array von Objekten | Gibt die Zeitleiste bestimmter Schritte im Ziel an. Weitere Informationen finden [ im ](#target) Abschnitt unten. |
| [!UICONTROL Fortlaufend] | `continous` | Boolesch | Gibt an, ob nach Erreichen des Ziels eine fortlaufende Aktivität erforderlich ist, um das Ziel aufrechtzuerhalten. |
| [!UICONTROL Lebenszyklus-Status] | `lifecycleStatus` | String | Der Status des Lebenszyklus des Ziels. Der Wert dieser Eigenschaft muss einem der folgenden bekannten Enum-Werte entsprechen. <li> `proposed` </li> <li> `planned` </li> <li> `accepted` </li> <li> `active` </li> <li> `on-hold` </li> <li> `completed` </li> <li> `cancelled` </li> <li> `entered-in-error` </li> <li> `rejected` </li> |
| [!UICONTROL Startdatum] | `startDate` | Datum | Das Datum, nach dem das Ziel verfolgt werden soll. |
| [!UICONTROL Statusdatum] | `statusDate` | Datum | Gibt an, wann der Status erstellt wurde. |
| [!UICONTROL Statusgrund] | `statusReason` | String | Erfasst den Grund für den aktuellen Status. |

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/goal.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/goal.example.1.json)

## `target` {#target}

`target` wird als Array von -Objekten bereitgestellt. Im Folgenden wird die Struktur der einzelnen Objekte beschrieben.

![Zielstruktur](../../../images/healthcare/field-groups/goal/target.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Detail codierbares Konzept] | `detailCodeableConcept` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Der Ziel-Code, der erreicht werden soll, um die Erfüllung des Ziels anzugeben. |
| [!UICONTROL Menge angeben] | `detailQuantity` | [[!UICONTROL Menge]](../data-types/quantity.md) | Die Zielmenge, die erreicht werden soll, um die Erfüllung des Ziels anzugeben. |
| [!UICONTROL Detailbereich] | `detailRange` | [[!UICONTROL Bereich]](../data-types/range.md) | Der Zielbereich, der erreicht werden soll, um die Erfüllung des Ziels anzugeben. |
| [!UICONTROL Detailverhältnis] | `detailRatio` | [[!UICONTROL Verhältnis]](../data-types/ratio.md) | Das Zielverhältnis, das erreicht werden soll, um die Erfüllung des Ziels anzugeben. |
| [!UICONTROL Maßnahme] | `measure` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Der Wert des Parameters wird verfolgt. |
| [!UICONTROL Detail Boolean] | `detailBoolean` | Boolesch | Gibt an, ob das Ziel erreicht wurde. |
| [!UICONTROL Ganzzahl] | `detailInteger` | Ganzzahl | Die Zielzahl, die erreicht werden soll, um die Erfüllung des Ziels anzugeben. |
| [!UICONTROL Detailzeichenfolge] | `detailString` | String | Der zu erreichende Zielwert, der die Erfüllung des Ziels angibt. |
| [!UICONTROL Fälligkeitsdatum] | `dueDate` | Datum | Das Datum, bis zu dem das Ziel erreicht sein sollte. |
