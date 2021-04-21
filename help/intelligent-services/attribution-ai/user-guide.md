---
keywords: Experience Platform;Benutzerhandbuch;Zuordnungs-Hilfe;beliebte Themen;Region
solution: Experience Platform, Intelligent Services
title: Attribution AI UI Guide
topic-legacy: User guide
description: Dieses Dokument dient als Leitfaden für die Interaktion mit Attribution AIS in der Benutzeroberfläche von Intelligent Services.
exl-id: 32e1dd07-31a8-41c4-88df-8893ff773f79
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1765'
ht-degree: 6%

---

# Handbuch zur Benutzeroberfläche von Attribution AI

Attribution AI als Teil von Intelligent Services ist ein algorithmischer Zuordnungsdienst mit mehreren Kanälen, der den Einfluss und die inkrementelle Auswirkung von Kundeninteraktionen auf bestimmte Ergebnisse berechnet. Mit Attribution AI können Marketing-Experten die Ausgaben für Marketing und Werbung messen und optimieren, indem sie die Auswirkungen einzelner Kundeninteraktionen in einzelnen Phasen der Customer Journey untersuchen.

Dieses Dokument dient als Leitfaden für die Interaktion mit Attribution AIS in der Benutzeroberfläche von Intelligent Services.

## Erstellen einer Instanz

Klicken Sie in der Benutzeroberfläche [!DNL Adobe Experience Platform] in der linken Navigation auf **[!UICONTROL Dienste]**. Der Browser **[!UICONTROL Dienste]** wird angezeigt und zeigt verfügbare intelligente Dienste für Adoben an. Klicken Sie im Container für Attribution AI auf **[!UICONTROL Öffnen]**.

![Zugreifen auf Ihre Instanz](./images/user-guide/open_Attribution_ai.png)

Die Seite des Attribution AI-Service wird angezeigt. Auf dieser Seite werden Dienstinstanzen von Attribution AI aufgelistet und Informationen zu diesen angezeigt, einschließlich des Namens der Instanz, der Konversionsereignisse, der Häufigkeit der Ausführung der Instanz und des Status der letzten Aktualisierung.

Sie finden die Metrik **[!UICONTROL Gesamte Ereignis für die Konversion, die]** bewertet wurde, unten rechts im Container **[!UICONTROL Instanz erstellen]**. Diese Metrik verfolgt die Gesamtanzahl der Konversionsdaten, die von Attribution AIS für das aktuelle Kalenderjahr bewertet wurden, einschließlich aller Sandbox-Umgebung und aller gelöschten Dienstinstanzen.

![](./images/user-guide/total_conversions.png)

Dienstinstanzen können mithilfe der Steuerelemente auf der rechten Seite der Benutzeroberfläche bearbeitet, geklont und gelöscht werden. Um diese Steuerelemente anzuzeigen, wählen Sie eine Instanz aus den vorhandenen **[!UICONTROL Dienstinstanzen]** aus. Die Steuerelemente enthalten die folgenden Informationen:

- **[!UICONTROL Bearbeiten]**: Durch Auswahl von  **** Bearbeiten können Sie eine vorhandene Dienstinstanz ändern. Sie können den Namen, die Beschreibung, den Status und die Bewertungsfrequenz der Instanz bearbeiten.
- **[!UICONTROL Klonen]**: Durch Auswahl von  **** Clonecopies wird die ausgewählte Dienstinstanz kopiert. Anschließend können Sie den Workflow ändern, um kleinere Änderungen vorzunehmen und ihn als neue Instanz umzubenennen.
- **[!UICONTROL Löschen]**: Sie können eine Dienstinstanz einschließlich aller historischen Ausführung löschen.
- **[!UICONTROL Datenquelle]**: Ein Link zum Datensatz, der von dieser Instanz verwendet wird.
- **[!UICONTROL Details]** der letzten Ausführung: Dies wird nur angezeigt, wenn eine Ausführung fehlschlägt. Informationen darüber, warum die Ausführung fehlgeschlagen ist, wie Fehlercodes werden hier angezeigt.

![](./images/user-guide/side_panel.png)

- **[!UICONTROL Konversions-Ereignis]**: Eine schnelle Übersicht über die für diese Instanz konfigurierten Konvertierungs-Ereignis.
- **[!UICONTROL Lookback-Fenster]**: Der von Ihnen definierte Zeitraum, der angibt, wie viele Tage vor dem Konversions-Ereignis-Touchpoints eingeschlossen werden.
- **[!UICONTROL Touchpoints]**: Eine Liste aller Touchpoints, die Sie beim Erstellen dieser Instanz definiert haben.

![](./images/user-guide/side_panel_2.png)

Wählen Sie **[!UICONTROL Instanz erstellen]**, um zu beginnen.

![Instanz erstellen](./images/user-guide/landing_page.png)

Als Nächstes wird die Setup-Seite für Attribution AI angezeigt, auf der Sie grundlegende Informationen bereitstellen und ein Datensatz für die Instanz angeben können.

![Setup-Seite](./images/user-guide/setup_attribution.png)

### Benennen der Instanz

Geben Sie unter **[!UICONTROL Grundlegende Informationen]** einen Namen und eine optionale Beschreibung für Ihre Dienstinstanz ein.

![Benennen einer Instanz](./images/user-guide/naming_instance.png)

### Datensatz auswählen

Nachdem Sie die grundlegenden Informationen ausgefüllt haben, klicken Sie auf das Dropdown-Menü **Datensatz auswählen**, um Ihren Datensatz auszuwählen. Der Datensatz wird verwendet, um das Modell zu trainieren und die nachfolgenden Daten zu bewerten, die es erzeugt. Wenn Sie einen Datensatz aus der Dropdown-Auswahl auswählen, werden nur die Datensätze aufgelistet, die mit Attribution AI kompatibel sind und dem XDM-Schema (Experience Data Model) entsprechen. Klicken Sie nach Auswahl eines Datensatzes auf **Weiter** oben rechts, um mit der Seite &quot;Ereignis definieren&quot;fortzufahren.

>[!TIP]
>
>Adobe Analytics-Datensätze werden über den Analytics-Source-Connector unterstützt.

![Setup-Seite](./images/user-guide/dataset_selector.png)

## Definieren von Ereignissen

Es gibt drei verschiedene Arten von Eingabedaten, die zur Definition von Ereignissen verwendet werden:

- **Umrechnungsziele:** Geschäftsziele, die die Auswirkungen von Marketing-Aktivitäten wie E-Commerce-Bestellungen, Einkäufe im Geschäft und Website-Besuche identifizieren.
- **Lookback-Fenster:** Stellt einen Zeitraum bereit, der angibt, wie viele Tage vor dem Konversions-Ereignis-Touchpoints eingeschlossen werden sollen.
- **Touchpoints: Marketing-Ereignis auf** Empfänger-, Einzel- und oder Cookie-Ebene, die zur Bewertung der numerischen oder umsatzbasierten Auswirkungen von Konversionen verwendet werden.

### Definieren von Konversions-Ereignissen {#define-conversion-events}

Um ein Konversions-Ereignis zu definieren, müssen Sie dem Ereignis einen Namen geben und den Ereignistyp auswählen, indem Sie auf das Dropdown-Menü **Feldname eingeben** klicken.

![yes dropdown](./images/user-guide/conversion_event_2.png)

Nach Auswahl eines Ereignisses wird rechts ein neues Dropdown-Feld angezeigt. Die zweite Dropdownliste dient dazu, durch die Verwendung von Vorgängen weiteren Kontext für Ihr Ereignis zu schaffen. Für dieses Konvertierungs-Ereignis wird der Standardvorgang *exists* verwendet.

>[!NOTE]
>
>Eine Zeichenfolge unter dem Umrechnungsnamen *wird aktualisiert, wenn Sie Ihr Ereignis definieren.*

![no dropdown](./images/user-guide/conversion_event_1.png)

Die Schaltflächen **[!UICONTROL Hinzufügen Ereignis]** und **[!UICONTROL Hinzufügen Gruppe]** werden verwendet, um Ihre Konvertierung weiter zu definieren. Je nach der von Ihnen definierten Konversion müssen Sie möglicherweise die Schaltflächen **[!UICONTROL Hinzufügen Ereignis]** und **[!UICONTROL Hinzufügen Gruppe]** verwenden, um weitere Kontexte bereitzustellen.

![Ereignis hinzufügen](./images/user-guide/add_event.png)

Durch Klicken auf **[!UICONTROL Hinzufügen Ereignis]** werden weitere Felder erstellt, die nach der oben beschriebenen Methode ausgefüllt werden können. Hierdurch wird der Zeichenfolgendefinition unter dem Konvertierungsnamen eine AND-Anweisung hinzugefügt. Klicken Sie auf **x**, um ein hinzugefügtes Ereignis zu entfernen.

![Menü &quot;Ereignis hinzufügen&quot;](./images/user-guide/add_event_result.png)

Wenn Sie auf **[!UICONTROL Hinzufügen Gruppe]** klicken, können Sie zusätzliche Felder getrennt vom Original erstellen. Nach dem Hinzufügen von Gruppen wird eine blaue Schaltfläche *und* angezeigt. Wenn Sie auf **und** klicken, können Sie den Parameter so ändern, dass er &quot;Oder&quot;enthält. &quot;Oder&quot;wird verwendet, um mehrere erfolgreiche Konvertierungspfade zu definieren. &quot;Und&quot;erweitert den Konvertierungspfad um zusätzliche Bedingungen.

![und](./images/user-guide/and_or.png)

Wenn Sie mehr als eine Konvertierung benötigen, klicken Sie auf **Hinzufügen Konvertierung**, um eine neue Konvertierungskarte zu erstellen. Sie können den obigen Prozess wiederholen, um mehrere Konvertierungen zu definieren.

![Konvertierung hinzufügen](./images/user-guide/add_conversion.png)

### Lookback-Fenster {#lookback-window} definieren

Nachdem Sie Ihre Konvertierung definiert haben, müssen Sie Ihr Lookback-Fenster bestätigen. Geben Sie mithilfe der Pfeiltasten oder durch Klicken auf den Standardwert (56) an, wie viele Tage vor dem Konversions-Ereignis Touchpoints eingefügt werden sollen. Touchpoints werden im nächsten Schritt definiert.

![lookback](./images/user-guide/lookback_window.png)

### Definieren von Touchpoints

Das Definieren von Touchpoints erfolgt nach einem ähnlichen Arbeitsablauf wie [das Definieren von Konversionen](#define-conversion-events). Zuerst müssen Sie Ihren Touchpoint benennen und im Dropdown-Menü *Feldname eingeben* einen Touchpoint-Wert auswählen. Nach der Auswahl wird das Dropdown-Feld &quot;Operator&quot;mit dem Standardwert &quot;exists&quot;angezeigt. Klicken Sie auf das Dropdownmenü, um eine Liste der Operatoren anzuzeigen.

![Operatoren](./images/user-guide/operators.png)

Wählen Sie für diesen Touchpoint **gleich**.

![Schritt 1](./images/user-guide/touchpoint_step1.png)

Sobald ein Operator für einen Touchpoint ausgewählt ist, wird *Feldwert eingeben* verfügbar gemacht. Die Dropdown-Werte für *Feldwert eingeben* werden basierend auf dem zuvor ausgewählten Operator- und Touchpoint-Wert gefüllt. Wenn ein Wert nicht in der Dropdown-Liste enthalten ist, können Sie diesen Wert manuell eingeben. Klicken Sie auf das Dropdown-Menü und wählen Sie **KLICKEN**.

>[!NOTE]
>
>Den Operatoren &quot;exists&quot;und &quot;not exists&quot;sind keine Feldwerte zugeordnet.

![Touchpoint-Dropdown](./images/user-guide/touchpoint_dropdown.png)

Mit den Schaltflächen *Hinzufügen Ereignis* und *Hinzufügen Gruppe* können Sie Ihren Touchpoint weiter definieren. Aufgrund der komplexen Natur rund um Touchpoints ist es nicht ungewöhnlich, mehrere Ereignis und Gruppen für einen einzigen Touchpoint zu haben.

Durch Klicken auf **Hinzufügen Ereignis** können weitere Felder hinzugefügt werden. Klicken Sie auf **x**, um ein hinzugefügtes Ereignis zu entfernen.

![Ereignis hinzufügen](./images/user-guide/touchpoint_add_event.png)

Wenn Sie auf **Hinzufügen Gruppe** klicken, können Sie zusätzliche Felder getrennt vom Original erstellen. Nach dem Hinzufügen von Gruppen wird eine blaue Schaltfläche *und* angezeigt. Klicken Sie auf **Und**, um den Parameter zu ändern, wird der neue Parameter &quot;Oder&quot;verwendet, um mehrere erfolgreiche Pfade zu definieren. Dieser Touchpoint hat nur einen erfolgreichen Pfad, daher ist &quot;Oder&quot;nicht erforderlich.

![Touchpoint-Übersicht](./images/user-guide/add_group_touchpoint.png)

>[!NOTE]
>
>Verwenden Sie die Zeichenfolge unter *Touchpoint-Name*, um einen schnellen Überblick über Ihren Touchpoint zu erhalten. Beachten Sie, dass die Zeichenfolge mit dem Namen des Touchpoints übereinstimmt.

![](./images/user-guide/touchpoint_string.png)

Sie können weitere Touchpoints hinzufügen, indem Sie auf **Hinzufügen Touchpoint** klicken und den obigen Vorgang wiederholen.

![Touchpoint hinzufügen](./images/user-guide/add_touchpoint.png)

Nachdem Sie alle erforderlichen Touchpoints definiert haben, scrollen Sie nach oben und klicken Sie auf **Weiter** in der oberen rechten Ecke, um mit dem letzten Schritt fortzufahren.

![fertig definieren](./images/user-guide/define_event_next.png)

## Erweiterte Schulungs- und Bewertungseinstellungen

Die letzte Seite in Attribution AI ist die Seite **[!UICONTROL Erweitert]**, die zum Einrichten der Schulung und Bewertung verwendet wird.

![neue Seite erweitert](./images/user-guide/advanced_settings.png)

### Schulung planen

Mithilfe von *Plan* können Sie einen Wochentag und eine Uhrzeit für die Bewertung auswählen.

Klicken Sie auf das Dropdownfeld unter *Bewertungshäufigkeit*, um zwischen Tages-, Wochen- und Monatsbewertungen auszuwählen. Wählen Sie anschließend die Wochentage aus, an denen die Bewertung erfolgen soll. Es können mehrere Tage ausgewählt werden. Klicken Sie ein zweites Mal auf einen Tag, um die Auswahl aufzuheben.

![Schulung planen](./images/user-guide/schedule_training.png)

Klicken Sie auf das Uhrensymbol, um die Uhrzeit zu ändern, zu der die Bewertung erfolgen soll. Geben Sie in der neuen Überlagerung, die angezeigt wird, die Uhrzeit ein, zu der die Bewertung erfolgen soll. Klicken Sie auf eine Stelle außerhalb der Überlagerung, um sie zu schließen.

>[!NOTE]
>
>Es kann bis zu 24 Stunden dauern, bis jeder Bewertungsvorgang abgeschlossen ist.

![Uhrensymbol](./images/user-guide/time_of_day.png)

### Spalten mit zusätzlichen Ergebnisdatensätzen (optional)

Standardmäßig wird für jede Dienstinstanz in einem Standard-Schema ein Ergebnisdatensatz erstellt. Sie können je nach Konversions- und Touchpoint-Konfigurationen weitere Spalten zur Ergebnisdatenaset-Ausgabe hinzufügen. Beginn, indem Sie Spalten aus Ihrem Eingabedataset auswählen, können Sie sie per Drag &amp; Drop verschieben, um die Reihenfolge zu ändern, indem Sie die linke Maustaste über dem Hamburger-Symbol gedrückt halten.

![Zusatz zur Bewertungsdatasäule](./images/user-guide/Add-score-dataset.png)

### Regionale Modellierung (optional) {#region-based-modeling-optional}

Das Verhalten Ihrer Kunden kann sich je nach Land und Region erheblich unterscheiden. Für globale Unternehmen kann die Verwendung von länderbasierten oder regionsbasierten Modellen die Genauigkeit der Zuordnung erhöhen. Jede hinzugefügte Region erstellt ein neues Modell mit den Daten dieser Region.

Um einen neuen Bereich zu definieren, klicken Sie auf **[!UICONTROL Hinzufügen Region]**. Geben Sie in dem angezeigten Container einen Namen für die Region ein. Nur ein Wert (&quot;placeContext.geo.countryCode&quot;) wird aus der Dropdownliste **[!UICONTROL Feldname eingeben]** ausgefüllt. Wählen Sie diesen Wert aus.

![Region auswählen unter](./images/user-guide/select_region_att.png)

Wählen Sie als Nächstes einen Operator aus.

![Regionsoperator](./images/user-guide/region_operators.png)

Geben Sie abschließend den Ländercode in das Dropdown-Feld **[!UICONTROL Feldwert eingeben]** ein.

>[!NOTE]
>
> Ländercodes sind zwei Zeichen lang. Eine vollständige Liste finden Sie hier: [ISO 3166-1 alpha-2](https://datahub.io/core/country-list).

![region](./images/user-guide/region-based.png)

### Schulungsfenster {#training-window}

Um sicherzustellen, dass Sie das bestmögliche Modell erhalten, ist es wichtig, Ihr Modell mit historischen Daten auszubilden, die Ihr Geschäft repräsentieren. Standardmäßig wird das Ereignis mit 2 Quartalen (6 Monate) Konversionsdaten trainiert. Wählen Sie das Dropdown-Menü aus, um die Standardeinstellung zu ändern. Sie können zwischen einem und vier Quartalen der Daten (3-12 Monate) trainieren.

>[!NOTE]
>
>Ein kürzeres Schulungsfenster ist anfälliger für aktuelle Trends, während ein längeres Schulungsfenster ein robusteres Modell schafft und weniger anfällig für aktuelle Trends ist.

![Schulungsfenster](./images/user-guide/training_window.png)

Klicken Sie nach Auswahl des Schulungsfensters in der oberen rechten Ecke auf **[!UICONTROL Fertig stellen]**. Warten Sie einige Zeit, bis die Daten verarbeitet werden. Nach Abschluss des Vorgangs wird ein Popup-Dialogfeld angezeigt, in dem bestätigt wird, dass die Instanzeinrichtung abgeschlossen ist. Klicken Sie auf **[!UICONTROL OK]**, um zur Seite **[!UICONTROL Dienstinstanzen]** umgeleitet zu werden, auf der Sie Ihre Dienstinstanz sehen können.

![setup complete](./images/user-guide/instance_setup_complete.png)

## Nächste Schritte

Durch Befolgen dieser Übung haben Sie erfolgreich eine Dienstinstanz in Attribution AI erstellt. Sobald die Instanz ihre Bewertung abgeschlossen hat (bis zu 24 Stunden), können Sie [Einblicke in Attribution AI](./discover-insights.md) entdecken. Wenn Sie Ihre Ergebnisse herunterladen möchten, lesen Sie außerdem die Dokumentation [Download-Ergebnisse](./download-scores.md).

## Zusätzliche Ressourcen

Im folgenden Video wird ein durchgängiger Arbeitsablauf zum Erstellen einer neuen Instanz in Attribution AI beschrieben.

>[!VIDEO](https://video.tv.adobe.com/v/32668?learn=on&quality=12)
