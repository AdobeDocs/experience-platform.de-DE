---
title: Übersicht über Chatlio Source
description: Erfahren Sie, wie Sie Chatlio mithilfe von APIs oder der Benutzeroberfläche über Webhooks mit Adobe Experience Platform verbinden
badge: Beta
exl-id: 4a71d1dc-e0eb-443e-a956-8caa0e82fa18
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 7%

---

# [!DNL Chatlio]

>[!NOTE]
>
>Die [!DNL Chatlio]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta[gekennzeichneten Quellen finden Sie ](../../home.md#terms-and-conditions) „Quellen - Übersicht“.

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform unterstützt die Aufnahme von Daten aus Streaming-Anwendungen. Unterstützung für Streaming-Anbieter umfasst [!DNL Chatlio].

[[!DNL Chatlio]](https://chatlio.com/) ist eine Live-Chat-App, die vollständig mit [!DNL Slack] integriert ist und es mehreren Support-Agenten ermöglicht, einem einzelnen Site-Besucher gleichzeitig zu helfen. [!DNL Chatlio] nutzt die [!DNL Chatio Zapier App], um [!DNL Chatlio] mit über 2000 verschiedenen Apps und Services zu verbinden.

Mit der [!DNL Chatlio] Quelle können Sie unterstützte Webhook-Ereignisschemata und die zugehörigen Ereignisdaten aus [!DNL Chatlio.com] mithilfe von [[!DNL Chatlio] Webhooks](https://chatlio.com/docs/webhooks/) aufnehmen.

Folgende Webhooks werden unterstützt:

* Chattranskripte exportieren
* Offline-Nachrichten exportieren
* Neue Unterhaltung hat begonnen
* Der Besucher hat nicht rechtzeitig eine Antwort erhalten
* Besucher hat Feedback nach einem Chat hinterlassen

## Voraussetzungen {#prerequisites}

Bevor Sie eine [!DNL Chatlio]-Quellverbindung erstellen können, müssen Sie zunächst sicherstellen, dass Folgendes vorhanden ist:

* Ein [!DNL Chatlio]. Wenn Sie noch keine haben, besuchen Sie die [[!DNL Chatlio] Anmeldeseite](https://chatlio.com/app/#/signup) um sich zu registrieren und Ihr Konto zu erstellen.
* Nachdem Sie ein Konto erfolgreich registriert haben, befolgen Sie die [[!DNL Chatlio] Einrichtungsdokumentation](https://chatlio.com/docs/setup/), um Ihre Kontoeinrichtung abzuschließen.

### Webhook [!DNL Chatlio] {#set-up-webhook}

Nachdem Sie Ihren Datenfluss erfolgreich erstellt haben, müssen Sie einen Webhook einrichten, um Experience Platform über [!DNL Chatlio] Ereignisse zu informieren. Webhooks können Sie sofort benachrichtigen, wenn sich Kundenattribute ändern oder wenn Personen Ihre Nachrichten öffnen und diese Informationen an Ihre [!DNL Chatlio] senden.

Weitere Informationen finden Sie in den Tutorials zum [ der Streaming-Endpunkt-URL und ](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#get-streaming-endpoint)Einrichten [ Webhooks [!DNL Chatlio]  ](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md#set-up-webhook).

## Verbinden von [!DNL Chatlio] mit Experience Platform {#connect-to-platform}

Die folgende Dokumentation enthält Informationen zum Erstellen eines [!DNL Chatlio] Streaming-Connectors für die Verbindung mit [!DNL Experience Platform] mithilfe von APIs oder der Benutzeroberfläche:

### Verbinden von [!DNL Chatlio] mit Experience Platform mithilfe von APIs {#connect-to-platform-using-api}

* [Erstellen Sie eine Quellverbindung, um - [!DNL Chatlio]  mithilfe von APIs in Experience Platform zu importieren.](../../tutorials/api/create/marketing-automation/chatlio-webhook.md)

### Verbinden von [!DNL Chatlio] mit Experience Platform über die Benutzeroberfläche {#connect-to-platform-using-ui}

* [Erstellen Sie eine Quellverbindung, um - [!DNL Chatlio]  über die Benutzeroberfläche in Experience Platform zu importieren](../../tutorials/ui/create/marketing-automation/chatlio-webhook.md)
