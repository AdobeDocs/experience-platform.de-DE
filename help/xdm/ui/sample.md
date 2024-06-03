---
solution: Experience Platform
title: Generieren von Beispieldaten für ein XDM-Schema in der Benutzeroberfläche
description: Erfahren Sie, wie Sie JSON-Beispieldaten basierend auf einem vorhandenen Schema in der Benutzeroberfläche von Adobe Experience Platform generieren.
exl-id: e60eedb2-2245-42cd-b574-43caf9e3426c
source-git-commit: 19a9341a9f53559fe3f619b2f157015e53b25b64
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 1%

---

# Generieren von Beispieldaten für ein XDM-Schema in der Benutzeroberfläche {#generate-sample-data-for-an-xdm-schema}

>[!CONTEXTUALHELP]
>id="platform_xdm_downloadsamplefile"
>title="Musterdatei herunterladen"
>abstract="Generieren Sie ein JSON-Beispielobjekt, das der Struktur Ihres ausgewählten Schemas entspricht. Dieses Objekt kann als Vorlage dienen, um sicherzustellen, dass Ihre Daten für die Aufnahme in Datensätze, die dieses Schema verwenden, korrekt formatiert sind. Die JSON-Beispieldatei wird von Ihrem Browser heruntergeladen."

Um Daten in Adobe Experience Platform zu erfassen, müssen Format und Datenstruktur einem vorhandenen Experience-Datenmodell (XDM)-Schema entsprechen. Je nach Komplexität des Schemas für einen bestimmten Datensatz kann es schwierig sein, die genaue Form der Daten zu bestimmen, die der Datensatz bei der Erfassung erwartet.

Für jedes Schema, das Sie in der Experience Platform-Benutzeroberfläche definieren, können Sie ein JSON-Beispielobjekt generieren, das der Schemastruktur entspricht. Dieses Objekt kann als Vorlage für alle Daten dienen, die in Datensätze aufgenommen werden, die das betreffende Schema verwenden.

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Schemas]** in der linken Navigation. Unter dem **[!UICONTROL Durchsuchen]** Suchen Sie nach dem Schema, für das Sie Beispieldaten generieren möchten. Wählen Sie es aus der Liste aus und die rechte Leiste wird aktualisiert, um Details zum Schema anzuzeigen. Wählen Sie von hier aus **[!UICONTROL Beispieldatei herunterladen]**.

![Im Tab Durchsuchen des Arbeitsbereichs Schemas wird ein ausgewähltes Schema ausgewählt und die Beispieldatei für den Download hervorgehoben.](../images/ui/sample/sample-data.png)

Eine JSON-Beispieldatei wird vom Browser heruntergeladen. Sie können diese Datei jetzt als Referenz verwenden, um Ihre Daten bei der Aufnahme in Datensätze zu strukturieren, die dieses Schema verwenden.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie eine JSON-Beispieldatei aus einem XDM-Schema in der Platform-Benutzeroberfläche generieren. Informationen zum Generieren von Beispieldaten mithilfe der Schema Registry-API finden Sie in der [Beispiel-Daten-Endpunkthandbuch](../api/sample-data.md).

Sobald Sie bereit sind, Daten zu erfassen, finden Sie im Tutorial zu [Zuordnen einer CSV-Datei zu XDM](../../ingestion/tutorials/map-csv/overview.md) , um zu erfahren, wie Sie eine flache Datendatei (z. B. ein CSV) einem XDM-Schema zuordnen und in Platform erfassen. Alternativ können Sie eine [Quellverbindung](../../sources/home.md) , um Ihre Daten aus einer externen Quelle einzubringen und sie XDM zuzuordnen.

Weitere Informationen zu den Funktionen der [!UICONTROL Schemas] Arbeitsbereich der Benutzeroberfläche, siehe [[!UICONTROL Schemas] Arbeitsbereich - Übersicht](./overview.md).
