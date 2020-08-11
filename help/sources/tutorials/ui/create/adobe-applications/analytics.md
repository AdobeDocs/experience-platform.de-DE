---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Quell-Connectors für Adobe Analytics über die Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: 41fe3e5b2a830c3182b46b3e0873b1672a1f1b03
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 15%

---


# Erstellen eines Quell-Connectors für Adobe Analytics über die Benutzeroberfläche

This tutorial provides steps for creating an Adobe Analytics source connector in the UI to bring consumer data into Adobe Experience Platform.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Experience-Datenmodell (XDM)-System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
* [Echtzeit-Kundenprofil](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

## Create a source connection with Adobe Analytics

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann in der linken Navigationsleiste die Option &quot; **[!UICONTROL Quellen]** &quot;, um auf den Quellarbeitsbereich zuzugreifen. Im Anzeigebereich &quot; *Katalog* &quot;werden verfügbare Quellen zum Erstellen von eingehenden Verbindungen angezeigt. Jede Quelle zeigt die Anzahl der vorhandenen Konten und Datenströme, die ihnen zugeordnet sind.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle mit der Suchoption finden.

Wählen Sie unter der Kategorie *Adobe Applications* die Option **[!UICONTROL Adobe Analytics]** , um eine Informationsleiste auf der rechten Seite Ihres Bildschirms anzuzeigen. Die Informationsleiste enthält eine kurze Beschreibung der ausgewählten Quelle sowie Optionen zum Herstellen einer Verbindung zur Quelle oder Ansicht der zugehörigen Dokumentation. Um vorhandene Konten Ansicht, wählen Sie **[!UICONTROL Konten]**.

![](../../../../images/tutorials/create/analytics/catalog.png)

### Daten auswählen

Der *Adobe Analytics* -Schritt wird angezeigt. In diesem Anzeigebereich werden zuvor eingerichtete Datenflüsse für Analytics aufgeführt. Sie können einen neuen Datenfluss erstellen, indem Sie auf Daten **[!UICONTROL auswählen]** klicken.

>[!NOTE]
>
>Es können mehrere eingehende Verbindungen zu einer Quelle hergestellt werden, um verschiedene Daten einzubringen.

![](../../../../images/tutorials/create/analytics/dataset-flows.png)

<!---Analytics report suites can be configured for one sandbox at a time. To import the same report suite into a different sandbox, the dataset flow will have to be deleted and instantiated again via configuration for a different sandbox.--->

Wählen Sie in der Liste der verfügbaren Report Suites die Report Suites aus, die Sie in die Plattform aufnehmen möchten, und klicken Sie auf **[!UICONTROL Weiter]**.

![](../../../../images/tutorials/create/analytics/select-data.png)

### Benennen des Datenflusses

Der Schritt *Datenfluss* im Detail wird angezeigt, in dem Sie einen Namen und eine optionale Beschreibung für den Datenfluss angeben müssen. Wählen Sie **[UICONTROL! Als Nächstes]** fertig.

![](../../../../images/tutorials/create/analytics/dataset-flow-detail.png)

### Überprüfen des Datenflusses

Der *Review* -Schritt wird angezeigt, mit dem Sie Ihren neuen Analytics-In-bound-Datenfluss überprüfen können, bevor er erstellt wird. Die Verbindungsdetails werden nach Kategorien gruppiert, darunter:

* *Verbindung*: Zeigt den Typ der Quellverbindung und die ausgewählte Report Suite an.
* *Assign dataset &amp; map fields*: When creating other source connectors, this container shows which dataset the source data is ingesting into, including the schema the dataset adheres to. Das Schema und der Datensatz für die Ausgabe werden automatisch für Analytics-Dataset-Datenflüsse konfiguriert.

![](../../../../images/tutorials/create/analytics/review.png)

### Überwachen des Datenflusses

Nachdem Sie den Datenfluss erstellt haben, können Sie die Daten überwachen, die über den Dataset aufgenommen werden. From the *Catalog* screen, select *Dataset flows* to view a list of established flows associated with your Analytics account.

![](../../../../images/tutorials/create/analytics/catalog-dataset-flows.png)

The *Dataset flows* screen appears. Auf dieser Seite finden Sie eine Reihe von Datenströmen, einschließlich Informationen zu ihrem Namen, ihren Quelldaten, ihrer Erstellungszeit und ihrem Status.

Der Connector instanziiert zwei Datenströme. Ein Fluss stellt Aufstockungsdaten dar, der andere für Live-Daten. Aufstockungsdaten werden nicht zum Profil konfiguriert, sondern für analytische und datenwissenschaftliche Anwendungsfälle an den Datensee gesendet.

For more information on backfill, live data, and their respective latencies, see the [Analytics Data Connector overview](../../../../connectors/adobe-applications/analytics.md).

Select the dataset flow you wish to view from the list.

![](../../../../images/tutorials/create/analytics/backfill.png)

Die Seite *Aktivität* des Datensatzes wird angezeigt. This page displays the rate of messages being consumed in the form of a graph. Wählen Sie *Datenverwaltung* in der oberen Kopfzeile, um auf die Beschriftungsfelder zuzugreifen.

![](../../../../images/tutorials/create/analytics/batches.png)

Sie können die geerbten Beschriftungen eines Dataset-Flusses im Anzeigebereich &quot; *Datenverwaltung* &quot;Ansicht werden. Um auf bestimmte Beschriftungen zuzugreifen, klicken Sie oben rechts auf die Schaltfläche &quot;Bearbeiten&quot;.

![](../../../../images/tutorials/create/analytics/data-gov.png)

The *Edit governance labels* panel appears. This screen allows you to access and edit a dataset flow&#39;s contract, identity, and sensitive labels.

For more information on how to label data coming from Analytics, visit the [data usage labels guide](../../../../../data-governance/labels/user-guide.md).

![](../../../../images/tutorials/create/analytics/labels.png)

## Nächste Schritte und zusätzliche Ressourcen

Nachdem die Verbindung erstellt wurde, wird automatisch ein Zielgruppe-Schema und ein Datenfluss erstellt, der die eingehenden Daten enthält. Darüber hinaus werden bis zu 13 Monate historischer Daten aufgefüllt und erfasst. Nach Abschluss der anfänglichen Erfassung werden Analytics-Daten verwendet und von nachgeschalteten Plattformdiensten wie dem Echtzeit-Kundendienst und dem Segmentierungsdienst verwendet. Weitere Informationen finden Sie in den folgenden Dokumenten:

* [Übersicht über das Echtzeit-Kundenprofil](../../../../../profile/home.md)
* [Übersicht über den Segmentierungsdienst](../../../../../segmentation/home.md)
* [Übersicht über den Data Science Workspace](../../../../../data-science-workspace/home.md)
* [Query Service – Übersicht](../../../../../query-service/home.md)

The following video is intended to support your understanding of ingesting data using the Adobe Analytics Source connector:

>[!WARNING]
>
> Die im folgenden Video dargestellte [!DNL Platform] Benutzeroberfläche ist veraltet. Die neuesten Screenshots und Funktionen der Benutzeroberfläche finden Sie in der obigen Dokumentation.

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)

