---
title: XDM Business Account Person Relation Class
description: Erfahren Sie mehr über die Klasse "XDM Business Account Person Relation"im Experience-Datenmodell (XDM).
exl-id: d51abe9b-d936-4c84-96e2-35a81ca6b67f
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 3%

---

# [!UICONTROL Personenbeziehung zwischen XDM-Geschäftskonto] class

>[!IMPORTANT]
>
>Diese Klasse ist für Organisationen mit Zugriff auf [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Sie müssen Zugriff auf Real-Time CDP B2B Edition haben, damit diese Klasse an [Echtzeit-Kundenprofil](../../../profile/home.md).

[!UICONTROL Personenbeziehung zwischen XDM-Geschäftskonto] ist eine standardmäßige Experience-Datenmodell (XDM)-Klasse, die die erforderlichen Mindesteigenschaften einer Person erfasst, die mit einem Geschäftskonto verknüpft ist.

![Die Struktur der XDM Business Account Person Relation-Klasse, wie sie in der Benutzeroberfläche angezeigt wird](../../images/classes/b2b/business-account-person-relation.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für das Konto in der Beziehung zwischen Konto und Person. |
| `accountPersonKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Entität der Kontoperson-Beziehung. |
| `extSourceSystemAudit` | [[!UICONTROL Audit-Attribute des externen Quellsystems]](../../data-types/external-source-system-audit-attributes.md) | Wenn die Beziehung zwischen Konto und Person aus einem externen Quellsystem stammt, erfasst dieses Objekt Prüfattribute für dieses System. |
| `personKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Person in der Konto-Person-Beziehung. |
| `_id` | Zeichenfolge | Eine eindeutige Kennung für den Datensatz. Dies ist ein systemgenerierter Wert, der von den anderen von der Klasse erfassten ID-Feldern getrennt ist. |
| `accountID` | Zeichenfolge | Eine eindeutige Kennung für das Konto in der Beziehung zwischen Konto und Person. |
| `accountPersonID` | Zeichenfolge | Eine eindeutige Kennung für die Entität der Kontoperson-Beziehung. |
| `currencyCode` | Zeichenfolge | Der Währungscode nach ISO 4217, der für die Beziehung zwischen Konto und Person verwendet wird. |
| `isActive` | Boolesch | Gibt an, ob die Beziehung zwischen Konto und Person aktiv ist. |
| `isDeleted` | Boolesch | Gibt an, ob diese Beziehung zwischen Konto und Person im Marketo Engage gelöscht wurde.<br><br>Bei Verwendung von [Marketo-Quell-Connector](../../../sources/connectors/adobe-applications/marketo/marketo.md), werden alle in Marketo gelöschten Datensätze automatisch in das Echtzeit-Kundenprofil übernommen. Datensätze, die sich auf diese Profile beziehen, können jedoch im Data Lake bestehen bleiben. Durch Festlegen von `isDeleted` nach `true`können Sie mithilfe des Felds herausfiltern, welche Datensätze bei der Abfrage des Data Lake aus Ihren Quellen gelöscht wurden. |
| `isDirect` | Boolesch | Gibt an, ob dies eine direkte Beziehung zwischen dem Konto und der Person ist. |
| `isPrimary` | Boolesch | Gibt an, ob die Person der Hauptkontakt für dieses Konto ist. |
| `personID` | Zeichenfolge | Eine eindeutige Kennung für die Person in der Beziehung zwischen Konto und Person. |
| `personRoles` | Zeichenfolgen-Array | Führt die Rollen der Person in der Beziehung zwischen Konto und Person auf. |
| `relationEndDate` | DateTime | Das Datum, an dem die Beziehung zwischen dem Konto und der Person endete. |
| `relationStartDate` | DateTime | Das Datum, an dem die Beziehung zwischen dem Konto und der Person begann. |
| `relationshipSource` | Zeichenfolge | Die Quelle der Konto-Person-Beziehung. |

{style="table-layout:auto"}

Siehe Handbuch unter [Schemabeziehungen in Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) um zu erfahren, wie diese Klasse konzeptionell mit den anderen B2B-Klassen in Beziehung steht und wie Sie diese Beziehungen in der Adobe Experience Platform-Benutzeroberfläche herstellen können.
