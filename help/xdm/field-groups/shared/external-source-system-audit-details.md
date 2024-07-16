---
title: Audit-Details des externen Quellsystems
description: Erfahren Sie mehr über die Feldergruppe "Experience-Datenmodell (XDM)"für externe Source-Systemprüfungsdetails.
source-git-commit: 656070cf69e3713c7889f53d51937e0e70085d96
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 6%

---

# Feldergruppe &quot;[!UICONTROL External Source System Audit Details]&quot;

[!UICONTROL External Source System Audit Details] ist eine standardmäßige Experience-Datenmodell (XDM)-Feldergruppe, die den Kerndatentyp &quot;External Source System Audit Attributes&quot;erweitert, indem auf seine Eigenschaften verwiesen und kontextbezogene Metadaten hinzugefügt werden. Dies ermöglicht ein detailliertes Audit-Tracking und eine flexible Datenintegration aus externen Quellen.

![Ein Schemadiagramm der Feldergruppe &quot;Audit-Details des externen Source-Systems&quot;.](../../images/field-groups/shared/external-source-system-audit-details.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| -------------------------------------------------| ---------------------------------------- | --------- | --- |
| [!UICONTROL Prüfdetails für externe Source-Systeme] | `external-source-system-audit-details` | [[!UICONTROL Externe Source-Systemprüfungsattribute]](../../data-types/external-source-system-audit-attributes.md) | Die Feldergruppe &quot;[!UICONTROL External Source System Audit Details]&quot; erweitert den Kerndatentyp &quot;External Source System Audit Attributes&quot;, indem sie auf seine Eigenschaften verweist und kontextbezogene Metadaten hinzufügt. Dies erleichtert das detaillierte Audit-Tracking und die flexible Datenintegration für externe Quellen und ermöglicht so die asynchrone Erfassung von Profilen. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/shared/external-source-system-audit-details.schema.json)