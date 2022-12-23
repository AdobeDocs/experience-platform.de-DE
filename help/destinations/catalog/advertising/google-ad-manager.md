---
keywords: google ad manager;google ad;doubleclick;DoubleClick AdX;DoubleClick;Google Ad Manager;Google ad manager;DFP
title: Google Ad Manager-Verbindung
description: Google Ad Manager, früher als DoubleClick für Herausgeber oder DoubleClick AdX bekannt, ist eine AdX-Plattform von Google, die Herausgebern die Möglichkeit gibt, die Anzeige von Werbung auf ihren Websites, über Videos und in Mobile Apps zu verwalten.
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: 94cd05ca8b5c8331b1b49e5172daf499918d2320
workflow-type: ht
source-wordcount: '955'
ht-degree: 100%

---

# [!DNL Google Ad Manager]-Verbindung

## Übersicht {#overview}

[!DNL Google Ad Manager], früher als [!DNL DoubleClick for Publishers] (DFP) oder [!DNL DoubleClick AdX] bekannt, ist eine Adserving-Plattform von [!DNL Google], die Herausgebern die Möglichkeit gibt, das Anzeigen von Werbung auf ihren Websites, über Videos und in Mobile Apps zu verwalten.

## Zielspezifikationen {#specifics}

Beachten Sie folgende Details, die speziell für [!DNL Google Ad Manager]-Ziele gelten:

* Aktivierte Zielgruppen werden in der [!DNL Google]-Plattform programmgesteuert erstellt.
* [!DNL Platform] umfasst derzeit keine Messmetrik zur Validierung erfolgreicher Aktivierungen. Konsultieren Sie die Audience-Zahlen in Google, um die Integration zu validieren und die Audience-Größe zu verstehen.
* Nachdem Sie ein Segment einem [!DNL Google Ad Manager]-Ziel zugeordnet haben, wird der Segmentname sofort in der [!DNL Google Ad Manager]-Benutzeroberfläche angezeigt.
* Es dauert 24-48 Stunden, bis die Segmentpopulation in [!DNL Google Ad Manager] angezeigt wird. Darüber hinaus müssen Segmente über eine Zielgruppengröße von mindestens 50 Profilen verfügen, damit sie in [!DNL Google Ad Manager] angezeigt werden. Segmente mit Zielgruppengrößen von weniger als 50 Profilen werden nicht in [!DNL Google Ad Manager] aufgeführt.

## Unterstützte Identitäten {#supported-identities}

[!DNL Google Ad Manager] unterstützt die Aktualisierung von Identitäten, die in der folgenden Tabelle beschrieben werden.

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| IDFA | [!DNL Apple ID for Advertisers] | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein IDFA-Namespace ist. |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=de), auch bekannt als [!DNL Device ID]. Eine numerische, 38-stellige Geräte-ID, die Audience Manager jedem Gerät zuordnet, mit dem er interagiert. | Google verwendet [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=de), um Benutzende in Kalifornien als Ziel anzusprechen, und die Google-Cookie-ID für alle anderen Benutzenden. |
| [!DNL Google]-Cookie-ID | [!DNL Google]-Cookie-ID | [!DNL Google] verwendet diese ID, um Benutzende außerhalb von Kalifornien anzusprechen. |
| RIDA | Roku-ID für Werbung. Diese ID identifiziert Roku-Geräte eindeutig. |  |
| MAID | Microsoft Advertising-ID. Diese ID identifiziert Geräte, auf denen Windows 10 ausgeführt wird, eindeutig. |  |
| Amazon Fire TV ID | Diese ID identifiziert Amazon Fire TVs eindeutig. |  |

{style=&quot;table-layout:auto&quot;}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Segmentexport]** | Sie exportieren alle Mitglieder eines Segments (Zielgruppe) in das Google-Ziel. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentbewertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Voraussetzungen {#prerequisites}

Wenn Sie Ihr erstes Ziel mit [!DNL Google Ad Manager] erstellen möchten und die [ID-Synchronisierungsfunktion](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html?lang=de) im ID-Service von Experience Cloud noch nicht aktiviert haben (mit Audience Manager oder anderen Anwendungen), wenden Sie sich an Adobe Consulting oder die Kundenunterstützung, um ID-Synchronisierungen zu aktivieren. Wenn Sie zuvor schon [!DNL Google]-Integrationen in Audience Manager eingerichtet hatten, werden die von Ihnen eingerichteten ID-Synchronisierungen auf Platform übertragen.

### Zulassungsauflistung {#allow-listing}

>[!NOTE]
>
>Die Zulassungsauflistung ist obligatorisch, bevor Sie Ihr erstes [!DNL Google Ad Manager]-Ziel in Platform einrichten. Vergewissern Sie sich, dass der unten beschriebene Zulassungsauflistungsprozess von [!DNL Google] abgeschlossen wurde, bevor Sie ein Ziel erstellen.
>Die Ausnahme für diese Regel betrifft [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html?lang=de)-Kunden. Wenn Sie bereits eine Verbindung zu diesem Google-Ziel in Audience Manager erstellt haben, ist es nicht erforderlich, den Zulassungsauflistungsprozess erneut zu durchlaufen. Sie können mit den nächsten Schritten fortfahren.

Vor der Erstellung des [!DNL Google Ad Manager]-Ziels in Platform müssen Sie [!DNL Google] kontaktieren, damit Adobe in die Liste der zugelassenen Datenanbieter aufgenommen wird und Ihr Konto der Zulassungsliste hinzugefügt werden kann. Kontaktieren Sie [!DNL Google] und machen Sie folgende Angaben:

* **Konto-ID**: Dies ist die Konto-ID von Adobe bei Google. Konto-ID: 87933855.
* **Kunden-ID**: Dies ist die Kundenkonto-ID von Adobe bei Google. Kunden-ID: 89690775.
* **Netzwerk-Code**: Dies ist Ihre Netzwerk-ID bei [!DNL Google Ad Manager], die unter **[!UICONTROL Admin > Globale Einstellungen]** in der Google-Benutzeroberfläche sowie in der URL zu finden ist.
* **Audience-Link-ID**: Dies ist eine spezifische Kennung, die mit Ihrem [!DNL Google Ad Manager]-Netzwerk (nicht Ihrem [!DNL Network code]) verbunden ist und die auch unter **[!UICONTROL Admin > Globale Einstellungen]** in der Google-Benutzeroberfläche zu finden ist.
* Ihr Kontotyp. DFP von Google oder AdX Buyer.

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
   * Verwenden von `DFP by Google` für [!DNL DoubleClick] for Publishers
   * Verwenden von `AdX buyer` für [!DNL Google AdX]
* **[!UICONTROL Konto-ID]**: Geben Sie Ihre Audience-Link-ID für [!DNL Google] ein.

>[!NOTE]
>
>Wenn Sie ein [!DNL Google Ad Manager]-Ziel einrichten, wenden Sie sich bitte an Ihren [!DNL Google Account Manager] oder den Adobe-Support-Mitarbeiter, um zu erfahren, welchen Kontotyp Sie haben.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Streaming-Segmentexportziele](../../ui/activate-segment-streaming-destinations.md).

## Exportierte Daten {#exported-data}

Um sich zu vergewissern, dass die Daten erfolgreich in das [!DNL Google Ad Manager]-Ziel exportiert wurden, überprüfen Sie Ihr [!DNL Google Ad Manager]-Konto. Wenn die Aktivierung erfolgreich war, werden in Ihrem Konto Zielgruppen ausgefüllt.
