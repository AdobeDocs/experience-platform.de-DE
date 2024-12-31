---
title: Identitätsdiagramm-Viewer
description: Im Identitätsdiagramm werden die Beziehungen zwischen den verschiedenen Identitäten eines Kunden zusammengefasst. Dort wird visuell veranschaulicht, wie der Kunde auf unterschiedlichen Kanälen mit Ihrer Marke interagiert.
exl-id: ccd5f8d8-595b-4636-9191-553214e426bd
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 6%

---

# Identitätsdiagramm-Viewer

Im Identitätsdiagramm werden die Beziehungen zwischen den verschiedenen Identitäten eines Kunden zusammengefasst. Dort wird visuell veranschaulicht, wie der Kunde auf unterschiedlichen Kanälen mit Ihrer Marke interagiert. Alle Identitätsdiagramme werden von Adobe Experience Platform Identity Service bei Kundenaktivität nahezu in Echtzeit verwaltet und aktualisiert.

Mit dem Identitätsdiagramm-Viewer in der Platform-Benutzeroberfläche können Sie visualisieren und besser verstehen, welche Kundenidentitäten auf welche Weise miteinander verknüpft sind. Mit dem Viewer können Sie verschiedene Teile des Diagramms per Drag-and-drop verschieben und mit ihnen interagieren, sodass Sie komplexe Identitätsbeziehungen untersuchen, Fehler effizient beheben und von einer erhöhten Transparenz bei der Verwendung von Informationen profitieren können. 

Das folgende Dokument beschreibt die Schritte für den Zugriff auf und die Verwendung des Identitätsdiagramm-Viewers in der Platform-Benutzeroberfläche.

## Anleitungsvideo

Das folgende Video soll Ihnen dabei helfen, den Identitätsdiagramm-Viewer zu verstehen.

>[!VIDEO](https://video.tv.adobe.com/v/331030/?quality=12&learn=on)

## Erste Schritte

Für die Arbeit mit dem Identitätsdiagramm-Viewer sind Kenntnisse der verschiedenen betroffenen Adobe Experience Platform-Services erforderlich. Bevor Sie mit der Arbeit mit dem Identitätsdiagramm-Viewer beginnen, lesen Sie die Dokumentation für die folgenden Services:

- [[!DNL Identity Service]](../home.md): Verschaffen Sie sich einen besseren Überblick über einzelne Kunden und deren Verhalten, indem Sie Identitäten geräte- und systemübergreifend verknüpfen.
- [Echtzeit-Kundenprofil](../../profile/home.md): Identitätsdiagramme werden vom Echtzeit-Kundenprofil genutzt, um eine umfassende und einzigartige Ansicht Ihrer Kundenattribute und Verhaltensweisen zu erstellen.

### Terminologie

- **Identität (Knoten):** Eine Identität oder ein Knoten sind Daten, die für eine Entität, normalerweise eine Person, eindeutig sind. Eine Identität besteht aus einem Identity-Namespace und einem Identitätswert. Eine vollständig qualifizierte Identität kann beispielsweise aus einem Identity-Namespace für **E-Mail** in Kombination mit dem Identitätswert **robin<span>@email.com** bestehen.
- **Verknüpfung (Edge):** Eine Verknüpfung oder Kante stellt die Verbindung zwischen Identitäten dar. Identitätsverknüpfungen enthalten Eigenschaften wie die Zeitstempel der ersten Erstellung und der letzten Aktualisierung. Der zuerst eingerichtete Zeitstempel definiert das Datum und die Uhrzeit, zu der eine neue Identität mit einer vorhandenen Identität verknüpft wird. Der Zeitstempel der letzten Aktualisierung definiert das Datum und die Uhrzeit, zu der ein vorhandener Identitätslink zuletzt aktualisiert wurde.
- **Diagramm (Cluster):** Ein Diagramm oder ein Cluster ist eine Gruppe von Identitäten und Links, die eine Person darstellen.

## Zugriff auf den Identitätsdiagramm-Viewer {#access-identity-graph-viewer}

Wählen Sie in der Platform-Benutzeroberfläche **[!UICONTROL Identitäten]** im linken Navigationsbereich und anschließend **[!UICONTROL Identitätsdiagramm]** aus der Liste der Registerkarten in der Kopfzeile aus.

![Der Arbeitsbereich „Identitäten“ in der Experience Platform-Benutzeroberfläche mit ausgewählter Registerkarte „Identitätsdiagramm“.](../images/graph-viewer/identity-graph.png)

Um ein Identitätsdiagramm anzuzeigen, geben Sie einen Identity-Namespace und den entsprechenden Wert an und wählen Sie dann **[!UICONTROL Anzeigen]** aus.

>[!TIP]
>
>Wählen Sie das Tabellensymbol ![Tabellensymbol](/help/images/icons/table.png) aus, um ein Bedienfeld mit einer Liste aller in Ihrer Organisation verfügbaren Identity-Namespaces anzuzeigen. Sie können jeden der Identity-Namespaces verwenden, solange mit ihm ein gültiger Identitätswert verbunden ist. Weitere Informationen finden Sie im [Handbuch zu Identity-Namespaces](./namespaces.md).

![Ein Identity-Namespace und der entsprechende Wert, bereitgestellt im Suchbildschirm des Identitätsdiagramms.](../images/graph-viewer/namespace-and-value.png)

## Grundlegendes zur Benutzeroberfläche des Identitätsdiagramm-Viewers

Die Benutzeroberfläche des Identitätsdiagramm-Viewers besteht aus mehreren Elementen, die Sie verwenden können, um mit Ihren Identitätsdaten zu interagieren und sie besser zu verstehen.

![Die Benutzeroberfläche des Identitätsdiagramm-Viewers.](../images/graph-viewer/identity-graph-viewer-main.png)

Das Identitätsdiagramm zeigt alle Identitäten an, die mit der eingegebenen Kombination aus Identity-Namespace und Wert verknüpft sind. Jeder Knoten besteht aus einem Identity-Namespace und dem entsprechenden Wert. Sie können jeden Knoten auswählen, gedrückt halten und ziehen, um mit dem Graphen zu interagieren. Alternativ können Sie den Mauszeiger über einen Knoten bewegen, um Informationen über den entsprechenden Identitätswert anzuzeigen. Wählen Sie **[!UICONTROL Diagramm anzeigen]**, um das Diagramm auszublenden oder anzuzeigen.

>[!IMPORTANT]
>
>Ein Identitätsdiagramm erfordert die Generierung von mindestens zwei verknüpften Identitäten und eine gültige Kombination aus Identitäts-Namespace und Wert. Die maximale Anzahl von Identitäten, die der Diagramm-Viewer anzeigen kann, beträgt 50. Weitere Informationen finden Sie [ Abschnitt ](#appendix)Anhang“.

![Der Identitätsdiagramm-Viewer mit fünf verknüpften Identitäten.](../images/graph-viewer/graph.png)

Wählen Sie einen Link im Diagramm aus, um den Datensatz und die Batch-ID anzuzeigen, die zu diesem Link beitragen. Durch die Auswahl eines Links wird auch die rechte Leiste aktualisiert, um weitere Informationen zu Datenquellendetails sowie Eigenschaften wie erstmalige Erstellung und letzte Aktualisierung von Zeitstempeln bereitzustellen.

![Der Identitätslink zwischen den ausgewählten E-Mail- und GAID-Knoten.](../images/graph-viewer/identity-link.png)

Die [!UICONTROL Identitäten]-Tabelle bietet eine andere Ansicht Ihrer Identitätsdaten, in der der Identity-Namespace und die Kombination der Identitätswerte in einem tabellarischen Format aufgelistet sind. Wenn Sie einen Knoten im Diagramm auswählen, wird der hervorgehobene Zeileneintrag in der Tabelle [!UICONTROL Identitäten] aktualisiert.

![Die Identitätstabelle mit der Liste der im Diagramm verknüpften Identitäten.](../images/graph-viewer/identities-table.png)

Verwenden Sie das Dropdown-Menü, um die Diagrammdaten zu sortieren und Informationen zu einem bestimmten Identity-Namespace hervorzuheben. Wählen Sie beispielsweise **[!UICONTROL E-Mail]** aus dem Menü aus, um Daten anzuzeigen, die für den Identity-Namespace der E-Mail spezifisch sind.

![Die Identitätstabelle wird so sortiert, dass nur E-Mail-Daten angezeigt werden.](../images/graph-viewer/sort-email.png)

Die rechte Leiste zeigt Informationen zu einer ausgewählten Identität an, einschließlich des zuletzt aktualisierten Zeitstempels. In der rechten Leiste werden auch Informationen zur Datenquelle angezeigt, die der ausgewählten Identität entsprechen, darunter die Batch-ID, der Datensatzname, die Datensatz-ID und der Schemaname.

Die folgende Tabelle enthält zusätzliche Informationen zu den Datenquelleneigenschaften, die in der rechten Leiste angezeigt werden:

| Datenquelle | Beschreibung |
| --- | --- | 
| Batch-ID | Die automatisch generierte Kennung, die Ihren Batch-Daten entspricht. |
| Datensatz-ID | Die automatisch generierte Kennung, die Ihrem Datensatz entspricht. |
| Datensatzname | Der Name des Datensatzes, der Ihre Batch-Daten enthält. |
| Schemaname | Der Name des Schemas. Das Schema bietet einen Satz von Regeln, die die Struktur und das Format von Daten darstellen und validieren. |

![Die rechte Leiste, die Identitätsdaten sowie Informationen zur Datenquelle anzeigt.](../images/graph-viewer/right-rail.png)

Sie können auch die *[!UICONTROL Datenquelle“ verwenden]* um eine Liste von Datenquellen anzuzeigen, die zu Ihren Identitäten beitragen. Wählen Sie [!UICONTROL Datenquelle] aus, um eine tabellarische Ansicht Ihrer Datensätze und Batch-IDs zu erhalten.

![Die ausgewählte Registerkarte „Datenquelle“.](../images/graph-viewer/data-source-table.png)

Verwenden Sie den Schieberegler, um Diagrammdaten nach dem Zeitpunkt zu filtern, zu dem Identitäten erstmals erstellt wurden. Standardmäßig zeigt der Identitätsdiagramm-Viewer alle Identitäten an, die mit dem Diagramm verknüpft sind. Halten Sie den Schieberegler gedrückt, und ziehen Sie ihn, um den Zeitpunkt an den letzten Zeitstempel anzupassen, an dem eine neue Identität mit dem Diagramm verknüpft wurde. Im folgenden Beispiel zeigt das Diagramm an, dass der letzte Identitätslink (GAID) am **[!UICONTROL 08/19/2020, 16:29:29 Uhr eingerichtet]**.

![Der Zeitstempel-Schieberegler des Diagrammanzeigers ist ausgewählt.](../images/graph-viewer/slider-one.png)

Stellen Sie den Schieberegler ein, um zu sehen, dass am **[!UICONTROL 08/19/2020, 16:30 :25: ein weiterer Identitätslink (E-Mail) hergestellt]**.

![Der Zeitstempelregler des Diagrammanzeigers wurde auf den zuletzt eingerichteten neuen Link eingestellt.](../images/graph-viewer/slider-two.png)

Sie können den Schieberegler auch anpassen, um die früheste Iteration des Diagramms anzuzeigen. Im folgenden Beispiel zeigt der Identitätsdiagramm-Viewer an, dass das Diagramm zuerst am **[!UICONTROL 08/19/2020, 16:11:49 Uhr]** erstellt wurde, wobei die ersten Links ECID, E-Mail und Telefon sind.

![Der Zeitstempelregler des Diagrammanzeigers wurde auf den ersten eingerichteten neuen Link eingestellt.](../images/graph-viewer/slider-three.png)

## Anhang

Im folgenden Abschnitt finden Sie zusätzliche Informationen zum Arbeiten mit dem Identitätsdiagramm-Viewer.

### Fehlermeldungen verstehen

Beim Zugriff auf den Identitätsdiagramm-Viewer können Fehler auftreten. Im Folgenden finden Sie eine Liste der Voraussetzungen und Einschränkungen, die bei der Arbeit mit dem Identitätsdiagramm-Viewer zu beachten sind.

- Im ausgewählten Namespace muss ein Identitätswert vorhanden sein.
- Für den Identitätsdiagramm-Viewer sind mindestens zwei verknüpfte Identitäten zum Generieren erforderlich. Es ist möglich, dass nur ein Identitätswert und keine verknüpften Identitäten vorhanden sind. In diesem Fall würde der Wert nur [!DNL Profile] Viewer vorhanden sein.
- Der Identitätsdiagramm-Viewer darf die maximal zulässigen 50 Identitäten nicht überschreiten.

![error-screen](../images/graph-viewer/error-screen.png)

### Zugreifen auf den Identitätsdiagramm-Viewer aus Datensätzen

Sie können auch über die Oberfläche Datensätze auf den Identitätsdiagramm-Viewer zugreifen. Wählen Sie auf der Seite [!UICONTROL Durchsuchen] einen Datensatz aus, mit dem Sie interagieren möchten, und wählen Sie dann **[!UICONTROL Datensatz in der Vorschau anzeigen]**

![preview-dataset](../images/identity-graph-viewer/preview-dataset.png)

Wählen Sie im Vorschaufenster ein Fingerabdrucksymbol aus, um die Identitäten anzuzeigen, die durch den Identitätsdiagramm-Viewer dargestellt werden.

>[!TIP]
>
>Das Fingerabdruck-Symbol wird nur angezeigt, wenn der Datensatz zwei oder mehr Identitäten aufweist.

![Fingerabdruck](../images/identity-graph-viewer/fingerprint.png)

## Nächste Schritte

Durch das Lesen dieses Dokuments haben Sie gelernt, wie Sie die Identitätsdiagramme Ihrer Kunden in der Platform-Benutzeroberfläche untersuchen können. Weiterführende Informationen zu Identitäten in Platform finden Sie in der [Identity Service - Übersicht](../home.md)

## Änderungsprotokoll

| Datum | Aktion |
| ---- | ------ |
| 2021-01 | <ul><li>Es wurde Unterstützung für das Streaming aufgenommener Daten und Nicht-Produktions-Sandboxes hinzugefügt.</li><li>Geringfügige Fehlerbehebungen.</li></ul> |
| 2021-02 | <ul><li>Der Zugriff auf den Identitätsdiagramm-Viewer wird über die Datensatzvorschau ermöglicht.</li><li>Geringfügige Fehlerbehebungen.</li><li>Der Identitätsdiagramm-Viewer wird allgemein verfügbar gemacht.</li></ul> |
| 2023-01 | <ul><li>Aktualisierungen der Benutzeroberfläche.</li></ul> |
