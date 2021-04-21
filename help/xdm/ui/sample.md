---
solution: Experience Platform
title: Musterdaten für ein XDM-Schema in der Benutzeroberfläche generieren
description: Hier erfahren Sie, wie Sie JSON-Beispieldaten auf Grundlage eines vorhandenen Schemas in der Adobe Experience Platform-Benutzeroberfläche generieren.
topic-legacy: user guide
exl-id: e60eedb2-2245-42cd-b574-43caf9e3426c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# Musterdaten für ein XDM-Schema in der Benutzeroberfläche generieren

Um Daten in Adobe Experience Platform zu erfassen, müssen Format und Struktur der Daten einem vorhandenen XDM-Schema (Experience Data Model) entsprechen. Je nach Komplexität des Schemas für einen bestimmten Datensatz kann es schwierig sein, die genaue Form der Daten zu bestimmen, die der Datensatz bei der Erfassung erwartet.

Für jedes Schema, das Sie in der Benutzeroberfläche &quot;Experience Platform&quot;definieren, können Sie ein JSON-Beispielobjekt generieren, das der Struktur des Schemas entspricht. Dieses Objekt kann als Vorlage für alle Daten dienen, die in Datasets mit dem betreffenden Schema erfasst werden.

Wählen Sie in der Benutzeroberfläche &quot;Plattform&quot;im linken Navigationsbereich **[!UICONTROL Schema]** aus. Suchen Sie unter der Registerkarte **[!UICONTROL Durchsuchen]** das Schema, für das Sie Musterdaten generieren möchten. Wählen Sie es aus der Liste aus und die rechte Leiste wird aktualisiert, um Details zum Schema anzuzeigen. Wählen Sie **[!UICONTROL Beispieldatei herunterladen]**.

![](../images/ui/sample/sample-data.png)

Eine JSON-Beispieldatei wird vom Browser heruntergeladen. Sie können diese Datei jetzt als Referenz für die Strukturierung Ihrer Daten verwenden, wenn Sie sie in Datensätze mit diesem Schema einfügen.

## Nächste Schritte

In diesem Handbuch wird beschrieben, wie Sie eine JSON-Beispieldatei aus einem XDM-Schema in der Plattform-Benutzeroberfläche generieren. Informationen zum Generieren von Musterdaten mithilfe der Schema Registry API finden Sie im Handbuch [Beispiel-Daten-Endpunkt](../api/sample-data.md).

Sobald Sie zum Beginn der Dateneingabe bereit sind, lesen Sie das Lernprogramm zu [Zuordnen einer CSV-Datei zu XDM](../../ingestion/tutorials/map-a-csv-file.md), um zu erfahren, wie Sie eine flache Datendatei (z. B. eine CSV-Datei) zu einem XDM-Schema zuordnen und sie in Plattform erfassen. Alternativ können Sie eine [Quellverbindung](../../sources/home.md) einrichten, um Ihre Daten von einer externen Quelle einzufügen und sie XDM zuzuordnen.

Weitere Informationen zu den Funktionen des Arbeitsbereichs [!UICONTROL Schema] in der Benutzeroberfläche finden Sie unter [[!UICONTROL Schema] Arbeitsflächenübersicht](./overview.md).
