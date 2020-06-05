---
keywords: Experience Platform;insights;attribution ai;popular topics
solution: Experience Platform
title: Erkenntnisse über Attribution AI
topic: Attribution AI insights
translation-type: tm+mt
source-git-commit: 83e74ad93bdef056c8aef07c9d56313af6f4ddfd
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 1%

---


# Erkenntnisse über Attribution AI

Zuordnungs-AI-Dienstinstanzen bieten Einblicke, die bei der Entscheidungsfindung und Messung von Marketingentscheidungen im Zusammenhang mit der Marketingleistung und der Kapitalrendite genutzt werden können. Die Auswahl einer Dienstinstanz bietet Visualisierungen und Filter, die Ihnen helfen, die Auswirkungen jeder Kundeninteraktion in jeder Phase der Customer Journey zu verstehen.

Dieses Dokument dient als Leitfaden für die Interaktion mit Dienstinstanzinformationen in der Benutzeroberfläche von Adobe Intelligent Services.

## Erste Schritte

Um Einblicke in Attribution AI zu verwenden, benötigen Sie eine Dienstinstanz mit einem erfolgreichen Ausführungsstatus. Um eine neue Dienstinstanz zu erstellen, besuchen Sie das Benutzerhandbuch zur [Attribution AI](./user-guide.md). Wenn Sie kürzlich eine Dienstinstanz erstellt haben und sie weiterhin trainiert und bewertet wird, erlauben Sie bitte 24 Stunden, damit sie ausgeführt werden kann.

## Übersicht über Dienstinstanzen

In the [!DNL Adobe Experience Platform] UI, click **Services** in the left navigation. Der *Dienste* -Browser wird angezeigt und zeigt verfügbare Adobe Intelligent Services an. In the container for Attribution AI, click **Open**.

![Zugriff auf Ihre Instanz](./images/insights/open_Attribution_ai.png)

Die Seite des Zuordnungs-API-Dienstes wird angezeigt. Auf dieser Seite werden Dienstinstanzen von Attribution AI Liste und Informationen zu diesen Instanzen, einschließlich des Namens der Instanz, der Konvertierungseinstellungen, der Häufigkeit der Ausführung der Instanz und des Status der letzten Aktualisierung, angezeigt. Klicken Sie auf einen Dienstinstanznamen, um zu beginnen.

>[!NOTE] Es können nur Dienstinstanzen ausgewählt werden, die erfolgreiche Testläufe abgeschlossen haben.

![Instanz erstellen](./images/insights/select-service-instance.png)

Als Nächstes wird die Einblicke-Seite für diese Dienstinstanz angezeigt, auf der Sie Visualisierungen und eine Reihe von Filtern zur Interaktion mit Ihren Daten erhalten. Die Visualisierungen und Filter werden in diesem Handbuch ausführlicher erläutert.

![Setup-Seite](./images/insights/landing-page.png)

### Details zur Dienstinstanz

Um weitere Details für eine Dienstinstanz Ansicht, klicken Sie oben rechts auf Mehr **** anzeigen.

![Mehr anzeigen](./images/insights/show-more.png)

Eine detaillierte Liste wird angezeigt. Weitere Informationen zu den aufgelisteten Eigenschaften finden Sie im Benutzerhandbuch zur [Attribution AI](./user-guide.md).

![Details anzeigen](./images/insights/advanced-details.png)

### Bearbeiten einer Instanz

Um eine Instanz zu bearbeiten, klicken Sie in der Navigation oben rechts auf *Bearbeiten* .
![Klicken Sie auf die Schaltfläche &quot;Bearbeiten&quot;](./images/insights/edit-button.png)

Das Dialogfeld &quot;Bearbeiten&quot;wird angezeigt, in dem Sie die Beschreibung und die Bewertungsfrequenz der Instanz bearbeiten können. Um die Änderungen zu bestätigen und das Dialogfeld zu schließen, klicken Sie unten rechts auf *Bearbeiten* .

![Bearbeiten-Popup](./images/insights/edit-popover.png)

### Weitere Aktionen

Die Schaltfläche &quot; *Mehr Aktionen* &quot;befindet sich in der oberen rechten Navigation neben *Bearbeiten*. Wenn Sie auf **Mehr Aktionen** klicken, wird ein Dropdown-Menü geöffnet, in dem Sie eine der folgenden Vorgänge auswählen können:

- **Löschen**: Löscht die Instanz.
- **Zusammenfassungsdaten** herunterladen: Lädt eine CSV-Datei mit den Übersichtsdaten herunter.
- **Zugangsdaten**: Durch Klicken auf *Zugriffswerte* gelangen Sie zu den [Zugriffswerten für Attribution AI-Tutorial](./download-scores.md).
- **Ansicht-Ausführungsverlauf**: Es wird ein Popup mit einer Liste aller mit der Dienstinstanz verknüpften Bewertungsläufe angezeigt.

![mehr Aktionen](./images/insights/more-actions.png)

## Filtern Ihrer Daten

Mithilfe von Attributions-AI-Einblicken können Sie Ihre Daten filtern und die UI-Visualisierungen automatisch auf Grundlage Ihrer ausgewählten Filter aktualisieren.

>[!NOTE] Standardmäßig ist jeder Filter auf &quot;Alle&quot;eingestellt, mit Ausnahme des Filters für das *Zuordnungsmodell* , der auf &quot;Inkrementelle und einflussreiche zurechenbare Konvertierungen&quot;eingestellt ist.

### Konversions-Ereignis

Wenn Sie eine neue Instanz in Attribution AI erstellen, ist eines der erforderlichen Ereignisse &quot;Conversion&quot;. Umrechnungsziele sind Geschäftsziele, die die Auswirkungen von Marketing-Aktivitäten wie E-Commerce-Bestellungen, In-Store-Käufe und Website-Besuche identifizieren.

Innerhalb der Instanz können Sie mit dem Dropdownmenü *Konvertierungseinstellungen* eines der für Ihre Instanz definierten Ereignis auswählen, um Ihre Daten zu filtern. Wenn Sie bestimmte Ereignis auswählen, werden die Visualisierungen der Benutzeroberfläche so geändert, dass nur Konvertierungen aus diesen Ereignissen gefüllt werden.

![Konversions-Ereignis](./images/insights/conversion-event.png)

### Attributionsmodell

Durch Klicken auf *Zuordnungsmodell* wird eine Dropdown-Liste mit allen verfügbaren Zuordnungsmodellen geöffnet. Sie können mehrere Modelle zum Vergleich der Ergebnisse auswählen. Weitere Informationen zu den verschiedenen Zuordnungsmodellen und ihrer Funktionsweise finden Sie in der Übersicht über die [Zuordnungs-API](./overview.md) , die eine Tabelle mit Informationen zu den einzelnen Modellen enthält.

![Zuordnungsmodell](./images/insights/attribution-model.png)

### Produkt

Mit dem *Filter &quot;Produkt* &quot;können Sie aus allen Produkten auswählen, die ursprünglich bei der Erstellung Ihrer Instanz berücksichtigt wurden. Klicken Sie auf das Dropdown-Feld und wählen Sie mit der Suchfunktion schnell alle Produkte aus, die Sie vergleichen möchten.

![Produktfilter](./images/insights/product-filter.png)

### Geografie

Der *Geografie* -Filter füllt Ländercodes basierend auf regional basierten Modellen. Abhängig von Ihren Daten ist dieser Filter möglicherweise nicht vorhanden.

>[!NOTE] Ländercodes sind zwei Zeichen lang. Eine vollständige Liste finden Sie hier: [ISO 3166-1 alpha-2](https://datahub.io/core/country-list).

### Region

>[!NOTE] Dieser Filter ist nur verfügbar, wenn Sie beim Erstellen Ihrer Dienstinstanz das optionale, auf [Regionen basierte Modellieren](./user-guide.md#region-based-modeling-optional) im Benutzeroberflächen-Handbuch Attribution AI durchgeführt haben.

Mit diesem Filter können Sie alle Regionen auswählen, die Sie im Instanzerstellungsprozess eingerichtet haben.

### Kanal

Wenn Sie auf den *Kanal* -Filter klicken, wird eine Dropdown-Liste mit allen verfügbaren Marketing-Kanälen angezeigt. Sie können mehrere Kanal zum Vergleich auswählen.

![Kanal](./images/insights/channel.png)

### Datumsbereich

Klicken Sie auf das Kalendersymbol, um das Popup für den Datumsbereich zu öffnen. Die Daten des Start- und Endkonvertierungs-Ereignisses bestimmen die Datenmenge, die in der Benutzeroberfläche ausgefüllt wird. Sie können den Datumsbereich einschränken oder erweitern, um die aufgefüllten Daten zu fokussieren oder zu erweitern.

![Datumsbereich](./images/insights/display-date-range.png)

## Übersicht über Ihre Daten

Die *Übersichtskarte* zeigt Ihre Gesamtumrechnungen nach Zuordnungsmodell an. Die Gesamtzahl ändert sich je nach Art der Suche anhand der zuvor in diesem Dokument beschriebenen Filter. Wenn Sie weitere Modelle auswählen, werden der Übersicht weitere Kreise hinzugefügt, die jeweils eine eigene Farbe haben, die der Legende entspricht.

![Übersicht](./images/insights/Overview.png)

## Wöchentliche Trends

Die *Karte &quot;Wöchentliche Trends* &quot;unterteilt Ihre Gesamtumrechnung nach dem Datumsbereich, den Sie während des Filtervorgangs festgelegt haben.

![Trends](./images/insights/weekly-trends.png)

Wenn Sie auf die Ellipsen oben rechts auf der Karte mit *wöchentlichen Trends* klicken, wird eine Dropdownliste angezeigt, in der Sie Tages-, Wochen- oder Monatstrends auswählen können.

Wenn Sie den Mauszeiger über die Datenzeile eines bestimmten Zuordnungsmodells bewegen, wird ein Popup erstellt, das die Gesamtanzahl der Konversionen für dieses Datum anzeigt.

![Hover-Trends](./images/insights/weekly-trend-hover.png)

## Aufschlüsselung nach Kanal

Die *Aufschlüsselungskarte nach Kanal* wird verwendet, um die Gesamtanzahl der Konversionen im Verhältnis zu den einzelnen Kanälen zu ermitteln. Mit dieser Karte können Entscheidungen über die Effektivität der einzelnen Kanal und die Kapitalrendite getroffen werden.

![Aufschlüsselungs-Kanal](./images/insights/channel-breakdown.png)

Wenn Sie auf die Auslassungspunkte oben rechts auf der Karte &quot; *Aufschlüsselung nach Kanal* &quot;klicken, wird eine Dropdown-Liste geöffnet, in der Sie Daten basierend auf Touchpoints füllen können.

![Touchpoints](./images/insights/breakdown-by-touchpoints.png)

## Häufigste Kampagnen

Auf der Karte &quot; *Wichtigste Kampagnen* &quot;wird ein Überblick über Ihre Kampagnen und die Leistung der Kampagne in den einzelnen Kanälen angezeigt. Diese Karte kann Ihnen helfen, Ihr Team über die Effektivität einer bestimmten Kampagne für einen bestimmten Kanal zu informieren und einen Einblick darin zu geben, wo Sie weiter investieren können.

![Top-Kampagnen](./images/insights/top-campaigns.png)

## Nächste Schritte

Sobald Sie die Daten gefiltert haben und die entsprechenden Informationen anzeigen können, haben Sie die Möglichkeit, auf die Ergebnisse zuzugreifen. Eine ausführliche Anleitung zum Zugriff auf Ihre Punktzahlen finden Sie in der [Anleitung zur Attribution AI](./download-scores.md) . Darüber hinaus können Sie die Zusammenfassungsdaten wie in [weiteren Aktionen](#more-actions)angegeben herunterladen. Wenn Sie &quot;Zusammenfassungsdaten herunterladen&quot;auswählen, werden die nach Datumsangaben aggregierten Zusammenfassungsdaten heruntergeladen.

## Zusätzliche Ressourcen

Das folgende Video hilft Ihnen dabei zu lernen, wie Sie die Insight-Seite &quot;Attribution AI&quot;nutzen können, um den ROI von Marketing-Kanälen und -Kampagnen zu verstehen.

>[!VIDEO](https://video.tv.adobe.com/v/32669?learn=on&quality=12)