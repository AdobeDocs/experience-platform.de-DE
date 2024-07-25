---
title: Übersicht über die Trade Desk Real-Time Conversions API-Erweiterung
description: Erfahren Sie mehr über die Trade Desk Real-Time Conversions API-Erweiterung für die Ereignisweiterleitung in Adobe Experience Platform.
hide: true
hidefromtoc: true
exl-id: 1ff32e2b-9ff8-4395-ae44-cba75a2da515
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 3%

---

# Übersicht über die [!DNL The Trade Desk Real-Time Conversions API]-Erweiterung

Sie können die Erweiterung [[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi) verwenden, um Daten vom Adobe Experience Platform-Edge Network an [!DNL The Trade Desk] zu senden, indem Sie die API-Funktionen in Ihren [Ereignisweiterleitungsregeln](../../../ui/event-forwarding/overview.md) verwenden.

Mit der Erweiterung [!DNL The Trade Desk Real-Time Conversions API] können Sie die API-Funktionen in Ihren [Ereignisweiterleitungsregeln](../../../ui/event-forwarding/overview.md) nutzen, um Daten vom Adobe Experience Platform-Edge Network an [!DNL The Trade Desk] zu senden.

In diesem Dokument erfahren Sie, wie Sie die Erweiterung installieren und ihre Funktionen in einer Ereignisweiterleitung verwenden, [Regel](../../../ui/managing-resources/rules.md).

>[!NOTE]
>
>Diese Erweiterungs- und Dokumentationsseite wird vom [!DNL The Trade Desk] -Team verwaltet. Bei Fragen oder Aktualisierungsanfragen kontaktieren Sie diese bitte direkt.

## Voraussetzungen {#prerequisites}

Sie müssen über eine relevante Advertiser-ID, eine UPixel-ID und eine Tracker-ID in Ihrem [!DNL The Trade Desk]-Konto verfügen, um die [[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi) zu konfigurieren.

>[!INFO]
>
>Wenn Sie ein Händler sind, müssen Sie auch Ihre Merchant-ID abrufen.

## Installieren und Konfigurieren der [!DNL The Trade Desk] Real-Time Conversions API {#install}

Um die Erweiterung zu installieren, erstellen Sie [eine Ereignisweiterleitungs-Eigenschaft](../../../ui/event-forwarding/overview.md#properties) oder wählen Sie eine vorhandene Eigenschaft aus, die stattdessen bearbeitet werden soll.

Wählen Sie **[!UICONTROL Erweiterungen]** in der linken Navigation aus. Wählen Sie auf der Registerkarte **[!UICONTROL Katalog]** die Karte **[!UICONTROL Trade Desk]** Real-Time Conversions API und dann **[!UICONTROL Install]**.

![Der Erweiterungskatalog, der die Installation der Erweiterungskarte [!DNL The Trade Desk] hervorhebt.](../../../images/extensions/server/tradedesk/install-extension.png)

Geben Sie im nächsten Bildschirm die [!UICONTROL Advertiser-ID] und optional eine [!UICONTROL Merchant-ID] ein. Sie können die IDs direkt in diese Eingaben einfügen oder stattdessen ein Datenelement verwenden. Diese Werte dienen als Standardwerte, die beim Ausführen eines Ereignisaufrufs für die [!DNL The Trade Desk] Echtzeit-Konversions-API verwendet werden. Wählen Sie **[!UICONTROL Speichern]**, wenn Sie fertig sind.

Um zu erfahren, wie Sie Datenelemente erstellen und sie für Erweiterungen in Ihrer Tag-Eigenschaft verfügbar machen können, befolgen Sie das Tutorial [Datenelemente erstellen](https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/tags/create-data-elements) .

![Die Konfigurationsseite der Erweiterung [!DNL The Trade Desk] mit den Feldern [!UICONTROL Advertiser-ID] und [!UICONTROL Merchant-ID] wurde hervorgehoben.](../../../images/extensions/server/tradedesk/configure-extension.png)

Die -Erweiterung ist installiert und Sie können jetzt ihre Funktionen in Ihren Ereignisweiterleitungsregeln verwenden.

## Konfigurieren einer Ereignisweiterleitungsregel {#rule}

Nachdem Sie die Erweiterung installiert und konfiguriert haben, können Sie mit der Erstellung von Ereignisweiterleitungsregeln beginnen, die bestimmen, wie und wann Ereignisse an [!DNL The Trade Desk] gesendet werden.

Sie sollten in Erwägung ziehen, mehrere Regeln zu konfigurieren, um alle akzeptierten [Anfrageeigenschaften](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties) über die API für die Echtzeit-Konvertierung [!DNL The Trade Desk] und [!DNL The Trade Desk] zu senden.

>[!NOTE]
>
>Ereignisse sollten in Echtzeit oder so nah wie möglich in Echtzeit gesendet werden.

Erstellen Sie in Ihrer Ereignisweiterleitungseigenschaft eine neue Ereignisweiterleitungsregel [Regel](../../../ui/managing-resources/rules.md). Fügen Sie unter **[!UICONTROL Aktionen]** eine neue Aktion hinzu und legen Sie die Erweiterung auf **[!UICONTROL The Trade Desk]** fest. Wählen Sie als Nächstes **[!UICONTROL Echtzeit-Konversion]** für den **[!UICONTROL Aktionstyp]** aus.

![Die Ansicht &quot;Eigenschaftsregeln für die Ereignisweiterleitung&quot;mit den Feldern, die zum Hinzufügen einer Aktionskonfiguration für die Ereignisweiterleitung erforderlich sind, hervorgehoben.](../../../images/extensions/server/tradedesk/tradedesk-event-action.png)

Nach der Auswahl scheinen zusätzliche Steuerelemente die Ereignisdaten, die an [!DNL The Trade Desk] gesendet werden, weiter zu konfigurieren. Wählen Sie **[!UICONTROL Änderungen beibehalten]** aus, um die Regel zu speichern.

Die Konfigurationsoptionen sind wie unten beschrieben in drei Hauptabschnitte unterteilt:

**[!UICONTROL Grundlegende Anforderungseigenschaften]**

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

![Der Abschnitt [!DNL Basic Request Properties], der Beispieldaten in die Felder eingibt.](../../../images/extensions/server/tradedesk/configure-extension-basic-request-properties.png)

Weitere Informationen zu den [Anforderungseigenschaften](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties), die von der [!DNL The Trade Desk] Real-Time Conversions API akzeptiert werden, finden Sie in der [!DNL The Trade Desk] Entwicklerdokumentation .

**[!UICONTROL Objektanforderungsparameter]**

Ein JSON-Objekt mit weiteren Informationen. Sie haben die Möglichkeit, einen reduzierten Satz von Schlüsselwerteingaben zu verwenden oder rohe JSON-Daten bereitzustellen. Darüber hinaus können Sie dynamische Daten aus einem Datenelement abrufen, indem Sie rechts die Festplatten (![Diskettensymbol](/help/images/icons/database.png)) auswählen.


![ Der Abschnitt [!DNL Object Request Parameters] mit den verfügbaren Feldern.](../../../images/extensions/server/tradedesk/configure-object-request-params.png)

Weitere Informationen zu den [!UICONTROL Objektanforderungsparametern] und ihren Eigenschaften finden Sie in der Dokumentation zum [Echtzeit-Konversionsereignis](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties-items) .

**[!UICONTROL Konfigurationsüberschreibungen]**

>[!NOTE]
>
>Mit den Feldern [!UICONTROL Konfigurationsüberschreibungen] können Sie für jede Regel einen anderen [!DNL Advertiser ID] und/oder einen anderen [!DNL Merchant ID] festlegen.

| Eingabe | Beschreibung |
| --- | --- |
| Advertiser-ID | Eindeutige Kennung für den Advertiser, mit dem dieses Ereignis verknüpft ist. Es kann eine andere Advertiser-ID bereitgestellt werden, um die in der Erweiterungskonfiguration angegebene ID zu überschreiben. |
| Merchant-ID | Die eindeutige Kennung, die jeder Händler während des gesamten Onboarding-Verfahrens von [!DNL The Trade Desk] erhält. Es kann eine andere Merchant-ID bereitgestellt werden, um die in der Erweiterungskonfiguration angegebene ID zu überschreiben. |

![ Der Abschnitt [!DNL Configuration Overrides] mit den verfügbaren Feldern.](../../../images/extensions/server/tradedesk/configure-overrides.png)

Wenn Sie mit der Regel zufrieden sind, wählen Sie **[!UICONTROL In Bibliothek speichern]** aus. Veröffentlichen Sie abschließend eine neue Ereignisweiterleitung [build](../../../ui/publishing/builds.md) , um die an der Bibliothek vorgenommenen Änderungen zu aktivieren.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie serverseitige Ereignisdaten mit der API-Erweiterung [!DNL The Trade Desk] für Echtzeitkonversionen an [!DNL The Trade Desk] senden. Von hier aus wird empfohlen, Ihre Integration zu erweitern, indem separate Regeln erstellt werden, die spezifische Konversionsereignisse je nach Kampagne senden. Weitere Informationen zu den Ereignisweiterleitungsfunktionen in [!DNL Adobe Experience Platform] finden Sie in der [Übersicht über die Ereignisweiterleitung](../../../ui/event-forwarding/overview.md).

Weitere Anleitungen zur effektiven Implementierung Ihrer Integration finden Sie in der Dokumentation zu [!DNL The Trade Desk] Best Practices für die  [!DNL The Trade Desk] Echtzeit-Konversions-API](https://www.facebook.com/business/help/308855623839366?id=818859032317965) .[

Weitere Informationen zum Debugging Ihrer Implementierung mithilfe des Experience Platform Debugger- und Ereignisweiterleitungs-Überwachungstools finden Sie in der [Adobe Experience Platform Debugger-Übersicht](../../../../debugger/home.md) und in der [Überwachung der Aktivitäten in der Ereignisweiterleitung](../../../ui/event-forwarding/monitoring.md).
