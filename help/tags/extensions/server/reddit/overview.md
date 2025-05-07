---
title: Reddit Conversions API-Erweiterung
description: Erfahren Sie, wie Sie mit der API-Erweiterung „Reddit Ads Conversions“ Benutzerinteraktionsereignisse für zielgruppengerechte Werbung an Reddit Ads senden können.
last-substantial-update: 2025-05-1
source-git-commit: 603cc86892f518852552eaa2fe1bdeaa296137cf
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 2%

---

# [!DNL Reddit] Conversions-API-Erweiterung - Übersicht

Reddit ist eine Social-Media-Plattform mit einer vielfältigen Nutzerbasis, die sich ideal für Werbetreibende eignet, die bestimmte Zielgruppen ansprechen.

Verwenden Sie die [[!DNL Reddit] Konversions-API](https://ads-api.reddit.com/docs/v2/#tag/Conversions-API)Erweiterung, um in Adobe Experience Platform Edge Network erfasste Benutzerinteraktionsereignisse an [!DNL Reddit Ads] zu senden. Mit dieser Erweiterung können Sie Ihrer Marke helfen, eine Zielgruppe von mehr als 379 Millionen aktiven wöchentlichen Benutzern zu erreichen, das Benutzerverhalten besser zu verstehen und zielgerichtete Werbung zu schalten.

Lesen Sie dieses Handbuch, um zu erfahren, wie Sie die [!DNL Reddit] Conversions-API-Erweiterung in Ihrer Ereignisweiterleitung (Regeln[ installieren, konfigurieren und ](https://experienceleague.adobe.com/de/docs/experience-platform/tags/ui/rules).

## Wichtigste Vorteile {#benefits}

Verwenden Sie die API-Erweiterung „Reddit Conversions“ für Folgendes:

- **Erreichen Sie Ihre Zielgruppe**: Interagieren Sie mit über 379 Millionen aktiven Benutzern pro Woche auf [!DNL Reddit].
- **Benutzerverhalten analysieren**: Nutzen Sie Benutzerinteraktionsdaten, um das Verhalten zu verstehen und Kampagnen zu optimieren.
- **Bereitstellung zielgerichteter Anzeigen**: Führen Sie personalisierte Anzeigen auf der Grundlage von in Adobe Experience Platform erfassten Benutzerinteraktionen aus.

## Voraussetzungen {#prerequisites}

Sie müssen über ein gültiges Reddit Ads-Konto verfügen, um diese Erweiterung verwenden zu können. Navigieren Sie [[!DNL Reddit Ads] Registrierungsseite](https://business.reddithelp.com/s/article/Create-and-manage-your-Reddit-Ads-account), um sich zu registrieren und ein Konto zu erstellen, falls Sie noch keines haben. Nachdem Sie Ihr Konto eingerichtet haben, fordern [Zugriff auf die Ads-API an](https://www.redditforbusiness.com/api-partnership).

### Sammeln erforderlicher Konfigurationsdetails {#configuration-details}

Um den Experience Platform mit [!DNL Reddit] zu verbinden, sind die folgenden Eingaben erforderlich:

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| Pixel-ID | Die Pixel-ID ist eine eindeutige Kennung, die mit Ihrem [!DNL Reddit Ads]-Konto verknüpft ist. Er wird verwendet, um Benutzerinteraktionen und Konversionsereignisse auf Ihrer Website oder in Ihrer App zu verfolgen. Sie finden Ihre Pixel-ID in Ihrem [!DNL Reddit Ads] [Konto](https://ads.reddit.com/accounts). | 123456789012 |
| Konversionszugriffstoken | Ihr [!DNL Reddit]-Konversions-Zugriffstoken. Eine Anleitung dazu finden [[!DNL Reddit]  im Dokument ](https://business.reddithelp.com/s/article/conversion-access-token)Konversions-API“. <br> **Sie müssen diesen Prozess nur einmal durchlaufen, da dieses Token nicht abläuft.** | {YOUR_REDDIT_BEARER_TOKEN} |

## Installieren und Konfigurieren der [!DNL Reddit] {#install-configure}

Führen Sie die folgenden Schritte aus, um die [!DNL Reddit] Conversions-API-Erweiterung zu installieren und zu konfigurieren:

1. Wählen Sie in der Datenerfassungs-UI von Experience Platform [!UICONTROL Erweiterungen] in der linken Navigationsleiste aus, um auf den [!UICONTROL Erweiterungen]-Katalog zuzugreifen. Erstellen [ dann eine neue Ereignisweiterleitungs-Eigenschaft ](https://experienceleague.adobe.com/de/docs/experience-platform/tags/event-forwarding/overview#properties) wählen Sie eine vorhandene Eigenschaft aus.
2. Navigieren Sie **[!UICONTROL linken Navigationsbereich zu]** Erweiterungen“. Wählen Sie **[!UICONTROL Katalog]** und wählen Sie dann die **[!DNL Reddit]** aus.
   ![Der Adobe Experience Platform Extensions-Katalog mit hervorgehobener Reddit-Erweiterung.](../../../images/extensions/server/reddit/reddit-extension.png)
3. Geben Sie die folgenden Konfigurationsdetails an:
   - **Pixel-ID**: Geben Sie Ihre [!DNL Reddit Ads] Pixel-ID ein.
   - **Konversionszugriffs-Token**: Geben Sie das in Ihrem [!DNL Reddit Ads]-Konto generierte Token ein und wählen Sie **[!UICONTROL Speichern]**, wenn Sie fertig sind.

     ![Konfigurationsdetails für die API-Erweiterung „Reddit Conversions“, einschließlich Feldern für Pixel-ID und Konversionszugriffs-Token.](../../../images/extensions/server/reddit/reddit-capi-details.png)

## Konfigurieren einer Ereignisweiterleitungsregel {#config-rule}

Erstellen Sie nach dem Einrichten der Datenelemente Regeln für die Ereignisweiterleitung, um zu bestimmen, wann und wie Ereignisse an [!DNL Reddit Ads] gesendet werden.

1. Navigieren Sie zu **Regeln** in Ihrer Ereignisweiterleitungs-Eigenschaft und erstellen Sie eine neue [Regel](https://experienceleague.adobe.com/de/docs/experience-platform/tags/ui/rules).
2. Fügen Sie **Aktionen** eine neue Aktion hinzu und legen Sie die Erweiterung auf **[!DNL Reddit CAPI]** fest.
3. Legen Sie den **Aktionstyp** auf &quot;**&quot;**.
   ![Regelkonfigurationsschnittstelle für die Ereignisweiterleitungsregel für die API-Erweiterung „Reddit Conversions“, wobei die Felder „Erweiterung“ und „Aktionstyp“ hervorgehoben sind.](../../../images/extensions/server/reddit/reddit-rule.png)
4. Konfigurieren Sie die zusätzlichen Steuerelemente für Ihr Ereignis, wie in der folgenden Tabelle dargestellt:

   | Feldname | Beschreibung | Beispiel |
   | --- | --- | --- |
   | `Event Name` | Geben Sie den Namen des Konversionsereignisses an. | `Purchase` |
   | `Event Type` | Definieren Sie den Ereignistyp, der ein [unterstütztes Reddit-Konversionsereignis](https://business.reddithelp.com/s/article/supported-conversion-events#supported-conversion-events) oder ein benutzerdefiniertes sein kann. | `SignUp`, `MyCustomEvent` |
   | `Timestamp` | Ereigniszeit im ISO-Format oder Epochenzeit angeben. | `2025-04-15T16:01:00.000Z`, `1744742460000` |
   | `Client Dedupe ID` | Hinzufügen einer eindeutigen ID für die Deduplizierung. | `abc123` |
   | `Match Keys` | Benutzer- und Gerätekennungen für die Attribution einschließen. | `{"email":"hashed_email@example.com", "phone":"hashed_phone"}` |
   | `Value` | Geben Sie den Geldwert des Ereignisses an. | `99.99` |
   | `Currency Code` | Verwenden Sie das ISO-4217-Format für die Währung. | `USD` |
   | `Units Sold` | Geben Sie die Menge der gekauften Artikel ein. | `3` |
   | `Country Code` | Geben Sie das Land an, in dem das Ereignis aufgetreten ist. | `US` |
   | `Data Processing Options` | Fügen Sie Datenschutzkennzeichnungen wie LDU (Limited Data Usage) hinzu. | `{"modes":["LDU"],"country":"US","region":"US-NY"}` |
   | `Consent` | Geben Sie das Einverständnis des Benutzers zur Datennutzung in der Werbung an. | `true` |

5. Wählen **Änderungen beibehalten**, um die Regel zu speichern.

## Ereignis-Metadaten {#event-metadata}

Lesen Sie diesen Abschnitt für eine detaillierte Aufschlüsselung der Felder für Ereignismetadaten und Benutzerdaten, um sicherzustellen, dass Sie die erforderlichen und optionalen Parameter zum Konfigurieren Ihrer Ereignisse verstehen. Die angezeigten Felder können je nach ausgewähltem Ereignistyp variieren.

>[!NOTE]
>
>Um die besten Ergebnisse aus Ihren Konversionsereignissen zu erhalten, füllen Sie bei der Einrichtung von (dynamischen [) alle Felder ](https://business.reddithelp.com/s/article/dynamic-product-ads).

### Ereignis-Metadatenfelder

![Konfigurationsdetails für die API-Erweiterung „Reddit Conversions“, einschließlich Feldern für Pixel-ID und Konversionszugriffs-Token.](../../../images/extensions/server/reddit/reddit-event-metadata.png)

| Feldname | Beschreibung | Beispiel |
| --- | --- | --- |
| `Conversion ID` (erforderlich) | Die eindeutige ID für das Konversionsereignis, die für die Deduplizierung verwendet wird. | `abc123` |
| `Item Count` | Die Gesamtzahl der Elemente für das Konversionsereignis. | `6` |
| `Currency` | Die Währung für den Wert wird im [ISO-4217](https://www.iso.org/iso-4217-currency-codes.html)-Format angegeben. | `USD` |
| `Value` | Der gesamte monetäre Wert des Konversionsereignisses einschließlich der Dezimalstellen. | `1.23` |
| `Products` | Ein JSON-Array von Objekten mit Details zu den Produkten, die mit dem Ereignis verknüpft sind. Jedes Objekt muss mindestens einen `id` enthalten. | `[{"id":"SKU123","name":"ProductName","category":"CategoryName"},{"id":"SKU456","name":"ProductName","category":"CategoryName"}]` |

### Benutzerdatenfelder

Die folgenden Parameter sind optional, werden jedoch empfohlen:

| Feldname | Beschreibung | Beispiel |
| --- | --- | --- |
| `Email` (dringend empfohlen) | Eine gehashte oder nicht gehashte Benutzer-E-Mail. | `example@email.com` |
| `External ID` | Eine Hash- oder Unhash-Advertiser-zugewiesene Benutzer-ID. | `customer12345` |
| `UUID` (dringend empfohlen) | Die vom Reddit-Pixel auf Ihrer Website generierte ID. | `1677712978045.b8f7eb7d-b357-437b-8bd3-e1c8166c7132` |
| `IP Address` (dringend empfohlen) | Die Geräte-IP-Adresse des Benutzers. | `192.168.0.1` |
| `User Agent` (dringend empfohlen) | Der vom Benutzer verwendete Browser oder die App. | `Chrome/98.0.4758.102` |
| `IDFA` | Eine gehashte oder ungehashte Apple-Kennung für Advertiser. | `8A2E4F6D-0852-4B2A-B9D5-79334DE14B16` |
| `AAID` | Eine gehashte oder ungehashte Android Advertising ID. | `38400000-8cf0-11bd-b23e-10b96e40000d` |
| `Screen Width` | Die Breite der Anzeige des Benutzers. | `1920` |
| `Screen Height` | Die Höhe der Anzeige des Benutzers. | `1080` |
| `Data Processing Options` (JSON-Format) | Die Datenschutzeinstellungen des Benutzers. Unterstützt nur LDU (Eingeschränkte Datennutzung). | `{"modes":["LDU"],"country":"US","region":"US-NY"}` |

### Wichtige Überlegungen

Vor dem Senden von Daten an [!DNL Reddit Ads] werden die Werte der folgenden Felder von der Erweiterung gehasht und normalisiert: `Email`, `External ID`, `IDFA` und `AAID`. Die Erweiterung hasst diese Werte nicht erneut, wenn sie bereits in [!DNL SHA-256] gehasht wurden.

## Validieren und Bereitstellen {#validate-deploy}

Validieren Sie nach dem Konfigurieren der Erweiterung und der Regeln die Integration, indem Sie die Ereignisdaten im [[!DNL Reddit Ads] Ereignis-Manager](https://business.reddithelp.com/s/article/Events-Manager) überprüfen. Verwenden Sie den [Match Quality Score (MQS](https://business.reddithelp.com/s/article/match-quality-score), um die Genauigkeit und Zuverlässigkeit Ihrer Signalintegrationen zu bewerten.

Weitere Informationen zu [!DNL Reddit Ads] finden Sie in der [Dokumentation zu Reddit Ads](https://ads.reddit.com/).

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Dokuments sollten Sie jetzt wissen, wie Sie die [!DNL Reddit] Conversions-API-Erweiterung konfigurieren und verwenden. Weitere Informationen zu den Ereignisweiterleitungsfunktionen in Adobe Experience Platform finden Sie in der [Übersicht über die Ereignisweiterleitung](../../../ui/event-forwarding/overview.md) oder in den folgenden Ressourcen:

- [Übereinstimmungsschlüssel freigeben](https://business.reddithelp.com/s/article/about-attribution-matching-signals) und [Ereignismetadaten](https://business.reddithelp.com/s/article/about-event-metadata): Erfahren Sie, wie Sie Übereinstimmungsschlüssel und Ereignismetadaten effektiv freigeben.
- [Ereignisse deduplizieren](https://business.reddithelp.com/s/article/event-deduplication): Stellen Sie durch Deduplizierung von Ereignissen eine genaue Ereignisverfolgung sicher.
- [Erstellen eines Konversionszugriffs-Tokens](https://business.reddithelp.com/helpcenter/s/article/conversion-access-token): Führen Sie die Schritte aus, um ein Konversionszugriffs-Token für die sichere API-Authentifizierung zu erstellen.
