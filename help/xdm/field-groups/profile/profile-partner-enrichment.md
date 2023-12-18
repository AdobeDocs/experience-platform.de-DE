---
title: Feldergruppe "Profilpartner-Anreicherung"(Beispiel)
description: Erfahren Sie mehr über die Schemafeldgruppe Profilpartner-Anreicherung (Beispiel) .
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 14%

---


# [!UICONTROL Profilpartner-Anreicherung (Beispiel)] Schemafeldgruppe

[!UICONTROL Profilpartner-Anreicherung (Beispiel)] ist eine Standardschemafeldgruppe für die [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md). Verwenden Sie diese Feldergruppe, um zusätzliche Daten im Zusammenhang mit Partner-gesteuerten Anreicherungen für Kundenprofile bereitzustellen.

![Ein Diagramm des [!UICONTROL Profilpartner-Anreicherung (Beispiel)] Feldergruppe.](../../images/field-groups/profile-partner-enrichment-sample.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|-----------------------------|------------------------|-----------|----------------------------------|
| [!UICONTROL ageRangeInHousbudget] | `ageRangeInHousehold` | Zeichenfolge | Die Altersgruppe im Haushalt. |
| [!UICONTROL apparelZubehör] | `apparelAccessories` | Zeichenfolge | Daten zu Bekleidung und Zubehör. |
| [!UICONTROL Radfahren] | `bicycling` | Zeichenfolge | Fahrradbezogene Informationen. |
| [!UICONTROL kabelTv] | `cableTv` | Zeichenfolge | Informationen zum Kabelfernsehen. |
| [!UICONTROL Domänen] | `domestics` | Zeichenfolge | Interne Daten. |
| [!UICONTROL Elektronik] | `electronics` | Zeichenfolge | Elektronische Informationen. |
| [!UICONTROL foodAndBeverage] | `foodAndBeverage` | Zeichenfolge | Daten zu Lebensmitteln und Getränken. |
| [!UICONTROL Schuhe] | `footwear` | Zeichenfolge | Informationen zu Schuhen. |
| [!UICONTROL healthFoods] | `healthFoods` | Zeichenfolge | Daten zu gesundheitlichen Lebensmitteln. |
| [!UICONTROL Wandern] | `hiking` | Zeichenfolge | Informationen zum Wandern. |
| [!UICONTROL budgetId] | `householdId` | Zeichenfolge | Die eindeutige ID für einen Haushalt. |
| [!UICONTROL uniqueId] | `individualId` | Zeichenfolge | Die eindeutige ID für eine Person. |
| [!UICONTROL inferredCardHolder] | `inferredCardHolder` | Zeichenfolge | Abgeleitete Angaben zum Karteninhaber. |
| [!UICONTROL inferredPremiumCardholder] | `inferredPremiumCardholder` | Zeichenfolge | Angaben zu den Inhabern der Prämienbescheinigung. |
| [!UICONTROL matchLevelFlag] | `matchLevelFlag` | Zeichenfolge | Kennzeichnungs-Daten der Übereinstimmungsebene. |
| [!UICONTROL BuyerRating] | `buyerRating` | Zeichenfolge | Informationen zur Bestellbewertung. |
| [!UICONTROL DonorRating] | `donorRating` | Zeichenfolge | Angaben zur Geberbewertung. |
| [!UICONTROL InvestmentRating] | `investmentRating` | Zeichenfolge | Daten zur Anlagebewertung. |
| [!UICONTROL ResponderRating] | `responderRating` | Zeichenfolge | Informationen zur Antwortenbewertung. |
| [!UICONTROL SpendingVelocity] | `spendingVelocity` | Zeichenfolge | Details zur Ausgabedarstellungsgeschwindigkeit. |
| [!UICONTROL SpendingVolume] | `spendingVolume` | Zeichenfolge | Ausgabenvolumeninformationen. |
| [!UICONTROL recordId] | `recordId` | Zeichenfolge | Eindeutige Datensatz-ID. |
| [!UICONTROL residenceId] | `residenceId` | Zeichenfolge | Eindeutige Kennung für den Aufenthalt. |
| [!UICONTROL Segeln] | `sailing` | Zeichenfolge | Sailing-bezogene Daten. |
| [!UICONTROL seasonHolidayProducts] | `seasonalHolidayProducts` | Zeichenfolge | Produktinformationen zu saisonalen Feiertagen. |
| [!UICONTROL Skifahren] | `skiing` | Zeichenfolge | Skiing-bezogene Daten. |
| [!UICONTROL Tennis] | `tennis` | Zeichenfolge | Tennisbezogene Informationen. |
| [!UICONTROL tvShoppers] | `tvShoppers` | Zeichenfolge | Informationen der Fernsehkäufer. |

{style="table-layout:auto"}

Weiterführende Informationen zur Feldergruppe finden Sie im Abschnitt [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/partner-profile-enrichment/profile-partner-enrichment-sample.schema.json) im öffentlichen XDM-Repository.
