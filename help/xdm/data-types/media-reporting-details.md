---
title: Datentyp Medien-Reporting
description: Erfahren Sie mehr über den Datentyp "Experience-Datenmodell (XDM) für Medienberichte-Details".
exl-id: e8bf20a9-9ac0-4339-8200-5d6d9328ce3b
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 2%

---

# Datentyp [!UICONTROL Medien-Reporting-Details]

>[!NOTE]
>
>Mediensammlungsfelder erfassen Daten und senden sie zur weiteren Verarbeitung an andere Adobe-Dienste. Die Felder für die Medienberichte werden von Adobe-Diensten verwendet, um die von Benutzern gesendeten Mediensammlungsfelder zu analysieren. Diese Daten werden zusammen mit anderen spezifischen Benutzermetriken berechnet und in Berichten verwendet.

[!UICONTROL Medien-Reporting-Details] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der wichtige Details zu Medienwiedergabeereignissen erfasst. Verwenden Sie den Datentyp [!UICONTROL Medien-Reporting-Details] , um Details wie die Abspielposition im Inhalt, eindeutige Sitzungs-IDs und verschiedene verschachtelte Eigenschaften im Zusammenhang mit der Sitzung zu erfassen. Dieser Datentyp bietet einen umfassenden Überblick über das Wiedergabeerlebnis, das die Verfolgung und Analyse von Mediennutzungsmustern und zugehörigen Ereignissen während Wiedergabesitzungen ermöglicht.

>[!NOTE]
>
>Die unten genannten Felder werden nicht direkt zum Erstellen von Anforderungen verwendet. Stattdessen wird die an Adobe Experience Platform oder Adobe Analytics gesendete Feldsammlung aus Ihren Anfragedaten zusammengestellt und Metriken werden dann von der Serverinfrastruktur integriert oder verarbeitet. Während Platform verschiedene Typen Ihrer Benutzerereignisse erfasst, konzentrieren sich die an Sie zurückgegebenen Berichte auf bestimmte Ereignisse wie `media.sessionStart`, `media.adStart` und `media.sessionComplete`. Das bedeutet, dass Sie zwar 12 Arten von Ereignissen während der Erfassung übertragen, Ihre Berichte jedoch nur Aufschlüsselungen nach den fünf unten aufgeführten Ereignissen enthalten.

+++Auswählen , um ein Diagramm des Datentyps [!UICONTROL Medien-Berichtsdetails] anzuzeigen.
![Ein Diagramm des Datentyps [!UICONTROL Medien-Berichterstellungsdetails].](../images/data-types/media-reporting-details.png)
+++

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --------------------- | --------------- | --------- | ----------- |
| [!UICONTROL Advertising-Details] | `advertisingDetails` | [[!UICONTROL advertisingDetails]](./advertising-details-reporting.md) | Advertising-Details beziehen sich auf spezifische Informationen zu Werbeaktivitäten während des Erlebnisereignisses. Dazu gehören Anzeigenmetadaten, Targeting-Details und Leistungsmetriken. |
| [!UICONTROL Advertising-Werbeunterbrechungsdetails] | `advertisingPodDetails` | [[!UICONTROL advertisingPodDetails]](./advertising-pod-details-reporting.md) | Advertising-Werbeunterbrechungsdetails enthalten Informationen zu Anzeigen-Pods innerhalb des Erlebnisereignisses. Sie bietet Einblicke in Anzeigensequenz, Inhalt und Interaktionsmetriken. |
| [!UICONTROL Kapiteldetails] | `chapterDetails` | [[!UICONTROL chapterDetails]](./chapter-details-reporting.md) | Kapiteldetails erfassen Daten zu den Kapiteln oder segmentierten Teilen des Inhalts. Es enthält Informationen zu Kapitelmarken, Zeitleisten und zugehörigen Metadaten. |
| [!UICONTROL Liste der Status] | `states` | [[!UICONTROL playerStateData]](./player-state-data-reporting.md) | Die Statuseigenschaft ist ein Array, das verschiedene Status während des Erlebnisereignisses erfasst. Diese Eigenschaft bietet sequenzielle Daten zu Wiedergabe, Benutzeraktionen oder Inhaltsänderungen. |
| [!UICONTROL QoE-Datendetails] | `qoeDataDetails` | [[!UICONTROL qoeDataDetails]](./qoe-data-details-reporting.md) | QoE (Quality of Experience) Datendetails erfassen leistungsbezogene Metriken und Benutzererlebnisdaten. Es bietet Einblicke in Qualität, Reaktionsfähigkeit und Benutzerinteraktionen. |
| [!UICONTROL Sitzungsdetails] | `sessionDetails` | [[!UICONTROL sessionDetails]](./session-details-reporting.md) | Sitzungsdetails enthalten umfassende Informationen zum Erlebnisereignis und bieten Einblicke in Benutzerinteraktionen, Dauer und Kontextdaten, die für die Wiedergabesitzung relevant sind. |
| [!UICONTROL Die benutzerdefinierten Metadaten] | `customMetadata` | [[!UICONTROL customMetadataDetails]](./custom-metadata-details-reporting.md) | Benutzerdefinierte Metadaten enthalten benutzerdefinierte oder zusätzliche Metadaten, die mit dem Erlebnisereignis verknüpft sind. Diese Metadaten ermöglichen die Aufnahme personalisierter oder spezifischer Daten in den Ereigniskontext. |
| [!UICONTROL Abspielleiste] | `playhead` | integer | Die Abspielleiste stellt die aktuelle Wiedergabeposition innerhalb des Medieninhalts dar. Bei Live-Inhalten wird die aktuelle Sekunde des Tages angezeigt (0 &lt;= Abspielleiste &lt; 86400). Bei aufgezeichneten Inhalten spiegelt dies die aktuelle Sekunde der Inhaltsdauer wider (0 &lt;= Abspielleiste &lt; Inhaltsdauer). |

{style="table-layout:auto"}
