---
title: XDM Business Marketing List-Member-Klasse
description: Erfahren Sie mehr über die Klasse der XDM Business Marketing List-Mitglieder im Experience-Datenmodell (XDM).
exl-id: 069002c2-5583-4c59-84ee-c071e2acaaec
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 2%

---

# [!UICONTROL XDM Business Marketing List Members] class

>[!IMPORTANT]
>
>Diese Klasse ist für Organisationen mit Zugriff auf [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md) vorgesehen. Sie müssen Zugriff auf Real-Time CDP B2B Edition haben, damit diese Klasse am [Echtzeit-Kundenprofil](../../../profile/home.md) teilnehmen kann.

[!UICONTROL XDM Business Marketing List Members] ist eine standardmäßige Experience-Datenmodell (XDM)-Klasse, die Mitglieder, Personen oder Kontakte beschreibt, die mit einer Marketingliste verknüpft sind.

![Die Struktur der XDM Business Marketing List Members-Klasse, wie sie in der Benutzeroberfläche angezeigt wird](../../images/classes/b2b/business-marketing-list-members.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Externe Source-Systemprüfungsattribute]](../../data-types/external-source-system-audit-attributes.md) | Wenn die Mitgliedschaft in der Marketing-Liste aus einem externen Quellsystem stammt, erfasst dieses Objekt Prüfattribute für dieses System. |
| `marketingListKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Marketing-Liste, der die Person angehört. |
| `marketingListMemberKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Entität der Mitgliedschaft in einer Marketing-Liste. |
| `personKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Person, die Mitglied der Marketing-Liste ist. |
| `_id` | Zeichenfolge | Eine eindeutige Kennung für den Datensatz. Dies ist ein vom System erstellter Wert, der getrennt vom `marketingListMemberID` ist. |
| `isDeleted` | Boolesch | Gibt an, ob diese Entität eines Mitglieds der Marketingliste im Marketo Engage gelöscht wurde.<br><br>Bei Verwendung des [Marketo-Quell-Connectors](../../../sources/connectors/adobe-applications/marketo/marketo.md) werden alle in Marketo gelöschten Datensätze automatisch im Echtzeit-Kundenprofil angezeigt. Datensätze, die sich auf diese Profile beziehen, können jedoch im Data Lake bestehen bleiben. Durch Festlegen von `isDeleted` auf `true` können Sie mithilfe des Felds herausfiltern, welche Datensätze bei der Abfrage des Data Lake aus Ihren Quellen gelöscht wurden. |
| `marketingListID` | Zeichenfolge | Eine eindeutige ID für die Marketing-Liste. |
| `marketingListMemberID` | Zeichenfolge | Eine eindeutige ID für die Entität der Mitgliedschaft in der Marketing-Liste. |
| `personId` | Zeichenfolge | Eine eindeutige ID für die Person. |

{style="table-layout:auto"}

Weitere Informationen dazu, wie diese Klasse konzeptionell mit den anderen B2B-Klassen in Verbindung steht und wie Sie diese Beziehungen in der Adobe Experience Platform-Benutzeroberfläche herstellen können, finden Sie im Handbuch zu [Schemabeziehungen in Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) .
