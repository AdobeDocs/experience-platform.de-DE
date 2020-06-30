---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Google Cloud-Datenspeicherung-Connector
topic: overview
translation-type: tm+mt
source-git-commit: 6ffdcc2143914e2ab41843a52dc92344ad51bcfb
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---


# Google Cloud-Datenspeicherung-Connector

Adobe Experience Platform bietet native Konnektivität für Cloud-Anbieter wie AWS [!DNL Google Cloud Platform]und [!DNL Azure]ermöglicht es Ihnen, Ihre Daten von diesen Systemen zu übertragen.

Cloud-Datenspeicherung-Quellen können Ihre eigenen Daten in [!DNL Platform] ohne Download, Format oder Upload übertragen. Ingetierte Daten können als XDM-JSON-, XDM-Parkett oder als Trennzeichen formatiert werden. Jeder Schritt des Prozesses ist in den Sources-Workflow integriert. [!DNL Platform] ermöglicht Ihnen, Daten aus [!DNL Google Cloud Storage] Stapeln einzubringen.

## Voraussetzungen für die Verbindung mit Ihrem [!DNL Google Cloud Storage] Konto

Um eine Verbindung herzustellen, müssen Sie zunächst die Interoperabilität für Ihr [!DNL Platform][!DNL Google Cloud Storage] Konto aktivieren. Um auf die Interoperabilitätseinstellung zuzugreifen, öffnen [!DNL Google Cloud Platform] und wählen Sie im Navigationsbereich unter der Option &quot; **[!UICONTROL Datenspeicherung]** &quot;die Option &quot; **[!UICONTROL Einstellungen]** &quot;aus.

![](../../images/tutorials/create/google-cloud-storage/nav.png)

Die Seite **[!UICONTROL Einstellungen]** wird angezeigt. Von hier aus können Sie Informationen zu Ihrer [!DNL Google] Projekt-ID und Details zu Ihrem [!DNL Google Cloud Storage] Konto sehen. Um auf die Interoperabilitätseinstellungen zuzugreifen, wählen Sie in der oberen Kopfzeile die Option &quot; **[!UICONTROL Interoperabilität]** &quot;aus.

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

Die Seite &quot; **[!UICONTROL Interoperabilität]** &quot;enthält Informationen zur Authentifizierung, zu Zugriffsschlüsseln und zum Standardprojekt, das mit Ihrem Benutzerkonto verknüpft ist. Wenn Sie noch kein Standardprojekt für den interoperablen Zugriff eingerichtet haben, können Sie eines im Abschnitt *[!UICONTROL &quot;Standard&quot;für den interoperablen Zugriff]* einrichten. Wenn bereits ein Standardprojekt eingerichtet wurde, wird im Abschnitt eine Bestätigung angezeigt, dass ein Projekt als Standard festgelegt wurde.

Um eine neue Zugriffsschlüssel-ID und einen geheimen Zugriffsschlüssel für Ihr Benutzerkonto zu erstellen, wählen Sie &quot;Schlüssel **[!UICONTROL erstellen&quot;]**.

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

Sie können Ihre neu generierte Zugriffsschlüssel-ID und den geheimen Zugriffsschlüssel verwenden, um Ihr [!DNL Google Cloud Storage] Konto mit Ihrem Konto zu verbinden [!DNL Platform].

Die nachstehende Dokumentation enthält Informationen zum Herstellen einer Verbindung [!DNL Google Cloud Storage] mit [!DNL Platform] APIs oder der Benutzeroberfläche:

## Verbinden [!DNL Google Cloud Storage] mit [!DNL Platform]

Die nachstehende Dokumentation enthält Informationen zum Herstellen einer Verbindung [!DNL Google Cloud Storage] mit [!DNL Platform] APIs oder der Benutzeroberfläche:

### APIs verwenden

- [Erstellen eines Google Cloud-Datenspeicherung-Connectors mithilfe der Flow Service API](../../tutorials/api/create/cloud-storage/google.md)
- [Kennenlernen eines Cloud-Datenspeicherung-Systems mithilfe der Flow Service API](../../tutorials/api/explore/cloud-storage.md)
- [Erfassen von Cloud-Datenspeicherung-Daten mithilfe der Flow Service API](../../tutorials/api/collect/cloud-storage.md)

### Verwenden der Benutzeroberfläche

- [Erstellen eines Google Cloud-Datenspeicherung-Quellconnectors in der Benutzeroberfläche](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Konfigurieren eines Datenflusses für einen Cloud-Datenspeicherung-Connector in der Benutzeroberfläche](../../tutorials/ui/dataflow/batch/cloud-storage.md)