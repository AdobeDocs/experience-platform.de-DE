---
title: Übersicht über die Chatlio-Quelle
description: Erfahren Sie, wie Sie mithilfe von APIs oder der Benutzeroberfläche Chatlio mit Adobe Experience Platform verbinden können, indem Sie Webhooks nutzen.
badge: "Beta"
source-git-commit: 2c13cb5a951a3144d0047b567194732acdc35dab
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 21%

---

# [!DNL Chatlio]

>[!NOTE]
>
>Die [!DNL Chatlio]-Quelle befindet sich in der Beta-Phase. Bitte lesen Sie die [Quellen - Übersicht](../../home.md#terms-and-conditions) für weitere Informationen zur Verwendung von Beta-beschrifteten Quellen.

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform unterstützt die Aufnahme von Daten aus Streaming-Anwendungen. Unterstützung für Streaming-Anbieter umfasst [!DNL Chatlio].

[[!DNL Chatlio]](https://chatlio.com/) ist eine Live-Chat-App, die vollständig in [!DNL Slack] und ermöglicht es mehreren Support-Agenten, einem einzelnen Site-Besucher gleichzeitig zu helfen. [!DNL Chatlio] verwendet die [!DNL Chatio Zapier App] Verbindung herstellen [!DNL Chatlio] mit über 2000 verschiedenen Apps und Diensten.

Die [!DNL Chatlio] -Quelle können Sie unterstützte Webhook-Ereignisschemata und die zugehörigen Ereignisdaten aus [!DNL Chatlio.com] mithilfe der [[!DNL Chatlio] Webhooks](https://chatlio.com/docs/webhooks/).

Folgende Webhooks werden unterstützt:

* Chat-Transkripte exportieren
* Exportieren von Offline-Nachrichten
* Neue Konversation gestartet
* Besucher hat keine Antwort rechtzeitig erhalten
* Besucher hinterließ Feedback nach einem Chat

## Voraussetzungen {#prerequisites}

Bevor Sie eine [!DNL Chatlio] -Quellverbindung verwenden, müssen Sie zunächst Folgendes sicherstellen:

* A [!DNL Chatlio] -Konto. Wenn Sie noch keinen Besuch haben, finden Sie unter [[!DNL Chatlio] Anmeldeseite](https://chatlio.com/app/#/signup) , um sich zu registrieren und Ihr Konto zu erstellen.
* Nachdem Sie ein Konto erfolgreich registriert haben, folgen Sie dem [[!DNL Chatlio] Setup-Dokumentation](https://chatlio.com/docs/setup/) , um Ihre Kontoeinrichtung abzuschließen.

### Einrichtung [!DNL Chatlio] Webhook {#set-up-webhook}

Nachdem Sie Ihren Datenfluss erfolgreich erstellt haben, müssen Sie einen Webhook einrichten, um Platform über [!DNL Chatlio] -Ereignisse. Webhooks können Sie sofort benachrichtigen, wenn sich Kundenattribute ändern oder wenn Benutzer Ihre Nachrichten öffnen und diese Informationen an Ihre [!DNL Chatlio] -Quelle.

Weitere Informationen finden Sie in den Tutorials unter [Abrufen der Streaming-Endpunkt-URL](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#get-streaming-endpoint) und [Einrichtung einer [!DNL Chatlio] Webhook](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#set-up-webhook).

## Verbinden von [!DNL Chatlio] mit Platform {#connect-to-platform}

Die folgende Dokumentation enthält Informationen zum Erstellen einer [!DNL Chatlio] Streaming-Connector für die Verbindung [!DNL Platform] Verwendung von APIs oder der Benutzeroberfläche:

### Verbinden von [!DNL Chatlio] mit Platform mithilfe von APIs {#connect-to-platform-using-api}

* [Erstellen Sie eine Quellverbindung, um [!DNL Chatlio] -Daten über APIs in Platform zu importieren.](../../tutorials/api/create/marketing-automation/chatlio-webhook.md)

### Verbinden von [!DNL Chatlio] mit Platform über die Benutzeroberfläche {#connect-to-platform-using-ui}

* [Erstellen Sie eine Quellverbindung, um sie zu bringen. [!DNL Chatlio] Daten an Platform mithilfe der Benutzeroberfläche](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md)

