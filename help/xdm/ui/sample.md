---
solution: Experience Platform
title: Generieren von Beispieldaten für ein XDM-Schema in der Benutzeroberfläche
description: Erfahren Sie, wie Sie JSON-Beispieldaten basierend auf einem vorhandenen Schema in der Benutzeroberfläche von Adobe Experience Platform generieren.
exl-id: e60eedb2-2245-42cd-b574-43caf9e3426c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 15%

---

# Generieren von Beispieldaten für ein XDM-Schema in der Benutzeroberfläche {#generate-sample-data-for-an-xdm-schema}

>[!CONTEXTUALHELP]
>id="platform_xdm_downloadsamplefile"
>title="Herunterladen einer Beispieldatei"
>abstract="Generieren Sie ein JSON-Beispielobjekt, das der Struktur Ihres ausgewählten Schemas entspricht. Dieses Objekt kann als Vorlage dienen, um sicherzustellen, dass Ihre Daten für die Aufnahme in Datensätze, die dieses Schema verwenden, korrekt formatiert sind. Die JSON-Beispieldatei wird von Ihrem Browser heruntergeladen."

Um Daten in Adobe Experience Platform aufzunehmen, müssen das Format und die Struktur der Daten einem vorhandenen Experience-Datenmodell (XDM)-Schema entsprechen. Je nach Komplexität des Schemas für einen bestimmten Datensatz kann es schwierig sein, die genaue Form der Daten zu bestimmen, die der Datensatz bei der Aufnahme erwartet.

Für jedes Schema, das Sie in der Experience Platform-Benutzeroberfläche definieren, können Sie ein JSON-Beispielobjekt generieren, das der Schemastruktur entspricht. Dieses Objekt kann als Vorlage für alle Daten dienen, die in Datensätze aufgenommen werden, die das betreffende Schema verwenden.

Wählen Sie in der Benutzeroberfläche von Experience Platform im linken Navigationsbereich **[!UICONTROL Schemas]** aus. Suchen Sie auf der Registerkarte **[!UICONTROL Browse]** das Schema, für das Sie Beispieldaten generieren möchten. Wenn Sie sie aus der Liste auswählen, wird die rechte Leiste aktualisiert, um Details zum Schema anzuzeigen. Klicken Sie von hier aus auf **[!UICONTROL Download sample file]**.

![Die Registerkarte „Durchsuchen“ des Arbeitsbereichs „Schemata“ mit einem ausgewählten Schema und hervorgehobener Option „Beispieldatei herunterladen“.](../images/ui/sample/sample-data.png)

Eine JSON-Beispieldatei wird vom Browser heruntergeladen. Sie können diese Datei jetzt als Referenz verwenden, um zu erfahren, wie Sie Ihre Daten strukturieren können, wenn Sie sie in Datensätze aufnehmen, die dieses Schema verwenden.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie eine JSON-Beispieldatei aus einem XDM-Schema in der Experience Platform-Benutzeroberfläche generieren. Informationen zum Generieren von Beispieldaten mithilfe der Schema Registry-API finden Sie im [Handbuch zu Beispieldaten-Endpunkten](../api/sample-data.md).

Wenn Sie bereit sind, mit der Aufnahme von Daten zu beginnen, erfahren Sie in der Anleitung zum [Zuordnen einer CSV-Datei zu XDM](../../ingestion/tutorials/map-csv/overview.md) , wie Sie eine einfache Datendatei (z. B. eine CSV-Datei) einem XDM-Schema zuordnen und in Experience Platform aufnehmen. Alternativ können Sie eine [Quellverbindung“ einrichten](../../sources/home.md) um Ihre Daten aus einer externen Quelle einzubringen und sie XDM zuzuordnen.

Weiterführende Informationen zu den Funktionen von [!UICONTROL Schemas] Workspace in der Benutzeroberfläche finden Sie im Abschnitt Übersicht über [[!UICONTROL Schemas] Workspace ](./overview.md).
