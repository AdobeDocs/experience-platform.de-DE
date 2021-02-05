---
keywords: Experience Platform;Home;beliebte Themen;Streaming-Verbindung;Streaming-Verbindung erstellen;UI-Handbuch;Tutorial;Erstellen einer Streaming-Verbindung;Streaming-Verbindung;Erfassung;
solution: Experience Platform
title: Erstellen einer Streaming-Verbindung mithilfe der Benutzeroberfläche
topic: tutorial
type: Tutorial
description: Diese Anleitung für die Benutzeroberfläche hilft Ihnen beim Erstellen einer Streaming-Verbindung für Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 70%

---


# Aufbauen einer Streaming-Verbindung über die Benutzeroberfläche

Diese Anleitung für die Benutzeroberfläche hilft Ihnen beim Erstellen einer Streaming-Verbindung für Adobe Experience Platform.

## Erste Schritte

Um Streaming-Daten auf [!DNL Experience Platform] Beginn, müssen Sie zunächst eine Streaming-HTTP-Verbindung erstellen. Beim Erstellen einer Streaming-Verbindung müssen Sie wichtige Details wie die Quelle der Streaming-Daten angeben und festlegen, ob Daten von einer vertrauenswürdigen (authentifizierten) oder einer nicht vertrauenswürdigen (nicht authentifizierten) Quelle gesendet werden sollen.

Nach der Registrierung einer Streaming-Verbindung haben Sie eine eindeutige URL, mit der Daten an [!DNL Platform] gestreamt werden können.

Beachten Sie, dass Sie zum Ausführen dieser Anleitung Zugriff auf Adobe Experience Platform benötigen. Wenn Sie keinen Zugriff auf [!DNL Platform] haben, wenden Sie sich an Ihren Systemadministrator, bevor Sie fortfahren.

## Aufbauen einer Streaming-Verbindung

Klicken Sie nach dem Anmelden bei der [!DNL Experience Platform]-Benutzeroberfläche auf **[!UICONTROL Quellen]**, um die Registerkarte **[!UICONTROL Katalog]** zu öffnen. Auf dieser Seite werden die verfügbaren Quelltypen als einzelne Karten angezeigt. Jede Karte enthält dabei eine Blase, die die Anzahl der Datenflüsse anzeigt, die über Streaming-Verbindungen zu Datensätzen erstellt wurden.

![](../images/streaming-ingestion/ui/click-sources.png)

Klicken Sie auf der Seite **[!UICONTROL Quellen]** auf **[!UICONTROL HTTP-API]** und dann auf **[!UICONTROL Quelle verbinden]**.

![](../images/streaming-ingestion/ui/click-connect-source.png)

Der Bildschirm **[!UICONTROL Mit HTTP verbinden]** wird angezeigt. Geben Sie unter **[!UICONTROL Dienstdetails]** sowohl den Namen als auch eine Beschreibung für Ihre neue Streaming-Verbindung ein.

Wählen Sie unter **[!UICONTROL Kontoauthentifizierung]** die folgenden Konfigurationseigenschaften für Ihre Streaming-Verbindung aus:

- **[!UICONTROL Authentifizierung]:** Hierfür ist eine Authentifizierung für die Streaming-Verbindung erforderlich. Authentifizierung stellt sicher, dass Daten aus vertrauenswürdigen Quellen erfasst werden. Es wird empfohlen, diese Option zu aktivieren, wenn Sie mit personenbezogenen Daten arbeiten.
- **[!UICONTROL XDM-Schema-Kompatibilität]:** Ob diese Streaming-Verbindung Ereignis sendet, die mit XDM-Schemas kompatibel sind. Standardmäßig ist diese Eigenschaft **aktiviert**.

Nachdem Sie die Konfigurationseigenschaften ausgewählt haben, klicken Sie auf **[!UICONTROL Verbinden]**. Ihre Streaming-HTTP-Verbindung wird erstellt und kann jetzt auf dem Tab **[!UICONTROL Durchsuchen]** im Arbeitsbereich **[!UICONTROL Quellen]** angezeigt werden.

![](../images/streaming-ingestion/ui/http-sources-details.png)

Sie können auf dem Tab **[!UICONTROL Durchsuchen]** auf Ihre neu erstellte Streaming-HTTP-Verbindung klicken, um die Details dieser Verbindung anzuzeigen.

![](../images/streaming-ingestion/ui/browse-sources.png)

Wenn Sie auf den Hyperlink des Verbindungsnamens klicken, können Sie anzuzeigende Daten auswählen, indem Sie festlegen, welcher Datensatz verbunden wird, indem Sie auf **[!UICONTROL Daten auswählen]** klicken.

![](../images/streaming-ingestion/ui/select-data.png)

Sie können entweder einen [neuen Datensatz erstellen](#create-a-new-dataset) oder einen [vorhandenen Datensatz verwenden](#use-an-existing-dataset).

### Neuen Datensatz erstellen

Um einen neuen Datensatz zu erstellen, geben Sie den Namen, die Beschreibung sowie das Schema für die Zielgruppe des Datensatzes ein.

![](../images/streaming-ingestion/ui/create-new-dataset.png)

Nachdem Sie alle Details eingefügt und auf **[!UICONTROL Weiter]** geklickt haben, können Sie die angegebenen Details überprüfen, bevor Sie auf **[!UICONTROL Fertig stellen]** klicken, um den Datensatz mit Ihrer Streaming-HTTP-Verbindung zu verbinden.

![](../images/streaming-ingestion/ui/review-create-new-dataset.png)

### Vorhandenen Datensatz verwenden

Um einen vorhandenen Datensatz zu nutzen, wählen Sie den Namen des **[!UICONTROL Ausgabedatensatzes]** aus.

![](../images/streaming-ingestion/ui/use-existing-dataset.png)

Nachdem Sie auf **[!UICONTROL Weiter]** geklickt haben, können Sie die Details überprüfen, bevor Sie auf **[!UICONTROL Fertig stellen]** klicken, um den ausgewählten Datensatz mit Ihrer Streaming-HTTP-Verbindung zu verbinden.

![](../images/streaming-ingestion/ui/review-existing-dataset.png)

## Nächste Schritte

In diesem Lernprogramm haben Sie eine Streaming-HTTP-Verbindung erstellt, über die Sie den Streaming-Endpunkt verwenden können, um auf eine Vielzahl von [!DNL Data Ingestion]-APIs zuzugreifen. Anweisungen zum Erstellen einer Streaming-Verbindung in der API finden Sie in der [Anleitung zum Erstellen einer Streaming-Verbindung](../tutorials/create-streaming-connection.md).
