---
title: Datentyp „Media Reporting Details“
description: Erfahren Sie mehr über den Datentyp Experience-Datenmodell (XDM) für Details zur Medienberichterstattung.
exl-id: e8bf20a9-9ac0-4339-8200-5d6d9328ce3b
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 2%

---

# Datentyp [!UICONTROL Media Reporting]Details

>[!NOTE]
>
>Mediensammlungsfelder erfassen Daten und senden sie zur weiteren Verarbeitung an andere Adobe-Services. Medienberichte -Felder werden von Adobe-Services verwendet, um die von Benutzenden gesendeten Mediensammlungsfelder zu analysieren. Diese Daten werden zusammen mit anderen spezifischen Benutzermetriken berechnet und in Berichten erfasst.

[!UICONTROL Media Reporting Details] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der wesentliche Details zu Medienwiedergabeereignissen erfasst. Verwenden Sie den Datentyp [!UICONTROL Media Reporting], um Details wie die Abspielposition innerhalb des Inhalts, eindeutige Sitzungskennungen und verschiedene verschachtelte Eigenschaften im Zusammenhang mit der Sitzung zu erfassen. Dieser Datentyp bietet einen umfassenden Überblick über das Wiedergabeerlebnis, der die Verfolgung und Analyse von Mediennutzungsmustern und zugehörigen Ereignissen während Wiedergabesitzungen ermöglicht.

>[!NOTE]
>
>Die unten genannten Felder werden nicht direkt zum Erstellen von Anfragen verwendet. Stattdessen wird die Sammlung von Feldern, die an Adobe Experience Platform oder Adobe Analytics gesendet werden, aus Ihren Anfragedaten zusammengestellt, und Metriken werden dann von der Server-Infrastruktur integriert oder verarbeitet. Während Platform verschiedene Typen Ihrer Benutzerereignisse erfasst, konzentrieren sich die an Sie zurückgegebenen Berichte auf bestimmte Ereignisse wie `media.sessionStart`, `media.adStart` und `media.sessionComplete`. Das bedeutet, dass Sie während der Erfassung zwar 12 Ereignistypen übertragen, Ihre Berichte jedoch nur Aufschlüsselungen auf der Grundlage der fünf unten aufgeführten Ereignisse anzeigen.

+++Wählen Sie diese Option aus, um ein Diagramm des Datentyps [!UICONTROL Media Reporting-]&quot; anzuzeigen.
![Abbildung des Datentyps [!UICONTROL Details zur Medienberichterstattung].](../images/data-types/media-reporting-details.png)
+++

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --------------------- | --------------- | --------- | ----------- |
| [!UICONTROL Advertising-Details] | `advertisingDetails` | [[!UICONTROL advertisingDetails]](./advertising-details-reporting.md) | Advertising-Details beziehen sich auf bestimmte Informationen zu Werbeaktivitäten während des Erlebnisereignisses. Dazu gehören Anzeigenmetadaten, Zielgruppenbestimmtheit und Leistungsmetriken. |
| Details zum [!UICONTROL Advertising Pod] | `advertisingPodDetails` | [[!UICONTROL advertisingPodDetails]](./advertising-pod-details-reporting.md) | Advertising Pod-Details enthalten Informationen zu Anzeigen-Pods im Erlebnisereignis. Es bietet Einblicke in die Anzeigensequenz, die Inhalte und die Interaktionsmetriken. |
| [!UICONTROL Kapiteldetails] | `chapterDetails` | [[!UICONTROL chapterDetails]](./chapter-details-reporting.md) | Kapiteldetails erfasst Daten, die sich auf die Kapitel oder segmentierten Teile des Inhalts beziehen. Es enthält Informationen zu Kapitelmarken, Timelines und zugehörigen Metadaten. |
| [!UICONTROL Liste der Bundesstaaten] | `states` | [[!UICONTROL playerStateData]](./player-state-data-reporting.md) | Die States-Eigenschaft ist ein Array, das verschiedene Status im gesamten Erlebnisereignis erfasst. Diese Eigenschaft stellt sequenzielle Daten zur Wiedergabe, zu Benutzeraktionen oder zu Inhaltsänderungen bereit. |
| [!UICONTROL QoE-Datendetails] | `qoeDataDetails` | [[!UICONTROL qoeDataDetails]](./qoe-data-details-reporting.md) | QoE-Daten (Quality of Experience) erfassen leistungsbezogene Metriken und Benutzererlebnisdaten. Es bietet Einblicke in Qualität, Reaktionsfähigkeit und Benutzerinteraktionen. |
| [!UICONTROL Sitzungsdetails] | `sessionDetails` | [[!UICONTROL sessionDetails]](./session-details-reporting.md) | Sitzungsdetails enthalten umfassende Informationen zum Erlebnisereignis, die Einblicke in Benutzerinteraktionen, die Dauer und kontextuelle Daten bieten, die für die Wiedergabesitzung relevant sind. |
| [!UICONTROL Die benutzerdefinierten Metadaten] | `customMetadata` | [[!UICONTROL customMetadataDetails]](./custom-metadata-details-reporting.md) | Benutzerdefinierte Metadaten enthalten benutzerdefinierte oder zusätzliche Metadaten, die mit dem Erlebnisereignis verknüpft sind. Diese Metadaten ermöglichen die Aufnahme personalisierter oder spezifischer Daten in den Ereigniskontext. |
| [!UICONTROL Abspielkopf] | `playhead` | integer | Der Abspielkopf stellt die aktuelle Wiedergabeposition innerhalb des Medieninhalts dar. Für Live-Inhalte wird die aktuelle Sekunde des Tages angegeben (0 &lt;= Abspielkopf &lt; 86400). Bei aufgezeichneten Inhalten wird die aktuelle Sekunde der Inhaltsdauer (0 &lt;= Abspielkopf &lt; Inhaltslänge) angezeigt. |

{style="table-layout:auto"}
