---
title: Überblick über die Quelle von Customer.io
description: Erfahren Sie, wie Sie mithilfe von APIs oder der Benutzeroberfläche Customer.io mit Adobe Experience Platform verbinden können, indem Sie Webhooks nutzen.
badge: Beta
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 0f4ee106-c22b-465c-9c5e-83709e8424f5
source-git-commit: 0cc4eab97dcd56d2b1d679cf5f35932976d22634
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 16%

---

# [!DNL Customer.io]

>[!NOTE]
>
>Die [!DNL Customer.io]-Quelle befindet sich in der Beta-Phase. Bitte lesen Sie die [Quellen - Übersicht](../../home.md#terms-and-conditions) für weitere Informationen zur Verwendung von Beta-beschrifteten Quellen.

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform unterstützt die Aufnahme von Daten aus Streaming-Anwendungen. Unterstützung für Streaming-Anbieter umfasst [!DNL Customer.io].

[[!DNL Customer.io]](https://customer.io/) ist eine automatisierte Messaging-Plattform für Marketing-Experten, die mehr Kontrolle und Flexibilität beim Erstellen und Senden datengesteuerter E-Mails, Push-Benachrichtigungen, In-App-Nachrichten und SMS wünschen.

Die [!DNL Customer.io] -Quelle können Sie unterstützte Webhook-Ereignisschemata und die zugehörigen Ereignisdaten aus [!DNL Customer.io] mithilfe der [[!DNL Customer.io] Webhooks für Berichterstellung](https://customer.io/docs/api/webhooks/).

Folgende Webhook-Ereignisschemata werden unterstützt:

* Kundenereignisse
* E-Mail-Ereignisse
* SMS-Ereignisse
* Push-Benachrichtigungsereignisse
* In-App-Nachrichtenereignisse
* Slack-Ereignisse
* Webhook-Ereignisse

Eine Liste der über Webhooks verfügbaren Veranstaltungen finden Sie im Abschnitt [[!DNL Customer.io] Webhook-Ereignisse melden](https://customer.io/docs/webhooks/#events) Dokumentation.

## Voraussetzungen {#prerequisites}

Bevor Sie eine [!DNL Customer.io] -Quellverbindung verwenden, müssen Sie zunächst Folgendes sicherstellen:

* A [!DNL Customer.io] -Konto. Wenn Sie keinen haben, lesen Sie die [[!DNL Customer.io] Anmeldeseite](https://fly.customer.io/signup) , um sich zu registrieren und Ihr Konto zu erstellen.
* Nachdem Sie Ihr Konto erstellt haben, müssen Sie auch Ihr Konto validieren lassen. Befolgen Sie die im Abschnitt [[!DNL Customer.io] Kontoüberprüfung](https://customer.io/docs/account-verification/) Seite, um den Prozess abzuschließen.

### Einrichten [!DNL Customer.io] Webhook {#set-up-webhook}

Nachdem Sie Ihren Datenfluss erfolgreich erstellt haben, müssen Sie einen Reporting-Webhook einrichten, um Platform über [!DNL Customer.io] -Ereignisse. Webhooks können Sie sofort benachrichtigen, wenn sich Kundenattribute ändern oder wenn Benutzer Ihre Nachrichten öffnen, und diese Informationen an Ihre [!DNL Customer.io] -Quelle. Weitere Informationen finden Sie in den Tutorials unter [Abrufen der Streaming-Endpunkt-URL](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#get-streaming-endpoint) und [Einrichtung einer [!DNL Customer.io] Webhook](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#set-up-webhook).

## Verbinden [!DNL Customer.io] Platform {#connect-to-platform}

Die folgende Dokumentation enthält Informationen zum Erstellen einer [!DNL Customer.io] Streaming-Verbindung mit [!DNL Platform] Verwendung von APIs oder der Benutzeroberfläche:

### Verbinden von [!DNL Customer.io] mit Platform mithilfe von APIs {#connect-to-platform-using-api}

* [Erstellen Sie eine Quellverbindung und einen Datenfluss, um [!DNL Customer.io] Daten mithilfe von APIs an Platform übermitteln.](../../tutorials/api/create/marketing-automation/customerio-webhook.md)

### Verbinden von [!DNL Customer.io] mit Platform über die Benutzeroberfläche {#connect-to-platform-using-ui}

* [Erstellen Sie eine Quellverbindung und einen Datenfluss, um [!DNL Customer.io] Daten an Platform mithilfe der Benutzeroberfläche](../../tutorials/ui/create/marketing-automation/customerio-webhook.md)
