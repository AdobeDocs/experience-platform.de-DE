---
title: Feldergruppe „Interessentendetails für Partner“ (Beispiel)
description: Erfahren Sie mehr über die Schemafeldgruppe „Partner Prospect Details (Sample) Field Group (XDM)“.
exl-id: 2de1eb7a-2e44-4417-9bdd-7a8a4b2d3a7f
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 11%

---

# [!UICONTROL Details zum Interessenten des Partners (Beispiel] Feldergruppe

[!UICONTROL Partner Prospect Details (Beispiel)] ist eine standardmäßige Schemafeldgruppe für die [[!DNL XDM ExperienceEvent] Klasse](../../classes/experienceevent.md). Der [!UICONTROL Partner-Interessentendetails (Beispiel)] bietet ein Beispiel-Framework für verschiedene Details, die sich auf das Profil eines Interessenten beziehen. Dieses Framework optimiert den Prozess der Organisation und Verwaltung verschiedener Informationen zu Interessenten.

Diese Feldergruppe erweitert die Klasse [Individuelles Interessentenprofil](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/prospect.html?lang=de) im Kontext eines Partners.

![Abbildung der Feldergruppe &quot;[!UICONTROL &#x200B; Interessentendetails (Beispiel)].](../../images/field-groups/partner/partner-prospect-details-sample.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|---------------------------------------|-----------------------------|-----------|--------------------------------------------------|
| [!UICONTROL ageRangeInHousehold] | `ageRangeInHousehold` | Zeichenfolge | Altersspanne im Haushalt. |
| [!UICONTROL bekleidungszubehör] | `apparelAccessories` | Zeichenfolge | Präferenzen oder Beteiligung an Bekleidung/Accessoires. |
| [!UICONTROL Radfahren] | `bicycling` | Zeichenfolge | Interesse oder Beteiligung an Radfahraktivitäten. |
| [!UICONTROL KabelTV] | `cableTv` | Zeichenfolge | Zeigt Interaktion mit Kabelfernsehen an. |
| [!UICONTROL Inland] | `domestics` | Zeichenfolge | Präferenzen oder Beteiligung an inländischen Tätigkeiten. |
| [!UICONTROL Elektronik] | `electronics` | Zeichenfolge | Interesse oder Engagement in elektronischen Geräten. |
| [!UICONTROL foodAndBeverage] | `foodAndBeverage` | Zeichenfolge | Präferenzen oder Beteiligung an Lebensmitteln/Getränken. |
| [!UICONTROL Schuhe] | `footwear` | Zeichenfolge | Interesse oder Beteiligung an Schuhen. |
| [!UICONTROL healthFoods] | `healthFoods` | Zeichenfolge | Präferenzen oder Beteiligung an gesunden Lebensmitteln. |
| [!UICONTROL Wandern] | `hiking` | Zeichenfolge | Interesse oder Beteiligung an Wanderaktivitäten. |
| [!UICONTROL householdId] | `householdId` | Zeichenfolge | Eine eindeutige Kennung für den Haushalt. |
| [!UICONTROL individualId] | `individualId` | Zeichenfolge | Eine eindeutige Kennung für den Kontakt. |
| [!UICONTROL inferredCardHolder] | `inferredCardHolder` | Zeichenfolge | Die Schlussfolgerung, ein Karteninhaber zu sein. |
| [!UICONTROL inferredPremiumCardHolder] | `inferredPremiumCardholder]` | Zeichenfolge | Die Schlussfolgerung, ein Premium-Karteninhaber zu sein. |
| [!UICONTROL matchLevelFlag] | `matchLevelFlag` | Zeichenfolge | Ein Indikator für die Übereinstimmungsebene. |
| [!UICONTROL BuyerRating] | `buyerRating` | Zeichenfolge | Eine Bewertung im Zusammenhang mit dem Kaufverhalten. |
| [!UICONTROL DonorRating] | `donorRating` | Zeichenfolge | Eine Bewertung im Zusammenhang mit dem Spenderverhalten. |
| [!UICONTROL InvestmentRating] | `investmentRating` | Zeichenfolge | Ein Rating in Bezug auf das Anlageverhalten. |
| [!UICONTROL ResponderRating] | `responderRating` | Zeichenfolge | Eine Bewertung im Zusammenhang mit dem Verhalten der Antwortenden. |
| [!UICONTROL SpendingVelocity] | `spendingVelocity` | Zeichenfolge | Die Geschwindigkeit oder die Rate der Ausgaben. |
| [!UICONTROL Ausgabenvolumen] | `spendingVolume` | Zeichenfolge | Höhe oder Volumen der Ausgaben. |
| [!UICONTROL recordId] | `recordId` | Zeichenfolge | Eine eindeutige Kennung für den Datensatz. |
| [!UICONTROL residenceId] | `residenceId` | Zeichenfolge | Eine eindeutige Kennung für die Residenz. |
| [!UICONTROL Segeln] | `sailing` | Zeichenfolge | Zeigt das Interesse oder die Beteiligung an Segelaktivitäten an. |
| [!UICONTROL seasonHolidayProducts] | `seasonalHolidayProducts` | Zeichenfolge | Gibt die Präferenzen oder die Beteiligung an Ferienprodukten an. |
| [!UICONTROL Skifahren] | `skiing` | Zeichenfolge | Zeigt das Interesse oder die Beteiligung an Skiaktivitäten. |
| [!UICONTROL Tennis] | `tennis` | Zeichenfolge | Zeigt das Interesse oder die Beteiligung an Tennisaktivitäten an. |
| [!UICONTROL tvShoppers] | `tvShoppers` | Zeichenfolge | Zeigt Interaktion mit TV-Shopping an. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie unter [vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/partner-prospect/merkle/prospect-details-partner-sample.schema.json) im öffentlichen XDM-Repository.
