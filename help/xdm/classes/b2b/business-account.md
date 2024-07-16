---
title: XDM Business Account-Klasse
description: Erfahren Sie mehr über die XDM Business Account-Klasse im Experience-Datenmodell (XDM).
exl-id: abe4c919-a680-4aad-918e-6e56cae8bd4d
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 2%

---

# [!UICONTROL XDM Business Account] class

>[!IMPORTANT]
>
>Diese Klasse ist für Organisationen mit Zugriff auf [Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/b2b-overview.md) vorgesehen. Sie müssen Zugriff auf Real-Time CDP B2B Edition haben, damit diese Klasse am [Echtzeit-Kundenprofil](../../../profile/home.md) teilnehmen kann.

[!UICONTROL XDM Business Account] ist eine standardmäßige Experience-Datenmodell (XDM)-Klasse, die die erforderlichen Mindesteigenschaften eines Geschäftskontos erfasst.

![Die Struktur der XDM Business Account-Klasse, wie sie in der Benutzeroberfläche angezeigt wird](../../images/classes/b2b/business-account.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `accountKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Eine zusammengesetzte Kennung für die Kontoentität. |
| `extSourceSystemAudit` | [[!UICONTROL Externe Source-Systemprüfungsattribute]](../../data-types/external-source-system-audit-attributes.md) | Wenn das Konto von einem externen Quellsystem stammt, erfasst dieses Objekt Prüfattribute für dieses System. |
| `_id` | Zeichenfolge | Eine eindeutige Kennung für den Datensatz. Dies ist ein systemgenerierter Wert, der von der `accountKey` -Kennung getrennt ist. |
| `isDeleted` | Boolesch | Gibt an, ob diese Kontoentität im Marketo Engage gelöscht wurde.<br><br>Bei Verwendung des [Marketo-Quell-Connectors](../../../sources/connectors/adobe-applications/marketo/marketo.md) werden alle in Marketo gelöschten Datensätze automatisch im Echtzeit-Kundenprofil angezeigt. Datensätze, die sich auf diese Profile beziehen, können jedoch im Data Lake bestehen bleiben. Durch Festlegen von `isDeleted` auf `true` können Sie mithilfe des Felds herausfiltern, welche Datensätze bei der Abfrage des Data Lake aus Ihren Quellen gelöscht wurden. |

{style="table-layout:auto"}

Weitere Informationen dazu, wie diese Klasse konzeptionell mit den anderen B2B-Klassen in Verbindung steht und wie Sie diese Beziehungen in der Adobe Experience Platform-Benutzeroberfläche herstellen können, finden Sie im Handbuch zu [Schemabeziehungen in Real-Time CDP B2B Edition](../../tutorials/relationship-b2b.md) .
