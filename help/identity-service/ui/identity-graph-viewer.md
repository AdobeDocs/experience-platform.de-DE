---
keywords: Experience Platform;home;popular topics;identity graph viewer;Identity graph viewer;graph viewer;Graph viewer;identity namespace;Identity namespace;identity;Identity;Identity service;identity service
solution: Experience Platform
title: Adobe Experience Platform Identity Service
topic: tutorial
description: Ein Identitätsdiagramm ist eine Zusammenstellung der Beziehungen zwischen verschiedenen Identitäten eines bestimmten Kunden und bietet Ihnen eine visuelle Darstellung der Interaktion Ihres Kunden mit Ihrer Marke über verschiedene Kanal hinweg.
translation-type: tm+mt
source-git-commit: 7c52760bdceb8d45d76cd22d69241f8c23943674
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 3%

---


# (Beta) Identitätsdiagramm-Viewer

>[!NOTE]
>
>Der Identitätsdiagramm-Viewer befindet sich derzeit in der Betaphase. Seine Merkmale können sich ändern.

Ein Identitätsdiagramm ist eine Zusammenstellung der Beziehungen zwischen verschiedenen Identitäten eines bestimmten Kunden und bietet Ihnen eine visuelle Darstellung der Interaktion Ihres Kunden mit Ihrer Marke über verschiedene Kanal hinweg. Alle Kundenidentitätsdiagramme werden von Adobe Experience Platform Identity Service in Echtzeit verwaltet und aktualisiert, um die Aktivität der Kunden zu gewährleisten.

Mit dem Identitätsdiagramm-Viewer in der Benutzeroberfläche der Plattform können Sie visualisieren und besser verstehen, welche Kundenidentitäten zusammengeführt werden und auf welche Weise. Mit dem Viewer können Sie verschiedene Teile des Diagramms ziehen und mit ihnen interagieren. So können Sie komplexe Identitätsbeziehungen untersuchen, effizienter debuggen und von einer größeren Transparenz bei der Verwendung von Informationen profitieren.

## Erste Schritte

Die Arbeit mit dem Identitätsdiagramm-Viewer erfordert ein Verständnis der verschiedenen beteiligten Adobe Experience Platform-Dienste. Bevor Sie mit der Arbeit mit dem Identitätsdiagramm-Viewer beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [[!DNL Identity Service]](../home.md): Sorgt für eine bessere Darstellung einzelner Kunden und deren Verhalten, indem Identitäten zwischen Geräten und Systemen überbrückt werden.

### Terminologie

- **Identität (Knoten):** Eine Identität oder eine Node sind Daten, die für eine Entität, normalerweise eine Person, eindeutig sind. Eine Identität besteht aus einem Namensraum und einem Identitätswert.
- **Link (Kante):** Ein Link oder eine Kante stellt die Verbindung zwischen Identitäten dar.
- **Diagramm (Cluster):** Ein Diagramm oder ein Cluster ist eine Gruppe von Identitäten und Links, die eine Person repräsentieren.

## Zugriff auf den Identitätsdiagramm-Viewer

Um den Identitätsdiagramm-Viewer in der Benutzeroberfläche zu verwenden, wählen Sie im linken Navigationsbereich die Option &quot; **[!UICONTROL Identitäten]** &quot;und dann die Registerkarte &quot; **[!UICONTROL Identitätsdiagramm]** &quot;aus. Klicken Sie im Bildschirm &quot; **[!UICONTROL Identitäts-Namensraum]** &quot;auf das Symbol Identität **[!UICONTROL auswählen Namensraum]** , um nach dem Namensraum zu suchen, den Sie verwenden möchten.

![namensraum-Screen](../images/identity-graph-viewer/identity-namespace.png)

Das Bedienfeld **[!UICONTROL Identitäts-Namensraum]** auswählen wird angezeigt. Dieser Bildschirm enthält eine Liste der Namensraum, die für Ihr Unternehmen zur Verfügung stehen, einschließlich Informationen zum **[!UICONTROL Anzeigenamen]**, **[!UICONTROL Identitätssymbol]**, **[!UICONTROL Inhaber]**, **[!UICONTROL Zuletzt aktualisiert]** und **[!UICONTROL Beschreibung]** des Namensraums. Sie können einen beliebigen Namensraum verwenden, sofern ein gültiger Identitätswert mit ihm verbunden ist.

Wählen Sie den gewünschten Namensraum aus und klicken Sie auf **[!UICONTROL Auswählen]** , um fortzufahren.

![select-identity-Namensraum](../images/identity-graph-viewer/select-identity-namespace.png)

Wenn Sie einen Namensraum ausgewählt haben, geben Sie den entsprechenden Wert für einen bestimmten Kunden in das Textfeld **[!UICONTROL Identitätswert]** ein und wählen Sie **[!UICONTROL Ansicht]** aus.

![add-identity-value](../images/identity-graph-viewer/identity-value-filled.png)

Der Identitätsdiagramm-Viewer wird angezeigt. Auf der linken Seite des Bildschirms befindet sich das Identitätsdiagramm mit allen Identitäten, die mit dem ausgewählten Namensraum verknüpft sind, sowie dem eingegebenen Identitätswert. Jeder Identitätsknoten besteht aus einem Namensraum und dem zugehörigen ID-Wert. Sie können eine beliebige Identität auswählen und halten, um das Diagramm zu ziehen und mit ihm zu interagieren. Alternativ können Sie den Mauszeiger über eine Identität bewegen, um Informationen zum ID-Wert anzuzeigen. Die Diagrammausgabe wird auch als eingebrachte Liste in der Mitte des Bildschirms angezeigt.

>[!IMPORTANT]
>
>Ein Identitätsdiagramm erfordert mindestens zwei verknüpfte Identitäten sowie ein gültiges Namensraum- und ID-Paar. Die maximale Anzahl von Identitäten, die der Diagramm-Viewer anzeigen kann, beträgt 150. Weitere Informationen finden Sie im [Anhang](#appendix) .

![identity-graph](../images/identity-graph-viewer/graph-viewer.png)

Wählen Sie eine Identität aus, um die hervorgehobene Zeile in der Tabelle &quot; **[!UICONTROL Identitäten]** &quot;zu aktualisieren und die Informationen in der rechten Leiste zu aktualisieren, die den **[!UICONTROL Wert]**, die **[!UICONTROL Stapel-ID]** und das **[!UICONTROL letzte aktualisierte]** Datum einer Identität enthalten.

![select-identity](../images/identity-graph-viewer/select-identity.png)

Sie können durch ein Diagramm filtern und einen bestimmten Namensraum isolieren, indem Sie die Sortieroption über der Tabelle &quot; **[!UICONTROL Identitäten]** &quot;verwenden. Wählen Sie im Dropdownmenü den Namensraum aus, den Sie markieren möchten.

![filter-by-Namensraum](../images/identity-graph-viewer/filter-namespace.png)

Der Diagramm-Viewer gibt den ausgewählten Namensraum wieder. Mit der Filteroption wird auch die Tabelle &quot; **[!UICONTROL Identitäten]** &quot;aktualisiert, sodass nur Informationen für den ausgewählten Namensraum zurückgegeben werden.

![gefiltert](../images/identity-graph-viewer/filtered.png)

Die obere rechte Ecke des Diagrammansichtsfelds enthält Optionen zur Vergrößerung. Klicken Sie auf das Symbol **(+)** , um in das Diagramm zu zoomen, oder auf das Symbol **(-)** , um es zu verkleinern.

![zoomen](../images/identity-graph-viewer/zoom.png)

Sie können weitere Informationen zu Stapeln durch Auswahl der **[!UICONTROL Datenquelle]** in der Kopfzeile Ansicht werden. Die **[!UICONTROL Datenquellen]** -Tabelle enthält eine Liste der mit dem Diagramm verknüpften **[!UICONTROL Stapel-IDs]** sowie die zugehörigen **[!UICONTROL verknüpften IDs]**, das Quell-Schema und das Erfassungsdatum.

![data-source](../images/identity-graph-viewer/data-source-table.png)

Sie können einen der Links in einem Identitätsdiagramm auswählen, um alle Quellstapel anzuzeigen, die zu dem Link beigetragen haben.

![select-links](../images/identity-graph-viewer/select-edge.png)

Alternativ können Sie einen Stapel auswählen, um alle Links anzuzeigen, zu denen dieser Stapel beigetragen hat.

![select-links](../images/identity-graph-viewer/select-batch.png)

Identitätsdiagramme mit größeren Gruppen von Identitäten können auch über den Identitätsdiagramm-Viewer aufgerufen werden.

![Großcluster](../images/identity-graph-viewer/large-cluster.png)

## Anhang

Im folgenden Abschnitt finden Sie weitere Informationen zum Arbeiten mit dem Identitätsdiagramm-Viewer.

### Fehlermeldungen

Fehler können beim Zugriff auf den Identitätsdiagramm-Viewer auftreten. Im Folgenden finden Sie eine Liste der Voraussetzungen und Einschränkungen, die beim Arbeiten mit dem Identitätsdiagramm-Viewer zu beachten sind.

- Im ausgewählten Namensraum muss ein Identitätswert vorhanden sein.
- Für den Identitätsdiagramm-Viewer sind mindestens zwei verknüpfte Identitäten erforderlich.
- Der Identitätsdiagramm-Viewer darf nicht länger als 150 Identitäten sein.
- Der Identitätsdiagramm-Viewer ist derzeit in Nicht-Produktions-Sandboxes nicht verfügbar.
- Der Identitätsdiagramm-Viewer unterstützt derzeit nur gezählte Daten und zeigt keine Daten an, die mit Streaming-Quellen erfasst wurden.

![error-screen](../images/identity-graph-viewer/error-screen.png)

## Nächste Schritte

Durch Lesen dieses Dokuments haben Sie gelernt, wie Sie die Identitätsdiagramme Ihrer Kunden in der Plattform-Benutzeroberfläche erkunden können. Weitere Informationen zu Identitäten in der Plattform finden Sie in der Übersicht über den [Identitätsdienst](../home.md)