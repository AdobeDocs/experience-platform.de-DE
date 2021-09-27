---
title: XDM Business Campaign-Mitgliederklasse
description: Dieses Dokument bietet einen Überblick über die XDM Business Campaign Members-Klasse im Experience-Datenmodell (XDM).
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 4%

---

# [!UICONTROL XDM Business Campaign ] Membersclass

>[!NOTE]
>
>Diese Klasse ist nur für Unternehmen verfügbar, die Zugriff auf die B2B-Edition der Echtzeit-Kundendatenplattform haben.

[!UICONTROL XDM Business Campaign ] Membersis ist eine standardmäßige XDM-Klasse (Experience-Datenmodell), die einen Kontakt oder einen Lead beschreibt, der mit einer Geschäftskampagne verknüpft ist.

![](../../images/classes/b2b/business-campaign-members.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die zugehörige Kampagne. |
| `campaignMemberKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Kampagnenmitgliedschaft-Entität. |
| `extSourceSystemAudit` | [[!UICONTROL Audit-Attribute des externen Quellsystems]](../../data-types/external-source-system-audit-attributes.md) | Wenn die Kampagnenmitgliedschaft aus einem externen Quellsystem stammt, erfasst dieses Objekt Prüfattribute für dieses System. |
| `personKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Person, die Mitglied der zugehörigen Kampagne ist. |
| `_id` | Zeichenfolge | Eine eindeutige Kennung für den Datensatz. Dies ist ein systemgenerierter Wert, der von `campaignMemberID` getrennt ist. |
| `campaignID` | Zeichenfolge | Eine eindeutige ID für die zugehörige Kampagne. |
| `campaignMemberID` | Zeichenfolge | Eine eindeutige ID für die Kampagnenmitgliedschaft-Entität. |
| `personId` | Zeichenfolge | Eine eindeutige ID für die Person, die Mitglied der zugehörigen Kampagne ist. |
