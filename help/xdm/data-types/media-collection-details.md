---
title: Datentyp „Mediensammlungsdetails“
description: Erfahren Sie mehr über den Datentyp „Details zur Mediensammlung - Experience-Datenmodell (XDM)“.
exl-id: 1faf60f7-6afb-4ce2-b50d-967776a57715
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---

# [!UICONTROL Media Collection Details] Datentyp

[!UICONTROL Media Collection Details] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der wesentliche Details zu Medienwiedergabeereignissen erfasst. Verwenden Sie den Datentyp [!UICONTROL Mediensammlungsdetails], um Details wie die Abspielposition im Inhalt, eindeutige Sitzungskennungen und verschiedene verschachtelte Eigenschaften im Zusammenhang mit der Sitzung zu erfassen. Dieser Datentyp bietet einen umfassenden Überblick über das Wiedergabeerlebnis, der die Verfolgung und Analyse von Mediennutzungsmustern und zugehörigen Ereignissen während Wiedergabesitzungen ermöglicht.

>[!NOTE]
>
>Mediensammlungsfelder erfassen Daten und senden sie zur weiteren Verarbeitung an andere Adobe-Services. Medienberichte -Felder werden von Adobe-Services verwendet, um die von Benutzenden gesendeten Mediensammlungsfelder zu analysieren. Diese Daten werden zusammen mit anderen spezifischen Benutzermetriken berechnet und in Berichten erfasst.

+++Wählen Sie diese Option aus, um ein Diagramm des Datentyps [!UICONTROL Media Collection Details] anzuzeigen.
![Abbildung der [!UICONTROL Informationen zu Mediensammlungsdetails] Datentyp.](../images/data-types/media-collection-details.png)
+++

| Anzeigename | Eigenschaft | Erforderliche Ereignisse für | Datentyp | Beschreibung |
| ------------------------------------ | ----------------------- | ---------------------------------------------------------- | --------- | ----------- |
| [!UICONTROL Advertising-Details] | `advertisingDetails` | `adStart` | [[!UICONTROL advertisingDetails] - Sammlung](./advertising-details-collection.md) | Advertising-Details beziehen sich auf bestimmte Informationen zu Werbeaktivitäten während des Erlebnisereignisses. Dazu gehören Anzeigenmetadaten, Zielgruppenbestimmtheit und Leistungsmetriken. |
| Details zum [!UICONTROL Advertising Pod] | `advertisingPodDetails` | `adBreakStart` | [[!UICONTROL advertisingPodDetails] - Sammlung](./advertising-pod-details-collection.md) | Advertising Pod-Details enthalten Informationen zu Anzeigen-Pods im Erlebnisereignis. Es bietet Einblicke in die Anzeigensequenz, die Inhalte und die Interaktionsmetriken. |
| [!UICONTROL Kapiteldetails] | `chapterDetails` | `chapterStart` | [[!UICONTROL chapterDetails] - Sammlung](./chapter-details-collection.md) | Kapiteldetails erfasst Daten, die sich auf die Kapitel oder segmentierten Teile des Inhalts beziehen. Es enthält Informationen zu Kapitelmarken, Timelines und zugehörigen Metadaten. |
| [!UICONTROL Fehlerdetails] | `errorDetails` | `error` | [[!UICONTROL errorDetails] - Sammlung](./error-details-collection.md) | Fehlerdetails enthalten Informationen zu Fehlern, die während des Erlebnisereignisses aufgetreten sind. Dazu gehören Fehler-Codes, Beschreibungen, Zeitstempel und relevante kontextuelle Daten. |
| [!UICONTROL Liste der Bundesstaaten endet] | `statesEnd` | Verwendet in `statesUpdate` | [[!UICONTROL statesEnd] - Sammlung](./list-of-states-end-collection.md) | End States stellt ein Array bereit, mit dem die Status nach Abschluss des Erlebnisereignisses aufgelistet werden. Es enthält Details zu den endgültigen Wiedergabestatus oder Inhaltsstatus. |
| [!UICONTROL Liste der Status Start] | `statesStart` | Verwendet in `statesUpdate` | [[!UICONTROL statesStart] - Sammlung](./list-of-states-start-collection.md) | „Startstatus“ stellt ein Array bereit, in dem die Status zu Beginn des Erlebnisereignisses aufgelistet werden. Es enthält Daten zur Wiedergabe, zu Benutzeraktionen oder zu Inhaltsdetails. |
| [!UICONTROL QoE-Datendetails] | `qoeDataDetails` | Optional für alle | [[!UICONTROL qoeDataDetails] - Sammlung](./qoe-data-details-collection.md) | QoE-Daten (Quality of Experience) erfassen leistungsbezogene Metriken und Benutzererlebnisdaten. Es bietet Einblicke in Qualität, Reaktionsfähigkeit und Benutzerinteraktionen. |
| [!UICONTROL Sitzungsdetails] | `sessionDetails` | `sessionStart` | [[!UICONTROL sessionDetails] - Sammlung](./session-details-collection.md) | Sitzungsdetails enthalten umfassende Informationen zum Erlebnisereignis, die Einblicke in Benutzerinteraktionen, die Dauer und kontextuelle Daten bieten, die für die Wiedergabesitzung relevant sind. |
| [!UICONTROL Die benutzerdefinierten Metadaten] | `customMetadata` | Optional für `sessionStart`, `adStart`, `sessionStart` | [[!UICONTROL customMetadataDetails] - Sammlung](./custom-metadata-details-collection.md) | Benutzerdefinierte Metadaten enthalten benutzerdefinierte oder zusätzliche Metadaten, die mit dem Erlebnisereignis verknüpft sind. Diese Metadaten ermöglichen die Aufnahme personalisierter oder spezifischer Daten in den Ereigniskontext. |
| [!UICONTROL Mediensitzungs-ID] | `sessionID` | Alle Ereignisse **außer** `sessionStart` und heruntergeladene Inhalte. | Zeichenfolge | Die Mediensitzungs-ID identifiziert eine Instanz eines Inhalts-Streams während einer einzelnen Wiedergabesitzung eindeutig. Sie dient als charakteristische Kennung für das Tracking und die Verwaltung des spezifischen Wiedergabeerlebnisses, das einem Benutzer oder Betrachter zugeordnet ist.<br><em>Hinweis:<em>`sessionId` wird für alle Ereignisse gesendet, mit Ausnahme von `sessionStart` und für alle heruntergeladenen Ereignisse. |
| [!UICONTROL Abspielkopf] | `playhead` | Alle Ereignisse | integer | Der Abspielkopf stellt die aktuelle Wiedergabeposition innerhalb des Medieninhalts dar. Für Live-Inhalte wird die aktuelle Sekunde des Tages angegeben (0 &lt;= Abspielkopf &lt; 86400). Bei aufgezeichneten Inhalten wird die aktuelle Sekunde der Inhaltsdauer (0 &lt;= Abspielkopf &lt; Inhaltslänge) angezeigt. |

{style="table-layout:auto"}
