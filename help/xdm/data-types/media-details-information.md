---
title: Datentyp "Mediendetails-Informationen"
description: Erfahren Sie mehr über den Datentyp "Experience-Datenmodell (XDM) mit Mediendetails-Informationen".
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 2%

---

# [!UICONTROL Informationen zu Mediendetails] Datentyp

[!UICONTROL Informationen zu Mediendetails] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der wichtige Details zu Medienwiedergabeereignissen erfasst. Verwenden Sie die [!UICONTROL Informationen zu Mediendetails] Datentyp zum Erfassen von Details wie der Abspielposition innerhalb des Inhalts, eindeutigen Sitzungs-IDs und verschiedenen verschachtelten Eigenschaften im Zusammenhang mit der Sitzung. Dieser Datentyp bietet einen umfassenden Überblick über das Wiedergabeerlebnis, mit dem sich Medien-Verbrauchsmuster und zugehörige Ereignisse während Wiedergabesitzungen verfolgen und analysieren lassen.

+++Auswählen , um ein Diagramm des [!UICONTROL Informationen zu Mediendetails] Datentyp.
![Ein Diagramm des [!UICONTROL Informationen zu Mediendetails] Datentyp.](../images/data-types/media-details-information.png)
+++

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --------------------- | --------------- | --------- | ----------- |
| [!UICONTROL Abspielleiste] | `playhead` | integer | Die Abspielleiste stellt die aktuelle Wiedergabeposition innerhalb des Medieninhalts dar. Bei Live-Inhalten wird die aktuelle Sekunde des Tages angezeigt (0 &lt;= Abspielleiste &lt; 86400). Bei aufgezeichneten Inhalten spiegelt dies die aktuelle Sekunde der Inhaltsdauer wider (0 &lt;= Abspielleiste &lt; Inhaltsdauer). |
| [!UICONTROL Mediensitzungs-ID] | `sessionID` | Zeichenfolge | Die Mediensitzungs-ID identifiziert eine Instanz eines Inhalts-Streams während einer einzelnen Wiedergabesitzung eindeutig. Sie dient als eindeutige Kennung zum Tracking und Verwalten des spezifischen Wiedergabeerlebnisses, das einem Benutzer oder Viewer zugeordnet ist. |
| [!UICONTROL Sitzungsdetails] | `sessionDetails` | [[!UICONTROL sessionDetails]](./session-details-information.md) | Sitzungsdetails enthalten umfassende Informationen zum Erlebnisereignis und bieten Einblicke in Benutzerinteraktionen, Dauer und Kontextdaten, die für die Wiedergabesitzung relevant sind. |
| [!UICONTROL Werbedetails] | `advertisingDetails` | [[!UICONTROL advertisingDetails]](./advertising-details-information.md) | Werbedetails beziehen sich auf spezifische Informationen zu Werbeaktivitäten während des Erlebnisereignisses. Dazu gehören Anzeigenmetadaten, Targeting-Details und Leistungsmetriken. |
| [!UICONTROL Details der Werbeunterbrechung] | `advertisingPodDetails` | [[!UICONTROL advertisingPodDetails]](./advertising-pod-details-information.md) | Details der Werbeunterbrechung enthalten Informationen zu Anzeigen-Pods innerhalb des Erlebnisereignisses. Sie bietet Einblicke in Anzeigensequenz, Inhalt und Interaktionsmetriken. |
| [!UICONTROL Kapiteldetails] | `chapterDetails` | [[!UICONTROL chapterDetails]](./chapter-details-information.md) | Kapiteldetails erfassen Daten zu den Kapiteln oder segmentierten Teilen des Inhalts. Es enthält Informationen zu Kapitelmarken, Zeitleisten und zugehörigen Metadaten. |
| [!UICONTROL Fehlerdetails] | `errorDetails` | [[!UICONTROL errorDetails]](./error-details-information.md) | Fehlerdetails enthalten Informationen zu Fehlern, die während des Erlebnisereignisses aufgetreten sind. Dazu gehören Fehlercodes, Beschreibungen, Zeitstempel und relevante Kontextdaten. |
| [!UICONTROL QoE-Datendetails] | `qoeDataDetails` | [[!UICONTROL qoeDataDetails]](./qoe-data-details-information.md) | QoE (Quality of Experience) Datendetails erfassen leistungsbezogene Metriken und Benutzererlebnisdaten. Es bietet Einblicke in Qualität, Reaktionsfähigkeit und Benutzerinteraktionen. |
| [!UICONTROL Liste der Statusstarts] | `statesStart` | [[!UICONTROL playerStateData]](./player-state-data-information.md) | Statusstart bietet ein Array, das die Status am Anfang des Erlebnisereignisses auflistet. Es enthält Daten zu Wiedergabe, Benutzeraktionen oder Inhaltsspezifikationen. |
| [!UICONTROL Liste der Statusenden] | `statesEnd` | [[!UICONTROL playerStateData]](./player-state-data-information.md) | Status-Ende bietet ein Array, das die Status beim Abschluss des Erlebnisereignisses auflistet. Es enthält Details zum endgültigen Wiedergabestatus oder Inhaltsstatus. |
| [!UICONTROL Liste der Status] | `states` | [[!UICONTROL playerStateData]](./player-state-data-information.md) | Die Statuseigenschaft ist ein Array, das verschiedene Status während des Erlebnisereignisses erfasst. Diese Eigenschaft bietet sequenzielle Daten zu Wiedergabe, Benutzeraktionen oder Inhaltsänderungen. |
| [!UICONTROL Benutzerdefinierte Metadaten] | `customMetadata` | [[!UICONTROL customMetadataDetails]](./custom-metadata-details-information.md) | Benutzerdefinierte Metadaten enthalten benutzerdefinierte oder zusätzliche Metadaten, die mit dem Erlebnisereignis verknüpft sind. Diese Metadaten ermöglichen die Aufnahme personalisierter oder spezifischer Daten in den Ereigniskontext. |

{style="table-layout:auto"}

Weiterführende Informationen zur Feldergruppe finden Sie im Abschnitt [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json)
