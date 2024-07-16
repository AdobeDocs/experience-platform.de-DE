---
keywords: Ereignisweiterleitungs-Erweiterung;twitter;twitter-Ereignisweiterleitungs-Erweiterung
title: Twitter-Ereignisweiterleitungs-Erweiterung
description: Mit dieser Ereignisweiterleitungs-Erweiterung von Adobe Experience Platform können Sie für Ihre Geschäftsanforderungen Ereignisse in Twitter aufnehmen.
last-substantial-update: 2023-05-24T00:00:00Z
exl-id: 54c240e5-6160-4654-ac5b-6afa8d99a765
source-git-commit: 4ee895cb8371646fd2013e2a8f65c2ffdae95850
workflow-type: tm+mt
source-wordcount: '1048'
ht-degree: 7%

---

# [!DNL Twitter]-Erweiterung zur Ereignisweiterleitung

[[!DNL Twitter]](https://twitter.com/i/flow/login) ist ein Online-Dienst für soziale Netzwerke und soziale Netzwerke, auf dem Benutzer Nachrichten mit einer Länge von 280 Zeichen posten und mit ihnen interagieren, die als Tweets bezeichnet werden. Benutzer können mit Twitter über einen Browser, eine mobile Frontend-Software oder programmgesteuert über ihre [APIs](https://developer.twitter.com/en/docs/twitter-api) interagieren

Mit der Erweiterung [!DNL Twitter] Web Conversions API [event forward](../../../ui/event-forwarding/overview.md) können Sie die im Adobe Experience Platform-Edge Network erfassten Daten nutzen und an [!DNL Twitter] senden. In diesem Dokument werden die Anwendungsfälle der Erweiterung, ihre Installation und die Integration ihrer Funktionen in die Ereignisweiterleitung von [Regeln](../../../ui/managing-resources/rules.md) behandelt.

[!DNL Twitter] erfordert [OAuth 1.0](https://developer.twitter.com/en/docs/authentication/oauth-1-0a) für die Authentifizierung mit der [!DNL Twitter] [!DNL Web Conversions]-API.

## Anwendungsfälle

Diese Erweiterung sollte verwendet werden, wenn Sie Daten aus dem Edge Network in [!DNL Twitter] verwenden möchten, um die Analyse- und Targeting-Funktionen von Kunden nutzen zu können.

Betrachten Sie beispielsweise ein Marketing-Team in einer Organisation. Das Team erfasst Benutzerinteraktionsereignisdaten von seiner Website als Ereignisdaten von seiner Website und lädt sie mithilfe dieser Ereignisweiterleitungs-Erweiterung in [!DNL Twitter].

Die Marketing- und Analyseteams können dann die [!DNL Twitter's]-Funktionen nutzen, um zusätzliche Analysen durchzuführen und diese Benutzer für gezielte Werbekampagnen anzusprechen.

Weitere Informationen zu [!DNL Twitter] spezifischen Anwendungsfällen finden Sie in der Dokumentation zu [[!DNL Twitter] Anwendungsfällen](https://developer.twitter.com/en/use-cases/build-for-businesses) .

## [!DNL Twitter] Voraussetzungen und Limits {#prerequisites}

Sie müssen über ein gültiges [!DNL Twitter] -Konto verfügen, um diese Erweiterung verwenden zu können. Rufen Sie die [[!DNL Twitter] Registrierungsseite](https://help.twitter.com/en/using-twitter/create-twitter-account) auf, um sich zu registrieren und ein Konto zu erstellen, falls noch keines vorhanden ist.

Sie müssen Ihr Konto als [!DNL Twitter] -Entwicklerkonto einrichten. Informationen zur Anmeldung als Entwickler finden Sie im [[!DNL Twitter] Entwicklerkonto](https://developer.twitter.com/en/support/twitter-api/developer-account1).

### API-Limits {#guardrails}

Die [!DNL Twitter] Web Conversions-API hat eine Quotenbegrenzung von 60.000 Anfragen pro 15-minütigen Intervall, wobei jede Anfrage 500 Ereignisse zulässt.

### Erforderliche Konfigurationsdetails sammeln {#configuration-details}

Um die Experience Platform mit [!DNL Twitter] zu verbinden, sind die folgenden Eingaben erforderlich:

| Schlüsseltyp | Beschreibung |
| --- | --- |
| Consumer Key | &#x200B; Der API-Schlüssel der App für den Zugriff auf die [!DNL Twitter]-API. Eine Anleitung dazu finden Sie in der Dokumentation zu [!DNL Twitter] für [api-Schlüssel und Geheimnisse](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret) . | |
| Verbrauchergeheimnis | Mit dem API-Geheimnis kann Ihre App auf die [!DNL Twitter] -API zugreifen. Eine Anleitung dazu finden Sie in der Dokumentation zu [!DNL Twitter] für [api-Schlüssel und Geheimnisse](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret) . |
| Token-Geheimnis | Das nicht ablaufende Token-Geheimnis Ihrer App, das zur Authentifizierung bei der [!DNL Twitter]-API über OAuth verwendet wird. Eine Anleitung dazu finden Sie in der Dokumentation zu [!DNL Twitter] unter [Abrufen von Anwendungs-Zugriffstoken](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens) . |
| Zugriffs-Token | Das nicht ablaufende Zugriffstoken Ihrer App, das zur Authentifizierung bei der [!DNL Twitter]-API über OAuth verwendet wird. Eine Anleitung dazu finden Sie in der Dokumentation zu [!DNL Twitter] unter [Abrufen von Anwendungs-Zugriffstoken](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens) . |
| Pixel-ID | Das Pixel [!DNL Twitter] ist ein Website-Tag, das auf Ihrer Website implementiert wird, um Site-Aktionen oder -Konversionen zu verfolgen. Eine Anleitung dazu finden Sie in der [!DNL Twitter] -Dokumentation zum [Konversions-Tracking für Websites](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html) . |

## Installieren und Konfigurieren der [!DNL Twitter] -Erweiterung {#install}

Um die Erweiterung zu installieren, erstellen Sie [eine Ereignisweiterleitungs-Eigenschaft](../../../ui/event-forwarding/overview.md#properties) oder wählen Sie eine vorhandene Eigenschaft aus, die Sie stattdessen bearbeiten möchten.

Wählen Sie **[!UICONTROL Erweiterungen]** in der linken Navigation aus. Wählen Sie auf der Registerkarte **[!UICONTROL Katalog]** die Option **[!UICONTROL Installieren]** auf der Karte für die Erweiterung [!DNL Twitter] aus.

![Katalog, der die Installation der [!DNL Twitter]-Erweiterung hervorhebt.](../../../images/extensions/server/twitter/install.png)

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

![[!DNL Twitter] Konfigurationsbildschirm für die [!DNL Twitter] Erweiterung.](../../../images/extensions/server/twitter/configure.png)

## Konfigurieren einer Ereignisweiterleitungsregel {#config-rule}

Sobald alle Ihre Datenelemente eingerichtet sind, können Sie mit der Erstellung von Ereignisweiterleitungsregeln beginnen, die bestimmen, wann und wie Ihre Ereignisse an [!DNL Twitter] gesendet werden.

Erstellen Sie eine neue [Regel](../../../ui/managing-resources/rules.md) in Ihrer Ereignisweiterleitungseigenschaft. Fügen Sie unter **[!UICONTROL Aktionen]** eine neue Aktion hinzu und legen Sie die Erweiterung auf **[!UICONTROL Twitter]** fest. Um Edge Network-Ereignisse an [!DNL Twitter] zu senden, setzen Sie den **[!UICONTROL Aktionstyp]** auf **[!UICONTROL Web-Konversion senden].**

Nach der Auswahl scheinen zusätzliche Steuerelemente das Ereignis weiter zu konfigurieren. Sie müssen die [!DNL Twitter] -Ereigniseigenschaften den zuvor erstellten Datenelementen zuordnen. Weitere Informationen finden Sie in der [[!DNL Twitter] Web Conversions API](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions).

![Der [!DNL Twitter], der eine Konversionsereignisregel erstellt.](../../../images/extensions/server/twitter/action-configuration.png)

**[!UICONTROL Benutzeridentifizierung]**

| Feldname | Beschreibung | Beispiel | Erforderlich |
| --- | --- | --- | --- |
| [!UICONTROL [!DNL Twitter] Klick-ID] | [!DNL Twitter] Klick-ID, wie aus der Clickthrough-URL analysiert. | 26l6412g5p4iyj65a2oic2ayg2 | Erforderlich, wenn keine andere Kennung hinzugefügt wird. |
| [!UICONTROL E-Mail] | Eine mit SHA256 gehashte E-Mail-Adresse. Der Text muss in Kleinbuchstaben geschrieben werden und alle nachfolgenden oder führenden Leerzeichen müssen vor dem Hashing entfernt werden. | eventforwarding@example.com | Erforderlich, wenn keine andere Kennung hinzugefügt wird. |
| [!UICONTROL Phone] | Phone dient als ID zum Abgleich des Konversionsereignisses. Die Telefonnummer muss im E164-Format [+][Ländercode][Bereichscode][local phone number] vorliegen, bevor ein Hashing erfolgt. | +911234567875 | Erforderlich, wenn keine andere Kennung hinzugefügt wird. |

**[!UICONTROL Konversionsdaten]**

| Feldname | Beschreibung | Beispiel | Erforderlich |
| --- | --- | --- | --- |
| [!UICONTROL Konvertierungszeit] | Datum/Uhrzeit als Zeichenfolge im ISO 8601- oder im `yyyy-MM-dd'T'HH:mm:ss:SSSZ`-Format. | 2022-02-18T01:14:00.603Z | Ja |
| [!UICONTROL Ereignis-ID] | Die base-36-ID eines bestimmten Ereignisses. Diese ID sollte mit einem vorkonfigurierten Ereignis übereinstimmen, das in Ihrem [!DNL Twitter] -Anzeigenkonto enthalten ist. Dies wird als ID für das entsprechende Ereignis im Ereignismanager bezeichnet. | o87ne oder tw-o8z6j-o87ne (tw-pixel_id-event-id) | Ja |
| [!UICONTROL Anzahl der Elemente] | Die Anzahl der Artikel, die im Ereignis gekauft werden. Hierbei muss es sich um eine positive Zahl größer als 0 handeln. | 4 | Nein |
| [!UICONTROL Währung] | Die Währung der Artikel, die im Ereignis gekauft werden. Dies wird in ISO-4217 ausgedrückt und falls nicht angegeben, ist der Standardwert USD. | USD | Nein |
| [!UICONTROL Wert] | Der Preiswert der Artikel, die im Ereignis gekauft werden. | 100,00 | Nein |
| [!UICONTROL Konversions-ID] | Ein Bezeichner für ein Konversionsereignis, das zur Deduplizierung zwischen Web-Pixel- und Konversions-API-Konvertierungen im selben Ereignis-Tag verwendet werden kann. | 23294827 | Nein |
| [!UICONTROL Beschreibung] | Eine Beschreibung mit zusätzlichen Informationen zu den Konvertierungen. | Testkonversion | Nein |

## Daten mit [!DNL Twitter] validieren

Sobald die Ereignisweiterleitungsregel erstellt und ausgeführt wurde, überprüfen Sie, ob das Ereignis, das an die [!DNL Twitter] -API gesendet wurde, wie erwartet in der Benutzeroberfläche von [!DNL Twitter] angezeigt wird.

Wenn die Ereigniserfassung und die Integration von [!DNL Experience Platform] erfolgreich waren, werden Ereignisse im [!DNL Twitter] [!UICONTROL Ereignismanager] angezeigt.

![Der [!DNL Twitter] Ereignismanager](../../../images/extensions/server/twitter/event-manager.png)

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Konversionsereignisse mithilfe der Ereignisweiterleitung an [!DNL Twitter] gesendet werden. Weitere Informationen zu diesen Technologien finden Sie in der offiziellen Dokumentation:

* [[!DNL Twitter] APIs](https://developer.twitter.com/en/docs/twitter-api)
* [[!DNL Twitter] Web-Konversions-API](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions)
* [[!DNL Twitter] Benutzerzugriffs-Token](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens)
* [Pixel-ID und Konversions-Tracking](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html)
