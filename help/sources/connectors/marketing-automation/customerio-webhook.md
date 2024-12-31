---
title: Übersicht über Customer.io Source
description: Erfahren Sie, wie Sie Customer.io mithilfe von APIs oder der Benutzeroberfläche über Webhooks mit Adobe Experience Platform verbinden
badge: Beta
exl-id: 0f4ee106-c22b-465c-9c5e-83709e8424f5
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 17%

---

# [!DNL Customer.io]

>[!NOTE]
>
>Die [!DNL Customer.io]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta[gekennzeichneten Quellen finden Sie ](../../home.md#terms-and-conditions) „Quellen - Übersicht“.

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform unterstützt die Aufnahme von Daten aus Streaming-Anwendungen. Unterstützung für Streaming-Anbieter umfasst [!DNL Customer.io].

[[!DNL Customer.io]](https://customer.io/) ist eine automatisierte Messaging-Plattform für Marketing-Fachleute, die mehr Kontrolle und Flexibilität beim Erstellen und Senden datengesteuerter E-Mails, Push-Benachrichtigungen, In-App-Nachrichten und SMS wünschen.

Mit der [!DNL Customer.io] Quelle können Sie unterstützte Webhook-Ereignisschemata und die zugehörigen Ereignisdaten aus [!DNL Customer.io] mithilfe der [[!DNL Customer.io] Reporting-Webhooks“ ](https://customer.io/docs/api/webhooks/).

Folgende Webhook-Ereignisschemata werden unterstützt:

* Kundenereignisse
* E-Mail-Ereignisse
* SMS-Ereignisse
* Push-Benachrichtigungsereignisse
* In-App-Nachrichtenereignisse
* Slack-Ereignisse
* Webhook-Ereignisse

Eine Liste der Ereignisse, die über Webhooks verfügbar sind, finden Sie in der Dokumentation [[!DNL Customer.io] Reporting-Webhook](https://customer.io/docs/webhooks/#events)Ereignisse .

## Voraussetzungen {#prerequisites}

Bevor Sie eine [!DNL Customer.io]-Quellverbindung erstellen können, müssen Sie zunächst sicherstellen, dass Folgendes vorhanden ist:

* Ein [!DNL Customer.io]. Wenn Sie noch keinen haben, lesen Sie die [[!DNL Customer.io] Anmeldeseite](https://fly.customer.io/signup), um sich zu registrieren und Ihr Konto zu erstellen.
* Nachdem Sie Ihr Konto erstellt haben, müssen Sie es auch validieren lassen. Führen Sie die auf der Seite [[!DNL Customer.io] Kontoüberprüfung](https://customer.io/docs/account-verification/) dokumentierten Schritte aus, um den Vorgang abzuschließen.

### Webhook [!DNL Customer.io] {#set-up-webhook}

Nachdem Sie Ihren Datenfluss erfolgreich erstellt haben, müssen Sie einen Reporting-Webhook einrichten, um Platform über [!DNL Customer.io] Ereignisse zu informieren. Webhooks können Sie sofort benachrichtigen, wenn sich Kundenattribute ändern oder wenn Personen Ihre Nachrichten öffnen, und diese Informationen an Ihre [!DNL Customer.io] senden. Weitere Informationen finden Sie in den Tutorials zum [ der Streaming-Endpunkt-URL und ](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#get-streaming-endpoint)Einrichten [ Webhooks [!DNL Customer.io]  ](../../tutorials/ui/create/marketing-automation/customerio-webhook.md#set-up-webhook).

## Verbinden von [!DNL Customer.io] mit Platform {#connect-to-platform}

Die folgende Dokumentation enthält Informationen zum Erstellen einer [!DNL Customer.io] Streaming-Verbindung für die Verbindung mit [!DNL Platform] mithilfe von APIs oder der Benutzeroberfläche:

### Verbinden von [!DNL Customer.io] mit Platform mithilfe von APIs {#connect-to-platform-using-api}

* [Erstellen Sie eine Quellverbindung und einen Datenfluss, um - [!DNL Customer.io]  mithilfe von APIs in Platform zu übertragen.](../../tutorials/api/create/marketing-automation/customerio-webhook.md)

### Verbinden von [!DNL Customer.io] mit Platform über die Benutzeroberfläche {#connect-to-platform-using-ui}

* [Erstellen einer Quellverbindung und eines Datenflusses, um - [!DNL Customer.io]  über die Benutzeroberfläche in Platform zu übertragen](../../tutorials/ui/create/marketing-automation/customerio-webhook.md)
