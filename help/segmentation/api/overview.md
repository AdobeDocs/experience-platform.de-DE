---
title: Handbuch zur Segmentierungsdienst-API
description: Mit der Segmentation Service-API können Entwickler Segmentierungsvorgänge in Adobe Experience Platform programmgesteuert verwalten. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 5%

---

# Handbuch zur Segmentierungsdienst-API

Adobe Experience Platform [!DNL Segmentation Service] ermöglicht Ihnen das Erstellen von Zielgruppen über Segmentdefinitionen oder andere Quellen in Adobe Experience Platform aus Ihrer [!DNL Real-Time Customer Profile] Daten.

Die [!DNL Segmentation Service] Die API bietet mehrere Endpunkte, mit denen Sie Ihre Segmentierungsvorgänge in programmgesteuert verwalten können. [!DNL Experience Platform]. Dieses Übersichtsdokument enthält allgemeine Einführungsoptionen für jeden dieser Endpunkte und Links zu den zugehörigen Endpunkthandbüchern für Details. Lesen Sie vor dem Lesen der einzelnen Endpunkthandbücher die Informationen unter [Erste Schritte](./getting-started.md) für wichtige Informationen zu erforderlichen Kopfzeilen, zum Lesen von Beispiel-API-Aufrufen und mehr.

Informationen zum Anzeigen aller verfügbaren Endpunkte und CRUD-Vorgänge finden Sie im Abschnitt [Referenz zur Segmentierungsdienst-API](https://www.adobe.io/experience-platform-apis/references/segmentation/).

## Zielgruppen

Zielgruppen sind eine Sammlung von Personen, die ähnliche Verhaltensweisen und/oder Merkmale aufweisen. Diese können entweder mithilfe von Platform oder aus externen Quellen generiert werden. Sie können die `/audiences` Endpunkt zum Abrufen aller Zielgruppen, Erstellen einer neuen Zielgruppe, Abrufen von Details einer bestimmten Zielgruppe, Aktualisieren einer bestimmten Zielgruppe oder Löschen einer bestimmten Zielgruppe.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im Abschnitt [Handbuch zum Zielgruppen-Endpunkt](./audiences.md).

## Exportaufträge

Exportaufträge sind asynchrone Prozesse, mit denen Zielgruppensegmentmitglieder in Datensätzen beibehalten werden. Sie können die `/export/jobs` Endpunkt zum Abrufen aller Exportaufträge, Erstellen eines neuen Exportauftrags, Abrufen von Details zu einem bestimmten Exportauftrag oder Abbrechen eines bestimmten Exportauftrags.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im Abschnitt [Endpunktleitfaden für Exportaufträge](./export-jobs.md).

## Vorschau und Schätzungen

Die Vorschau bietet eine paginierte Liste qualifizierter Profile für eine Segmentdefinition, mit der Sie die Ergebnisse mit dem, was Sie erwarten, vergleichen können. Sie können die `/preview` -Endpunkt, um einen neuen Vorschauauftrag zu erstellen oder Ergebnisse eines bestimmten Vorschauauftrags nachzuschlagen.

Schätzungen liefern statistische Informationen für Segmentdefinitionen, z. B. die prognostizierte Zielgruppengröße, das Konfidenzintervall und die Standardabweichung von Fehlern. Sie können die `/estimate` -Endpunkt, um eine Schätzung einer Segmentdefinition anzuzeigen.

Weitere Informationen zur Verwendung dieser Endpunkte finden Sie im Abschnitt [Handbuch zu Vorschau- und Schätzendpunkten](./previews-and-estimates.md).

## Zeitpläne

Zeitpläne sind ein Tool, mit dem Batch-Segmentierungsaufträge einmal täglich automatisch ausgeführt werden können. Sie können die `/config/schedules` Endpunkt zum Abrufen einer Liste von Zeitplänen, Erstellen eines neuen Zeitplans, Abrufen von Details eines bestimmten Zeitplans, Aktualisieren eines bestimmten Zeitplans oder Löschen eines bestimmten Zeitplans.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im Abschnitt [Endpunktleitfaden für Zeitpläne](./schedules.md).

## Segmentdefinitionen

Segmentdefinitionen definieren, welche Profile Teil welcher Zielgruppe sein sollen. Sie können die `/segment/definitions` -Endpunkt zum Verwalten von Segmentdefinitionen.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im Abschnitt [Endleitfaden für Segmentdefinitionen](./segment-definitions.md).

## Segmentaufträge

Segmentaufträge verarbeiten zuvor eingerichtete Segmentdefinitionen zum Generieren einer Zielgruppe. Sie können die `/segment/jobs` -Endpunkt zum Verwalten von Segmentaufträgen.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im Abschnitt [Endpunktleitfaden für Segmentaufträge](./segment-jobs.md).

## Segmentsuche

Die Segmentsuche wird verwendet, um Felder zu durchsuchen, die in verschiedenen Datenquellen enthalten sind, und sie nahezu in Echtzeit zurückzugeben. Informationen zum Arbeiten mit der Segmentsuche finden Sie unter [Suchendpunktanleitung](segment-search.md)

## Nächste Schritte

Erste Schritte mit dem [!DNL Segmentation Service] API finden Sie in den verschiedenen Endpunkthandbüchern detaillierte Anweisungen dazu, wie Sie Aufrufe an die verschiedenen Endpunkte des Dienstes durchführen können. Weitere Informationen zum Arbeiten mit Segmenten finden Sie unter [!DNL Platform] Benutzeroberfläche, siehe [Benutzerhandbuch zur Segmentierung](../ui/overview.md).
