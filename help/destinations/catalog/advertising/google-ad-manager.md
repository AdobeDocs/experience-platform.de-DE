---
keywords: google ad manager;google ad;doubleclick;DoubleClick AdX;DoubleClick;Google Ad Manager;Google ad manager;DFP
title: Google Ad Manager-Verbindung
description: Google Ad Manager, früher als DoubleClick für Herausgeber oder DoubleClick AdX bekannt, ist eine AdX-Plattform von Google, die Herausgebern die Möglichkeit gibt, die Anzeige von Werbung auf ihren Websites, über Videos und in Mobile Apps zu verwalten.
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 78%

---

# [!DNL Google Ad Manager]-Verbindung

## Übersicht {#overview}

[!DNL Google Ad Manager], früher als [!DNL DoubleClick for Publishers] (DFP) oder [!DNL DoubleClick AdX] bekannt, ist eine Adserving-Plattform von [!DNL Google], die Herausgebern die Möglichkeit gibt, das Anzeigen von Werbung auf ihren Websites, über Videos und in Mobile Apps zu verwalten.

## Zielspezifikationen {#specifics}

Beachten Sie folgende Details, die speziell für [!DNL Google Ad Manager]-Ziele gelten:

* Aktivierte Zielgruppen werden in der [!DNL Google]-Plattform programmgesteuert erstellt.
* [!DNL Platform] umfasst derzeit keine Messmetrik zur Validierung erfolgreicher Aktivierungen. Konsultieren Sie die Zielgruppen-Zahlen in Google, um die Integration zu validieren und die Zielgruppen-Größe zu verstehen.
* Nach dem Zuordnen einer Zielgruppe zu einem [!DNL Google Ad Manager] Ziel, wird der Zielgruppenname sofort im [!DNL Google Ad Manager] -Benutzeroberfläche.
* Es dauert 24-48 Stunden, bis die Segmentpopulation in [!DNL Google Ad Manager] angezeigt wird. Darüber hinaus müssen Zielgruppen eine Zielgruppengröße von mindestens 50 Profilen aufweisen, damit sie in [!DNL Google Ad Manager]. Zielgruppen mit einer Größe von weniger als 50 Profilen werden nicht in [!DNL Google Ad Manager].

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

In diesem Abschnitt wird beschrieben, welche Zielgruppentypen Sie an dieses Ziel exportieren können.

| Audience Origin | Unterstützt | Beschreibung |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Über die Experience Platform generierte Zielgruppen [Segmentierungsdienst](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/overview.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Zielgruppe in das Google-Ziel. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Voraussetzungen {#prerequisites}

Wenn Sie Ihr erstes Ziel mit [!DNL Google Ad Manager] erstellen möchten und die [ID-Synchronisierungsfunktion](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html?lang=de) im ID-Service von Experience Cloud noch nicht aktiviert haben (mit Audience Manager oder anderen Anwendungen), wenden Sie sich an Adobe Consulting oder die Kundenunterstützung, um ID-Synchronisierungen zu aktivieren. Wenn Sie zuvor schon [!DNL Google]-Integrationen in Audience Manager eingerichtet hatten, werden die von Ihnen eingerichteten ID-Synchronisierungen auf Platform übertragen.

### Zulassungsauflistung {#allow-listing}

Die Zulassungsauflistung ist obligatorisch, bevor Sie Ihr erstes [!DNL Google Ad Manager]-Ziel in Platform einrichten. Stellen Sie sicher, dass Sie den unten beschriebenen Zulassungsauflistungsprozess abgeschlossen haben, bevor Sie Ihr Ziel erstellen.

1. Führen Sie die im Abschnitt [Dokumentation zu Google Ad Manager](https://support.google.com/admanager/answer/3289669?hl=de) um Adobe als verknüpfte Data Management Platform (DMP) hinzuzufügen.
2. Im [!DNL Google Ad Manager] -Benutzeroberfläche, navigieren Sie zu **[!UICONTROL Admin]** > **[!UICONTROL Globale Einstellungen]** > **[!UICONTROL Netzwerkeinstellungen]** und aktivieren Sie die **[!UICONTROL API-Zugriff]** festlegen.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

### Verbindungsparameter {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam_appendSegmentID"
>title="Zielgruppen-ID an Zielgruppennamen anhängen"
>abstract="Wählen Sie diese Option aus, damit der Zielgruppenname in Google Ad Manager die Zielgruppen-ID aus Experience Platform wie folgt enthält: `Audience Name (Audience ID)`"

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Geben Sie den gewünschten Namen für das Ziel ein.
* **[!UICONTROL Beschreibung]**: Optional. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden.
* **[!UICONTROL Konto-ID]**: Geben Sie Ihre [!DNL Audience Link ID] aus dem [!DNL Google] -Konto. Dies ist eine spezifische Kennung, die mit Ihrem [!DNL Google Ad Manager] Netzwerk (nicht [!DNL Network code]). Sie finden dies unter **[!UICONTROL Admin > Globale Einstellungen]** im [!DNL Google Ad Manager] -Schnittstelle.
* **[!UICONTROL Kontotyp]**: Wählen Sie je nach Konto bei Google eine Option aus:
   * Verwenden von `DFP by Google` für [!DNL DoubleClick] for Publishers
   * Verwenden von `AdX buyer` für [!DNL Google AdX]
* **[!UICONTROL Zielgruppen-ID an Zielgruppennamen anhängen]**: Wählen Sie diese Option, damit der Zielgruppenname in Google Ad Manager die Zielgruppen-ID von Experience Platform wie folgt enthält: `Audience Name (Audience ID)`.

>[!NOTE]
>
>Wenn Sie ein [!DNL Google Ad Manager]-Ziel einrichten, wenden Sie sich bitte an Ihren [!DNL Google Account Manager] oder den Adobe-Support-Mitarbeiter, um zu erfahren, welchen Kontotyp Sie haben.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die [Zugriffskontrollberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Streaming-Zielgruppen-Exportziele](../../ui/activate-segment-streaming-destinations.md).

## Exportierte Daten {#exported-data}

Um sich zu vergewissern, dass die Daten erfolgreich in das [!DNL Google Ad Manager]-Ziel exportiert wurden, überprüfen Sie Ihr [!DNL Google Ad Manager]-Konto. Wenn die Aktivierung erfolgreich war, werden in Ihrem Konto Zielgruppen ausgefüllt.

## Fehlerbehebung {#troubleshooting}

Sollten bei der Verwendung dieses Ziels Fehler auftreten und Sie sich an Adobe oder Google wenden müssen, halten Sie die folgenden IDs bereit.

Dies sind Adobe-Google-Konto-IDs:

* **[!UICONTROL Konto-ID]**: 87933855
* **[!UICONTROL Kunden-ID]**: 89690775