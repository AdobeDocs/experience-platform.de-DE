---
title: Übersicht über die Trade Desk Real-Time Conversions API-Erweiterung
description: Erfahren Sie mehr über die Trade Desk Real-Time Conversions API-Erweiterung für die Ereignisweiterleitung in Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: d9d185685106ac160dcbefc5e9567a85c8302a73
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 3%

---

# [!DNL The Trade Desk Real-Time Conversions API] Erweiterungsübersicht

Sie können die [[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi) Erweiterung zum Senden von Daten vom Adobe Experience Platform-Edge Network an [!DNL The Trade Desk] durch Nutzung der API-Funktionen in Ihren [Ereignisweiterleitung](../../../ui/event-forwarding/overview.md) Regeln.

Verwenden [!DNL The Trade Desk Real-Time Conversions API] -Erweiterung verwenden, können Sie die API-Funktionen in Ihrer [Ereignisweiterleitung](../../../ui/event-forwarding/overview.md) Regeln zum Senden von Daten an [!DNL The Trade Desk] vom Adobe Experience Platform-Edge Network aus.

In diesem Dokument erfahren Sie, wie Sie die Erweiterung installieren und ihre Funktionen in der Ereignisweiterleitung verwenden. [Regel](../../../ui/managing-resources/rules.md).

>[!NOTE]
>
>Diese Erweiterungs- und Dokumentationsseite wird von [!DNL The Trade Desk] Team. Bei Fragen oder Aktualisierungsanfragen kontaktieren Sie diese bitte direkt.

## Voraussetzungen {#prerequisites}

Sie müssen über eine relevante Advertiser-ID, eine UPixel-ID und eine Tracker-ID in Ihrer [!DNL The Trade Desk] -Konto, um die [[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi).

>[!INFO]
>
>Wenn Sie ein Händler sind, müssen Sie auch Ihre Merchant-ID abrufen.

## Installieren und konfigurieren Sie die [!DNL The Trade Desk] Echtzeit-Konversions-API {#install}

So installieren Sie die Erweiterung: [Erstellen einer Ereignisweiterleitungs-Eigenschaft](../../../ui/event-forwarding/overview.md#properties) oder wählen Sie eine vorhandene Eigenschaft aus, die Sie stattdessen bearbeiten möchten.

Wählen Sie **[!UICONTROL Erweiterungen]** in der linken Navigation aus. Im **[!UICONTROL Katalog]** auswählen, wählen Sie die **[!UICONTROL Handelsabteilung]** API-Karte für Echtzeitkonversionen auswählen und **[!UICONTROL Installieren]**.

![Der Erweiterungskatalog, der die [!DNL The Trade Desk] Erweiterungskartenmarkierung.](../../../images/extensions/server/tradedesk/install-extension.png)

Geben Sie im nächsten Bildschirm die [!UICONTROL Advertiser-ID]und optional eine [!UICONTROL Merchant-ID]. Sie können die IDs direkt in diese Eingaben einfügen oder stattdessen ein Datenelement verwenden. Diese Werte dienen als Standardwerte, die beim Ausführen eines Ereignisaufrufs zu verwendet werden. [!DNL The Trade Desk] Echtzeit-Konversions-API. Wählen Sie **[!UICONTROL Speichern]**, wenn Sie fertig sind.

Um zu erfahren, wie Sie Datenelemente erstellen und sie für Erweiterungen in Ihrer Tag-Eigenschaft verfügbar machen können, folgen Sie dem [Erstellen von Datenelementen](https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/tags/create-data-elements) Tutorial.

![Die [!DNL The Trade Desk] Erweiterungskonfigurationsseite mit [!UICONTROL Advertiser-ID] und [!UICONTROL Merchant-ID] hervorgehobene Felder.](../../../images/extensions/server/tradedesk/configure-extension.png)

Die -Erweiterung ist installiert und Sie können jetzt ihre Funktionen in Ihren Ereignisweiterleitungsregeln verwenden.

## Konfigurieren einer Ereignisweiterleitungsregel {#rule}

Nachdem Sie die Erweiterung installiert und konfiguriert haben, können Sie mit der Erstellung von Ereignisweiterleitungsregeln beginnen, die bestimmen, wie und wann Ereignisse an gesendet werden [!DNL The Trade Desk].

Sie sollten erwägen, mehrere Regeln zu konfigurieren, um alle akzeptierten zu senden [Anfrageeigenschaften](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties) via [!DNL The Trade Desk] und [!DNL The Trade Desk] Echtzeit-Konversions-API.

>[!NOTE]
>
>Ereignisse sollten in Echtzeit oder so nah wie möglich in Echtzeit gesendet werden.

Neue Ereignisweiterleitung erstellen [Regel](../../../ui/managing-resources/rules.md) in Ihrer Ereignisweiterleitungseigenschaft. under **[!UICONTROL Aktionen]**, fügen Sie eine neue Aktion hinzu und legen Sie die Erweiterung auf **[!UICONTROL Handelsabteilung]**. Wählen Sie als Nächstes **[!UICONTROL Echtzeit-Konversion]** für die **[!UICONTROL Aktionstyp]**.

![Die Ansicht &quot;Eigenschaftsregeln für die Ereignisweiterleitung&quot;mit den Feldern, die zum Hinzufügen einer Aktionskonfiguration für Ereignisweiterleitungsregeln erforderlich sind, hervorgehoben.](../../../images/extensions/server/tradedesk/tradedesk-event-action.png)

Nach der Auswahl scheinen zusätzliche Steuerelemente die Ereignisdaten, die an gesendet werden, weiter zu konfigurieren [!DNL The Trade Desk]. Auswählen **[!UICONTROL Änderungen beibehalten]** , um die Regel zu speichern.

Die Konfigurationsoptionen sind wie unten beschrieben in drei Hauptabschnitte unterteilt:

**[!UICONTROL Grundlegende Anfrageeigenschaften]**

| Eingabe | Beschreibung |
| --- | --- |
| Tracker-ID | Die Plattform-ID des Ereignistrackers. |
| UPixel-ID | Die universelle Pixel-ID für das Ereignis. |
| Referrer-URL | Die Website-URL, von der aus das Ereignis aufgetreten ist (falls vorhanden). |
| Ereignisname | Der von der Partnerplattform definierte Ereignistyp. |
| Wert | Der Umsatz-Tracking-Wert in Dezimalzeichenfolge (z. B. &quot;19.98&quot;). |
| Währung | Währungscode im ISO-Format. |
| Client-IP | Die IP-Adresse des Clients IPv4 oder IPv6. |
| Anzeigen-ID | Die eindeutige Anzeigen-ID für das Ereignis. |
| Anzeigen-ID-Typ | Der Typ der Anzeigen-ID, der in der Eigenschaft &quot;AD ID&quot;angegeben ist: TDID, IDFA, AAID, DAID, NAID, IDL, EUID oder UID2. |
| Impression | Eine 36-stellige Zeichenfolge (einschließlich Bindestrichen), die als eindeutige ID für die Impression dient, der das Ereignis zugeordnet wird. |
| Auftrags-ID | Die zugehörige Bestellkennung des Ereignisses. |
| td1-td10 | Zehn sequenziell nummerierte benutzerdefinierte dynamische Eigenschaften, die zur Bereitstellung zusätzlicher Konversionsmetadaten verwendet werden können. |

{style="table-layout:auto"}

![Die [!DNL Basic Request Properties] -Abschnitt mit Beispieldaten in die Felder.](../../../images/extensions/server/tradedesk/configure-extension-basic-request-properties.png)

Siehe Abschnitt [!DNL The Trade Desk] Entwicklerdokumentation für weitere Informationen zu [Anfrageeigenschaften](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties) akzeptiert von [!DNL The Trade Desk] Echtzeit-Konversions-API.

**[!UICONTROL Objektanforderungsparameter]**

Ein JSON-Objekt mit weiteren Informationen. Sie haben die Möglichkeit, einen reduzierten Satz von Schlüsselwerteingaben zu verwenden oder rohe JSON-Daten bereitzustellen. Darüber hinaus können Sie dynamische Daten aus einem Datenelement abrufen, indem Sie die Festplatten (![Diskettensymbol](../../../images/extensions/server/tradedesk/disk-icon.png)) rechts.


![Die [!DNL Object Request Parameters] Abschnitt mit verfügbaren Feldern.](../../../images/extensions/server/tradedesk/configure-object-request-params.png)

Siehe Abschnitt [Echtzeit-Konversionsereignis](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties-items) Dokumentation für weitere Informationen zu [!UICONTROL Objektanforderungsparameter] und deren Eigenschaften.

**[!UICONTROL Konfigurationsüberschreibungen]**

>[!NOTE]
>
>Die [!UICONTROL Konfigurationsüberschreibungen] -Felder können Sie eine andere [!DNL Advertiser ID] und/oder [!DNL Merchant ID] auf jeder Regel.

| Eingabe | Beschreibung |
| --- | --- |
| Advertiser-ID | Eindeutige Kennung für den Advertiser, mit dem dieses Ereignis verknüpft ist. Es kann eine andere Advertiser-ID bereitgestellt werden, um die in der Erweiterungskonfiguration angegebene ID zu überschreiben. |
| Merchant-ID | Die eindeutige Kennung, die jeder Händler von [!DNL The Trade Desk] während des gesamten Onboarding-Verfahrens. Es kann eine andere Merchant-ID bereitgestellt werden, um die in der Erweiterungskonfiguration angegebene ID zu überschreiben. |

![Die [!DNL Configuration Overrides] Abschnitt mit verfügbaren Feldern.](../../../images/extensions/server/tradedesk/configure-overrides.png)

Wenn Sie mit der Regel zufrieden sind, wählen Sie **[!UICONTROL In Bibliothek speichern]**. Veröffentlichen Sie schließlich eine neue Ereignisweiterleitung [build](../../../ui/publishing/builds.md) um die Änderungen zu aktivieren, die an der Bibliothek vorgenommen wurden.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie serverseitige Ereignisdaten an senden [!DNL The Trade Desk] mithilfe der [!DNL The Trade Desk] API-Erweiterung für Echtzeitkonversionen . Von hier aus wird empfohlen, Ihre Integration zu erweitern, indem separate Regeln erstellt werden, die spezifische Konversionsereignisse je nach Kampagne senden. Weitere Informationen zu den Ereignisweiterleitungsfunktionen finden Sie unter [!DNL Adobe Experience Platform], lesen Sie die [Übersicht über die Ereignisweiterleitung](../../../ui/event-forwarding/overview.md).

Siehe [!DNL The Trade Desk] Dokumentation zu [Best Practices für [!DNL The Trade Desk] Echtzeit-Konversions-API](https://www.facebook.com/business/help/308855623839366?id=818859032317965) für weitere Anleitungen zur effektiven Implementierung Ihrer Integration.

Weitere Informationen zum Debugging Ihrer Implementierung mithilfe des Experience Platform Debugger- und Ereignisweiterleitungs-Überwachungstools finden Sie in der [Übersicht über Adobe Experience Platform Debugger](../../../../debugger/home.md) und [Überwachen von Aktivitäten in der Ereignisweiterleitung](../../../ui/event-forwarding/monitoring.md).
