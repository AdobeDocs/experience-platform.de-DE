---
title: XDM Business Marketing List-Member-Klasse
description: Dieses Dokument bietet einen Überblick über die XDM Business Marketing List Members-Klasse im Experience-Datenmodell (XDM).
exl-id: 069002c2-5583-4c59-84ee-c071e2acaaec
source-git-commit: edf7afc5db219430232a3226dc691570b50a32bd
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 5%

---

# [!UICONTROL XDM Business Marketing List-Mitglieder] class

[!UICONTROL XDM Business Marketing List-Mitglieder] ist eine standardmäßige Experience-Datenmodell (XDM)-Klasse, die Mitglieder, Personen oder Kontakte beschreibt, die mit einer Marketing-Liste verknüpft sind.

![](../../images/classes/b2b/business-marketing-list-members.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Audit-Attribute des externen Quellsystems]](../../data-types/external-source-system-audit-attributes.md) | Wenn die Mitgliedschaft in der Marketing-Liste aus einem externen Quellsystem stammt, erfasst dieses Objekt Prüfattribute für dieses System. |
| `marketingListKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Marketing-Liste, der die Person angehört. |
| `marketingListMemberKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Entität der Mitgliedschaft in einer Marketing-Liste. |
| `personKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Person, die Mitglied der Marketing-Liste ist. |
| `_id` | Zeichenfolge | Eine eindeutige Kennung für den Datensatz. Dies ist ein systemgenerierter Wert, der getrennt vom `marketingListMemberID`. |
| `marketingListID` | Zeichenfolge | Eine eindeutige ID für die Marketing-Liste. |
| `marketingListMemberID` | Zeichenfolge | Eine eindeutige ID für die Entität der Mitgliedschaft in der Marketing-Liste. |
| `personId` | Zeichenfolge | Eine eindeutige ID für die Person. |

{style=&quot;table-layout:auto&quot;}

Siehe Handbuch unter [Schemabeziehungen in der Echtzeit-Kundendatenplattform B2B Edition](../../tutorials/relationship-b2b.md) um zu erfahren, wie diese Klasse konzeptionell mit den anderen B2B-Klassen in Beziehung steht und wie Sie diese Beziehungen in der Adobe Experience Platform-Benutzeroberfläche herstellen können.
