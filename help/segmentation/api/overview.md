---
title: Handbuch zur Segmentierungs-Service-API
description: Mit der Segmentierungs-Service-API können Entwicklerinnen und Entwickler Segmentierungsvorgänge in Adobe Experience Platform programmgesteuert verwalten. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
role: Developer
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
source-git-commit: f6d700087241fb3a467934ae8e64d04f5c1d98fa
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 5%

---

# Handbuch zur Segmentierungsdienst-API

Mit Adobe Experience Platform [!DNL Segmentation Service] können Sie Zielgruppen über Segmentdefinitionen oder andere Quellen in Adobe Experience Platform aus Ihren [!DNL Real-Time Customer Profile] erstellen.

Die [!DNL Segmentation Service]-API bietet mehrere Endpunkte, mit denen Sie Ihre Segmentierungsvorgänge in [!DNL Experience Platform] programmgesteuert verwalten können. Dieses Übersichtsdokument enthält allgemeine Einführungen zu diesen Endpunkten und Links zu den zugehörigen Endpunkthandbüchern, in denen Sie Details finden. Bevor Sie die einzelnen Endpunkthandbücher lesen, lesen Sie das Handbuch [Erste Schritte](./getting-started.md), um wichtige Informationen zu erforderlichen Kopfzeilen, zum Lesen von Beispiel-API-Aufrufen und mehr zu erhalten.

Informationen zum Anzeigen aller verfügbaren Endpunkte und CRUD-Vorgänge finden Sie in der [API-Referenz zum Segmentierungs-Service](https://www.adobe.io/experience-platform-apis/references/segmentation/).

## Zielgruppen

Zielgruppen sind eine Sammlung von Personen, die ähnliche Verhaltensweisen und/oder Merkmale aufweisen. Diese können entweder mithilfe von Experience Platform oder aus externen Quellen generiert werden. Sie können den `/audiences`-Endpunkt verwenden, um alle Zielgruppen abzurufen, eine neue Zielgruppe zu erstellen, Details zu einer bestimmten Zielgruppe abzurufen, eine bestimmte Zielgruppe zu aktualisieren oder eine bestimmte Zielgruppe zu löschen.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im [Handbuch für Zielgruppen-Endpunkte](./audiences.md).

## Exportaufträge

Exportvorgänge sind asynchrone Prozesse, mit denen Zielgruppensegmentmitglieder in Datensätzen persistiert werden. Sie können den `/export/jobs`-Endpunkt verwenden, um alle Exportvorgänge abzurufen, einen neuen Exportvorgang zu erstellen, Details zu einem bestimmten Exportvorgang abzurufen oder einen bestimmten Exportvorgang abzubrechen.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im [Handbuch zu Exportvorgängen](./export-jobs.md).

## Vorschau und Schätzungen

Die Vorschau bietet eine paginierte Liste von qualifizierten Profilen für eine Segmentdefinition, sodass Sie die Ergebnisse mit dem vergleichen können, was Sie erwarten. Sie können den `/preview`-Endpunkt verwenden, um einen neuen Vorschauauftrag zu erstellen oder die Ergebnisse eines bestimmten Vorschauauftrags nachzuschlagen.

Schätzungen liefern statistische Informationen für Segmentdefinitionen, wie projizierte Zielgruppengröße, Konfidenzintervall und Fehler-Standardabweichung. Sie können den `/estimate`-Endpunkt verwenden, um eine Schätzung einer Segmentdefinition anzuzeigen.

Weitere Informationen zur Verwendung dieser Endpunkte finden Sie im [Handbuch zu Vorschauen und Schätzungen von Endpunkten](./previews-and-estimates.md).

## Zeitpläne

Zeitpläne sind ein Tool, mit dem Batch-Segmentierungsvorgänge automatisch einmal täglich ausgeführt werden können. Sie können den `/config/schedules`-Endpunkt verwenden, um eine Liste von Zeitplänen abzurufen, einen neuen Zeitplan zu erstellen, Details zu einem bestimmten Zeitplan abzurufen, einen bestimmten Zeitplan zu aktualisieren oder einen bestimmten Zeitplan zu löschen.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im [Handbuch zu Endpunkten für Zeitpläne](./schedules.md).

## Segmentdefinitionen

Segmentdefinitionen definieren, welche Profile zu welcher Zielgruppe gehören werden. Sie können den `/segment/definitions`-Endpunkt verwenden, um Segmentdefinitionen zu verwalten.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im [Handbuch zu Segmentdefinitionen-Endpunkten](./segment-definitions.md).

## Segmentaufträge

Segmentaufträge verarbeiten zuvor festgelegte Segmentdefinitionen, um eine Zielgruppe zu generieren. Sie können den `/segment/jobs`-Endpunkt verwenden, um Segmentaufträge zu verwalten.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im [Handbuch zu Segmentvorgängen](./segment-jobs.md).

## Segmentsuche

Die Segmentsuche wird verwendet, um Felder aus verschiedenen Datenquellen zu suchen und sie nahezu in Echtzeit zurückzugeben. Informationen zum Einstieg in die Segmentsuche finden Sie im [Handbuch zum search-Endpunkt](segment-search.md)

## Nächste Schritte

Für die ersten Schritte mit der [!DNL Segmentation Service]-API finden Sie in den verschiedenen Endpunkthandbüchern ausführliche Schritte, wie Sie Aufrufe an die verschiedenen Endpunkte des Services durchführen. Weitere Informationen zum Arbeiten mit Segmenten über die [!DNL Experience Platform]-Benutzeroberfläche finden Sie im [Segmentierungs-Benutzerhandbuch](../ui/overview.md).
