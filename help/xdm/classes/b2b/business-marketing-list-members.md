---
title: XDM Business Marketing List-Member-Klasse
description: Dieses Dokument bietet einen Überblick über die XDM Business Marketing List Members-Klasse im Experience-Datenmodell (XDM).
exl-id: 069002c2-5583-4c59-84ee-c071e2acaaec
source-git-commit: 50e5fe8573d828f88867ed33fe86e974c85de60a
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 7%

---

# [!UICONTROL XDM Business Marketing List-Mitglieder] class

>[!IMPORTANT]
>
>Diese Klasse ist für Organisationen mit Zugriff auf [Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Sie müssen Zugriff auf die Echtzeit-CDP B2B Edition haben, damit diese Klasse an [Echtzeit-Kundenprofil](../../../profile/home.md).

[!UICONTROL XDM Business Marketing List-Mitglieder] ist eine standardmäßige Experience-Datenmodell (XDM)-Klasse, die Mitglieder, Personen oder Kontakte beschreibt, die mit einer Marketing-Liste verknüpft sind.

![Die Struktur der XDM Business Marketing List Members-Klasse, wie sie in der Benutzeroberfläche angezeigt wird](../../images/classes/b2b/business-marketing-list-members.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Audit-Attribute des externen Quellsystems]](../../data-types/external-source-system-audit-attributes.md) | Wenn die Mitgliedschaft in der Marketing-Liste aus einem externen Quellsystem stammt, erfasst dieses Objekt Prüfattribute für dieses System. |
| `marketingListKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Marketing-Liste, der die Person angehört. |
| `marketingListMemberKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Entität der Mitgliedschaft in einer Marketing-Liste. |
| `personKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Person, die Mitglied der Marketing-Liste ist. |
| `_id` | Zeichenfolge | Eine eindeutige Kennung für den Datensatz. Dies ist ein systemgenerierter Wert, der getrennt vom `marketingListMemberID`. |
| `isDeleted` | Boolesch | Gibt an, ob diese Entität eines Mitglieds der Marketingliste in Marketo Engage gelöscht wurde.<br><br>Bei Verwendung von [Marketo-Quell-Connector](../../../sources/connectors/adobe-applications/marketo/marketo.md), werden alle in Marketo gelöschten Datensätze automatisch im Echtzeit-Kundenprofil angezeigt. Datensätze, die sich auf diese Profile beziehen, können jedoch im Data Lake bestehen bleiben. Durch Festlegen von `isDeleted` nach `true`können Sie mithilfe des Felds herausfiltern, welche Datensätze bei der Abfrage des Data Lake aus Ihren Quellen gelöscht wurden. |
| `marketingListID` | Zeichenfolge | Eine eindeutige ID für die Marketing-Liste. |
| `marketingListMemberID` | Zeichenfolge | Eine eindeutige ID für die Entität der Mitgliedschaft in der Marketing-Liste. |
| `personId` | Zeichenfolge | Eine eindeutige ID für die Person. |

{style=&quot;table-layout:auto&quot;}

Siehe Handbuch unter [Schemabeziehungen in der Echtzeit-Kundendatenplattform B2B Edition](../../tutorials/relationship-b2b.md) um zu erfahren, wie diese Klasse konzeptionell mit den anderen B2B-Klassen in Beziehung steht und wie Sie diese Beziehungen in der Adobe Experience Platform-Benutzeroberfläche herstellen können.
