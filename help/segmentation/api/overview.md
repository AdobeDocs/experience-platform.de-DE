---
keywords: Experience Platform; Startseite; beliebte Themen; Segmentierung; Segmentierung; Segmentierungsdienst; API; API;
title: Handbuch zur Segmentierungsdienst-API
topic-legacy: guide
description: Mit der Segmentation Service-API können Entwickler Segmentierungsvorgänge in Adobe Experience Platform programmgesteuert verwalten. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
source-git-commit: 5160bc8057a7f71e6b0f7f2d594ba414bae9d8f6
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 7%

---

# Handbuch zur Segmentierungsdienst-API

[!DNL Adobe Experience Platform Segmentation Service] ermöglicht Ihnen das Erstellen von Segmenten und das Generieren von Zielgruppen in  [!DNL Adobe Experience Platform] aus Ihren  [!DNL Real-time Customer Profile] Daten.

Die [!DNL Segmentation Service]-API bietet mehrere Endpunkte, mit denen Sie Ihre Segmentierungsvorgänge in [!DNL Experience Platform] programmgesteuert verwalten können. Dieses Übersichtsdokument enthält allgemeine Einführungsoptionen für jeden dieser Endpunkte und Links zu den zugehörigen Endpunkthandbüchern für Details. Bevor Sie die einzelnen Endpunkthandbücher lesen, lesen Sie im [Erste Schritte-Handbuch](./getting-started.md) wichtige Informationen zu erforderlichen Kopfzeilen, lesen Sie Beispiel-API-Aufrufe und vieles mehr.

Informationen zum Anzeigen aller verfügbaren Endpunkte und CRUD-Vorgänge finden Sie in der [Segmentation Service API-Referenz](https://www.adobe.io/experience-platform-apis/references/segmentation/).

## Exportaufträge

Exportaufträge sind asynchrone Prozesse, die zum Beibehalten von Zielgruppensegmentmitgliedern in Datensätzen verwendet werden. Mit dem Endpunkt `/export/jobs` können Sie alle Exportaufträge abrufen, einen neuen Exportauftrag erstellen, Details zu einem bestimmten Exportauftrag abrufen oder einen bestimmten Exportauftrag abbrechen.

Weiterführende Informationen zur Verwendung dieses Endpunkts finden Sie im [Endpunktleitfaden für Exportaufträge](./export-jobs.md).

## Vorschau und Schätzung

Die Vorschau bietet eine paginierte Liste qualifizierter Profile für eine Segmentdefinition, mit der Sie die Ergebnisse mit dem, was Sie erwarten, vergleichen können. Sie können den Endpunkt `/preview` verwenden, um einen neuen Vorschauauftrag zu erstellen oder Ergebnisse eines bestimmten Vorschauauftrags nachzuschlagen.

Schätzungen liefern statistische Informationen für Segmentdefinitionen, z. B. die prognostizierte Zielgruppengröße, das Konfidenzintervall und die Standardabweichung von Fehlern. Sie können den Endpunkt `/estimate` verwenden, um eine Schätzung einer Segmentdefinition anzuzeigen.

Weiterführende Informationen zur Verwendung dieser Endpunkte finden Sie im [Handbuch zu Vorschauen und Schätzungen-Endpunkten](./previews-and-estimates.md).

## Zeitpläne

Zeitpläne sind ein Tool, mit dem Batch-Segmentierungsaufträge einmal täglich automatisch ausgeführt werden können. Sie können den Endpunkt `/config/schedules` verwenden, um eine Liste von Zeitplänen abzurufen, einen neuen Zeitplan zu erstellen, Details eines bestimmten Zeitplans abzurufen, einen bestimmten Zeitplan zu aktualisieren oder einen bestimmten Zeitplan zu löschen.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im [Endpunktleitfaden für Zeitpläne](./schedules.md).

## Segmentdefinitionen

Segmentdefinitionen definieren, welche Profile zu welchen Zielgruppensegmenten gehören. Sie können den Endpunkt `/segment/definitions` verwenden, um Segmentdefinitionen zu verwalten.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im [Endpunktleitfaden für Segmentdefinitionen](./segment-definitions.md).

## Segmentaufträge

Segmentaufträge verarbeiten zuvor festgelegte Segmentdefinitionen, um ein Zielgruppensegment zu erstellen. Sie können den Endpunkt `/segment/jobs` verwenden, um Segmentaufträge zu verwalten.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im [Endpunkt-Handbuch für Segmentaufträge](./segment-jobs.md).

## Segmentsuche

Die Segmentsuche wird verwendet, um Felder zu durchsuchen, die in verschiedenen Datenquellen enthalten sind, und sie nahezu in Echtzeit zurückzugeben. Informationen zum Arbeiten mit der Segmentsuche finden Sie im [Suchendpunktleitfaden](segment-search.md) .

## Nächste Schritte

Um mit der API [!DNL Segmentation Service] zu beginnen, lesen Sie die verschiedenen Endpunkthandbücher , um detaillierte Anweisungen dazu zu erhalten, wie Sie Aufrufe an die verschiedenen Endpunkte des Dienstes durchführen können. Weitere Informationen zum Arbeiten mit Segmenten mithilfe der [!DNL Platform]-Benutzeroberfläche finden Sie im [Benutzerhandbuch zur Segmentierung](../ui/overview.md).
