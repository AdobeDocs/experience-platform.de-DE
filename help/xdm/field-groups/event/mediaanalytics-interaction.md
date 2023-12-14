---
title: MediaAnalytics-Schema-Feldergruppe "Interaktionsdetails"
description: Erfahren Sie mehr über die Schemafeldergruppe "MediaAnalytics-Interaktionsdetails".
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 5%

---

# [!UICONTROL Details zur MediaAnalytics-Interaktion] Schemafeldgruppe

[!UICONTROL Details zur MediaAnalytics-Interaktion] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Verwenden Sie diese Feldergruppe, um angereicherte Datenfelder zu erfassen, die Interaktionen mit Medieninhalten auf verschiedenen Plattformen oder Kanälen umfassend überwachen und analysieren.

![Ein Schemadiagramm der [!UICONTROL Details zur MediaAnalytics-Interaktion] Schemafeldgruppe.](../../images/field-groups/mediaanalytics-interaction.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|---| --- | --- | --- |
| [!UICONTROL Details zur Mediensammlung] | `mediaCollection` | [[!UICONTROL Informationen zu Mediendetails]](../../data-types/media-details-information.md) | Attribute im Zusammenhang mit einer Sammlung von Medienelementen. |
| [!UICONTROL Medienberichterstellungsdetails] | `mediaReporting` | [[!UICONTROL Informationen zu Mediendetails]](../../data-types/media-details-information.md) | Berichterstellungsdetails und Metriken, die mit dem Medieninhalt verknüpft sind. |
| [!UICONTROL Liste der von Mediensammlung heruntergeladenen Inhaltsereignisse] | `mediaDownloadedEvents` | [!UICONTROL Array] von [[!UICONTROL mediaEvent]](../../data-types/media-event-information.md) | Ereignisse, die das Herunterladen von Inhalten in der Mediensammlung verfolgen. |

{style="table-layout:auto"}

Weiterführende Informationen zur Feldergruppe finden Sie im Abschnitt [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-analytics.schema.json)
