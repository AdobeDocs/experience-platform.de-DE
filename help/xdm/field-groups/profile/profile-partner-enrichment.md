---
title: Feldergruppe "Profilpartner-Anreicherung"(Beispiel)
description: Erfahren Sie mehr über die Schemafeldgruppe Profilpartner-Anreicherung (Beispiel) .
exl-id: 02f7c358-3cf9-45cb-a5c5-e2cb1f140d93
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 14%

---

# [!UICONTROL Profil-Partner-Anreicherung (Beispiel)] Schemafeldgruppe

[!UICONTROL Profil-Partner-Anreicherung (Beispiel)] ist eine Standardschemafeldgruppe für die [[!DNL XDM Individual Profile] Klasse](../../classes/individual-profile.md). Verwenden Sie diese Feldergruppe, um zusätzliche Daten im Zusammenhang mit Partner-gesteuerten Anreicherungen für Kundenprofile bereitzustellen.

![Ein Diagramm der Feldergruppe [!UICONTROL Profil-Partner-Anreicherung (Beispiel)].](../../images/field-groups/profile-partner-enrichment-sample.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|-----------------------------|------------------------|-----------|----------------------------------|
| [!UICONTROL ageRangeInHousbudget] | `ageRangeInHousehold` | Zeichenfolge | Die Altersgruppe im Haushalt. |
| [!UICONTROL apparelAccessoires] | `apparelAccessories` | Zeichenfolge | Daten zu Bekleidung und Zubehör. |
| [!UICONTROL Fahrrad] | `bicycling` | Zeichenfolge | Fahrradbezogene Informationen. |
| [!UICONTROL kabelTv] | `cableTv` | Zeichenfolge | Informationen zum Kabelfernsehen. |
| [!UICONTROL domestics] | `domestics` | Zeichenfolge | Interne Daten. |
| [!UICONTROL electronics] | `electronics` | Zeichenfolge | Elektronische Informationen. |
| [!UICONTROL foodAndBeverage] | `foodAndBeverage` | Zeichenfolge | Daten zu Lebensmitteln und Getränken. |
| [!UICONTROL Schuhe] | `footwear` | Zeichenfolge | Informationen zu Schuhen. |
| [!UICONTROL healthFoods] | `healthFoods` | Zeichenfolge | Daten zu gesundheitlichen Lebensmitteln. |
| [!UICONTROL wandern] | `hiking` | Zeichenfolge | Informationen zum Wandern. |
| [!UICONTROL budgetId] | `householdId` | Zeichenfolge | Die eindeutige ID für einen Haushalt. |
| [!UICONTROL einzelnId] | `individualId` | Zeichenfolge | Die eindeutige ID für eine Person. |
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
| [!UICONTROL sailing] | `sailing` | Zeichenfolge | Sailing-bezogene Daten. |
| [!UICONTROL seasonHolidayProducts] | `seasonalHolidayProducts` | Zeichenfolge | Produktinformationen zu saisonalen Feiertagen. |
| [!UICONTROL  skiing] | `skiing` | Zeichenfolge | Skiing-bezogene Daten. |
| [!UICONTROL tennis] | `tennis` | Zeichenfolge | Tennisbezogene Informationen. |
| [!UICONTROL tvShoppers] | `tvShoppers` | Zeichenfolge | Informationen der Fernsehkäufer. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im [vollständigen Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/partner-profile-enrichment/profile-partner-enrichment-sample.schema.json) des öffentlichen XDM-Repositorys.
