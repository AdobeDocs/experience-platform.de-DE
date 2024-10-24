---
keywords: Experience Platform; Einblicke; Kundenunterstützung; beliebte Themen; Kundendateneinblicke
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Insights mit Customer AI
description: Dieses Dokument dient als Leitfaden für die Interaktion mit Einblicken von Dienstinstanzen in der Benutzeroberfläche von Intelligent Services Customer AI.
exl-id: 8aaae963-4029-471e-be9b-814147a5f160
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '2098'
ht-degree: 6%

---

# Einblicke in Customer AI

Customer AI als Teil von Intelligent Services bietet Marketing-Experten die Möglichkeit, Adobe Sensei zu nutzen, um vorherzusagen, was Ihre Kunden als Nächstes tun werden. Customer AI wird verwendet, um für einzelne Profile skaliert benutzerdefinierte Tendenzwerte wie Abwanderung und Konversion zu berechnen. Das ist möglich, ohne dass die geschäftlichen Anforderungen in eine Aufgabe für maschinelles Lernen umgewandelt werden müssen, indem ein Algorithmus, ein Training oder eine Bereitstellung ausgewählt wird.

Dieses Dokument dient als Leitfaden für die Interaktion mit Einblicken von Dienstinstanzen in der Benutzeroberfläche von Intelligent Services Customer AI.

## Erste Schritte

Um Einblicke in Customer AI zu nutzen, benötigen Sie eine Dienstinstanz mit einem erfolgreichen Ausführungsstatus. Um eine neue Dienstinstanz zu erstellen, besuchen Sie [Konfigurieren einer Customer AI-Instanz](./configure.md). Wenn Sie kürzlich eine Dienstinstanz erstellt haben und diese sich noch in der Trainings- und Bewertungsphase befindet, warten Sie bitte 24 Stunden, bis sie fertig ist.

## Übersicht über die Dienstinstanz

Wählen Sie in der Benutzeroberfläche von [!DNL Adobe Experience Platform] im linken Navigationsbereich die Option **[!UICONTROL Dienste]** aus. Der Browser *Dienste* wird angezeigt und zeigt verfügbare Intelligent Services an. Wählen Sie im Container für Customer AI **[!UICONTROL Öffnen]** aus.

![Zugreifen auf Ihre Instanz](../images/insights/navigate-to-service.png)

Die Seite des Customer AI-Service wird angezeigt. Auf dieser Seite werden Dienstinstanzen von Customer AI aufgelistet und Informationen zu ihnen angezeigt, einschließlich Name der Instanz, Tendenztyp, Häufigkeit der Ausführung der Instanz und Status der letzten Aktualisierung.

>[!NOTE]
>
>Nur Dienstinstanzen, die erfolgreiche Scoring-Läufe abgeschlossen haben, verfügen über Einblicke.

![Instanz erstellen](../images/insights/dashboard.png)

Wählen Sie einen Dienstinstanznamen aus, der gestartet werden soll.

![Instanz erstellen](../images/insights/click-the-name.png)

Als Nächstes wird die Insight-Seite für diese Dienstinstanz mit der Option &quot;**[!UICONTROL Neueste Bewertungen]**&quot;oder &quot;**[!UICONTROL Leistungszusammenfassung]**&quot;angezeigt. Die Standardregisterkarte **[!UICONTROL Neueste Bewertungen]** enthält Visualisierungen Ihrer Daten. Die Visualisierungen und die Möglichkeiten, die Daten zu nutzen, werden in diesem Handbuch ausführlicher erläutert.

Die Registerkarte **[!UICONTROL Leistungszusammenfassung]** enthält die tatsächlichen Abwanderungs- oder Konversionsraten für jeden Neigungsbehälter. Weitere Informationen finden Sie im Abschnitt zu den Metriken mit der [Leistungszusammenfassung](#performance-metrics).

![Setup-Seite](../images/insights/landing_page_insights.png)

## Details zur Dienstinstanz

Es gibt zwei Möglichkeiten, Details der Dienstinstanz anzuzeigen: über das Dashboard oder innerhalb der Dienstinstanz.

### Dashboard der Dienstinstanz

Um eine Übersicht über die Details der Dienstinstanz im Dashboard anzuzeigen, wählen Sie einen Dienstinstanzcontainer aus, wobei der mit dem Namen verknüpfte Hyperlink vermieden wird. Dadurch wird eine rechte Leiste mit zusätzlichen Details geöffnet. Die Steuerelemente enthalten Folgendes:

- **[!UICONTROL Bearbeiten]**: Durch Auswahl von **[!UICONTROL Bearbeiten]** können Sie eine vorhandene Dienstinstanz ändern. Sie können den Namen, die Beschreibung und die Scoring-Häufigkeit der Instanz bearbeiten.
- **[!UICONTROL Klonen]**: Durch Auswahl von **[!UICONTROL Klonen]** wird die derzeit ausgewählte Dienstinstanz kopiert, die eingerichtet ist. Anschließend können Sie den Workflow ändern, um kleinere Änderungen vorzunehmen, und ihn in eine neue Instanz umbenennen.
- **[!UICONTROL Löschen]**: Sie können eine Dienstinstanz, einschließlich aller historischen Ausführungen, löschen.
- **[!UICONTROL Datenquelle]**: Ein Link zu dem von dieser Instanz verwendeten Datensatz.
- **[!UICONTROL Ausführungsfrequenz]**: Wie oft und wann ein Scoring ausgeführt wird.
- **[!UICONTROL Score-Definition]**: Ein kurzer Überblick über das Ziel, das Sie für diese Instanz konfiguriert haben.

![](../images/user-guide/service-instance-panel.png)

>[!NOTE]
>
>Wenn ein Scoring-Lauf fehlschlägt, wird eine Fehlermeldung angezeigt. Die Fehlermeldung wird unter **Letzte Ausführungsdetails** in der rechten Leiste aufgeführt, die nur für fehlgeschlagene Ausführungen sichtbar ist.

![Fehlerausführungsmeldung](../images/insights/failed-run.png)

### Dropdown &quot;Weitere Einblicke anzeigen&quot;

Die zweite Möglichkeit, zusätzliche Details für eine Dienstinstanz anzuzeigen, finden Sie auf der Insight-Seite. Wählen Sie oben rechts **[!UICONTROL Mehr anzeigen]** aus, um eine Dropdown-Liste zu füllen. Details wie die Punktzahl-Definition, der Erstellungszeitpunkt, der Tendenztyp und die verwendeten Datensätze werden aufgelistet. Weitere Informationen zu den aufgelisteten Eigenschaften finden Sie unter [Konfigurieren einer Customer AI-Instanz](./configure.md).

![Mehr anzeigen](../images/insights/landing-show-more.png)

### Popover zur Vorschau von Customer AI-Datensätzen

Wenn mehrere Datensätze von Customer AI verwendet werden, wird ein Hyperlink mit der Bezeichnung **[!UICONTROL Mehrere]** gefolgt von der Anzahl der Datensätze in eckigen Klammern `()` bereitgestellt.

![mehrere Datensätze](../images/insights/insights-multi-datasets.png)

Wenn Sie die Verknüpfung mit mehreren Datensätzen auswählen, wird das Popup-Fenster für die Vorschau des Customer AI-Datensatzes geöffnet. Jede Farbe in der Vorschau stellt einen Datensatz dar, wie der Farbschlüssel links neben den Datensatzspalten zeigt. In diesem Beispiel sehen Sie, dass nur **Datensatz 1** die Spalte `PROP1` enthält.

![Mehr anzeigen](../images/insights/dataset-preview.png)

### Bearbeiten einer Instanz

Um eine Instanz zu bearbeiten, wählen Sie in der oberen rechten Navigation **[!UICONTROL Bearbeiten]** aus.

![Auf Bearbeiten-Schaltfläche klicken](../images/insights/edit-button.png)

Das Dialogfeld &quot;Bearbeiten&quot;wird angezeigt, in dem Sie den Namen, die Beschreibung, den Status und die Scoring-Häufigkeit der Instanz bearbeiten können. Um Ihre Änderungen zu bestätigen und das Dialogfeld zu schließen, wählen Sie rechts unten **[!UICONTROL Speichern]** aus.

![Bearbeiten-Popup-Fenster](../images/insights/edit-instance.png)

### Mehr Aktionen

Die Schaltfläche **[!UICONTROL Mehr Aktionen]** befindet sich in der oberen rechten Navigation neben **[!UICONTROL Bearbeiten]**. Wenn Sie **[!UICONTROL Mehr Aktionen]** auswählen, wird eine Dropdown-Liste geöffnet, in der Sie einen der folgenden Vorgänge auswählen können:

- **[!UICONTROL Klonen]**: Durch Auswahl von **[!UICONTROL Klonen]** wird die eingerichtete Dienstinstanz kopiert. Anschließend können Sie den Workflow ändern, um kleinere Änderungen vorzunehmen, und ihn in eine neue Instanz umbenennen.
- **[!UICONTROL Löschen]**: Löscht die Instanz.
- **[!UICONTROL Auf Bewertungen zugreifen]**: Durch Auswahl von **[!UICONTROL Auf Bewertungen zugreifen]** wird ein Dialogfeld geöffnet, das einen Link zum Tutorial [Herunterladen von Bewertungen für Customer AI](./download-scores.md) enthält. Außerdem enthält das Dialogfeld die Datensatz-ID, die zum Ausführen von API-Aufrufen erforderlich ist.
- **[!UICONTROL Ausführungsverlauf anzeigen]**: Ein Dialogfeld mit einer Liste aller mit der Dienstinstanz verknüpften Scoring-Läufe wird angezeigt.

![Mehr Aktionen](../images/insights/more-actions.png)

## Bewertungszusammenfassung {#scoring-summary}

Die Bewertungszusammenfassung zeigt die Gesamtzahl der bewerteten Profile und kategorisiert sie in Behälter mit hoher, mittlerer und niedriger Tendenz. Die Tendenzbehälter werden anhand des Punktbereichs bestimmt, niedrig ist kleiner als 24, mittel ist 25 bis 74 und hoch ist über 74. Jeder Behälter hat eine der Legende entsprechende Farbe.

>[!NOTE]
>
>Wenn es sich um einen Konversionsintensitätswert handelt, werden die hohen Werte grün und die niedrigen Punkte rot angezeigt. Wenn Sie die Abwanderungsneigung vorhersagen, wird diese gespiegelt, die hohen Werte sind rot und die niedrigen Werte grün. Der mittlere Eimer bleibt gelb, unabhängig vom gewählten Tendenztyp.

![Bewertungszusammenfassung](../images/insights/scoring-summary.png)

Sie können den Mauszeiger über eine beliebige Farbe im Ring bewegen, um zusätzliche Informationen anzuzeigen, z. B. einen Prozentsatz und die Gesamtzahl der Profile, die zu einem Behälter gehören.

![](../images/insights/scoring-ring.png)

## Verteilung der Werte

Die Karte **[!UICONTROL Verteilung der Punktzahl]** bietet eine visuelle Zusammenfassung der Population basierend auf dem Ergebnis. Die Farben, die Sie auf der Karte [!UICONTROL Verteilung der Bewertungen] sehen, entsprechen dem Typ des generierten Tendenzwerts. Wenn Sie den Mauszeiger über eine der Scoring-Distributionen bewegen, erhalten Sie die genaue Anzahl, die zu dieser Distribution gehört.

![Verteilung der Punktzahl](../images/insights/distribution-of-scores.png)

## Einflussfaktoren

Für jeden Punktebehälter wird eine Karte generiert, die die 10 wichtigsten Einflussfaktoren für diesen Behälter anzeigt. Die Einflussfaktoren geben Ihnen zusätzliche Details darüber, warum Ihre Kunden zu verschiedenen Punktgruppen gehören.

![Einflussfaktoren](../images/insights/influential-factors.png)

### Drilldowns für Einflussfaktoren

Wenn Sie den Mauszeiger über einen der wichtigsten Einflussfaktoren bewegen, werden die Daten weiter aufgeschlüsselt. Sie erhalten eine Übersicht darüber, warum bestimmte Profile zu einer Tendenzbehälter gehören. Je nach Faktor können Ihnen Zahlenwerte, Kategorienwerte oder boolesche Werte zugewiesen werden. Das folgende Beispiel zeigt kategorische Werte nach Region.

![Drilldown-Screenshot](../images/insights/drilldown.png)

Darüber hinaus können Sie mithilfe von Drilldowns einen Verteilungsfaktor vergleichen, wenn er in zwei oder mehr Tendenzbehälter auftritt, und spezifischere Segmente mit diesen Werten erstellen. Das folgende Beispiel zeigt den ersten Anwendungsfall:

![](../images/insights/drilldown-compare.png)

Sie können sehen, dass Profile mit geringer Konversionsneigung einen kürzlichen Besuch auf den Webseiten adobe.com weniger wahrscheinlich gemacht haben. Der Faktor &quot;Tage seit dem letzten WebVisit&quot;deckt nur 8 % ab, verglichen mit 26 % bei mittleren Tendenzprofilen. Mithilfe dieser Zahlen können Sie die Verteilung innerhalb der einzelnen Behälter anhand des Faktors vergleichen. Diese Informationen können verwendet werden, um darauf hinzuweisen, dass die Neuigkeit bei Webbesuch im Bereich der geringen Tendenz nicht so einflussreich ist wie bei der Gruppe der mittleren Tendenz.

### Erstellen eines Segments

Wenn Sie die Schaltfläche **[!UICONTROL Segment erstellen]** in einem der Behälter für niedrige, mittlere und hohe Neigung auswählen, werden Sie zum Segment-Builder weitergeleitet.

>[!NOTE]
>
>Die Schaltfläche **[!UICONTROL Segment erstellen]** ist nur verfügbar, wenn das Echtzeit-Kundenprofil für den Datensatz aktiviert ist. Weitere Informationen zum Aktivieren des Echtzeit-Kundenprofils finden Sie in der Übersicht über das [Echtzeit-Kundenprofil](../../../rtcdp/overview.md) .

![Klicken Sie auf Segment erstellen](../images/insights/influential-factors-create-segment.png)

![Erstellen eines Segments](../images/insights/create-segment.png)

Der Segment Builder wird verwendet, um ein Segment zu definieren. Bei Auswahl von **[!UICONTROL Segment erstellen]** auf der Seite &quot;Einblicke&quot;fügt Customer AI die ausgewählten Behälterinformationen automatisch zum Segment hinzu. Um die Erstellung Ihres Segments abzuschließen, füllen Sie einfach die Container **Name** und **Beschreibung** aus, die sich in der rechten Leiste der Benutzeroberfläche des Segmentaufbaus befinden. Nachdem Sie dem Segment einen Namen und eine Beschreibung gegeben haben, wählen Sie oben rechts **[!UICONTROL Speichern]** aus.

>[!NOTE]
>
>Da die Tendenzwerte in das jeweilige Profil geschrieben werden, sind sie im Segment Builder wie alle anderen Profilattribute verfügbar. Wenn Sie zum Segment Builder navigieren, um neue Segmente zu erstellen, können Sie alle verschiedenen Tendenzwerte unter Ihrem Namespace Customer AI anzeigen.

![Segmentfüllung in ](../images/insights/segment-saving.png)

Um Ihr neues Segment in der Platform-Benutzeroberfläche anzuzeigen, wählen Sie im linken Navigationsbereich **[!UICONTROL Segmente]** aus. Die Seite **[!UICONTROL Durchsuchen]** wird angezeigt und zeigt alle verfügbaren Segmente an.

![Alle Ihre Segmente](../images/insights/Segments-dashboard.png)

## Historische Leistung {#historical-performance}

Die Registerkarte **[!UICONTROL Leistungszusammenfassung]** enthält die tatsächlichen Abwanderungs- oder Konversionsraten, die in die von Customer AI bewerteten Tendenzbehälter aufgeteilt sind.

![Registerkarte &quot;Leistungszusammenfassung&quot;](../images/insights/summary_tab.png)

Zunächst werden nur erwartete Raten (gepunktete Linien) angezeigt. Die erwarteten Raten werden angezeigt, wenn kein Scoring-Lauf stattgefunden hat und noch keine Daten verfügbar sind. Sobald jedoch ein Ergebnisfenster vorüber ist, wird die erwartete Rate durch eine tatsächliche Rate (feste Linie) ersetzt.

Wenn Sie den Mauszeiger über die Zeilen bewegen, werden das Datum und die tatsächliche/erwartete Rate für diesen Tag in diesem Behälter angezeigt.

![Bucket-Beispiel](../images/insights/churn_tab.png)

Sie können den Zeitrahmen nach den erwarteten und tatsächlichen angezeigten Raten filtern. Wählen Sie das Symbol **Kalendersymbol** ![ ](/help/images/icons/calendar.png) und dann einen neuen Datumsbereich aus. Die Ergebnisse in den einzelnen Behältern werden aktualisiert und innerhalb des neuen Datumsbereichs angezeigt.

![Datumsauswahl](../images/insights/date_selector.png)

### Individuelle Scoring-Ausführungsraten

In der unteren Hälfte der Registerkarte **[!UICONTROL Leistungszusammenfassung]** werden die Ergebnisse für jeden einzelnen Scoring-Lauf angezeigt. Wählen Sie das Dropdown-Datum oben rechts aus, um die Ergebnisse für einen anderen Scoring-Lauf anzuzeigen.

Je nachdem, ob Sie Abwanderung oder Konversion vorhersagen, zeigt das Diagramm [!UICONTROL Verteilung der Werte] die Verteilung der Profile an, die in jeder einzelnen Erhöhung aktiviert/konvertiert und nicht umgestellt/nicht konvertiert wurden.

![individuelles Scoring](../images/insights/scoring_tab.png)

## Modellauswertung {#model-evaluation}

Zusätzlich zum Tracking der prognostizierten und tatsächlichen Ergebnisse im Zeitverlauf auf der Registerkarte &quot;Historische Leistung&quot;haben Marketingexperten im Tab Modellauswertung noch mehr Transparenz in Bezug auf die Modellqualität. Sie können die Diagramme Steigerung und Gewinne verwenden, um die Unterschiede bei der Verwendung eines prädiktiven Modells im Vergleich zum zufälligen Targeting zu ermitteln. Darüber hinaus können Sie bestimmen, wie viele positive Ergebnisse bei jedem Score-Cutoff erfasst werden. Dies ist nützlich für die Segmentierung und für die Abstimmung der Kapitalrendite auf Marketing-Aktionen.

### Lift-Diagramm

![Steigerungsdiagramm](../images/user-guide/lift-chart.png)

Das Steigerungsdiagramm misst die Verbesserung der Verwendung eines Vorhersagemodells anstelle von zufälligem Targeting.

Zu den hochwertigen Modellindikatoren gehören:

- Hohe Steigerungswerte in den ersten Dezimalstellen. Das bedeutet, dass das Modell gut darin ist, die Benutzer zu identifizieren, die die größte Neigung haben, die gewünschten Aktionen durchzuführen.
- Absteigende Steigerungswerte Dies bedeutet, dass Kunden mit höheren Werten mit höherer Wahrscheinlichkeit die Aktion von Interesse ausführen als Kunden mit niedrigeren Werten.

### Gewinnerdiagramm

![Gewinndiagramm](../images/user-guide/gains-chart.png)

Das Diagramm für kumulative Gewinne misst den Prozentsatz der positiven Ergebnisse, die durch Targeting-Ergebnisse über einem bestimmten Schwellenwert erfasst werden. Nach Sortierung der Kunden nach Tendenzwert von hoch bis niedrig wird die Population in Dezimalstellen aufgeteilt - 10 gleich große Gruppen. Ein perfektes Modell würde alle positiven Ergebnisse in den höchsten Punktzahlen erfassen. Eine zufällige Basismethode erfasst positive Ergebnisse proportional zur Größe der Gruppe. Bei der Zielgruppenbestimmung würden 30 % der Benutzer 30 % der Ergebnisse erfassen.

Zu den hochwertigen Modellindikatoren gehören:

- Die kumulierten Gewinne nähern sich 100% schnell.
- Die kumulierte Gewinnkurve für das Modell ist näher an der oberen linken Ecke des Diagramms.
- Das Diagramm für kumulierte Gewinne kann verwendet werden, um die Bewertungsabbrüche für die Segmentierung und das Targeting zu bestimmen. Wenn das Modell beispielsweise 70 % der positiven Ergebnisse in den ersten 2 Bewertungsdezimeln erfasst, wird erwartet, dass das Targeting von Benutzern mit PerzentilScore > 80 ca. 70 % der positiven Ergebnisse erfasst.

### AUC (Fläche unter der Kurve)

Die AUC spiegelt die Stärke der Beziehung zwischen dem Rang nach Bewertung und dem Auftreten des prognostizierten Ziels wider. Ein **AUC** -Wert von 0,5 bedeutet, dass das Modell nicht besser ist als eine zufällige Schätzung. Eine **AUC** von 1 bedeutet, dass das Modell perfekt vorhersagen kann, wer die entsprechende Aktion ausführen wird.

## Nächste Schritte

In diesem Dokument wurden die Einblicke einer Customer AI-Dienstinstanz beschrieben. Sie können jetzt mit dem Tutorial zum Herunterladen von Bewertungen in Customer AI](./download-scores.md) fortfahren oder die anderen verfügbaren Handbücher für Adobe Intelligent Services](../../home.md) durchsuchen.[[

## Zusätzliche Ressourcen

Im folgenden Video wird beschrieben, wie Sie mit Customer AI die Ausgabe der Modelle und Einflussfaktoren anzeigen können.

>[!VIDEO](https://video.tv.adobe.com/v/32666?learn=on&quality=12)
