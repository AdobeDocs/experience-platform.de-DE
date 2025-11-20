---
keywords: google ad manager;google ad;doubleclick;DoubleClick AdX;DoubleClick;Google Ad Manager;Google ad manager;DFP
title: Google Ad Manager-Verbindung
description: Google Ad Manager, früher als DoubleClick für Herausgeber oder DoubleClick AdX bekannt, ist eine AdX-Plattform von Google, die Herausgebern die Möglichkeit gibt, die Anzeige von Werbung auf ihren Websites, über Videos und in Mobile Apps zu verwalten.
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1077'
ht-degree: 56%

---

# [!DNL Google Ad Manager]-Verbindung

>[!IMPORTANT]
>
> Google veröffentlicht Änderungen an der [Google Ads API](https://developers.google.com/google-ads/api/docs/start), [Customer Match](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) und der [Display &amp; Video 360 API](https://developers.google.com/display-video/api/guides/getting-started/overview), um die Compliance- und Zustimmungsanforderungen zu unterstützen, die im [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA) in der Europäischen Union definiert sind ([EU-Richtlinie zur &#x200B;](https://www.google.com/about/company/user-consent-policy/)). Die Durchsetzung dieser Änderungen an den Einverständnisanforderungen ist ab dem 6. März 2024 aktiv.
><br/>
>Um die EU-Richtlinie zur Benutzerzustimmung einzuhalten und weiterhin Zielgruppenlisten für Nutzer im Europäischen Wirtschaftsraum (EWR) zu erstellen, müssen Werbetreibende und Partner sicherstellen, dass sie beim Hochladen von Zielgruppendaten die Zustimmung der Endnutzer weitergeben. Als Google-Partner stellt Adobe Ihnen die erforderlichen Tools zur Verfügung, um diese Zustimmungsanforderungen gemäß dem DMA in der Europäischen Union zu erfüllen.
><br/>
>Kunden, die Adobe Privacy &amp; Security Shield erworben und eine [Einverständnisrichtlinie“ &#x200B;](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) haben, um nicht einverstandene Profile herauszufiltern, müssen keine Maßnahmen ergreifen.
><br/>
>Kunden, die Adobe Privacy &amp; Security Shield nicht erworben haben, müssen die [Segmentdefinition](../../../segmentation/home.md#segment-definitions)-Funktionen in [Segment Builder](../../../segmentation/ui/segment-builder.md) verwenden, um nicht einverstandene Profile herauszufiltern, damit die bestehenden Real-Time CDP Google-Ziele ohne Unterbrechung weiter verwendet werden können.


[!DNL Google Ad Manager], früher als [!DNL DoubleClick for Publishers] (DFP) oder [!DNL DoubleClick AdX] bekannt, ist eine Adserving-Plattform von [!DNL Google], die Herausgebern die Möglichkeit gibt, das Anzeigen von Werbung auf ihren Websites, über Videos und in Mobile Apps zu verwalten.

## Zielspezifikationen {#specifics}

Beachten Sie folgende Details, die speziell für [!DNL Google Ad Manager]-Ziele gelten:

* Aktivierte Zielgruppen werden in der [!DNL Google]-Plattform programmgesteuert erstellt.
* [!DNL Experience Platform] umfasst derzeit keine Messmetrik zur Validierung erfolgreicher Aktivierungen. Konsultieren Sie die Zielgruppen-Zahlen in Google, um die Integration zu validieren und die Zielgruppen-Größe zu verstehen.
* Nachdem Sie eine Zielgruppe einem [!DNL Google Ad Manager] Ziel zugeordnet haben, wird der Zielgruppenname sofort in der [!DNL Google Ad Manager]-Benutzeroberfläche angezeigt.
* Es dauert 24-48 Stunden, bis die Segmentpopulation in [!DNL Google Ad Manager] angezeigt wird. Darüber hinaus müssen Zielgruppen über eine Zielgruppengröße von mindestens 50 Profilen verfügen, damit sie in [!DNL Google Ad Manager] angezeigt werden. Zielgruppen mit einer Größe von weniger als 50 Profilen werden nicht in [!DNL Google Ad Manager] ausgefüllt.

## Unterstützte Identitäten {#supported-identities}

[!DNL Google Ad Manager] unterstützt die Aktivierung von Zielgruppen basierend auf den in der folgenden Tabelle aufgeführten Identitäten. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Identität | Beschreibung | Zu beachten |
|---|---|---|
| GAID | [!DNL Google Advertising ID] |  |
| IDFA | [!DNL Apple ID for Advertisers] |  |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=de), auch bekannt als [!DNL Device ID]. Eine numerische, 38-stellige Geräte-ID, die Audience Manager jedem Gerät zuordnet, mit dem er interagiert. | Google verwendet [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=de), um Benutzende in Kalifornien als Ziel anzusprechen, und die Google-Cookie-ID für alle anderen Benutzenden. |
| [!DNL Google]-Cookie-ID | [!DNL Google]-Cookie-ID | [!DNL Google] verwendet diese ID, um Benutzende außerhalb von Kalifornien anzusprechen. |
| RIDA | Roku-ID für Werbung. Diese ID identifiziert Roku-Geräte eindeutig. |  |
| MAID | Microsoft Advertising-ID. Diese ID identifiziert Geräte, auf denen Windows 10 ausgeführt wird, eindeutig. |  |
| Amazon Fire TV ID | Diese ID identifiziert Amazon Fire TVs eindeutig. |  |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Arten von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die über den Experience Platform-[&#x200B; (Segmentierungs-Service) generiert &#x200B;](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Sie exportieren alle Mitglieder einer Zielgruppe in das Google-Ziel. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Voraussetzungen {#prerequisites}

Wenn Sie Ihr erstes Ziel mit [!DNL Google Ad Manager] erstellen möchten und die [ID-Synchronisierungsfunktion](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html?lang=de) im ID-Service von Experience Cloud noch nicht aktiviert haben (mit Audience Manager oder anderen Anwendungen), wenden Sie sich an Adobe Consulting oder die Kundenunterstützung, um ID-Synchronisierungen zu aktivieren. Wenn Sie zuvor [!DNL Google] Integrationen in Audience Manager eingerichtet hatten, werden die von Ihnen eingerichteten ID-Synchronisierungen auf Experience Platform übertragen.

### Zulassungsauflistung {#allow-listing}

Die Zulassungsauflistung ist obligatorisch, bevor Sie Ihr erstes [!DNL Google Ad Manager]-Ziel in Experience Platform einrichten. Stellen Sie sicher, dass Sie den unten beschriebenen Zulassungsauflistungsprozess abschließen, bevor Sie Ihr Ziel erstellen.

1. Führen Sie die in der Dokumentation zu Google Ad Manager [beschriebenen Schritte aus](https://support.google.com/admanager/answer/3289669?hl=de) um Adobe als verknüpfte Datenverwaltungsplattform (DMP) hinzuzufügen.
2. Wechseln Sie in der [!DNL Google Ad Manager] zu **[!UICONTROL Admin]** > **[!UICONTROL Global Settings]** > **[!UICONTROL Network Settings]** und aktivieren Sie den **[!UICONTROL API Access]**.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage Destinations]** Zugriffssteuerungsberechtigungen[. &#x200B;](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

### Verbindungsparameter {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam_appendSegmentID"
>title="Anhängen der Zielgruppen-ID an Zielgruppennamen"
>abstract="Wählen Sie diese Option aus, damit der Zielgruppenname in Google Ad Manager die Zielgruppen-ID aus Experience Platform wie folgt enthält: `Audience Name (Audience ID)`"

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Geben Sie einen bevorzugten Namen für das Ziel ein.
* **[!UICONTROL Description]**: Optional. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden.
* **[!UICONTROL Account ID]**: Geben Sie Ihre [!DNL Audience Link ID] aus Ihrem [!DNL Google] ein. Dies ist eine spezifische Kennung, die mit Ihrem [!DNL Google Ad Manager]-Netzwerk (nicht Ihrem [!DNL Network code]) verbunden ist. Sie finden diese unter **[!UICONTROL Admin > Global settings]** in der [!DNL Google Ad Manager].
* **[!UICONTROL Account Type]**: Wählen Sie je nach Konto bei Google eine Option aus:
   * Verwenden von `DFP by Google` für [!DNL DoubleClick] for Publishers
   * Verwenden von `AdX buyer` für [!DNL Google AdX]
* **[!UICONTROL Append audience ID to audience name]**: Wählen Sie diese Option aus, damit der Zielgruppenname in Google Ad Manager die Zielgruppen-ID aus Experience Platform wie folgt enthält: `Audience Name (Audience ID)`.

>[!NOTE]
>
>Wenn Sie ein [!DNL Google Ad Manager]-Ziel einrichten, wenden Sie sich bitte an Ihren [!DNL Google Account Manager] oder den Adobe-Support-Mitarbeiter, um zu erfahren, welchen Kontotyp Sie haben.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Streaming-Zielgruppen-Exportziele](../../ui/activate-segment-streaming-destinations.md).

## Exportierte Daten {#exported-data}

Um sich zu vergewissern, dass die Daten erfolgreich in das [!DNL Google Ad Manager]-Ziel exportiert wurden, überprüfen Sie Ihr [!DNL Google Ad Manager]-Konto. Wenn die Aktivierung erfolgreich war, werden in Ihrem Konto Zielgruppen ausgefüllt.

## Fehlerbehebung {#troubleshooting}

Falls bei der Verwendung dieses Ziels Fehler auftreten und Sie sich entweder an Adobe oder Google wenden müssen, halten Sie die folgenden IDs bereit.

Dies sind die Google-Konto-IDs von Adobe:

* **[!UICONTROL Account ID]**: 87933855
* **[!UICONTROL Customer ID]**: 89690775