---
keywords: Ereignisweiterleitungs-Erweiterung;pinterest;pinterest-Ereignisweiterleitungs-Erweiterung
title: Pinterest-Ereignisweiterleitungs-Erweiterung
description: Mit dieser Ereignisweiterleitungs-Erweiterung von Adobe Experience Platform können Sie Ereignisse für Ihre Geschäftsanforderungen in Pinterest erfassen.
last-substantial-update: 2023-04-27T00:00:00Z
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '1548'
ht-degree: 7%

---

# [!DNL Pinterest]-Erweiterung zur Ereignisweiterleitung

[!DNL Pinterest] ist eine visuelle Erkennungsmaschine, mit der Ideen wie Rezepte, Innendekoration, Stilinspirierungen und mehr gefunden werden können. Es sind Milliarden von Pins auf [!DNL Pinterest], die auch für andere Benutzer freigegeben werden können [!DNL Pinterest]. Sie können die Benutzerinteraktionsereignisse zusammenstellen und [!DNL Pinterest Analytics] , um das Benutzerverhalten zu verstehen und zielgerichtete Werbung zu betreiben.

Die [[!DNL Pinterest] Konversionen](https://developers.pinterest.com/docs/conversions/conversion-management/) API [Ereignisweiterleitung](../../../ui/event-forwarding/overview.md) -Erweiterung ermöglicht es Ihnen, die im Adobe Experience Platform Edge Network erfassten Daten zu nutzen und an [!DNL Pinterest]. In diesem Dokument werden die Anwendungsfälle der Erweiterung, ihre Installation und die Integration ihrer Funktionen in die Ereignisweiterleitung behandelt. [Regeln](../../../ui/managing-resources/rules.md).

Konversions-Zugriffstoken werden von der Authentifizierungsmethode verwendet [!DNL Pinterest] bei der Interaktion mit dem [!DNL Pinterest] API.

## Anwendungsfälle

Diese Erweiterung sollte verwendet werden, wenn Sie Daten aus dem Edge-Netzwerk in [!DNL Pinterest] , um die Funktionen der Kundenanalyse zu nutzen.

Betrachten Sie beispielsweise ein Marketing-Team in einer Organisation. Das Team erfasst Benutzerinteraktionsereignisdaten von seiner Website und lädt sie in [!DNL Pinterest] mit dieser Ereignisweiterleitungs-Erweiterung verwenden.

Die Marketing- und Analyseteams können dann [!DNL Pinterest] Analytics-Funktionen, um wichtige Benutzerinteraktionen und -verhalten zu verstehen, sodass Sie Benutzer besser verstehen und gezielt für zielgerichtete Anzeigenkampagnen ansprechen können.

Weitere Informationen zu spezifischen Anwendungsfällen für [!DNL Pinterest], siehe [[!DNL Pinterest] Anwendungsfälle](https://business.pinterest.com/en/success-stories) Dokumentation.

## Voraussetzungen für [!DNL Pinterest] {#prerequisites}

Sie müssen über gültige [!DNL Pinterest] [Geschäftskonto](https://help.pinterest.com/en/business/article/get-a-business-account) , um diese Erweiterung zu verwenden. Navigieren Sie zu [[!DNL Pinterest] Registrierungsseite](https://www.pinterest.com/business/create/) , um sich zu registrieren und ein Konto zu erstellen, falls Sie noch kein Konto haben.

Sie benötigen außerdem [!DNL Pinterest] Entwicklerkonto, das mit Ihrem [!DNL Pinterest] Geschäftskonto. Informationen zum Verknüpfen Ihres Entwicklerkontos mit Ihrem Geschäftskonto finden Sie im Abschnitt [[!DNL Pinterest ] Entwicklerkonto](https://developers.pinterest.com/account-setup/).

### Erforderliche Konfigurationsdetails sammeln {#configuration-details}

Um die Experience Platform an [!DNL Pinterest], sind folgende Eingaben erforderlich:

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| Anzeigen-Konto-ID | Ihre [!DNL Pinterest] Anzeigen-Konto-ID. Eine Anleitung finden Sie in der [[!DNL Pinterest] Dokumentation](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager). | 123456789012 |
| Konversionszugriffstoken | Ihre [!DNL Pinterest] Konversionszugriffstoken. Siehe Abschnitt [[!DNL Pinterest] Konversions-API](https://developers.pinterest.com/docs/conversions/conversions/#Get%20the%20conversion%20token) Leitfaden. <br> **Sie müssen dies nur einmal tun, da dieses Token nicht abläuft.** | {YOUR_PINTEREST_BEARER_TOKEN} |

## Installieren und konfigurieren Sie die [!DNL Pinterest] Erweiterung {#install}

So installieren Sie die Erweiterung: [Erstellen einer Ereignisweiterleitungs-Eigenschaft](../../../ui/event-forwarding/overview.md#properties) oder wählen Sie eine vorhandene Eigenschaft aus, die Sie stattdessen bearbeiten möchten.

Wählen Sie im linken Navigationsbereich die Option **[!UICONTROL Erweiterungen]**. Auswählen **[!UICONTROL Installieren]** auf der Karte für die [!DNL Pinterest] -Erweiterung in **[!UICONTROL Katalog]** Registerkarte.

![Katalog, der die [!DNL Pinterest] Erweiterung mit [!UICONTROL Installieren] hervorgehoben.](../../../images/extensions/server/pinterest/install.png)

### [!DNL Pinterest]-Erweiterung konfigurieren

>[!IMPORTANT]
>
>Je nach Ihren Implementierungsanforderungen müssen Sie möglicherweise ein Schema, Datenelemente und einen Datensatz erstellen, bevor Sie die Erweiterung konfigurieren. Bitte überprüfen Sie alle Konfigurationsschritte, bevor Sie beginnen, um festzustellen, welche Entitäten Sie für Ihren Anwendungsfall einrichten müssen.

Wählen Sie im linken Navigationsbereich die Option **[!UICONTROL Erweiterungen]**. Auswählen **[!UICONTROL Konfigurieren]** auf der Karte für die [!DNL Pinterest] -Erweiterung in [!UICONTROL Installiert]Registerkarte **.

![[!DNL Pinterest] -Erweiterung, die im [!UICONTROL Installieren] Registerkarte mit [!UICONTROL Konfigurieren] hervorgehoben.](../../../images/extensions/server/pinterest/configure.png)

Geben Sie im nächsten Bildschirm die [!UICONTROL Anzeigen-Konto-ID] und [!UICONTROL Konversionszugriffstoken] die Sie zuvor im [Konfigurationsdetails](#configuration-details) Abschnitt. Klicken Sie abschließend auf **[!UICONTROL Speichern]**.

![Die [!DNL Pinterest] [!UICONTROL Konfigurieren] -Bildschirm, der die [!UICONTROL Anzeigen-Konto-ID] und [!UICONTROL Konversionszugriffstoken] Eingabefelder.](../../../images/extensions/server/pinterest/input.png)

## Konfigurieren einer Ereignisweiterleitungsregel {#config-rule}

Sobald alle Ihre Datenelemente eingerichtet sind, können Sie mit der Erstellung von Ereignisweiterleitungsregeln beginnen, die bestimmen, wann und wie Ihre Ereignisse an gesendet werden [!DNL Pinterest].

Erstellen Sie eine neue [Regel](../../../ui/managing-resources/rules.md) in Ihrer Ereignisweiterleitungseigenschaft. under **[!UICONTROL Aktionen]**, fügen Sie eine neue Aktion hinzu und legen Sie die Erweiterung auf **[!UICONTROL Pinterest]**. So senden Sie Edge Network-Ereignisse an [!DNL Pinterest], legen Sie die **[!UICONTROL Aktionstyp]** nach **[!UICONTROL Ereignis senden].**

![Die [!DNL Pinterest] [!UICONTROL Ereignis senden] Regelerstellung.](../../../images/extensions/server/pinterest/rule.png)

Nach der Auswahl scheinen zusätzliche Steuerelemente das Ereignis weiter zu konfigurieren. Sie müssen die [!DNL Pinterest] Ereigniseigenschaften zu den zuvor erstellten Datenelementen hinzufügen.

### [!UICONTROL Ereignisdaten]

Die folgenden Ereignisdaten sind erforderlich, um die neue Regel zu erstellen:

| Feldname | Beschreibung | Beispiel |
| --- | --- | --- | 
| [!UICONTROL Ereignisname] | Der Typ des Benutzerereignisses. Dies kann jedoch ein beliebiger Ereignistyp sein, mit dem [!DNL Pinterest Analytics] Es wird empfohlen, [[!DNL Pinterest] Ereigniscodes](https://help.pinterest.com/en/business/article/add-event-codes) | * Kasse <br> * add_to_cart <br> * page_visit <br> * Anmeldung <br> * [Benutzerdefiniertes Ereignis] |
| [!UICONTROL Aktionsquelle] | Die Quelle, die angibt, wo das Konversionsereignis aufgetreten ist. | * app_android <br> * app_ios <br> * Web <br> * offline |
| [!UICONTROL Ereigniszeit] | Dies bezieht sich auf die Ereigniszeit. Das standardmäßig verwendete Zeitformat ist UNIX, im Format `<seconds>.<miliseconds>` abhängig von Ihrer lokalen Zeitzone. Weitere Informationen finden Sie im Abschnitt [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/#operation/events/create). | 1433188255.500 bedeutet 143318255 Sekunden und 500 Millisekunden nach der Epoche oder Montag, 1. Juni 2015, 7:50:17.00 Uhr GMT. |
| [!UICONTROL Ereignis-ID] | Eine eindeutige ID-Zeichenfolge, die dieses Ereignis identifiziert und zur Deduplizierung zwischen Ereignissen verwendet werden kann, die sowohl über die Konversions-API als auch über das Pinterest-Tracking erfasst werden. Andernfalls werden die Ereignisdaten wahrscheinlich doppelt gezählt und die Metrikinflation gemeldet. | ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad |
| [!UICONTROL Ereigniseigenschaften] | Ein JSON-Objekt mit benutzerdefinierten Eigenschaften des Ereignisses. Wählen Sie aus der Bereitstellung von rohen JSON-Dateien oder der Verwendung eines vereinfachten Satzes von Schlüsselwerteingaben. | { &quot;event_source_url&quot;: &quot;http://site.com&quot; } |

![Die [!DNL Pinterest] [!UICONTROL Ereignisdaten] in der Regelaktion hervorgehoben.](../../../images/extensions/server/pinterest/event-data.png)

Die folgenden Ereigniseigenschaften können konfiguriert werden:

| Feldname | Beschreibung |
| --- | --- |
| Ereignisquellen-URL | URL des Web-Konversionsereignisses. |
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
| [!UICONTROL Mobile Advertising-IDs] | Sha256-Hashes der &quot;Google Advertising IDs&quot;(GAIDs) oder &quot;Apples Identifier for Advertisers&quot;(IDFAs) des Benutzers | ebd543592...f2b7e1 |
| [!UICONTROL Client-IP-Adresse] | Die IP-Adresse des Benutzers, die entweder im IPv4- oder IPv6-Format vorliegen kann. Wird für die Zuordnung verwendet. | 192.168.0.1 |
| [!UICONTROL Client User Agent] | Die Benutzeragenten-Zeichenfolge des Webbrowsers des Benutzers. | Mozilla/5.0 (Plattform; rv:geckoversion) Gecko/geckotrail Firefox/firefoxversion |
| [!UICONTROL Kundeninformationsdaten] | Ein JSON-Objekt, das andere Kundeninformationen enthält. Wählen Sie aus der Bereitstellung von rohen JSON-Dateien oder der Verwendung eines vereinfachten Satzes von Schlüsselwerteingaben. | { &quot;ph&quot;: &quot;122333445&quot; } |

![Die [!DNL Pinterest] [!UICONTROL Benutzerdaten] in der Regelaktion hervorgehoben.](../../../images/extensions/server/pinterest/user-data.png)

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
>Vor dem Senden der Daten an die [!DNL Pinterest] API-Endpunkt verwendet, hasst die Erweiterung die Werte der folgenden Felder und normalisiert sie: E-Mail, Telefonnummer, Vorname, Nachname, Geschlecht, Geburtsdatum, Stadt, Bundesland, Postleitzahl, Land und externe ID. Die Erweiterung hasst den Wert dieser Felder nicht, wenn bereits eine SHA256-Zeichenfolge vorhanden ist.

### [!UICONTROL Benutzerdefinierte Daten]

Die folgenden benutzerdefinierten Daten können für die Regel eingegeben werden:

| Feldname | Beschreibung |
| --- | --- |
| Währung | Der Währungscode nach ISO-4217. Wenn dies nicht angegeben wird, [!DNL Pinterest] wird standardmäßig auf die Währung des Werbetreibenden gesetzt, die bei der Kontoerstellung festgelegt wurde. |
| Wert | Gesamtwert des Ereignisses. Wird in der Anfrage als Zeichenfolge akzeptiert. Dies wird in eine zweistellige Zahl geparst. |
| Suchzeichenfolge | Die Suchzeichenfolge für das Benutzerkonversionsereignis. |
| Auftrags-ID | Die Bestell-ID. Senden `order_id` Hilfe [!DNL Pinterest] deduplizieren Sie Ereignisse bei Bedarf. |
| Anzahl Produkte | Gesamtzahl der Produkte der Veranstaltung. Beispielsweise die Gesamtzahl der bei einem Checkout-Ereignis gekauften Artikel. |
| Inhalts-IDs | Liste (Array) der Produkt-IDs. |
| Inhalt | Eine Liste (Array) von Objekten, die Informationen über Produkte enthalten, wie Preis und Menge. |

![Die [!DNL Pinterest] [!UICONTROL Benutzerdefinierte Daten] in der Regelaktion hervorgehoben.](../../../images/extensions/server/pinterest/custom-data.png)

## Validieren von Daten in [!DNL Pinterest]

Überprüfen Sie nach der Erstellung und Ausführung der Ereignisweiterleitungsregel, ob das Ereignis, das an die [!DNL Pinterest] Die API wird wie erwartet im [!DNL Pinterest] Benutzeroberfläche.

Wenn die Ereigniskollektion und [!DNL Experience Platform] -Integration erfolgreich war, werden Ereignisse im [!DNL Pinterest] Benutzeroberfläche.

![Die [!DNL Pinterest] Ereignismanager](../../../images/extensions/server/pinterest/event-history.png)

Sie können die [!DNL Pinterest] Ereignisdatenverteilung.

![Die [!DNL Pinterest] Datenverteilung](../../../images/extensions/server/pinterest/event-history-distribution.png)

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie die [!DNL Pinterest] Ereignisweiterleitungs-Erweiterung in der Benutzeroberfläche. Weitere Informationen finden Sie in der offiziellen Dokumentation:

* [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/)
* [[!DNL Pinterest] Übersicht über die Konversions-API](https://help.pinterest.com/en/business/article/the-pinterest-api-for-conversions)
