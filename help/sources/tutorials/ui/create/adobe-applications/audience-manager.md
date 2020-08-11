---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Quell-Connectors für Adobe Audience Manager über die Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: 41fe3e5b2a830c3182b46b3e0873b1672a1f1b03
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 13%

---


# Erstellen eines Quell-Connectors für Adobe Audience Manager über die Benutzeroberfläche

Dieses Lernprogramm führt Sie durch die Schritte zum Erstellen von Quell-Connectors für Adobe Audience Manager, um Verbrauchererlebnis-Ereignis-Daten über die Benutzeroberfläche in Platform einzubringen.

## Erstellen einer Quellverbindung mit Adobe Audience Manager

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann in der linken Navigationsleiste die Option &quot; **Quellen** &quot;, um auf den Quellarbeitsbereich zuzugreifen. Im Anzeigebereich &quot; *Katalog* &quot;werden verschiedene Quellen angezeigt, mit denen Sie Quellverbindungen erstellen können. Jede Quelle zeigt die Anzahl der vorhandenen Verbindungen an, die mit ihnen verbunden sind.

Wählen Sie unter der Kategorie *Adobe Applications* die Option **Adobe Audience Manager** , um eine Informationsleiste auf der rechten Seite des Bildschirms anzuzeigen. Die Informationsleiste enthält eine kurze Beschreibung der ausgewählten Quelle sowie Optionen zur Ansicht der Dokumentation oder zur Verbindung mit der Quelle.

To create a new source connector for Adobe Audience Manager, click **Add data**.

![](../../../../images/tutorials/create/aam/catalog.png)

Das folgende Dialogfeld wird angezeigt. Click **Connect** to create the connection.

![](../../../../images/tutorials/create/aam/connect_full.png)

If a source connection with Adobe Audience Manager is established, the *Source activity* page for Audience Manager connector be displayed.

![](../../../../images/tutorials/create/aam/flow.png)

Wenn Sie eingehende Daten des Audience Managers anhalten möchten, können Sie dies tun, indem Sie auf die Dataflow-Liste klicken und deren *Status* in der rechten Spalte &quot; *Eigenschaften* &quot;umschalten.

![](../../../../images/tutorials/create/aam/flow_disable.png)

## Nächste Schritte

Während ein Audience Manager-Datendurchlauf aktiv ist, werden eingehende Daten automatisch in Echtzeit-Kundendaten erfasst. Sie können diese eingehenden Daten jetzt nutzen und mit dem Plattformsegmentierungsdienst Audiencen erstellen. Weitere Informationen finden Sie in den folgenden Dokumenten:

- [Übersicht über das Echtzeit-Kundenprofil](../../../../../profile/home.md)
- [Übersicht über den Segmentierungsdienst](../../../../../segmentation/home.md)