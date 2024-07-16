---
title: Pendo Source - Übersicht
description: Erfahren Sie, wie Sie Pendo über APIs oder die Benutzeroberfläche mit Adobe Experience Platform verbinden können, indem Sie Webhooks nutzen.
badge: Beta
exl-id: 376f18ef-1eea-4c42-8041-6fadb5906e9b
source-git-commit: 8de45a54607bed17fd79bbed693666beb09c0502
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 18%

---

# [!DNL Pendo]

>[!NOTE]
>
>Die [!DNL Pendo]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta-beschrifteten Quellen finden Sie in der [Quellenübersicht](../../home.md#terms-and-conditions) .

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform unterstützt die Aufnahme von Daten aus Analytics-Anwendungen von Drittanbietern. Unterstützung für Analytics-Anbieter ist [!DNL Pendo].

[[!DNL Pendo]](https://pendo.io/) ist eine Produktanalyseanwendung, die Software-Unternehmen dabei unterstützt, Produkte zu entwickeln, die bei Kunden ankommen. Die App ermöglicht es Softwareherstellern, ihre Produkte mit einer breiten Palette von Tools einzubetten, die sowohl zu einer besseren Produkterfahrung für Benutzer als auch zu neuen Einblicken für das Produktteam führen können.

Mit der Quelle [!DNL Pendo] können Sie unterstützte Webhook-Ereignisschemas und die zugehörigen Ereignisdaten aus [!DNL Pendo.io] mithilfe der [[!DNL Pendo] Webhooks](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks) erfassen. Die Quelle [!DNL Pendo] funktioniert mit [!DNL Pendo] URL-Webhooks.

Folgende Webhooks werden unterstützt:

* [Guide](https://support.pendo.io/hc/en-us/articles/8146679315867-Creating-a-Guide) angezeigt
* [Umfrage](https://support.pendo.io/hc/en-us/articles/360031867152-Polls-Classic-) angezeigt/gesendet
* [Net Promoter-Punktzahl](https://support.pendo.io/hc/en-us/articles/360033527151-Set-up-an-NPS-Survey) angezeigt/gesendet

## Voraussetzungen {#prerequisites}

Bevor Sie eine [!DNL Pendo]-Quellverbindung erstellen können, müssen Sie zunächst Folgendes sicherstellen:

Ein [!DNL Pendo] -Konto. Wenn noch keines vorhanden ist, wird die Seite [[!DNL Pendo] register](https://app.pendo.io/register) angezeigt, auf der Sie sich registrieren und Ihr Konto erstellen können.

### Webhook einrichten [!DNL Pendo] {#set-up-webhook}

Nachdem Sie Ihren Datenfluss erfolgreich erstellt haben, müssen Sie einen Webhook einrichten, um Platform über [!DNL Pendo] -Ereignisse zu informieren. [!DNL Pendo] Webhooks können Echtzeit-Benachrichtigungen an andere Dienste senden, wenn bestimmte Ereignisse eintreten, und diese Informationen an Ihre [!DNL Pendo]-Quelle senden. Weitere Informationen finden Sie in den Tutorials zu [Abrufen der Streaming-Endpunkt-URL](../../tutorials/ui/create/analytics/pendo-webhook.md#get-streaming-endpoint) und [Einrichten eines [!DNL Pendo] Webhook](../../tutorials/ui/create/analytics/pendo-webhook.md#set-up-webhook) .

## Verbinden von [!DNL Pendo] mit Platform {#connect-to-platform}

Die folgende Dokumentation enthält Informationen zum Erstellen eines [!DNL Pendo]-Streaming-Connectors für die Verbindung mit [!DNL Platform] mithilfe von APIs oder der Benutzeroberfläche:

### Verbinden von [!DNL Pendo] mit Platform mithilfe von APIs {#connect-to-platform-using-api}

* [Erstellen Sie eine Quellverbindung, um [!DNL Pendo] Daten mithilfe von APIs an Platform zu übertragen.](../../tutorials/api/create/analytics/pendo-webhook.md)

### Verbinden von [!DNL Pendo] mit Platform über die Benutzeroberfläche {#connect-to-platform-using-ui}

* [Erstellen einer Quellverbindung zum Übertragen von [!DNL Pendo] Daten an Platform mithilfe der Benutzeroberfläche](../../tutorials/ui/create/analytics/pendo-webhook.md)
