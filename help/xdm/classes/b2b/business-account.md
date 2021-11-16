---
title: XDM Business Account-Klasse
description: Dieses Dokument bietet einen Überblick über die XDM Business Account-Klasse im Experience-Datenmodell (XDM).
exl-id: abe4c919-a680-4aad-918e-6e56cae8bd4d
source-git-commit: 8718512a9768158183b9fb6b9e336081e47cd889
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 4%

---

# [!UICONTROL XDM-Geschäftskonto] class

>[!IMPORTANT]
>
>Diese Klasse ist für Organisationen mit Zugriff auf [Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md). Sie müssen Zugriff auf die Echtzeit-CDP B2B Edition haben, damit diese Klasse an [Echtzeit-Kundenprofil](../../../profile/home.md).

[!UICONTROL XDM-Geschäftskonto] ist eine standardmäßige Experience-Datenmodell (XDM)-Klasse, die die erforderlichen Mindesteigenschaften eines Geschäftskontos erfasst.

![](../../images/classes/b2b/business-account.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B-Quelle]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Kontoentität. |
| `extSourceSystemAudit` | [[!UICONTROL Audit-Attribute des externen Quellsystems]](../../data-types/external-source-system-audit-attributes.md) | Wenn das Konto von einem externen Quellsystem stammt, erfasst dieses Objekt Prüfattribute für dieses System. |
| `_id` | Zeichenfolge | Eine eindeutige Kennung für den Datensatz. Dies ist ein systemgenerierter Wert, der getrennt vom `accountID`. |
| `accountID` | Zeichenfolge | Eine eindeutige Kennung für die Kontoentität. |

{style=&quot;table-layout:auto&quot;}

Siehe Handbuch unter [Schemabeziehungen in der Echtzeit-Kundendatenplattform B2B Edition](../../tutorials/relationship-b2b.md) um zu erfahren, wie diese Klasse konzeptionell mit den anderen B2B-Klassen in Beziehung steht und wie Sie diese Beziehungen in der Adobe Experience Platform-Benutzeroberfläche herstellen können.
