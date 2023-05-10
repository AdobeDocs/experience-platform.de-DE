---
title: Feldergruppe "Anfragedetails"
description: Dieses Dokument bietet einen Überblick über die Feldergruppe Anführungsanforderungsdetails .
exl-id: 19be76fa-d212-4b00-815a-d3869c1054e2
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 6%

---

# [!UICONTROL Anführungsanfragedetails] Schemafeldgruppe

[!UICONTROL Anführungsanfragedetails] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Die Feldergruppe stellt eine `quotes` -Objekt auf ein Schema verweist, das die Details des Anfrageprozesses für verschiedene Arten von Anführungszeichen erfasst, einschließlich Versicherungspolicen, Gesundheitsversorgung, Fertigungsaufträge und High-Tech-Bestellungen.

![](../../images/field-groups/quote-request-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `discount` | [[!UICONTROL Währung]](../../data-types/currency.md) | Der Rabattbetrag für ein Angebot, das einem Besucher angezeigt wird. |
| `premium` | [[!UICONTROL Währung]](../../data-types/currency.md) | Der Premium-Betrag für ein Angebot, das einem Besucher angezeigt wird. |
| `location` | [!UICONTROL String] | Die Postleitzahl, die verwendet wird, um Einzelhändler in der Nähe des Besucherorts zu finden. |
| `requestID` | [!UICONTROL String] | Eine eindeutige Kennung für die Anführungsanforderung. |
| `selectedRetailer` | [!UICONTROL String] | Der ausgewählte Händler für die Angebotsanforderung, falls zutreffend. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im Abschnitt [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-quote-request-details.schema.json).
