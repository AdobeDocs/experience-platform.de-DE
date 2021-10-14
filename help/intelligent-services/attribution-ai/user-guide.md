---
keywords: Experience Platform; Benutzerhandbuch; Attribution; beliebte Themen; Region
feature: Attribution AI
title: Benutzerhandbuch zu Attribution AI
topic-legacy: User guide
description: Dieses Dokument dient als Leitfaden für die Interaktion mit Attribution AI in der Benutzeroberfläche von Intelligent Services.
exl-id: 32e1dd07-31a8-41c4-88df-8893ff773f79
source-git-commit: c3320f040383980448135371ad9fae583cfca344
workflow-type: tm+mt
source-wordcount: '1765'
ht-degree: 6%

---

# Handbuch zur Benutzeroberfläche von Attribution AI

Attribution AI als Teil von Intelligent Services ist ein algorithmischer Attributionsdienst mit mehreren Kanälen, der den Einfluss und die inkrementelle Auswirkung von Kundeninteraktionen auf bestimmte Ergebnisse berechnet. Mit Attribution AI können Marketing-Experten die Ausgaben für Marketing und Werbung messen und optimieren, indem sie die Auswirkungen einzelner Kundeninteraktionen in einzelnen Phasen der Customer Journey untersuchen.

Dieses Dokument dient als Leitfaden für die Interaktion mit Attribution AI in der Benutzeroberfläche von Intelligent Services.

## Erstellen einer Instanz

Klicken Sie in der [!DNL Adobe Experience Platform] -Benutzeroberfläche im linken Navigationsbereich auf **[!UICONTROL Dienste]** . Der Browser **[!UICONTROL Dienste]** wird angezeigt und zeigt verfügbare Adobe Intelligent Services an. Klicken Sie im Container für Attribution AI auf **[!UICONTROL Öffnen]**.

![Zugreifen auf Ihre Instanz](./images/user-guide/open_Attribution_ai.png)

Die Seite des Attribution AI-Service wird angezeigt. Auf dieser Seite werden Dienstinstanzen von Attribution AI aufgelistet und Informationen zu diesen angezeigt, einschließlich des Namens der Instanz, der Konversionsereignisse, der Häufigkeit der Ausführung der Instanz und des Status der letzten Aktualisierung.

Sie finden die Metrik **[!UICONTROL Gesamte Konversionsereignisse, die]** bewertet wurden, unten rechts im Container **[!UICONTROL Instanz erstellen]** . Diese Metrik verfolgt die Gesamtzahl der Konversionsereignisse, die von Attribution AI für das aktuelle Kalenderjahr bewertet wurden, einschließlich aller Sandbox-Umgebungen und aller gelöschten Dienstinstanzen.

![](./images/user-guide/total_conversions.png)

Dienstinstanzen können mithilfe der Steuerelemente auf der rechten Seite der Benutzeroberfläche bearbeitet, geklont und gelöscht werden. Um diese Steuerelemente anzuzeigen, wählen Sie eine Instanz aus Ihren vorhandenen **[!UICONTROL Dienstinstanzen]** aus. Die Steuerelemente enthalten die folgenden Informationen:

- **[!UICONTROL Bearbeiten]**: Durch Auswahl von  **** Bearbeiten können Sie eine vorhandene Dienstinstanz ändern. Sie können den Namen, die Beschreibung, den Status und die Scoring-Häufigkeit der Instanz bearbeiten.
- **[!UICONTROL Klonen]**: Durch Auswahl von  **** Clonecopies wird die ausgewählte Dienstinstanz kopiert. Anschließend können Sie den Workflow ändern, um kleinere Änderungen vorzunehmen, und ihn in eine neue Instanz umbenennen.
- **[!UICONTROL Löschen]**: Sie können eine Dienstinstanz einschließlich aller historischen Ausführungen löschen.
- **[!UICONTROL Datenquelle]**: Ein Link zum Datensatz, der von dieser Instanz verwendet wird.
- **[!UICONTROL Letzte Ausführungsdetails]**: Dies wird nur angezeigt, wenn eine Ausführung fehlschlägt. Informationen dazu, warum die Ausführung fehlgeschlagen ist, wie Fehlercodes, werden hier angezeigt.

![](./images/user-guide/side_panel.png)

- **[!UICONTROL Konversionsereignisse]**: Ein kurzer Überblick über die für diese Instanz konfigurierten Konversionsereignisse.
- **[!UICONTROL Lookback-Fenster]**: Der von Ihnen definierte Zeitrahmen, der angibt, wie viele Tage vor den Touchpoints des Konversionsereignisses vergangen sind.
- **[!UICONTROL Touchpoints]**: Eine Liste aller Touchpoints, die Sie beim Erstellen dieser Instanz definiert haben.

![](./images/user-guide/side_panel_2.png)

Wählen Sie **[!UICONTROL Instanz erstellen]** aus, um zu beginnen.

![Instanz erstellen](./images/user-guide/landing_page.png)

Als Nächstes wird die Setup-Seite für Attribution AI angezeigt, auf der Sie grundlegende Informationen bereitstellen und einen Datensatz für die Instanz angeben können.

![Setup-Seite](./images/user-guide/setup_attribution.png)

### Benennen Sie die Instanz.

Geben Sie unter **[!UICONTROL Grundlegende Informationen]** einen Namen und eine optionale Beschreibung für Ihre Dienstinstanz ein.

![Benennen einer Instanz](./images/user-guide/naming_instance.png)

### Datensatz auswählen

Nachdem Sie die grundlegenden Informationen ausgefüllt haben, klicken Sie auf das Dropdown-Menü **Datensatz auswählen**, um Ihren Datensatz auszuwählen. Der Datensatz wird verwendet, um das Modell zu trainieren und die nachfolgenden Daten zu bewerten, die es erzeugt. Bei der Auswahl eines Datensatzes aus der Dropdown-Auswahl werden nur Datensätze aufgelistet, die mit Attribution AI kompatibel sind und dem Experience-Datenmodell (XDM)-Schema entsprechen. Nachdem Sie einen Datensatz ausgewählt haben, klicken Sie in der oberen rechten Ecke auf **Weiter** , um mit der Seite &quot;Ereignisse definieren&quot;fortzufahren.

>[!TIP]
>
>Adobe Analytics-Datensätze werden über Analytics Source Connector unterstützt.

![Setup-Seite](./images/user-guide/dataset_selector.png)

## Ereignisse definieren

Es gibt drei verschiedene Arten von Eingabedaten, die zur Definition von Ereignissen verwendet werden:

- **Konversionsereignisse:**  Geschäftsziele, die die Auswirkungen von Marketing-Aktivitäten identifizieren, wie z. B. E-Commerce-Bestellungen, In-Store-Käufen und Website-Besuchen.
- **Lookback-Fenster:** Bietet einen Zeitrahmen, der angibt, wie viele Tage vor den Touchpoints des Konversionsereignisses eingeschlossen werden sollen.
- **Touchpoints:** Marketing-Ereignisse auf Empfänger-, Kontakt- und Cookie-Ebene, die zur Bewertung der numerischen oder umsatzbasierten Auswirkungen von Konversionen verwendet werden.

### Konversionsereignisse definieren {#define-conversion-events}

Um ein Konversionsereignis zu definieren, müssen Sie dem Ereignis einen Namen geben und den Ereignistyp auswählen, indem Sie auf das Dropdown-Menü **Feldname eingeben** klicken.

![Ja Dropdown](./images/user-guide/conversion_event_2.png)

Sobald ein Ereignis ausgewählt ist, wird rechts ein neues Dropdown-Menü angezeigt. Das zweite Dropdown-Menü wird verwendet, um durch die Verwendung von Vorgängen weiteren Kontext für Ihr Ereignis bereitzustellen. Für dieses Konversionsereignis wird der Standardvorgang *exists* verwendet.

>[!NOTE]
>
>Eine Zeichenfolge unter *Konversionsname* wird aktualisiert, wenn Sie Ihr Ereignis definieren.

![kein Dropdown](./images/user-guide/conversion_event_1.png)

Die Schaltflächen **[!UICONTROL Ereignis hinzufügen]** und **[!UICONTROL Gruppe hinzufügen]** werden verwendet, um Ihre Konvertierung weiter zu definieren. Je nach der von Ihnen definierten Konversion müssen Sie möglicherweise die Schaltflächen **[!UICONTROL Ereignis hinzufügen]** und **[!UICONTROL Gruppe hinzufügen]** verwenden, um weiteren Kontext bereitzustellen.

![Ereignis hinzufügen](./images/user-guide/add_event.png)

Durch Klicken auf **[!UICONTROL Ereignis hinzufügen]** werden zusätzliche Felder erstellt, die mit der oben beschriebenen Methode ausgefüllt werden können. Hierdurch wird der Zeichenfolgendefinition unter dem Konversionsnamen eine AND-Anweisung hinzugefügt. Klicken Sie auf **x**, um ein hinzugefügtes Ereignis zu entfernen.

![Ereignismenü hinzufügen](./images/user-guide/add_event_result.png)

Wenn Sie auf **[!UICONTROL Gruppe hinzufügen]** klicken, können Sie zusätzliche Felder erstellen, die vom Original getrennt sind. Durch Hinzufügen von Gruppen wird eine blaue *Und*-Schaltfläche angezeigt. Durch Klicken auf **Und** erhalten Sie eine Option, den Parameter so zu ändern, dass er &quot;Oder&quot;enthält. &quot;Oder&quot;wird verwendet, um mehrere erfolgreiche Konversionspfade zu definieren. &quot;Und&quot;erweitert den Konversionspfad um zusätzliche Bedingungen.

![und](./images/user-guide/and_or.png)

Wenn Sie mehr als eine Konvertierung benötigen, klicken Sie auf **Konvertierung hinzufügen** , um eine neue Konversionskarte zu erstellen. Sie können den obigen Prozess wiederholen, um mehrere Konversionen zu definieren.

![Konvertierung hinzufügen](./images/user-guide/add_conversion.png)

### Lookback-Fenster definieren {#lookback-window}

Nachdem Sie die Definition Ihrer Konvertierung abgeschlossen haben, müssen Sie Ihr Lookback-Fenster bestätigen. Geben Sie mithilfe der Pfeiltasten oder durch Klicken auf den Standardwert (56) an, wie viele Tage vor dem Konversionsereignis Sie Touchpoints einbeziehen möchten. Touchpoints werden im nächsten Schritt definiert.

![Lookback](./images/user-guide/lookback_window.png)

### Definieren von Touchpoints

Die Definition von Touchpoints folgt einem ähnlichen Workflow wie [Definieren von Konversionen](#define-conversion-events). Zunächst müssen Sie Ihren Touchpoint benennen und einen Touchpoint-Wert aus dem Dropdown-Menü *Feldname eingeben* auswählen. Nach der Auswahl wird das Dropdown-Menü für den Operator mit dem Standardwert &quot;vorhanden&quot;angezeigt. Klicken Sie auf das Dropdown-Menü, um eine Liste der Benutzer anzuzeigen.

![Operatoren](./images/user-guide/operators.png)

Wählen Sie für diesen Touchpoint **gleich** aus.

![Schritt 1](./images/user-guide/touchpoint_step1.png)

Sobald ein Operator für einen Touchpoint ausgewählt ist, wird *Feldwert eingeben* verfügbar gemacht. Die Dropdown-Werte für *Feldwert eingeben* werden basierend auf dem zuvor ausgewählten Operator- und Touchpoint-Wert gefüllt. Wenn ein Wert nicht in der Dropdown-Liste ausgefüllt wird, können Sie diesen Wert manuell eingeben. Klicken Sie auf das Dropdown-Menü und wählen Sie **KLICKEN** aus.

>[!NOTE]
>
>Den Operatoren &quot;vorhanden&quot;und &quot;nicht vorhanden&quot;sind keine Feldwerte zugeordnet.

![Touchpoint-Dropdown](./images/user-guide/touchpoint_dropdown.png)

Mit den Schaltflächen *Ereignis hinzufügen* und *Gruppe hinzufügen* können Sie Ihren Touchpoint weiter definieren. Aufgrund der komplexen Natur rund um Touchpoints ist es nicht ungewöhnlich, mehrere Ereignisse und Gruppen für einen einzelnen Touchpoint zu haben.

Durch Klicken auf **Ereignis hinzufügen** können zusätzliche Felder hinzugefügt werden. Klicken Sie auf **x**, um ein hinzugefügtes Ereignis zu entfernen.

![Ereignis hinzufügen](./images/user-guide/touchpoint_add_event.png)

Wenn Sie auf **Gruppe hinzufügen** klicken, haben Sie die Möglichkeit, zusätzliche Felder separat vom Original zu erstellen. Durch Hinzufügen von Gruppen wird eine blaue *Und*-Schaltfläche angezeigt. Klicken Sie auf **Und** , um den Parameter zu ändern. Der neue Parameter &quot;Oder&quot;wird verwendet, um mehrere erfolgreiche Pfade zu definieren. Dieser bestimmte Touchpoint hat nur einen erfolgreichen Pfad, daher ist &quot;Oder&quot;nicht erforderlich.

![Touchpoint-Übersicht](./images/user-guide/add_group_touchpoint.png)

>[!NOTE]
>
>Verwenden Sie die Zeichenfolge unter *Touchpoint-Name* , um einen schnellen Überblick über Ihren Touchpoint zu erhalten. Beachten Sie, dass die Zeichenfolge mit dem Namen des Touchpoints übereinstimmt.

![](./images/user-guide/touchpoint_string.png)

Sie können zusätzliche Touchpoints hinzufügen, indem Sie auf **Touchpoint hinzufügen** klicken und den obigen Prozess wiederholen.

![Touchpoint hinzufügen](./images/user-guide/add_touchpoint.png)

Nachdem Sie alle erforderlichen Touchpoints definiert haben, scrollen Sie nach oben und klicken Sie in der oberen rechten Ecke auf **Weiter** , um mit dem letzten Schritt fortzufahren.

![finished](./images/user-guide/define_event_next.png)

## Erweiterte Trainings- und Scoring-Einrichtung

Die letzte Seite in Attribution AI ist die **[!UICONTROL Erweiterte]**-Seite, die zum Einrichten von Trainings- und Scoring-Tests verwendet wird.

![neue Seite erweitert](./images/user-guide/advanced_settings.png)

### Planen von Schulungen

Mit dem *Zeitplan* können Sie einen Tag und eine Uhrzeit der Woche auswählen, an der die Auswertung erfolgen soll.

Klicken Sie unter *Scoring-Häufigkeit* auf das Dropdown-Menü, um zwischen täglicher, wöchentlicher und monatlicher Auswertung auszuwählen. Wählen Sie als Nächstes die Wochentage aus, an denen die Auswertung erfolgen soll. Es können mehrere Tage ausgewählt werden. Klicken Sie ein zweites Mal auf einen Tag, um die Auswahl aufzuheben.

![Planen von Schulungen](./images/user-guide/schedule_training.png)

Klicken Sie auf das Uhrensymbol, um die Tageszeit zu ändern, zu der die Auswertung erfolgen soll. Geben Sie in der neuen Überlagerung, die angezeigt wird, die Tageszeit ein, zu der die Auswertung erfolgen soll. Klicken Sie außerhalb der Überlagerung, um sie zu schließen.

>[!NOTE]
>
>Es kann bis zu 24 Stunden dauern, bis jeder Scoring-Prozess abgeschlossen ist.

![Uhrensymbol](./images/user-guide/time_of_day.png)

### Zusätzliche Ergebnisdatensatzspalten (optional)

Standardmäßig wird für jede Dienstinstanz in einem Standardschema ein Bewertungsdatensatz erstellt. Sie können zusätzliche Spalten auf Grundlage Ihrer Konversionsereignis- und Touchpoint-Konfigurationen zur Ergebnisdatensatzausgabe hinzufügen. Wählen Sie zunächst Spalten aus Ihrem Eingabedatensatz aus und ziehen Sie sie per Drag-and-Drop, um die Reihenfolge zu ändern. Halten Sie dazu die linke Maustaste über dem Hamburger-Symbol gedrückt.

![Hinzufügung der Datensatzspalte](./images/user-guide/Add-score-dataset.png)

### Regionale Modellierung (optional) {#region-based-modeling-optional}

Das Verhalten Ihrer Kunden kann sich je nach Land und Region erheblich unterscheiden. Für globale Unternehmen kann die Verwendung länderbasierter oder regionenbasierter Modelle die Attributionsgenauigkeit erhöhen. Jede hinzugefügte Region erstellt ein neues Modell mit den Daten dieser Region.

Um einen neuen Bereich zu definieren, klicken Sie zunächst auf **[!UICONTROL Bereich hinzufügen]**. Geben Sie im angezeigten Container einen Namen für die Region ein. Nur ein Wert (&quot;placeContext.geo.countryCode&quot;) wird aus der Dropdown-Liste **[!UICONTROL Feldname eingeben]** ausgefüllt. Wählen Sie diesen Wert aus.

![Region auswählen unter](./images/user-guide/select_region_att.png)

Wählen Sie anschließend einen Operator aus.

![Regionsoperator](./images/user-guide/region_operators.png)

Geben Sie abschließend den Ländercode in das Dropdown-Menü **[!UICONTROL Feldwert eingeben]** ein.

>[!NOTE]
>
> Ländercodes sind zwei Zeichen lang. Eine vollständige Liste finden Sie hier: [ISO 3166-1 alpha-2](https://datahub.io/core/country-list).

![region](./images/user-guide/region-based.png)

### Schulungsfenster {#training-window}

Um sicherzustellen, dass Sie ein möglichst präzises Modell erhalten, müssen Sie Ihr Modell mit historischen Daten trainieren, die Ihr Unternehmen repräsentieren. Standardmäßig wird das Modell mit 2 Quartalen (6 Monate) der Konversionsereignisdaten trainiert. Wählen Sie das Dropdown-Menü aus, um die Standardeinstellung zu ändern. Sie können eine Schulung mit einem bis vier Quartalen der Daten (3-12 Monate) durchführen.

>[!NOTE]
>
>Ein kürzeres Trainings-Fenster reagiert empfindlicher auf aktuelle Trends, während ein längeres Trainings-Fenster ein robusteres Modell schafft und weniger empfindlich gegenüber aktuellen Trends ist.

![Trainingsfenster](./images/user-guide/training_window.png)

Nachdem Sie Ihr Schulungsfenster ausgewählt haben, klicken Sie in der oberen rechten Ecke auf **[!UICONTROL Beenden]** . Warten Sie etwas, bis die Daten verarbeitet werden. Nach Abschluss des Vorgangs wird ein Popup-Dialogfeld angezeigt, in dem bestätigt wird, dass die Instanzeinrichtung abgeschlossen ist. Klicken Sie auf **[!UICONTROL OK]** , um zur Seite **[!UICONTROL Dienstinstanzen]** umgeleitet zu werden, auf der Sie Ihre Dienstinstanz sehen können.

![Setup abgeschlossen](./images/user-guide/instance_setup_complete.png)

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich eine Dienstinstanz in Attribution AI erstellt. Sobald die Instanz die Auswertung abgeschlossen hat (bis zu 24 Stunden erlaubt), können Sie [Attribution AI Insights](./discover-insights.md) ermitteln. Wenn Sie Ihre Scoring-Ergebnisse herunterladen möchten, besuchen Sie außerdem die Dokumentation [Herunterladen von Bewertungen](./download-scores.md) .

## Weitere Ressourcen

Im folgenden Video wird ein durchgängiger Workflow zum Erstellen einer neuen Instanz in Attribution AI beschrieben.

>[!VIDEO](https://video.tv.adobe.com/v/32668?learn=on&quality=12)
