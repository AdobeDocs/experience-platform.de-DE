---
title: Zielschemafeldgruppe
description: Erfahren Sie mehr über die Zielschemafeldgruppe.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 68fa7ea5de1629886cc9ba3d5c8efd4e5d57d4b3
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 6%

---

# [!UICONTROL Ziel] Schemafeldgruppe

[!UICONTROL Ziel] ist eine Standardschemafeldgruppe für die [[!DNL XDM Individual Profile] Klasse](../../classes/individual-profile.md) und die [[!DNL Provider class]](../../classes/provider.md). Es stellt ein einzelnes Objektfeld `healthcareGoal` bereit, das die beabsichtigten Ziele für eine Patienten-, Gruppen- oder Organisationsbetreuung beschreibt.

![Feldgruppenstruktur](../../images/field-groups/healthcare-goal/goal.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Erfüllungsstatus] | `achievementStatus` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Beschreibt den Fortschritt bzw. das Fehlen von Fortschritten beim Erreichen des Ziels gegen das Ziel. |
| [!UICONTROL Adressen] | `addresses` | Array von [[!UICONTROL Verweis]](../../data-types/healthcare/reference.md) | Die Bedingungen und anderen Elemente des Gesundheitsdatensatzes, die vom Ziel angesprochen werden sollen. |
| [!UICONTROL Kategorie] | `category` | Array von [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Gibt eine Kategorie an, in die das Ziel fällt, z. B. Nahrung oder Verhalten. |
| [!UICONTROL Beschreibung] | `description` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Der Code oder Text, der das Ziel beschreibt. |
| [!UICONTROL ID] | `identifier` | Array von [[!UICONTROL Bezeichner]](../../data-types/healthcare/identifier.md) | Die diesem Ziel vom Performer oder anderen Systemen zugewiesenen Geschäftskennungen, die konstant bleiben, wenn die Ressource aktualisiert wird und von Server zu Server übertragen wird. |
| [!UICONTROL Hinweis] | `note` | Array von [[!UICONTROL Anmerkung]](../../data-types/healthcare/annotation.md) | Kommentare zum Ziel. |
| [!UICONTROL Ergebnis] | `outcome` | Array von [[!UICONTROL Codeable Reference]](../../data-types/healthcare/codeable-reference.md) | Identifiziert die Änderung (oder das Fehlen von Änderungen) bei der Bewertung des Status des Ziels. |
| [!UICONTROL Priorität] | `priority` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Ermittelt den einvernehmlich vereinbarten Umfang an Bedeutung, der mit der Erreichung oder Aufrechterhaltung des Ziels verbunden ist. |
| [!UICONTROL Quelle] | `source` | [[!UICONTROL Referenz]](../../data-types/healthcare/reference.md) | Gibt die Quelle des Ziels an, z. B. den Patienten oder Praktiker. |
| [!UICONTROL  Codeable-Konzept starten] | `startCodeableConcept` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Das Ereignis, nach dem das Ziel fortgesetzt werden soll. |
| [!UICONTROL  Betreff |]`subject` | [[!UICONTROL Referenz]](../../data-types/healthcare/reference.md) | Identifiziert den Patienten, die Gruppe oder die Organisation, für die das Ziel festgelegt wird. |
| [!UICONTROL Zielgruppe] | `target` | Array von Objekten | Gibt die Zeitleiste bestimmter Schritte im Ziel an. Weitere Informationen finden Sie im Abschnitt [unter ](#target) . |
| [!UICONTROL Weiter] | `continous` | Boolesch | Gibt an, ob nach Erreichen des Ziels eine laufende Aktivität erforderlich ist, um das Ziel zu erreichen. |
| [!UICONTROL Lebenszyklusstatus] | `lifecycleStatus` | String | Der Status des Lebenszyklus des Ziels. Der Wert dieser Eigenschaft muss mit einem der folgenden bekannten Enum-Werte übereinstimmen. <li> `proposed` </li> <li> `planned` </li> <li> `accepted` </li> <li> `active` </li> <li> `on-hold` </li> <li> `completed` </li> <li> `cancelled` </li> <li> `entered-in-error` </li> <li> `rejected` </li> |
| [!UICONTROL Startdatum] | `startDate` | Datum | Das Datum, nach dem das Ziel erreicht werden soll. |
| [!UICONTROL Statusdatum] | `statusDate` | Datum | Gibt an, wann der Status erstellt wurde. |
| [!UICONTROL Statusgrund] | `statusReason` | String | Erfasst den Grund für den aktuellen Status. |

Weitere Informationen zur Feldergruppe finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/goal.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/goal.example.1.json)

## `target` {#target}

`target` wird als Array von Objekten bereitgestellt. Die Struktur der einzelnen Objekte wird nachfolgend beschrieben.

![Zielstruktur](../../images/field-groups/healthcare-goal/target.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL Detail-Codeable-Konzept] | `detailCodeableConcept` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Der Zielcode, der erreicht werden soll, um die Erfüllung des Ziels zu kennzeichnen. |
| [!UICONTROL Detailmenge] | `detailQuantity` | [[!UICONTROL Quantity]](../../data-types/healthcare/quantity.md) | Die Zielmenge, die erreicht werden soll, um die Erreichung des Ziels zu kennzeichnen. |
| [!UICONTROL Detailbereich] | `detailRange` | [[!UICONTROL Bereich]](../../data-types/healthcare/range.md) | Der Zielbereich, der erreicht werden soll, um die Erreichung des Ziels zu kennzeichnen. |
| [!UICONTROL Detailverhältnis] | `detailRatio` | [[!UICONTROL Verhältnis]](../../data-types/healthcare/ratio.md) | Das zu erreichende Zielverhältnis zur Erreichung des Ziels. |
| [!UICONTROL Maßnahme] | `measure` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Der -Parameter, der den Wert enthält, wird verfolgt. |
| [!UICONTROL Detail Boolean] | `detailBoolean` | Boolesch | Gibt die Erfüllung des Ziels an. |
| [!UICONTROL Detail Integer] | `detailInteger` | Ganzzahl | Die Zielzahl, die erreicht werden soll, um die Erreichung des Ziels zu kennzeichnen. |
| [!UICONTROL Detailzeichenfolge] | `detailString` | String | Der Zielwert, der erreicht werden soll, um die Erreichung des Ziels zu kennzeichnen. |
| [!UICONTROL Fälligkeitsdatum] | `dueDate` | Datum | Das Datum, bis zu dem die Zielgruppe erreicht werden soll. |
