---
title: Übersicht über die Erweiterung der Trade Desk Real-time Conversions-API
description: Erfahren Sie mehr über die Real-Time Conversions-API-Erweiterung von Trade Desk für die Ereignisweiterleitung in Adobe Experience Platform.
exl-id: 1ff32e2b-9ff8-4395-ae44-cba75a2da515
source-git-commit: eb650da02ac69c5afbebfe6ba371cc19617f79d0
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 3%

---

# [!DNL The Trade Desk Real-Time Conversions API] - Übersicht

Sie können die [[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi)-Erweiterung verwenden, um Daten aus dem Adobe Experience Platform-Edge Network an [!DNL The Trade Desk] zu senden, indem Sie die API-Funktionen in Ihren Regeln [Ereignisweiterleitung](../../../ui/event-forwarding/overview.md) nutzen.

Mit [!DNL The Trade Desk Real-Time Conversions API] -Erweiterung können Sie die Funktionen der API in Ihren Regeln [Ereignisweiterleitung“ nutzen](../../../ui/event-forwarding/overview.md) um Daten aus dem Adobe Experience Platform-Edge Network an [!DNL The Trade Desk] zu senden.

Lesen Sie dieses Dokument, um zu erfahren, wie Sie die Erweiterung installieren und ihre Funktionen in einer Ereignisweiterleitungsregel ([) ](../../../ui/managing-resources/rules.md).

>[!NOTE]
>
>Diese Erweiterungs- und Dokumentationsseite wird von [!DNL The Trade Desk] Team gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an die Kontaktperson.

## Voraussetzungen {#prerequisites}

Sie müssen über eine relevante Advertiser-ID, UPixel-ID und Tracker-ID verfügen, die in Ihrem [!DNL The Trade Desk]-Konto erforderlich sind, um die [[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi) zu konfigurieren.

>[!INFO]
>
>Wenn Sie ein Händler sind, müssen Sie auch Ihre Händler-ID erhalten.

## Installieren und Konfigurieren der [!DNL The Trade Desk] Echtzeit-Konversions-API {#install}

Um die Erweiterung zu installieren[ erstellen Sie eine Ereignisweiterleitungseigenschaft oder ](../../../ui/event-forwarding/overview.md#properties) Sie stattdessen eine vorhandene Eigenschaft aus, die bearbeitet werden soll.

Wählen Sie **[!UICONTROL Erweiterungen]** in der linken Navigation aus. Wählen Sie auf **[!UICONTROL Registerkarte]** die API-Karte **[!UICONTROL The Trade Desk]** Real-Time Conversions aus und klicken Sie dann auf **[!UICONTROL Installieren]**.

![Der Erweiterungskatalog mit der [!DNL The Trade Desk] Erweiterungskarte, in der install hervorgehoben ist.](../../../images/extensions/server/tradedesk/install-extension.png)

Geben Sie im nächsten Bildschirm die [!UICONTROL Advertiser-ID] und optional eine [!UICONTROL Händler-ID] ein. Sie können die IDs direkt in diese Eingaben einfügen oder stattdessen ein Datenelement verwenden. Diese dienen als Standardwerte, die bei einem Ereignisaufruf an [!DNL The Trade Desk] Echtzeit-Konversions-API verwendet werden. Wählen Sie **[!UICONTROL Speichern]**, wenn Sie fertig sind.

Um zu erfahren, wie Sie Datenelemente erstellen und sie Erweiterungen in Ihrer Tag-Eigenschaft zur Verfügung stellen können, folgen Sie dem Tutorial [Datenelemente erstellen](https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/tags/create-data-elements) .

![Die Konfigurationsseite der [!DNL The Trade Desk]-Erweiterung mit den [!UICONTROL Advertiser-ID] und [!UICONTROL Händler-ID] hervorgehobenen Feldern.](../../../images/extensions/server/tradedesk/configure-extension.png)

Die Erweiterung ist installiert und Sie können jetzt ihre Funktionen in Ihren Ereignisweiterleitungsregeln verwenden.

## Konfigurieren einer Ereignisweiterleitungsregel {#rule}

Nachdem Sie die Erweiterung installiert und konfiguriert haben, können Sie mit der Erstellung von Ereignisweiterleitungsregeln beginnen, die bestimmen, wie und wann Ihre Ereignisse an [!DNL The Trade Desk] gesendet werden.

Sie sollten erwägen, mehrere Regeln zu konfigurieren, um alle akzeptierten [Anfrageeigenschaften](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties) über die [!DNL The Trade Desk] und [!DNL The Trade Desk] Echtzeit-Konversions-API zu senden.

>[!NOTE]
>
>Ereignisse sollten in Echtzeit oder so nah wie möglich an der Echtzeit gesendet werden.

Erstellen Sie eine neue [ (Regel](../../../ui/managing-resources/rules.md) in Ihrer Ereignisweiterleitungseigenschaft. Fügen Sie **[!UICONTROL Aktionen]** eine neue Aktion hinzu und legen Sie die Erweiterung auf **[!UICONTROL The Trade Desk]** fest. Wählen Sie als Nächstes **[!UICONTROL Echtzeit-]**) für den **[!UICONTROL Aktionstyp]**.

![Die Ansicht mit den Eigenschaftsregeln für die Ereignisweiterleitung mit den Feldern, die zum Hinzufügen einer Regelkonfiguration für die Ereignisweiterleitung erforderlich sind, ist hervorgehoben.](../../../images/extensions/server/tradedesk/tradedesk-event-action.png)

Nach der Auswahl erscheinen zusätzliche Steuerelemente, um die Ereignisdaten, die an [!DNL The Trade Desk] gesendet werden, weiter zu konfigurieren. Wählen **[!UICONTROL Änderungen beibehalten]**, um die Regel zu speichern.

Die Konfigurationsoptionen sind wie unten beschrieben in drei Hauptabschnitte unterteilt:

**[!UICONTROL Allgemeine Anfrageeigenschaften]**

| Eingabe | Beschreibung |
| --- | --- |
| Tracker-ID | Die Plattform-ID der Ereignisverfolgung. |
| BILDPUNKT-ID | Die universelle Pixel-ID für das Ereignis. |
| Referrer-URL | Die Website-URL, von der aus das Ereignis aufgetreten ist, falls vorhanden. |
| Ereignisname | Der von der Partnerplattform definierte Ereignistyp. |
| Wert | Der Wert für die Umsatzverfolgung in einer Dezimalzeichenfolge (z. B. „19.98„). |
| Währung | Währungscode im ISO-Format. |
| Client-IP | Die IPv4- oder IPv6-IP-Adresse des Clients. |
| Anzeigen-ID | Die eindeutige Werbe-ID für die Veranstaltung. |
| Anzeigen-ID-Typ | Der Typ der Werbe-ID, der in der Eigenschaft der Anzeigenkennung angegeben ist: TDID, IDFA, AAID, DAID, NAID, IDL, EUID oder UID2. |
| Impression | Eine 36-stellige Zeichenfolge (einschließlich Bindestrichen), die als eindeutige ID für die Impression dient, der das Ereignis zugeordnet wird. |
| Auftrags-ID | Die Kennung der zugehörigen Bestellung des Ereignisses. |
| td1-td10 | Zehn sequenziell nummerierte benutzerdefinierte dynamische Eigenschaften, die zur Bereitstellung zusätzlicher Konversionsmetadaten verwendet werden können. |

{style="table-layout:auto"}

![Der [!DNL Basic Request Properties] Abschnitt mit Beispieldaten, die in die Felder eingegeben werden.](../../../images/extensions/server/tradedesk/configure-extension-basic-request-properties.png)

In der Entwicklerdokumentation zu [!DNL The Trade Desk] finden Sie weitere Informationen zu den [Anfrageeigenschaften](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties) die von [!DNL The Trade Desk] Echtzeit-Konversions-API akzeptiert werden.

**[!UICONTROL Objektanforderungsparameter]**

Ein JSON-Objekt, das weitere Informationen enthält. Sie haben die Möglichkeit, einen reduzierten Satz von Schlüsselwerteingaben zu verwenden oder rohe JSON-Dateien bereitzustellen. Darüber hinaus können Sie dynamische Daten aus einem Datenelement abrufen, indem Sie die Festplatten (![Disk Icon](/help/images/icons/database.png)) auf der rechten Seite auswählen.


![Der [!DNL Object Request Parameters] Abschnitt mit den verfügbaren Feldern.](../../../images/extensions/server/tradedesk/configure-object-request-params.png)

Weitere Informationen zu den [Objektanforderungsparametern](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties-items) und deren Eigenschaften finden [!UICONTROL  in der Dokumentation zu ]Echtzeit-Konversionen“.

**[!UICONTROL Konfigurationsüberschreibungen]**

>[!NOTE]
>
>Die [!UICONTROL Konfigurationsüberschreibungen] ermöglichen es Ihnen, für jede Regel einen anderen [!DNL Advertiser ID] und/oder eine andere [!DNL Merchant ID] festzulegen.

| Eingabe | Beschreibung |
| --- | --- |
| Advertiser-ID | Eindeutige Kennung für den Advertiser, mit dem dieses Ereignis verknüpft ist. Es kann eine andere Advertiser-ID angegeben werden, um die in der Erweiterungskonfiguration angegebene ID zu überschreiben. |
| Händler-ID | Die eindeutige Kennung, die jedem Händler während des Onboarding-Verfahrens von [!DNL The Trade Desk] zugewiesen wird. Es kann eine andere Händler-ID angegeben werden, um die in der Erweiterungskonfiguration angegebene ID zu überschreiben. |

![Der [!DNL Configuration Overrides] Abschnitt mit den verfügbaren Feldern.](../../../images/extensions/server/tradedesk/configure-overrides.png)

Wenn Sie mit der Regel zufrieden sind, wählen Sie **[!UICONTROL In Bibliothek speichern]** aus. Veröffentlichen Sie abschließend eine neue Ereignisweiterleitung [build](../../../ui/publishing/builds.md), um die an der Bibliothek vorgenommenen Änderungen zu aktivieren.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie Server-seitige Ereignisdaten mithilfe der [!DNL The Trade Desk] Real-Time Conversions-API-Erweiterung an [!DNL The Trade Desk] senden. Von hier aus wird empfohlen, Ihre Integration zu erweitern, indem unterschiedliche Regeln erstellt werden, die spezifische Konversionsereignisse senden, wie für jede Kampagne zutreffend. Weitere Informationen zu den Ereignisweiterleitungsfunktionen in [!DNL Adobe Experience Platform] finden Sie unter [Übersicht über die Ereignisweiterleitung](../../../ui/event-forwarding/overview.md).

Weitere Anleitungen zur effektiven Implementierung [ Integration finden Sie in der [!DNL The Trade Desk] Dokumentation  [!DNL The Trade Desk] Best Practices für die Echtzeit](https://www.facebook.com/business/help/308855623839366?id=818859032317965)Konversions-API).

Weitere Informationen zum Debuggen Ihrer Implementierung mit dem Experience Platform-Debugger und dem Überwachungs-Tool für die Ereignisweiterleitung finden Sie unter [Adobe Experience Platform Debugger - Übersicht](../../../../debugger/home.md) und [Überwachen von Aktivitäten in der Ereignisweiterleitung](../../../ui/event-forwarding/monitoring.md).
