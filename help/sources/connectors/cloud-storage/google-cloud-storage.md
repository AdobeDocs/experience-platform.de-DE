---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Google Cloud-Datenspeicherung-Connector
topic: overview
translation-type: tm+mt
source-git-commit: 256a193e56e69078d1c01c622656f0b1a18e73ff
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---


# Google Cloud-Datenspeicherung-Connector

Adobe Experience Platform bietet native Konnektivität für Cloud-Anbieter wie AWS, Google Cloud Platform und Azurblase. Sie können Ihre Daten aus diesen Systemen in Plattform übertragen.

Cloud-Datenspeicherung-Quellen können Ihre eigenen Daten in die Plattform übertragen, ohne dass Sie sie herunterladen, formatieren oder hochladen müssen. Ingetierte Daten können als XDM-JSON-, XDM-Parkett oder als Trennzeichen formatiert werden. Jeder Schritt des Prozesses ist in den Sources-Workflow integriert. Mit der Plattform können Sie Daten aus der Google Cloud-Datenspeicherung in Batches importieren.

## Voraussetzungen für die Einrichtung des Kontos für die Google Cloud-Datenspeicherung

Um eine Verbindung zur Plattform herzustellen, müssen Sie zunächst die Interoperabilität für Ihr Google Cloud-Datenspeicherung-Konto aktivieren. Um auf die Interoperabilitätseinstellung zuzugreifen, öffnen Sie die Google Cloud-Plattform und wählen Sie **[!UICONTROL Einstellungen]** aus der Option &quot; **[!UICONTROL Datenspeicherung]** &quot;im Navigationsbereich.

![](../../images/tutorials/create/google-cloud-storage/nav.png)

Die Seite **[!UICONTROL Einstellungen]** wird angezeigt. Von hier aus können Sie Informationen zu Ihrer Google-Projekt-ID und Details zu Ihrem Google Cloud-Datenspeicherung-Konto sehen. Um auf die Interoperabilitätseinstellungen zuzugreifen, wählen Sie in der oberen Kopfzeile die Option &quot; **[!UICONTROL Interoperabilität]** &quot;aus.

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

Die Seite &quot; **[!UICONTROL Interoperabilität]** &quot;enthält Informationen zur Authentifizierung, zu Zugriffsschlüsseln und zum Standardprojekt, das mit Ihrem Benutzerkonto verknüpft ist. Wenn Sie noch kein Standardprojekt für den interoperablen Zugriff eingerichtet haben, können Sie eines im Abschnitt *[!UICONTROL &quot;Standard&quot;für den interoperablen Zugriff]* einrichten. Wenn bereits ein Standardprojekt eingerichtet wurde, wird im Abschnitt eine Bestätigung angezeigt, dass ein Projekt als Standard festgelegt wurde.

Um eine neue Zugriffsschlüssel-ID und einen geheimen Zugriffsschlüssel für Ihr Benutzerkonto zu erstellen, wählen Sie &quot;Schlüssel **[!UICONTROL erstellen&quot;]**.

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

Sie können Ihre neu generierte Zugriffsschlüssel-ID und Ihren geheimen Zugriffsschlüssel verwenden, um Ihr Google Cloud-Datenspeicherung-Konto mit Platform zu verbinden.

Die nachstehende Dokumentation enthält Informationen dazu, wie die Verbindung der Google Cloud-Datenspeicherung mit der Plattform mithilfe von APIs oder der Benutzeroberfläche hergestellt wird:

## Google Cloud-Datenspeicherung mit Plattform verbinden

Die nachstehende Dokumentation enthält Informationen dazu, wie die Verbindung der Google Cloud-Datenspeicherung mit der Plattform mithilfe von APIs oder der Benutzeroberfläche hergestellt wird:

### APIs verwenden

- [Erstellen eines Google Cloud-Datenspeicherung-Connectors mithilfe der Flow Service API](../../tutorials/api/create/cloud-storage/google.md)
- [Kennenlernen eines Cloud-Datenspeicherung-Systems mithilfe der Flow Service API](../../tutorials/api/explore/cloud-storage.md)
- [Erfassen von Cloud-Datenspeicherung-Daten mithilfe der Flow Service API](../../tutorials/api/collect/cloud-storage.md)

### Verwenden der Benutzeroberfläche

- [Erstellen eines Google Cloud-Datenspeicherung-Quellconnectors in der Benutzeroberfläche](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Konfigurieren eines Datenflusses für einen Cloud-Datenspeicherung-Connector in der Benutzeroberfläche](../../tutorials/ui/dataflow/batch/cloud-storage.md)