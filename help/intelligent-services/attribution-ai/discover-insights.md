---
keywords: Experience Platform;insights;attribution ai;popular topics;attribution ai insights
solution: Experience Platform
title: Gewinnen von Einblicken in Attribution AI
topic: Attribution AI insights
description: Dieses Dokument dient als Handbuch für die Interaktion mit Einblicken der Dienstinstanz in der Benutzeroberfläche von Adobe Intelligent Services.
translation-type: tm+mt
source-git-commit: c30bbaead775e68f869b080e24e18d4a23cda973
workflow-type: tm+mt
source-wordcount: '1183'
ht-degree: 97%

---


# Gewinnen von Einblicken in Attribution AI

Die Instanzen des Attribution AI-Service bieten Einblicke, anhand derer Marketing-Entscheidungen in Bezug auf Marketing-Performance und ROI getroffen und gemessen werden können. Durch die Auswahl einer Dienstinstanz erhalten Sie Visualisierungen und Filter, anhand derer Sie die Auswirkungen jeder Kundeninteraktion in jeder Phase der Customer Journey verstehen können.

Dieses Dokument dient als Handbuch für die Interaktion mit Einblicken der Dienstinstanz in der Benutzeroberfläche von Adobe Intelligent Services.

## Erste Schritte

Um Einblicke für Attribution AI zu verwenden, benötigen Sie eine Dienstinstanz mit einem erfolgreichen Ausführungsstatus. Um eine neue Dienstinstanz zu erstellen, gehen Sie zum [Benutzeroberflächenhandbuch für Attribution AI](./user-guide.md). Wenn Sie kürzlich eine Dienstinstanz erstellt haben und diese sich noch in der Trainings- und Bewertungsphase befindet, warten Sie bitte 24 Stunden, bis sie fertig ist.

## Übersicht über Einblicke von Dienstinstanzen

In the [!DNL Adobe Experience Platform] UI, click **Services** in the left navigation. Der *Dienste*-Browser wird geöffnet und zeigt verfügbare Adobe Intelligent Services an. Klicken Sie im Container für Attribution AI auf **Öffnen**.

![Zugreifen auf Ihre Instanz](./images/insights/open_Attribution_ai.png)

Die Seite des Attribution AI-Service wird angezeigt. Auf dieser Seite werden Dienstinstanzen von Attribution AI aufgelistet und Informationen zu diesen angezeigt, einschließlich des Namens der Instanz, der Konversionsereignisse, der Häufigkeit der Ausführung der Instanz und des Status der letzten Aktualisierung. Klicken Sie zuerst auf den Namen einer Dienstinstanz.

>[!NOTE]
>
>Es können nur Dienstinstanzen ausgewählt werden, die erfolgreiche Bewertungsläufe abgeschlossen haben.

![Instanz erstellen](./images/insights/select-service-instance.png)

Als Nächstes wird die Seite mit den Einblicken für diese Dienstinstanz angezeigt. Hier werden Visualisierungen und eine Reihe von Filtern zur Interaktion mit Ihren Daten bereitgestellt. Die Visualisierungen und Filter werden in diesem Handbuch ausführlicher erläutert.

![Setup-Seite](./images/insights/landing-page.png)

### Details zur Dienstinstanz

Um weitere Details für eine Dienstinstanz anzuzeigen, klicken Sie oben rechts auf **Mehr anzeigen**.

![Mehr anzeigen](./images/insights/show-more.png)

Es wird eine detaillierte Liste angezeigt. Weitere Informationen zu den aufgelisteten Eigenschaften finden Sie im [Benutzerhandbuch für Attribution AI](./user-guide.md).

![Details anzeigen](./images/insights/advanced-details.png)

### Bearbeiten einer Instanz

Um eine Instanz zu bearbeiten, klicken Sie in oben rechts in der Navigation auf *Bearbeiten*.
![Auf Bearbeiten-Schaltfläche klicken](./images/insights/edit-button.png)

Das Dialogfeld „Bearbeiten“ wird angezeigt, in dem Sie die Beschreibung und die Bewertungshäufigkeit der Instanz bearbeiten können. Um die Änderungen zu bestätigen und das Dialogfeld zu schließen, klicken Sie unten rechts auf *Bearbeiten*.

![Bearbeiten-Popup-Fenster](./images/insights/edit-popover.png)

### Mehr Aktionen {#more-actions}

Die Schaltfläche *Mehr Aktionen* befindet sich in der oberen rechten Navigation neben *Bearbeiten*. Wenn Sie auf **Mehr Aktionen** klicken, wird ein Dropdown-Menü geöffnet, in dem Sie eine der folgenden Vorgänge auswählen können:

- **Löschen**: Löscht die Instanz.
- **Zusammenfassungsdaten herunterladen**: Lädt eine CSV-Datei mit den Zusammenfassungsdaten herunter.
- **Auf Bewertungen zugreifen**: Indem Sie auf *Auf Bewertungen zugreifen* klicken, gelangen Sie zum [Tutorial für den Zugriff auf Bewertungen für Attribution AI](./download-scores.md).
- **Ausführungsverlauf anzeigen**: Ein Popup-Fenster mit einer Liste aller mit der Dienstinstanz verbundenen Bewertungsläufe wird angezeigt.

![Mehr Aktionen](./images/insights/more-actions.png)

## Filtern Ihrer Daten

Mithilfe von Attribution AI-Einblicken können Sie Ihre Daten filtern und die Visualisierungen der Benutzeroberfläche automatisch anhand Ihrer ausgewählten Filter aktualisieren.

>[!NOTE]
>
> Standardmäßig ist jeder Filter auf „Alle“ eingestellt, mit Ausnahme des Filters für das *Attributionsmodell*, der auf „Inkrementelle und beeinflusste zugeordnete Konversionen“ eingestellt ist.

### Konversionsereignis

Wenn Sie eine neue Instanz in Attribution AI erstellen, ist eines der erforderlichen Felder „Konversionsereignisse“. Konversionsereignisse sind Unternehmensziele, die die Auswirkungen von Marketing-Aktivitäten wie E-Commerce-Bestellungen, In-Store-Käufen und Website-Besuchen ermitteln.

Innerhalb der Instanz können Sie mit dem Dropdown-Menü *Konversionsereignisse* eines der für Ihre Instanz definierten Ereignisse auswählen, um Ihre Daten zu filtern. Wenn Sie bestimmte Ereignisse auswählen, werden die Visualisierungen der Benutzeroberfläche so geändert, dass nur Konversionen aus diesen Ereignissen gefüllt werden.

![Konversionsereignis](./images/insights/conversion-event.png)

### Attributionsmodell

Durch Klicken auf *Attributionsmodell* wird eine Dropdown-Liste mit allen verfügbaren Attributionsmodellen geöffnet. Sie können mehrere Modelle zum Vergleich der Ergebnisse auswählen. Weitere Informationen zu den verschiedenen Attributionsmodellen und ihrer Funktionsweise finden Sie in der Übersicht über [Attribution AI](./overview.md), die eine Tabelle mit Informationen zu den einzelnen Modellen enthält.

![Attributionsmodell](./images/insights/attribution-model.png)

### Produkt

Mit dem Filter *Produkt* können Sie aus allen Produkten auswählen, die ursprünglich bei der Erstellung Ihrer Instanz berücksichtigt wurden. Klicken Sie auf das Dropdown-Feld und wählen Sie mit der Suchfunktion alle Produkte aus, die Sie vergleichen möchten.

![Produktfilter](./images/insights/product-filter.png)

### Geografie

Der Filter *Geografie* füllt Ländercodes anhand regionenbasierter Modelle. Je nach Ihren Daten ist dieser Filter möglicherweise nicht vorhanden.

>[!NOTE]
>
> Ländercodes sind zwei Zeichen lang. Eine vollständige Liste finden Sie hier: [ISO 3166-1 alpha-2](https://datahub.io/core/country-list).

### Region

>[!NOTE]
>
>Dieser Filter ist nur verfügbar, wenn Sie beim Erstellen Ihrer Dienstinstanz die optionale [regionenbasierte Modellierung](./user-guide.md#region-based-modeling-optional) im Benutzerhandbuch zur Attribution AI-Benutzeroberfläche ausgeführt haben.

Mit diesem Filter können Sie alle Regionen auswählen, die Sie beim Erstellen der Instanz eingerichtet haben.

### Kanal

Wenn Sie auf den Filter *Kanal* klicken, wird eine Dropdown-Liste mit allen verfügbaren Marketing-Kanälen angezeigt. Sie können mehrere Kanäle zum Vergleich auswählen.

![Kanal](./images/insights/channel.png)

### Datumsbereich

Klicken Sie auf das Kalendersymbol, um das Popup-Fenster für den Datumsbereich zu öffnen. Die Start- und Enddaten für die Konversionsereignisse bestimmen die Datenmenge, die in der Benutzeroberfläche angezeigt wird. Sie können den Datumsbereich einschränken oder erweitern, um die Menge der angezeigten Daten zu fokussieren oder zu vergrößern.

![Datumsbereich](./images/insights/display-date-range.png)

## Übersicht über Ihre Daten

Die Karte *Übersicht* zeigt Ihre Konversionen insgesamt nach Attributionsmodell an. Die Gesamtzahl ändert sich je nach Art der Suche anhand der zuvor in diesem Dokument beschriebenen Filter. Durch die Auswahl weiterer Modelle werden der Übersicht zusätzliche Kreise hinzugefügt, jeder mit einer eigenen Farbe entsprechend der Legende.

![Übersicht](./images/insights/Overview.png)

## Wöchentliche Trends

Die Karte *Wöchentliche Trends* unterteilt Ihre Konversionen insgesamt nach dem Datumsbereich, den Sie während des Filtervorgangs festgelegt haben.

![Trends](./images/insights/weekly-trends.png)

Wenn Sie auf die drei Punkte oben rechts auf der Karte *Wöchentliche Trends* klicken, wird eine Dropdown-Liste angezeigt, in der Sie Tages-, Wochen- oder Monatstrends auswählen können.

Wenn Sie den Mauszeiger über die Datenzeile eines bestimmten Attributionsmodells bewegen, wird ein Popup-Fenster angezeigt, das die Gesamtzahl der Konversionen für dieses Datum anzeigt.

![Über Trends bewegen](./images/insights/weekly-trend-hover.png)

## Aufschlüsselung nach Kanal

Die Karte *Aufschlüsselung nach Kanal* wird verwendet, um die Gesamtanzahl der Konversionen im Verhältnis zu den einzelnen Kanälen zu ermitteln. Mit dieser Karte können Entscheidungen über die Effektivität der einzelnen Kanäle und die ROI getroffen werden.

![Aufschlüsseln der Kanäle](./images/insights/channel-breakdown.png)

Wenn Sie auf die drei Punkte oben rechts auf der Karte *Aufschlüsselung nach Kanal* klicken, wird eine Dropdown-Liste geöffnet, in der Sie Daten anhand von Touchpoints füllen können.

![Touchpoints](./images/insights/breakdown-by-touchpoints.png)

## Topkampagnen

Auf der Karte *Topkampagnen* wird ein Überblick über Ihre Kampagnen und die Leistung der Kampagne in den einzelnen Kanälen angezeigt. Diese Karte kann Ihnen helfen, Ihr Team über die Wirksamkeit einer bestimmten Kampagne für einen bestimmten Kanal zu informieren und Aufschluss darüber zu geben, wo weiter investiert werden sollte.

![Topkampagnen](./images/insights/top-campaigns.png)

## Nächste Schritte

Sobald Sie die Daten gefiltert haben und die entsprechenden Informationen anzeigen können, können Sie auf die Bewertungen zuzugreifen. Eine ausführliche Anleitung zum Zugriff auf Ihre Bewertungen finden Sie im [Tutorial für den Zugriff auf Bewertungen in Attribution AI](./download-scores.md). Darüber hinaus können Sie die Zusammenfassungsdaten herunterladen, wie in [Mehr Aktionen](#more-actions) angegeben. Wenn Sie „Zusammenfassungsdaten herunterladen“ auswählen, werden die nach Datumsangaben aggregierten Zusammenfassungsdaten heruntergeladen.

## Zusätzliche Ressourcen

Das folgende Video hilft Ihnen dabei zu lernen, wie Sie die Einblicke in Attribution AI nutzen können, um den ROI von Marketing-Kanälen und -Kampagnen zu verstehen.

>[!VIDEO](https://video.tv.adobe.com/v/32669?learn=on&quality=12)