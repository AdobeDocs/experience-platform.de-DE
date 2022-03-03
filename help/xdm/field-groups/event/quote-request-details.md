---
title: Feldergruppe "Anfragedetails"
description: Dieses Dokument bietet einen Überblick über die Feldergruppe Anführungsanforderungsdetails .
source-git-commit: 32d8798d426696d8fd4ace4c53a8bf9b4db26b61
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 8%

---

# [!UICONTROL Anführungsanfragedetails] Schemafeldgruppe

[!UICONTROL Anführungsanfragedetails] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Die Feldergruppe stellt eine `quotes` -Objekt auf ein Schema verweist, das die Details des Anfrageprozesses für verschiedene Arten von Anführungszeichen erfasst, einschließlich Versicherungspolicen, Gesundheitsversorgung, Fertigungsaufträge und High-Tech-Bestellungen.

![](../../images/field-groups/quote-request-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `discount` | [[!UICONTROL Währung]](../../data-types/currency.md) | Der Rabattbetrag für ein Angebot, das einem Besucher angezeigt wird. |
| `premium` | [[!UICONTROL Währung]](../../data-types/currency.md) | Der Premium-Betrag für ein Angebot, das einem Besucher angezeigt wird. |
| `location` | [!UICONTROL Zeichenfolge] | Die Postleitzahl, die verwendet wird, um Einzelhändler in der Nähe des Besucherorts zu finden. |
| `requestID` | [!UICONTROL Zeichenfolge] | Eine eindeutige Kennung für die Anführungsanforderung. |
| `selectedRetailer` | [!UICONTROL Zeichenfolge] | Der ausgewählte Händler für die Angebotsanforderung, falls zutreffend. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zur Feldergruppe finden Sie im Abschnitt [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-quote-request-details.schema.json).
