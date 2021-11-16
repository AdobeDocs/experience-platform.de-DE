---
title: XDM Business Campaign-Mitgliederklasse
description: Dieses Dokument bietet einen Überblick über die XDM Business Campaign Members-Klasse im Experience-Datenmodell (XDM).
exl-id: a39eac7d-46ee-4e9c-a1c0-4dbb63f2c813
source-git-commit: 8718512a9768158183b9fb6b9e336081e47cd889
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 4%

---

# [!UICONTROL XDM Business Campaign-Mitglieder] class

>[!IMPORTANT]
>
>Diese Klasse ist für Organisationen mit Zugriff auf [Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Sie müssen Zugriff auf die Echtzeit-CDP B2B Edition haben, damit diese Klasse an [Echtzeit-Kundenprofil](../../../profile/home.md).

[!UICONTROL XDM Business Campaign-Mitglieder] ist eine standardmäßige Experience-Datenmodell (XDM)-Klasse, die einen Kontakt oder Lead beschreibt, der mit einer Geschäftskampagne verknüpft ist.

![](../../images/classes/b2b/business-campaign-members.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die zugehörige Kampagne. |
| `campaignMemberKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Kampagnenmitgliedschaft-Entität. |
| `extSourceSystemAudit` | [[!UICONTROL Audit-Attribute des externen Quellsystems]](../../data-types/external-source-system-audit-attributes.md) | Wenn die Kampagnenmitgliedschaft aus einem externen Quellsystem stammt, erfasst dieses Objekt Prüfattribute für dieses System. |
| `personKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Person, die Mitglied der zugehörigen Kampagne ist. |
| `_id` | Zeichenfolge | Eine eindeutige Kennung für den Datensatz. Dies ist ein systemgenerierter Wert, der getrennt vom `campaignMemberID`. |
| `campaignID` | Zeichenfolge | Eine eindeutige ID für die zugehörige Kampagne. |
| `campaignMemberID` | Zeichenfolge | Eine eindeutige ID für die Kampagnenmitgliedschaft-Entität. |
| `personId` | Zeichenfolge | Eine eindeutige ID für die Person, die Mitglied der zugehörigen Kampagne ist. |

{style=&quot;table-layout:auto&quot;}

Siehe Handbuch unter [Schemabeziehungen in der Echtzeit-Kundendatenplattform B2B Edition](../../tutorials/relationship-b2b.md) um zu erfahren, wie diese Klasse konzeptionell mit den anderen B2B-Klassen in Beziehung steht und wie Sie diese Beziehungen in der Adobe Experience Platform-Benutzeroberfläche herstellen können.
