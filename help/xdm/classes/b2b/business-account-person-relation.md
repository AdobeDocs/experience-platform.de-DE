---
title: XDM Business Account Person Relation Class
description: Dieses Dokument bietet einen Überblick über die XDM Business Account Person Relation-Klasse im Experience-Datenmodell (XDM).
source-git-commit: 5fd82b02eb25f3d575de695c2f2b14a5e5b18400
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 4%

---

# [!UICONTROL XDM Business Account Person ] Relationclass

>[!NOTE]
>
>Diese Klasse ist nur für Unternehmen verfügbar, die Zugriff auf die Echtzeit-Kundendatenplattform B2B Edition haben.

[!UICONTROL XDM Business Account Person ] Relationation ist eine standardmäßige Experience-Datenmodell (XDM)-Klasse, die die erforderlichen Mindesteigenschaften einer Person erfasst, die mit einem Geschäftskonto verknüpft ist.

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

Informationen dazu, wie diese Klasse konzeptionell mit anderen B2B-Klassen in Beziehung steht und wie Sie diese Beziehungen in der Adobe Experience Platform-Benutzeroberfläche herstellen können, finden Sie im Handbuch zu [Schemabeziehungen in der Echtzeit-Kundendatenplattform B2B Edition](../../tutorials/relationship-b2b.md).
