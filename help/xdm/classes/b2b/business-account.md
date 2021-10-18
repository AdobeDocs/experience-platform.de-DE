---
title: XDM Business Account-Klasse
description: Dieses Dokument bietet einen Überblick über die XDM Business Account-Klasse im Experience-Datenmodell (XDM).
exl-id: abe4c919-a680-4aad-918e-6e56cae8bd4d
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 9%

---

# [!UICONTROL XDM Business ] Accountclass (Beta)

>[!IMPORTANT]
>
>Diese Klasse ist als Teil der Real-time Customer Data Platform B2B Edition verfügbar, die sich derzeit in der Beta-Phase befindet. Dokumentation und Funktionalität können sich ändern.

[!UICONTROL XDM Business ] Accounts ist eine standardmäßige Experience-Datenmodell (XDM)-Klasse, die die erforderlichen Mindesteigenschaften eines Geschäftskontos erfasst.

![](../../images/classes/b2b/business-account.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Kontoentität. |
| `extSourceSystemAudit` | [[!UICONTROL Audit-Attribute des externen Quellsystems]](../../data-types/external-source-system-audit-attributes.md) | Wenn das Konto von einem externen Quellsystem stammt, erfasst dieses Objekt Prüfattribute für dieses System. |
| `_id` | Zeichenfolge | Eine eindeutige Kennung für den Datensatz. Dies ist ein systemgenerierter Wert, der von `accountID` getrennt ist. |
| `accountID` | Zeichenfolge | Eine eindeutige Kennung für die Kontoentität. |

{style=&quot;table-layout:auto&quot;}

Informationen dazu, wie diese Klasse konzeptionell mit anderen B2B-Klassen in Beziehung steht und wie Sie diese Beziehungen in der Adobe Experience Platform-Benutzeroberfläche herstellen können, finden Sie im Handbuch zu [Schemabeziehungen in der Echtzeit-Kundendatenplattform B2B Edition](../../tutorials/relationship-b2b.md).
