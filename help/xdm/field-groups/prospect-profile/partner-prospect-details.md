---
title: Feldergruppe "Details der Partnervorschau"(Beispiel)
description: Erfahren Sie mehr über die Feldergruppe "Partner Prospect Details"(Beispiel) mit XDM-Schemafeldern.
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 9%

---

# [!UICONTROL Details zur Partnervorschau (Beispiel)] Feldergruppe

[!UICONTROL Details zur Partnervorschau (Beispiel)] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Die [!UICONTROL Details zur Partnervorschau (Beispiel)] bietet ein Beispiel-Framework für verschiedene Details im Zusammenhang mit dem Profil eines Interessenten. Dieses Framework optimiert den Prozess der Organisation und Verwaltung verschiedener prospektbezogener Informationen.

Diese Feldergruppe erweitert die [Individuelle Prospect-Profilklasse](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/prospect.html) im Kontext eines Partners.

![Ein Diagramm des [!UICONTROL Details zur Partnervorschau (Beispiel)] Feldergruppe.](../../images/field-groups/partner/partner-prospect-details-sample.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|---------------------------------------|-----------------------------|-----------|--------------------------------------------------|
| [!UICONTROL ageRangeInHousbudget] | `ageRangeInHousehold` | Zeichenfolge | Altersgruppe im Haushalt. |
| [!UICONTROL apparelZubehör] | `apparelAccessories` | Zeichenfolge | Voreinstellungen oder Einbeziehung in Bekleidung/Zubehör. |
| [!UICONTROL Radfahren] | `bicycling` | Zeichenfolge | Interesse oder Beteiligung an Fahrradaktivitäten. |
| [!UICONTROL kabelTv] | `cableTv` | Zeichenfolge | Gibt die Interaktion mit Kabelfernsehen an. |
| [!UICONTROL Domänen] | `domestics` | Zeichenfolge | Präferenzen oder Interaktion bei inländischen Aktivitäten. |
| [!UICONTROL Elektronik] | `electronics` | Zeichenfolge | Interesse oder Interaktion mit elektronischen Geräten. |
| [!UICONTROL foodAndBeverage] | `foodAndBeverage` | Zeichenfolge | Präferenzen oder Beteiligung an Lebensmitteln/Getränken. |
| [!UICONTROL Schuhe] | `footwear` | Zeichenfolge | Interesse oder Beteiligung an Schuhen. |
| [!UICONTROL healthFoods] | `healthFoods` | Zeichenfolge | Präferenzen oder Einbeziehung in gesundheitsfördernde Lebensmittel. |
| [!UICONTROL Wandern] | `hiking` | Zeichenfolge | Interesse oder Beteiligung an Wanderaktivitäten. |
| [!UICONTROL budgetId] | `householdId` | Zeichenfolge | Eine eindeutige Kennung für den Haushalt. |
| [!UICONTROL uniqueId] | `individualId` | Zeichenfolge | Eine eindeutige Kennung für die Person. |
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
| [!UICONTROL Segeln] | `sailing` | Zeichenfolge | Gibt das Interesse oder die Beteiligung an Segelaktivitäten an. |
| [!UICONTROL seasonHolidayProducts] | `seasonalHolidayProducts` | Zeichenfolge | Gibt die Voreinstellungen oder die Beteiligung an Weihnachtsprodukten an. |
| [!UICONTROL Skifahren] | `skiing` | Zeichenfolge | Gibt das Interesse oder die Beteiligung an Skiaktivitäten an. |
| [!UICONTROL Tennis] | `tennis` | Zeichenfolge | Gibt das Interesse oder die Beteiligung an Tennisaktivitäten an. |
| [!UICONTROL tvShoppers] | `tvShoppers` | Zeichenfolge | Zeigt die Interaktion mit dem TV-Einkauf an. |

{style="table-layout:auto"}

Weiterführende Informationen zur Feldergruppe finden Sie im Abschnitt [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/partner-prospect/merkle/prospect-details-partner-sample.schema.json) im öffentlichen XDM-Repository.
