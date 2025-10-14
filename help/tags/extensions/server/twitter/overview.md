---
keywords: Erweiterung für Ereignisweiterleitung;Twitter;Twitter-Erweiterung für Ereignisweiterleitung
title: Twitter-Erweiterung zur Ereignisweiterleitung
description: Mit dieser Adobe Experience Platform-Ereignisweiterleitungserweiterung können Sie für Ihre Geschäftsanforderungen Ereignisse in Twitter aufnehmen.
last-substantial-update: 2023-05-24T00:00:00Z
exl-id: 54c240e5-6160-4654-ac5b-6afa8d99a765
source-git-commit: 374c140a5db678adfa2e038b69478ad8c7f8dc95
workflow-type: tm+mt
source-wordcount: '1048'
ht-degree: 7%

---

# [!DNL Twitter]-Erweiterung zur Ereignisweiterleitung

[[!DNL Twitter]](https://twitter.com/i/flow/login) ist ein Online-Dienst für soziale Medien und soziale Netzwerke, auf dem Nutzer 280 Zeichen lange Nachrichten, auch Tweets genannt, posten und damit interagieren können. Benutzer können mit Twitter über einen Browser, eine mobile Frontend-Software oder programmgesteuert über die [APIs) &#x200B;](https://developer.twitter.com/en/docs/twitter-api)

Mit der [!DNL Twitter] Web Conversions-API [Ereignisweiterleitung](../../../ui/event-forwarding/overview.md) können Sie die in Adobe Experience Platform Edge Network erfassten Daten nutzen und an [!DNL Twitter] senden. In diesem Dokument werden die Anwendungsfälle der Erweiterung, deren Installation und die Integration der Funktionen in die Ereignisweiterleitung ([) &#x200B;](../../../ui/managing-resources/rules.md).

[!DNL Twitter] erfordert [OAuth 1.0](https://developer.twitter.com/en/docs/authentication/oauth-1-0a) für die Authentifizierung mit der [!DNL Twitter] [!DNL Web Conversions]-API.

## Anwendungsfälle

Diese Erweiterung sollte verwendet werden, wenn Sie Daten aus der Edge Network verwenden möchten, [!DNL Twitter] die Analyse- und Targeting-Funktionen von Customer Journey Analytics zu nutzen.

Betrachten Sie beispielsweise ein Marketing-Team in einer Organisation. Das Team erfasst Ereignisdaten von Benutzerinteraktionen auf seiner Website als Ereignisdaten von seiner Website und lädt sie mithilfe dieser Erweiterung für die Ereignisweiterleitung in [!DNL Twitter].

Die Marketing- und Analyse-Teams können dann [!DNL Twitter's] Funktionen nutzen, um zusätzliche Analysen durchzuführen und diese Benutzer für zielgerichtete Werbekampagnen anzusprechen.

Weitere Informationen zu [!DNL Twitter]-spezifischen Anwendungsfällen finden Sie in der Dokumentation [[!DNL Twitter] Anwendungsfälle](https://developer.twitter.com/en/use-cases/build-for-businesses) .

## [!DNL Twitter] Voraussetzungen und Leitlinien {#prerequisites}

Sie müssen über ein gültiges [!DNL Twitter] verfügen, um diese Erweiterung verwenden zu können. Navigieren Sie zur [[!DNL Twitter] Registrierungsseite](https://help.twitter.com/en/using-twitter/create-twitter-account), um sich zu registrieren und ein Konto zu erstellen, falls Sie noch keines haben.

Sie müssen Ihr -Konto als [!DNL Twitter]-Entwicklerkonto einrichten. Wie Sie sich als Entwickler anmelden, erfahren Sie im Abschnitt [[!DNL Twitter] Entwicklerkonto](https://developer.twitter.com/en/support/twitter-api/developer-account1).

### API-Leitplanken {#guardrails}

Die [!DNL Twitter] Web Conversions-API erlaubt eine Ratenbeschränkung von 60.000 Anfragen pro 15-Minuten-Intervall, wobei jede Anfrage 500 Ereignisse zulässt.

### Sammeln erforderlicher Konfigurationsdetails {#configuration-details}

Um den Experience Platform mit [!DNL Twitter] zu verbinden, sind die folgenden Eingaben erforderlich:

| Schlüsseltyp | Beschreibung |
| --- | --- |
| Consumer Key | &#x200B; Der API-Schlüssel der App für den Zugriff auf die [!DNL Twitter]-API. Eine Anleitung finden Sie in der [!DNL Twitter]-Dokumentation [API-Schlüssel und &#x200B;](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret)). |
| Verbrauchergeheimnis | Das API-Geheimnis ermöglicht Ihrer App den Zugriff auf die [!DNL Twitter]-API. Eine Anleitung finden Sie in der [!DNL Twitter]-Dokumentation [API-Schlüssel und &#x200B;](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret)). |
| Geheimer Token | Das nicht ablaufende Geheimnis-Token Ihrer App, das für die Authentifizierung bei der [!DNL Twitter]-API über OAuth verwendet wird. Eine Anleitung finden Sie in der [!DNL Twitter] Dokumentation [&#x200B; Abrufen von Zugriffstoken &#x200B;](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens) Benutzende . |
| Zugriffs-Token | Das nicht ablaufende Zugriffstoken Ihrer App, das für die Authentifizierung bei der [!DNL Twitter]-API über OAuth verwendet wird. Eine Anleitung finden Sie in der [!DNL Twitter] Dokumentation [&#x200B; Abrufen von Zugriffstoken &#x200B;](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens) Benutzende . |
| Pixel-ID | Das [!DNL Twitter] Pixel ist ein Website-Tag, das auf Ihrer Website implementiert wird, um Site-Aktionen oder Konversionen zu verfolgen. Eine Anleitung finden Sie in der [!DNL Twitter]-Dokumentation [Konversionsverfolgung für Websites](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html) . |

## Installieren und Konfigurieren der [!DNL Twitter] {#install}

Um die Erweiterung zu installieren[&#x200B; erstellen Sie eine Ereignisweiterleitungseigenschaft oder &#x200B;](../../../ui/event-forwarding/overview.md#properties) Sie stattdessen eine vorhandene Eigenschaft aus, die bearbeitet werden soll.

Wählen Sie **[!UICONTROL Erweiterungen]** in der linken Navigation aus. Wählen Sie auf der **[!UICONTROL Katalog]**-Registerkarte **[!UICONTROL Installieren]** auf der Karte für die [!DNL Twitter] aus.

![Katalog mit der [!DNL Twitter]-Erweiterung, in der install hervorgehoben ist.](../../../images/extensions/server/twitter/install.png)

>[!IMPORTANT]
>
>Je nach Ihren Implementierungsanforderungen müssen Sie möglicherweise ein Schema, Datenelemente und einen Datensatz erstellen, bevor Sie die Erweiterung konfigurieren. Bitte überprüfen Sie alle Konfigurationsschritte, bevor Sie beginnen, um festzustellen, welche Entitäten Sie für Ihren Anwendungsfall einrichten müssen.

Geben Sie im nächsten Bildschirm die folgenden [Konfigurationswerte](#configuration-details) ein, die Sie zuvor aus [!DNL Twitter] erfasst haben:

* **[!UICONTROL Pixel-ID]**
* **[!UICONTROL Consumer Key]**
* **[!UICONTROL Consumer Secret]**
* **[!UICONTROL Token]**
* **[!UICONTROL Token-Geheimnis]**

Klicken Sie abschließend auf **[!UICONTROL Speichern]**.

![[!DNL Twitter] Konfigurationsbildschirm für die [!DNL Twitter].](../../../images/extensions/server/twitter/configure.png)

## Konfigurieren einer Ereignisweiterleitungsregel {#config-rule}

Nachdem alle Datenelemente eingerichtet wurden, können Sie mit der Erstellung von Ereignisweiterleitungsregeln beginnen, die bestimmen, wann und wie Ihre Ereignisse an [!DNL Twitter] gesendet werden.

Erstellen Sie eine neue [Regel](../../../ui/managing-resources/rules.md) in Ihrer Ereignisweiterleitungs-Eigenschaft. Fügen Sie **[!UICONTROL Aktionen]** eine neue Aktion hinzu und legen Sie die Erweiterung auf **[!UICONTROL Twitter]** fest. Um Edge Network-Ereignisse an [!DNL Twitter] zu senden, setzen Sie **[!UICONTROL Aktionstyp]** auf **[!UICONTROL Web-Konversion senden].**

Nach der Auswahl erscheinen zusätzliche Steuerelemente, um das Ereignis weiter zu konfigurieren. Sie müssen die [!DNL Twitter] Ereigniseigenschaften den Datenelementen zuordnen, die Sie zuvor erstellt haben. Weitere Informationen finden Sie unter [[!DNL Twitter] Web Conversions-API](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions).

![Die [!DNL Twitter], die eine Konversionsereignisregel erstellt.](../../../images/extensions/server/twitter/action-configuration.png)

**[!UICONTROL Benutzeridentifizierung]**

| Feldname | Beschreibung | Beispiel | Erforderlich |
| --- | --- | --- | --- |
| [!UICONTROL [!DNL Twitter]-Klick-ID] | [!DNL Twitter] Klicken auf die ID, die von der Clickthrough-URL geparst wurde. | 26L6412G5P4IYJ65A2OIC2AYG2 | Erforderlich, wenn keine andere Kennung hinzugefügt wird. |
| [!UICONTROL E-Mail] | Eine mit SHA256 gehashte E-Mail-Adresse. Der Text muss in Kleinbuchstaben geschrieben werden, und alle nachfolgenden oder führenden Leerzeichen müssen vor dem Hashing entfernt werden. | eventforwarding@example.com | Erforderlich, wenn keine andere Kennung hinzugefügt wird. |
| [!UICONTROL Phone] | Telefon dient als Kennung für das Konversionsereignis. Die Telefonnummer muss im E164-Format [+][Ländercode][Vorwahl][local phone number] vor dem Hashing angegeben werden. | +911234567875 | Erforderlich, wenn keine andere Kennung hinzugefügt wird. |

**[!UICONTROL Konversionsdaten]**

| Feldname | Beschreibung | Beispiel | Erforderlich |
| --- | --- | --- | --- |
| [!UICONTROL Konvertierungszeit] | Datum-Uhrzeit als Zeichenfolge in ISO 8601 oder im `yyyy-MM-dd'T'HH:mm:ss:SSSZ`. | 2022-02-18T01:14:00.603Z | Ja |
| [!UICONTROL Ereignis-ID] | Die Base-36-ID eines bestimmten Ereignisses. Diese ID sollte mit einem vorkonfigurierten Ereignis übereinstimmen, das in Ihrem [!DNL Twitter]-Werbekonto enthalten ist. Dies wird als ID für das entsprechende Ereignis im Ereignis-Manager bezeichnet. | o87ne oder tw-o8z6j-o87ne (tw-pixel_id-event-id) | Ja |
| [!UICONTROL Anzahl der Elemente] | Die Anzahl der Artikel, die im Ereignis gekauft werden. Dies muss eine positive Zahl größer als 0 sein. | 4 | Nein |
| [!UICONTROL Währung] | Die Währung der Artikel, die im Ereignis gekauft werden. Dies wird in ISO-4217 ausgedrückt. Wenn dies nicht angegeben wird, lautet der Standardwert USD. | USD | Nein |
| [!UICONTROL Wert] | Der Preiswert der Artikel, die im Ereignis gekauft werden. | 100,00 | Nein |
| [!UICONTROL Konversions-ID] | Eine Kennung für ein Konversionsereignis, die für die Deduplizierung zwischen Web-Pixel- und Konversions-API-Konversionen im selben Ereignis-Tag verwendet werden kann. | 23294827 | Nein |
| [!UICONTROL Beschreibung] | Eine Beschreibung mit zusätzlichen Informationen zu den Konversionen. | Konvertierung testen | Nein |

## Validieren von Daten in [!DNL Twitter]

Überprüfen Sie nach der Erstellung und Ausführung der Ereignisweiterleitungsregel, ob das an die [!DNL Twitter]-API gesendete Ereignis wie erwartet in der [!DNL Twitter]-Benutzeroberfläche angezeigt wird.

Wenn die Ereignissammlung und [!DNL Experience Platform] Integration erfolgreich waren, werden Ereignisse im [!DNL Twitter]Ereignis-Manager[!UICONTROL &#x200B; angezeigt].

![Der [!DNL Twitter] Event Manager](../../../images/extensions/server/twitter/event-manager.png)

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie Konversionsereignisse mithilfe der Ereignisweiterleitung an [!DNL Twitter] senden. Weitere Informationen zu diesen zugrunde liegenden Technologien finden Sie in der offiziellen Dokumentation:

* [[!DNL Twitter] APIs](https://developer.twitter.com/en/docs/twitter-api)
* [[!DNL Twitter] Web-Konversions-API](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions)
* [[!DNL Twitter] Benutzerzugriffs-Token](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens)
* [Pixel-ID und Konversionsverfolgung](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html)
