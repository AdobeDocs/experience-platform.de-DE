---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Streaming-Verbindung über die Benutzeroberfläche erstellen
topic: tutorial
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 77%

---


# Streaming-Verbindung über die Benutzeroberfläche erstellen

Diese Anleitung für die Benutzeroberfläche hilft Ihnen beim Erstellen einer Streaming-Verbindung für Adobe Experience Platform.

## Erste Schritte

In order to start streaming data to [!DNL Experience Platform], you must first create a streaming HTTP connection. Beim Erstellen einer Streaming-Verbindung müssen Sie wichtige Details wie die Quelle der Streaming-Daten angeben und festlegen, ob Daten von einer vertrauenswürdigen (authentifizierten) oder einer nicht vertrauenswürdigen (nicht authentifizierten) Quelle gesendet werden sollen.

After registering a streaming connection you will have a unique URL which can be used to stream data to [!DNL Platform].

Beachten Sie, dass Sie zum Ausführen dieser Anleitung Zugriff auf Adobe Experience Platform benötigen. If you do not have access to [!DNL Platform], please contact your system administrator before proceeding.

## Streaming-Verbindung erstellen

After logging in to the [!DNL Experience Platform] UI, click **[!UICONTROL Sources]** to open the *[!UICONTROL Catalog]* tab. Auf dieser Seite werden die verfügbaren Quelltypen als einzelne Karten angezeigt. Jede Karte enthält dabei eine Blase, die die Anzahl der Datenflüsse anzeigt, die über Streaming-Verbindungen zu Datensätzen erstellt wurden.

![](../images/streaming-ingestion/ui/click-sources.png)

Klicken Sie auf der Seite *[!UICONTROL Quellen]* auf **[!UICONTROL HTTP-API]** und dann auf **[!UICONTROL Quelle verbinden]**.

![](../images/streaming-ingestion/ui/click-connect-source.png)

Der Bildschirm *[!UICONTROL Mit HTTP verbinden]* wird angezeigt. Geben Sie unter *[!UICONTROL Dienstdetails]* sowohl den **[!UICONTROL Namen]** als auch eine **[!UICONTROL Beschreibung]** für Ihre neue Streaming-Verbindung ein.

Wählen Sie unter *[!UICONTROL Kontoauthentifizierung]* die folgenden Konfigurationseigenschaften für Ihre Streaming-Verbindung aus:

- **[!UICONTROL Authentifizierung]:**Gibt an, ob die Streaming-Verbindung authentifiziert werden muss. Authentifizierung stellt sicher, dass Daten aus vertrauenswürdigen Quellen erfasst werden. Es wird empfohlen, diese Option zu aktivieren, wenn Sie mit personenbezogenen Daten arbeiten.
- **[!UICONTROL XDM-Schema-Kompatibilität]:**Ob diese Streaming-Verbindung Ereignis sendet, die mit XDM-Schemas kompatibel sind. Standardmäßig ist diese Eigenschaft**aktiviert **.

Nachdem Sie die Konfigurationseigenschaften ausgewählt haben, klicken Sie auf **[!UICONTROL Verbinden]**. Ihre Streaming-HTTP-Verbindung wird erstellt und kann jetzt auf dem Tab *[!UICONTROL Durchsuchen]* im Arbeitsbereich *[!UICONTROL Quellen]* angezeigt werden.

![](../images/streaming-ingestion/ui/http-sources-details.png)

Sie können auf dem Tab *[!UICONTROL Durchsuchen]* auf Ihre neu erstellte Streaming-HTTP-Verbindung klicken, um die Details dieser Verbindung anzuzeigen.

![](../images/streaming-ingestion/ui/browse-sources.png)

Wenn Sie auf den Hyperlink des Verbindungsnamens klicken, können Sie anzuzeigende Daten auswählen, indem Sie festlegen, welcher Datensatz verbunden wird, indem Sie auf *[!UICONTROL Daten auswählen]* klicken.

![](../images/streaming-ingestion/ui/select-data.png)

Sie können entweder einen [neuen Datensatz erstellen](#create-a-new-dataset) oder einen [vorhandenen Datensatz verwenden](#use-an-existing-dataset).

### Neuen Datensatz erstellen

Um einen neuen Datensatz zu erstellen, geben Sie den **[!UICONTROL Namen]**, eine **[!UICONTROL Beschreibung]** sowie das **[!UICONTROL Zielschema]** für den Datensatz an.

![](../images/streaming-ingestion/ui/create-new-dataset.png)

Nachdem Sie alle Details eingefügt und auf **[!UICONTROL Weiter]** geklickt haben, können Sie die angegebenen Details überprüfen, bevor Sie auf **[!UICONTROL Fertig stellen]** klicken, um den Datensatz mit Ihrer Streaming-HTTP-Verbindung zu verbinden.

![](../images/streaming-ingestion/ui/review-create-new-dataset.png)

### Vorhandenen Datensatz verwenden

Um einen vorhandenen Datensatz zu nutzen, wählen Sie den Namen des **[!UICONTROL Ausgabedatensatzes]** aus.

![](../images/streaming-ingestion/ui/use-existing-dataset.png)

Nachdem Sie auf **[!UICONTROL Weiter]** geklickt haben, können Sie die Details überprüfen, bevor Sie auf **[!UICONTROL Fertig stellen]** klicken, um den ausgewählten Datensatz mit Ihrer Streaming-HTTP-Verbindung zu verbinden.

![](../images/streaming-ingestion/ui/review-existing-dataset.png)

## Nächste Schritte

By following this tutorial, you have created a streaming HTTP connection, enabling you to use the streaming endpoint to access a variety of [!DNL Data Ingestion] APIs. Anweisungen zum Erstellen einer Streaming-Verbindung in der API finden Sie in der [Anleitung zum Erstellen einer Streaming-Verbindung](../tutorials/create-streaming-connection.md).
