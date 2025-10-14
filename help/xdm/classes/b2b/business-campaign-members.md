---
title: XDM Business Campaign Members-Klasse
description: Erfahren Sie mehr über die Klasse XDM Business Campaign Members im Experience-Datenmodell (XDM).
exl-id: a39eac7d-46ee-4e9c-a1c0-4dbb63f2c813
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 2%

---

# [!UICONTROL XDM Business Campaign Members]-Klasse

>[!IMPORTANT]
>
>Diese Klasse ist für die Verwendung durch Organisationen vorgesehen, die Zugriff auf [Adobe Real-time Customer Data Platform B2B edition](../../../rtcdp/b2b-overview.md) haben. Sie müssen Zugriff auf Real-Time CDP B2B edition haben, damit diese Klasse am Echtzeit[Kundenprofil teilnehmen &#x200B;](../../../profile/home.md).

[!UICONTROL XDM Business Campaign Members] ist eine standardmäßige Klasse des Experience-Datenmodells (XDM), das einen Kontakt oder Lead beschreibt, der einer Unternehmenskampagne zugeordnet ist.

![Die Struktur der Klasse XDM Business Campaign Members , wie sie in der Benutzeroberfläche angezeigt wird](../../images/classes/b2b/business-campaign-members.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B-Source]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die zugehörige Kampagne. |
| `campaignMemberKey` | [[!UICONTROL B2B-Source]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Entität der Kampagnenmitgliedschaft. |
| `extSourceSystemAudit` | [[!UICONTROL Audit-Attribute des externen Source-Systems]](../../data-types/external-source-system-audit-attributes.md) | Wenn die Kampagnenmitgliedschaft von einem externen Quellsystem stammt, erfasst dieses Objekt Audit-Attribute für dieses System. |
| `personKey` | [[!UICONTROL B2B-Source]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Person, die Mitglied der zugehörigen Kampagne ist. |
| `_id` | String | Eine eindeutige Kennung für den Datensatz. Dies ist ein vom System generierter Wert, der vom `campaignMemberID` getrennt ist. |

{style="table-layout:auto"}

Informationen dazu, wie sich diese Klasse konzeptionell auf die anderen B2B-Klassen bezieht und wie Sie diese Beziehungen in der Adobe Experience Platform-Benutzeroberfläche herstellen können, finden Sie im Handbuch zu [Schemabeziehungen in Real-Time CDP B2B edition](../../tutorials/relationship-b2b.md)

Weitere Felder, die mit dieser Klasse kompatibel sind, finden Sie in der Referenz für Feldergruppen für [[!UICONTROL XDM Business Campaign Member Details]](../../field-groups/b2b-campaign-members/details.md).
