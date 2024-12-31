---
title: Feldergruppe „Profilpartner-Anreicherung (Beispiel)“
description: Erfahren Sie mehr über die Schemafeldgruppe „Profilpartner-Anreicherung (Beispiel)“.
exl-id: 02f7c358-3cf9-45cb-a5c5-e2cb1f140d93
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 14%

---

# Schemafeldgruppe [!UICONTROL Profilpartneranreicherung (Beispiel])

[!UICONTROL Profilpartneranreicherung (Beispiel)] ist eine standardmäßige Schemafeldgruppe für die [[!DNL XDM Individual Profile] Klasse](../../classes/individual-profile.md). Verwenden Sie diese Feldergruppe, um zusätzliche Daten im Zusammenhang mit von Partnern durchgeführten Anreicherungen für Kundenprofile bereitzustellen.

![Abbildung der Feldergruppe [!UICONTROL Profilpartneranreicherung (Beispiel)].](../../images/field-groups/profile-partner-enrichment-sample.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|-----------------------------|------------------------|-----------|----------------------------------|
| [!UICONTROL ageRangeInHousehold] | `ageRangeInHousehold` | Zeichenfolge | Der Altersbereich innerhalb des Haushalts. |
| [!UICONTROL bekleidungszubehör] | `apparelAccessories` | Zeichenfolge | Bekleidungs- und Zubehördaten. |
| [!UICONTROL Radfahren] | `bicycling` | Zeichenfolge | Informationen zum Fahrradfahren. |
| [!UICONTROL KabelTV] | `cableTv` | Zeichenfolge | Informationen zu Kabelfernsehen. |
| [!UICONTROL Inland] | `domestics` | Zeichenfolge | Inlandsbezogene Daten. |
| [!UICONTROL Elektronik] | `electronics` | Zeichenfolge | Elektronik-bezogene Informationen. |
| [!UICONTROL foodAndBeverage] | `foodAndBeverage` | Zeichenfolge | In: Food and Beverage Data. |
| [!UICONTROL Schuhe] | `footwear` | Zeichenfolge | Informationen über Schuhe. |
| [!UICONTROL healthFoods] | `healthFoods` | Zeichenfolge | In: Health Foods Data. |
| [!UICONTROL Wandern] | `hiking` | Zeichenfolge | Informationen zum Wandern. |
| [!UICONTROL householdId] | `householdId` | Zeichenfolge | Die eindeutige ID für einen Haushalt. |
| [!UICONTROL individualId] | `individualId` | Zeichenfolge | Die eindeutige ID für eine Person. |
| [!UICONTROL inferredCardHolder] | `inferredCardHolder` | Zeichenfolge | Abgeleitete Karteninhaberinformationen. |
| [!UICONTROL inferredPremiumCardHolder] | `inferredPremiumCardholder` | Zeichenfolge | Abgeleitete Premium-Karteninhaberdetails. |
| [!UICONTROL matchLevelFlag] | `matchLevelFlag` | Zeichenfolge | Flag-Daten auf Übereinstimmungsebene. |
| [!UICONTROL BuyerRating] | `buyerRating` | Zeichenfolge | Informationen zur Kaufbewertung. |
| [!UICONTROL DonorRating] | `donorRating` | Zeichenfolge | Details zur Spenderbewertung. |
| [!UICONTROL InvestmentRating] | `investmentRating` | Zeichenfolge | Anlagebewertungsdaten. |
| [!UICONTROL ResponderRating] | `responderRating` | Zeichenfolge | Informationen zur Responder-Bewertung. |
| [!UICONTROL SpendingVelocity] | `spendingVelocity` | Zeichenfolge | Details zur Ausgabengeschwindigkeit. |
| [!UICONTROL Ausgabenvolumen] | `spendingVolume` | Zeichenfolge | Informationen zum Ausgabenvolumen. |
| [!UICONTROL recordId] | `recordId` | Zeichenfolge | Eindeutige Eintragskennung. |
| [!UICONTROL residenceId] | `residenceId` | Zeichenfolge | Eindeutige ID für den Wohnsitz. |
| [!UICONTROL Segeln] | `sailing` | Zeichenfolge | Segelbezogene Daten. |
| [!UICONTROL seasonHolidayProducts] | `seasonalHolidayProducts` | Zeichenfolge | Produktinformationen zu saisonalen Feiertagen. |
| [!UICONTROL Skifahren] | `skiing` | Zeichenfolge | Daten zum Skifahren. |
| [!UICONTROL Tennis] | `tennis` | Zeichenfolge | Informationen zum Tennis. |
| [!UICONTROL tvShoppers] | `tvShoppers` | Zeichenfolge | In: TV Shoppers&#39; information. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie unter [vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/partner-profile-enrichment/profile-partner-enrichment-sample.schema.json) im öffentlichen XDM-Repository.
