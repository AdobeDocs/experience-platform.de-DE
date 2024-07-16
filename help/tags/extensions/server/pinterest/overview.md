---
keywords: Ereignisweiterleitungs-Erweiterung;pinterest;pinterest-Ereignisweiterleitungs-Erweiterung
title: Pinterest-Ereignisweiterleitungs-Erweiterung
description: Mit dieser Ereignisweiterleitungs-Erweiterung von Adobe Experience Platform können Sie Ereignisse für Ihre Geschäftsanforderungen in Pinterest erfassen.
last-substantial-update: 2023-04-27T00:00:00Z
exl-id: 44f38a9b-0a28-4b51-bead-ee460eb8405e
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '1478'
ht-degree: 6%

---

# [!DNL Pinterest]-Erweiterung zur Ereignisweiterleitung

[!DNL Pinterest] ist eine visuelle Suchmaschine, mit der Ideen wie Rezepte, Innendekoration, Stilinspirierungen und mehr gefunden werden können. Es gibt Milliarden von Pins auf [!DNL Pinterest], die auch für andere auf [!DNL Pinterest] freigegeben werden können. Sie können die Benutzerinteraktionsereignisse sortieren und [!DNL Pinterest Analytics] verwenden, um das Benutzerverhalten zu verstehen und zielgerichtete Werbung auszuführen.

Mit der Erweiterung [[!DNL Pinterest] Konversions](https://developers.pinterest.com/docs/conversions/conversion-management/) API [ Ereignisweiterleitung](../../../ui/event-forwarding/overview.md) können Sie die im Adobe Experience Platform-Edge Network erfassten Daten nutzen und an [!DNL Pinterest] senden. In diesem Dokument werden die Anwendungsfälle der Erweiterung, ihre Installation und die Integration ihrer Funktionen in die Ereignisweiterleitung von [Regeln](../../../ui/managing-resources/rules.md) behandelt.

Konversions-Zugriffstoken sind die Authentifizierungsmethode, die von [!DNL Pinterest] bei der Interaktion mit der [!DNL Pinterest] -API verwendet wird.

## Anwendungsfälle

Diese Erweiterung sollte verwendet werden, wenn Sie Daten aus dem Edge Network in [!DNL Pinterest] verwenden möchten, um die Kundenanalysefunktionen zu nutzen.

Betrachten Sie beispielsweise ein Marketing-Team in einer Organisation. Das Team erfasst Benutzerinteraktionsereignisdaten von seiner Website und lädt sie mithilfe dieser Ereignisweiterleitungs-Erweiterung in [!DNL Pinterest].

Die Marketing- und Analyseteams können dann [!DNL Pinterest] Analytics-Funktionen nutzen, um wichtige Benutzerinteraktionen und -verhalten zu verstehen, sodass Sie Benutzer besser verstehen und gezielt für zielgerichtete Werbekampagnen ansprechen können.

Weitere Informationen zu [!DNL Pinterest] spezifischen Anwendungsfällen finden Sie in der Dokumentation zu [[!DNL Pinterest] Anwendungsfällen](https://business.pinterest.com/en/success-stories) .

## Voraussetzungen für [!DNL Pinterest] {#prerequisites}

Sie müssen über ein gültiges [!DNL Pinterest] [Geschäftskonto](https://help.pinterest.com/en/business/article/get-a-business-account) verfügen, um diese Erweiterung verwenden zu können. Rufen Sie die [[!DNL Pinterest] Registrierungsseite](https://www.pinterest.com/business/create/) auf, um sich zu registrieren und ein Konto zu erstellen, falls noch keines vorhanden ist.

Sie benötigen außerdem ein [!DNL Pinterest] -Entwicklerkonto, das mit Ihrem [!DNL Pinterest] -Geschäftskonto verknüpft werden muss. Informationen zum Verknüpfen Ihres Entwicklerkontos mit Ihrem Geschäftskonto finden Sie im [[!DNL Pinterest ] Entwicklerkonto](https://developers.pinterest.com/account-setup/).

### Erforderliche Konfigurationsdetails sammeln {#configuration-details}

Um die Experience Platform mit [!DNL Pinterest] zu verbinden, sind die folgenden Eingaben erforderlich:

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| Anzeigen-Konto-ID | Ihre [!DNL Pinterest] Kontokennung für Anzeigen. Eine Anleitung finden Sie in der [[!DNL Pinterest] Dokumentation](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager). | 123456789012 |
| Konversionszugriffstoken | Ihr [!DNL Pinterest] Konversions-Zugriffstoken. Eine Anleitung finden Sie im Dokument [[!DNL Pinterest] Konversions-API](https://developers.pinterest.com/docs/conversions/conversions/#Get%20the%20conversion%20token) . <br> **Sie müssen dies nur einmal tun, da dieses Token nicht abläuft.** | {YOUR_PINTEREST_BEARER_TOKEN} |

## Installieren und Konfigurieren der [!DNL Pinterest] -Erweiterung {#install}

Um die Erweiterung zu installieren, erstellen Sie [eine Ereignisweiterleitungs-Eigenschaft](../../../ui/event-forwarding/overview.md#properties) oder wählen Sie eine vorhandene Eigenschaft aus, die Sie stattdessen bearbeiten möchten.

Wählen Sie im linken Navigationsbereich **[!UICONTROL Erweiterungen]** aus. Wählen Sie **[!UICONTROL Installieren]** auf der Karte für die Erweiterung [!DNL Pinterest] auf der Registerkarte **[!UICONTROL Katalog]** aus.

![Katalog, der die Erweiterung [!DNL Pinterest] anzeigt, wobei [!UICONTROL Install] hervorgehoben ist.](../../../images/extensions/server/pinterest/install.png)

### [!DNL Pinterest]-Erweiterung konfigurieren

>[!IMPORTANT]
>
>Je nach Ihren Implementierungsanforderungen müssen Sie möglicherweise ein Schema, Datenelemente und einen Datensatz erstellen, bevor Sie die Erweiterung konfigurieren. Bitte überprüfen Sie alle Konfigurationsschritte, bevor Sie beginnen, um festzustellen, welche Entitäten Sie für Ihren Anwendungsfall einrichten müssen.

Wählen Sie im linken Navigationsbereich **[!UICONTROL Erweiterungen]** aus. Wählen Sie **[!UICONTROL Konfigurieren]** auf der Karte für die Erweiterung [!DNL Pinterest] auf der Registerkarte [!UICONTROL Installiert]**.

Erweiterung ![[!DNL Pinterest] wird auf der Registerkarte [!UICONTROL Installieren] angezeigt, wobei [!UICONTROL Konfigurieren] hervorgehoben ist.](../../../images/extensions/server/pinterest/configure.png)

Geben Sie im nächsten Bildschirm die [!UICONTROL Konto-ID des Anzeigenkontos] und das [!UICONTROL Konversionszugriffs-Token] ein, die Sie zuvor im Abschnitt [Konfigurationsdetails](#configuration-details) erfasst haben. Klicken Sie abschließend auf **[!UICONTROL Speichern]**.

![ Der Bildschirm [!DNL Pinterest] [!UICONTROL Konfigurieren] , auf dem die Eingabefelder [!UICONTROL Konto-ID der Anzeigen] und [!UICONTROL Konversionszugriffstoken] markiert werden.](../../../images/extensions/server/pinterest/input.png)

## Konfigurieren einer Ereignisweiterleitungsregel {#config-rule}

Sobald alle Ihre Datenelemente eingerichtet sind, können Sie mit der Erstellung von Ereignisweiterleitungsregeln beginnen, die bestimmen, wann und wie Ihre Ereignisse an [!DNL Pinterest] gesendet werden.

Erstellen Sie eine neue [Regel](../../../ui/managing-resources/rules.md) in Ihrer Ereignisweiterleitungseigenschaft. Fügen Sie unter **[!UICONTROL Aktionen]** eine neue Aktion hinzu und legen Sie die Erweiterung auf **[!UICONTROL Pinterest]** fest. Um Edge Network-Ereignisse an [!DNL Pinterest] zu senden, setzen Sie den **[!UICONTROL Aktionstyp]** auf **[!UICONTROL Ereignis senden].**

![Die Regelerstellung [!DNL Pinterest] [!UICONTROL Ereignis senden] ](../../../images/extensions/server/pinterest/rule.png).

Nach der Auswahl scheinen zusätzliche Steuerelemente das Ereignis weiter zu konfigurieren. Sie müssen die [!DNL Pinterest] -Ereigniseigenschaften den zuvor erstellten Datenelementen zuordnen.

### [!UICONTROL Ereignisdaten]

Die folgenden Ereignisdaten sind erforderlich, um die neue Regel zu erstellen:

| Feldname | Beschreibung | Beispiel |
| --- | --- | --- | 
| [!UICONTROL Ereignisname] | Der Typ des Benutzerereignisses. Dies kann jedoch ein beliebiger Ereignistyp sein, um [!DNL Pinterest Analytics] zu nutzen. Es wird empfohlen, [[!DNL Pinterest] Ereigniscodes](https://help.pinterest.com/en/business/article/add-event-codes) zu verwenden. | * checkout <br> * add_to_cart <br> * page_visit <br> * signup <br> * [Benutzerdefiniertes Ereignis] |
| [!UICONTROL Action Source] | Die Quelle, die angibt, wo das Konversionsereignis aufgetreten ist. | * app_android <br> * app_ios <br> * web <br> * offline |
| [!UICONTROL Ereigniszeit] | Dies bezieht sich auf die Ereigniszeit. Das standardmäßig verwendete Zeitformat ist UNIX, das je nach lokaler Zeitzone im Format `<seconds>.<miliseconds>` vorliegt. Weitere Informationen finden Sie in der [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/#operation/events/create). | 1433188255.500 bedeutet 143318255 Sekunden und 500 Millisekunden nach der Epoche oder Montag, den 1. Juni 2015, um 19 Uhr GMT.:50: |
| [!UICONTROL Ereignis-ID] | Eine eindeutige ID-Zeichenfolge, die dieses Ereignis identifiziert und zur Deduplizierung zwischen Ereignissen verwendet werden kann, die sowohl über die Konversions-API als auch über das Pinterest-Tracking erfasst werden. Andernfalls werden die Ereignisdaten wahrscheinlich doppelt gezählt und die Metrikinflation gemeldet. | ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad |
| [!UICONTROL Ereigniseigenschaften] | Ein JSON-Objekt mit benutzerdefinierten Eigenschaften des Ereignisses. Wählen Sie aus der Bereitstellung von rohen JSON-Dateien oder der Verwendung eines vereinfachten Satzes von Schlüsselwerteingaben. | { &quot;event_source_url&quot;: &quot;http://site.com&quot; } |

![Die in der Regelaktion hervorgehobenen [!DNL Pinterest] [!UICONTROL Ereignisdaten].](../../../images/extensions/server/pinterest/event-data.png)

Die folgenden Ereigniseigenschaften können konfiguriert werden:

| Feldname | Beschreibung |
| --- | --- |
| Ereignis-Source-URL | URL des Web-Konversionsereignisses. |
| App Store-ID | Die App Store-App-ID. |
| Anwendungsname | Der Name der Anwendung. |
| Application Version | Die Version der Anwendung. |
| Gerätemarke | Marke des Geräts, das vom Benutzer verwendet wird. |
| Geräteträger | Mobilnetzbetreiber des Benutzers für sein Gerät. |
| Gerätemodell | Modell des Geräts des Benutzers. |
| Device Type | Gerätetyp, der vom Benutzer verwendet wird. |
| Betriebssystemversion | Version des Betriebssystems des Geräts. |
| Benutzersprache | Zweistelliger ISO-639-1-Sprachcode, der die Sprache des Benutzers angibt. |

### [!UICONTROL Benutzerdaten]

Die folgenden Benutzerdaten können von eingegeben werden und sind keine Pflichtfelder:

| Feldname | Beschreibung | Beispiel |
| --- | --- | --- | 
| [!UICONTROL E-Mail] | Benutzer-E-Mail-Adresse oder ein SHA256-Hash der E-Mail-Adresse des Benutzers. | ebd543592...f2b7e1 |
| [!UICONTROL Mobile Advertising IDs] | Sha256-Hashes der &quot;Google Advertising IDs&quot;(GAIDs) oder &quot;Apples Identifier for Advertisers&quot;(IDFAs) des Benutzers | ebd543592...f2b7e1 |
| [!UICONTROL Client-IP-Adresse] | Die IP-Adresse des Benutzers, die entweder im IPv4- oder IPv6-Format vorliegen kann. Wird für die Zuordnung verwendet. | 192 168,0,1 |
| [!UICONTROL Client-Benutzeragent] | Die Benutzeragenten-Zeichenfolge des Webbrowsers des Benutzers. | Mozilla/5.0 (Plattform; rv:geckoversion) Gecko/geckotrail Firefox/firefoxversion |
| [!UICONTROL Kundeninformationsdaten] | Ein JSON-Objekt, das andere Kundeninformationen enthält. Wählen Sie aus der Bereitstellung von rohen JSON-Dateien oder der Verwendung eines vereinfachten Satzes von Schlüsselwerteingaben. | { &quot;ph&quot;: &quot;122333445&quot; } |

![Die in der Regelaktion hervorgehobenen [!DNL Pinterest] [!UICONTROL Benutzerdaten].](../../../images/extensions/server/pinterest/user-data.png)

Die Eigenschaften der Kundeninformationen, die konfiguriert werden können, sind:

| Feldname | Beschreibung |
| --- | --- |
| Telefon | Kontaktnummer des Benutzers. Es werden nur Ziffern akzeptiert, die mit Ländercode, Gebietscode und Nummer eingegeben werden sollten. |
| Geschlecht | Das Geschlecht kann entweder als &quot;f&quot;für weiblich, als &quot;m&quot;für männlich oder als &quot;n&quot;für nicht binär eingegeben werden. |
| Geburtsdatum | Geburtsdatum, angegeben als Jahr, Monat und Tag. |
| Nachname | Nachname des Benutzers. |
| Vorname | Vorname des Benutzers. |
| Stadt | Wohnort des Benutzers. Dies wird hauptsächlich für Abrechnungszwecke verwendet. |
| Land | Benutzerstatus, der in Kleinbuchstaben als Code mit zwei Buchstaben bereitgestellt wird. |
| Postleitzahl | Postleitzahl des Benutzers, der hauptsächlich für Abrechnungszwecke verwendet wird. |
| Land | Zweistelliger ISO-3166-Ländercode, der das Land des Benutzers angibt. |
| Externe ID | Eindeutige ID des Advertisers, der einen Benutzer in seinem Bereich identifiziert. z. B. Benutzer-ID, Treueprogramm-ID usw. |
| Klick-ID | Die eindeutige Kennung, die im _epik -Cookie in Ihrer Domäne oder im Abfrageparameter &amp;epik= in der URL gespeichert ist. |

>[!IMPORTANT]
>
>Bevor die Daten an den API-Endpunkt [!DNL Pinterest] gesendet werden, hasst und normalisiert die Erweiterung die Werte der folgenden Felder: E-Mail, Telefonnummer, Vorname, Nachname, Geschlecht, Geburtsdatum, Stadt, Bundesland, Postleitzahl, Land und externe ID. Die Erweiterung hasst den Wert dieser Felder nicht, wenn bereits eine SHA256-Zeichenfolge vorhanden ist.

### [!UICONTROL Benutzerdefinierte Daten]

Die folgenden benutzerdefinierten Daten können für die Regel eingegeben werden:

| Feldname | Beschreibung |
| --- | --- |
| Währung | Der Währungscode nach ISO-4217. Wenn dies nicht angegeben wird, wird [!DNL Pinterest] standardmäßig in der Währung des Werbetreibenden verwendet, die bei der Kontoerstellung festgelegt wurde. |
| Wert | Gesamtwert des Ereignisses. Wird in der Anfrage als Zeichenfolge akzeptiert. Dies wird in eine zweistellige Zahl geparst. |
| Suchzeichenfolge | Die Suchzeichenfolge für das Benutzerkonversionsereignis. |
| Auftrags-ID | Die Bestell-ID. Der Versand von `order_id` hilft [!DNL Pinterest] bei der Deduplizierung von Ereignissen bei Bedarf. |
| Anzahl Produkte | Gesamtzahl der Produkte der Veranstaltung. Beispielsweise die Gesamtzahl der bei einem Checkout-Ereignis gekauften Artikel. |
| Inhalts-IDs | Liste (Array) der Produkt-IDs. |
| Inhalt | Eine Liste (Array) von Objekten, die Informationen über Produkte enthalten, wie Preis und Menge. |

![Die in der Regelaktion hervorgehobenen [!DNL Pinterest] [!UICONTROL benutzerdefinierten Daten].](../../../images/extensions/server/pinterest/custom-data.png)

## Daten mit [!DNL Pinterest] validieren

Sobald die Ereignisweiterleitungsregel erstellt und ausgeführt wurde, überprüfen Sie, ob das Ereignis, das an die [!DNL Pinterest] -API gesendet wurde, wie erwartet in der Benutzeroberfläche von [!DNL Pinterest] angezeigt wird.

Wenn die Ereigniserfassung und die Integration von [!DNL Experience Platform] erfolgreich waren, werden Ereignisse in der Benutzeroberfläche von [!DNL Pinterest] angezeigt.

![Der [!DNL Pinterest] Ereignismanager](../../../images/extensions/server/pinterest/event-history.png)

Sie können die [!DNL Pinterest]-Ereignisdatenverteilung weiter durchlaufen und anzeigen.

![Die [!DNL Pinterest] Datenverteilung](../../../images/extensions/server/pinterest/event-history-distribution.png)

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie die Erweiterung [!DNL Pinterest] für die Ereignisweiterleitung in der Benutzeroberfläche installieren und konfigurieren. Weitere Informationen finden Sie in der offiziellen Dokumentation:

* [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/)
* [[!DNL Pinterest] Übersicht über die Konversions-API](https://help.pinterest.com/en/business/article/the-pinterest-api-for-conversions)
