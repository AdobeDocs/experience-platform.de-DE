---
title: Schemafeldgruppe „Angebotsanfragedetails“
description: Erfahren Sie mehr über die Schemafeldgruppe „Angebotsanfrage-Details“.
exl-id: 19be76fa-d212-4b00-815a-d3869c1054e2
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 6%

---

# Schemafeldgruppe [!UICONTROL Details ] Angebotsanfrage“

[!UICONTROL Details zur Angebotsanfrage] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] Klasse](../../classes/experienceevent.md). Die Feldergruppe stellt ein einzelnes `quotes` für ein Schema bereit, das die Anfrageprozessdetails für verschiedene Angebotstypen erfasst, einschließlich Versicherungspolicen, Gesundheitswesen, Fertigungsaufträge und High-Tech-Bestellungen.

![](../../images/field-groups/quote-request-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `discount` | [[!UICONTROL Währung]](../../data-types/currency.md) | Der Rabattbetrag für ein Angebot, der einem Besucher angezeigt wird. |
| `premium` | [[!UICONTROL Währung]](../../data-types/currency.md) | Der Prämienbetrag für ein Angebot, das einem Besucher angezeigt wird. |
| `location` | [!UICONTROL String] | Die Postleitzahl, die verwendet wird, um Einzelhändler in der Nähe des Standorts des Besuchers zu finden. |
| `requestID` | [!UICONTROL String] | Eine eindeutige Kennung für die Angebotsanfrage. |
| `selectedRetailer` | [!UICONTROL String] | Der für die Angebotsanfrage ausgewählte Händler, falls zutreffend. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie unter [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-quote-request-details.schema.json).
