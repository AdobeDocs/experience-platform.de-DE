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

[[!DNL Twitter]](https://twitter.com/i/flow/login) ist ein Online-Dienst für soziale Medien und soziale Netzwerke, bei dem Benutzer Nachrichten mit einer Länge von 280 Zeichen posten und mit ihnen interagieren, die als Tweets bezeichnet werden. Benutzer können über einen Browser, eine mobile Frontend-Software oder programmgesteuert mit Twitter interagieren [APIs](https://developer.twitter.com/en/docs/twitter-api)

Die [!DNL Twitter] Web Conversions API [Ereignisweiterleitung](../../../ui/event-forwarding/overview.md) -Erweiterung ermöglicht es Ihnen, die im Adobe Experience Platform Edge Network erfassten Daten zu nutzen und an [!DNL Twitter]. In diesem Dokument werden die Anwendungsfälle der Erweiterung, ihre Installation und die Integration ihrer Funktionen in die Ereignisweiterleitung behandelt. [Regeln](../../../ui/managing-resources/rules.md).

[!DNL Twitter] erfordert [OAuth 1.0](https://developer.twitter.com/en/docs/authentication/oauth-1-0a) für die Authentifizierung mit der [!DNL Twitter] [!DNL Web Conversions] API.

## Anwendungsfälle

Diese Erweiterung sollte verwendet werden, wenn Sie Daten aus dem Edge-Netzwerk in [!DNL Twitter] , um die Analyse- und Targeting-Funktionen der Kunden zu nutzen.

Betrachten Sie beispielsweise ein Marketing-Team in einer Organisation. Das Team erfasst Benutzerinteraktionsereignisdaten von seiner Website als Ereignisdaten von seiner Website und lädt sie in [!DNL Twitter] mit dieser Ereignisweiterleitungs-Erweiterung verwenden.

Die Marketing- und Analyseteams können dann [!DNL Twitter's] Funktionen zur Durchführung zusätzlicher Analysen und zur Ausrichtung dieser Benutzer auf zielgerichtete Werbekampagnen.

Weitere Informationen zu spezifischen Anwendungsfällen für [!DNL Twitter], siehe [[!DNL Twitter] Anwendungsfälle](https://developer.twitter.com/en/use-cases/build-for-businesses) Dokumentation.

## [!DNL Twitter] Voraussetzungen und Limits {#prerequisites}

Sie müssen über gültige [!DNL Twitter] , um diese Erweiterung zu verwenden. Navigieren Sie zu [[!DNL Twitter] Registrierungsseite](https://help.twitter.com/en/using-twitter/create-twitter-account) , um sich zu registrieren und ein Konto zu erstellen, falls Sie noch kein Konto haben.

Sie müssen Ihr Konto als [!DNL Twitter] Entwicklerkonto. Informationen zur Anmeldung als Entwickler finden Sie im Abschnitt [[!DNL Twitter] Entwicklerkonto](https://developer.twitter.com/en/support/twitter-api/developer-account1).

### API-Limits {#guardrails}

Die [!DNL Twitter] Die Web Conversions-API hat eine Ratenbegrenzung von 60.000 Anfragen pro 15-minütigen Intervall, wobei jede Anfrage 500 Ereignisse zulässt.

### Erforderliche Konfigurationsdetails sammeln {#configuration-details}

Um die Experience Platform an [!DNL Twitter], sind folgende Eingaben erforderlich:

| Schlüsseltyp | Beschreibung |
| --- | --- |
| Consumer Key | &#x200B; API-Schlüssel der App für den Zugriff auf die [!DNL Twitter] API. Siehe Abschnitt [!DNL Twitter] Dokumentation zu [API-Schlüssel und Geheimnisse](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret) für Leitlinien. | |
| Verbrauchergeheimnis | Der API-Geheimnis ermöglicht es Ihrer App, auf die [!DNL Twitter] API. Siehe Abschnitt [!DNL Twitter] Dokumentation zu [API-Schlüssel und Geheimnisse](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret) für Leitlinien. |
| Token-Geheimnis | Das nicht ablaufende Token-Geheimnis Ihrer App, das für die Authentifizierung bei der [!DNL Twitter] API über OAuth. Siehe Abschnitt [!DNL Twitter] Dokumentation zu [Verwenden von Zugriffstoken abrufen](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens) für Leitlinien. |
| Zugriffs-Token | Das nicht ablaufende Zugriffstoken Ihrer App, das zur Authentifizierung bei der [!DNL Twitter] API über OAuth. Siehe Abschnitt [!DNL Twitter] Dokumentation zu [Verwenden von Zugriffstoken abrufen](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens) für Leitlinien. |
| Pixel-ID | Die [!DNL Twitter] Pixel ist ein Website-Tag, das auf Ihrer Website implementiert wird, um Site-Aktionen oder -Konversionen zu verfolgen. Siehe Abschnitt [!DNL Twitter] Dokumentation zu [Konversions-Tracking für Websites](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html) für Leitlinien. |

## Installieren und konfigurieren Sie die [!DNL Twitter] Erweiterung {#install}

So installieren Sie die Erweiterung: [Erstellen einer Ereignisweiterleitungs-Eigenschaft](../../../ui/event-forwarding/overview.md#properties) oder wählen Sie eine vorhandene Eigenschaft aus, die Sie stattdessen bearbeiten möchten.

Wählen Sie **[!UICONTROL Erweiterungen]** in der linken Navigation aus. Im **[!UICONTROL Katalog]** Registerkarte auswählen **[!UICONTROL Installieren]** auf der Karte für die [!DNL Twitter] -Erweiterung.

![Katalog, der die [!DNL Twitter] Erweiterungsmarkierungsinstallation.](../../../images/extensions/server/twitter/install.png)

>[!IMPORTANT]
>
>Je nach Ihren Implementierungsanforderungen müssen Sie möglicherweise ein Schema, Datenelemente und einen Datensatz erstellen, bevor Sie die Erweiterung konfigurieren. Bitte überprüfen Sie alle Konfigurationsschritte, bevor Sie beginnen, um festzustellen, welche Entitäten Sie für Ihren Anwendungsfall einrichten müssen.

Geben Sie im nächsten Bildschirm Folgendes ein: [Konfigurationswerte](#configuration-details) die Sie zuvor aus [!DNL Twitter]:

* **[!UICONTROL Pixel-ID]**
* **[!UICONTROL Consumer Key]**
* **[!UICONTROL Verbrauchergeheimnis]**
* **[!UICONTROL Token]**
* **[!UICONTROL Token-Geheimnis]**

Klicken Sie abschließend auf **[!UICONTROL Speichern]**.

![[!DNL Twitter] Konfigurationsbildschirm für [!DNL Twitter] -Erweiterung.](../../../images/extensions/server/twitter/configure.png)

## Konfigurieren einer Ereignisweiterleitungsregel {#config-rule}

Sobald alle Ihre Datenelemente eingerichtet sind, können Sie mit der Erstellung von Ereignisweiterleitungsregeln beginnen, die bestimmen, wann und wie Ihre Ereignisse an gesendet werden [!DNL Twitter].

Erstellen Sie eine neue [Regel](../../../ui/managing-resources/rules.md) in Ihrer Ereignisweiterleitungseigenschaft. under **[!UICONTROL Aktionen]**, fügen Sie eine neue Aktion hinzu und legen Sie die Erweiterung auf **[!UICONTROL Twitter]**. So senden Sie Edge Network-Ereignisse an [!DNL Twitter], legen Sie die **[!UICONTROL Aktionstyp]** nach **[!UICONTROL Web-Konversion senden].**

Nach der Auswahl scheinen zusätzliche Steuerelemente das Ereignis weiter zu konfigurieren. Sie müssen die [!DNL Twitter] Ereigniseigenschaften zu den zuvor erstellten Datenelementen hinzufügen. Weitere Informationen finden Sie im Abschnitt [[!DNL Twitter] Web Conversions API](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions).

![Die [!DNL Twitter] Erstellen einer Konversionsereignisregel.](../../../images/extensions/server/twitter/action-configuration.png)

**[!UICONTROL Benutzeridentifizierung]**

| Feldname | Beschreibung | Beispiel | Erforderlich |
| --- | --- | --- | --- |
| [!UICONTROL [!DNL Twitter] Klick-ID] | [!DNL Twitter] Klick-ID wie von der Clickthrough-URL analysiert. | 26l6412g5p4iyj65a2oic2ayg2 | Erforderlich, wenn keine andere Kennung hinzugefügt wird. |
| [!UICONTROL E-Mail] | Eine mit SHA256 gehashte E-Mail-Adresse. Der Text muss in Kleinbuchstaben geschrieben werden und alle nachfolgenden oder führenden Leerzeichen müssen vor dem Hashing entfernt werden. | eventforwarding@example.com | Erforderlich, wenn keine andere Kennung hinzugefügt wird. |
| [!UICONTROL Phone] | Phone dient als ID zum Abgleich des Konversionsereignisses. Die Telefonnummer muss das Format E164 aufweisen [+][Ländercode].[Bereichscode][local phone number] vor dem Hashing. | +911234567875 | Erforderlich, wenn keine andere Kennung hinzugefügt wird. |

**[!UICONTROL Konversionsdaten]**

| Feldname | Beschreibung | Beispiel | Erforderlich |
| --- | --- | --- | --- |
| [!UICONTROL Konvertierungszeit] | Datum/Uhrzeit als Zeichenfolge in ISO 8601 oder in `yyyy-MM-dd'T'HH:mm:ss:SSSZ` Format. | 2022-02-18T01:14:00.603 Z | Ja |
| [!UICONTROL Ereignis-ID] | Die base-36-ID eines bestimmten Ereignisses. Diese ID sollte mit einem vorkonfigurierten Ereignis übereinstimmen, das in Ihrer [!DNL Twitter] Anzeigenkonto. Dies wird als ID für das entsprechende Ereignis im Ereignismanager bezeichnet. | o87ne oder tw-o8z6j-o87ne (tw-pixel_id-event-id) | Ja |
| [!UICONTROL Anzahl der Elemente] | Die Anzahl der Artikel, die im Ereignis gekauft werden. Hierbei muss es sich um eine positive Zahl größer als 0 handeln. | 4 | Nein |
| [!UICONTROL Währung] | Die Währung der Artikel, die im Ereignis gekauft werden. Dies wird in ISO-4217 ausgedrückt und falls nicht angegeben, ist der Standardwert USD. | USD | Nein |
| [!UICONTROL Wert] | Der Preiswert der Artikel, die im Ereignis gekauft werden. | 100,00 | Nein |
| [!UICONTROL Konversions-ID] | Ein Bezeichner für ein Konversionsereignis, das zur Deduplizierung zwischen Web-Pixel- und Konversions-API-Konvertierungen im selben Ereignis-Tag verwendet werden kann. | 23294827 | Nein |
| [!UICONTROL Beschreibung] | Eine Beschreibung mit zusätzlichen Informationen zu den Konvertierungen. | Testkonversion | Nein |

## Validieren von Daten in [!DNL Twitter]

Überprüfen Sie nach der Erstellung und Ausführung der Ereignisweiterleitungsregel, ob das Ereignis, das an die [!DNL Twitter] Die API wird wie erwartet im [!DNL Twitter] Benutzeroberfläche.

Wenn die Ereigniskollektion und [!DNL Experience Platform] -Integration erfolgreich war, werden Ereignisse im [!DNL Twitter] [!UICONTROL Ereignismanager].

![Die [!DNL Twitter] Ereignismanager](../../../images/extensions/server/twitter/event-manager.png)

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Konversionsereignisse an gesendet werden [!DNL Twitter] über die Ereignisweiterleitung. Weitere Informationen zu diesen Technologien finden Sie in der offiziellen Dokumentation:

* [[!DNL Twitter] APIs](https://developer.twitter.com/en/docs/twitter-api)
* [[!DNL Twitter] Web Conversion API](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions)
* [[!DNL Twitter] Benutzerzugriffs-Token](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens)
* [Pixel-ID und Konversions-Tracking](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html)
