---
title: Übersicht über Chatlio Source
description: Erfahren Sie, wie Sie mithilfe von APIs oder der Benutzeroberfläche Chatlio mit Adobe Experience Platform verbinden können, indem Sie Webhooks nutzen.
badge: Beta
exl-id: 4a71d1dc-e0eb-443e-a956-8caa0e82fa18
source-git-commit: 8de45a54607bed17fd79bbed693666beb09c0502
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 18%

---

# [!DNL Chatlio]

>[!NOTE]
>
>Die [!DNL Chatlio]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta-beschrifteten Quellen finden Sie in der [Quellenübersicht](../../home.md#terms-and-conditions) .

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform unterstützt die Aufnahme von Daten aus Streaming-Anwendungen. Unterstützung für Streaming-Anbieter ist [!DNL Chatlio].

[[!DNL Chatlio]](https://chatlio.com/) ist eine Live-Chat-App, die vollständig in [!DNL Slack] integriert ist und es mehreren Support-Agenten ermöglicht, einem einzelnen Site-Besucher gleichzeitig zu helfen. [!DNL Chatlio] verwendet die [!DNL Chatio Zapier App], um [!DNL Chatlio] mit über 2000 verschiedenen Apps und Diensten zu verbinden.

Mit der Quelle [!DNL Chatlio] können Sie unterstützte Webhook-Ereignisschemas und die zugehörigen Ereignisdaten aus [!DNL Chatlio.com] mithilfe der [[!DNL Chatlio] Webhooks](https://chatlio.com/docs/webhooks/) erfassen.

Folgende Webhooks werden unterstützt:

* Chat-Transkripte exportieren
* Exportieren von Offline-Nachrichten
* Neue Konversation gestartet
* Besucher hat keine Antwort rechtzeitig erhalten
* Besucher hinterließ Feedback nach einem Chat

## Voraussetzungen {#prerequisites}

Bevor Sie eine [!DNL Chatlio]-Quellverbindung erstellen können, müssen Sie zunächst Folgendes sicherstellen:

* Ein [!DNL Chatlio] -Konto. Wenn Sie noch keinen haben, rufen Sie die [[!DNL Chatlio] Anmeldeseite](https://chatlio.com/app/#/signup) auf, um sich zu registrieren und Ihr Konto zu erstellen.
* Nachdem Sie ein Konto erfolgreich registriert haben, befolgen Sie die [[!DNL Chatlio] Einrichtungsdokumentation](https://chatlio.com/docs/setup/) , um Ihre Kontoeinrichtung abzuschließen.

### Einrichten von [!DNL Chatlio] Webhook {#set-up-webhook}

Nachdem Sie Ihren Datenfluss erfolgreich erstellt haben, müssen Sie einen Webhook einrichten, um Platform über [!DNL Chatlio] -Ereignisse zu informieren. Webhooks können Sie sofort benachrichtigen, wenn sich Kundenattribute ändern oder wenn Benutzer Ihre Nachrichten öffnen und diese Informationen an Ihre [!DNL Chatlio]-Quelle senden.

Weitere Informationen finden Sie in den Tutorials zu [Abrufen der Streaming-Endpunkt-URL](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#get-streaming-endpoint) und [Einrichten eines [!DNL Chatlio] Webhook](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#set-up-webhook) .

## Verbinden von [!DNL Chatlio] mit Platform {#connect-to-platform}

Die folgende Dokumentation enthält Informationen zum Erstellen eines [!DNL Chatlio]-Streaming-Connectors für die Verbindung mit [!DNL Platform] mithilfe von APIs oder der Benutzeroberfläche:

### Verbinden von [!DNL Chatlio] mit Platform mithilfe von APIs {#connect-to-platform-using-api}

* [Erstellen Sie eine Quellverbindung, um [!DNL Chatlio] Daten mithilfe von APIs an Platform zu übertragen.](../../tutorials/api/create/marketing-automation/chatlio-webhook.md)

### Verbinden von [!DNL Chatlio] mit Platform über die Benutzeroberfläche {#connect-to-platform-using-ui}

* [Erstellen einer Quellverbindung zum Übertragen von [!DNL Chatlio] Daten an Platform mithilfe der Benutzeroberfläche](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md)
