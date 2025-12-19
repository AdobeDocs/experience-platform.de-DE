---
title: NextDoor Conversion-API-Erweiterung
description: Erfahren Sie, wie Sie mit der -Erweiterung der Nextdoor-Konversions-API Konversionsereignisse senden können, um die Leistung Ihrer Werbekampagnen zu verfolgen.
last-substantial-update: 2025-12-18T00:00:00Z
source-git-commit: 56c69696300dd9de8c0e98ecc71cafc7328f1620
workflow-type: tm+mt
source-wordcount: '1772'
ht-degree: 9%

---


# [!DNL Nextdoor] Conversion API-Erweiterung - Benutzerhandbuch

## Überblick

[!DNL Nextdoor] ist ein sozialer Netzwerkdienst für Wohnviertel, der die Menschen mit ihren lokalen Gemeinschaften verbindet. Es ist eine Plattform, auf der Nachbarn kommunizieren, Informationen austauschen, über lokale Veranstaltungen und Nachrichten auf dem Laufenden bleiben und Artikel mit anderen in ihrer Umgebung kaufen und verkaufen können.

Verwenden Sie die [[!DNL Nextdoor] Conversion API-Erweiterung](https://help.nextdoor.com/s/article/About-the-Nextdoor-Conversion-API) um Konversionsereignisse direkt an [!DNL Nextdoor's] Conversion API zu senden. Mit dieser Erweiterung können Sie die Leistung Ihrer [!DNL Nextdoor] Werbekampagnen verfolgen und messen, indem Sie Server-seitige Konversionsdaten senden.

In diesem Handbuch erfahren Sie, wie Sie die [!DNL Nextdoor] Conversion API-Erweiterung in Ihren Ereignisweiterleitungsregeln ([) installieren, konfigurieren und &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/tags/ui/rules).

## Voraussetzungen {#prerequisites}

Sie benötigen ein gültiges [!DNL Nextdoor] Ads Manager-Konto, um diese Erweiterung verwenden zu können. Wenn Sie noch kein Konto haben, gehen Sie zur [[!DNL Nextdoor Ads] Anmeldeseite](https://ads.nextdoor.com/v2/signup) um sich zu registrieren und Ihr Konto zu erstellen.

### Sammeln erforderlicher Konfigurationsdetails {#configuration-details}

Um Experience Platform mit [!DNL Nextdoor] zu verbinden, benötigen Sie die folgenden Informationen:

| Anmeldedaten | Beschreibung | Sicherheitshinweise |
| --- | --- | --- |
| Datenquellen-ID | Ihre eindeutige Datenquellenkennung von [!DNL Nextdoor], die Sie in Ihrem [!DNL Nextdoor Ads Manager] finden können, indem Sie auf die Seite Assets > Pixel zugreifen und ein Nextdoor-Pixel generieren. | Es ist sicher, dies innerhalb Ihrer Organisation freizugeben. |
| Zugriffs-Token | Ihr API-Authentifizierungs-Zugriffstoken für eine sichere Kommunikation. Sie können dieses Token generieren, indem Sie sich bei Ihrem [!DNL Nextdoor Ads Manager]-Konto anmelden und auf die API-Einstellungen zugreifen. | Schützen Sie dieses Token, da es Zugriff auf Ihr Konto bietet. |

## Installieren und Konfigurieren der [!DNL Nextdoor] {#install}

Um die Erweiterung zu installieren, klicken Sie im linken Navigationsbereich auf **[!UICONTROL Extensions]** . Wählen Sie auf der Registerkarte **[!UICONTROL Catalog]** die **[!UICONTROL Nextdoor Conversion API Extension]** und dann **[!UICONTROL Install]** aus.

![Der Erweiterungskatalog mit der [!DNL Nextdoor] Erweiterungskarte, in der install hervorgehoben ist.](../../../images/extensions/server/nextdoor/install-extension.png)

Geben Sie im nächsten Bildschirm die Konfigurationswerte ein, die Sie aus Ihrer [!DNL Nextdoor Ads Manager] generiert haben:

* **[!UICONTROL Data Source ID]**
* **[!UICONTROL Access Token]**

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Save]** aus.

![[!DNL Nextdoor] Konfigurationsbildschirm für die Erweiterung der [!DNL Nextdoor]-Konversions-API.](../../../images/extensions/server/nextdoor/configure.png)

## Konfigurieren einer Ereignisweiterleitungsregel {#config-rule}

Nachdem alle Datenelemente eingerichtet wurden, können Sie Regeln für die Ereignisweiterleitung erstellen, die bestimmen, wann und wie Ihre Ereignisse an [!DNL Nextdoor] gesendet werden.

Erstellen Sie eine neue [Regel](../../../ui/managing-resources/rules.md) in Ihrer Ereignisweiterleitungs-Eigenschaft. Fügen Sie unter **[!UICONTROL Actions]** eine neue Aktion hinzu und legen Sie die Erweiterung auf **[!UICONTROL Nextdoor Conversion API Extension]** fest. Um Edge Network-Ereignisse an [!DNL Nextdoor] zu senden, setzen Sie den **[!UICONTROL Action Type]** auf **[!UICONTROL Report Web Conversions]**.

![Der [!UICONTROL Report Web Conversions] Aktionstyp, der für eine [!DNL Nextdoor] in der Datenerfassungs-Benutzeroberfläche ausgewählt wird.](../../../images/extensions/server/nextdoor/select-action.png)

Nach dieser Auswahl werden zusätzliche Steuerelemente angezeigt, mit denen Sie das Ereignis weiter konfigurieren können, wie unten beschrieben. Wählen Sie anschließend **[!UICONTROL Keep Changes]** aus, um die Regel zu speichern.

**Haupttextparameter**

Diese Kernparameter definieren Ihr Konversionsereignis:

| Parameter | Beschreibung | Datentyp | Erforderlich | Optionen/Format | Beispiel |
| ------------------------------------ | -------------- | -------------- | -------------- | -------------- | -------------- |
| [!UICONTROL Event Name] | Gibt den Typ des zu verfolgenden Konversionsereignisses an. | Zeichenfolge (Dropdown) | Erforderlich | <ul><li>Kauf</li><li>Lead</li><li>Registrierung</li><li>Zum Warenkorb hinzufügen</li><li>Auschecken starten</li><li>Seitenansicht</li><li>Suche</li><li>Inhalt anzeigen</li><li>Zur Wunschliste hinzufügen</li><li>Abonnieren</li><li>Benutzerspezifisch</li></li>Konversion 1-10</li></ul> | `Purchase` |
| [!UICONTROL Event ID] | Eindeutige Kennung, um doppelte Ereignisberichte zu verhindern. Dieser wird automatisch generiert, wenn er leer ist. | Zeichenfolge | Optional | Eindeutige Zeichenfolgenkennung | `order_12345` |
| [!UICONTROL Event Time (Unix Epoch)] | Zeitstempel, wann das Konversionsereignis aufgetreten ist. Die Standardeinstellung ist die aktuelle Zeit, wenn sie leer gelassen wird. | Ganzzahl | Optional | Unix-Zeitstempel in Sekunden | `1703980800` (30. Dezember 2023) |
| [!UICONTROL Action Source] | Kanal oder Plattform, in dem/der die Konvertierung stattgefunden hat. | Zeichenfolge (Dropdown) | Erforderlich | <ul><li>Website</li><li>email</li><li>App</li><li>phone_call</li><li>Chat</li><li>Physical_Store</li><li>system_generated</li><li>Sonstige</li></ul> | `website` |
| [!UICONTROL Data Source ID] | Überschreiben der globalen Datenquellen-ID für bestimmte Ereignisse. Erbt von der Konfiguration, wenn es leer gelassen wird. | Zeichenfolge | Optional | alphanumerischer String | `12345` |
| [!UICONTROL Action Source URL] | Die spezifische URL, in der die Konvertierung stattgefunden hat. | Zeichenfolge | Optional | Vollständige URL einschließlich Protokoll | https://example.com/checkout/success |

**Datenschutz- und Compliance-Parameter**

Verwenden Sie diese Parameter, um die Einhaltung von Datenschutzbestimmungen sicherzustellen:

| Parameter | Beschreibung | Datentyp | Erforderlich | Werte/Format | Beispiel |
| -------------------------------------------- | ---------------------------------------------------  | --------- | -------- | ---------------------------------------------------------- | ---------- |
| [!UICONTROL Restricted Data Usage] | Flag zur Einschränkung der Datennutzung zwecks Einhaltung von Datenschutzbestimmungen. | Ganzzahl | Optional | <ul><li>0 = Keine Einschränkungen</li><li>1= Restrict</li></ul> | `0` |
| [!UICONTROL Restricted Data Usage (Country)] | Länderspezifische Einschränkungen bei der Datenverarbeitung. | Ganzzahl | Optional | 1 = USA (andere Codes können unterstützt werden) | `1` |
| [!UICONTROL Restricted Data Usage (State)] | Bundesstaatliche Beschränkungen für US-Benutzer. | Ganzzahl | Optional | 1000 = CA, 1001 = CO, etc. | `1000` |
| [!UICONTROL Test Event] | Markiert das Ereignis als Test für die Entwicklung/das Debugging. | Zeichenfolge | Optional | Beliebige nicht leere Zeichenfolge | `test` |

**Kundeninformationsparameter**

>[!IMPORTANT]
>
>Sie müssen mindestens einen Kundeninformationsparameter für die ordnungsgemäße Ereigniszuordnung und -zuordnung angeben.

| Parameter | Beschreibung | Datentyp | Erforderlich | Format | Beispiel |
| ------------------------------ | ----------------------------------------------- | --------- | ------------------------------------ | ------------------------------------ | -------------------------- |
| [!UICONTROL Email] | E-Mail-Adresse des Kunden für den Identitätsabgleich. | String | Mindestens ein Kundenfeld erforderlich | Nur Text oder SHA-256-Hash | `user@example.com` |
| [!UICONTROL Phone Number] | Telefonnummer des Kunden für den Identitätsabgleich. | String | Mindestens ein Kundenfeld erforderlich | E.164-Format (gehasht mit SHA-256) | `+15551234567` |
| [!UICONTROL First Name] | Vorname des Kunden für die erweiterte Zuordnung. | String | Mindestens ein Kundenfeld erforderlich | Nur Text oder SHA-256-Hash | `John` |
| [!UICONTROL Last Name] | Nachname des Kunden für den erweiterten Abgleich. | String | Mindestens ein Kundenfeld erforderlich | Nur Text oder SHA-256-Hash | `Smith` |
| [!UICONTROL Date of Birth] | Geburtsdatum des Kunden für den demografischen Abgleich. | Zeichenfolge | Optional | JJJJMMTT (SHA-256 HASH) | `19900115` |
| [!UICONTROL Gender] | Geschlecht des Kunden beim demografischen Targeting. | Zeichenfolge | Optional | M/F/O (SHA-256-Hash) | `M` |
| [!UICONTROL External ID] | Ihre interne Kundenkennung. | Zeichenfolge | Optional | Beliebige eindeutige Zeichenfolge | `customer_12345` |
| [!UICONTROL Street Address] | Straße des Kunden. | Zeichenfolge | Optional | SHA-256 gehasht | `123 Main Street` (Hash) |
| [!UICONTROL City] | Stadt des Kunden. | Zeichenfolge | Optional | SHA-256 gehasht | `San Francisco` (Hash) |
| [!UICONTROL State] | Bundesland/Region des Kunden | Zeichenfolge | Optional | Code mit zwei Buchstaben (SHA-256 mit Hash) | `CA` (Hash) |
| [!UICONTROL Zip Code] | Postleitzahl des Kunden. | Zeichenfolge | Optional | Erste 5-stellige US-Ziffern (SHA-256 mit Hash) | `94102` (Hash) |
| [!UICONTROL Country] | Land des Kunden. | Zeichenfolge | Optional | ISO-3166-1 alpha-2 (SHA-256 gehasht) | `US` (Hash) |
| [!UICONTROL Click ID] | NextDoor-Klick-Kennung für Attribution. | Zeichenfolge | Optional | Erfasst aus `ndclid` URL-Parameter | `nd_click_12345abcdef` |
| [!UICONTROL Client IP Address] | IP-Adresse des Geräts des Benutzers. | Zeichenfolge | Optional | IPv4- oder IPv6-Adresse | `192.168.1.1` |
| [!UICONTROL Client User Agent] | Browser-Benutzeragenten-Zeichenfolge. | Zeichenfolge | Optional | Unformatierte Browser-Benutzeragenten-Zeichenfolge | `Mozilla/5.0 (Windows...)` |

**Benutzerdefinierte Parameter**

Diese Parameter liefern zusätzlichen Kontext zu Ihrem Konversionsereignis:

| Parameter | Beschreibung | Datentyp | Erforderlich | Format | Beispiel |
| ------------------------------ | ---------------------------------------------- | ------------------- | -------------------------------- | --------------------------------------- | ----------------------- |
| [!UICONTROL Order Value] | Gesamtwert der Kauftransaktion. | String | **ERFORDERLICH für Kaufereignisse** | ISO 4217 Währung + Betrag (keine Leerzeichen) | `USD123.45` |
| [!UICONTROL Order ID] | Eindeutige Transaktions- oder Bestellkennung. | Zeichenfolge | Optional | Beliebige eindeutige Zeichenfolge | `order_12345` |
| [!UICONTROL Delivery Category] | Methode der Produkt-/Dienstleistungsbereitstellung. | Zeichenfolge | Optional | <ul><li>`in_store`</li><li>`curbside`</li><li>`home_delivery`</li></ul> | `home_delivery` |
| [!UICONTROL Product Context] | Detaillierte Informationen über gekaufte Produkte. | Zeichenfolge (JSON-Array) | Optional | JSON-Array von Produktobjekten | `[{"id":"SKU123","content_name":"Widget","item_price":29.99,"quantity":1}]` |

**Mobile-App-Parameter**

Sie müssen diese Parameter bei der `Action Source = 'APP'` einbeziehen:

| Parameter | Beschreibung | Datentyp | Erforderlich | Format | Beispiel |
| --------------------------------- | --------------------------------------------- | --------- | --------------------------- | ----------------------------------------- | ----------------- |
| [!UICONTROL App ID*] | Kennung der Mobile App. | String | **ERFORDERLICH für APP-Ereignisse** | <ul><li>Paket-ID (iOS)</li><li>Paketname (Android)</li></ul> | `com.company.app` |
| [!UICONTROL App Tracking Enabled] | iOS App Tracking Transparency Consent Status. | String | **ERFORDERLICH für APP-Ereignisse** | Boolesche Zeichenfolge | `true` |
| [!UICONTROL Platform] | Mobiles Betriebssystem. | String | **ERFORDERLICH für APP-Ereignisse** | <ul><li>`iOS`</li><li>`Android`</li></ul> | `Android` |
| [!UICONTROL App Version] | Version der Mobile App. | String | **ERFORDERLICH für APP-Ereignisse** | Versionszeichenfolge wie von der App definiert | `2.0.0-beta` |

## Ereignistypen {#event-types}

Die folgenden Ereignistypen werden für verschiedene Konversionsszenarien unterstützt:

| Ereignisname | Ereignistyp | Beschreibung | Anwendungsfall | Erforderliche Felder | Anmerkungen |
| ------------------------ | ---------- | -------------------------------------- | --------------------------------------- | -------------------------------------- | ------------------------------------- |
| [!UICONTROL Purchase] | Standard | Abgeschlossene Kauftransaktion. | E-Commerce-Konversionen | <ul><li>Ereignisname</li><li>Bestellwert</li><li>Kundeninformationen</li></ul> | Am wichtigsten für die ROAS-Optimierung |
| [!UICONTROL Lead] | Standard | Lead-Generierung oder -Anfrage | Formularübermittlungen, Kontaktanfragen | <ul><li>Ereignisname</li><li>Kundeninformationen</li></ul> | Hochwertige Konversion für B2B |
| [!UICONTROL Sign Up] | Standard | Benutzerregistrierung oder Kontoerstellung. | Newsletter-Anmeldung, Kontoregistrierung | <ul><li>Ereignisname</li><li>Kundeninformationen</li></ul> | Top-funnel-Konversionsverfolgung |
| [!UICONTROL Add to Cart] | Standard | Produkt zum Warenkorb hinzugefügt. | E-Commerce-Tracking mit funnel | <ul><li>Ereignisname</li><li>Kundeninformationen</li></ul> | Interaktionssignal Mid-funnel |
| [!UICONTROL Initiate Checkout] | Standard | Checkout-Prozess gestartet. | Tracking der Kaufabsicht | <ul><li>Ereignisname</li><li>Kundeninformationen</li></ul> | Starker Indikator für die Kaufabsicht |
| [!UICONTROL Page View] | Standard | Wichtige besuchte Seite. | Content-Interaktion, Landingpages | <ul><li>Ereignisname</li><li>Kundeninformationen</li></ul> | Nur für hochwertige Seiten verwenden |
| [!UICONTROL Search] | Standard | Suche vor Ort durchgeführt. | Produkt-/Inhaltssuche | <ul><li>Ereignisname</li><li>Kundeninformationen</li></ul> | Zeigt aktive Benutzerinteraktion an |
| [!UICONTROL View Content] | Standard | Inhalt oder Produkt angesehen. | Produktseitenansichten, Content-Interaktion | <ul><li>Ereignisname</li><li>Kundeninformationen</li></ul> | Nützlich für Remarketing-Audiences |
| [!UICONTROL Add to Wishlist] | Standard | Produkt zur Wunschliste hinzugefügt. | Zukünftige Kaufabsicht | <ul><li>Ereignisname</li><li>Kundeninformationen</li></ul> | Zeigt starkes Produktinteresse |
| [!UICONTROL Subscribe] | Standard | Abonnement für Dienst/Newsletter. | Wiederkehrender Umsatz, Interaktion | <ul><li>Ereignisname</li><li>Kundeninformationen</li></ul> | Indikator für hohen Lebenszeitwert |
| [!UICONTROL Custom Conversion 1 - 10] | Benutzerspezifisch | Geschäftsspezifisches Konversionsereignis. | Definieren eines eigenen Konversionstyps | <ul><li>Ereignisname</li><li>Kundeninformationen</li></ul> | Anpassen für eindeutige Geschäftsaktionen |

## Integration von Datenelementen {#data-element}

Alle -Felder unterstützen Datenelemente für die Adobe-Ereignisweiterleitung. Wählen Sie das Datenelementsymbol ![Datenelemente](../../../images/extensions/server/nextdoor/data-element-icon.png) neben einem beliebigen Feld aus, um:

* **Vorhandene Datenelemente auswählen**: Wählen Sie aus Datenelementen, die bereits erstellt wurden.
* **Neue Datenelemente hinzufügen**: Erstellen und definieren Sie neue Datenelemente nach Bedarf.
* **Dynamische Werte anwenden**: Füllen Sie Felder mit dynamischen Inhalten aus Ihrer Website.

## Best Practices {#best-practices}

Befolgen Sie diese Best Practices, um ein genaues Konversions-Tracking sicherzustellen, die Datenqualität zu verbessern und Datenschutzbestimmungen einzuhalten. Diese Empfehlungen helfen Ihnen, die Effektivität Ihrer [!DNL Nextdoor] Conversion API-Integration zu maximieren und Ihre Werbeleistung zu optimieren.

### Einhaltung von Datenqualität und Datenschutz

Eine ordnungsgemäße Datenverarbeitung ist unerlässlich, um die Genauigkeit der Konversionszuordnung zu maximieren und gleichzeitig den Datenschutz der Benutzer und die Einhaltung von Vorschriften zu gewährleisten. Diese Praktiken helfen sicherzustellen, dass Ihre Kundendaten korrekt formatiert, sicher verarbeitet und gemäß den Datenschutzbestimmungen verarbeitet werden.

* **Konsistente Datenformatierung verwenden**: Formatieren Sie E-Mails, Telefonnummern und andere Daten konsistent:

   * **E-Mail-Normalisierung**: Konvertieren Sie E-Mails in Kleinbuchstaben, kürzen Sie Leerzeichen und entfernen Sie Punkte aus [!DNL Gmail].
   * **Telefonnummernstandardisierung**: Verwenden Sie das E.164-Format (+1234567890) für internationale Kompatibilität.
   * **Adressnormalisierung**: Standardisieren Sie die Straßenabkürzungen (St., Ave., Rd.) und entfernen Sie alle zusätzlichen Leerzeichen.
   * **Namensformatierung**: Namen in Kleinbuchstaben konvertieren, zusätzliche Leerzeichen entfernen und Sonderzeichen konsistent verarbeiten.

* **Hash-**: Erwägen Sie, sensible Kundendaten vor dem Senden zu hashen. Normalisieren Sie Ihre Daten immer vor dem Hashing, um konsistente Hash-Werte sicherzustellen:

   * Verwenden Sie SHA-256-Hashing für Telefonnummern, Adressen und andere personenbezogene Daten.
   * Die Erweiterung hasht automatisch Text-E-Mails - Sie können beide Formate senden.
   * Hashing von Daten konsistent über alle Tracking-Implementierungen hinweg.
      * **Beispiel**: Normalisieren Sie &quot;John@Example.COM&quot; → &quot;john@example.com&quot; vor dem Hashing.

* **Vollständige Informationen bereitstellen**: Geben Sie so viele Kundeninformationen wie möglich an, um einen besseren Abgleich zu ermöglichen:

   * Mehrere Kennungen einschließen (E-Mail + Telefon oder E-Mail + Name + Adresse), wenn verfügbar.
   * Verwenden Sie externe Kunden-IDs, um Konversionsereignisse mit Ihren CRM-Daten zu verknüpfen.
   * Geben Sie demografische Daten (Alter, Geschlecht) an, sofern verfügbar und mit den Datenschutzgesetzen konform.

* **Einverständnisverwaltung**: Stellen Sie sicher, dass Sie über ein ordnungsgemäßes Einverständnis für die Datenerfassung verfügen:

   * Implementieren Sie geeignete Einverständnismechanismen, bevor Sie Kundendaten erfassen.
   * Berücksichtigen Sie die Voreinstellungen für das Benutzer-Opt-out und Anfragen zur Datenlöschung.
   * Verwenden Sie die eingeschränkten Datennutzungsparameter für Benutzer, die sich abgemeldet haben.
   * **Ressourcen**:
      * [DSGVO-Compliance-Handbuch](https://gdpr.eu/compliance/)
      * [CCPA-Datenschutzanforderungen](https://oag.ca.gov/privacy/ccpa)

* **Datenminimierung**: Senden Sie nur die für das Konversions-Tracking erforderlichen Daten:

   * Sammeln und senden Sie nur Daten, die für Attribution und Optimierung unerlässlich sind.
   * Überprüfen und überprüfen Sie regelmäßig die Datenfelder, die Sie senden.
   * Entfernen Sie unnötige Kundeninformationen, um das Datenschutzrisiko zu reduzieren.

* **Verwenden genauer Zeitstempel**: Stellen Sie sicher, dass Ereignis-Zeitstempel für eine ordnungsgemäße Zuordnung korrekt sind.
   * Verwenden Sie den Zeitpunkt, zu dem die Konvertierung stattgefunden hat, nicht die Verarbeitungszeit der Daten.
   * Stellen Sie sicher, dass Zeitstempel im Unix-Epochenformat vorliegen (Sekunden seit dem 1. Januar 1970).
   * Berücksichtigen Sie Zeitzonenunterschiede bei Ihren Zeitstempelberechnungen.

### Ereignis-Deduplizierung

Verhindern Sie doppelte Konversionsereignisse, um eine genaue Kampagnenmessung sicherzustellen und überhöhte Leistungsmetriken zu vermeiden. Implementieren Sie eine ordnungsgemäße Deduplizierung, sodass jede Konvertierung nur einmal gezählt wird und zuverlässige Daten für Ihre Optimierungsentscheidungen bereitgestellt werden.

* **Eindeutige Ereignis-IDs bereitstellen**: Verwenden Sie immer eindeutige Ereignis-IDs, um doppelte Konvertierungen zu verhindern.
* **Konsistente Benennung verwenden**: Wenden Sie eine konsistente Ereignisbenennung auf Ihre gesamte Implementierung an.

### Ratenbegrenzung

Die [!DNL Nextdoor]-Konversions-API unterliegt einer Ratenbegrenzung. Die aktuelle Ratenbeschränkung beträgt **100 Anfragen/Minute** pro Advertiser. Wenn Sie das Ratenlimit überschreiten, gibt die API einen `HTTP 429 Too Many Requests` Fehlercode zurück.

## Zusammenfassung {#conclusion}

Die [!DNL Nextdoor] Conversion API-Erweiterung bietet eine leistungsstarke Möglichkeit, Konversionen zu verfolgen und die Effektivität Ihrer [!DNL Nextdoor] Werbekampagnen zu messen. Wenn Sie diesem Handbuch folgen und die Best Practices implementieren, können Sie ein genaues Konversions-Tracking sicherstellen und die Anzeigenleistung optimieren.

Die aktuellsten Informationen und zusätzlichen Ressourcen finden Sie unter [[!DNL Nextdoor Ads Manager]](https://ads.nextdoor.com).

## Nächste Schritte {#next-steps}

In diesem Handbuch wurde gezeigt, wie Sie Server-seitige Ereignisdaten mithilfe der [!DNL Nextdoor] Conversion API-Erweiterung an [!DNL Nextdoor] senden. Weitere Informationen zu den Funktionen der Ereignisweiterleitung in [!DNL Adobe Experience Platform] finden Sie unter [Übersicht über die Ereignisweiterleitung](../../../ui/event-forwarding/overview.md).
