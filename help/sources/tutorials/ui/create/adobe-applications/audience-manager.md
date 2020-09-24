---
keywords: Experience Platform;home;popular topics;Audience manager source connector;Audience Manager;audience manager connector
solution: Experience Platform
title: Erstellen eines Quell-Connectors für Adobe Audience Manager über die Benutzeroberfläche
topic: overview
type: Tutorial
description: Dieses Lernprogramm führt Sie durch die Schritte zum Erstellen von Quell-Connectors für Adobe Audience Manager, um Verbrauchererlebnis-Ereignis-Daten über die Benutzeroberfläche in Platform einzubringen.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 11%

---


# Erstellen eines Quell-Connectors für Adobe Audience Manager über die Benutzeroberfläche

Dieses Lernprogramm führt Sie durch die Schritte zum Erstellen von Quell-Connectors für Adobe Audience Manager, um Verbrauchererlebnis-Ereignis-Daten über die Benutzeroberfläche in Platform einzubringen.

## Erstellen einer Quellverbindung mit Adobe Audience Manager

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann in der linken Navigationsleiste die Option &quot; **Quellen** &quot;, um auf den Quellarbeitsbereich zuzugreifen. Im Anzeigebereich &quot; *Katalog* &quot;werden verschiedene Quellen angezeigt, mit denen Sie Quellverbindungen erstellen können. Jede Quelle zeigt die Anzahl der vorhandenen Verbindungen an, die mit ihnen verbunden sind.

Wählen Sie unter der Kategorie *Adobe Applications* die Option **Adobe Audience Manager** , um eine Informationsleiste auf der rechten Seite des Bildschirms anzuzeigen. Die Informationsleiste enthält eine kurze Beschreibung der ausgewählten Quelle sowie Optionen zur Ansicht der Dokumentation oder zur Verbindung mit der Quelle.

Um einen neuen Quellanschluss für Adobe Audience Manager zu erstellen, klicken Sie auf **Hinzufügen Daten**.

![](../../../../images/tutorials/create/aam/catalog.png)

Das folgende Dialogfeld wird angezeigt. Klicken Sie auf **Verbinden** , um die Verbindung zu erstellen.

![](../../../../images/tutorials/create/aam/connect_full.png)

Wird eine Quellverbindung mit Adobe Audience Manager hergestellt, wird die Seite *Quellcode-Aktivität* für den Audience Manager-Connector angezeigt.

![](../../../../images/tutorials/create/aam/flow.png)

Wenn Sie eingehende Daten des Audience Managers anhalten möchten, können Sie dies tun, indem Sie auf die Dataflow-Liste klicken und deren *Status* in der rechten Spalte &quot; *Eigenschaften* &quot;umschalten.

![](../../../../images/tutorials/create/aam/flow_disable.png)

## Nächste Schritte

Während ein Audience Manager-Datendurchlauf aktiv ist, werden eingehende Daten automatisch in Echtzeit-Kundendaten erfasst. Sie können diese eingehenden Daten jetzt nutzen und mit dem Plattformsegmentierungsdienst Audiencen erstellen. Weitere Informationen finden Sie in den folgenden Dokumenten:

- [Übersicht über das Echtzeit-Kundenprofil](../../../../../profile/home.md)
- [Übersicht über den Segmentierungsdienst](../../../../../segmentation/home.md)