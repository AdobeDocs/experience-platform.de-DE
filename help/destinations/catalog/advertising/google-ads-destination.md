---
keywords: Google-Anzeigen; Google-Anzeigen; Google-Adwords; Google AdWords; Google-Adwords
title: Google Ads-Verbindung
description: Google Ads, früher Google AdWords genannt, ist ein Online-Werbedienst, der Unternehmen Pay-per-Click-Werbung für textbasierte Suchvorgänge, grafische Displays, YouTube-Videos und In-App-Anzeigen zu nutzen.
exl-id: 7143f476-49a8-42aa-bfb4-b11fc2b8f5c3
source-git-commit: 16365865e349f8805b8346ec98cdab89cd027363
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 68%

---

# [!DNL Google Ads]-Verbindung

## Übersicht {#overview}

[!DNL Google Ads], früher bekannt als [!DNL Google AdWords], ist ein Online-Werbedienst, mit dem Unternehmen Pay-per-Click-Werbung für textbasierte Suchvorgänge und grafische Displays erstellen können. [!DNL YouTube] Videos und mobile In-App-Anzeigen.

## Zielspezifikationen {#specifics}

Beachten Sie folgende Details, die speziell für [!DNL Google Ads]-Ziele gelten:

* Aktivierte Zielgruppen werden in der [!DNL Google]-Plattform programmgesteuert erstellt.
* [!DNL Platform] umfasst derzeit keine Messmetrik zur Validierung erfolgreicher Aktivierungen. Konsultieren Sie die Audience-Zahlen in Google, um die Integration zu validieren und die Audience-Größe zu verstehen.

>[!IMPORTANT]
>
>Wenn Sie Ihr erstes Ziel mit [!DNL Google Ads] erstellen möchten und die [ID-Synchronisierungsfunktion](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html?lang=de) im ID-Service von Experience Cloud noch nicht aktiviert haben (mit Audience Manager oder anderen Anwendungen), wenden Sie sich an Adobe Consulting oder die Kundenunterstützung, um ID-Synchronisierungen zu aktivieren. Wenn Sie zuvor Google-Integrationen in Audience Manager eingerichtet haben, werden die von Ihnen eingerichteten ID-Synchronisierungen auf Platform übertragen.

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

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt werden alle Zielgruppen beschrieben, die Sie an dieses Ziel exportieren können.

Dieses Ziel unterstützt die Aktivierung aller durch die Experience Platform generierten Zielgruppen [Segmentierungsdienst](../../../segmentation/home.md).

*Zusätzlich*, unterstützt dieses Ziel auch die Aktivierung der in der folgenden Tabelle beschriebenen Zielgruppen.

| Zielgruppentyp | Beschreibung |
---------|----------|
| Benutzerdefinierte Uploads | Zielgruppen [importiert](../../../segmentation/ui/overview.md#import-audience) in die Experience Platform aus CSV-Dateien. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Zielgruppe in das Google-Ziel. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform basierend auf der Zielgruppenbewertung aktualisiert wird, sendet der Connector das Update an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Voraussetzungen {#prerequisites}

### Bestehend [!DNL Google Ads] account

>[!IMPORTANT]
>
> [!DNL Google] hat veraltete neue [!DNL Google Ads] Cookie-Integrationen mit Drittanbietern. Um die Zulassungslisten im nächsten Abschnitt durchführen zu können, müssen Sie über eine bestehende Integration mit [!DNL Google Ads]. Daher wird der empfohlene Ansatz für die Verwendung von [!DNL Google Ads] richtet eine [!DNL Google Customer Match] Integration. Weitere Informationen zum Erstellen eines [!DNL Google Customer Match] Integration lesen Sie bitte das Tutorial zum Erstellen einer [[!DNL Google Customer Match]](./google-customer-match.md) Verbindung herzustellen.

### Zulassungsauflistung {#allow-listing}

>[!NOTE]
>
>Die Zulassungsauflistung ist obligatorisch, bevor Sie Ihr erstes [!DNL Google Ads]-Ziel in Platform einrichten. Vergewissern Sie sich, dass der unten beschriebene Zulassungsauflistungsprozess von [!DNL Google] abgeschlossen wurde, bevor Sie ein Ziel erstellen.
>Die Ausnahme für diese Regel betrifft [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html?lang=de)-Kunden. Wenn Sie bereits eine Verbindung zu diesem Google-Ziel in Audience Manager erstellt haben, ist es nicht erforderlich, den Zulassungsauflistungsprozess erneut zu durchlaufen. Sie können mit den nächsten Schritten fortfahren.

Vor der Erstellung des [!DNL Google Ads]-Ziels in Platform müssen Sie [!DNL Google] kontaktieren, damit Adobe in die Liste der zugelassenen Datenanbieter aufgenommen wird und Ihr Konto der Zulassungsliste hinzugefügt werden kann. Kontaktieren Sie [!DNL Google] und machen Sie folgende Angaben:

* **Konto-ID**: Dies ist die Konto-ID von Adobe bei Google. Konto-ID: 87933855.
* **Kunden-ID**: Dies ist die Kundenkonto-ID von Adobe bei Google. Kunden-ID: 89690775.
* Ihr Kontotyp: **AdWords**
* **Google AdWords-ID**: Dies ist Ihre ID mit [!DNL Google]. Das Format der Kennung lautet in der Regel 123-456-7890.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Geben Sie den gewünschten Namen für das Ziel ein.
* **[!UICONTROL Beschreibung]**: Optional. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden.
* **[!UICONTROL Kontotyp]**: AdWords ist die einzige verfügbare Option.
* **[!UICONTROL Konto-ID]**: Geben Sie Ihre Konto-ID mit [!DNL Google Ads]. Das Format der Kennung lautet in der Regel 123-456-7890.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die [Zugriffskontrollberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Siehe [Aktivieren von Zielgruppendaten für Streaming-Zielgruppenexport-Ziele](../../ui/activate-segment-streaming-destinations.md) für Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel.

## Exportierte Daten

Um sich zu vergewissern, dass die Daten erfolgreich in das [!DNL Google Ads]-Ziel exportiert wurden, überprüfen Sie Ihr [!DNL Google Ads]-Konto. Wenn die Aktivierung erfolgreich war, werden in Ihrem Konto Zielgruppen ausgefüllt.

## Fehlerbehebung {#troubleshooting}

### 400 Fehlermeldung &quot;Bad Request&quot; {#bad-request}

Beim Konfigurieren dieses Ziels wird möglicherweise der folgende Fehler angezeigt:

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Dieser Fehler tritt auf, wenn Kundenkonten die [Voraussetzungen](#prerequisites) oder wenn Kunden versuchen, das Ziel ohne vorhandene [!DNL Google Ads] -Konto.

[!DNL Google] hat veraltete neue [!DNL Google Ads] Cookie-Integrationen mit Drittanbietern. Um die [allow-list](#allow-listing) Schritte, müssen Sie über eine vorhandene Integration mit [!DNL Google Ads].

Der empfohlene Ansatz für die Verwendung von [!DNL Google Ads] richtet eine [[!DNL Google Customer Match]](google-customer-match.md) Integration.
