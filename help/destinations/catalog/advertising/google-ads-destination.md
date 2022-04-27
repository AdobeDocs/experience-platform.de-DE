---
keywords: Google-Anzeigen; Google-Anzeigen; Google-Adwords; Google AdWords; Google-Adwords
title: Google Ads-Verbindung
description: Google Ads, früher Google AdWords genannt, ist ein Online-Werbedienst, der Unternehmen Pay-per-Click-Werbung für textbasierte Suchvorgänge, grafische Displays, YouTube-Videos und In-App-Anzeigen zu nutzen.
exl-id: 7143f476-49a8-42aa-bfb4-b11fc2b8f5c3
source-git-commit: 0006c498cd33d9deb66f1d052b4771ec7504457d
workflow-type: tm+mt
source-wordcount: '835'
ht-degree: 19%

---

# [!DNL Google Ads]-Verbindung

## Übersicht {#overview}

[!DNL Google Ads], früher bekannt als [!DNL Google AdWords], ist ein Online-Werbedienst, mit dem Unternehmen Pay-per-Click-Werbung für textbasierte Suchvorgänge und grafische Displays erstellen können. [!DNL YouTube] Videos und mobile In-App-Anzeigen.

## Zielspezifikationen {#specifics}

Beachten Sie die folgenden Details, die spezifisch für [!DNL Google Ads] Ziele:

* Aktivierte Zielgruppen werden programmgesteuert im [!DNL Google] Plattform.
* [!DNL Platform] enthält derzeit keine Messmetrik zur Validierung einer erfolgreichen Aktivierung. Konsultieren Sie die Zielgruppenzahlen in Google, um die Integration zu validieren und die Zielgruppengröße zu verstehen.

>[!IMPORTANT]
>
>Wenn Sie Ihr erstes Ziel mit [!DNL Google Ads] und nicht aktiviert haben, [ID-Synchronisierungsfunktion](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) Wenden Sie sich in der Vergangenheit (mit Audience Manager oder anderen Experience Cloud-ID-Diensten) an Adobe Consulting oder die Kundenunterstützung, um ID-Synchronisierungen zu aktivieren. Wenn Sie zuvor Google-Integrationen in Audience Manager eingerichtet haben, werden die von Ihnen eingerichteten ID-Synchronisierungen auf Platform übertragen.

## Unterstützte Identitäten {#supported-identities}

[!DNL Google Ad Manager] unterstützt die Aktivierung der in der folgenden Tabelle beschriebenen Identitäten.

| Zielgruppenidentität | Beschreibung | Zu beachten |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| IDFA | [!DNL Apple ID for Advertisers] | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein IDFA-Namespace ist. |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), auch bekannt als [!DNL Device ID]. Eine numerische, 38-stellige Geräte-ID, die der Audience Manager jedem Gerät zuordnet, mit dem er interagiert. | Google verwendet [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) , um Benutzer in Kalifornien als Ziel auszuwählen, und die Google-Cookie-ID für alle anderen Benutzer. |
| [!DNL Google] Cookie-ID | [!DNL Google] Cookie-ID | [!DNL Google] verwendet diese ID, um Benutzer außerhalb von Kalifornien anzusprechen. |
| RIDA | Roku-ID für Werbung. Diese ID identifiziert Roku-Geräte eindeutig. |  |
| MAID | Microsoft Advertising-ID. Diese ID identifiziert Geräte mit Windows 10 eindeutig. |  |
| Amazon Fire TV ID | Diese ID identifiziert Amazon Fire TVs eindeutig. |  |

{style=&quot;table-layout:auto&quot;}

## Exportart und -frequenz {#export-type-frequency}

Informationen zum Zielexporttyp und zur Häufigkeit finden Sie in der unten stehenden Tabelle.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Segmentexport]** | Sie exportieren alle Mitglieder eines Segments (Zielgruppe) in das Google-Ziel. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind &quot;immer auf&quot;-API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentbewertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Mehr dazu [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Voraussetzungen {#prerequisites}

### Bestehend [!DNL Google Ads] account

>[!IMPORTANT]
>
> [!DNL Google] hat veraltete neue [!DNL Google Ads] Cookie-Integrationen mit Drittanbietern. Um die Zulassungslisten im nächsten Abschnitt durchführen zu können, müssen Sie über eine bestehende Integration mit [!DNL Google Ads]. Daher wird der empfohlene Ansatz für die Verwendung von [!DNL Google Ads] richtet eine [!DNL Google Customer Match] Integration. Weitere Informationen zum Erstellen eines [!DNL Google Customer Match] Integration lesen Sie bitte das Tutorial zum Erstellen einer [[!DNL Google Customer Match]](./google-customer-match.md) Verbindung.

### Zulassungsauflistung {#allow-listing}

>[!NOTE]
>
>Die Zulassungsliste ist vor der Einrichtung der ersten [!DNL Google Ads] Ziel in Platform. Vergewissern Sie sich, dass die unten beschriebene Zulassungsliste durch [!DNL Google] vor dem Erstellen eines Ziels.

Vor der Erstellung [!DNL Google Ads] Ziel in Platform müssen Sie [!DNL Google] , damit die Adobe in die Liste der zugelassenen Datenanbieter aufgenommen und Ihr Konto zur Zulassungsliste hinzugefügt werden kann. Kontakt [!DNL Google] und geben Sie die folgenden Informationen an:

* **Konto-ID**: Kontokennung der Adobe mit Google. Konto-ID: 87933855.
* **Kunden-ID**: Kundenkonto-ID von Adobe mit Google. Kunden-ID: 89690775.
* Ihr Kontotyp: **AdWords**
* **Google AdWords-ID**: Dies ist Ihre ID mit [!DNL Google]. Das Format der Kennung lautet in der Regel 123-456-7890.

## Herstellen einer Verbindung mit der Datenbank {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele verwalten]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Geben Sie den gewünschten Namen für das Ziel ein.
* **[!UICONTROL Beschreibung]**: Optional. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden.
* **[!UICONTROL Kontotyp]**: AdWords ist die einzige verfügbare Option.
* **[!UICONTROL Konto-ID]**: Geben Sie Ihre Konto-ID mit [!DNL Google Ads]. Das Format der Kennung lautet in der Regel 123-456-7890.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Siehe [Aktivieren von Zielgruppendaten für Streaming-Segmentexportziele](../../ui/activate-segment-streaming-destinations.md) für Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel.

## Exportierte Daten

So überprüfen Sie, ob die Daten erfolgreich in die [!DNL Google Ads] Ziel, überprüfen Sie Ihre [!DNL Google Ads] -Konto. Bei erfolgreicher Aktivierung werden Zielgruppen in Ihr Konto eingetragen.

## Fehlerbehebung {#troubleshooting}

### 400 Fehlermeldung &quot;Bad Request&quot; {#bad-request}

Beim Konfigurieren dieses Ziels wird möglicherweise der folgende Fehler angezeigt:

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Dieser Fehler tritt auf, wenn Kundenkonten die [Voraussetzungen](#prerequisites) oder wenn Kunden versuchen, das Ziel ohne vorhandene [!DNL Google Ads] -Konto.

[!DNL Google] hat veraltete neue [!DNL Google Ads] Cookie-Integrationen mit Drittanbietern. So führen Sie die [allow-list](#allow-listing) Schritte, müssen Sie über eine vorhandene Integration mit [!DNL Google Ads].

Der empfohlene Ansatz für die Verwendung von [!DNL Google Ads] richtet eine [[!DNL Google Customer Match]](google-customer-match.md) Integration.
