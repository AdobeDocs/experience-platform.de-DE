---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handbuch zur Segmentaufbau-Benutzeroberfläche
topic: ui guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '2683'
ht-degree: 0%

---


# Segment Builder-Benutzerhandbuch

[!DNL Adobe Experience Platform Segmentation Service] stellt eine RESTful-API und eine Benutzeroberfläche zum Erstellen von Segmentdefinitionen aus [!DNL Real-time Customer Profile] Daten bereit.

## Erste Schritte

Das Arbeiten mit Segmentdefinitionen erfordert ein Verständnis der verschiedenen mit der Segmentierung verbundenen [!DNL Experience Platform] Dienste. Bevor Sie dieses Benutzerhandbuch lesen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [!DNL Segmentation Service](../home.md): Mit dem Segmentierungsdienst können Sie Daten, [!DNL Experience Platform] die zu Einzelpersonen (z. B. Kunden, Potenzieller Kunden, Benutzer oder Organisationen) gespeichert wurden, in kleinere Gruppen unterteilen, die ähnliche Eigenschaften aufweisen und ähnlich wie Marketingstrategien reagieren.
- [!DNL Real-time Customer Profile](../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
- [!DNL Identity Service](../../identity-service/home.md): Ermöglicht [!DNL Real-time Customer Profile] die Überbrückung von Identitäten aus unterschiedlichen Datenquellen, die in die Platform aufgenommen werden.
- [!DNL Experience Data Model (XDM)](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten [!DNL Platform] organisiert werden.

Es ist außerdem wichtig, zwei Schlüsselbegriffe zu kennen, die in diesem Dokument verwendet werden, und den Unterschied zwischen ihnen zu verstehen:
- **Segmentdefinition**: Der Regelsatz, der zur Beschreibung wichtiger Merkmale oder Verhaltensweisen einer Zielgruppe-Audience verwendet wird.
- **Audience**: Der resultierende Satz von Profilen, die die Kriterien einer Segmentdefinition erfüllen.

## Zugriff auf Segmentdefinitionen

Um mit der Arbeit mit Segmentdefinitionen in zu beginnen, [!DNL Adobe Experience Platform]klicken Sie im linken Navigationsbereich auf **[!UICONTROL Segmente]** . Um alle Segmentdefinitionen für Ihr Unternehmen anzuzeigen, klicken Sie auf die Registerkarte &quot; *[!UICONTROL Durchsuchen]* &quot;. Diese Ansicht Liste Informationen zur Segmentdefinition, einschließlich der Bewertungsmethode, des erstellten Datums und des zuletzt geänderten Datums.

Die Bewertungsmethode kann entweder Streaming oder Batch sein. Streaming-Segmente werden ständig ausgewertet, wenn Daten in das System gelangen. Stapelsegmente werden gemäß einem festgelegten Zeitplan ausgewertet.

Für Stapelsegmente werden zusätzliche Informationen angezeigt, die sowohl das letzte Bewertungsdatum als auch das nächste Bewertungsdatum für den Stapel anzeigen.

Durch Klicken auf Segment **** erstellen in der oberen rechten Ecke wird der Segment Builder-Arbeitsbereich geöffnet, in dem Sie mit der Erstellung einer Segmentdefinition beginnen können.

![](../images/segment-builder/segment-browse.png)

## [!UICONTROL Segmentaufbau] -Arbeitsbereich

[!UICONTROL Der Segmentaufbau] bietet eine umfangreiche Arbeitsfläche, mit der Sie mit [!DNL Profile] Datenelementen interagieren können. Der Arbeitsbereich bietet intuitive Steuerelemente zum Erstellen und Bearbeiten von Regeln, z. B. Drag &amp; Drop-Kacheln, die zur Darstellung von Dateneigenschaften verwendet werden.

![](../images/segment-builder/segment-builder.png)

## Bausteine für die Segmentdefinition

Die grundlegenden Bausteine der Segmentdefinitionen sind **[!UICONTROL Attribute]** und **[!UICONTROL Ereignis]**. Darüber hinaus können die in bestehenden **[!UICONTROL Audiencen]** enthaltenen Attribute und Ereignis auch als Komponenten für neue Definitionen verwendet werden.

Sie können diese Bausteine im Abschnitt &quot; *Felder* &quot;auf der linken Seite des [!UICONTROL Segmentaufbaus] sehen. *[!UICONTROL Felder]* enthalten eine Registerkarte für jeden der Hauptbausteine: **[!UICONTROL Attribute]**, **[!UICONTROL Ereignis]** und **[!UICONTROL Audiencen]**.

![](../images/segment-builder/segment-fields.png)

### Attribute

Auf der Registerkarte &quot; **[!UICONTROL Attribute]** &quot;können Sie nach [!DNL Profile] Attributen suchen, die zur [!DNL XDM Individual Profile] Klasse gehören. Jeder Ordner kann erweitert werden, um zusätzliche Attribute anzuzeigen. Jedes Attribut ist eine Kachel, die in die Arbeitsfläche des Regelaufbaus in der Mitte des Arbeitsbereichs gezogen werden kann. Die Arbeitsfläche [des](#rule-builder-canvas) Regelaufbaus wird weiter unten in diesem Handbuch erläutert.

![](../images/segment-builder/attributes.png)

### Ereignisse

Auf der Registerkarte &quot; **[!UICONTROL Ereignis]** &quot;können Sie eine Audience erstellen, die auf Ereignissen oder Aktionen basiert, die mit XDM ExperienceEvent-Datenelementen durchgeführt wurden. Sie finden Ereignistyp auch auf der Registerkarte &quot; **[!UICONTROL Ereignis]** &quot;, bei denen es sich um eine Sammlung häufig verwendeter Ereignis handelt, mit denen Sie Ihre Segmente schneller erstellen können.

Sie können nicht nur nach [!DNL ExperienceEvent] Elementen suchen, sondern auch nach Ereignistypen suchen. Ereignistyp verwenden dieselbe Kodierungslogik wie [!DNL ExperienceEvents], ohne dass Sie nach dem richtigen Ereignis suchen müssen, um die [!DNL XDM ExperienceEvent] Klasse zu durchsuchen. Wenn Sie z. B. in der Suchleiste nach &quot;Warenkorb&quot;suchen, werden die Ereignistyp &quot;[!UICONTROL Warenkorb]&quot;und &quot;[!UICONTROL Warenkorb]&quot;zurückgegeben, bei denen es sich um zwei sehr häufig verwendete Warenkorbaktionen beim Erstellen von Segmentdefinitionen handelt.

Sie können nach beliebigen Komponenten suchen, indem Sie deren Namen in die Suchleiste eingeben, die die Suchsyntax von [Lucene verwendet](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). Die Suchergebnisse beginnen mit der Eingabe ganzer Wörter zu füllen. Wenn Sie beispielsweise eine Regel auf Grundlage des XDM-Felds erstellen möchten, geben Sie `ExperienceEvent.commerce.productViews`im Suchfeld Beginn &quot;product Ansichten&quot;ein. Sobald das Wort &quot;Produkt&quot;eingegeben wurde, werden die Suchergebnisse angezeigt. Jedes Ergebnis enthält die Objekthierarchie, zu der es gehört.

>[!NOTE]
>
>Die Anzeige von benutzerdefinierten Schema-Feldern, die von Ihrem Unternehmen definiert wurden, kann bis zu 24 Stunden in Anspruch nehmen und steht für die Verwendung bei der Erstellung von Regeln zur Verfügung.

Sie können dann einfach per Drag &amp; Drop [!DNL ExperienceEvents] und [!UICONTROL Ereignistyp] in Ihre Segmentdefinition ziehen.

![](../images/segment-builder/events-eventTypes.png)

Standardmäßig werden nur ausgefüllte Schema-Felder aus Ihrem Datenspeicher angezeigt. Dies schließt [!UICONTROL Ereignistyp]ein. Wenn die Liste &quot; [!UICONTROL Ereignistyp] &quot;nicht sichtbar ist oder Sie nur &quot;[!UICONTROL Beliebig]&quot;als [!UICONTROL Ereignistyp]auswählen können, klicken Sie auf das Zahnradsymbol neben &quot; *[!UICONTROL Felder]*&quot;und wählen Sie dann unter &quot;Verfügbare Felder&quot;die Option &quot;Vollständiges XDM-Schema **** ** anzeigen&quot;unter &quot; verfügbare Felder&quot;aus. Klicken Sie erneut auf das Zahnradsymbol, um zur Registerkarte &quot; *[!UICONTROL Felder]* &quot;zurückzukehren, und Sie sollten jetzt mehrere [!UICONTROL Ereignistyp] - und Schema-Felder unabhängig davon, ob sie Daten enthalten oder nicht, Ansicht werden können.

![](../images/segment-builder/show-populated.png)

### Zielgruppen

Auf der Registerkarte &quot; **[!UICONTROL Audiencen]** &quot;werden alle Audiencen, die aus externen Quellen importiert wurden (z. B. Adobe Audience Manager), sowie alle darin erstellten Audiencen Liste [!DNL Experience Platform].

Auf der Registerkarte &quot; [!UICONTROL Audiencen] &quot;können Sie alle verfügbaren Quellen als Ordnergruppe anzeigen. Wenn Sie in diese Ordner klicken, werden verfügbare Unterordner und Audiencen angezeigt. Außerdem können Sie auf das Ordnersymbol klicken (wie im Bild ganz rechts), um die Ordnerstruktur (ein Häkchen gibt den Ordner an, in dem Sie sich befinden) Ansicht und einfach durch Klicken auf den Ordnernamen im Baum durch die Ordnerstruktur zurück zu navigieren.

Wenn Sie den Mauszeiger über das ⓘ neben einer Audience halten, können Sie Informationen zur Ansicht der Audience einschließlich ID, Beschreibung und Ordnerhierarchie aufrufen, um die Audience zu suchen.

![](../images/segment-builder/audience-folder-structure.png)

Sie können auch über die Suchleiste nach [!UICONTROL Audiencen] suchen, die die Suchsyntax [von](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)Lucene verwendet. Wenn Sie auf der Registerkarte &quot; *[!UICONTROL Audiencen]* &quot;einen Ordner der obersten Ebene auswählen, wird die Suchleiste angezeigt, sodass Sie in diesem Ordner suchen können. Die Suchergebnisse beginnen erst dann zu füllen, wenn die gesamten Wörter eingegeben wurden. Wenn Sie beispielsweise eine [!UICONTROL Audience] mit dem Namen `Online Shoppers`suchen möchten, geben Sie in der Suchleiste Beginn &quot;Online&quot;ein. Sobald das Wort &quot;Online&quot; vollständig eingegeben wurde, erscheinen die Suchergebnisse mit dem Wort &quot;Online&quot;.

## Arbeitsfläche Regelaufbau {#rule-builder-canvas}

Eine Segmentdefinition ist eine Auflistung von Regeln, die zur Beschreibung der Hauptmerkmale oder des Verhaltens einer Zielgruppe-Audience verwendet werden. Diese Regeln werden mithilfe der Arbeitsfläche *[!UICONTROL des]* Regelaufbaus im Zentrum des [!UICONTROL Segmentaufbaus]erstellt.

Um Ihrer Segmentdefinition eine neue Regel hinzuzufügen, ziehen Sie eine Kachel aus der Registerkarte &quot; *[!UICONTROL Felder]* &quot;und legen Sie sie auf der Arbeitsfläche des Regelaufbaus ab. Anschließend werden Ihnen kontextspezifische Optionen entsprechend der Art der hinzugefügten Daten angezeigt. Zu den verfügbaren Datentypen gehören: Zeichenfolgen, Datumsangaben, [!DNL ExperienceEvents]Ereignistyp [!UICONTROL und]Audiencen .

![](../images/segment-builder/rule-builder-canvas.png)

### Hinzufügen von Audiencen

Sie können eine Audience per Drag &amp; Drop von der Registerkarte &quot; *[!UICONTROL Audience]* &quot;auf die Arbeitsfläche &quot;Rule Builder&quot;ziehen, um auf die Mitgliedschaft in der Audience in der neuen Segmentdefinition zu verweisen. Auf diese Weise können Sie die Audiencen-Mitgliedschaft als Attribut in der neuen Segmentregel ein- oder ausschließen.

Bei [!DNL Platform] Audiencen, die mit dem [!UICONTROL Segmentaufbau]erstellt wurden, können Sie die Audience in den Regelsatz konvertieren, der in der Segmentdefinition für diese Audience verwendet wurde. Diese Konversion erstellt eine Kopie der Regellogik, die dann ohne Beeinträchtigung der ursprünglichen Segmentdefinition geändert werden kann. Vergewissern Sie sich, dass Sie alle Änderungen an Ihrer Segmentdefinition gespeichert haben, bevor Sie sie in Regellogik konvertieren.

>[!NOTE]
>
>Beim Hinzufügen einer Audience aus einer externen Quelle wird nur auf die Audience-Mitgliedschaft verwiesen. Sie können die Audience nicht in Regeln konvertieren. Daher können die zum Erstellen der ursprünglichen Audience verwendeten Regeln in der neuen Segmentdefinition nicht geändert werden.

![](../images/segment-builder/add-audience-to-segment.png)

Treten beim Konvertieren von Audiencen in Regeln Konflikte auf, versucht der [!UICONTROL Segmentaufbau] , die vorhandenen Optionen optimal zu erhalten.

### Code-Ansicht

Alternativ können Sie eine codebasierte Version einer Regel, die im [!UICONTROL Segmentaufbau]erstellt wurde, Ansicht vornehmen. Nachdem Sie Ihre Regel auf der Arbeitsfläche des Regelaufbaus erstellt haben, können Sie die **[!UICONTROL Code-Ansicht]** auswählen, um Ihr Segment als PQL anzuzeigen.

![](../images/segment-builder/code-view.png)

Die Code-Ansicht bietet eine Schaltfläche, mit der Sie den Segmentwert kopieren können, der in API-Aufrufen verwendet werden soll. Um die neueste Version des Segments abzurufen, stellen Sie sicher, dass Sie die neuesten Änderungen am Segment gespeichert haben.

![](../images/segment-builder/copy-code.png)

## Behälter

Segmentregeln werden in der Reihenfolge bewertet, in der sie aufgeführt sind. Container ermöglichen die Steuerung der Ausführungsreihenfolge durch die Verwendung verschachtelter Abfragen.

Nachdem Sie der Regelaufbauarbeitsfläche mindestens eine Kachel hinzugefügt haben, können Sie beginnen, Container hinzuzufügen. Um einen neuen Container zu erstellen, klicken Sie auf die Ellipsen (...) in der oberen rechten Ecke der Kachel und dann auf **[!UICONTROL Hinzufügen Container]**.

![](../images/segment-builder/add-container.png)

Ein neuer Container wird als untergeordnetes Element des ersten Containers angezeigt. Sie können die Hierarchie jedoch durch Ziehen und Verschieben der Container anpassen. Das Standardverhalten eines Containers besteht darin, das angegebene Attribut, Ereignis oder die bereitgestellte Audience mit &quot;[!UICONTROL Einschließen]&quot;zu versehen. Sie können die Regel auf Profil[!UICONTROL ausschließen]einstellen, die den Kriterien des Containers entsprechen, indem Sie in der oberen linken Ecke der Kachel auf **[!UICONTROL Einschließen]** klicken und &quot;[!UICONTROL Ausschließen]&quot;wählen.

Ein untergeordneter Container kann auch extrahiert und inline zum übergeordneten Container hinzugefügt werden, indem auf &quot;Container aufheben&quot;im untergeordneten Container geklickt wird. Klicken Sie auf die Auslassungspunkte (...) in der oberen rechten Ecke des untergeordneten Containers, um auf diese Option zuzugreifen.

![](../images/segment-builder/include-exclude.png)

Wenn Sie auf Container **[!UICONTROL aufheben]** klicken, wird der untergeordnete Container entfernt und die Kriterien werden inline angezeigt.

>[!NOTE]
>
>Achten Sie beim Entpacken von Containern darauf, dass die Logik weiterhin der gewünschten Segmentdefinition entspricht.

![](../images/segment-builder/unwrapped-container-inline.png)

## Zusammenführungsrichtlinien

[!DNL Experience Platform] ermöglicht es Ihnen, Daten aus mehreren Quellen zusammenzuführen und zu kombinieren, um eine vollständige Ansicht der einzelnen Kunden zu erhalten. When bringing this data together, merge policies are the rules that [!DNL Platform] uses to determine how data will be prioritized and what data will be combined to create a profile.

Sie können eine Zusammenführungsrichtlinie auswählen, die Ihrem Marketingzweck für diese Audience entspricht, oder die standardmäßige Zusammenführungsrichtlinie verwenden, die von [!DNL Platform]bereitgestellt wird. Sie können mehrere, für Ihr Unternehmen spezifische Zusammenführungsrichtlinien erstellen, einschließlich der Erstellung Ihrer eigenen Standardrichtlinie für die Zusammenführung. Eine schrittweise Anleitung zum Erstellen von Richtlinien zum Zusammenführen für Ihr Unternehmen finden Sie im Lernprogramm zum [Arbeiten mit Richtlinien zum Zusammenführen mithilfe der Benutzeroberfläche](../../profile/ui/merge-policies.md).

Um eine Richtlinie zum Zusammenführen für Ihre Segmentdefinition auszuwählen, klicken Sie auf das Zahnradsymbol auf der Registerkarte &quot; *[!UICONTROL Felder]* &quot;und wählen Sie dann im Dropdownmenü &quot; *[!UICONTROL Richtlinie]zusammenführen&quot;die gewünschte Richtlinie aus *.

![](../images/segment-builder/merge-policy-selector.png)

## Segmenteigenschaften

Beim Erstellen einer Segmentdefinition zeigt der Abschnitt *[!UICONTROL Segmenteigenschaften]* auf der rechten Seite des Arbeitsbereichs eine Schätzung der Größe des resultierenden Segments an, sodass Sie die Segmentdefinition nach Bedarf anpassen können, bevor Sie die Audience selbst erstellen.

Im Abschnitt *[!UICONTROL Segmenteigenschaften]* können Sie außerdem wichtige Informationen zur Segmentdefinition angeben, einschließlich *[!UICONTROL Name]* und *[!UICONTROL Beschreibung]*. Segmentdefinitionsnamen werden verwendet, um Ihr Segment unter den von Ihrer Organisation definierten zu identifizieren. Daher sollten sie beschreibend, knapp und eindeutig sein.

Wenn Sie Ihre Segmentdefinition weiter erstellen, können Sie eine paginierte Vorschau der Audience durch Auswahl der Profil für die **[!UICONTROL Ansicht]** Ansicht erstellen.

![](../images/segment-builder/segment-properties.png)

>[!NOTE]
>
>Die Schätzungen der Audience werden anhand einer Stichprobengröße der Stichprobendaten dieses Tages erstellt. Wenn sich in Ihrem Profil-Store weniger als 1 Million Entitäten befinden, wird der vollständige Datensatz verwendet. für zwischen 1 und 20 Millionen Unternehmen werden 1 Million Einheiten verwendet; und für mehr als 20 Millionen Unternehmen werden 5 % der Gesamteinheiten verwendet. Weitere Informationen zum Generieren von Segmentschätzungen finden Sie im Abschnitt zur [Schätzung der Generierung](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) des Lernprogramms zur Segmenterstellung.

## Geplante Segmentierung aktivieren {#enable-scheduled-segmentation}

Nachdem Sie Segmentdefinitionen erstellt haben, können Sie diese dann durch On-Demand- oder geplante (kontinuierliche) Evaluierung bewerten. Bewertung bedeutet, dass [!DNL Real-time Customer Profile] Daten durch Segmentdefinitionen verschoben werden, um entsprechende Audiencen zu erhalten. Nach der Erstellung werden die Audiencen gespeichert und gespeichert, damit sie mit [!DNL Experience Platform] APIs exportiert werden können.

Bei der On-Demand-Bewertung wird die API zur Durchführung von Evaluierungen und zum Aufbau von Audiencen nach Bedarf verwendet. Bei der geplanten Auswertung (auch als &quot;geplante Segmentierung&quot;bezeichnet) können Sie jedoch einen Zeitplan erstellen, um die Segmentdefinitionen zu einem bestimmten Zeitpunkt (maximal einmal täglich) zu bewerten.

Die Aktivierung Ihrer Segmentdefinitionen für die geplante Evaluierung kann über die Benutzeroberfläche oder die API erfolgen. Kehren Sie in der Benutzeroberfläche zur Registerkarte &quot; *[!UICONTROL Durchsuchen]* &quot;innerhalb von **[!UICONTROL Segmenten]** zurück und schalten Sie auf Alle Segmente **[!UICONTROL auswerten]** um. Dadurch werden alle Segmente basierend auf dem von Ihrer Organisation festgelegten Zeitplan bewertet.

>[!NOTE]
>
>Geplante Evaluierung kann für Sandboxen mit maximal fünf (5) Zusammenführungsrichtlinien aktiviert werden, für die [!DNL XDM Individual Profile]die Funktion aktiviert ist. Wenn Ihr Unternehmen über mehr als fünf Zusammenführungsrichtlinien für [!DNL XDM Individual Profile] eine einzige Sandbox-Umgebung verfügt, können Sie keine geplante Auswertung verwenden.

Zeitpläne können derzeit nur mit der API erstellt werden. Ausführliche Anweisungen zum Erstellen, Bearbeiten und Arbeiten mit Zeitplänen mithilfe der API finden Sie im Tutorial zur Evaluierung und zum Zugriff auf Segmentergebnisse, insbesondere im Abschnitt zur [geplanten Auswertung mithilfe der API](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![](../images/segment-builder/scheduled-segmentation.png)

## Streaming-Segmentierung {#streaming-segmentation}

>[!NOTE]
>
>Damit Streaming-Segmentierung funktioniert, muss der Kunde die geplante Segmentierung für das Unternehmen aktivieren. Weitere Informationen zur Aktivierung der geplanten Segmentierung finden Sie im vorherigen Abschnitt [dieses Benutzerhandbuchs](#enable-scheduled-segmentation).

Eine Abfrage wird automatisch mit Streaming-Segmentierung bewertet, wenn sie eines der folgenden Kriterien erfüllt:

| Abfrage | Details | Beispiel |
| ---------- | ------- | ------- |
| Eingehender Treffer | Eine Segmentdefinition, die auf ein einzelnes eingehendes Ereignis ohne Zeitbeschränkung verweist. | ![](../images/segment-builder/incoming-hit.png) |
| Eingehender Treffer innerhalb eines relativen Zeitfensters | Eine Segmentdefinition, die auf ein einzelnes eingehendes Ereignis **innerhalb der letzten sieben Tage** verweist. | ![](../images/segment-builder/relative-hit-success.png) |
| Eingehender Treffer, der sich auf ein Profil bezieht | Eine Segmentdefinition, die sich auf ein einzelnes eingehendes Ereignis ohne Zeitbeschränkung und ein oder mehrere Profil-Attribute bezieht. | ![](../images/segment-builder/profile-hit.png) |
| Eingehender Treffer, der sich auf ein Profil innerhalb eines relativen Zeitfensters bezieht | Eine Segmentdefinition, die sich **innerhalb der letzten sieben Tage** auf ein einzelnes eingehendes Ereignis und ein oder mehrere Profil-Attribute bezieht. | ![](../images/segment-builder/profile-relative-success.png) |
| Mehrere Ereignis, die auf ein Profil verweisen | Jede Segmentdefinition, die sich **innerhalb der letzten 24 Stunden** auf mehrere Ereignis bezieht und (optional) ein oder mehrere Profil-Attribute besitzt. | ![](../images/segment-builder/event-history-success.png) |

Im folgenden Abschnitt werden Segmentdefinitionsbeispiele Liste, die für die Streaming-Segmentierung **nicht** aktiviert werden.

| Abfrage | Details |
| ---------- | ------- | 
| Eingehender Treffer innerhalb eines relativen Zeitfensters | Wenn sich die Segmentdefinition auf ein eingehendes Ereignis bezieht, das **nicht** innerhalb der **letzten sieben Tage** liegt. Zum Beispiel innerhalb der **letzten zwei Wochen**. | ![](../images/segment-builder/relative-hit-failure.png) |
| Eingehender Treffer, der sich auf ein Profil in einem relativen Fenster bezieht | Die folgenden Optionen unterstützen **keine** Streaming-Segmentierung:<ul><li>Ein eingehendes Ereignis **nicht** innerhalb der **letzten sieben Tage**.</li><li>Eine Segmentdefinition, die [!DNL Adobe Audience Manager (AAM)] Segmente oder Eigenschaften enthält.</li></ul> | ![](../images/segment-builder/profile-relative-failure.png) |
| Mehrere Ereignis, die auf ein Profil verweisen | Die folgenden Optionen unterstützen **keine** Streaming-Segmentierung:<ul><li>Ein Ereignis, das **nicht** innerhalb **der letzten 24 Stunden** auftritt.</li><li>Eine Segmentdefinition, die Segmente oder Eigenschaften des Adobe Audience Managers (AAM) enthält.</li></ul> | ![](../images/segment-builder/event-history-failure.png) |
| Abfragen mit mehreren Entitäten | Abfragen mit mehreren Entitäten werden durch Streaming-Segmentierung insgesamt **nicht** unterstützt. |  |

Darüber hinaus gelten einige Richtlinien für die Streaming-Segmentierung:

| Abfrage | Leitlinie |
| ---------- | -------- |
| Abfrage mit einem Ereignis | Das Rückblickfenster ist auf **sieben Tage** begrenzt. |
| Abfrage mit Ereignis-Verlauf | <ul><li>Das Lookback-Fenster ist auf **einen Tag** beschränkt.</li><li>Zwischen den Ereignissen **muss** eine strikte Zeitbestellbedingung bestehen.</li><li>Nur einfache Zeitreihenfolgen (vor und nach) zwischen den Ereignissen sind zulässig.</li><li>Die einzelnen Ereignis **können nicht** negiert werden. Die gesamte Abfrage **kann** jedoch negiert werden.</li></ul> |

### Überwachung der Streaming-Segmentierung

Nachdem Sie ein Streaming-fähiges Segment erstellt haben, können Sie Details zu diesem Segment überwachen.

![](../images/segment-builder/monitoring-streaming-segment.png)

Insbesondere werden Details zur Größe der *[!UICONTROL gesamten qualifizierten Audience]* angezeigt. Wenn ein Auftrag innerhalb der letzten 24 Stunden ausgeführt wurde, wird neben einem Liniendiagramm für die hinzugefügte Audience die **[!UICONTROL Gesamtgröße]** der Audience angezeigt. Andernfalls wird neben einer Visualisierungstrends-Linie auch die **[!UICONTROL geschätzte Audience]** angezeigt.

![](../images/segment-builder/monitoring-streaming-segment-graph.png)

Weitere Informationen zur letzten Segmentauswertung erhalten Sie, wenn Sie auf die Informationsblase klicken.

![](../images/segment-builder/info-bubble.png)

## Verstöße gegen DULE-Richtlinien

>[!NOTE]
>
>Verstöße gegen DULE-Richtlinien gelten nur, wenn Sie ein Segment erstellen, das einem Ziel zugewiesen wurde.

Nachdem Sie Ihr Segment erstellt haben, wird das Segment analysiert, [!DNL Data Governance] um sicherzustellen, dass es keine Richtlinienverletzungen innerhalb des Segments gibt. Weitere Informationen zu DUL- und Richtlinienverletzungen finden Sie in der Übersicht über die [Datenverwendung](../../data-governance/labels/overview.md).

![](../images/segment-builder/segment-dule-policy-violations.png)

## Nächste Schritte

Der Segmentaufbau bietet einen umfassenden Arbeitsablauf, mit dem Sie marktfähige Audiencen von [!DNL Real-time Customer Profile] Daten isolieren können. Nach dem Lesen dieses Handbuchs sollten Sie jetzt in der Lage sein:

- Erstellen Sie Segmentdefinitionen mit einer Kombination aus Attributen, Ereignissen und vorhandenen Audiencen als Bausteine.
- Verwenden Sie die Arbeitsfläche und Container des Regelaufbaus, um die Reihenfolge zu steuern, in der Segmentregeln ausgeführt werden.
- Ansicht schätzt die voraussichtliche Audience, sodass Sie Ihre Segmentdefinitionen nach Bedarf anpassen können.
- Aktivieren Sie alle Segmentdefinitionen für die geplante Segmentierung.
- Aktivieren Sie die angegebenen Segmentdefinitionen für die Streaming-Segmentierung.

Eine schrittweise Anleitung zum Arbeiten mit [!DNL Segmentation Service] der [!DNL Segmentation Service] API finden Sie im Lernprogramm zum [Erstellen von Segmenten mit APIs](../tutorials/create-a-segment.md) .