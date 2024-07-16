---
title: XDM Business Account Person Relation Class
description: Erfahren Sie mehr über die Klasse "XDM Business Account Person Relation"im Experience-Datenmodell (XDM).
exl-id: d51abe9b-d936-4c84-96e2-35a81ca6b67f
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 12%

---

# [!UICONTROL XDM Business Account Person Relation] class

>[!IMPORTANT]
>
>Diese Klasse ist für Organisationen mit Zugriff auf [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md) vorgesehen. Sie müssen Zugriff auf Real-Time CDP B2B Edition haben, damit diese Klasse am [Echtzeit-Kundenprofil](../../../profile/home.md) teilnehmen kann.

[!UICONTROL XDM Business Account Person Relation] ist eine standardmäßige Experience-Datenmodell (XDM)-Klasse, die die erforderlichen Mindesteigenschaften einer Person erfasst, die mit einem Geschäftskonto verknüpft ist.

![Die Struktur der XDM Business Account Person Relation-Klasse, wie sie in der Benutzeroberfläche angezeigt wird](../../images/classes/b2b/business-account-person-relation.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für das Konto in der Beziehung zwischen Konto und Person. |
| `accountPersonKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Entität der Kontoperson-Beziehung. |
| `extSourceSystemAudit` | [[!UICONTROL Externe Source-Systemprüfungsattribute]](../../data-types/external-source-system-audit-attributes.md) | Wenn die Beziehung zwischen Konto und Person aus einem externen Quellsystem stammt, erfasst dieses Objekt Prüfattribute für dieses System. |
| `personKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Person in der Konto-Person-Beziehung. |
| `_id` | Zeichenfolge | Eine eindeutige Kennung für den Datensatz. Dies ist ein systemgenerierter Wert, der von den anderen von der Klasse erfassten ID-Feldern getrennt ist. |
| `accountID` | Zeichenfolge | Eine eindeutige Kennung für das Konto in der Beziehung zwischen Konto und Person. |
| `accountPersonID` | Zeichenfolge | Eine eindeutige Kennung für die Entität der Kontoperson-Beziehung. |
| `currencyCode` | Zeichenfolge | Der ISO 4217-Währungscode, der für die Beziehung zwischen dem Konto und der Person verwendet wird. |
| `isActive` | Boolesch | Gibt an, ob die Beziehung zwischen Konto und Person aktiv ist. |
| `isDeleted` | Boolesch | Gibt an, ob diese Beziehung zwischen Konto und Person im Marketo Engage gelöscht wurde.<br><br>Bei Verwendung des [Marketo-Quell-Connectors](../../../sources/connectors/adobe-applications/marketo/marketo.md) werden alle in Marketo gelöschten Datensätze automatisch im Echtzeit-Kundenprofil angezeigt. Datensätze, die sich auf diese Profile beziehen, können jedoch im Data Lake bestehen bleiben. Durch Festlegen von `isDeleted` auf `true` können Sie mithilfe des Felds herausfiltern, welche Datensätze bei der Abfrage des Data Lake aus Ihren Quellen gelöscht wurden. |
| `isDirect` | Boolesch | Gibt an, ob dies eine direkte Beziehung zwischen dem Konto und der Person ist. |
| `isPrimary` | Boolesch | Gibt an, ob die Person der Hauptkontakt für dieses Konto ist. |
| `personID` | Zeichenfolge | Eine eindeutige Kennung für die Person in der Beziehung zwischen Konto und Person. |
| `personRoles` | Zeichenfolgen-Array | Führt die Rollen der Person in der Beziehung zwischen Konto und Person auf. |
| `relationEndDate` | DateTime | Das Datum, an dem die Beziehung zwischen dem Konto und der Person beendet wurde. |
| `relationStartDate` | DateTime | Das Datum, an dem die Beziehung zwischen dem Konto und der Person begann. |
| `relationshipSource` | Zeichenfolge | Die Quelle der Konto-Person-Beziehung. |

{style="table-layout:auto"}

Weitere Informationen dazu, wie diese Klasse konzeptionell mit den anderen B2B-Klassen in Verbindung steht und wie Sie diese Beziehungen in der Adobe Experience Platform-Benutzeroberfläche herstellen können, finden Sie im Handbuch zu [Schemabeziehungen in Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) .
