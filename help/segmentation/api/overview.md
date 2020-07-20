---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Entwicklerhandbuch zum Adobe Experience Platform Segmentation Service
topic: guide
translation-type: tm+mt
source-git-commit: aff81a4f3243ef77cbdfc776220a5de46e360084
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 6%

---


# Entwicklerhandbuch zur Adobe Experience Platform Segmentation Service API

[!DNL Adobe Experience Platform Segmentation Service] ermöglicht Ihnen das Erstellen von Segmenten und das Generieren von Audiencen [!DNL Adobe Experience Platform] aus Ihren [!DNL Real-time Customer Profile] Daten.

Die [!DNL Segmentation Service] API bietet mehrere Endpunkte, mit denen Sie Ihre Segmentierungsvorgänge programmgesteuert verwalten können [!DNL Experience Platform]. Dieses Dokument mit einer Übersicht enthält allgemeine Einführungen zu jedem dieser Endpunkte sowie Links zu den zugehörigen Endpunktleitfäden. Bevor Sie die einzelnen Endpunktleitfäden lesen, lesen Sie in der Anleitung [zu den ersten Schritten](./getting-started.md) wichtige Informationen zu erforderlichen Kopfzeilen, zum Lesen von Beispiel-API-Aufrufen und mehr.

Informationen zur Ansicht aller verfügbaren Endpunkte und CRUD-Vorgänge finden Sie in der [Segmentierungsdienst-API-Referenz](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml).

## Exportaufträge

Exportaufträge sind asynchrone Prozesse, die dazu verwendet werden, Segmentmitglieder von Audiencen in Datasets zu erhalten. Mit dem `/export/jobs` Endpunkt können Sie alle Exportaufträge abrufen, einen neuen Exportauftrag erstellen, Details zu einem bestimmten Exportauftrag abrufen oder einen bestimmten Exportauftrag abbrechen.

For more information on using this endpoint, please read the [export jobs endpoint guide](./export-jobs.md).

## Vorschauen und Schätzungen

Vorschauen bieten eine paginierte Liste von qualifizierten Profilen für eine Segmentdefinition, mit der Sie die Ergebnisse mit Ihren Erwartungen vergleichen können. Sie können den `/preview` Endpunkt verwenden, um einen Auftrag für eine neue Vorschau zu erstellen oder die Ergebnisse eines bestimmten Auftrags für eine bestimmte Vorschau nachzuschlagen.

Schätzungen liefern statistische Informationen für Segmentdefinitionen, wie z. B. projizierte Audience, Konfidenzintervall und Standardabweichung. Sie können den `/estimate` Endpunkt verwenden, um eine Schätzung einer Segmentdefinition Ansicht.

Weitere Informationen zur Verwendung dieser Endpunkte finden Sie im Handbuch [Vorschauen und Schätzungen-Endpunkte](./previews-and-estimates.md).

## Zeitpläne

Zeitpläne sind ein Tool, mit dem Stapelsegmentierungsaufträge einmal täglich automatisch ausgeführt werden können. Mit dem `/config/schedules` Endpunkt können Sie eine Liste von Zeitplänen abrufen, einen neuen Zeitplan erstellen, Details zu einem bestimmten Zeitplan abrufen, einen bestimmten Zeitplan aktualisieren oder einen bestimmten Zeitplan löschen.

For more information on using this endpoint, please read the [schedules endpoint guide](./schedules.md).

## Segmentdefinitionen

Segmentdefinitionen definieren, welche Profil zu welchen Audiencen gehören. Mit dem `/segment/definitions` Endpunkt können Sie Segmentdefinitionen verwalten.

For more information on using this endpoint, please read the [segment definitions endpoint guide](./segment-definitions.md).

## Segmentaufträge

Segmentaufträge verarbeiten zuvor festgelegte Segmentdefinitionen, um ein Zielgruppensegment zu erstellen. Mit dem `/segment/jobs` Endpunkt können Sie Segmentaufträge verwalten.

For more information on using this endpoint, please read the [segment jobs endpoint guide](./segment-jobs.md).

## Segmentsuche

Die Segmentsuche dient zum Durchsuchen von Feldern, die in verschiedenen Datenquellen enthalten sind, und zum Zurückgeben in Echtzeit. Weitere Informationen zum Arbeiten mit der Segmentsuche finden Sie im Handbuch [für den Suchendpunkt](segment-search.md)

## Nächste Schritte

Um mit der [!DNL Segmentation Service] API zu beginnen, lesen Sie die verschiedenen Endpunktleitfäden, um detaillierte Schritte zum Aufrufen der verschiedenen Endpunkte des Dienstes zu erhalten. To learn more about working with segments using the [!DNL Platform] UI, see the [Segmentation user guide](../ui/overview.md).