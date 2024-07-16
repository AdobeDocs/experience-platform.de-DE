---
title: XDM Business Opportunity-Klasse
description: Erfahren Sie mehr über die XDM Business Opportunity-Klasse im Experience-Datenmodell (XDM).
exl-id: d816b0f9-fd37-45da-aa55-247f7f662da0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 3%

---

# [!UICONTROL XDM Business Opportunity]-Klasse

>[!IMPORTANT]
>
>Diese Klasse ist für Organisationen mit Zugriff auf [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md) vorgesehen. Sie müssen Zugriff auf Real-Time CDP B2B Edition haben, damit diese Klasse am [Echtzeit-Kundenprofil](../../../profile/home.md) teilnehmen kann.

[!UICONTROL XDM Business Opportunity] ist eine standardmäßige Experience-Datenmodell (XDM)-Klasse, die die erforderlichen Mindesteigenschaften einer Geschäftschance erfasst.

![Die Struktur der XDM Business Opportunity-Klasse, wie sie in der Benutzeroberfläche angezeigt wird](../../images/classes/b2b/business-opportunity.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für das Konto, mit dem diese Gelegenheit verknüpft ist. |
| `extSourceSystemAudit` | [[!UICONTROL Externe Source-Systemprüfungsattribute]](../../data-types/external-source-system-audit-attributes.md) | Wenn die Möglichkeit von einem externen Quellsystem stammt, erfasst dieses Objekt Prüfattribute für dieses System. |
| `opportunityKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Opportunity. |
| `_id` | Zeichenfolge | Eine eindeutige Kennung für den Datensatz. Dies ist ein vom System erstellter Wert, der getrennt vom `opportunityID` ist. |
| `accountID` | Zeichenfolge | Eine eindeutige ID für das Konto, mit dem diese Gelegenheit verknüpft ist. |
| `isDeleted` | Boolesch | Gibt an, ob diese Entität der Marketingliste im Marketo Engage gelöscht wurde.<br><br>Bei Verwendung des [Marketo-Quell-Connectors](../../../sources/connectors/adobe-applications/marketo/marketo.md) werden alle in Marketo gelöschten Datensätze automatisch im Echtzeit-Kundenprofil angezeigt. Datensätze, die sich auf diese Profile beziehen, können jedoch im Data Lake bestehen bleiben. Durch Festlegen von `isDeleted` auf `true` können Sie mithilfe des Felds herausfiltern, welche Datensätze bei der Abfrage des Data Lake aus Ihren Quellen gelöscht wurden. |
| `opportunityDescription` | Zeichenfolge | Eine Beschreibung der Gelegenheit. |
| `opportunityID` | Zeichenfolge | Eine eindeutige ID für die Opportunity. |
| `opportunityName` | Zeichenfolge | Der Name der Gelegenheit. |
| `opportunityStage` | Zeichenfolge | Die Verkaufsphase der Chance. |
| `opportunityType` | Zeichenfolge | Die Art von Gelegenheit. |

{style="table-layout:auto"}

Weitere Informationen dazu, wie diese Klasse konzeptionell mit den anderen B2B-Klassen in Verbindung steht und wie Sie diese Beziehungen in der Adobe Experience Platform-Benutzeroberfläche herstellen können, finden Sie im Handbuch zu [Schemabeziehungen in Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) .
