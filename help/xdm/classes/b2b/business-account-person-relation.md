---
title: Personenbeziehungsklasse für XDM Business-Konto
description: Erfahren Sie mehr über die Klasse „XDM Business Account Person Relation“ im Experience-Datenmodell (XDM).
exl-id: d51abe9b-d936-4c84-96e2-35a81ca6b67f
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 12%

---

# [!UICONTROL XDM Business Account Person Relation]-Klasse

>[!IMPORTANT]
>
>Diese Klasse ist für die Verwendung durch Organisationen vorgesehen, die Zugriff auf [Adobe Real-time Customer Data Platform B2B edition](../../../rtcdp/b2b-overview.md) haben. Sie müssen Zugriff auf Real-Time CDP B2B edition haben, damit diese Klasse am Echtzeit[Kundenprofil teilnehmen &#x200B;](../../../profile/home.md).

[!UICONTROL XDM Business Account Person Relation] ist eine standardmäßige Experience-Datenmodell (XDM)-Klasse, die die erforderlichen Mindesteigenschaften einer Person erfasst, die einem Geschäftskonto zugeordnet ist.

![Die Struktur der Personenbeziehungsklasse des XDM Business-Kontos, wie sie in der Benutzeroberfläche angezeigt wird](../../images/classes/b2b/business-account-person-relation.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B-Source]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für das Konto in der Konto-Personen-Beziehung. |
| `accountPersonKey` | [[!UICONTROL B2B-Source]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Entität der Konto-Personen-Beziehung. |
| `extSourceSystemAudit` | [[!UICONTROL Audit-Attribute des externen Source-Systems]](../../data-types/external-source-system-audit-attributes.md) | Wenn die Konto-Personen-Beziehung von einem externen Quellsystem stammt, erfasst dieses Objekt Audit-Attribute für dieses System. |
| `personKey` | [[!UICONTROL B2B-Source]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Person in der Konto-Personen-Beziehung. |
| `_id` | String | Eine eindeutige Kennung für den Datensatz. Dies ist ein systemgenerierter Wert, der von den anderen ID-Feldern, die von der Klasse erfasst werden, getrennt ist. |
| `accountID` | String | Eine eindeutige Kennung für das Konto in der Konto-Personen-Beziehung. |
| `accountPersonID` | String | Eine eindeutige Kennung für die Entität der Konto-Personen-Beziehung. |
| `currencyCode` | String | Der ISO 4217-Währungscode, der für die Beziehung zwischen dem Konto und der Person verwendet wird. |
| `isActive` | Boolesch | Gibt an, ob die Beziehung zwischen dem Konto und der Person aktiv ist. |
| `isDeleted` | Boolesch | Gibt an, ob diese Konto-Personen-Beziehung auf Marketo Engage gelöscht wurde.<br><br>Bei Verwendung des [Marketo-Quell](../../../sources/connectors/adobe-applications/marketo/marketo.md)Connectors werden alle in Marketo gelöschten Datensätze automatisch im Echtzeit-Kundenprofil angezeigt. Datensätze, die sich auf diese Profile beziehen, können jedoch weiterhin im Data Lake vorhanden sein. Wenn Sie `isDeleted` auf `true` setzen, können Sie das Feld verwenden, um herauszufiltern, welche Datensätze aus Ihren Quellen gelöscht wurden, wenn Sie den Data Lake abfragen. |
| `isDirect` | Boolesch | Gibt an, ob dies eine direkte Beziehung zwischen dem Konto und der Person ist. |
| `isPrimary` | Boolesch | Gibt an, ob die Person der primäre Kontakt für dieses Konto ist. |
| `personID` | String | Eine eindeutige Kennung für die Person in der Konto-Personen-Beziehung. |
| `personRoles` | Zeichenfolgen-Array | Listet die Rollen der Person in der Konto-Personen-Beziehung auf. |
| `relationEndDate` | DateTime | Das Datum, an dem die Beziehung zwischen dem Konto und der Person beendet wurde. |
| `relationStartDate` | DateTime | Das Datum, an dem die Beziehung zwischen dem Konto und der Person begann. |
| `relationshipSource` | String | Die Quelle der Konto-Personen-Beziehung. |

{style="table-layout:auto"}

Lesen Sie das Handbuch zu [Schemabeziehungen in Real-Time CDP B2B edition](../../tutorials/relationship-b2b.md), um zu erfahren, wie sich diese Klasse konzeptionell auf die anderen B2B-Klassen bezieht und wie Sie diese Beziehungen in der Adobe Experience Platform-Benutzeroberfläche herstellen können.
