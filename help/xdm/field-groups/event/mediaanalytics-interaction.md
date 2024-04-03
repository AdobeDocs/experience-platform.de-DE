---
title: MediaAnalytics-Schema-Feldergruppe "Interaktionsdetails"
description: Erfahren Sie mehr über die Schemafeldergruppe "MediaAnalytics-Interaktionsdetails".
exl-id: 1096d28a-5796-49cc-bd45-b3f5188f699e
source-git-commit: b81afb8f6c4eaedb19a58b6fe3896286f1486804
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 2%

---

# [!UICONTROL Details zur MediaAnalytics-Interaktion] Schemafeldgruppe

[!UICONTROL Details zur MediaAnalytics-Interaktion] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Verwenden Sie diese Feldergruppe, um angereicherte Datenfelder zu erfassen, die Interaktionen mit Medieninhalten auf verschiedenen Plattformen oder Kanälen umfassend überwachen und analysieren.

![Ein Schemadiagramm der [!UICONTROL Details zur MediaAnalytics-Interaktion] Schemafeldgruppe.](../../images/field-groups/mediaanalytics-interaction.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|---| --- | --- | --- |
| [!UICONTROL Details zur Mediensammlung] | `mediaCollection` | [[!UICONTROL Details zur Mediensammlung]](../../data-types/media-collection-details.md) | Attribute im Zusammenhang mit einer Sammlung von Medienelementen. Verwenden Sie die Mediensammlungsfelder, um Daten zu erfassen und zur weiteren Verarbeitung an andere Adobe-Dienste zu senden. |
| [!UICONTROL Medienberichterstellungsdetails] | `mediaReporting` | [[!UICONTROL Medienberichterstellungsdetails]](../../data-types/media-reporting-details.md) | Berichterstellungsdetails und Metriken, die mit dem Medieninhalt verknüpft sind. * Die Felder für die Medienberichte werden von Adobe-Diensten verwendet, um die von Benutzern gesendeten Mediensammlungsfelder zu analysieren. Diese Daten werden zusammen mit anderen spezifischen Benutzermetriken berechnet und in Berichten verwendet. |
| [!UICONTROL Liste der von Mediensammlung heruntergeladenen Inhaltsereignisse] | `mediaDownloadedEvents` | [!UICONTROL Array] von [[!UICONTROL mediaEvent]](../../data-types/media-event-information.md) | Ereignisse, die das Herunterladen von Inhalten in der Mediensammlung verfolgen. |

{style="table-layout:auto"}

>[!TIP]
>
>Sie können Felder ausblenden, die nicht von der Media Edge-API verwendet werden. Das Ausblenden dieser Felder erleichtert das Lesen und Verstehen des Schemas, ist jedoch nicht erforderlich. Diese Felder beziehen sich nur auf die Felder im [!UICONTROL Details zur MediaAnalytics-Interaktion] fieldgroup. Befolgen Sie die Anweisungen im Abschnitt [Dokumentation zu Media Analytics zum Ausblenden nicht verwendeter Felder](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/implementation-edge.html#set-up-the-schema-in-adobe-experience-platform).

<!-- 
>[!NOTE]
>
>Schemas contain fields that are not used in every context or situation. They provide a potential blueprint to map an object. Schemas displayed for the Media Edge API Collection or Reporting data types only portray the relevant fields. You can manually select and deselect the fields that you want to use if you intend to use a schema for the Media Edge API interaction. You can find instructions on [hiding unnecessary fields](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/implementation-edge.html#set-up-the-schema-in-adobe-experience-platform) in the guide to install Media Analytics with Experience Platform Edge.
 -->
