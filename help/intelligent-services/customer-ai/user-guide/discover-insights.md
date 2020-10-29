---
keywords: Experience Platform;insights;customer ai;popular topics;customer ai insights
solution: Experience Platform
title: Einblicke in die Kundentechnik
topic: Discovering insights
description: Dieses Dokument dient als Leitfaden für die Interaktion mit Dienstinstanzinformationen in der Benutzeroberfläche der Intelligent Services Customer AI.
translation-type: tm+mt
source-git-commit: 0b92346065b7c9615d8aef4c9b13c84e0383b4b9
workflow-type: tm+mt
source-wordcount: '1389'
ht-degree: 12%

---


# Einblicke in die Kundentechnik

Die Kundentechnik als Teil von Intelligent Services bietet Marketern die Möglichkeit, Adobe Sensei zu nutzen, um vorherzusehen, was Ihre Kunden als Nächstes tun werden. Customer AI wird verwendet, um für einzelne Profile skaliert benutzerdefinierte Tendenzwerte wie Abwanderung und Konversion zu berechnen. Das ist möglich, ohne dass die geschäftlichen Anforderungen in eine Aufgabe für maschinelles Lernen umgewandelt werden müssen, indem ein Algorithmus, ein Training oder eine Implementierung ausgewählt wird.

Dieses Dokument dient als Leitfaden für die Interaktion mit Dienstinstanzinformationen in der Benutzeroberfläche der Intelligent Services Customer AI.

## Erste Schritte

Um Einblicke in die Kundenaktivität zu erhalten, benötigen Sie eine Dienstinstanz mit einem erfolgreichen Ausführungsstatus. Um eine neue Dienstinstanz zu erstellen, besuchen Sie [Konfigurieren einer Kunden-AI-Instanz](./configure.md). Wenn Sie kürzlich eine Dienstinstanz erstellt haben und diese sich noch in der Trainings- und Bewertungsphase befindet, warten Sie bitte 24 Stunden, bis sie fertig ist.

## Übersicht über die Dienstinstanzen

In the [!DNL Adobe Experience Platform] UI, click **[!UICONTROL Services]** in the left navigation. Der *Dienste*-Browser wird geöffnet und zeigt verfügbare Intelligent Services an. Klicken Sie im Container für Customer AI auf **[!UICONTROL Öffnen]**.

![Zugreifen auf Ihre Instanz](../images/insights/navigate-to-service.png)

Die Seite zum Kundendienst wird angezeigt. Auf dieser Seite werden Dienstinstanzen der Kunden-API Liste und Informationen zu diesen Instanzen, einschließlich Instanzname, Tendenztyp, Häufigkeit der Ausführung der Instanz und Status der letzten Aktualisierung, angezeigt.

>[!NOTE]
>
>Nur Dienstinstanzen, die erfolgreiche Testläufe abgeschlossen haben, haben Einblicke.

![Instanz erstellen](../images/insights/dashboard.png)

Klicken Sie zuerst auf den Namen einer Dienstinstanz.

![Instanz erstellen](../images/insights/click-the-name.png)

Als Nächstes wird die Einblicke-Seite für diese Dienstinstanz angezeigt, auf der Sie Visualisierungen Ihrer Daten erhalten. Die Visualisierungen und die Möglichkeiten, die Sie mit den Daten haben, werden in diesem Handbuch ausführlicher erläutert.

![Setup-Seite](../images/insights/landing-page.png)


### Details zur Dienstinstanz

Es gibt zwei Möglichkeiten, Dienstinstanzdetails Ansicht: aus dem Dashboard oder innerhalb der Dienstinstanz.

Um eine Übersicht über die Details der Dienstinstanz im Dashboard Ansicht, wählen Sie einen Dienstinstanz-Container aus, wobei der mit dem Namen verknüpfte Hyperlink vermieden werden soll. Dadurch wird eine rechte Leiste mit weiteren Details geöffnet. Die Steuerelemente enthalten Folgendes:

- **[!UICONTROL Bearbeiten]**: Durch Auswahl von **[!UICONTROL Bearbeiten]** können Sie eine vorhandene Dienstinstanz ändern. Sie können den Namen, die Beschreibung und die Bewertungsfrequenz der Instanz bearbeiten.
- **[!UICONTROL Klonen]**: Durch Auswahl von **[!UICONTROL Klonen]** wird die aktuell ausgewählte Dienstinstanz kopiert, die eingerichtet wurde. Anschließend können Sie den Workflow ändern, um kleinere Änderungen vorzunehmen und ihn als neue Instanz umzubenennen.
- **[!UICONTROL Löschen]**: Sie können eine Dienstinstanz einschließlich aller historischen Ausführung löschen.
- **[!UICONTROL Datenquelle]**: Ein Link zum Datensatz, der von dieser Instanz verwendet wird.
- **[!UICONTROL Ausführungsfrequenz]**: Wie oft und wann eine Punktwertung stattfindet.
- **[!UICONTROL Score-Definition]**: Eine schnelle Übersicht über das Ziel, das Sie für diese Instanz konfiguriert haben.

![](../images/user-guide/service-instance-panel.png)

>[!NOTE]
>
>In dem Ereignis, dass eine Bewertungsausführung fehlschlägt, wird eine Fehlermeldung angezeigt. Die Fehlermeldung wird unter **Letzte Ausführung Details** in der rechten Leiste aufgeführt, die nur für fehlgeschlagene Ausführung sichtbar ist.

![fehlgeschlagene Ausführungsmeldung](../images/insights/failed-run.png)

Die zweite Möglichkeit zur Ansicht zusätzlicher Details für eine Dienstinstanz befindet sich auf der Einblicke-Seite. Sie können oben rechts auf Mehr **** anzeigen klicken, um eine Dropdown-Liste auszufüllen. Details werden aufgelistet, wie die Score-Definition, der Erstellungszeitpunkt und der Tendenztyp. Weitere Informationen zu den aufgelisteten Eigenschaften finden Sie unter [Konfigurieren einer Kunden-AI-Instanz](./configure.md).

![Mehr anzeigen](../images/insights/landing-show-more.png)

![Mehr anzeigen](../images/insights/show-more.png)

### Bearbeiten einer Instanz

Um eine Instanz zu bearbeiten, klicken Sie in oben rechts in der Navigation auf **[!UICONTROL Bearbeiten]**.

![Auf Bearbeiten-Schaltfläche klicken](../images/insights/edit-button.png)

Das Dialogfeld &quot;Bearbeiten&quot;wird angezeigt, in dem Sie den Namen, die Beschreibung, den Status und die Bewertungsfrequenz der Instanz bearbeiten können. To confirm your changes and close the dialog, select **[!UICONTROL Save]** in the bottom-right corner.

![Bearbeiten-Popup-Fenster](../images/insights/edit-instance.png)

### Mehr Aktionen

Die Schaltfläche **[!UICONTROL Mehr Aktionen]** befindet sich in der oberen rechten Navigation neben **[!UICONTROL Bearbeiten]**. Wenn Sie auf **[!UICONTROL Mehr Aktionen]** klicken, wird ein Dropdown-Menü geöffnet, in dem Sie eine der folgenden Vorgänge auswählen können:

- **[!UICONTROL Klonen]**: Durch Auswahl von **[!UICONTROL Klonen]** wird die eingerichtete Dienstinstanz kopiert. Anschließend können Sie den Workflow ändern, um kleinere Änderungen vorzunehmen und ihn als neue Instanz umzubenennen.
- **[!UICONTROL Löschen]**: Löscht die Instanz.
- **[!UICONTROL Zugangsdaten]**: Durch Auswahl von **[!UICONTROL Zugriffsergebnissen]** wird ein Dialogfeld geöffnet, das einen Link zu den [Download-Ergebnissen für das Tutorial zur Kundenwerbung](./download-scores.md) enthält. Außerdem enthält das Dialogfeld die Dataset-ID, die zum Aufrufen von API-Aufrufen erforderlich ist.
- **[!UICONTROL Ansicht-Ausführungsverlauf]**: Ein Dialogfeld mit einer Liste aller mit der Dienstinstanz verknüpften Bewertungsläufe wird angezeigt.

![Mehr Aktionen](../images/insights/more-actions.png)

## Bewertungszusammenfassung {#scoring-summary}

Die Bewertungszusammenfassung zeigt die Gesamtanzahl der bewerteten Profil an und kategorisiert sie in Behälter mit hoher, mittlerer und niedriger Tendenz. Die Tendenzbehälter werden basierend auf dem Ergebnisbereich bestimmt, niedrig ist weniger als 24, mittel ist 25 bis 74 und hoch ist über 74. Jeder Behälter hat eine Farbe, die der Legende entspricht.

>[!NOTE]
>
>Wenn es sich um einen Umrechnungsneigungswert handelt, werden die hohen Werte grün und die niedrigen Werte rot angezeigt. Wenn Sie die Kürbisneigung vorhersagen, wird diese umgedreht, die hohen Werte sind in Rot und die niedrigen Werte sind grün. Der mittlere Eimer bleibt gelb, unabhängig vom gewählten Tendenztyp.

![Bewertungszusammenfassung](../images/insights/scoring-summary.png)

Wenn Sie den Mauszeiger über eine beliebige Farbe auf dem Ring halten, werden zusätzliche Informationen wie die prozentuale und die Gesamtanzahl der Profil, die zu einem Behälter gehören, Ansicht.

![](../images/insights/scoring-ring.png)

## Verteilung der Ergebnisse

Die Karte **[!UICONTROL Verteilung der Ergebnisse]** gibt Ihnen eine visuelle Zusammenfassung der Population, die auf dem Ergebnis basiert. Die Farben, die Sie in der Karte [!UICONTROL Verteilung der Ergebnisse] sehen, stellen die Art des generierten Tendenzwerts dar. Wenn Sie den Mauszeiger über eine der Scoring-Distributionen bewegen, erhalten Sie die exakte Anzahl, die zu dieser Distribution gehört.

![Verteilung der Ergebnisse](../images/insights/distribution-of-scores.png)

## Einflussfaktoren

Für jeden Ergebnisbehälter wird eine Karte generiert, die die 10 wichtigsten Einflussfaktoren für diesen Behälter anzeigt. Die einflussreichen Faktoren geben Ihnen zusätzliche Informationen darüber, warum Ihre Kunden zu verschiedenen Ergebnisbehältern gehören.

![Einflussfaktoren](../images/insights/influential-factors.png)

### Abdrillen von Einflussfaktoren

Wenn Sie den Mauszeiger über einen der wichtigsten einflussreichsten Faktoren bewegen, werden die Daten weiter aufgeschlüsselt. Sie erhalten einen Überblick darüber, warum bestimmte Profil zu einem Tendenzbehälter gehören. Je nach Faktor können Sie Zahlenwerte, kategorische oder boolesche Werte erhalten. Im folgenden Beispiel werden kategorische Werte nach Region angezeigt.

![Drilldown-Screenshot](../images/insights/drilldown.png)

Darüber hinaus können Sie mithilfe von Drilldowns einen Verteilungsfaktor vergleichen, wenn er in zwei oder mehr Tendenzbehältern auftritt, und spezifischere Segmente mit diesen Werten erstellen. Im folgenden Beispiel wird der erste Verwendungsfall veranschaulicht:

![](../images/insights/drilldown-compare.png)

Sie können sehen, dass Profil mit geringer Tendenz zur Konvertierung weniger häufig die Websites adobe.com besucht haben. Der Faktor &quot;Tage seit dem letzten WebVisit&quot;deckt nur 8% ab, verglichen mit 26% in mittelständischen Profilen. Mithilfe dieser Zahlen können Sie die Verteilung innerhalb der Behälter für den Faktor vergleichen. Diese Informationen können verwendet werden, um zu erkennen, dass die Neuigkeit im Webvisit nicht so einflussreich im Bucket mit niedriger Tendenz ist, wie es in der Gruppe mit mittlerer Tendenz der Fall ist.

### Erstellen eines Segments

Durch Auswahl der Schaltfläche Segment **** erstellen in einer der Behälter für niedrige, mittlere und hohe Tendenz werden Sie zum Segmentaufbau weitergeleitet.

>[!NOTE]
>
>Die Schaltfläche &quot;Segment **** erstellen&quot;ist nur verfügbar, wenn für den Datensatz das Kundenkonto in Echtzeit aktiviert ist. Weitere Informationen zur Aktivierung von Echtzeit-Kundendaten finden Sie in der Übersicht über das [Echtzeit-Profil](../../../rtcdp/overview.md).

![Klicken Sie auf Segment erstellen](../images/insights/influential-factors-create-segment.png)

![Erstellen eines Segments](../images/insights/create-segment.png)

Mit dem Segmentaufbau wird ein Segment definiert. Wenn Sie auf der Seite &quot;Einblicke&quot;die Option Segment **** erstellen auswählen, fügt die Kunden-API dem Segment automatisch die ausgewählten Behälterinformationen hinzu. Füllen Sie zum Abschluss der Segmenterstellung einfach die Container *Name* und *Beschreibung* in der rechten Leiste der Segment Builder-Benutzeroberfläche aus. Nachdem Sie dem Segment einen Namen und eine Beschreibung gegeben haben, klicken Sie oben rechts auf **[!UICONTROL Speichern]** .

>[!NOTE]
>
>Da die Tendenzwerte in das jeweilige Profil geschrieben werden, sind sie wie alle anderen Segmentattribute im Segmentaufbau verfügbar. Wenn Sie zum Segmentaufbau navigieren, um neue Segmente zu erstellen, können Sie alle verschiedenen Tendenzwerte unter Ihrer Namensraum Customer AI sehen.

![Segmentfüllung](../images/insights/segment-saving.png)

Um Ihr neues Segment in der Plattform-Benutzeroberfläche Ansicht, klicken Sie im linken Navigationsbereich auf **[!UICONTROL Segmente]** . Die Seite &quot; **[!UICONTROL Durchsuchen]** &quot;wird angezeigt und zeigt alle verfügbaren Segmente an.

![Alle Segmente](../images/insights/Segments-dashboard.png)

## Nächste Schritte

In diesem Dokument werden die Einblicke einer Instanz des Kundenservice erläutert. Sie können jetzt das Tutorial zum [Herunterladen von Punktzahlen in der Kundenaktivität](./download-scores.md) fortsetzen oder die anderen angebotenen [Adobe Intelligent Services](../../home.md) -Handbücher durchsuchen.

## Zusätzliche Ressourcen

In dem folgenden Video wird erläutert, wie die KUNDENKI verwendet werden kann, um die Ausgabe der Modelle und einflussreichen Faktoren zu sehen.

>[!VIDEO](https://video.tv.adobe.com/v/32666?learn=on&quality=12)