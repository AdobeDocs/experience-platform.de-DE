---
keywords: Experience Platform;Einblicke;Zuordnungs-Hilfe;beliebte Themen;Zuordnungsai-Einblicke
solution: Intelligent Services, Experience Platform
title: Discover Insight in Attribution AI
topic-legacy: Attribution AI insights
description: Dieses Dokument dient als Handbuch für die Interaktion mit Einblicken der Dienstinstanz in der Benutzeroberfläche von Adobe Intelligent Services.
exl-id: 6b8e51e7-1b56-4f4e-94cf-96672b426c88
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1656'
ht-degree: 49%

---

# Entdecken Sie Einblicke in Attribution AI

Die Instanzen des Attribution AI-Service bieten Einblicke, anhand derer Marketing-Entscheidungen in Bezug auf Marketing-Performance und ROI getroffen und gemessen werden können. Durch die Auswahl einer Dienstinstanz erhalten Sie Visualisierungen und Filter, anhand derer Sie die Auswirkungen jeder Kundeninteraktion in jeder Phase der Customer Journey verstehen können.

Dieses Dokument dient als Handbuch für die Interaktion mit Einblicken der Dienstinstanz in der Benutzeroberfläche von Adobe Intelligent Services.

## Erste Schritte

Um Einblicke für Attribution AI zu verwenden, benötigen Sie eine Dienstinstanz mit einem erfolgreichen Ausführungsstatus. Um eine neue Dienstinstanz zu erstellen, gehen Sie zum [Benutzeroberflächenhandbuch für Attribution AI](./user-guide.md). Wenn Sie kürzlich eine Dienstinstanz erstellt haben und diese sich noch in der Trainings- und Bewertungsphase befindet, warten Sie bitte 24 Stunden, bis sie fertig ist.

## Übersicht über Einblicke von Dienstinstanzen

Wählen Sie in der Benutzeroberfläche [!DNL Adobe Experience Platform] in der linken Navigation **[!UICONTROL Dienste]** aus. Der **[!UICONTROL Dienste]**-Browser wird geöffnet und zeigt verfügbare Adobe Intelligent Services an. Wählen Sie im Container für Attribution AI **[!UICONTROL Öffnen]**.

![Zugreifen auf Ihre Instanz](./images/insights/open_Attribution_ai.png)

Die Seite des Attribution AI-Service wird angezeigt. Auf dieser Seite werden Dienstinstanzen von Attribution AI aufgelistet und Informationen zu diesen angezeigt, einschließlich des Namens der Instanz, der Konversionsereignisse, der Häufigkeit der Ausführung der Instanz und des Status der letzten Aktualisierung. Wählen Sie einen Dienstinstanznamen aus, der beginnen soll.

>[!NOTE]
>
>Es können nur Dienstinstanzen ausgewählt werden, die erfolgreiche Bewertungsläufe abgeschlossen haben.

![Instanz erstellen](./images/insights/select-service-instance.png)

Als Nächstes wird die Seite mit den Einblicken für diese Dienstinstanz angezeigt. Hier werden Visualisierungen und eine Reihe von Filtern zur Interaktion mit Ihren Daten bereitgestellt. Die Visualisierungen und Filter werden in diesem Handbuch ausführlicher erläutert.

![Setup-Seite](./images/insights/landing-page.png)

### Details zur Dienstinstanz

Um weitere Details für eine Dienstinstanz Ansicht, wählen Sie oben rechts **[!UICONTROL Mehr anzeigen]**.

![Mehr anzeigen](./images/insights/show-more.png)

Es wird eine detaillierte Liste angezeigt. Weitere Informationen zu den aufgelisteten Eigenschaften finden Sie im [Benutzerhandbuch für Attribution AI](./user-guide.md).

![Details anzeigen](./images/insights/advanced-details.png)

### Bearbeiten einer Instanz

Um eine Instanz zu bearbeiten, wählen Sie **[!UICONTROL Bearbeiten]** in der Navigation oben rechts.
![Auf Bearbeiten-Schaltfläche klicken](./images/insights/edit-button.png)

Das Dialogfeld &quot;Bearbeiten&quot;wird angezeigt, in dem Sie den Namen, die Beschreibung und die Bewertungsfrequenz der Instanz bearbeiten können. Wenn der Instanzstatus deaktiviert ist, kann die Scoring-Frequenz nicht bearbeitet werden. Um Ihre Änderungen zu bestätigen und das Dialogfeld zu schließen, wählen Sie **[!UICONTROL Speichern]** in der unteren rechten Ecke aus.

![Bearbeiten-Popup-Fenster](./images/insights/edit-popover.png)

### Mehr Aktionen {#more-actions}

Die Schaltfläche **[!UICONTROL Mehr Aktionen]** befindet sich in der oberen rechten Navigation neben **[!UICONTROL Bearbeiten]**. Wenn Sie **[!UICONTROL Mehr Aktionen]** auswählen, wird ein Dropdown-Menü geöffnet, in dem Sie eine der folgenden Vorgänge auswählen können:

- **[!UICONTROL Klonen]**: Klont die Instanz.
- **[!UICONTROL Löschen]**: Löscht die Instanz.
- **[!UICONTROL Zusammenfassungsdaten herunterladen]**: Lädt eine CSV-Datei mit den Zusammenfassungsdaten herunter.
- **[!UICONTROL Zugangsdaten]**: Durch Auswahl des  **[!UICONTROL Zugriffs-]** Scoreservers werden Sie zu den  [Zugangswerten für das Attribution AI-Lernprogramm](./download-scores.md) weitergeleitet.
- **[!UICONTROL Ausführungsverlauf anzeigen]**: Ein Popup-Fenster mit einer Liste aller mit der Dienstinstanz verbundenen Bewertungsläufe wird angezeigt.

![Mehr Aktionen](./images/insights/more-actions.png)

## Filtern Ihrer Daten

Mithilfe von Attribution AI-Einblicken können Sie Ihre Daten filtern und die Visualisierungen der Benutzeroberfläche automatisch anhand Ihrer ausgewählten Filter aktualisieren.

### Konversionsereignis

Wenn Sie eine neue Instanz in Attribution AI erstellen, ist eines der erforderlichen Felder „Konversionsereignisse“. Konversionsereignisse sind Unternehmensziele, die die Auswirkungen von Marketing-Aktivitäten wie E-Commerce-Bestellungen, In-Store-Käufen und Website-Besuchen ermitteln.

Innerhalb der Instanz können Sie mit dem Dropdown-Menü **[!UICONTROL Konversionsereignisse]** eines der für Ihre Instanz definierten Ereignisse auswählen, um Ihre Daten zu filtern. Wenn Sie bestimmte Ereignisse auswählen, werden die Visualisierungen der Benutzeroberfläche so geändert, dass nur Konversionen aus diesen Ereignissen gefüllt werden.

![Konversionsereignis](./images/insights/conversion-event.png)

### Attributionsmodell

Durch Auswahl von **[!UICONTROL Zuordnungsmodell]** wird eine Dropdown-Liste mit allen verfügbaren Zuordnungsmodellen geöffnet. Sie können mehrere Modelle zum Vergleich der Ergebnisse auswählen. Weitere Informationen zu den verschiedenen Attributionsmodellen und ihrer Funktionsweise finden Sie in der Übersicht über [Attribution AI](./overview.md), die eine Tabelle mit Informationen zu den einzelnen Modellen enthält.

![Attributionsmodell](./images/insights/attribution-model.png)

### Region

>[!NOTE]
>
>Dieser Filter ist nur verfügbar, wenn Sie beim Erstellen Ihrer Dienstinstanz die optionale [regionenbasierte Modellierung](./user-guide.md#region-based-modeling-optional) im Benutzerhandbuch zur Attribution AI-Benutzeroberfläche ausgeführt haben.

Mit diesem Filter können Sie alle Regionen auswählen, die Sie beim Erstellen der Instanz eingerichtet haben.

### hinzufügen Filter

Sie können weitere Filter hinzufügen, indem Sie auf das Symbol **filter** klicken, um das Popup **[!UICONTROL Hinzufügen Filter]** zu öffnen. Mit dem Popup **[!UICONTROL Hinzufügen Filter]** können Sie nach Kanal, Geografie, Medientyp und Produkt filtern. Nur die entsprechenden Filter für eine Dienstinstanz werden vom Popup-Fenster ausgefüllt. Wenn Sie beispielsweise keine geografischen Daten oder einen Medientyp angegeben haben, stehen diese Filterattribute nicht für Ihre Instanz zur Verfügung.

![zusätzliche Filter](./images/insights/additional-filters.png)

![Filter Popup](./images/insights/filter-popover.png)

- **[!UICONTROL Kanal]:Durch** Auswahl des Attributs &quot;Kanal&quot;können Sie alle verfügbaren Marketing-Kanal filtern. Sie können mehrere Kanäle zum Vergleich auswählen.
- **[!UICONTROL Geografie]: Durch die** Auswahl des geografischen Attributs können Sie Ländercodes auf Grundlage regionsbasierter Modelle filtern. Abhängig von Ihren Daten ist dieser Filter möglicherweise vorhanden.  Ländercodes sind zwei Zeichen lang. Lesen Sie die vollständige Liste des Ländercodes [hier](https://datahub.io/core/country-list).
- **[!UICONTROL Medientyp]:Durch** Auswahl des Medientypattributs können Sie jeden Ihrer definierten Medientypen filtern.
- **[!UICONTROL Produkt]: Durch** Auswahl des Produktattributs können Sie aus allen Produkten filtern, die ursprünglich bei der Erstellung Ihrer Instanz berücksichtigt wurden.

### Datumsbereich

Wählen Sie das Kalendersymbol aus, um das Popup für den Datumsbereich zu öffnen. Die Start- und Enddaten für die Konversionsereignisse bestimmen die Datenmenge, die in der Benutzeroberfläche angezeigt wird. Sie können den Datumsbereich einschränken oder erweitern, um die Menge der angezeigten Daten zu fokussieren oder zu vergrößern.

![Datumsbereich](./images/insights/display-date-range.png)

## Übersicht über Ihre Daten

Die Karte **[!UICONTROL Übersicht]** zeigt Ihre Konversionen insgesamt nach Attributionsmodell an. Die Gesamtzahl ändert sich je nach Art der Suche anhand der zuvor in diesem Dokument beschriebenen Filter. Durch die Auswahl weiterer Modelle werden der Übersicht zusätzliche Kreise hinzugefügt, jeder mit einer eigenen Farbe entsprechend der Legende.

![Übersicht](./images/insights/Overview.png)

## Wöchentliche Trends

Die Karte **[!UICONTROL Wöchentliche Trends]** unterteilt Ihre Konversionen insgesamt nach dem Datumsbereich, den Sie während des Filtervorgangs festgelegt haben.

Wenn Sie die Ellipsen oben rechts auf der Karte **Wöchentliche Trends** auswählen, wird eine Dropdownliste angezeigt, in der Sie tägliche, wöchentliche oder monatliche Trends auswählen können.

Wenn Sie den Mauszeiger über die Datenzeile eines bestimmten Attributionsmodells bewegen, wird ein Popup-Fenster angezeigt, das die Gesamtzahl der Konversionen für dieses Datum anzeigt.

![Trends](./images/insights/weekly-trends.png)

## Aufschlüsselung nach Kanal

Die Karte **[!UICONTROL Aufschlüsselung nach Kanal]** wird verwendet, um die Gesamtanzahl der Konversionen im Verhältnis zu den einzelnen Kanälen zu ermitteln. Mit dieser Karte können Entscheidungen über die Effektivität der einzelnen Kanäle und die ROI getroffen werden.

Wenn Sie die Auslassungspunkte oben rechts auf der Karte **[!UICONTROL Aufschlüsselung nach Kanal]** auswählen, wird ein Dropdown-Menü geöffnet, in dem Sie Daten basierend auf Touchpoints füllen können.

![Aufschlüsseln der Kanäle](./images/insights/channel-breakdown.png)

## Topkampagnen

Auf der Karte **[!UICONTROL Topkampagnen]** wird ein Überblick über Ihre Kampagnen und die Leistung der Kampagne in den einzelnen Kanälen angezeigt. Diese Karte kann Ihr Team über die Effektivität einer bestimmten Kampagne für einen bestimmten Kanal informieren und Einblicke geben, in welche Kampagnen Sie weiter investieren sollten.

![Topkampagnen](./images/insights/top-campaigns.png)

## Aufschlüsselung nach Touchpoint-Position

Durch Auswahl der Registerkarte **[!UICONTROL Path Analyse]** werden die Diagramme **[!UICONTROL Aufschlüsselung nach Touchpoint-Position]** und **[!UICONTROL Top-Umrechnungspfade]** geladen.

Das Diagramm **[!UICONTROL Aufschlüsselung nach Touchpoint-Position]** ist eine Aufschlüsselung der zugewiesenen Konversionen nach Position des Touchpoints im Vergleich zu allen Konversionspfaden. Dieses Diagramm hilft Ihnen zu verstehen, welche Touchpoints in den verschiedenen Phasen des Konvertierungspfads effektiver sind. Die Bühnen sind Start, Spieler und näher.

- **Starter:** Gibt an, dass der Touchpoint der erste Touch in einem Konvertierungspfad war.
- **Player:** Gibt an, dass der Touchpoint nicht die erste oder letzte Berührung war, die zu einer Konversion führte.
- **Schließen:** Gibt an, dass der Touchpoint der letzte Touch vor einer Konvertierung war.

>!![NOTE]
Die Summe des prozentualen Beitrags für ein Zuordnungsmodell für alle Touchpoints und Positionen sollte 100 betragen.

![Benutzerpfad-Aufschlüsselungs-Touchpoint](./images/insights/user-paths.png)

## Top-Umrechnungspfade

Das Diagramm **[!UICONTROL Top-Konvertierungspfade]** zeigt die beeinflussten und algorithmischen Werte auf den Top-Konversionspfaden in den ausgewählten Regionen. Mit diesem Diagramm können Sie visualisieren, welche Touchpoints zu Umrechnungen beitragen und wie das Zuordnungsergebnis für jeden Touchpoint aussieht. Anhand dieser Informationen können Sie die häufigsten Pfade in einem bestimmten Bereich Ansicht und feststellen, ob zwischen den verschiedenen Gruppen von Touchpoints Muster auftreten.

![Bevorzugte Benutzerpfade](./images/insights/Touchpoint-paths.png)

## Touchpoint-Effektivität

Durch Auswahl der Registerkarte **[!UICONTROL Touchpoint-Effektivität]** wird die Karte **[!UICONTROL Touchpoint-Effektivität]** geladen. Diese Karte verwendet die Datenverteilung von Attribution AI, um Informationen zu jedem Touchpoint anzuzeigen. Die Daten für diese Tabelle werden nur für bestimmte Zeiträume generiert, wie durch das Datum **[!UICONTROL Ab]** oben rechts auf der Karte angegeben.

![Touchpoint-Effektivitätsauswahl](./images/insights/Touchpoint-effectiveness.png)

Sie können die Karteninformationen **[!UICONTROL Touchpoint-Effektivität]** verwenden, um zu verstehen, wie ein Touchpoint zu einer Konversion beiträgt. Sie können auch sehen, wie effektiv jeder Touchpoint mit den folgenden Leistungsmetriken ist:

**berührte** Pfade: Diese Metrik zeigt den Prozentsatz der Pfade an, die Konversionen für den Touchpoint erzielen/nicht erzielen. Sie sehen höhere zurechenbare Konvertierungen, wenn das Verhältnis der Pfade (Prozentsatz), die Konvertierung zu Pfaden erzielen, die keine Konversion erzielen, hoch ist.

![Pfade berührte Metrik](./images/insights/Touchpoint-metrics.png)

**Effizienzmaßnahme**: Diese Metrik zeigt Sterne auf einer Skala von 1 bis 5 an. Die Skala zeigt die relative Bedeutung eines Touchpoints für eine Konvertierung an.

>[!NOTE]
Höhere Touchpoint-Volumen garantieren keine höhere Effizienz.

**Gesamtvolumen**: Das Aggregat, wie oft ein Touchpoint von einem Benutzer berührt wurde. Dies umfasst sowohl Touchpoints, die auf einem Pfad angezeigt werden, auf dem Konversionen erzielt werden, als auch Pfade, die nicht zu einer Konvertierung führen.

## Nächste Schritte

Sobald Sie die Daten gefiltert haben und die entsprechenden Informationen anzeigen können, können Sie auf die Bewertungen zuzugreifen. Eine ausführliche Anleitung zum Zugriff auf Ihre Bewertungen finden Sie im [Tutorial für den Zugriff auf Bewertungen in Attribution AI](./download-scores.md). Darüber hinaus können Sie die Zusammenfassungsdaten herunterladen, wie in [Mehr Aktionen](#more-actions) angegeben. Wenn Sie „Zusammenfassungsdaten herunterladen“ auswählen, werden die nach Datumsangaben aggregierten Zusammenfassungsdaten heruntergeladen.

## Zusätzliche Ressourcen

Das folgende Video hilft Ihnen dabei zu lernen, wie Sie die Einblicke in Attribution AI nutzen können, um den ROI von Marketing-Kanälen und -Kampagnen zu verstehen.

>[!VIDEO](https://video.tv.adobe.com/v/32669?learn=on&quality=12)
