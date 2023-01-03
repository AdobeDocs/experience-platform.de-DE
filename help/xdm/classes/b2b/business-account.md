---
title: XDM Business Account-Klasse
description: Dieses Dokument bietet einen Überblick über die XDM Business Account-Klasse im Experience-Datenmodell (XDM).
exl-id: abe4c919-a680-4aad-918e-6e56cae8bd4d
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 6%

---

# [!UICONTROL XDM-Geschäftskonto] class

>[!IMPORTANT]
>
>Diese Klasse ist für Organisationen mit Zugriff auf [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Sie müssen Zugriff auf Real-Time CDP B2B Edition haben, damit diese Klasse an [Echtzeit-Kundenprofil](../../../profile/home.md).

[!UICONTROL XDM-Geschäftskonto] ist eine standardmäßige Experience-Datenmodell (XDM)-Klasse, die die erforderlichen Mindesteigenschaften eines Geschäftskontos erfasst.

![Die Struktur der XDM Business Account-Klasse, wie sie in der Benutzeroberfläche angezeigt wird](../../images/classes/b2b/business-account.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Kontoentität. |
| `extSourceSystemAudit` | [[!UICONTROL Audit-Attribute des externen Quellsystems]](../../data-types/external-source-system-audit-attributes.md) | Wenn das Konto von einem externen Quellsystem stammt, erfasst dieses Objekt Prüfattribute für dieses System. |
| `_id` | Zeichenfolge | Eine eindeutige Kennung für den Datensatz. Dies ist ein systemgenerierter Wert, der getrennt vom `accountKey` Kennung. |
| `isDeleted` | Boolesch | Gibt an, ob diese Kontoentität in Marketo Engage gelöscht wurde.<br><br>Bei Verwendung von [Marketo-Quell-Connector](../../../sources/connectors/adobe-applications/marketo/marketo.md), werden alle in Marketo gelöschten Datensätze automatisch in das Echtzeit-Kundenprofil übernommen. Datensätze, die sich auf diese Profile beziehen, können jedoch im Data Lake bestehen bleiben. Durch Festlegen von `isDeleted` nach `true`können Sie mithilfe des Felds herausfiltern, welche Datensätze bei der Abfrage des Data Lake aus Ihren Quellen gelöscht wurden. |

{style=&quot;table-layout:auto&quot;}

Siehe Handbuch unter [Schemabeziehungen in Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) um zu erfahren, wie diese Klasse konzeptionell mit den anderen B2B-Klassen in Beziehung steht und wie Sie diese Beziehungen in der Adobe Experience Platform-Benutzeroberfläche herstellen können.
