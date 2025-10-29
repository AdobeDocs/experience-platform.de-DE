---
keywords: Experience Platform;Insights;Attributions-KI;beliebte Themen;Attributions-KI-Insights
feature: Attribution AI
title: Einblicke in Attributions-KI
description: Dieses Dokument dient als Handbuch für die Interaktion mit Einblicken der Dienstinstanz in der Benutzeroberfläche von Adobe Intelligent Services.
exl-id: 6b8e51e7-1b56-4f4e-94cf-96672b426c88
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1583'
ht-degree: 39%

---

# Einblicke in Attributions-KI

Die Instanzen des Attribution AI-Service bieten Einblicke, anhand derer Marketing-Entscheidungen in Bezug auf Marketing-Performance und ROI getroffen und gemessen werden können. Durch die Auswahl einer Dienstinstanz erhalten Sie Visualisierungen und Filter, anhand derer Sie die Auswirkungen jeder Kundeninteraktion in jeder Phase der Customer Journey verstehen können.

Dieses Dokument dient als Handbuch für die Interaktion mit Einblicken der Dienstinstanz in der Benutzeroberfläche von Adobe Intelligent Services.

## Erste Schritte

Um Einblicke für Attribution AI zu verwenden, benötigen Sie eine Dienstinstanz mit einem erfolgreichen Ausführungsstatus. Um eine neue Dienstinstanz zu erstellen, gehen Sie zum [Benutzeroberflächenhandbuch für Attribution AI](./user-guide.md). Wenn Sie kürzlich eine Dienstinstanz erstellt haben und diese sich noch in der Trainings- und Bewertungsphase befindet, warten Sie bitte 24 Stunden, bis sie fertig ist.

## Übersicht über Einblicke von Dienstinstanzen

Wählen Sie in der [!DNL Adobe Experience Platform]-Benutzeroberfläche im linken Navigationsbereich **[!UICONTROL Services]** aus. Der **[!UICONTROL Services]** wird angezeigt und zeigt die verfügbaren Adobe Intelligent Services an. Wählen Sie im Container für Attributions-KI **[!UICONTROL Open]** aus.

![Zugreifen auf Ihre Instanz](./images/insights/open_Attribution_ai.png)

Die Seite des Attribution AI-Service wird angezeigt. Auf dieser Seite werden Dienstinstanzen von Attribution AI aufgelistet und Informationen zu diesen angezeigt, einschließlich des Namens der Instanz, der Konversionsereignisse, der Häufigkeit der Ausführung der Instanz und des Status der letzten Aktualisierung. Wählen Sie einen Namen für die Service-Instanz aus, um zu beginnen.

>[!NOTE]
>
>Es können nur Service-Instanzen ausgewählt werden, die erfolgreiche Scoring-Durchgänge abgeschlossen haben.

![Instanz erstellen](./images/insights/select-service-instance.png)

Als Nächstes wird die Seite mit den Einblicken für diese Dienstinstanz angezeigt. Hier werden Visualisierungen und eine Reihe von Filtern zur Interaktion mit Ihren Daten bereitgestellt. Die Visualisierungen und Filter werden in diesem Handbuch ausführlicher erläutert.

![Setup-Seite](./images/insights/landing-page.png)

### Details zur Dienstinstanz

Um zusätzliche Details für eine Service-Instanz anzuzeigen, wählen Sie oben rechts **[!UICONTROL Show more]** aus.

![Mehr anzeigen](./images/insights/show-more.png)

Es wird eine detaillierte Liste angezeigt. Weitere Informationen zu den aufgelisteten Eigenschaften finden Sie im [Benutzerhandbuch für Attribution AI](./user-guide.md).

![Details anzeigen](./images/insights/advanced-details.png)

### Bearbeiten einer Instanz

Um eine Instanz zu bearbeiten, wählen Sie in der oberen rechten Navigationsleiste **[!UICONTROL Edit]** aus.
![Auf Bearbeiten-Schaltfläche klicken](./images/insights/edit-button.png)

Das Dialogfeld „Bearbeiten“ wird angezeigt, in dem Sie den Namen, die Beschreibung und die Bewertungsfrequenz der Instanz bearbeiten können. Wenn der Instanzstatus deaktiviert ist, kann die Scoring-Häufigkeit nicht bearbeitet werden. Um Ihre Änderungen zu bestätigen und das Dialogfeld zu schließen, wählen Sie **[!UICONTROL Save]** in der rechten unteren Ecke aus.

![Bearbeiten-Popup-Fenster](./images/insights/edit-popover.png)

### Mehr Aktionen {#more-actions}

Die Schaltfläche **[!UICONTROL More actions]** befindet sich in der oberen rechten Navigationsleiste neben **[!UICONTROL Edit]**. Wenn Sie **[!UICONTROL More actions]** auswählen, wird ein Dropdown-Menü geöffnet, in dem Sie einen der folgenden Vorgänge auswählen können:

- **[!UICONTROL Clone]**: Klont die Instanz.
- **[!UICONTROL Delete]**: Löscht die Instanz.
- **[!UICONTROL Download summary data]**: Lädt eine CSV-Datei mit den Zusammenfassungsdaten herunter.
- **[!UICONTROL Access scores]**: Wenn Sie **[!UICONTROL Access scores]** auswählen, werden Sie zum Tutorial [Zugriff auf Scores für Attributions-KI](./download-scores.md) weitergeleitet.
- **[!UICONTROL View run history]**: Ein Pop-up mit einer Liste aller mit der Service-Instanz verbundenen Scoring-Durchgänge wird angezeigt.

![Mehr Aktionen](./images/insights/more-actions.png)

## Filtern Ihrer Daten

Mithilfe von Attribution AI-Einblicken können Sie Ihre Daten filtern und die Visualisierungen der Benutzeroberfläche automatisch anhand Ihrer ausgewählten Filter aktualisieren.

### Konversionsereignis

Wenn Sie eine neue Instanz in Attribution AI erstellen, ist eines der erforderlichen Felder „Konversionsereignisse“. Konversionsereignisse sind Unternehmensziele, die die Auswirkungen von Marketing-Aktivitäten wie E-Commerce-Bestellungen, In-Store-Käufen und Website-Besuchen ermitteln.

Innerhalb der Instanz können Sie mit dem Dropdown-Menü **[!UICONTROL Conversion events]** eines der für Ihre Instanz definierten Ereignisse auswählen, um Ihre Daten zu filtern. Wenn Sie bestimmte Ereignisse auswählen, werden die Visualisierungen der Benutzeroberfläche so geändert, dass nur Konversionen aus diesen Ereignissen gefüllt werden.

![Konversionsereignis](./images/insights/conversion-event.png)

### Attributionsmodell

Wenn Sie **[!UICONTROL Attribution Model]** auswählen, wird ein Dropdown-Menü mit allen verfügbaren Attributionsmodellen geöffnet. Sie können mehrere Modelle zum Vergleich der Ergebnisse auswählen. Weitere Informationen zu den verschiedenen Attributionsmodellen und ihrer Funktionsweise finden Sie in der Übersicht über [Attribution AI](./overview.md), die eine Tabelle mit Informationen zu den einzelnen Modellen enthält.

![Attributionsmodell](./images/insights/attribution-model.png)

### Region

>[!NOTE]
>
>Dieser Filter ist nur vorhanden, wenn Sie beim Erstellen Ihrer Service[Instanz im Handbuch zur Attributions](./user-guide.md#region-based-modeling-optional)KI-Benutzeroberfläche den optionalen Schritt „Regionsbasierte Modellierung“ ausgeführt haben.

Mit diesem Filter können Sie alle Regionen auswählen, die Sie beim Erstellen der Instanz eingerichtet haben.

### Filter hinzufügen

Sie können zusätzliche Filter hinzufügen, indem Sie auf das Symbol **Filter** klicken, um das **[!UICONTROL Add filters]**-Popover zu öffnen. Das **[!UICONTROL Add filters]**-Popover ermöglicht die Filterung nach Kanal, Geografie, Medientyp und Produkt. Nur die entsprechenden Filter für eine Dienstinstanz werden vom Popover ausgefüllt. Wenn Sie beispielsweise keine geografischen Daten oder einen Medientyp angegeben haben, sind diese Filterattribute für Ihre Instanz nicht verfügbar.

![zusätzliche Filter](./images/insights/additional-filters.png)

![Filter-Popover](./images/insights/filter-popover.png)

- **[!UICONTROL Channel]:** Wenn Sie das Kanalattribut auswählen, können Sie einen beliebigen Ihrer verfügbaren Marketing-Kanäle filtern. Sie können mehrere Kanäle zum Vergleich auswählen.
- **[!UICONTROL Geography]:** Durch Auswahl des Attributs „geography“ können Sie Länder-Codes nach regionsbasierten Modellen filtern. Abhängig von Ihren -Daten kann dieser Filter vorhanden sein oder nicht. Länder-Codes sind zwei Zeichen lang. Die vollständige Länder-Code-Liste [hier](https://datahub.io/core/country-list).
- **[!UICONTROL Media type]:** Wenn Sie das Medienartattribut auswählen, können Sie einen beliebigen Ihrer definierten Medientypen filtern.
- **[!UICONTROL Product]:** Wenn Sie das Produktattribut auswählen, können Sie aus allen Produkten filtern, die ursprünglich bei der Erstellung Ihrer Instanz aufgenommen wurden.

### Datumsbereich

Wählen Sie das Kalendersymbol aus, um das Popover „Datumsbereich“ zu öffnen. Die Start- und Enddaten für die Konversionsereignisse bestimmen die Datenmenge, die in der Benutzeroberfläche angezeigt wird. Sie können den Datumsbereich einschränken oder erweitern, um die Menge der angezeigten Daten zu fokussieren oder zu vergrößern.

![Datumsbereich](./images/insights/display-date-range.png)

## Übersicht über Ihre Daten

Die Karte **[!UICONTROL Overview]** zeigt Ihre gesamten Konversionen nach Attributionsmodell an. Die Gesamtzahl ändert sich je nach Art der Suche anhand der zuvor in diesem Dokument beschriebenen Filter. Durch die Auswahl weiterer Modelle werden der Übersicht zusätzliche Kreise hinzugefügt, jeder mit einer eigenen Farbe entsprechend der Legende.

![Übersicht](./images/insights/Overview.png)

## Wöchentliche Trends

Die **[!UICONTROL Weekly trends]**-Karte schlüsselt Ihre Gesamtkonvertierung nach dem Datumsbereich auf, den Sie während des Filtervorgangs festgelegt haben.

Wenn Sie oben rechts auf der Karte **Wöchentliche Trends** auf die Auslassungszeichen klicken, wird eine Dropdown-Liste angezeigt, in der Sie tägliche, wöchentliche oder monatliche Trends auswählen können.

Wenn Sie den Mauszeiger über die Datenzeile eines bestimmten Attributionsmodells bewegen, wird ein Popup-Fenster angezeigt, das die Gesamtzahl der Konversionen für dieses Datum anzeigt.

![Trends](./images/insights/weekly-trends.png)

## Aufschlüsselung nach Kanal

Die **[!UICONTROL Breakdown by channel]**-Karte wird verwendet, um die Gesamtzahl der Konversionen in Bezug auf jeden Kanal zu bestimmen. Mit dieser Karte können Entscheidungen über die Effektivität der einzelnen Kanäle und die ROI getroffen werden.

Wenn Sie oben rechts auf der **[!UICONTROL Breakdown by channel]** die Auslassungszeichen auswählen, wird eine Dropdown-Liste geöffnet, in der Sie Daten basierend auf Touchpoints ausfüllen können.

![Aufschlüsseln der Kanäle](./images/insights/channel-breakdown.png)

## Topkampagnen

Die Karte **[!UICONTROL Top campaigns]** zeigt einen Überblick über Ihre Kampagnen und deren Leistung in den einzelnen Kanälen an. Diese Karte kann dabei helfen, Ihr Team über die Effektivität einer bestimmten Kampagne für einen bestimmten Kanal zu informieren, und bietet Einblicke, z. B. in welche Kampagnen Sie weiter investieren sollten.

![Topkampagnen](./images/insights/top-campaigns.png)

## Aufschlüsselung nach Touchpoint-Position

Wenn Sie die Registerkarte **[!UICONTROL Path Analysis]** auswählen, werden die **[!UICONTROL Breakdown by touchpoint position]**- und **[!UICONTROL Top conversion paths]**-Diagramme geladen.

Das **[!UICONTROL Breakdown by touchpoint position]** Diagramm enthält eine Aufschlüsselung der zugewiesenen Konversionen nach Position des Touchpoints im Vergleich zu allen Konversionspfaden. Dieses Diagramm zeigt Ihnen, welche Touchpoints in verschiedenen Phasen des Konversionspfads effektiver sind. Die Bühnen sind Starter, Spieler und näher.

- **Starter:** Zeigt an, dass der Touchpoint der erste Touch in einem Konversionspfad war.
- **Player:** Zeigt an, dass der Touchpoint nicht der erste oder der letzte Touch war, der zu einer Konversion geführt hat.
- **Closer:** Zeigt an, dass der Touchpoint der letzte Touch vor einer Konversion war.

>[!NOTE]
>
>Die Summe des prozentualen Beitrags für ein Attributionsmodell über alle Touchpoints und Positionen hinweg sollte 100 betragen.

![Touchpoint für die Aufschlüsselung des Benutzerpfads](./images/insights/user-paths.png)

## Top-Konversionspfade

Das **[!UICONTROL Top conversion paths]** Diagramm zeigt die beeinflussten und algorithmischen Werte auf den obersten Konversionspfaden in den ausgewählten Regionen. In diesem Diagramm können Sie visualisieren, welche Touchpoints zu Konversionen beitragen und wie der Attributionswert für jeden Touchpoint aussieht. Mithilfe dieser Informationen können Sie die häufigsten Pfade in einer bestimmten Region anzeigen und sehen, ob Muster zwischen den verschiedenen Sätzen von Touchpoints auftreten.

![Die häufigsten Benutzerpfade](./images/insights/Touchpoint-paths.png)

## Touchpoint-Effektivität

Wenn Sie die Registerkarte **[!UICONTROL Touchpoint Effectiveness]** auswählen, wird die **[!UICONTROL Touchpoint effectiveness]** geladen. Diese Karte verwendet die Attribution AI-Datenverteilung, um Informationen zu jedem Touchpoint anzuzeigen. Die Daten für diese Tabelle werden nur für bestimmte Zeiträume generiert, die durch das **[!UICONTROL As of]** oben rechts auf der Karte angegeben werden.

![Touchpoint Effektivität auswählen](./images/insights/Touchpoint-effectiveness.png)

Mithilfe der **[!UICONTROL Touchpoint effectiveness]**-Karteninformationen lässt sich erkennen, wie ein Touchpoint zu einer Konversion beiträgt. Mit den folgenden Leistungsmetriken können Sie auch sehen, wie effektiv jeder Touchpoint ist:

**Pfade mit Touchpoint**: Diese Metrik zeigt einen Prozentsatz der Pfade an, die eine Konversion für den Touchpoint erzielen/nicht erreichen. Höhere zugewiesene Konversionen werden angezeigt, wenn das Verhältnis der Pfade (in Prozent), die eine Konversion erzielen, zu den Pfaden, die keine Konversion erzielen, hoch ist.

![Pfade - Touchmetrik](./images/insights/Touchpoint-metrics.png)

**Effizienzmessung**: Diese Metrik zeigt Sterne auf einer Skala von ein bis fünf an. Die Skala zeigt die relative Bedeutung eines Touchpoints für eine Konversion an.

>[!NOTE]
>
>Ein höheres Touchpoint-Volumen garantiert keine höhere Effizienz.

**Gesamtvolumen**: Die Gesamtzahl der Berührungen eines Touchpoints durch eine Benutzerin oder einen Benutzer. Dies schließt Touchpoints ein, die auf einem Pfad erscheinen, der eine Konversion erreicht, sowie Pfade, die keine Konversion ergeben.

## Nächste Schritte

Sobald Sie die Daten gefiltert haben und die entsprechenden Informationen anzeigen können, können Sie auf die Bewertungen zuzugreifen. Eine ausführliche Anleitung zum Zugriff auf Ihre Bewertungen finden Sie im [Tutorial für den Zugriff auf Bewertungen in Attribution AI](./download-scores.md). Darüber hinaus können Sie die Zusammenfassungsdaten herunterladen, wie in [Mehr Aktionen](#more-actions) angegeben. Wenn Sie „Zusammenfassungsdaten herunterladen“ auswählen, werden die nach Datumsangaben aggregierten Zusammenfassungsdaten heruntergeladen.

## Weitere Ressourcen

Das folgende Video soll Ihnen dabei helfen zu lernen, wie Sie die Insights-Seite „Attribution AI“ verwenden können, um den ROI von Marketing-Kanälen und -Kampagnen zu verstehen.

>[!VIDEO](https://video.tv.adobe.com/v/32669?learn=on&quality=12)
