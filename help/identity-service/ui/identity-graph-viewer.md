---
keywords: Experience Platform; Startseite; beliebte Themen; Identitätsdiagramm-Viewer; Identitätsdiagramm-Viewer; Diagramm-Viewer; Graph-Viewer; Identitäts-Namespace; Identität; Identität; Identity Service; Identitätsdienst
solution: Experience Platform
title: Identitätsdiagramm-Viewer - Übersicht
description: Ein Identitätsdiagramm ist eine Zusammenstellung der Beziehungen zwischen verschiedenen Identitäten für einen bestimmten Kunden und bietet Ihnen eine visuelle Darstellung, wie Ihr Kunde über verschiedene Kanäle hinweg mit Ihrer Marke interagiert.
exl-id: ccd5f8d8-595b-4636-9191-553214e426bd
source-git-commit: 25f1b2197e5b10b04668d16bff3a6ce48cfad5fc
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 9%

---

# Übersicht über den Identitätsdiagramm-Viewer

Ein Identitätsdiagramm ist eine Zusammenstellung der Beziehungen zwischen verschiedenen Identitäten für einen bestimmten Kunden und bietet Ihnen eine visuelle Darstellung, wie Ihr Kunde über verschiedene Kanäle hinweg mit Ihrer Marke interagiert. Alle Identitätsdiagramme werden von Adobe Experience Platform Identity Service bei Kundenaktivität nahezu in Echtzeit verwaltet und aktualisiert.

Mit dem Identitätsdiagramm-Viewer in der Benutzeroberfläche von Platform können Sie visualisieren und besser verstehen, welche Kundenidentitäten zusammengeführt werden und auf welche Weise. Mit dem Viewer können Sie verschiedene Teile des Diagramms per Drag-and-drop verschieben und mit ihnen interagieren, sodass Sie komplexe Identitätsbeziehungen untersuchen, Fehler effizient beheben und von einer erhöhten Transparenz bei der Verwendung von Informationen profitieren können. 

## Anleitungsvideo

Das folgende Video soll Ihr Verständnis des Identitätsdiagramm-Viewers unterstützen.

>[!VIDEO](https://video.tv.adobe.com/v/331030/?quality=12&learn=on)

## Erste Schritte

Die Arbeit mit dem Identitätsdiagramm-Viewer erfordert ein Verständnis der verschiedenen beteiligten Adobe Experience Platform-Dienste. Bevor Sie mit dem Identitätsdiagramm-Viewer arbeiten, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [[!DNL Identity Service]](../home.md): Verschaffen Sie sich einen besseren Überblick über einzelne Kunden und deren Verhalten, indem Sie Identitäten geräte- und systemübergreifend verknüpfen.

### Terminologie

- **Identität (Knoten):** Eine Identität oder ein Knoten sind Daten, die für eine Entität, normalerweise eine Person, eindeutig sind. Eine Identität besteht aus einem Namespace und einem Identitätswert.
- **Verknüpfung (Kante):** Ein Link oder ein Edge stellt die Verbindung zwischen Identitäten dar.
- **Diagramm (Cluster):** Ein Diagramm oder ein Cluster ist eine Gruppe von Identitäten und Links, die eine Person repräsentieren.

## Zugriff auf den Identitätsdiagramm-Viewer {#access-identity-graph-viewer}

Um den Identitätsdiagramm-Viewer in der Benutzeroberfläche zu verwenden, wählen Sie **[!UICONTROL Identitäten]** in der linken Navigation und wählen Sie dann die **[!UICONTROL Identitätsdiagramm]** Registerkarte. Aus dem **[!UICONTROL Identitäts-Namespace]** auf das **[!UICONTROL Identitäts-Namespace auswählen]** -Symbol, um nach dem Namespace zu suchen, den Sie verwenden möchten.

![namespace-screen](../images/identity-graph-viewer/identity-namespace.png)

Die **[!UICONTROL Identitäts-Namespace auswählen]** angezeigt. Dieser Bildschirm enthält eine Liste der für Ihr Unternehmen verfügbaren Namespaces, einschließlich Informationen zu den **[!UICONTROL Anzeigename]**, **[!UICONTROL Identitätssymbol]**, **[!UICONTROL Inhaber]**, **[!UICONTROL Letzte Aktualisierung]** Datum und **[!UICONTROL Beschreibung]**. Sie können einen beliebigen der bereitgestellten Namespaces verwenden, sofern ein gültiger Identitätswert mit ihm verbunden ist.

Wählen Sie den zu verwendenden Namespace aus und klicken Sie auf **[!UICONTROL Auswählen]** um fortzufahren.

![select-identity-namespace](../images/identity-graph-viewer/select-identity-namespace.png)

Nachdem Sie einen Namespace ausgewählt haben, geben Sie den entsprechenden Wert für einen bestimmten Kunden in die **[!UICONTROL Identitätswert]** Textfeld und wählen Sie **[!UICONTROL Ansicht]**.

![add-identity-value](../images/identity-graph-viewer/identity-value-filled.png)

### Zugriff auf den Identitätsdiagramm-Viewer aus Datensätzen

Sie können auch über die Oberfläche für Datensätze auf den Viewer für Identitätsdiagramme zugreifen. Aus den Datensätzen [!UICONTROL Durchsuchen] , wählen Sie einen Datensatz aus, mit dem Sie interagieren möchten, und klicken Sie auf **[!UICONTROL Vorschau des Datensatzes anzeigen]**

![preview-dataset](../images/identity-graph-viewer/preview-dataset.png)

Wählen Sie im Vorschaufenster ein Fingerabdrucksymbol aus, um die Identitäten anzuzeigen, die durch den Identitätsdiagramm-Viewer dargestellt werden.

>[!TIP]
>
>Das Symbol &quot;Fingerabdruck&quot;wird nur angezeigt, wenn der Datensatz zwei oder mehr Identitäten aufweist.

![Fingerabdruck](../images/identity-graph-viewer/fingerprint.png)

Der Identitätsdiagramm-Viewer wird angezeigt. Auf der linken Seite des Bildschirms befindet sich das Identitätsdiagramm, das alle Identitäten anzeigt, die mit dem ausgewählten Namespace verknüpft sind, sowie den eingegebenen Identitätswert. Jeder Identitätsknoten besteht aus einem Namespace und dem zugehörigen ID-Wert. Sie können eine beliebige Identität auswählen und speichern, um sie per Drag-and-Interaktion mit dem Diagramm zu verwenden. Alternativ können Sie den Mauszeiger über eine Identität bewegen, um Informationen zum ID-Wert anzuzeigen. Die Diagrammausgabe wird auch als eingereichte Liste in der Mitte des Bildschirms angezeigt.

>[!IMPORTANT]
>
>Für ein Identitätsdiagramm müssen mindestens zwei verknüpfte Identitäten generiert werden, sowie ein gültiges Namespace- und ID-Paar. Die maximale Anzahl von Identitäten, die der Diagramm-Viewer anzeigen kann, beträgt 150. Siehe [Anhang](#appendix) unten für weitere Informationen.

![identity-graph](../images/identity-graph-viewer/graph-viewer.png)

Wählen Sie eine Identität aus, um die markierte Zeile auf der **[!UICONTROL Identitäten]** und die in der rechten Leiste bereitgestellten Informationen zu aktualisieren, einschließlich der **[!UICONTROL Wert]**, **[!UICONTROL Batch-Kennung]** und **[!UICONTROL Letzte Aktualisierung]** Datum.

![select-identity](../images/identity-graph-viewer/select-identity.png)

Sie können durch ein Diagramm filtern und einen bestimmten Namespace mithilfe der Sortieroption oben im **[!UICONTROL Identitäten]** Tabelle. Wählen Sie im Dropdown-Menü den Namespace aus, den Sie hervorheben möchten.

![filter-by-namespace](../images/identity-graph-viewer/filter-namespace.png)

Der Diagramm-Viewer gibt zurück und hebt den ausgewählten Namespace hervor. Die Filteroption aktualisiert auch die **[!UICONTROL Identitäten]** -Tabelle, um nur Informationen für den ausgewählten Namespace zurückzugeben.

![filtern](../images/identity-graph-viewer/filtered.png)

Oben rechts im Viewer-Feld für Diagramme enthält Optionen zur Vergrößerung. Wählen Sie die **(+)** -Symbol, um in das Diagramm oder die **(-)** zum Verkleinern.

![Zoom](../images/identity-graph-viewer/zoom.png)

Sie können weitere Informationen zu Batches anzeigen, indem Sie die **[!UICONTROL Datenquelle]** aus der Kopfzeile. Die **[!UICONTROL Datenquelle]** zeigt eine Liste von **[!UICONTROL Batch-IDs]** mit dem Diagramm sowie dessen **[!UICONTROL Verknüpfte IDs]**, Quellschema und Datum der Aufnahme.

![data-source](../images/identity-graph-viewer/data-source-table.png)

Sie können einen beliebigen Link in einem Identitätsdiagramm auswählen, um alle Quell-Batches anzuzeigen, die zum Link beigetragen haben.

![select-links](../images/identity-graph-viewer/select-edge.png)

Alternativ können Sie einen Batch auswählen, um alle Links anzuzeigen, zu denen dieser Batch beigetragen hat.

![select-links](../images/identity-graph-viewer/select-batch.png)

Identitätsdiagramme mit größeren Identitätsclustern sind auch über den Identitätsdiagramm-Viewer verfügbar.

![Großcluster](../images/identity-graph-viewer/large-cluster.png)

## Anhang

Im folgenden Abschnitt finden Sie zusätzliche Informationen zum Arbeiten mit dem Identitätsdiagramm-Viewer.

### Grundlagen zu Fehlermeldungen

Beim Zugriff auf den Identitätsdiagramm-Viewer können Fehler auftreten. Im Folgenden finden Sie eine Liste von Voraussetzungen und Einschränkungen, die bei der Arbeit mit dem Identitätsdiagramm-Viewer zu beachten sind.

- Im ausgewählten Namespace muss ein Identitätswert vorhanden sein.
- Der Identitätsdiagramm-Viewer erfordert mindestens zwei verknüpfte Identitäten, die generiert werden müssen. Es ist möglich, dass es nur einen Identitätswert und keine verknüpften Identitäten gibt. In diesem Fall würde der Wert nur in [!DNL Profile] Viewer.
- Der Identitätsdiagramm-Viewer darf die maximal 150 Identitäten nicht überschreiten.

![error-screen](../images/identity-graph-viewer/error-screen.png)

## Nächste Schritte

Durch Lesen dieses Dokuments haben Sie erfahren, wie Sie die Identitätsdiagramme Ihrer Kunden in der Platform-Benutzeroberfläche untersuchen. Weiterführende Informationen zu Identitäten in Platform finden Sie im Abschnitt [Identity Service - Übersicht](../home.md)

## Änderungsprotokoll

| Datum | Aktion |
| ---- | ------ |
| 2021-01 | <ul><li>Unterstützung für Streaming von erfassten Daten und Nicht-Produktions-Sandbox hinzugefügt.</li><li>Geringfügige Fehlerbehebungen.</li></ul> |
| 2021-02 | <ul><li>Der Identitätsdiagramm-Viewer wird über die Datensatzvorschau verfügbar gemacht.</li><li>Geringfügige Fehlerbehebungen.</li><li>Der Identitätsdiagramm-Viewer wird allgemein verfügbar gemacht.</li></ul> |
