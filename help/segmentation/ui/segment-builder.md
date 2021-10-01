---
keywords: Experience Platform; Startseite; beliebte Themen; Segmentierungsdienst; Segmentierung; Segmentierungsdienst; Benutzerhandbuch; Benutzerhandbuch; Handbuch zur Segmentierung; Segment Builder; Segment Builder
solution: Experience Platform
title: Benutzerhandbuch für Segment Builder
topic-legacy: ui guide
description: Der Segmentaufbau in der Adobe Experience Platform-Benutzeroberfläche bietet einen umfassenden Arbeitsbereich, in dem Sie mit Profildatenelementen interagieren können. Der Arbeitsbereich bietet intuitive Steuerelemente zum Erstellen und Bearbeiten von Regeln, z. B. Drag-and-Drop-Kacheln, die zur Darstellung von Dateneigenschaften dienen.
exl-id: b27516ea-8749-4b44-99d0-98d3dc2f4c65
source-git-commit: 11e8acc3da7f7540421b5c7f3d91658c571fdb6f
workflow-type: tm+mt
source-wordcount: '1996'
ht-degree: 42%

---

# Handbuch für die [!DNL Segment Builder]-Benutzeroberfläche

[!DNL Segment Builder] bietet einen umfassenden Arbeitsbereich, in dem Sie mit  [!DNL Profile] Datenelementen interagieren können. Der Arbeitsbereich bietet intuitive Steuerelemente zum Erstellen und Bearbeiten von Regeln, z. B. Drag-and-Drop-Kacheln, die zur Darstellung von Dateneigenschaften dienen.

![](../images/ui/segment-builder/segment-builder.png)

## Bausteine einer Segmentdefinition

Die grundlegenden Bausteine von Segmentdefinitionen sind Attribute und Ereignisse. Darüber hinaus können die in bestehenden Zielgruppen enthaltenen Attribute und Ereignisse auch als Komponenten für neue Definitionen verwendet werden.

Sie können diese Bausteine im Abschnitt **[!UICONTROL Felder]** links im Arbeitsbereich von sehen.[!DNL Segment Builder] **** Felder enthalten für jeden der Hauptbausteine eine Registerkarte: &quot;[!UICONTROL Attribute]&quot;, &quot;[!UICONTROL Ereignisse]&quot;und &quot;[!UICONTROL Zielgruppen]&quot;.

![](../images/ui/segment-builder/segment-fields.png)

### Attribute

Auf der Registerkarte **[!UICONTROL Attribute]** können Sie [!DNL Profile]-Attribute durchsuchen, die zur Klasse [!DNL XDM Individual Profile] gehören. Jeder Ordner lässt sich erweitern, um zusätzliche Attribute anzuzeigen. Jedes Attribut ist eine Kachel, die in der Mitte des Arbeitsbereichs in die Arbeitsfläche des Regel-Builders gezogen werden kann. Die [Arbeitsfläche des Regel-Builders](#rule-builder-canvas) wird weiter unten in diesem Handbuch erläutert.

![](../images/ui/segment-builder/attributes.png)

### Ereignisse

Mit dem Tab **[!UICONTROL Ereignisse]** können Sie eine Zielgruppe basierend auf Ereignissen oder Aktionen erstellen, die mithilfe von [!DNL XDM ExperienceEvent] -Datenelementen stattgefunden haben. Sie finden Ereignistypen auch auf dem Tab **[!UICONTROL Ereignisse]**; dabei handelt es sich um eine Kollektion häufig verwendeter Ereignisse, mit denen Sie Segmente schneller erstellen können.

Sie können nicht nur nach [!DNL ExperienceEvent] -Elementen suchen, sondern auch nach Ereignistypen. Ereignistypen verwenden dieselbe Kodierungslogik wie [!DNL ExperienceEvents], ohne dass Sie die [!DNL XDM ExperienceEvent]-Klasse durchsuchen müssen, um nach dem richtigen Ereignis zu suchen. Wenn Sie beispielsweise die Suchleiste verwenden, um nach &quot;Warenkorb&quot;zu suchen, werden die Ereignistypen &quot;[!UICONTROL AddCart]&quot;und &quot;[!UICONTROL RemoveCart]&quot;zurückgegeben, bei denen es sich um zwei sehr häufig verwendete Warenkorbaktionen beim Erstellen von Segmentdefinitionen handelt.

Sie können nach beliebigen Komponenten suchen, indem Sie ihren Namen in die Suchleiste eingeben; diese verwendet die [Suchsyntax von Lucene](https://docs.microsoft.com/de-DE/azure/search/query-lucene-syntax). Die Suchergebnisse beginnen sich mit der Eingabe ganzer Wörter zu füllen. Wenn Sie beispielsweise eine Regel auf Grundlage des XDM-Felds `ExperienceEvent.commerce.productViews` erstellen möchten, beginnen Sie im Suchfeld mit der Eingabe von „product views“. Sobald Sie das Wort „product“ eingegeben haben, werden Suchergebnisse angezeigt. Jedes Ergebnis enthält die Objekthierarchie, zu der es gehört.

>[!NOTE]
>
>Es kann bis zu 24 Stunden dauern, bis benutzerdefinierte Schemafelder, die von Ihrer Organisation definiert wurden, angezeigt und zum Erstellen von Regeln verfügbar werden.

Anschließend können Sie [!DNL ExperienceEvents] und &quot;[!UICONTROL Ereignistypen]&quot;einfach in Ihre Segmentdefinition ziehen.

![](../images/ui/segment-builder/events-eventTypes.png)

Standardmäßig werden nur ausgefüllte Schemafelder aus Ihrem Datenspeicher angezeigt. Dazu gehört &quot;[!UICONTROL Ereignistypen]&quot;. Wenn die Liste &quot;[!UICONTROL Ereignistypen]&quot;nicht sichtbar ist oder Sie nur &quot;[!UICONTROL Any]&quot;als &quot;[!UICONTROL Ereignistyp]&quot;auswählen können, wählen Sie das **Zahnradsymbol** neben **[!UICONTROL Felder]** aus und wählen Sie dann **[!UICONTROL Vollständig anzeigen DM-Schema]** unter **[!UICONTROL Verfügbare Felder]**. Wählen Sie das Zahnradsymbol **** erneut aus, um zur Registerkarte **[!UICONTROL Felder]** zurückzukehren. Jetzt sollten Sie mehrere &quot;[!UICONTROL Ereignistypen]&quot;und Schemafelder anzeigen können, unabhängig davon, ob sie Daten enthalten oder nicht.

![](../images/ui/segment-builder/show-populated.png)

### Audiences

Im Tab **[!UICONTROL Zielgruppen]** werden alle Zielgruppen aufgelistet, die aus externen Quellen wie Adobe Audience Manager importiert wurden, sowie alle Zielgruppen, die mit [!DNL Experience Platform] erstellt wurden.

Auf der Registerkarte **[!UICONTROL Zielgruppen]** können Sie alle verfügbaren Quellen als Gruppe von Ordnern anzeigen. Bei der Auswahl der Ordner werden verfügbare Unterordner und Zielgruppen angezeigt. Darüber hinaus können Sie das Ordnersymbol (wie im Bild ganz rechts dargestellt) auswählen, um die Ordnerstruktur anzuzeigen (ein Häkchen gibt den Ordner an, in dem Sie sich gerade befinden) und durch Auswählen des Ordnernamens im Baum einfach durch die Ordner zurückzunavigieren.

Wenn Sie mit dem Mauszeiger über das ⓘ neben einer Zielgruppe fahren, können Sie Informationen zur Zielgruppe anzeigen, einschließlich Kennung, Beschreibung und Ordnerhierarchie zum Auffinden der Zielgruppe.

![](../images/ui/segment-builder/audience-folder-structure.png)

Sie können auch über die Suchleiste nach Zielgruppen suchen, die die Suchsyntax von [Lucene](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax) verwendet. Wenn Sie auf dem Tab **[!UICONTROL Audiences]** einen Ordner der obersten Ebene auswählen, wird die Suchleiste angezeigt, sodass Sie in diesem Ordner suchen können. Suchergebnisse beginnen sich erst dann zu füllen, wenn ganze Wörter eingegeben werden. Um beispielsweise eine Zielgruppe mit dem Namen `Online Shoppers` zu finden, geben Sie in die Suchleiste &quot;Online&quot;ein. Nach vollständiger Eingabe des Worts „Online“ erscheinen Suchergebnisse, die das Wort „Online“ enthalten.

## Arbeitsfläche des Regel-Builders {#rule-builder-canvas}

Eine Segmentdefinition ist eine Kollektion von Regeln, die zur Beschreibung der Hauptmerkmale oder Verhaltensweisen einer Zielgruppe dienen. Diese Regeln werden mithilfe der Arbeitsfläche des Regel-Builders erstellt, die sich in der Mitte von [!DNL Segment Builder] befindet.

Um Ihrer Segmentdefinition eine neue Regel hinzuzufügen, ziehen Sie eine Kachel aus dem Tab **[!UICONTROL Felder]** und legen Sie sie auf der Arbeitsfläche des Regel-Builders ab. Anschließend werden Ihnen je nach Art der hinzugefügten Daten kontextspezifische Optionen angezeigt. Zu den verfügbaren Datentypen gehören: Zeichenfolgen, Datumsangaben, [!DNL ExperienceEvents], &quot;[!UICONTROL Ereignistypen]&quot;und Zielgruppen.

![](../images/ui/segment-builder/rule-builder-canvas.png)

>[!IMPORTANT]
>
>Die neuesten Änderungen an Adobe Experience Platform haben die Verwendung der logischen Operatoren `OR` und `AND` zwischen Ereignissen aktualisiert. Diese Aktualisierungen wirken sich nicht auf bestehende Segmente aus. Diese Änderungen wirken sich jedoch auf alle nachfolgenden Aktualisierungen vorhandener Segmente und der Erstellung neuer Segmente aus. Weitere Informationen finden Sie unter [Update der Zeitkonstanten](./segment-refactoring.md) .

### Hinzufügen von Zielgruppen

Sie können eine Zielgruppe per Drag-and-Drop vom Tab **[!UICONTROL Zielgruppe]** auf die Arbeitsfläche des Regel-Builders ziehen, um auf die Zielgruppenzugehörigkeit in der neuen Segmentdefinition zu verweisen. Auf diese Weise können Sie Zielgruppenzugehörigkeit als Attribut in der neuen Segmentregel ein- oder ausschließen.

Für [!DNL Platform]-Zielgruppen, die mit [!DNL Segment Builder] erstellt wurden, haben Sie die Möglichkeit, die Zielgruppe in den Regelsatz zu konvertieren, der in der Segmentdefinition für diese Zielgruppe verwendet wurde. Diese Konversion erstellt eine Kopie der Regellogik, die dann ohne Beeinträchtigung der ursprünglichen Segmentdefinition verändert werden kann. Vergewissern Sie sich, dass Sie die letzten Änderungen an Ihrer Segmentdefinition gespeichert haben, bevor Sie sie in Regellogik konvertieren.

>[!NOTE]
>
> Beim Hinzufügen einer Zielgruppe aus einer externen Quelle wird nur auf die Zielgruppenzugehörigkeit verwiesen. Sie können die Zielgruppe nicht in Regeln konvertieren. Daher können die zum Erstellen der ursprünglichen Zielgruppe verwendeten Regeln in der neuen Segmentdefinition auch nicht geändert werden.

![](../images/ui/segment-builder/add-audience-to-segment.png)

Wenn beim Konvertieren von Zielgruppen in Regeln Konflikte auftreten, versucht [!DNL Segment Builder], die vorhandenen Optionen optimal zu erhalten.

### Codeansicht

Alternativ können Sie eine code-basierte Version einer Regel anzeigen, die in [!DNL Segment Builder] erstellt wurde. Nachdem Sie Ihre Regel auf der Arbeitsfläche des Regel-Builders erstellt haben, können Sie **[!UICONTROL Codeansicht]** auswählen, um Ihr Segment als PQL anzuzeigen.

![](../images/ui/segment-builder/code-view.png)

Die Codeansicht bietet eine Schaltfläche, mit der Sie den Wert des Segments kopieren können, das in API-Aufrufen verwendet werden soll. Um die neueste Version des Segments zu erhalten, stellen Sie sicher, dass Sie Ihre neuesten Änderungen am Segment gespeichert haben.

![](../images/ui/segment-builder/copy-code.png)

### Aggregationsfunktionen

Eine Aggregation in [!DNL Segment Builder] ist eine Berechnung für eine Gruppe von XDM-Attributen, deren Datentyp eine Zahl ist (entweder eine Dublette oder eine Ganzzahl). Die vier unterstützten Aggregationsfunktionen in Segment Builder sind SUM, AVERAGE, MIN und MAX.

Um eine Aggregationsfunktion zu erstellen, wählen Sie ein Ereignis aus der linken Leiste aus und fügen Sie es in den Container [!UICONTROL Events] ein.

![](../images/ui/segment-builder/select-event.png)

Nachdem Sie das Ereignis im Ereignisbehälter platziert haben, wählen Sie das Auslassungssymbol (...) gefolgt von **[!UICONTROL Aggregate]**.

![](../images/ui/segment-builder/add-aggregation.png)

Die Aggregation wird jetzt hinzugefügt. Jetzt können Sie die Aggregationsfunktion auswählen, das zu aggregierende Attribut, die Gleichheitsfunktion sowie den Wert auswählen. Im folgenden Beispiel würde dieses Segment alle Profile qualifizieren, deren Summe der erworbenen Werte über 100 USD liegt, selbst wenn jeder einzelne Kauf unter 100 USD liegt.

![](../images/ui/segment-builder/filled-aggregation.png)

### Count-Funktionen {#count-functions}

Mit den Count-Funktionen in Segment Builder können Sie nach bestimmten Ereignissen suchen und zählen, wie oft sie durchgeführt wurden. Die unterstützten Zählerfunktionen im Segmentaufbau sind &quot;Mindestens&quot;, &quot;höchstens&quot;, &quot;Genau&quot;, &quot;Zwischen&quot;und &quot;Alle&quot;.

Um eine Zählerfunktion zu erstellen, wählen Sie ein Ereignis aus der linken Leiste aus und fügen Sie es in den Container [!UICONTROL Ereignisse] ein.

![](../images/ui/segment-builder/add-event.png)

Nachdem Sie das Ereignis im Ereignisbehälter platziert haben, wählen Sie die Schaltfläche [!UICONTROL Mindestens 1] aus.

![](../images/ui/segment-builder/add-count.png)

Die Funktion count wird jetzt hinzugefügt. Jetzt können Sie die Funktion count und den Wert der Funktion auswählen. Im folgenden Beispiel sollen alle Ereignisse mit mindestens einem Klick einbezogen werden.

![](../images/ui/segment-builder/select-count.png)

## Container

Segmentregeln werden in der Reihenfolge ausgewertet, in der sie aufgelistet sind. Container ermöglichen eine Steuerung der Ausführungsreihenfolge durch Verwendung verschachtelter Abfragen.

Nachdem Sie der Arbeitsfläche des Regel-Builders mindestens eine Kachel hinzugefügt haben, können Sie beginnen, Container hinzuzufügen. Um einen neuen Container zu erstellen, wählen Sie die Auslassungszeichen (...) in der oberen rechten Ecke der Kachel aus und klicken Sie dann auf **[!UICONTROL Container hinzufügen]**.

![](../images/ui/segment-builder/add-container.png)

Ein neuer Container wird als untergeordnetes Element des ersten Containers angezeigt. Sie können die Hierarchie jedoch durch Ziehen und Verschieben der Container anpassen. Das Standardverhalten eines Containers besteht in der Angabe &quot;[!UICONTROL Include]&quot;des angegebenen Attributs, Ereignisses oder der angegebenen Zielgruppe. Sie können die Regel auf &quot;[!UICONTROL Profile ausschließen]&quot;setzen, die den Behälterkriterien entsprechen, indem Sie **[!UICONTROL Einschließen]** in der oberen linken Ecke der Kachel auswählen und &quot;[!UICONTROL Ausschließen]&quot;auswählen.

Ein untergeordneter Container kann auch extrahiert und inline zum übergeordneten Container hinzugefügt werden, indem Sie im untergeordneten Container &quot;Container entpacken&quot;auswählen. Wählen Sie die Auslassungszeichen (...) in der oberen rechten Ecke des untergeordneten Containers aus, um auf diese Option zuzugreifen.

![](../images/ui/segment-builder/include-exclude.png)

Sobald Sie **[!UICONTROL Container entfernen]** auswählen, wird der untergeordnete Container entfernt und die Kriterien werden inline angezeigt.

>[!NOTE]
>
>Achten Sie beim Entpacken von Containern darauf, dass die Logik weiterhin der gewünschten Segmentdefinition entspricht.

![](../images/ui/segment-builder/unwrapped-container-inline.png)

## Zusammenführungsrichtlinien

[!DNL Experience Platform]Mit können Sie Daten aus verschiedenen Quellen zusammenführen und kombinieren, damit Sie sich einen kompletten Überblick über einzelne Kunden verschaffen können. Beim Zusammenführen dieser Daten dienen Zusammenführungsrichtlinien als jene Regeln, mit denen [!DNL Platform] bestimmt, wie Daten priorisiert werden und welche Daten kombiniert werden, um ein Profil zu erstellen.

Sie können eine Zusammenführungsrichtlinie auswählen, die Ihrem Marketing-Zweck für diese Zielgruppe entspricht, oder die standardmäßige Zusammenführungsrichtlinie verwenden, die von [!DNL Platform] bereitgestellt wird. Sie können verschiedene, für Ihre Organisation eindeutige Zusammenführungsrichtlinien erstellen, einschließlich einer eigenen standardmäßigen Zusammenführungsrichtlinie. Eine schrittweise Anleitung zum Erstellen von Zusammenführungsrichtlinien für Ihr Unternehmen finden Sie in der [Übersicht über Zusammenführungsrichtlinien](../../profile/merge-policies/overview.md).

Um eine Zusammenführungsrichtlinie für Ihre Segmentdefinition auszuwählen, wählen Sie das Zahnradsymbol auf der Registerkarte **[!UICONTROL Felder]** aus und wählen Sie dann im Dropdown-Menü **[!UICONTROL Zusammenführungsrichtlinie]** die gewünschte Zusammenführungsrichtlinie aus.

![](../images/ui/segment-builder/merge-policy-selector.png)

## Segmenteigenschaften

Beim Erstellen einer Segmentdefinition zeigt der Abschnitt **[!UICONTROL Segmenteigenschaften]** auf der rechten Seite des Arbeitsbereichs eine geschätzte Größe des resultierenden Segments an, sodass Sie die Segmentdefinition nach Bedarf anpassen können, bevor Sie die eigentliche Zielgruppe erstellen.

Im Abschnitt **[!UICONTROL Segmenteigenschaften]** können Sie auch wichtige Informationen zur Segmentdefinition angeben, einschließlich Name und Beschreibung. Namen von Segmentdefinitionen dienen dazu, Ihr Segment unter den von Ihrer Organisation definierten Segmenten zu identifizieren. Sie sollten daher beschreibend, knapp und eindeutig sein.

Wenn Sie mit der Erstellung Ihrer Segmentdefinition fortfahren, können Sie durch Auswahl von **[!UICONTROL Profile anzeigen]** eine paginierte Vorschau der Zielgruppe anzeigen.

![](../images/ui/segment-builder/segment-properties.png)

>[!NOTE]
>
> Audience-Schätzungen werden anhand einer Stichprobengröße der Beispieldaten dieses Tages erstellt. Wenn sich in Ihrem Profilspeicher weniger als 1 Million Entitäten befinden, wird der vollständige Datensatz verwendet. Bei zwischen 1 und 20 Millionen Entitäten werden 1 Million Entitäten verwendet; bei mehr als 20 Millionen Entitäten werden 5 % der Gesamtentitäten genutzt. Weiterführende Informationen zum Generieren von Segmentschätzungen finden Sie in der Anleitung zur Segmenterstellung im Abschnitt zum [Generieren von Schätzungen](../tutorials/create-a-segment.md#estimate-and-preview-an-audience).

## Nächste Schritte {#next-steps}

Segment Builder bietet einen umfassenden Workflow, mit dem Sie marktfähige Zielgruppen aus [!DNL Real-time Customer Profile]-Daten isolieren können. Nach dem Lesen dieses Handbuchs sollten Sie jetzt Folgendes können:

- Segmentdefinitionen mit einer Kombination aus Attributen, Ereignissen und vorhandenen Zielgruppen als Bausteinen erstellen.
- Die Arbeitsfläche des Regel-Builders und Container verwenden, um die Reihenfolge zu steuern, in der Segmentregeln ausgeführt werden.
- Schätzungen der voraussichtlichen Zielgruppe anzeigen, sodass Sie Ihre Segmentdefinitionen nach Bedarf anpassen können.
- Alle Segmentdefinitionen für geplante Segmentierung aktivieren.
- Spezifische Segmentdefinitionen für Streaming-Segmentierung aktivieren.

Um mehr über [!DNL Segmentation Service] zu erfahren, lesen Sie bitte die Dokumentation weiter und ergänzen Sie Ihr Lernprogramm durch die zugehörigen Videos. Weitere Informationen zu den anderen Teilen der [!DNL Segmentation Service]-Benutzeroberfläche finden Sie im [[!DNL Segmentation Service] Benutzerhandbuch](./overview.md)
