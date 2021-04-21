---
keywords: Experience Platform;Startseite;beliebte Themen;Datumsbereich
solution: Experience Platform
title: Adobe I/O Ereignis-Benachrichtigungen abonnieren
topic-legacy: developer guide
description: 'In diesem Dokument wird beschrieben, wie Sie Adobe I/O Ereignis-Benachrichtigungen für Adobe Experience Platform-Dienste abonnieren. Es werden auch Referenzinformationen zu verfügbaren Ereignistypen sowie Links zu weiteren Dokumentationen zur Interpretation der zurückgegebenen Ereignis-Daten für jeden entsprechenden Dienst bereitgestellt. [!DNL Platform] '
exl-id: c0ad7217-ce84-47b0-abf6-76bcf280f026
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 4%

---

# Benachrichtigungen zum Adobe I/O Ereignis abonnieren

[!DNL Observability Insights] können Sie Adobe I/O Ereignis-Benachrichtigungen zu Adobe Experience Platform-Aktivitäten abonnieren. Diese Ereignis werden an einen konfigurierten Webshaken gesendet, um eine effiziente Automatisierung der Aktivität-Überwachung zu ermöglichen.

In diesem Dokument wird beschrieben, wie Sie Adobe I/O Ereignis-Benachrichtigungen für Adobe Experience Platform-Dienste abonnieren. Es werden auch Referenzinformationen zu verfügbaren Ereignistypen sowie Links zu weiteren Dokumentationen zur Interpretation der zurückgegebenen Ereignis-Daten für jeden anwendbaren [!DNL Platform]-Dienst bereitgestellt.

## Erste Schritte

Dieses Dokument erfordert ein funktionierendes Verständnis von Webhooks und wie ein Webhaken von einer Anwendung zur anderen verbunden werden kann. Eine Einführung zu Webhooks finden Sie in der [[!DNL I/O Events] Dokumentation](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md).

## Erstellen eines Webhofs

Um [!DNL I/O Event]-Benachrichtigungen zu erhalten, müssen Sie einen WebHook registrieren, indem Sie eine eindeutige WebHook-URL als Teil Ihrer Ereignis-Registrierungsdetails angeben.

Sie können Ihren Webshaken mit dem Client Ihrer Wahl konfigurieren. Um eine temporäre Webhosting-Adresse als Teil dieses Lernprogramms zu verwenden, besuchen Sie [WebHaken.site](https://webhook.site/) und kopieren Sie die angegebene eindeutige URL.

![](../images/notifications/webhook-url.png)

Während des anfänglichen Validierungsprozesses sendet [!DNL I/O Events] einen `challenge`-Abfrage-Parameter in einer GET-Anforderung an den Webhaken. Sie müssen Ihren Webshaken so konfigurieren, dass der Wert dieses Parameters in der Antwortnutzlast zurückgegeben wird. Wenn Sie WebHook.site verwenden, wählen Sie **[!DNL Edit]** in der oberen rechten Ecke aus und geben Sie `$request.query.challenge$` unter **[!DNL Response body]** ein, bevor Sie **[!DNL Save]** auswählen.

![](../images/notifications/response-challenge.png)

## Neues Projekt in der Adobe Developer Console erstellen

Wechseln Sie zu [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui_de) und melden Sie sich bei Ihrem Adobe ID an. Führen Sie anschließend die Schritte aus, die im Lernprogramm [Erstellen eines leeren Projekts](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) in der Adobe Developer Console-Dokumentation beschrieben werden.

## Ereignisse abonnieren

Nachdem Sie ein neues Projekt erstellt haben, navigieren Sie zum Übersichtsbildschirm dieses Projekts. Wählen Sie **[!UICONTROL Hinzufügen Ereignis]**.

![](../images/notifications/add-event-button.png)

Es wird ein Dialogfeld angezeigt, in dem Sie einen Ereignis Provider zu Ihrem Projekt hinzufügen können:

* Wenn Sie [!DNL Experience Platform]-Benachrichtigungen abonnieren, wählen Sie **[!UICONTROL Plattformbenachrichtigungen]**
* Wenn Sie Adobe Experience Platform [!DNL Privacy Service]-Benachrichtigungen abonnieren, wählen Sie **[!UICONTROL Privacy Service-Ereignis]**

Wenn Sie einen Ereignis-Provider ausgewählt haben, wählen Sie **[!UICONTROL Weiter]**.

![](../images/notifications/event-provider.png)

Im nächsten Bildschirm wird eine Liste von Ereignistypen angezeigt, die abonniert werden sollen. Wählen Sie die Ereignis aus, die Sie abonnieren möchten, und wählen Sie **[!UICONTROL Weiter]**.

>[!NOTE]
>
>Wenn Sie nicht sicher sind, welche Ereignis für den Dienst, mit dem Sie arbeiten, abonniert werden sollen, lesen Sie die dienstspezifische Benachrichtigungsdokumentation:
>
>* [[!DNL Privacy Service] Benachrichtigungen](../../privacy-service/privacy-events.md)
>* [[!DNL Data Ingestion] Benachrichtigungen](../../ingestion/quality/subscribe-events.md)
>* [[!DNL Flow Service (sources)] Benachrichtigungen](../../sources/notifications.md)


![](../images/notifications/choose-event-subscriptions.png)

Im nächsten Bildschirm werden Sie aufgefordert, ein JSON-WebToken (JWT) zu erstellen. Sie haben die Möglichkeit, automatisch ein Schlüsselpaar zu erstellen oder einen eigenen öffentlichen Schlüssel hochzuladen, der im Terminal generiert wurde.

Für diese Übung wird die erste Option verwendet. Wählen Sie das Optionsfeld für **[!UICONTROL Generate a key pair]** und klicken Sie dann unten rechts auf die Schaltfläche **[!UICONTROL Generate keypair]**.

![](../images/notifications/generate-keypair.png)

Wenn das Schlüsselpaar generiert wird, wird es automatisch vom Browser heruntergeladen. Sie müssen diese Datei selbst speichern, da sie nicht in der Developer Console beibehalten wird.

Im nächsten Bildschirm können Sie die Details des neu generierten Schlüsselpaars überprüfen. Wählen Sie **[!UICONTROL Weiter]**, um fortzufahren.

![](../images/notifications/keypair-generated.png)

Geben Sie im nächsten Bildschirm im Abschnitt [!UICONTROL Registrierungsdetails für Ereignisse] einen Namen und eine Beschreibung für die Registrierung des Ereignisses ein. Best Practice ist, einen eindeutigen, leicht identifizierbaren Namen zu erstellen, um diese Ereignis-Registrierung von anderen im selben Projekt zu unterscheiden.

![](../images/notifications/registration-details.png)

Weiter unten auf dem gleichen Bildschirm unter dem Abschnitt [!UICONTROL So erhalten Sie Ereignis] können Sie optional konfigurieren, wie Ereignis empfangen werden. **[!UICONTROL Mit]** Webhooks können Sie eine benutzerdefinierte Webhook-Adresse für den Empfang von Ereignissen angeben, während  **[!UICONTROL Laufzeit-]** Aktionen es Ihnen ermöglichen, dasselbe mit  [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime/docs.html) zu tun.

Wählen Sie für dieses Tutorial **[!UICONTROL WebHaken]** aus und geben Sie die URL des zuvor erstellten WebHook ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Konfigurierte Ereignis speichern]**, um die Ereignis-Registrierung abzuschließen.

![](../images/notifications/receive-events.png)

Die Detailseite für die neu erstellte Ereignis-Registrierung wird angezeigt, auf der Sie die Konfiguration bearbeiten, die empfangenen Ereignis überprüfen, die Debugging-Verfolgung durchführen und neue Ereignis-Provider hinzufügen können.

![](../images/notifications/registration-complete.png)

## Nächste Schritte

Indem Sie diesem Tutorial folgen, haben Sie einen Web-Haken registriert, um [!DNL I/O Event]-Benachrichtigungen für [!DNL Experience Platform] und/oder [!DNL Privacy Service] zu erhalten. Weitere Informationen zu verfügbaren Ereignissen und zur Interpretation der Benachrichtigungs-Nutzlasten für jeden Dienst finden Sie in der folgenden Dokumentation:

* [[!DNL Privacy Service] Benachrichtigungen](../../privacy-service/privacy-events.md)
* [[!DNL Data Ingestion] Benachrichtigungen](../../ingestion/quality/subscribe-events.md)
* [[!DNL Flow Service (sources)] Benachrichtigungen](../../sources/notifications.md)

Weitere Informationen zur Überwachung Ihrer Aktivitäten unter [!DNL Experience Platform] und [!DNL Privacy Service] finden Sie unter [[!DNL Observability Insights] overview](../home.md).
