---
title: Einverständnisanalyse und -verfolgung
description: Erfahren Sie, wie Sie ein Dashboard zur Einverständnisanalyse erstellen, um zu verfolgen, wie sich das Einverständnis der Benutzer im Laufe der Zeit entwickelt hat.
exl-id: 34accae5-8b4f-4281-8333-187a91db8199
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1910'
ht-degree: 0%

---

# Einverständnisanalyse und -verfolgung

In der heutigen Marketing-Landschaft müssen Sie die Voreinstellungen für das Kundeneinverständnis verstehen und respektieren. Adobe Real-Time Customer Data Platform bietet Marketing-Experten die Möglichkeit, das Einverständnis der Kunden zu analysieren, um Vertrauen aufzubauen, Datenschutzbestimmungen einzuhalten und personalisierte Erlebnisse bereitzustellen.

In diesem Dokument wird beschrieben, wie Sie ein Einverständnis-Dashboard für verschiedene Marketing-Anwendungsfälle für Real-Time CDP-Daten erstellen. Insbesondere wird beschrieben, wie Sie eine Zielgruppe mit den entsprechenden Attributen für Ihre Geschäftsanforderungen erstellen und diese Einblicke dann mithilfe vorkonfigurierter Widgets in der Adobe Experience Platform-Benutzeroberfläche nutzen können. Eine alternative Methode zum Erstellen eines eigenen benutzerdefinierten Widgets mit der benutzerdefinierten Dashboards-Funktion wird ebenfalls vorgestellt.

## Anwendungsszenarien {#use-cases}

Die in diesem Handbuch behandelten Anwendungsfälle sind Einverständnistrends und Einverständnisüberschneidungen.

- **Einverständnis-Trend** verfolgt, wie sich das Einverständnis der Benutzer im Laufe der Zeit entwickelt hat. Die Analyse der Änderungen der Einverständnisvoreinstellungen hilft Marketing-Experten, Kampagnen zu planen und auszuführen, die sich an diese Änderungen der Benutzervoreinstellungen anpassen. Sie können beispielsweise gezielte Aufklärungskampagnen, Transparenz- und Vertrauenskampagnen oder Anreizkampagnen durchführen, um die Einwilligungsentscheidung zu fördern. Sie können auch Kampagnen korrelieren, die sich negativ auf das Einverständnis ausgewirkt haben könnten, um die Häufigkeit dieser Kampagnen proaktiv zu reduzieren.
- **Einverständnisüberschneidung** verwendet die Überschneidung zwischen Einverständniskanälen, um konsistentes personalisiertes Messaging auf mehreren Kanälen für Ihre Kundinnen und Kunden bereitzustellen, die mehreren Kanälen zugestimmt haben. Marketing-Experten können Ressourcen priorisieren und bestimmten Kanälen zuweisen, in denen ein höheres Maß an Einverständnis und personalisiertes Messaging bei Kunden Anklang finden und höhere Reaktionsraten erzeugen kann.

## Erstellen von einverstandenen Zielgruppen {#create-consent-audiences}

Um ein Einverständnis-Dashboard zu erstellen, müssen Sie zunächst eine Zielgruppe aus allen Profilen erstellen, die dem Kontakt zugestimmt haben. Um zum Segment Builder von Real-Time Customer Data Platform zu navigieren, wählen Sie **[!UICONTROL Zielgruppen]** im linken Navigationsbereich der Experience Platform-Benutzeroberfläche aus. Wählen Sie auf der [!UICONTROL Kunde] Registerkarte des [!UICONTROL Zielgruppen]-Dashboards oben rechts **der Ansicht** Zielgruppe erstellen und dann **[!UICONTROL Regeln erstellen]**.

![Das [!UICONTROL Zielgruppen]-Dashboard mit [!UICONTROL Kunde], [!UICONTROL Zielgruppen] und [!UICONTROL Segment erstellen] hervorgehoben.](../images/insights-use-cases/consent-analysis/create-audience.png)

Der Segment Builder wird angezeigt. Wählen Sie als Nächstes **[!UICONTROL XDM Individual Profile]** aus den verfügbaren Optionen aus. Weitere Informationen zur Arbeitsfläche des Regel[Builders finden Sie in der ](../../segmentation/ui/segment-builder.md#rule-builder-canvas).

![Der Segment Builder mit dem hervorgehobenen [!UICONTROL XDM Individual Profile]-Attributordner.](../images/insights-use-cases/consent-analysis/xdm-individual-profile.png)

Suchen Sie Ihre Einverständnisattribute in den verfügbaren Optionen. Wählen Sie **[!UICONTROL Einverständnis und Voreinstellungen]** aus.

>[!NOTE]
>
>Wenn Sie Ihr Benutzereinverständnis in einem Attribut beibehalten haben, das sich von dem der von Adobe empfohlenen Feldergruppe unterscheidet, müssen Sie diese Attribute anstelle der unten aufgeführten auswählen.

Weitere Informationen finden Sie in der Dokumentation [Handhabung des Einverständnisses in der Segmentierung](../../segmentation/tutorials/consents.md#handling-consent-in-segmentation) .

![Der Segment Builder mit dem hervorgehobenen [!UICONTROL Einverständnis und Voreinstellungen] -Attributordner.](../images/insights-use-cases/consent-analysis/consent-and-preferences.png)

Die verschiedenen Einverständnis- und Voreinstellungsoptionen werden angezeigt. Da sich diese Demonstration auf das Einverständnis zum Kontakt über verschiedene Marketing-Kanäle konzentriert, wählen Sie **[!UICONTROL Marketing-Voreinstellungen]**.

![Der Segment Builder mit dem hervorgehobenen [!UICONTROL Marketing]Voreinstellungen“](../images/insights-use-cases/consent-analysis/marketing-preferences.png)

Die Liste der Marketing-Voreinstellungen wird angezeigt. Obwohl sich dieses Anwendungsbeispiel auf E-Mail, SMS und Anrufe konzentriert, können Sie Einblicke für jede andere Kombination oder die Gesamtheit der Optionen erstellen. Führen Sie für jeden Kanal die folgenden Schritte aus, um eine Zielgruppe zu erstellen.

Um mit der Konfiguration einer Zielgruppe zu beginnen, wählen **[!UICONTROL SMS empfangen]** / **[!UICONTROL E-Mail empfangen]** / **[!UICONTROL Anrufe empfangen]**.

![Die verfügbaren Kontaktkanäle für das Marketing sind in Audience Builder hervorgehoben.](../images/insights-use-cases/consent-analysis/channels.png)

Der [!UICONTROL Abonnements]-Ordner wird angezeigt. Wählen Sie aus den verfügbaren Optionen das Attribut **[!UICONTROL Auswahlwert]** aus und ziehen Sie es in den mittleren Bereich. Wählen Sie dann den gewünschten Wert aus der Dropdown-Liste aus. Wählen Sie in diesem Fall **Ja (Opt-in)**. Benennen Sie anschließend die Zielgruppe entsprechend Ihren Geschäftsanforderungen und geben Sie eine benutzerfreundliche Beschreibung an.

>[!NOTE]
>
>Es gibt eine weiche Begrenzung für die Anzahl der Zielgruppen, die Sie erstellen sollten. Weitere Informationen finden Sie in der Dokumentation zu [Segmentierungsleitplanken](../../profile/guardrails.md#segmentation-guardrails).

![Das Attribut [!UICONTROL Auswahlwert] mit dem hervorgehobenen Wert [!UICONTROL Ja (Opt-in)] in Segment Builder. Der Name und die Beschreibung der Zielgruppe sind ebenfalls hervorgehoben.](../images/insights-use-cases/consent-analysis/choice-value.png)

Nachdem Sie die erforderlichen Zielgruppen erstellt haben, werden sie auf der Registerkarte [!UICONTROL Zielgruppen] [!UICONTROL Durchsuchen] aufgeführt.

>[!NOTE]
>
>Beim Erstellen einer Zielgruppe müssen Sie warten, bis der Batch-Segmentierungsvorgang abgeschlossen ist, bevor die Daten verfügbar sind, um mit der Erstellung Ihres Einverständnis-Dashboards zu beginnen. Die Batch-Segmentierung beschreibt den Prozess des gleichzeitigen Verschiebens aller Profildaten durch Ihre Segmentdefinitionen, um die entsprechenden Zielgruppen zu erstellen. Nach der Erstellung wird diese Zielgruppe gespeichert, sodass Sie sie exportieren und verwenden können. Batch-Segmente werden automatisch alle 24 Stunden ausgewertet.

## Insights nutzen {#consume-insights}

Adobe hat verschiedene Einblicke erstellt, die automatisch für Sie in den Dashboards „Profile“, „Zielgruppen“ und „Ziele“ verfügbar sind. Jede Zielgruppe, die Sie erstellen, kann dann automatisch mit diesen vorkonfigurierten Einblicken verwendet werden. In der Dokumentation zu Standard-Widgets finden Sie eine Liste der Einblicke, die in den Dashboards [Profile](../guides/profiles.md#standard-widgets), [Zielgruppen](../guides/audiences.md#standard-widgets) und [Ziele](../guides/destinations.md) verfügbar sind.

## Zielgruppenüberschneidung {#audience-overlap}

Um die Überschneidung zwischen zwei Einverständnis-Zielgruppen zu überprüfen, fügen Sie [!UICONTROL Zielgruppenüberschneidung nach Zusammenführungsrichtlinie“ zu &#x200B;] Profile-Dashboard hinzu und wählen Sie die gewünschten Zielgruppen in den Dropdown-Menüs aus. Weitere Informationen zur insight finden Sie in der Dokumentation zu Anweisungen zum Hinzufügen eines Widgets zu Ihrem Dashboard [*Zielgruppenüberschneidung nach Zusammenführungsrichtlinie*](../guides/profiles.md#audience-overlap-by-merge-policy) .

<!-- Image needs updating to night mode -->

![Das Profile-Dashboard mit dem hervorgehobenen Widget „Zielgruppenüberschneidung nach Zusammenführungsrichtlinie“. Das Widget visualisiert Überschneidungen zwischen zwei Zustimmungs-Zielgruppen.](../images/insights-use-cases/consent-analysis/audience-overlap-by-merge-policy.png)

Mit dem Bericht zur Zielgruppenüberschneidung im Zielgruppen-Dashboard können Sie die Überschneidung aller Zielgruppen anzeigen, bei denen Benutzende dem Empfang von Anrufen über alle anderen Zielgruppen hinweg zugestimmt haben. Um die Überschneidung von Zustimmungs-Zielgruppen anzuzeigen, gehen Sie zunächst zur Registerkarte [!UICONTROL Zielgruppen] [!UICONTROL Übersicht]. Von dort aus können Sie das Widget [!UICONTROL Bericht Zielgruppenüberschneidung] zum Zielgruppen-Dashboard hinzufügen. Nachdem das Widget erstellt wurde, wählen Sie die Zielgruppe **[!UICONTROL Benutzer hat Anrufen zugestimmt]** aus dem Dropdown-Menü Übersicht der Zielgruppe oben auf der Seite aus. Wählen Sie als **[!UICONTROL im Widget Bericht Zielgruppenüberschneidung die Option]** Mehr anzeigen“ aus, um bis zu 50 der oberen Überschneidungen und bis zu 50 der geringsten Überschneidungen im Hinblick auf das ausgewählte Segment anzuzeigen.

<!-- Image needs updating to night mode -->

![Das Zielgruppen-Dashboard mit dem Widget „Bericht Zielgruppenüberschneidung“ wird angezeigt. Der Benutzer hat Anrufen von Audience als Vergleichs-Audience zugestimmt und der Link Mehr anzeigen ist beide hervorgehoben.](../images/insights-use-cases/consent-analysis/audience-overlap-report-user-consent-to-calls.png)

Das Dialogfeld Bericht Zielgruppenüberschneidung wird erweitert, um zusätzliche Daten zur Zielgruppenüberschneidung anzuzeigen.

<!-- Image needs updating to night mode -->

![Der Bericht zur Zielgruppenüberschneidung mit hervorgehobener Option „Einverständniserklärungen der Benutzer zur E-Mail-Zielgruppe“.](../images/insights-use-cases/consent-analysis/additional-audience-overlap-reports.png)

## Zielgruppengrößen-Trends {#audience-size-trends}

Wenn Sie eine auf Einverständnis basierende Zielgruppe erstellen, wird sie automatisch bis zu 12 Monate nach dem Datum der Erstellung der Zielgruppe trendweise angezeigt. Um einen voll funktionsfähigen Trend für Ihr Kundeneinverständnis zu erhalten, fügen Sie die folgenden Widgets zur Seite [!UICONTROL Segmente] [!UICONTROL Übersicht] hinzu. Diese Einblicke bieten eine leistungsstarke Möglichkeit zu verfolgen, wie sich Ihr Einverständnis im Laufe der Zeit verändert. Sie korrelieren sogar mit allen Kampagnen, die Sie parallel ausführen und die das Einverständnis positiv oder negativ beeinflussen können. Die für diese Widgets angebotenen Beschreibungen gelten für einen Anwendungsfall mit Einverständnis.

- [Trend der Zielgruppengröße](../guides/audiences.md#audience-size-trend): Dieses Widget bietet eine Möglichkeit, zu verfolgen, wie sich Ihr jeweiliges Einverständnis im Laufe der Zeit verändert hat.
- [Entwicklung der Zielgruppengröße](../guides/audiences.md#audience-size-change-trend): Dieses Widget verfolgt, wie sich das Einverständnis Ihrer Kunden täglich geändert hat. Wenn beispielsweise die Anzahl Ihrer Kundenzustimmung um 100.000 gesunken ist, können Sie sehen, wie diese Änderung täglich erfolgte.
- [Entwicklung der Zielgruppengröße nach Identität](../guides/audiences.md#audience-size-trend-by-identity): Mit diesem Widget können Sie verfolgen, wie sich Ihr jeweiliges Einverständnis im Laufe der Zeit verändert hat, aber weiter nach einer bestimmten Identität wie einer E-Mail gefiltert werden.

<!-- Image needs updating to night mode -->

![Das Zielgruppen-Dashboard mit dem Widget „Entwicklung der Zielgruppengröße“, „Entwicklung der Zielgruppengröße nach Identität“ und „Entwicklung der Zielgruppengröße“ wird angezeigt. Die Benutzenden, die der E-Mail-Zielgruppe zugestimmt haben, sind hervorgehoben.](../images/insights-use-cases/consent-analysis/three-audience-trend-widgets.png)

## Dashboard für Zielgruppenübersicht {#audiences-overview-dashboard}

Nachdem Sie eine einverständnisbezogene Zielgruppe erstellt haben, z. B. „Einverständnisbenutzer zu SMS“, können Sie wichtige personalisierte Einverständnisinformationen zu Ihrer Zielgruppe anzeigen, indem Sie die entsprechenden Widgets zu Ihrem Zielgruppen-Übersichts-Dashboard hinzufügen. Navigieren Sie zu [!UICONTROL Zielgruppen] [!UICONTROL Übersicht] und fügen Sie Ihre ausgewählten Widgets aus der Widget-Bibliothek hinzu. Jedes Widget, das zu Ihrer Ansicht des Dashboards hinzugefügt wird, kann mit der Funktion [!UICONTROL Dashboard ändern“ in der Größe angepasst &#x200B;] verschoben werden. Ihre personalisierte Ansicht kann Einblicke enthalten, z. B. den Trend im Zeitverlauf (bis zu 12 Monate), die Überschneidungen mit anderen Zielgruppen und die Identitätszusammensetzung der Zielgruppe. Nachfolgend finden Sie eine Beispielansicht.

![Das Zielgruppen-Dashboard mit Hervorhebung der Benutzer, die in die SMS-Zielgruppe eingewilligt haben , im Dropdown-Menü „Globale Zielgruppe“.](../images/insights-use-cases/consent-analysis/audience-dashboard-user-consent-to-sms.png)

## Benutzerdefinierte Dashboards {#usr-defined-dashboards}

Sie können auch eigene Widgets mit benutzerdefinierten Dashboards erstellen. Wenn Sie Ihr eigenes Widget erstellen, haben Sie die vollständige Kontrolle über den Typ des Widgets sowie die Möglichkeit, Filter und vieles mehr direkt in Adobe Real-Time CDP hinzuzufügen.

Beispiel: Sie möchten mehrere Einverständnis-Zielgruppen im selben Diagramm im Trend anzeigen, sodass Sie im Laufe der Zeit sehen können, wie sich Ihre Einverständnisvoreinstellungen geändert haben. Diese Art der Visualisierung ist mit benutzerdefinierten Dashboards in minimalen Schritten und einer einmaligen Einrichtung möglich. Wählen Sie zunächst **[!UICONTROL Dashboards]** im linken Navigationsbereich aus. Der [!UICONTROL Dashboards]-Arbeitsbereich wird angezeigt. Wählen Sie dann **[!UICONTROL Dashboard erstellen]** aus. Vollständige Anweisungen zum [ (Erstellen eines Dashboards und eines benutzerdefinierten ](../standard-dashboards.md)) finden Sie im Handbuch zu benutzerdefinierten Dashboards .

![Der Arbeitsbereich „Dashboards“ mit hervorgehobenen Optionen „Dashboards“ und „Dashboard erstellen“.](../images/standard-dashboards/create-dashboard.png)

Wenn Sie [Ihr Datenmodell auswählen](../standard-dashboards.md#select-data-model) wählen Sie im Widget-Composer `CDPInsights` und dann **[!UICONTROL Weiter]** aus. Das [!UICONTROL Tabelle auswählen] wird angezeigt.

![Das Dialogfeld „Datenmodell auswählen“ mit hervorgehobenem CDPInsights-Modell.](../images/standard-dashboards/select-data-model-dialog.png)

Die nächste Ansicht zeigt eine Liste der verfügbaren Tabellen in der linken Leiste an. Wählen Sie die `adwh_fact_profile_by_segment_and_namespace_trendlines`.

![Das Dialogfeld „Tabelle auswählen“ mit hervorgehobener Tabelle „adwh_fact_profile_by_segment_and_namespace_trendlines“.](../images/insights-use-cases/consent-analysis/select-table.png)

Nachdem der Widget-Composer mit Daten aus der ausgewählten Tabelle gefüllt wurde, führen Sie die folgenden Schritte aus:

- [Suchen Sie [!UICONTROL Attribute]](../standard-dashboards.md#add-filter-attributes) nach `[!UICONTROL date]` und fügen Sie dann über das Symbol + der X-Achse das `[!UICONTROL date]` Attribut aus dem Dropdown-Menü hinzu.
  ![Der Widget-Composer mit dem hervorgehobenen Add-on-Symbol und dem hervorgehobenen Dropdown-Menü.](../images/standard-dashboards/attributes-dropdown.png)
- Suchen Sie [!UICONTROL Attribute] nach `[!UICONTROL count_of_profiles]` und verwenden Sie dann das Symbol + , um der Y-Achse aus dem Dropdown-Menü das Attribut `[!UICONTROL count_of_profiles]` hinzuzufügen.
- Wählen Sie das Symbol `...` (Ellipsen) im Feld [!UICONTROL Y-Achse] und dann die Aggregatfunktion [!UICONTROL SUMME] aus dem Dropdown-Menü aus.
  ![Das Widget „Einverständnistrends des Widget-Composers“ mit Hervorhebung des Datenmodells, der Tabelle und des Dropdown-Menüs der Y-Achse und der Summenfunktion. ](../images/insights-use-cases/consent-analysis/y-axis-sum-function.png)
- Wählen Sie [!UICONTROL &#x200B; Dropdown]Menü „Markierungen“ aus und ändern Sie den Diagrammtyp in [!UICONTROL Linie].
- Suchen Sie [!UICONTROL Attribute] nach dem `[!UICONTROL segment_name]` und verwenden Sie dann das Symbol + , um die `segment_name` als [!UICONTROL Filter] aus dem Dropdown-Menü hinzuzufügen. Das [!UICONTROL Filter: Segment_name] wird angezeigt. Wählen Sie die zuvor erstellten Zielgruppen aus, die sich auf das Einverständnis beziehen. Wählen Sie für dieses Beispiel **[!UICONTROL Benutzer, die Anrufen zugestimmt haben]**, **[!UICONTROL Benutzer, die zu]** zugestimmt haben und **[!UICONTROL Benutzer, die zu E-Mails zugestimmt haben]** aus, gefolgt von **[!UICONTROL Apply]**.
- Suchen Sie [!UICONTROL Attribute] nach `[!UICONTROL segment_name]` und wählen Sie dann aus dem Dropdown-Menü das Symbol + aus, um `segment_name` als [!UICONTROL Color] hinzuzufügen.
- Öffnen Sie [Bedienfeld [!UICONTROL Eigenschaften] ](../standard-dashboards.md#widget-properties) und geben Sie einen geeigneten [!UICONTROL Widget-Titel] und [!UICONTROL Achsenbeschriftung].
  ![Der Widget-Composer mit dem Eigenschaftensymbol und dem hervorgehobenen Widget-Titel.](../images/standard-dashboards/properties-panel.png)
- Klicken Sie **[!UICONTROL Speichern und schließen]**, um Ihre Einstellungen zu bestätigen.

>[!TIP]
>
>Sie können jetzt die Größe des Widgets ändern oder es in die gewünschte Größe und Position verschieben, bevor Sie das Dashboard speichern.


Die folgende Abbildung zeigt, wie Ihr fertiges Widget angezeigt wird, und bietet weitere potenzielle benutzerdefinierte Einblicke. Weitere Informationen zu den Arten von Widgets, die erstellt werden können, finden Sie in der [Datenmodelldokumentation](../data-models/cdp-insights-data-model-b2c.md).

<!-- The diagram shows straight lines due to a lack of data, however in your environment the trends will reflect the actual changes over time. -->

![Das fertige Widget „Benutzerdefinierte Einverständnistrends“.](../images/insights-use-cases/consent-analysis/consent-trends-widget.png)

## Einverständnisrichtlinien verfolgen {#consent-policies}

Die von Ihnen erstellten Einverständnis-Dashboards erfassen **nur die Verteilung der Einverständnis- und Präferenzattribute**.

>[!NOTE]
>
>Für Kundinnen und Kunden von **Adobe Healthcare Shield** oder **Adobe Privacy &amp; Security Shield** spiegeln diese Dashboards **keine)** Verfolgung von Einverständnisrichtlinien wider. Das verfügbare Tracking umfasst die Anzahl der erstellten, aktivierten Richtlinien und die Auswirkungen auf die Zielgruppenzugehörigkeit.

## Nächste Schritte

Durch das Lesen dieses Dokuments haben Sie gelernt, wie Sie mithilfe von Real-Time CDP Insights Dashboards für eine umfassende Ansicht Ihrer Voreinstellungen für das Kundeneinverständnis erstellen können. In diesem Dokument wird gezeigt, wie Real-Time CDP eine robuste Lösung für die heutige datenschutzorientierte Landschaft bietet, in der die Erfassung, Segmentierung, Analyse und personalisierte Marketing-Kampagnen, die auf Einverständnisdaten basieren, für Marketing-Experten entscheidend sind.
