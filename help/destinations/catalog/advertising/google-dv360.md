---
keywords: DoubleClick Bid Manager;DoubleClick Bid Manager;DoubleClick;Display & Video 360;display 360;video 360;Video 360;Display 360;display and video
title: Google Display & Video 360-Verbindung
description: Display & Video 360, früher als DoubleClick Bid Manager bekannt, ist ein Tool zum Ausführen von digitalen Kampagnen für Retargeting und Zielgruppen-Targeting für Inventarquellen für Display, Video und Mobile.
exl-id: bdd3b3fd-891f-44ec-bd47-daf7f3289f92
source-git-commit: 326127996a27df41383ef67da765f7b0818f17f2
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 83%

---

# [!DNL Google Display & Video 360]-Verbindung

## Übersicht {#overview}

[!DNL Display & Video 360], früher als bekannt, ist ein Tool zum Ausführen von digitalen Kampagnen für Retargeting und Zielgruppen-Targeting für Inventarquellen für Display, Video und Mobile.[!DNL DoubleClick Bid Manager]

## Zielspezifikationen {#specifics}

Beachten Sie folgende Details, die speziell für [!DNL Google Display & Video 360]-Ziele gelten:

* Aktivierte Zielgruppen werden in der Google-Plattform programmgesteuert erstellt.
* Die Aktivierung von Zielgruppen-Backfilets für die [!DNL Google Display & Video 360] Das Ziel soll 24-48 Stunden nach der ersten Zuordnung eines Segments zu einer Zielverbindung auftreten. Diese Aktualisierung ist eine Reaktion auf die Google-Richtlinie, 24 Stunden auf die Aufnahme von Daten zu warten, und soll die Übereinstimmungsraten zwischen der Echtzeit-Kundendatenplattform und [!DNL Google Display & Video 360]. Beachten Sie, dass es sich hierbei um eine Backend-Konfiguration handelt, die nur für dieses Ziel gilt und nicht mit kundenkonfigurierbaren Planungsoptionen in der Benutzeroberfläche in Zusammenhang steht.

>[!IMPORTANT]
>
>Wenn Sie Ihr erstes Ziel mit Google Display &amp; Video 360 erstellen möchten und die [ID-Synchronisierungsfunktion](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html?lang=de) in Experience Cloud ID Service in der Vergangenheit nicht aktiviert hatten (mit Adobe Audience Manager oder anderen Anwendungen), wenden Sie sich an Adobe Consulting oder die Kundenunterstützung, um die ID-Synchronisierung zu aktivieren. Wenn Sie zuvor Google-Integrationen in Audience Manager eingerichtet haben, werden die von Ihnen eingerichteten ID-Synchronisierungen auf Platform übertragen.

## Unterstützte Identitäten {#supported-identities}

[!DNL Google Display & Video 360] unterstützt die Aktualisierung von Identitäten, die in der folgenden Tabelle beschrieben werden.

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| IDFA | [!DNL Apple ID for Advertisers] | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein IDFA-Namespace ist. |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=de), auch bekannt als [!DNL Device ID]. Eine numerische, 38-stellige Geräte-ID, die Audience Manager jedem Gerät zuordnet, mit dem er interagiert. | Google verwendet [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=de), um Benutzende in Kalifornien als Ziel anzusprechen, und die Google-Cookie-ID für alle anderen Benutzenden. |
| [!DNL Google]-Cookie-ID | [!DNL Google]-Cookie-ID | [!DNL Google] verwendet diese ID, um Benutzende außerhalb von Kalifornien anzusprechen. |
| RIDA | Roku-ID für Werbung. Diese ID identifiziert Roku-Geräte eindeutig. |  |
| MAID | Microsoft Advertising-ID. Diese ID identifiziert Geräte, auf denen Windows 10 ausgeführt wird, eindeutig. |  |
| Amazon Fire TV ID | Diese ID identifiziert Amazon Fire TVs eindeutig. |  |

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Segmentexport]** | Sie exportieren alle Mitglieder eines Segments (Zielgruppe) in das Google-Ziel. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentbewertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

## Voraussetzungen {#prerequisites}

### Zulassungsauflistung {#allow-listing}

>[!NOTE]
>
>Die Zulassungsauflistung ist obligatorisch, bevor Sie Ihr erstes [!DNL Google Display & Video 360]-Ziel in Platform einrichten. Vergewissern Sie sich, dass der unten beschriebene Zulassungsauflistungsprozess von [!DNL Google] abgeschlossen wurde, bevor Sie ein Ziel erstellen.
>Die Ausnahme für diese Regel betrifft [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html?lang=de)-Kunden. Wenn Sie bereits eine Verbindung zu diesem Google-Ziel in Audience Manager erstellt haben, ist es nicht erforderlich, den Zulassungsauflistungsprozess erneut zu durchlaufen. Sie können mit den nächsten Schritten fortfahren.

Vor der Erstellung [!DNL Google Display & Video 360] Ziel in Platform angeben, müssen Sie sich an Google wenden und darum bitten, die Adobe auf die Liste der zugelassenen Datenanbieter zu setzen und Ihr Konto der Zulassungsliste hinzuzufügen. Kontaktieren Sie Google und machen Sie folgende Angaben:

* **Konto-ID**: Dies ist die Konto-ID von Adobe bei Google. Konto-ID: 87933855.
* **Kunden-ID**: Dies ist die Kundenkonto-ID von Adobe bei Google. Kunden-ID: 89690775.
* **Ihr Kontotyp**: Verwenden Sie **[!DNL Invite advertiser]**, um die Freigabe von Zielgruppen nur für eine bestimmte Marke in Ihrem Display &amp; Video 360-Konto zu ermöglichen, oder verwenden Sie **[!DNL Invite partner]**, um die Freigabe von Zielgruppen für alle Marken in Ihrem Display &amp; Video 360-Konto zu ermöglichen.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Geben Sie den gewünschten Namen für das Ziel ein.
* **[!UICONTROL Beschreibung]**: Optional. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden.
* **[!UICONTROL Kontotyp]**: Wählen Sie je nach Konto bei Google eine Option aus:
   * Verwenden Sie `Invite Advertiser`, um die Freigabe von Zielgruppen nur für eine bestimmte Marke in Ihrem Display &amp; Video 360-Konto zu ermöglichen.
   * Verwenden Sie `Invite Partner`, um die Freigabe von Zielgruppen für alle Marken in Ihrem Display &amp; Video 360-Konto zu ermöglichen.
* **[!UICONTROL Kontokennung]**: Geben Sie Ihre **[!DNL Invite partner]**- oder **[!DNL Invite advertiser]**-Kontokennung bei Google ein. In der Regel ist dies eine sechsstellige oder siebenstellige ID.

>[!NOTE]
>
>Wenn Sie ein [!DNL Google Display & Video 360]-Ziel einrichten, wenden Sie sich bitte an Ihren [!DNL Google Account Manager] oder den Adobe-Support-Mitarbeiter, um zu erfahren, welchen Kontotyp Sie haben.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Streaming-Segmentexportziele](../../ui/activate-segment-streaming-destinations.md).

## Exportierte Daten

Um sich zu vergewissern, dass die Daten erfolgreich in das [!DNL Google Display & Video 360]-Ziel exportiert wurden, überprüfen Sie Ihr [!DNL Google Display & Video 360]-Konto. Wenn die Aktivierung erfolgreich war, werden in Ihrem Konto Zielgruppen ausgefüllt.

## Fehlerbehebung {#troubleshooting}

### 400 Fehlermeldung &quot;Bad Request&quot; {#bad-request}

Beim Konfigurieren dieses Ziels wird möglicherweise der folgende Fehler angezeigt:

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Dieser Fehler tritt auf, wenn Kundenkonten die [Voraussetzungen](#prerequisites). Wenden Sie sich zur Behebung dieses Problems an Google und stellen Sie sicher, dass Ihr Konto auf die Zulassungsliste gesetzt ist.