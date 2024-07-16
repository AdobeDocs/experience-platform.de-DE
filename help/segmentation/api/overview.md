---
title: Handbuch zur Segmentierungsdienst-API
description: Mit der Segmentation Service-API können Entwickler Segmentierungsvorgänge in Adobe Experience Platform programmgesteuert verwalten. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
role: Developer
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 5%

---

# Handbuch zur Segmentierungsdienst-API

Mit Adobe Experience Platform [!DNL Segmentation Service] können Sie Zielgruppen mithilfe von Segmentdefinitionen oder anderen Quellen in Adobe Experience Platform aus Ihren [!DNL Real-Time Customer Profile] -Daten erstellen.

Die [!DNL Segmentation Service] -API bietet mehrere Endpunkte, mit denen Sie Ihre Segmentierungsvorgänge in [!DNL Experience Platform] programmgesteuert verwalten können. Dieses Übersichtsdokument enthält allgemeine Einführungsoptionen für jeden dieser Endpunkte und Links zu den zugehörigen Endpunkthandbüchern für Details. Wichtige Informationen zu erforderlichen Kopfzeilen, zum Lesen von Beispiel-API-Aufrufen und mehr finden Sie im Leitfaden [Erste Schritte](./getting-started.md) , bevor Sie die einzelnen Endpunkthandbücher lesen.

Informationen zum Anzeigen aller verfügbaren Endpunkte und CRUD-Vorgänge finden Sie in der [API-Referenz für den Segmentation Service](https://www.adobe.io/experience-platform-apis/references/segmentation/).

## Zielgruppen

Zielgruppen sind eine Sammlung von Personen, die ähnliche Verhaltensweisen und/oder Merkmale aufweisen. Diese können entweder mithilfe von Platform oder aus externen Quellen generiert werden. Mit dem Endpunkt &quot;`/audiences`&quot;können Sie alle Zielgruppen abrufen, eine neue Zielgruppe erstellen, Details einer bestimmten Zielgruppe abrufen, eine bestimmte Zielgruppe aktualisieren oder eine bestimmte Zielgruppe löschen.

Weiterführende Informationen zur Verwendung dieses Endpunkts finden Sie im [Zielgruppen-Endpunkthandbuch](./audiences.md).

## Exportaufträge

Exportaufträge sind asynchrone Prozesse, mit denen Zielgruppensegmentmitglieder in Datensätzen beibehalten werden. Mit dem Endpunkt &quot;`/export/jobs`&quot;können Sie alle Exportaufträge abrufen, einen neuen Exportauftrag erstellen, Details zu einem bestimmten Exportauftrag abrufen oder einen bestimmten Exportauftrag abbrechen.

Weiterführende Informationen zur Verwendung dieses Endpunkts finden Sie im [Endpunkt-Handbuch für Exportaufträge](./export-jobs.md).

## Vorschau und Schätzungen

Die Vorschau bietet eine paginierte Liste qualifizierter Profile für eine Segmentdefinition, mit der Sie die Ergebnisse mit dem, was Sie erwarten, vergleichen können. Sie können den Endpunkt `/preview` verwenden, um einen neuen Vorschauauftrag zu erstellen oder die Ergebnisse eines bestimmten Vorschauauftrags nachzuschlagen.

Schätzungen liefern statistische Informationen für Segmentdefinitionen, z. B. die prognostizierte Zielgruppengröße, das Konfidenzintervall und die Standardabweichung von Fehlern. Sie können den Endpunkt `/estimate` verwenden, um eine Schätzung einer Segmentdefinition anzuzeigen.

Weiterführende Informationen zur Verwendung dieser Endpunkte finden Sie im Leitfaden [Vorschauen und Schätzungen-Endpunkte](./previews-and-estimates.md).

## Zeitpläne

Zeitpläne sind ein Tool, mit dem Batch-Segmentierungsaufträge einmal täglich automatisch ausgeführt werden können. Sie können den Endpunkt `/config/schedules` verwenden, um eine Liste von Zeitplänen abzurufen, einen neuen Zeitplan zu erstellen, Details eines bestimmten Zeitplans abzurufen, einen bestimmten Zeitplan zu aktualisieren oder einen bestimmten Zeitplan zu löschen.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im [Endpunktleitfaden für Zeitpläne](./schedules.md).

## Segmentdefinitionen

Segmentdefinitionen definieren, welche Profile Teil welcher Zielgruppe sein sollen. Sie können den Endpunkt `/segment/definitions` verwenden, um Segmentdefinitionen zu verwalten.

Weiterführende Informationen zur Verwendung dieses Endpunkts finden Sie im [Endpunktleitfaden zu Segmentdefinitionen](./segment-definitions.md) .

## Segmentaufträge

Segmentaufträge verarbeiten zuvor eingerichtete Segmentdefinitionen zum Generieren einer Zielgruppe. Sie können den Endpunkt `/segment/jobs` verwenden, um Segmentaufträge zu verwalten.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im [Endpunktleitfaden für Segmentaufträge](./segment-jobs.md).

## Segmentsuche

Die Segmentsuche wird verwendet, um Felder zu durchsuchen, die in verschiedenen Datenquellen enthalten sind, und sie nahezu in Echtzeit zurückzugeben. Informationen zum Arbeiten mit der Segmentsuche finden Sie im [Suchendpunkt-Handbuch](segment-search.md) .

## Nächste Schritte

Um mit der [!DNL Segmentation Service] -API zu beginnen, lesen Sie die verschiedenen Endpunkthandbücher , um detaillierte Anweisungen dazu zu erhalten, wie Sie Aufrufe an die verschiedenen Endpunkte des Dienstes vornehmen können. Weitere Informationen zum Arbeiten mit Segmenten mithilfe der [!DNL Platform] -Benutzeroberfläche finden Sie im [Benutzerhandbuch zur Segmentierung](../ui/overview.md).
