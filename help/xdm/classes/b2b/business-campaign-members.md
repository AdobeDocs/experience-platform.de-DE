---
title: XDM Business Campaign-Mitgliederklasse
description: Dieses Dokument bietet einen Überblick über die XDM Business Campaign Members-Klasse im Experience-Datenmodell (XDM).
exl-id: a39eac7d-46ee-4e9c-a1c0-4dbb63f2c813
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 8%

---

# [!UICONTROL XDM Business Campaign ] Membersclass (Beta)

>[!IMPORTANT]
>
>Diese Klasse ist als Teil der Real-time Customer Data Platform B2B Edition verfügbar, die sich derzeit in der Beta-Phase befindet. Dokumentation und Funktionalität können sich ändern.

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

{style=&quot;table-layout:auto&quot;}

Informationen dazu, wie diese Klasse konzeptionell mit anderen B2B-Klassen in Beziehung steht und wie Sie diese Beziehungen in der Adobe Experience Platform-Benutzeroberfläche herstellen können, finden Sie im Handbuch zu [Schemabeziehungen in der Echtzeit-Kundendatenplattform B2B Edition](../../tutorials/relationship-b2b.md).
