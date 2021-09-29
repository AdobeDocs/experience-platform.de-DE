---
title: XDM Business Marketing List-Member-Klasse
description: Dieses Dokument bietet einen Überblick über die XDM Business Marketing List Members-Klasse im Experience-Datenmodell (XDM).
exl-id: 069002c2-5583-4c59-84ee-c071e2acaaec
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 7%

---

# [!UICONTROL XDM Business Marketing List ] Membersclass (Beta)

>[!IMPORTANT]
>
>Diese Klasse ist als Teil der Echtzeit-Kundendatenplattform B2B Edition verfügbar, die sich derzeit in der Betaphase befindet. Dokumentation und Funktionalität können sich ändern.

[!UICONTROL XDM Business Marketing List ] Membersis ist eine standardmäßige Experience-Datenmodell (XDM)-Klasse, die Mitglieder, Personen oder Kontakte beschreibt, die mit einer Marketingliste verknüpft sind.

![](../../images/classes/b2b/business-marketing-list-members.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Audit-Attribute des externen Quellsystems]](../../data-types/external-source-system-audit-attributes.md) | Wenn die Mitgliedschaft in der Marketing-Liste von einem externen Quellsystem stammt, erfasst dieses Objekt Prüfattribute für dieses System. |
| `marketingListKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Marketing-Liste, der die Person angehört. |
| `marketingListMemberKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Entität der Mitgliedschaft in einer Marketing-Liste. |
| `personKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Person, die Mitglied der Marketing-Liste ist. |
| `_id` | Zeichenfolge | Eine eindeutige Kennung für den Datensatz. Dies ist ein systemgenerierter Wert, der von `marketingListMemberID` getrennt ist. |
| `marketingListID` | Zeichenfolge | Eine eindeutige ID für die Marketing-Liste. |
| `marketingListMemberID` | Zeichenfolge | Eine eindeutige ID für die Entität der Mitgliedschaft in der Marketing-Liste. |
| `personId` | Zeichenfolge | Eine eindeutige ID für die Person. |

{style=&quot;table-layout:auto&quot;}

Informationen dazu, wie diese Klasse konzeptionell mit anderen B2B-Klassen in Beziehung steht und wie Sie diese Beziehungen in der Adobe Experience Platform-Benutzeroberfläche herstellen können, finden Sie im Handbuch zu [Schemabeziehungen in der Echtzeit-Kundendatenplattform B2B Edition](../../tutorials/relationship-b2b.md).
