---
title: Feldergruppe "Details der Partnervorschau"(Beispiel)
description: Erfahren Sie mehr über die Feldergruppe "Partner Prospect Details"(Beispiel) mit XDM-Schemafeldern.
exl-id: 2de1eb7a-2e44-4417-9bdd-7a8a4b2d3a7f
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 11%

---

# Feldergruppe [!UICONTROL Partner-Interessensdetails (Beispiel)]

[!UICONTROL Partner Prospect Details (Beispiel)] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] Klasse](../../classes/experienceevent.md). Die [!UICONTROL Partner Prospect Details (Beispiel)] bietet ein Beispiel-Framework für verschiedene Details im Zusammenhang mit dem Profil eines Interessenten. Dieses Framework optimiert den Prozess der Organisation und Verwaltung verschiedener prospektbezogener Informationen.

Diese Feldergruppe erweitert die [Individual Prospect Profile class](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/prospect.html) im Kontext eines Partners.

![Ein Diagramm der Feldergruppe [!UICONTROL Partner-Interessensdetails (Beispiel)].](../../images/field-groups/partner/partner-prospect-details-sample.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|---------------------------------------|-----------------------------|-----------|--------------------------------------------------|
| [!UICONTROL ageRangeInHousbudget] | `ageRangeInHousehold` | Zeichenfolge | Altersgruppe im Haushalt. |
| [!UICONTROL apparelAccessoires] | `apparelAccessories` | Zeichenfolge | Voreinstellungen oder Einbeziehung in Bekleidung/Zubehör. |
| [!UICONTROL Fahrrad] | `bicycling` | Zeichenfolge | Interesse oder Beteiligung an Fahrradaktivitäten. |
| [!UICONTROL kabelTv] | `cableTv` | Zeichenfolge | Gibt die Interaktion mit Kabelfernsehen an. |
| [!UICONTROL domestics] | `domestics` | Zeichenfolge | Präferenzen oder Interaktion bei inländischen Aktivitäten. |
| [!UICONTROL electronics] | `electronics` | Zeichenfolge | Interesse oder Interaktion mit elektronischen Geräten. |
| [!UICONTROL foodAndBeverage] | `foodAndBeverage` | Zeichenfolge | Präferenzen oder Beteiligung an Lebensmitteln/Getränken. |
| [!UICONTROL Schuhe] | `footwear` | Zeichenfolge | Interesse oder Beteiligung an Schuhen. |
| [!UICONTROL healthFoods] | `healthFoods` | Zeichenfolge | Präferenzen oder Einbeziehung in gesundheitsfördernde Lebensmittel. |
| [!UICONTROL wandern] | `hiking` | Zeichenfolge | Interesse oder Beteiligung an Wanderaktivitäten. |
| [!UICONTROL budgetId] | `householdId` | Zeichenfolge | Eine eindeutige Kennung für den Haushalt. |
| [!UICONTROL einzelnId] | `individualId` | Zeichenfolge | Eine eindeutige Kennung für die Person. |
| [!UICONTROL inferredCardHolder] | `inferredCardHolder` | Zeichenfolge | Der Eindruck, ein Karteninhaber zu sein. |
| [!UICONTROL inferredPremiumCardholder] | `inferredPremiumCardholder]` | Zeichenfolge | Der Eindruck, ein Prämienkarteninhaber zu sein. |
| [!UICONTROL matchLevelFlag] | `matchLevelFlag` | Zeichenfolge | Ein Indikator für die entsprechende Ebene. |
| [!UICONTROL BuyerRating] | `buyerRating` | Zeichenfolge | Eine Bewertung im Zusammenhang mit dem Kaufverhalten. |
| [!UICONTROL DonorRating] | `donorRating` | Zeichenfolge | Eine Bewertung im Zusammenhang mit dem Geberverhalten. |
| [!UICONTROL InvestmentRating] | `investmentRating` | Zeichenfolge | Ein Rating im Zusammenhang mit dem Anlageverhalten. |
| [!UICONTROL ResponderRating] | `responderRating` | Zeichenfolge | Eine Bewertung bezüglich des Reaktionsverhaltens. |
| [!UICONTROL SpendingVelocity] | `spendingVelocity` | Zeichenfolge | Die Geschwindigkeit oder Rate der Ausgaben. |
| [!UICONTROL SpendingVolume] | `spendingVolume` | Zeichenfolge | Höhe oder Umfang der Ausgaben. |
| [!UICONTROL recordId] | `recordId` | Zeichenfolge | Eine eindeutige Kennung für den Datensatz. |
| [!UICONTROL residenceId] | `residenceId` | Zeichenfolge | Eine eindeutige Kennung für den Wohnsitz. |
| [!UICONTROL sailing] | `sailing` | Zeichenfolge | Gibt das Interesse oder die Beteiligung an Segelaktivitäten an. |
| [!UICONTROL seasonHolidayProducts] | `seasonalHolidayProducts` | Zeichenfolge | Gibt die Voreinstellungen oder die Beteiligung an Weihnachtsprodukten an. |
| [!UICONTROL  skiing] | `skiing` | Zeichenfolge | Gibt das Interesse oder die Beteiligung an Skiaktivitäten an. |
| [!UICONTROL tennis] | `tennis` | Zeichenfolge | Gibt das Interesse oder die Beteiligung an Tennisaktivitäten an. |
| [!UICONTROL tvShoppers] | `tvShoppers` | Zeichenfolge | Zeigt die Interaktion mit dem TV-Einkauf an. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im [vollständigen Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/partner-prospect/merkle/prospect-details-partner-sample.schema.json) des öffentlichen XDM-Repositorys.
