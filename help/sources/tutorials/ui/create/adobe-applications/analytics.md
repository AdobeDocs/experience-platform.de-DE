---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Adobe Analytics-Quellconnectors in der Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 3%

---


# Erstellen eines Adobe Analytics-Quellconnectors in der Benutzeroberfläche

In diesem Lernprogramm wird beschrieben, wie Sie einen Adobe Analytics-Quellanschluss in der Benutzeroberfläche erstellen, um Verbraucherdaten in die Adobe Experience Platform zu bringen.

## Erste Schritte

Dieses Lernprogramm erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

* [Erlebnis-Datenmodell (XDM)-System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
* [Echtzeit-Profil](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxen, die eine Instanz einer Platform in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

## Erstellen einer Quellverbindung mit Adobe Analytics

Melden Sie sich bei <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> an und wählen Sie dann in der linken Navigationsleiste **[!UICONTROL Quellen]** , um auf den Quellarbeitsbereich zuzugreifen. Im Anzeigebereich &quot; *Katalog* &quot;werden verfügbare Quellen zum Erstellen von eingehenden Verbindungen angezeigt. Jede Quelle zeigt die Anzahl der vorhandenen Konten und Datenströme, die ihnen zugeordnet sind.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle mit der Suchoption finden.

Wählen Sie unter der Kategorie &quot; *Adobe-Anwendungen* &quot;die Option &quot; **[!UICONTROL Adobe Analytics]** &quot;, um eine Informationsleiste auf der rechten Seite des Bildschirms anzuzeigen. Die Informationsleiste enthält eine kurze Beschreibung der ausgewählten Quelle sowie Optionen zum Herstellen einer Verbindung zur Quelle oder Ansicht der zugehörigen Dokumentation. Um vorhandene Konten Ansicht, wählen Sie **[!UICONTROL Konten]**.

![](../../../../images/tutorials/create/analytics/catalog.png)

### Daten auswählen

Der *Adobe Analytics* -Schritt wird angezeigt. In diesem Anzeigebereich werden zuvor eingerichtete Datenflüsse für Analytics aufgeführt. Sie können einen neuen Datenfluss erstellen, indem Sie auf Daten **[!UICONTROL auswählen]** klicken.

>[!NOTE]
>
>Es können mehrere eingehende Verbindungen zu einer Quelle hergestellt werden, um verschiedene Daten einzubringen.

![](../../../../images/tutorials/create/analytics/dataset-flows.png)

<!---Analytics report suites can be configured for one sandbox at a time. To import the same report suite into a different sandbox, the dataset flow will have to be deleted and instantiated again via configuration for a different sandbox.--->

Wählen Sie in der Liste der verfügbaren Report Suites die Report Suites aus, die Sie in die Platform aufnehmen möchten, und klicken Sie auf **[!UICONTROL Weiter]**.

![](../../../../images/tutorials/create/analytics/select-data.png)

### Benennen des Datenflusses

Der Schritt *Datenfluss* im Detail wird angezeigt, in dem Sie einen Namen und eine optionale Beschreibung für den Datenfluss angeben müssen. Wählen Sie **[UICONTROL! Als Nächstes]** fertig.

![](../../../../images/tutorials/create/analytics/dataset-flow-detail.png)

### Überprüfen des Datenflusses

Der *Überprüfungsschritt* wird angezeigt, mit dem Sie den neuen Analytics-Datenfluss vor der Erstellung überprüfen können. Die Verbindungsdetails werden nach Kategorien gruppiert, darunter:

* *Verbindung*: Zeigt den Typ der Quellverbindung und die ausgewählte Report Suite an.
* *Zuweisen von Dataset- und Zuordnungsfeldern*: Beim Erstellen anderer Quell-Connectors zeigt dieser Container, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, das der Datensatz einhält. Das Output-Schema und der DataSet werden automatisch für Analytics-Dataset-Datenströme konfiguriert.

![](../../../../images/tutorials/create/analytics/review.png)

### Überwachen des Datenflusses

Nachdem Sie den Datenfluss erstellt haben, können Sie die Daten überwachen, die über den Dataset aufgenommen werden. Wählen Sie im *Anzeigebereich &quot;Katalog* &quot;die Option &quot; *Dataset-Fluss* zur Ansicht einer Liste der mit Ihrem Analytics-Konto verknüpften etablierten Datenströme&quot;.

![](../../../../images/tutorials/create/analytics/catalog-dataset-flows.png)

Der Bildschirm &quot; *Datenfluss* &quot;wird angezeigt. Auf dieser Seite finden Sie eine Reihe von Datenströmen, einschließlich Informationen zu ihrem Namen, ihren Quelldaten, ihrer Erstellungszeit und ihrem Status.

Der Connector instanziiert zwei Datenströme. Ein Fluss stellt Aufstockungsdaten dar, der andere für Live-Daten. Aufstockungsdaten werden nicht zum Profil konfiguriert, sondern für analytische und datenwissenschaftliche Anwendungsfälle an den Datensee gesendet.

Weitere Informationen zur Aufstockung, zu Live-Daten und ihren jeweiligen Latenzen finden Sie in der [Analytics Data Connector-Übersicht](../../../../connectors/adobe-applications/analytics.md).

Wählen Sie aus der Liste den Datenfluss aus, der Ansicht werden soll.

![](../../../../images/tutorials/create/analytics/backfill.png)

Die Seite *Aktivität* des Datensatzes wird angezeigt. Diese Seite zeigt die Rate der Nachrichten an, die in Form eines Diagramms konsumiert werden. Wählen Sie *Datenverwaltung* in der oberen Kopfzeile, um auf die Beschriftungsfelder zuzugreifen.

![](../../../../images/tutorials/create/analytics/batches.png)

Sie können die geerbten Beschriftungen eines Dataset-Flusses im Anzeigebereich &quot; *Datenverwaltung* &quot;Ansicht werden. Um auf bestimmte Beschriftungen zuzugreifen, klicken Sie oben rechts auf die Schaltfläche &quot;Bearbeiten&quot;.

![](../../../../images/tutorials/create/analytics/data-gov.png)

Das Bedienfeld *Governance-Bezeichnungen* bearbeiten wird angezeigt. In diesem Anzeigebereich können Sie auf die Verträge, Identitäten und vertraulichen Beschriftungen eines Datasets zugreifen und diese bearbeiten.

Weitere Informationen zur Beschriftung von Daten aus Analytics finden Sie im Handbuch [zur Datenverwendung](../../../../../data-governance/labels/user-guide.md).

![](../../../../images/tutorials/create/analytics/labels.png)

## Nächste Schritte

Nachdem die Verbindung erstellt wurde, wird automatisch ein Zielgruppe-Schema und ein Datenfluss erstellt, der die eingehenden Daten enthält. Darüber hinaus werden bis zu 13 Monate historischer Daten aufgefüllt und erfasst. Nach Abschluss der anfänglichen Erfassung werden Analytics-Daten verwendet und von Diensten der nachgeschalteten Platform wie dem Echtzeit-Kundendienst und dem Segmentierungsdienst verwendet. Weitere Informationen finden Sie in den folgenden Dokumenten:

* [Übersicht über das Echtzeit-Kundenprofil](../../../../../profile/home.md)
* [Übersicht über den Segmentierungsdienst](../../../../../segmentation/home.md)
* [Übersicht über den Data Science Workspace](../../../../../data-science-workspace/home.md)
* [Übersicht über den Abfrage Service](../../../../../query-service/home.md)
