---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen einer Streaming-Verbindung über die Benutzeroberfläche
topic: tutorial
translation-type: tm+mt
source-git-commit: 181719e729748adcde62199c9406a97b7a807182
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---


# Erstellen einer Streaming-Verbindung über die Benutzeroberfläche

Diese Anleitung der Benutzeroberfläche hilft Ihnen beim Erstellen einer Streaming-Verbindung mit Adobe Experience Platform.

## Erste Schritte

Um Streaming-Daten an Experience Platform Beginn, müssen Sie zunächst eine Streaming-HTTP-Verbindung erstellen. Beim Erstellen einer Streaming-Verbindung müssen Sie wichtige Details wie die Quelle der Streaming-Daten angeben und angeben, ob Daten von einer vertrauenswürdigen (authentifizierten) oder einer nicht vertrauenswürdigen (nicht authentifizierten) Quelle gesendet werden sollen.

Nach der Registrierung einer Streaming-Verbindung haben Sie eine eindeutige URL, mit der Daten an die Plattform gestreamt werden können.

Bitte beachten Sie, dass Sie zum Ausfüllen dieses Handbuchs Zugriff auf die Adobe Experience Platform benötigen. Wenn Sie keinen Zugriff auf die Plattform haben, wenden Sie sich an Ihren Systemadministrator, bevor Sie fortfahren.

## Erstellen einer Streaming-Verbindung

Klicken Sie nach dem Anmelden bei der Experience Platform-Benutzeroberfläche auf **Quellen** , um die Registerkarte &quot; *Katalog* &quot;zu öffnen. Auf dieser Seite werden die verfügbaren Quelltypen als einzelne Karten angezeigt. Jede Karte enthält eine Blase, die die Anzahl der Datenflüsse anzeigt, die aus Streaming-Verbindungen zu Datasets erstellt wurden.

![](../images/streaming-ingestion/ui/click-sources.png)

Klicken Sie auf der Seite &quot; *Quellen* &quot;auf **HTTP-API** und dann auf **Connect-Quelle**.

![](../images/streaming-ingestion/ui/click-connect-source.png)

Der Bildschirm &quot; *Verbindung mit HTTP* herstellen&quot;wird angezeigt. Geben Sie unter *Dienstdetails* sowohl den **Namen** als auch eine **Beschreibung** für Ihre neue Streaming-Verbindung ein.

Wählen Sie unter *Kontoauthentifizierung* die folgenden Konfigurationseigenschaften für Ihre Streaming-Verbindung aus:

- **Authentifizierung:** Gibt an, ob die Streaming-Verbindung authentifiziert werden muss. Die Authentifizierung stellt sicher, dass Daten aus vertrauenswürdigen Quellen erfasst werden. Es wird empfohlen, dass diese Option aktiviert ist, wenn es sich um persönliche identifizierbare Informationen (PII) handelt.
- **XDM-Schema-Kompatibilität:** Ob diese Streaming-Verbindung Ereignis sendet, die mit XDM-Schemas kompatibel sind. Standardmäßig ist diese Eigenschaft **aktiviert**.

Nachdem Sie die Konfigurationseigenschaften ausgewählt haben, klicken Sie auf **Verbinden**. Ihre Streaming-HTTP-Verbindung wird jetzt erstellt und kann jetzt auf der Registerkarte &quot; *Durchsuchen* &quot;im Arbeitsbereich &quot; *Quellen* &quot;angezeigt werden.

![](../images/streaming-ingestion/ui/http-sources-details.png)

Auf der Registerkarte &quot; *Durchsuchen* &quot;können Sie auf Ihre neu erstellte Streaming-HTTP-Verbindung klicken und die Details zu dieser Verbindung in der Ansicht anzeigen.

![](../images/streaming-ingestion/ui/browse-sources.png)

Wenn Sie auf den Hyperlink des Verbindungsnamens klicken, können Sie die anzuzeigenden Daten auswählen, indem Sie konfigurieren, welcher Datensatz verbunden ist, indem Sie auf Daten *auswählen* klicken.

![](../images/streaming-ingestion/ui/select-data.png)

Sie können entweder einen neuen Datensatz [erstellen](#create-a-new-dataset) oder einen vorhandenen Datensatz [verwenden](#use-an-existing-dataset).

### Erstellen eines neuen Datensatzes

Um einen neuen Datensatz zu erstellen, geben Sie den **Namen**, die **Beschreibung** sowie das Zielgruppe- **Schema** für den Datensatz an.

![](../images/streaming-ingestion/ui/create-new-dataset.png)

Wenn Sie alle Details einfügen und auf **Weiter** klicken, können Sie die angegebenen Details überprüfen, bevor Sie auf **Fertig stellen** klicken, um den Datensatz mit Ihrer Streaming-HTTP-Verbindung zu verbinden.

![](../images/streaming-ingestion/ui/review-create-new-dataset.png)

### Vorhandenen Datensatz verwenden

Um einen vorhandenen Datensatz zu verwenden, wählen Sie den Namen des **Ausgabedatasets** aus.

![](../images/streaming-ingestion/ui/use-existing-dataset.png)

Nachdem Sie auf **Weiter** geklickt haben, können Sie die Details überprüfen, bevor Sie auf **Fertig stellen** klicken, um den ausgewählten Datensatz mit Ihrer Streaming-HTTP-Verbindung zu verbinden.

![](../images/streaming-ingestion/ui/review-existing-dataset.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Streaming-HTTP-Verbindung erstellt, über die Sie den Streaming-Endpunkt verwenden können, um auf eine Vielzahl von Data Ingestion-APIs zuzugreifen. Anweisungen zum Erstellen einer Streaming-Verbindung in der API finden Sie im Lernprogramm zum [Erstellen einer Streaming-Verbindung](../tutorials/create-streaming-connection.md).
