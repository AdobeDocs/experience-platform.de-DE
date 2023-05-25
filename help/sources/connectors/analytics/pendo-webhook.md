---
title: Pendo Source Overview
description: Erfahren Sie, wie Sie Pendo über APIs oder die Benutzeroberfläche mit Adobe Experience Platform verbinden können, indem Sie Webhooks nutzen.
badge: Beta
exl-id: 376f18ef-1eea-4c42-8041-6fadb5906e9b
source-git-commit: cfe5f34316e9db072f0a320143354f2771b4a3a9
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 20%

---

# [!DNL Pendo]

>[!NOTE]
>
>Die [!DNL Pendo]-Quelle befindet sich in der Beta-Phase. Bitte lesen Sie die [Quellen - Übersicht](../../home.md#terms-and-conditions) für weitere Informationen zur Verwendung von Beta-beschrifteten Quellen.

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform unterstützt die Aufnahme von Daten aus einer Analytics-Anwendung von Drittanbietern. Unterstützung für Analytics-Anbieter: [!DNL Pendo].

[[!DNL Pendo]](https://pendo.io/) ist eine Produktanalyseanwendung, die Software-Unternehmen bei der Entwicklung von Produkten unterstützt, die bei Kunden ankommen. Die App ermöglicht es Softwareherstellern, ihre Produkte mit einer breiten Palette von Tools einzubetten, die sowohl zu einer besseren Produkterfahrung für Benutzer als auch zu neuen Einblicken für das Produktteam führen können.

Die [!DNL Pendo] -Quelle können Sie unterstützte Webhook-Ereignisschemata und die zugehörigen Ereignisdaten aus [!DNL Pendo.io] mithilfe der [[!DNL Pendo] Webhooks](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks). Die [!DNL Pendo] -Quelle funktioniert mit [!DNL Pendo] URL-Webhooks.

Folgende Webhooks werden unterstützt:

* [Handbuch](https://support.pendo.io/hc/en-us/articles/8146679315867-Creating-a-Guide) Angezeigt
* [Umfrage](https://support.pendo.io/hc/en-us/articles/360031867152-Polls-Classic-) Angezeigt/gesendet
* [Net Promoter-Bewertung](https://support.pendo.io/hc/en-us/articles/360033527151-Set-up-an-NPS-Survey) Angezeigt/gesendet

## Voraussetzungen {#prerequisites}

Bevor Sie eine [!DNL Pendo] -Quellverbindung verwenden, müssen Sie zunächst Folgendes sicherstellen:

A [!DNL Pendo] -Konto. Wenn Sie noch keine haben, sehen Sie die [[!DNL Pendo] registrieren](https://app.pendo.io/register) Seite, um sich zu registrieren und Ihr Konto zu erstellen.

### Einrichten [!DNL Pendo] Webhook {#set-up-webhook}

Nachdem Sie Ihren Datenfluss erfolgreich erstellt haben, müssen Sie einen Webhook einrichten, um Platform über [!DNL Pendo] -Ereignisse. [!DNL Pendo] Webhooks können Echtzeit-Benachrichtigungen an andere Dienste senden, wenn bestimmte Ereignisse eintreten, und diese Informationen an Ihre [!DNL Pendo] -Quelle. Weitere Informationen finden Sie in den Tutorials unter [Abrufen der Streaming-Endpunkt-URL](../../tutorials/ui/create/analytics/pendo-webhook.md#get-streaming-endpoint) und [Einrichtung einer [!DNL Pendo] Webhook](../../tutorials/ui/create/analytics/pendo-webhook.md#set-up-webhook).

## Verbinden [!DNL Pendo] Platform {#connect-to-platform}

Die folgende Dokumentation enthält Informationen zum Erstellen einer [!DNL Pendo] Streaming-Connector für die Verbindung [!DNL Platform] Verwendung von APIs oder der Benutzeroberfläche:

### Verbinden von [!DNL Pendo] mit Platform mithilfe von APIs {#connect-to-platform-using-api}

* [Erstellen Sie eine Quellverbindung, um [!DNL Pendo] -Daten über APIs in Platform zu importieren.](../../tutorials/api/create/analytics/pendo-webhook.md)

### Verbinden von [!DNL Pendo] mit Platform über die Benutzeroberfläche {#connect-to-platform-using-ui}

* [Erstellen Sie eine Quellverbindung, um sie zu bringen. [!DNL Pendo] Daten an Platform mithilfe der Benutzeroberfläche](../../tutorials/ui/create/analytics/pendo-webhook.md)
