---
title: XDM Business Campaign-Klasse
description: Erfahren Sie mehr über die XDM Business Campaign-Klasse im Experience-Datenmodell (XDM).
exl-id: 4e3228a1-74be-43af-b355-45d84afb1611
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 3%

---

# [!UICONTROL XDM Business Campaign]-Klasse

>[!IMPORTANT]
>
>Diese Klasse ist für Organisationen mit Zugriff auf [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md) vorgesehen. Sie müssen Zugriff auf Real-Time CDP B2B Edition haben, damit diese Klasse am [Echtzeit-Kundenprofil](../../../profile/home.md) teilnehmen kann.

[!UICONTROL XDM Business Campaign] ist eine standardmäßige XDM-Klasse (Experience-Datenmodell), die die erforderlichen Mindesteigenschaften einer Geschäftskampagne erfasst.

![Die Struktur der XDM Business Campaign-Klasse, wie sie in der Benutzeroberfläche angezeigt wird](../../images/classes/b2b/business-campaign.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `campaignKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Kampagnenentität. |
| `extSourceSystemAudit` | [[!UICONTROL Externe Source-Systemprüfungsattribute]](../../data-types/external-source-system-audit-attributes.md) | Wenn die Kampagne aus einem externen Quellsystem stammt, erfasst dieses Objekt Prüfattribute für dieses System. |
| `_id` | Zeichenfolge | Eine eindeutige Kennung für den Datensatz. Dies ist ein vom System erstellter Wert, der getrennt vom `campaignID` ist. |
| `campaignDescription` | Zeichenfolge | Eine Beschreibung der Kampagne. |
| `campaignID` | Zeichenfolge | Eine eindeutige Kennung für die Kampagnenentität. |
| `campaignName` | Zeichenfolge | Der Name der Kampagne. |
| `campaignType` | Zeichenfolge | Kampagnentyp oder Zielgruppe. |

{style="table-layout:auto"}

Informationen dazu, wie diese Klasse konzeptionell mit den anderen B2B-Klassen verknüpft ist und wie Sie diese Beziehungen in der Adobe Experience Platform-Benutzeroberfläche herstellen können, finden Sie im Handbuch zu [Schemabeziehungen in Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) .

Weitere Felder, die mit dieser Klasse kompatibel sind, finden Sie in der Feldergruppenreferenz für [[!UICONTROL XDM Business Campaign Details]](../../field-groups/b2b-campaign/details.md).
