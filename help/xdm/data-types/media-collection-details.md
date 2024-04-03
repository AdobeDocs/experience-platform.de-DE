---
title: Datentyp "Mediensammlungsdetails"
description: Erfahren Sie mehr über den Datentyp "Experience-Datenmodell (XDM) für Mediensammlungsdetails".
source-git-commit: fe239bee3c853d43c04200092f59537dfeb00c87
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---

# [!UICONTROL Details zur Mediensammlung] Datentyp

[!UICONTROL Details zur Mediensammlung] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der wichtige Details zu Medienwiedergabeereignissen erfasst. Verwenden Sie die [!UICONTROL Details zur Mediensammlung] Datentyp zum Erfassen von Details wie der Abspielposition innerhalb des Inhalts, eindeutigen Sitzungs-IDs und verschiedenen verschachtelten Eigenschaften im Zusammenhang mit der Sitzung. Dieser Datentyp bietet einen umfassenden Überblick über das Wiedergabeerlebnis, das die Verfolgung und Analyse von Mediennutzungsmustern und zugehörigen Ereignissen während Wiedergabesitzungen ermöglicht.

>[!NOTE]
>
>Mediensammlungsfelder erfassen Daten und senden sie zur weiteren Verarbeitung an andere Adobe-Dienste. Die Felder für die Medienberichte werden von Adobe-Diensten verwendet, um die von Benutzern gesendeten Mediensammlungsfelder zu analysieren. Diese Daten werden zusammen mit anderen spezifischen Benutzermetriken berechnet und in Berichten verwendet.

+++Auswählen , um ein Diagramm des [!UICONTROL Details zur Mediensammlung] Datentyp.
![Ein Diagramm des [!UICONTROL Informationen zur Mediensammlung] Datentyp.](../images/data-types/media-collection-details.png)
+++

| Anzeigename | Eigenschaft | Für | Datentyp | Beschreibung |
| ------------------------------------ | ----------------------- | ---------------------------------------------------------- | --------- | ----------- |
| [!UICONTROL Werbedetails] | `advertisingDetails` | `adStart` | [[!UICONTROL advertisingDetails] - Sammlung](./advertising-details-collection.md) | Werbedetails beziehen sich auf spezifische Informationen zu Werbeaktivitäten während des Erlebnisereignisses. Dazu gehören Anzeigenmetadaten, Targeting-Details und Leistungsmetriken. |
| [!UICONTROL Details der Werbeunterbrechung] | `advertisingPodDetails` | `adBreakStart` | [[!UICONTROL advertisingPodDetails] - Sammlung](./advertising-pod-details-collection.md) | Details der Werbeunterbrechung enthalten Informationen zu Anzeigen-Pods innerhalb des Erlebnisereignisses. Sie bietet Einblicke in Anzeigensequenz, Inhalt und Interaktionsmetriken. |
| [!UICONTROL Kapiteldetails] | `chapterDetails` | `chapterStart` | [[!UICONTROL chapterDetails] - Sammlung](./chapter-details-collection.md) | Kapiteldetails erfassen Daten zu den Kapiteln oder segmentierten Teilen des Inhalts. Es enthält Informationen zu Kapitelmarken, Zeitleisten und zugehörigen Metadaten. |
| [!UICONTROL Fehlerdetails] | `errorDetails` | `error` | [[!UICONTROL errorDetails] - Sammlung](./error-details-collection.md) | Fehlerdetails enthalten Informationen zu Fehlern, die während des Erlebnisereignisses aufgetreten sind. Dazu gehören Fehlercodes, Beschreibungen, Zeitstempel und relevante Kontextdaten. |
| [!UICONTROL Liste der Statusenden] | `statesEnd` | Verwendet in `statesUpdate` | [[!UICONTROL statesEnd] - Sammlung](./list-of-states-end-collection.md) | Status-Ende bietet ein Array, das die Status beim Abschluss des Erlebnisereignisses auflistet. Es enthält Details zum endgültigen Wiedergabestatus oder Inhaltsstatus. |
| [!UICONTROL Liste der Statusstarts] | `statesStart` | Verwendet in `statesUpdate` | [[!UICONTROL statesStart] - Sammlung](./list-of-states-start-collection.md) | Statusstart bietet ein Array, das die Status am Anfang des Erlebnisereignisses auflistet. Es enthält Daten zu Wiedergabe, Benutzeraktionen oder Inhaltsspezifikationen. |
| [!UICONTROL QoE-Datendetails] | `qoeDataDetails` | Optional für alle | [[!UICONTROL qoeDataDetails] - Sammlung](./qoe-data-details-collection.md) | QoE (Quality of Experience) Datendetails erfassen leistungsbezogene Metriken und Benutzererlebnisdaten. Es bietet Einblicke in Qualität, Reaktionsfähigkeit und Benutzerinteraktionen. |
| [!UICONTROL Sitzungsdetails] | `sessionDetails` | `sessionStart` | [[!UICONTROL sessionDetails] - Sammlung](./session-details-collection.md) | Sitzungsdetails enthalten umfassende Informationen zum Erlebnisereignis und bieten Einblicke in Benutzerinteraktionen, Dauer und Kontextdaten, die für die Wiedergabesitzung relevant sind. |
| [!UICONTROL Benutzerdefinierte Metadaten] | `customMetadata` | Optional für `sessionStart`, `adStart`, `sessionStart` | [[!UICONTROL customMetadataDetails] - Sammlung](./custom-metadata-details-collection.md) | Benutzerdefinierte Metadaten enthalten benutzerdefinierte oder zusätzliche Metadaten, die mit dem Erlebnisereignis verknüpft sind. Diese Metadaten ermöglichen die Aufnahme personalisierter oder spezifischer Daten in den Ereigniskontext. |
| [!UICONTROL Mediensitzungs-ID] | `sessionID` | Alle Ereignisse **Außer** `sessionStart` und heruntergeladenen Inhalten. | Zeichenfolge | Die Mediensitzungs-ID identifiziert eine Instanz eines Inhalts-Streams während einer einzelnen Wiedergabesitzung eindeutig. Sie dient als eindeutige Kennung zum Tracking und Verwalten des spezifischen Wiedergabeerlebnisses, das einem Benutzer oder Viewer zugeordnet ist.<br><em>Hinweis:<em>`sessionId` wird für alle Ereignisse gesendet, mit Ausnahme von `sessionStart` und für alle heruntergeladenen Ereignisse. |
| [!UICONTROL Abspielleiste] | `playhead` | Alle Ereignisse | integer | Die Abspielleiste stellt die aktuelle Wiedergabeposition innerhalb des Medieninhalts dar. Bei Live-Inhalten wird die aktuelle Sekunde des Tages angezeigt (0 &lt;= Abspielleiste &lt; 86400). Bei aufgezeichneten Inhalten spiegelt dies die aktuelle Sekunde der Inhaltsdauer wider (0 &lt;= Abspielleiste &lt; Inhaltsdauer). |

{style="table-layout:auto"}
