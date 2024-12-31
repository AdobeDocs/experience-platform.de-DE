---
title: Übersicht über Pendo Source
description: Erfahren Sie, wie Sie Pendo mithilfe von APIs oder der Benutzeroberfläche über Webhooks mit Adobe Experience Platform verbinden
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
>Die [!DNL Pendo]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta[gekennzeichneten Quellen finden Sie ](../../home.md#terms-and-conditions) „Quellen - Übersicht“.

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform unterstützt die Aufnahme von Daten aus Analytics-Anwendungen von Drittanbietern. Der Support für Analytics-Anbieter umfasst [!DNL Pendo].

[[!DNL Pendo]](https://pendo.io/) ist eine Produktanalyseanwendung, die Softwareunternehmen bei der Entwicklung von Produkten unterstützt, die bei ihren Kunden Anklang finden. Die App ermöglicht es Software-Machern, ihre Produkte mit einer Vielzahl von Tools einzubetten, die sowohl zu einem besseren Produkterlebnis für Benutzende als auch zu neuen Einblicken für das Produkt-Team führen können.

Mit der [!DNL Pendo] Quelle können Sie unterstützte Webhook-Ereignisschemata und die zugehörigen Ereignisdaten aus [!DNL Pendo.io] mithilfe von [[!DNL Pendo] Webhooks](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks) aufnehmen. Die [!DNL Pendo]-Quelle funktioniert mit [!DNL Pendo] URL-Webhooks.

Folgende Webhooks werden unterstützt:

* [Guide](https://support.pendo.io/hc/en-us/articles/8146679315867-Creating-a-Guide) angezeigt
* [Abfrage](https://support.pendo.io/hc/en-us/articles/360031867152-Polls-Classic-) angezeigt/gesendet
* [Net Promoter Score](https://support.pendo.io/hc/en-us/articles/360033527151-Set-up-an-NPS-Survey) angezeigt/eingereicht

## Voraussetzungen {#prerequisites}

Bevor Sie eine [!DNL Pendo]-Quellverbindung erstellen können, müssen Sie zunächst sicherstellen, dass Folgendes vorhanden ist:

Ein [!DNL Pendo]. Wenn Sie noch keine haben, sehen Sie die Seite [[!DNL Pendo] registrieren](https://app.pendo.io/register), um sich zu registrieren und Ihr Konto zu erstellen.

### Webhook [!DNL Pendo] {#set-up-webhook}

Nachdem Sie Ihren Datenfluss erfolgreich erstellt haben, müssen Sie einen Webhook einrichten, um Platform über [!DNL Pendo] Ereignisse zu informieren. [!DNL Pendo] Webhooks können Echtzeit-Benachrichtigungen an andere Services senden, wenn bestimmte Ereignisse eintreten, und diese Informationen an Ihre [!DNL Pendo] senden. Weitere Informationen finden Sie in den Tutorials zum [ der Streaming-Endpunkt-URL und ](../../tutorials/ui/create/analytics/pendo-webhook.md#get-streaming-endpoint)Einrichten [ Webhooks [!DNL Pendo]  ](../../tutorials/ui/create/analytics/pendo-webhook.md#set-up-webhook).

## Verbinden von [!DNL Pendo] mit Platform {#connect-to-platform}

Die folgende Dokumentation enthält Informationen zum Erstellen eines [!DNL Pendo] Streaming-Connectors für die Verbindung mit [!DNL Platform] mithilfe von APIs oder der Benutzeroberfläche:

### Verbinden von [!DNL Pendo] mit Platform mithilfe von APIs {#connect-to-platform-using-api}

* [Erstellen Sie eine Quellverbindung, um - [!DNL Pendo]  mithilfe von APIs in Platform zu importieren.](../../tutorials/api/create/analytics/pendo-webhook.md)

### Verbinden von [!DNL Pendo] mit Platform über die Benutzeroberfläche {#connect-to-platform-using-ui}

* [Erstellen einer Quellverbindung, um - [!DNL Pendo]  über die Benutzeroberfläche in Platform zu importieren](../../tutorials/ui/create/analytics/pendo-webhook.md)
