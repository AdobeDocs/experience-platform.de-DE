---
keywords: Experience Platform;Home;beliebte Themen;Segmentierung;Segmentierung;Segmentierungsdienst;API;API;
title: Handbuch zur Segmentdienst-API
topic-legacy: guide
description: Die Segmentierungsdienst-API ermöglicht es Entwicklern, Segmentierungsvorgänge in Adobe Experience Platform programmgesteuert zu verwalten. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 6%

---

# Handbuch zur Segmentdienst-API

[!DNL Adobe Experience Platform Segmentation Service] ermöglicht Ihnen das Erstellen von Segmenten und das Generieren von Audiencen  [!DNL Adobe Experience Platform] aus Ihren  [!DNL Real-time Customer Profile] Daten.

Die [!DNL Segmentation Service]-API bietet mehrere Endpunkte, mit denen Sie Ihre Segmentierungsvorgänge programmgesteuert in [!DNL Experience Platform] verwalten können. Dieses Dokument mit einer Übersicht enthält allgemeine Einführungen zu jedem dieser Endpunkte sowie Links zu den zugehörigen Endpunktleitfäden. Bevor Sie die einzelnen Endpunktleitfäden lesen, lesen Sie im Handbuch [Erste Schritte](./getting-started.md) wichtige Informationen zu erforderlichen Kopfzeilen, zum Lesen von Beispiel-API-Aufrufen und mehr.

Informationen zur Ansicht aller verfügbaren Endpunkte und CRUD-Vorgänge finden Sie unter [Segmentierungsdienst-API-Referenz](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml).

## Exportaufträge

Exportaufträge sind asynchrone Prozesse, die dazu verwendet werden, Segmentmitglieder von Audiencen in Datasets zu erhalten. Mit dem Endpunkt `/export/jobs` können Sie alle Exportaufträge abrufen, einen neuen Exportauftrag erstellen, Details zu einem bestimmten Exportauftrag abrufen oder einen bestimmten Exportauftrag abbrechen.

Weitere Informationen zur Verwendung dieses Endpunktes finden Sie im Endpunkt [Exportaufträge ](./export-jobs.md).

## Vorschauen und Schätzungen

Vorschauen bieten eine paginierte Liste von qualifizierten Profilen für eine Segmentdefinition, mit der Sie die Ergebnisse mit Ihren Erwartungen vergleichen können. Sie können den Endpunkt `/preview` verwenden, um einen neuen Vorschau-Auftrag zu erstellen oder die Ergebnisse eines bestimmten Vorschau-Auftrags nachzuschlagen.

Schätzungen liefern statistische Informationen für Segmentdefinitionen, wie z. B. projizierte Audience, Konfidenzintervall und Standardabweichung. Sie können den Endpunkt `/estimate` verwenden, um eine Schätzung einer Segmentdefinition Ansicht.

Weitere Informationen zur Verwendung dieser Endpunkte finden Sie im Handbuch [Vorschauen und Schätzwerte](./previews-and-estimates.md).

## Zeitpläne

Zeitpläne sind ein Tool, mit dem Stapelsegmentierungsaufträge einmal täglich automatisch ausgeführt werden können. Mit dem Endpunkt `/config/schedules` können Sie eine Liste von Zeitplänen abrufen, einen neuen Zeitplan erstellen, Details zu einem bestimmten Zeitplan abrufen, einen bestimmten Zeitplan aktualisieren oder einen bestimmten Zeitplan löschen.

Weitere Informationen zur Verwendung dieses Endpunktes finden Sie im Endpunkt [PLZ](./schedules.md).

## Segmentdefinitionen

Segmentdefinitionen definieren, welche Profil zu welchen Audiencen gehören. Mit dem Endpunkt `/segment/definitions` können Sie Segmentdefinitionen verwalten.

Weitere Informationen zur Verwendung dieses Endpunktes finden Sie im Endpunktleitfaden [Segmentdefinitionen](./segment-definitions.md).

## Segmentaufträge

Segmentaufträge verarbeiten zuvor festgelegte Segmentdefinitionen, um ein Zielgruppensegment zu erstellen. Sie können den Endpunkt `/segment/jobs` verwenden, um Segmentaufträge zu verwalten.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im Endpunkt [Segmentaufträge-Handbuch](./segment-jobs.md).

## Segmentsuche

Die Segmentsuche dient zum Durchsuchen von Feldern, die in verschiedenen Datenquellen enthalten sind, und zum Zurückgeben in Echtzeit. Weitere Informationen zum Arbeiten mit der Segmentsuche finden Sie im Handbuch [zum Suchendpunkt](segment-search.md)

## Nächste Schritte

Um mit der [!DNL Segmentation Service]-API zu beginnen, lesen Sie die verschiedenen Endpunktleitfäden, um detaillierte Anweisungen zum Aufrufen der verschiedenen Endpunkte des Dienstes zu erhalten. Weitere Informationen zum Arbeiten mit Segmenten mithilfe der [!DNL Platform]-Benutzeroberfläche finden Sie im [Segmentierungsbenutzerleitfaden](../ui/overview.md).
