---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Überwachen von Konten und Datenflüssen
topic: overview
translation-type: tm+mt
source-git-commit: fc0a406bdea7b31e046d02427805a9deba557e93
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 1%

---


# Überwachen von Konten und Datenflüssen

Source Connectors in Adobe Experience Platform bieten die Möglichkeit, Daten aus externen Quellen planmäßig zu erfassen. Dieses Lernprogramm enthält Schritte zum Anzeigen vorhandener Konten und Datenflüsse aus dem *Quellarbeitsbereich* .

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

- [Erlebnis-Datenmodell (XDM)-System](../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   - [Grundlagen der Zusammensetzung](../../../xdm/schema/composition.md)des Schemas: Erfahren Sie mehr über die grundlegenden Bausteine von XDM-Schemas, einschließlich der wichtigsten Grundsätze und Best Practices bei der Schema-Komposition.
   - [Schema-Editor-Lernprogramm](../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
- [Echtzeit-Profil](../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

## Konten überwachen

Melden Sie sich bei <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> an und wählen Sie dann in der linken Navigationsleiste die Option &quot; **Quellen** &quot;, um auf den *Quellenarbeitsbereich* zuzugreifen. Im Anzeigebereich &quot; *Katalog* &quot;werden verschiedene Quellen angezeigt, mit denen Sie Konten-Dataset-Datenflüsse erstellen können. Jede Quelle zeigt die Anzahl der vorhandenen Konten und Datenflüsse, die ihnen zugeordnet sind.

Wählen Sie *Konten* aus der oberen Kopfzeile zur Ansicht vorhandener Konten.

![Katalog](../../images/tutorials/monitor/catalog.png)

Die Seiten *Konten* werden angezeigt. Auf dieser Seite finden Sie eine Liste von anzeigbaren Konten, einschließlich Informationen zu Quelle, Benutzername, Anzahl der Datenströme und Erstellungsdatum.

Klicken Sie auf das Symbol oben links, um das Sortierfenster zu starten.

![Konten](../../images/tutorials/monitor/accounts-list.png)

Über das Sortierfeld können Sie auf Konten aus einer bestimmten Quelle zugreifen. Wählen Sie die Quelle aus, mit der Sie arbeiten möchten, und wählen Sie das Konto in der Liste auf der rechten Seite aus.

![accounts-select](../../images/tutorials/monitor/accounts-sort.png)

Auf der Seite &quot; *Konten* &quot;können Sie eine Liste der vorhandenen Datenflüsse, die mit dem Konto, auf das Sie zugegriffen haben, verknüpft sind, Ansicht haben. Wählen Sie den zu Ansicht Datenfluss aus.

![accounts-page](../../images/tutorials/monitor/dataset-flows.png)

Der Bildschirm &quot;Aktivität *des* Datenflusses&quot;wird angezeigt. Diese Seite zeigt die Rate der Nachrichten an, die in Form eines Diagramms konsumiert werden.

![dataset-flow-Aktivität](../../images/tutorials/monitor/dataset-flows-activity.png)

## Überwachen von Datenflüssen

Auf Datenfluss kann direkt von der Seite &quot; *Katalog* &quot;aus zugegriffen werden, ohne *Konten* anzuzeigen. Wählen Sie &quot; *Datenfluss* von der obersten Kopfzeile zur Ansicht einer Liste der vorhandenen Datenströme&quot;.

![dataset-flows](../../images/tutorials/monitor/dataset-flows-list.png)

Ähnlich wie bei Konten können Sie die Liste der Datenströme mit dem Sortiersymbol oben links sortieren. Wählen Sie die zu Ansicht Quelle aus und wählen Sie den Datenfluss aus der Liste auf der rechten Seite aus.

![select-dataset-flows](../../images/tutorials/monitor/dataset-flows-sort.png)

Der Bildschirm &quot;Aktivität *des* Datenflusses&quot;wird angezeigt. Diese Seite zeigt die Rate der Nachrichten an, die in Form eines Diagramms konsumiert werden.

![dataset-flow-Aktivität](../../images/tutorials/monitor/dataset-flows-activity.png)

Weitere Informationen zur Überwachung von Datensätzen und zur Erfassung finden Sie im Lernprogramm zur [Überwachung von Streaming-Datenflüssen](../../../ingestion/quality/monitor-data-flows.md).

## Nächste Schritte

In diesem Lernprogramm haben Sie erfolgreich auf vorhandene Konten und Datenströme aus dem *Sources* -Arbeitsbereich zugegriffen. Eingehende Daten können jetzt von nachgeschalteten Plattformdiensten wie Real-time Customer Profil und Data Science Workspace verwendet werden. Weitere Informationen finden Sie in den folgenden Dokumenten:

- [Übersicht über das Echtzeit-Kundenprofil](../../../profile/home.md)
- [Übersicht über den Data Science Workspace](../../../data-science-workspace/home.md)