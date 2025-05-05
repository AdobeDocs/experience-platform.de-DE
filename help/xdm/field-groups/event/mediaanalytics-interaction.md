---
title: Schemafeldgruppe „Media Analytics Interaction Details“
description: Erfahren Sie mehr über die Schemafeldgruppe „MediaAnalytics Interaction Details“.
exl-id: 1096d28a-5796-49cc-bd45-b3f5188f699e
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 2%

---

# [!UICONTROL MediaAnalytics Interaction Details] Schemafeldgruppe

[!UICONTROL MediaAnalytics Interaction Details] ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Verwenden Sie diese Feldergruppe, um angereicherte Datenfelder zu erfassen, die die Interaktionen mit Medieninhalten über verschiedene Plattformen oder Kanäle hinweg umfassend überwachen und analysieren.

![Ein Schemadiagramm für die Schemafeldgruppe [!UICONTROL MediaAnalytics Interaction Details].](../../images/field-groups/mediaanalytics-interaction.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|---| --- | --- | --- |
| [!UICONTROL Details zur Mediensammlung] | `mediaCollection` | [[!UICONTROL Details zur Mediensammlung]](../../data-types/media-collection-details.md) | Attribute, die sich auf eine Sammlung von Medienelementen beziehen. Verwenden Sie die Mediensammlungsfelder, um Daten zu erfassen und zur weiteren Verarbeitung an andere Adobe-Services zu senden. |
| [!UICONTROL Details zu Medienberichten] | `mediaReporting` | [[!UICONTROL Details zur Medienberichterstattung]](../../data-types/media-reporting-details.md) | Reporting-Details und Metriken, die mit dem Medieninhalt verknüpft sind. * Media Reporting-Felder werden von Adobe-Services verwendet, um die von Benutzern gesendeten Mediensammlungsfelder zu analysieren. Diese Daten werden zusammen mit anderen spezifischen Benutzermetriken berechnet und in Berichten erfasst. |
| [!UICONTROL Liste der heruntergeladenen Inhaltsereignisse der Mediensammlung] | `mediaDownloadedEvents` | [!UICONTROL Array] von [[!UICONTROL mediaEvent]](../../data-types/media-event-information.md) | Ereignisse, die das Herunterladen von Inhalten in der Mediensammlung verfolgen. |

{style="table-layout:auto"}

>[!TIP]
>
>Sie können Felder ausblenden, die nicht von der Media Edge-API verwendet werden. Das Ausblenden dieser Felder erleichtert das Lesen und Verstehen des Schemas, es ist jedoch nicht erforderlich. Diese Felder beziehen sich nur auf die Felder in der Feldergruppe [!UICONTROL MediaAnalytics Interaction Details] . Um die Lesbarkeit in der Experience Platform-Benutzeroberfläche zu verbessern, folgen Sie den Anweisungen in der [Media Analytics-Dokumentation zum Ausblenden nicht verwendeter Felder](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/implementation-edge.html?lang=de#set-up-the-schema-in-adobe-experience-platform).

<!-- 
>[!NOTE]
>
>Schemas contain fields that are not used in every context or situation. They provide a potential blueprint to map an object. Schemas displayed for the Media Edge API Collection or Reporting data types only portray the relevant fields. You can manually select and deselect the fields that you want to use if you intend to use a schema for the Media Edge API interaction. You can find instructions on [hiding unnecessary fields](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/implementation-edge.html?lang=de#set-up-the-schema-in-adobe-experience-platform) in the guide to install Media Analytics with Experience Platform Edge.
 -->
