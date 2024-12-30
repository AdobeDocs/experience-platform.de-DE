---
keywords: -Erweiterung für die Ereignisweiterleitung;pinterest;pinterest-Erweiterung für die Ereignisweiterleitung
title: Pinterest-Ereignisweiterleitungserweiterung
description: Mit dieser Adobe Experience Platform-Ereignisweiterleitungserweiterung können Sie für Ihre Geschäftsanforderungen Ereignisse in Pinterest aufnehmen.
last-substantial-update: 2023-04-27T00:00:00Z
exl-id: 44f38a9b-0a28-4b51-bead-ee460eb8405e
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '1478'
ht-degree: 6%

---

# [!DNL Pinterest]-Erweiterung zur Ereignisweiterleitung

[!DNL Pinterest] ist eine visuelle Discovery-Engine zum Finden von Ideen wie Rezepten, Wohnkultur, Stilinspiration und mehr. Es gibt Milliarden von Pins auf [!DNL Pinterest], die auch mit anderen auf [!DNL Pinterest] geteilt werden können. Sie können die Benutzerinteraktionsereignisse zusammenstellen und [!DNL Pinterest Analytics] nutzen, um das Benutzerverhalten zu verstehen und zielgerichtete Anzeigen auszuführen.

Mit der [[!DNL Pinterest] Conversions](https://developers.pinterest.com/docs/conversions/conversion-management/)-API [Ereignisweiterleitung](../../../ui/event-forwarding/overview.md) können Sie die im Adobe Experience Platform-Edge Network erfassten Daten nutzen und an [!DNL Pinterest] senden. In diesem Dokument werden die Anwendungsfälle der Erweiterung, deren Installation und die Integration der Funktionen in die Ereignisweiterleitung ([) ](../../../ui/managing-resources/rules.md).

Konversionen-Zugriffstoken sind die Authentifizierungsmethode, die von [!DNL Pinterest] bei der Interaktion mit der [!DNL Pinterest]-API verwendet wird.

## Anwendungsfälle

Diese Erweiterung sollte verwendet werden, wenn Sie Daten aus dem Edge Network verwenden möchten, [!DNL Pinterest] die Kundenanalysefunktionen von zu nutzen.

Betrachten Sie beispielsweise ein Marketing-Team in einer Organisation. Das Team erfasst Ereignisdaten zu Benutzerinteraktionen von seiner Website und lädt sie mithilfe dieser Erweiterung zur Ereignisweiterleitung in [!DNL Pinterest].

Die Marketing- und Analyse-Teams können dann [!DNL Pinterest] Analytics-Funktionen nutzen, um wichtige Benutzerinteraktionen und -verhaltensweisen zu verstehen, sodass Sie Benutzer besser verstehen und sie für zielgerichtete Anzeigenkampagnen ansprechen können.

Weitere Informationen zu [!DNL Pinterest]-spezifischen Anwendungsfällen finden Sie in der Dokumentation [[!DNL Pinterest] Anwendungsfälle](https://business.pinterest.com/en/success-stories) .

## Voraussetzungen für [!DNL Pinterest] {#prerequisites}

Sie müssen über ein gültiges [!DNL Pinterest]Geschäftskonto[ verfügen](https://help.pinterest.com/en/business/article/get-a-business-account) um diese Erweiterung verwenden zu können. Navigieren Sie zur [[!DNL Pinterest] Registrierungsseite](https://www.pinterest.com/business/create/), um sich zu registrieren und ein Konto zu erstellen, falls Sie noch keines haben.

Sie benötigen außerdem ein [!DNL Pinterest] Entwicklerkonto, das mit Ihrem [!DNL Pinterest] Business-Konto verknüpft werden muss. Informationen zum Verknüpfen Ihres Entwicklerkontos mit Ihrem Geschäftskonto finden Sie unter [[!DNL Pinterest ] Entwicklerkonto](https://developers.pinterest.com/account-setup/).

### Sammeln erforderlicher Konfigurationsdetails {#configuration-details}

Um die Experience Platform an [!DNL Pinterest] anzuschließen, sind folgende Eingänge erforderlich:

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| Werbekonto-ID | Ihre [!DNL Pinterest] Ads-Konto-ID. Eine Anleitung finden Sie in der [[!DNL Pinterest] Dokumentation](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager). | 123456789012 |
| Konversionszugriffstoken | Ihr [!DNL Pinterest]-Konversions-Zugriffstoken. Eine Anleitung dazu finden [[!DNL Pinterest]  im Dokument ](https://developers.pinterest.com/docs/conversions/conversions/#Get%20the%20conversion%20token)Konversions-API“. <br> **Sie müssen dies nur einmal tun, da dieses Token nicht abläuft.** | {YOUR_PINTEREST_BEARER_TOKEN} |

## Installieren und Konfigurieren der [!DNL Pinterest] {#install}

Um die Erweiterung zu installieren[ erstellen Sie eine Ereignisweiterleitungseigenschaft oder ](../../../ui/event-forwarding/overview.md#properties) Sie stattdessen eine vorhandene Eigenschaft aus, die bearbeitet werden soll.

Wählen Sie in der linken Navigation **[!UICONTROL Erweiterungen]** aus. Wählen **[!UICONTROL auf]** Karte für die [!DNL Pinterest] Erweiterung auf der Registerkarte **[!UICONTROL Katalog]** aus.

![Katalog mit hervorgehobener [!DNL Pinterest]-Erweiterung [!UICONTROL Installieren].](../../../images/extensions/server/pinterest/install.png)

### [!DNL Pinterest]-Erweiterung konfigurieren

>[!IMPORTANT]
>
>Je nach Ihren Implementierungsanforderungen müssen Sie möglicherweise ein Schema, Datenelemente und einen Datensatz erstellen, bevor Sie die Erweiterung konfigurieren. Bitte überprüfen Sie alle Konfigurationsschritte, bevor Sie beginnen, um festzustellen, welche Entitäten Sie für Ihren Anwendungsfall einrichten müssen.

Wählen Sie in der linken Navigation **[!UICONTROL Erweiterungen]** aus. Wählen **[!UICONTROL auf]** Karte für die [!DNL Pinterest] Erweiterung auf der Registerkarte [!UICONTROL Installiert] aus**.

![[!DNL Pinterest] Erweiterung, die auf der Registerkarte [!UICONTROL Installieren] angezeigt wird, mit [!UICONTROL  hervorgehobenen ] „Konfigurieren“](../../../images/extensions/server/pinterest/configure.png)

Geben Sie im nächsten Bildschirm die [!UICONTROL Anzeigen-Konto-ID] und [!UICONTROL Konversionszugriffs-Token] ein, die Sie zuvor im Abschnitt [Konfigurationsdetails](#configuration-details) erfasst haben. Klicken Sie abschließend auf **[!UICONTROL Speichern]**.

![Der Bildschirm [!DNL Pinterest] [!UICONTROL Konfigurieren] in dem die Eingabefelder [!UICONTROL Anzeigen-Konto-ID] und [!UICONTROL Konversionszugriffs-Token] hervorgehoben sind.](../../../images/extensions/server/pinterest/input.png)

## Konfigurieren einer Ereignisweiterleitungsregel {#config-rule}

Nachdem alle Datenelemente eingerichtet wurden, können Sie mit der Erstellung von Ereignisweiterleitungsregeln beginnen, die bestimmen, wann und wie Ihre Ereignisse an [!DNL Pinterest] gesendet werden.

Erstellen Sie eine neue [Regel](../../../ui/managing-resources/rules.md) in Ihrer Ereignisweiterleitungs-Eigenschaft. Fügen **[!UICONTROL unter „Aktionen]** eine neue Aktion hinzu und legen Sie die Erweiterung auf **[!UICONTROL Pinterest]** fest. Edge Network Um Ereignisereignisse an [!DNL Pinterest] zu senden, setzen Sie **[!UICONTROL Aktionstyp]** auf **[!UICONTROL Ereignis senden].**

![Die [!DNL Pinterest] [!UICONTROL Ereignis senden] Regelerstellung.](../../../images/extensions/server/pinterest/rule.png)

Nach der Auswahl erscheinen zusätzliche Steuerelemente, um das Ereignis weiter zu konfigurieren. Sie müssen die [!DNL Pinterest] Ereigniseigenschaften den Datenelementen zuordnen, die Sie zuvor erstellt haben.

### [!UICONTROL Ereignisdaten]

Zum Erstellen der neuen Regel sind die folgenden Ereignisdaten erforderlich:

| Feldname | Beschreibung | Beispiel |
| --- | --- | --- | 
| [!UICONTROL Ereignisname] | Der Typ des Benutzerereignisses. Dies kann ein beliebiger Ereignistyp sein. Zur Nutzung [!DNL Pinterest Analytics] wird jedoch die Verwendung von [[!DNL Pinterest] Ereignis-Codes“ ](https://help.pinterest.com/en/business/article/add-event-codes) | * Checkout <br> * add_to_cart <br> * page_visit <br> * <br> * [Benutzerdefiniertes Ereignis] |
| [!UICONTROL Action Source] | Die Quelle, die angibt, wo das Konversionsereignis aufgetreten ist. | * app_android <br> * app_ios <br> * <br> * offline |
| [!UICONTROL Ereigniszeit] | Dies bezieht sich auf die Ereigniszeit. Das standardmäßig verwendete Zeitformat ist UNIX und das Format `<seconds>.<miliseconds>` abhängig von Ihrer lokalen Zeitzone. Weitere Informationen finden Sie unter [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/#operation/events/create). | 1433188255.500 gibt 1433188255 Sekunden und 500 Millisekunden nach Epoche oder Montag, den 1. Juni 2015, um 19:50:55 Uhr GMT an. |
| [!UICONTROL Ereignis-ID] | Eine eindeutige ID-Zeichenfolge, die dieses Ereignis identifiziert und für die Deduplizierung zwischen Ereignissen verwendet werden kann, die sowohl über die Konversions-API als auch über das Pinterest-Tracking aufgenommen werden. Andernfalls werden die Daten des Ereignisses wahrscheinlich doppelt gezählt und eine metrische Inflation gemeldet. | BA7816BF8F01CFEA414140DE5DAE2223B00361A396177A9CB410FF61F20015AD |
| [!UICONTROL Ereigniseigenschaften] | Ein JSON-Objekt mit benutzerdefinierten Eigenschaften des Ereignisses. Wählen Sie aus der Bereitstellung von unformatiertem JSON oder der Verwendung eines vereinfachten Satzes von Schlüssel-Wert-Eingaben. | { „event_source_url“: &quot;http://site.com&quot; } |

![Die [!DNL Pinterest] [!UICONTROL Ereignisdaten] in der Regelaktion hervorgehoben.](../../../images/extensions/server/pinterest/event-data.png)

Die folgenden Ereigniseigenschaften können konfiguriert werden:

| Feldname | Beschreibung |
| --- | --- |
| Event Source URL | URL des Web-Konversionsereignisses. |
| Kennung des Anwendungsspeichers | Die App Store-App-ID. |
| Anwendungsname | Der Name des Programms. |
| Application Version | Die Version des Programms. |
| Gerätemarke | Marke des Geräts, das vom Benutzer verwendet wird. |
| Geräteträger | Mobilnetzbetreiber des Benutzers für sein Gerät. |
| Gerätemodell | Modell des Geräts des Benutzers. |
| Device Type | Gerätetyp, der vom Benutzer verwendet wird. |
| Betriebssystemversion | Version des Betriebssystems des Geräts. |
| Benutzersprache | Zweistelliger ISO-639-1-Sprach-Code, der die Sprache des Benutzers angibt. |

### [!UICONTROL Benutzerdaten]

Die folgenden Benutzerdaten können über Felder eingegeben werden, die nicht erforderlich sind:

| Feldname | Beschreibung | Beispiel |
| --- | --- | --- | 
| [!UICONTROL E-Mail] | Benutzer-E-Mail-Adresse oder ein SHA256-Hash der Benutzer-E-Mail-Adresse. | EBD543592…F2B7E1 |
| [!UICONTROL Mobile Advertising-IDs] | SHA256-Hashes der &quot;Google Advertising IDs“ (GAIDs) oder &quot;Apple-Kennung für Werbetreibende“ (IDFAs) von Benutzenden | EBD543592…F2B7E1 |
| [!UICONTROL Client-IP-Adresse] | Die IP-Adresse des Benutzers, die entweder im IPv4- oder IPv6-Format vorliegen kann. Wird für den Abgleich verwendet. | 192.168.0.1 |
| [!UICONTROL Client-Benutzeragent] | Die Benutzeragenten-Zeichenfolge des Webbrowsers des Benutzers. | Mozilla/5.0 (platform; rv:geckoversion) Gecko/geckotrail Firefox/firefoxversion |
| [!UICONTROL Kundeninformationsdaten] | Ein JSON-Objekt, das andere Kundeninformationen enthält. Wählen Sie aus der Bereitstellung von unformatiertem JSON oder der Verwendung eines vereinfachten Satzes von Schlüssel-Wert-Eingaben. | { „ph“: „122333445“ } |

![Die [!DNL Pinterest] [!UICONTROL Benutzerdaten] in der Regelaktion hervorgehoben.](../../../images/extensions/server/pinterest/user-data.png)

Zu den Kundeninformationseigenschaften, die konfiguriert werden können, gehören:

| Feldname | Beschreibung |
| --- | --- |
| Telefon | Kontaktnummer des Benutzers Nur Ziffern werden akzeptiert und sollten mit Ländercode, Vorwahl und Nummer eingegeben werden. |
| Geschlecht | Das Geschlecht kann entweder als „f“ für weiblich, „m“ für männlich oder „n“ für nicht-binär eingegeben werden. |
| Geburtsdatum | Geburtsdatum, eingegeben als Jahr, Monat und Tag. |
| Nachname | Nachname des Benutzers. |
| Vorname | Vorname des Benutzers. |
| Stadt | Wohnort des Benutzers. Dies wird hauptsächlich für Abrechnungszwecke verwendet. |
| Land | Benutzerstatus, der als Code mit zwei Buchstaben in Kleinbuchstaben bereitgestellt wird. |
| Postleitzahl | Postleitzahl des Benutzers, die hauptsächlich zu Abrechnungszwecken verwendet wird. |
| Land | Zweistelliger ISO-3166-Ländercode, der das Land des Benutzers angibt. |
| Externe ID | Eindeutige ID des Advertisers, der einen Benutzer in seiner Platzierung identifiziert. Beispielsweise Benutzer-ID, Treueprogramm-ID usw. |
| Klick-ID | Die eindeutige Kennung, die im _epik-Cookie in Ihrer Domain oder im &amp;epik=-Abfrageparameter in der URL gespeichert ist. |

>[!IMPORTANT]
>
>Bevor die Daten an den [!DNL Pinterest]-API-Endpunkt gesendet werden, hasht und normalisiert die Erweiterung die Werte der folgenden Felder: E-Mail, Telefonnummer, Vorname, Nachname, Geschlecht, Geburtsdatum, Stadt, Bundesland, Postleitzahl, Land und externe ID. Die Erweiterung hasht den Wert dieser Felder nicht, wenn bereits eine SHA256-Zeichenfolge vorhanden ist.

### [!UICONTROL Benutzerdefinierte Daten]

Die folgenden benutzerdefinierten Daten können für die Regel eingegeben werden:

| Feldname | Beschreibung |
| --- | --- |
| Währung | Der ISO-4217-Währungscode. Wenn dies nicht angegeben wird, verwendet [!DNL Pinterest] standardmäßig die Währung des Advertisers, die bei der Kontoerstellung festgelegt wurde. |
| Wert | Gesamtwert des Ereignisses. Akzeptiert als Zeichenfolge in der Anfrage. Dies wird in eine zweistellige Zahl geparst. |
| Suchzeichenfolge | Die Suchzeichenfolge für das Benutzerkonversionsereignis. |
| Auftrags-ID | Die Auftrags-ID. Das Senden von `order_id` hilft bei [!DNL Pinterest] Deduplizierung von Ereignissen. |
| Anzahl der Produkte | Gesamtzahl der Produkte der Veranstaltung. Beispielsweise die Gesamtzahl der in einem Checkout-Ereignis gekauften Artikel. |
| Inhalts-IDs | Liste (Array) der Produkt-IDs. |
| Inhalt | Eine Liste (Array) von Objekten, die Informationen über Produkte enthalten, z. B. Preis und Menge. |

![Die [!DNL Pinterest] [!UICONTROL Benutzerdefinierte Daten] die in der Regelaktion hervorgehoben wird.](../../../images/extensions/server/pinterest/custom-data.png)

## Validieren von Daten in [!DNL Pinterest]

Überprüfen Sie nach der Erstellung und Ausführung der Ereignisweiterleitungsregel, ob das an die [!DNL Pinterest]-API gesendete Ereignis wie erwartet in der [!DNL Pinterest]-Benutzeroberfläche angezeigt wird.

Wenn die Ereignissammlung und [!DNL Experience Platform] Integration erfolgreich waren, werden Ereignisse in der [!DNL Pinterest] Benutzeroberfläche angezeigt.

![Der [!DNL Pinterest] Event Manager](../../../images/extensions/server/pinterest/event-history.png)

Sie können die [!DNL Pinterest] Ereignisdatenverteilung weiter aufschlüsseln und anzeigen.

![Die [!DNL Pinterest] Datenverteilung](../../../images/extensions/server/pinterest/event-history-distribution.png)

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie die [!DNL Pinterest]-Erweiterung für die Ereignisweiterleitung in der Benutzeroberfläche installieren und konfigurieren. Weitere Informationen finden Sie in der offiziellen Dokumentation:

* [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/)
* [[!DNL Pinterest] Konversions-API - Übersicht](https://help.pinterest.com/en/business/article/the-pinterest-api-for-conversions)
