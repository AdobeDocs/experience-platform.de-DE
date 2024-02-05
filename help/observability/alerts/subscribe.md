---
keywords: Experience Platform;Startseite;beliebte Themen;Datumsbereich
title: Abonnieren von Adobe I/O-Ereignisbenachrichtigungen
description: In diesem Dokument wird beschrieben, wie Sie Adobe I/O-Ereignisbenachrichtigungen für Services von Adobe Experience Platform abonnieren. Es werden auch Referenzinformationen zu verfügbaren Ereignistypen sowie Links zu weiteren Dokumentationen zur Interpretation der zurückgegebenen Ereignisdaten für jeden anwendbaren  [!DNL Platform] -Service bereitgestellt.
feature: Alerts
exl-id: c0ad7217-ce84-47b0-abf6-76bcf280f026
source-git-commit: 06ea57d41269e98ddd984c898f41c478ddefc618
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 90%

---

# Abonnieren von Adobe I/O-Ereignisbenachrichtigungen

Mit [!DNL Observability Insights] können Sie Ereignisbenachrichtigungen zu Aktivitäten von Adobe Experience Platform abonnieren. Diese Ereignisse werden an einen konfigurierten Webhook gesendet, um eine effiziente Automatisierung der Aktivitätsüberwachung zu ermöglichen.

In diesem Dokument wird beschrieben, wie Sie Adobe I/O-Ereignisbenachrichtigungen für Adobe Experience Platform-Dienste abonnieren können. Es werden auch Referenzinformationen zu verfügbaren Ereignistypen sowie Links zu weiteren Dokumentationen zur Interpretation der zurückgegebenen Ereignisdaten für die einzelnen zutreffenden [!DNL Platform] -Dienst.

## Erste Schritte

Dieses Dokument setzt voraus, dass Sie mit Webhooks vertraut sind und wissen, wie Sie einen Webhook von einer Anwendung zu einer anderen verbinden. Eine Einführung in Webhooks finden Sie in der [[!DNL I/O Events] Dokumentation](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md).

## Erstellen eines Webhooks

Um [!DNL I/O Event]-Benachrichtigungen zu erhalten, müssen Sie einen Webhook registrieren, indem Sie eine eindeutige Webhook-URL als Teil Ihrer Details zur Ereignisregistrierung angeben.

Sie können Ihren Webhook mit dem Client Ihrer Wahl konfigurieren. Eine temporäre Webhook-Adresse, die Sie im Rahmen dieses Tutorials verwenden können, finden Sie unter [Webhook.site](https://webhook.site/), von wo Sie die bereitgestellte eindeutige URL kopieren können.

![](../images/notifications/webhook-url.png)

Während des anfänglichen Validierungsprozesses sendet [!DNL I/O Events] einen `challenge`-Abfrageparameter in einer GET-Anfrage an den Webhook. Sie müssen Ihren Webhook so konfigurieren, dass der Wert dieses Parameters in der Antwort-Payload zurückgegeben wird. Wenn Sie Webhook.site verwenden, wählen Sie oben rechts **[!DNL Edit]** aus und geben Sie `$request.query.challenge$` unter **[!DNL Response body]** ein, bevor Sie **[!DNL Save]** auswählen.

![](../images/notifications/response-challenge.png)

## Erstellen eines neuen Projekts in Adobe Developer Console

Wechseln Sie zur [Adobe-Entwicklerkonsole](https://www.adobe.com/go/devs_console_ui) und melden Sie sich mit Ihrer Adobe ID an. Führen Sie anschließend die Schritte aus, die im Tutorial [Erstellen eines leeren Projekts](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) in der Dokumentation zu Adobe Developer Console beschrieben werden.

## Abonnieren von Ereignissen

>[!NOTE]
>
>Das Datenerfassungsbenachrichtigungsereignis wird im Adobe I/O nicht mehr unterstützt. Stattdessen sollten Sie die **Informationen zum Quellenfluss** E/A-Ereignis.

Nachdem Sie ein neues Projekt erstellt haben, navigieren Sie zum Übersichtsbildschirm dieses Projekts. Wählen Sie hier **[!UICONTROL Ereignis hinzufügen]** aus.

![](../images/notifications/add-event-button.png)

Es wird ein Dialogfeld angezeigt, in dem Sie einen Ereignisanbieter zu Ihrem Projekt hinzufügen können:

* Wenn Sie Warnhinweise für Experience Platformen abonnieren, wählen Sie **[!UICONTROL Platform-Benachrichtigungen]** aus.
* Wenn Sie [!DNL Privacy Service]-Benachrichtigungen von Adobe Experience Platform abonnieren, wählen Sie **[!UICONTROL Privacy Service-Ereignisse]** aus.

Nachdem Sie einen Ereignisanbieter ausgewählt haben, klicken Sie auf **[!UICONTROL Weiter]**.

![](../images/notifications/event-provider.png)

Im nächsten Bildschirm wird eine Liste der Ereignistypen angezeigt, die abonniert werden können. Wählen Sie die Ereignisse aus, die Sie abonnieren möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**.

>[!NOTE]
>
>Wenn Sie sich nicht sicher sind, welche Ereignisse Sie für den Service, mit dem sie arbeiten, abonnieren sollen, konsultieren Sie die Service-spezifische Dokumentation:
>
>* [Platform-Benachrichtigungen](./rules.md)
>* [Privacy Service-Benachrichtigungen](../../privacy-service/privacy-events.md)

![](../images/notifications/choose-event-subscriptions.png)

Im nächsten Bildschirm werden Sie aufgefordert, ein JSON-Web-Token (JWT) zu erstellen. Sie erhalten die Möglichkeit, automatisch ein Schlüsselpaar zu generieren oder Ihren eigenen öffentlichen Schlüssel hochzuladen, der im Terminal generiert wurde.

Für die Zwecke dieses Tutorials wird die erste Option verwendet. Wählen Sie das Optionsfeld für **[!UICONTROL Schlüsselpaar generieren]** aus und klicken Sie dann unten rechts auf die Schaltfläche **[!UICONTROL Schlüsselpaar generieren]**.

![](../images/notifications/generate-keypair.png)

Wenn das Schlüsselpaar generiert wird, wird es automatisch vom Browser heruntergeladen. Sie müssen diese Datei selbst speichern, da sie nicht in der Developer Console beibehalten wird.

Im nächsten Bildschirm können Sie die Details des neu generierten Schlüsselpaars überprüfen. Klicken Sie auf **[!UICONTROL Weiter]**, um fortzufahren.

![](../images/notifications/keypair-generated.png)

Geben Sie im nächsten Bildschirm im Abschnitt [!UICONTROL Details zur Ereignisregistrierung] einen Namen und eine Beschreibung für die Ereignisregistrierung ein. Es empfiehlt sich, einen eindeutigen, leicht identifizierbaren Namen zu wählen, um diese Ereignisregistrierung von anderen im selben Projekt zu unterscheiden.

![](../images/notifications/registration-details.png)

Im selben Bildschirm können Sie unter dem Abschnitt [!UICONTROL Ereignisempfang] weiter unten optional konfigurieren, wie Ereignisse empfangen werden sollen. Ein **[!UICONTROL Webhook]** ermöglicht es Ihnen, eine benutzerdefinierte Webhook-Adresse für den Empfang von Ereignissen anzugeben, während **[!UICONTROL Runtime-Aktionen]** das gleiche mit [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime/docs.html) ermöglichen.

Wählen Sie für dieses Tutorial **[!UICONTROL Webhook]** aus und geben Sie die URL des zuvor erstellten Webhooks an. Nachdem Sie fertig sind, wählen Sie **[!UICONTROL Konfigurierte Ereignisse speichern]** aus, um die Ereignisregistrierung abzuschließen.

![](../images/notifications/receive-events.png)

Die Detailseite für die neu erstellte Ereignisregistrierung wird angezeigt. Dort können Sie die Konfiguration bearbeiten, die empfangenen Ereignisse überprüfen, eine Debugging-Verfolgung durchführen und neue Ereignisanbieter hinzufügen.

![](../images/notifications/registration-complete.png)

## Nächste Schritte

In diesem Tutorial haben Sie einen Webhook registriert, um [!DNL I/O Event]-Benachrichtigungen für [!DNL Experience Platform] und/oder [!DNL Privacy Service] zu erhalten. Weitere Informationen zu verfügbaren Ereignissen und zur Interpretation der Benachrichtigungs-Payloads für jeden Service finden Sie in der folgenden Dokumentation:

* [[!DNL Privacy Service] Benachrichtigungen](../../privacy-service/privacy-events.md)
* [[!DNL Data Ingestion] Benachrichtigungen](../../ingestion/quality/subscribe-events.md)
* [[!DNL Flow Service] (Quellen)-Benachrichtigungen](../../sources/notifications.md)

Weitere Informationen dazu, wie Sie Ihre Aktivitäten auf [!DNL Experience Platform] und [!DNL Privacy Service] überwachen können, finden Sie in der [[!DNL Observability Insights] Übersicht](../home.md).
