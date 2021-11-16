---
title: XDM Business Account Person Relation Class
description: Dieses Dokument bietet einen Überblick über die XDM Business Account Person Relation-Klasse im Experience-Datenmodell (XDM).
exl-id: d51abe9b-d936-4c84-96e2-35a81ca6b67f
source-git-commit: 8718512a9768158183b9fb6b9e336081e47cd889
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 5%

---

# [!UICONTROL Personenbeziehung zwischen XDM-Geschäftskonto] class

>[!IMPORTANT]
>
>Diese Klasse ist für Organisationen mit Zugriff auf [Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Sie müssen Zugriff auf die Echtzeit-CDP B2B Edition haben, damit diese Klasse an [Echtzeit-Kundenprofil](../../../profile/home.md).

[!UICONTROL Personenbeziehung zwischen XDM-Geschäftskonto] ist eine standardmäßige Experience-Datenmodell (XDM)-Klasse, die die erforderlichen Mindesteigenschaften einer Person erfasst, die mit einem Geschäftskonto verknüpft ist.

![](../../images/classes/b2b/business-account-person-relation.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für das Konto in der Beziehung zwischen Konto und Person. |
| `accountPersonKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Entität der Kundenbeziehung. |
| `extSourceSystemAudit` | [[!UICONTROL Audit-Attribute des externen Quellsystems]](../../data-types/external-source-system-audit-attributes.md) | Wenn die Beziehung zwischen Konto und Person aus einem externen Quellsystem stammt, erfasst dieses Objekt Prüfattribute für dieses System. |
| `personKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Person in der Konto-Person-Beziehung. |
| `_id` | Zeichenfolge | Eine eindeutige Kennung für den Datensatz. Dies ist ein systemgenerierter Wert, der von den anderen von der Klasse erfassten ID-Feldern getrennt ist. |
| `accountID` | Zeichenfolge | Eine eindeutige Kennung für das Konto in der Beziehung zwischen Konto und Person. |
| `accountPersonID` | Zeichenfolge | Eine eindeutige Kennung für die Entität der Kundenbeziehung. |
| `currencyCode` | Zeichenfolge | Der Währungscode nach ISO 4217, der für die Beziehung zwischen dem Konto und der Person verwendet wird. |
| `isActive` | Boolesch | Gibt an, ob die Beziehung zwischen dem Konto und der Person aktiv ist. |
| `isDirect` | Boolesch | Gibt an, ob es sich um eine direkte Beziehung zwischen dem Konto und der Person handelt. |
| `isPrimary` | Boolesch | Gibt an, ob die Person der Hauptkontakt für dieses Konto ist. |
| `personID` | Zeichenfolge | Eine eindeutige Kennung für die Person in der Beziehung zwischen Konto und Person. |
| `personRole` | Zeichenfolge | Die Rolle der Person in der Beziehung zwischen Konto und Person. |
| `relationEndDate` | DateTime | Das Datum, an dem die Beziehung zwischen dem Konto und der Person endete. |
| `relationStartDate` | DateTime | Das Datum, an dem die Beziehung zwischen dem Konto und der Person begann. |

{style=&quot;table-layout:auto&quot;}

Siehe Handbuch unter [Schemabeziehungen in der Echtzeit-Kundendatenplattform B2B Edition](../../tutorials/relationship-b2b.md) um zu erfahren, wie diese Klasse konzeptionell mit den anderen B2B-Klassen in Beziehung steht und wie Sie diese Beziehungen in der Adobe Experience Platform-Benutzeroberfläche herstellen können.
