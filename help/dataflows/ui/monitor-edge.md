---
title: Überwachen der Edge-Segmentierung
description: Erfahren Sie, wie Sie mit dem Monitoring-Dashboard den Durchsatz der Edge-Segmentierung beobachten können.
exl-id: 7abba7e8-1f2d-4a21-a93f-8bda7aa4d849
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 6%

---

# Überwachen der Edge-Segmentierung

Sie können das Überwachungs-Dashboard in der Adobe Experience Platform-Benutzeroberfläche verwenden, um die Edge-Segmentierung in Ihrem Unternehmen in Echtzeit zu überwachen. Verwenden Sie diese Funktion, um den Durchsatz Ihrer Edge-Daten transparenter zu gestalten.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Experience Platform voraus:

* [Datenströme](../../datastreams/overview.md): Mit Datenströmen können Sie Experience Platform Edge Network mit Ihrem Datensatz verbinden.
* [Kapazitäten](../../landing/license-usage-and-guardrails/capacity.md): In Experience Platform teilen Ihnen die Kapazitäten mit, ob Ihr Unternehmen eine Ihrer Leitplanken überschritten hat, und erhalten Informationen zur Behebung dieser Probleme.
* [Edge-](../../segmentation/methods/edge-segmentation.md): Bei der Edge-Segmentierung werden Segmentdefinitionen in Adobe Experience Platform sofort ([&#x200B; Edge) ausgewertet](../../landing/edge-and-hub-comparison.md) was Anwendungsfälle für die Personalisierung derselben Seite und der nächsten Seite ermöglicht.

## Zugriff {#access}

Um auf das Überwachungs-Dashboard für den Durchsatz der Edge-Segmentierung zuzugreifen, wählen Sie **[!UICONTROL Monitoring]** im Abschnitt **[!UICONTROL Data management]** und dann **[!UICONTROL Edge]** aus.

![Die Methode für den Zugriff auf das Segmentierungs-Dashboard des Monitor-Edge ist hervorgehoben.](/help/dataflows/assets/ui/monitor-edge/access.png)

Das Überwachungs-Dashboard wird angezeigt. Hier werden Überwachungsmetriken für den Durchsatz des Edge-Streaming angezeigt, ein Diagramm zur Rate des Edge-Streaming-Durchsatzes und eine Datenstromansicht. Diese Metriken können nach Service, Edge und Datum gefiltert werden.

![Die Filteroptionen im Monitoring-Dashboard sind hervorgehoben.](/help/dataflows/assets/ui/monitor-edge/filtering.png)

>[!NOTE]
>
>Die Datenstromansicht wird nur angezeigt **wenn** &quot;[!UICONTROL Edge segmentation throughput]&quot; auswählen.

Wenn Sie nach Service filtern, können Sie auswählen, über welchen Service Sie die Durchsatzinformationen anzeigen möchten. Dazu gehören Services wie Edge-Segmentierung, Datenerfassung, Target, Adobe Journey Optimizer, Offer Decisioning, benutzerdefinierte personalisierte Ziele, Ereignisweiterleitung, Adobe Analytics und Adobe Audience Manager.

Wenn Sie nach Edge filtern, können Sie auswählen, zu welchem Edge Sie Informationen anzeigen möchten. Unterstützte Kanten sind die US-Ostküste, die US-Westküste, Europa, Indien, Singapur, Australien, Japan und die Schweiz. Sie können mehrere Kanten gleichzeitig zur Ansicht auswählen.

Wenn Sie nach Datum filtern, können Sie die Zeitskala zum Filtern Ihrer Ereignisse auswählen. Dieser Zeitraum kann auf 30 Tage festgelegt werden. Alternativ können Sie eine der folgenden vorkonfigurierten Zeitskalen verwenden: [!UICONTROL Last 6 hours], [!UICONTROL Last 12 hours], [!UICONTROL Last 24 hours], [!UICONTROL Last 7 days] und [!UICONTROL Last 30 days].

## Überwachen von Metriken für Edge-Durchsatz

Die Tabelle Metriken enthält spezifische Informationen zum Edge-Durchsatz des ausgewählten Services. Weitere Informationen zu den einzelnen Spalten finden Sie in der folgenden Tabelle.

| Metrik | Beschreibung |
| ------ | ----------- |
| Empfangene Anfragen | Die Anzahl der Anfragen, die von den ausgewählten Edges innerhalb des Zeitrahmens empfangen wurden. |
| Spitzendurchsatz | Die höchste Rate von Anfragen, die von den ausgewählten Edges innerhalb des Zeitrahmens empfangen wurden. |

{style="table-layout:auto"}

## Überwachen des Durchsatzes für die Edge-Segmentierung

Das Überwachungsdiagramm zeigt die Datensätze pro Sekunde an, die von den ausgewählten Edges innerhalb des zugewiesenen Zeitraums empfangen wurden, verglichen mit der maximal zulässigen Kapazität.

![Das Durchsatzdiagramm für die Edge-Segmentierung wird angezeigt.](/help/dataflows/assets/ui/monitor-edge/edge-segmentation-throughput.png)

## Datenstromansicht

>[!NOTE]
>
>Die Datenstromansicht ist **verfügbar** wenn Sie nach Edge-Segmentierungsdurchsatz filtern.

Im Abschnitt mit der Datenstromansicht wird eine Liste der neuesten Datenströme angezeigt, die durch die Ränder der Sandbox übertragen wurden.

![Die Datenstromansicht wird mit Informationen zu den aufgelisteten Datenströmen angezeigt.](/help/dataflows/assets/ui/monitor-edge/datastream-view.png)

| Feld | Beschreibung |
| ----- | ----------- |
| Datenstromname | Der Name des Datenstroms. |
| Datensätze | Der Name der Datensätze, zu denen der Datenstrom gehört. |
| Dienst aktiviert | Die Namen der Services, für die der Datenstrom aktiviert ist. |
| Anfragen | Die Anzahl der Anfragen, die den Datenstrom durchlaufen haben. |
| Spitzendurchsatz | Die höchste Rate von Anfragen, die den Datenstrom durchlaufen haben. |
