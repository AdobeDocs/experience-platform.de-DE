---
title: Google Display & Video 360-Verbindung
description: Display & Video 360 (zuvor DoubleClick Bid Manager) ist ein Tool zur Ausführung von Retargeting- und Audience-orientierten digitalen Kampagnen in den Inventarquellen Display, Video und Mobile.
exl-id: bdd3b3fd-891f-44ec-bd47-daf7f3289f92
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1134'
ht-degree: 49%

---

# [!DNL Google Display & Video 360]-Verbindung

>[!IMPORTANT]
>
> Google veröffentlicht Änderungen an der [Google Ads API](https://developers.google.com/google-ads/api/docs/start), [Customer Match](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) und der [Display &amp; Video 360 API](https://developers.google.com/display-video/api/guides/getting-started/overview), um die Compliance- und Zustimmungsanforderungen zu unterstützen, die im [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA) in der Europäischen Union definiert sind ([EU-Richtlinie zur ](https://www.google.com/about/company/user-consent-policy/)). Die Durchsetzung dieser Änderungen an den Einverständnisanforderungen ist ab dem 6. März 2024 aktiv.
> ><br/>
> >Um die EU-Richtlinie zur Benutzerzustimmung einzuhalten und weiterhin Zielgruppenlisten für Nutzer im Europäischen Wirtschaftsraum (EWR) zu erstellen, müssen Werbetreibende und Partner sicherstellen, dass sie beim Hochladen von Zielgruppendaten die Zustimmung der Endnutzer weitergeben. Als Google-Partner stellt Adobe Ihnen die erforderlichen Tools zur Verfügung, um diese Zustimmungsanforderungen gemäß dem DMA in der Europäischen Union zu erfüllen.
> ><br/>
> >Kunden, die Adobe Privacy &amp; Security Shield erworben und eine [Einverständnisrichtlinie“ ](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) haben, um nicht einverstandene Profile herauszufiltern, müssen keine Maßnahmen ergreifen.
> ><br/>
> >Kunden, die Adobe Privacy &amp; Security Shield nicht erworben haben, müssen die [Segmentdefinition](../../../segmentation/home.md#segment-definitions)-Funktionen in [Segment Builder](../../../segmentation/ui/segment-builder.md) verwenden, um nicht einverstandene Profile herauszufiltern, damit die bestehenden Real-Time CDP Google-Ziele ohne Unterbrechung weiter verwendet werden können.

[!DNL Display & Video 360], früher als [!DNL DoubleClick Bid Manager] bezeichnet, ist ein Tool, mit dem Sie Retargeting- und zielgruppenorientierte digitale Kampagnen über Display-, Video- und mobile Inventarquellen hinweg ausführen können.

## Zielspezifikationen {#specifics}

Beachten Sie folgende Details, die speziell für [!DNL Google Display & Video 360]-Ziele gelten:

* Aktivierte Zielgruppen werden in der Google-Plattform programmgesteuert erstellt.
* Die Aktivierung von Audience-Auffüllungen für das [!DNL Google Display & Video 360] Ziel ist 24-48 Stunden nach der erstmaligen Zuordnung einer Audience zu einer Zielverbindung geplant. Dieses Update ist eine Antwort auf die Google-Richtlinie, 24 Stunden bis zur Aufnahme von Daten zu warten, und soll die Übereinstimmungsraten zwischen Real-Time CDP und [!DNL Google Display & Video 360] verbessern. Dies ist eine Backend-Konfiguration, die nur für dieses Ziel gilt und nicht mit kundenkonfigurierbaren Planungsoptionen in der Benutzeroberfläche in Zusammenhang steht.

>[!IMPORTANT]
>
>Wenn Sie Ihr erstes Ziel mit Google Display &amp; Video 360 erstellen möchten und die [ID-Synchronisierungsfunktion](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html?lang=de) im Experience Cloud ID-Service in der Vergangenheit (mit Adobe Audience Manager oder anderen Anwendungen) nicht aktiviert haben, wenden Sie sich an Adobe Consulting oder die Kundenunterstützung, um ID-Synchronisierungen zu aktivieren. Wenn Sie zuvor bereits Google-Integrationen in Audience Manager eingerichtet hatten, werden die von Ihnen eingerichteten ID-Synchronisierungen auf Experience Platform übertragen.

## Unterstützte Identitäten {#supported-identities}

[!DNL Google Display & Video 360] unterstützt die Aktivierung von Zielgruppen basierend auf den in der folgenden Tabelle aufgeführten Identitäten. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Identität | Beschreibung | Zu beachten |
|---|---|---|
| GAID | [!DNL Google Advertising ID] |  |
| IDFA | [!DNL Apple ID for Advertisers] |  |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=de), auch bekannt als [!DNL Device ID]. Eine numerische, 38-stellige Geräte-ID, die Audience Manager jedem Gerät zuordnet, mit dem er interagiert. | Google verwendet [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=de), um Benutzende in Kalifornien als Ziel anzusprechen, und die Google-Cookie-ID für alle anderen Benutzenden. |
| [!DNL Google]-Cookie-ID | [!DNL Google]-Cookie-ID | [!DNL Google] verwendet diese ID, um Benutzende außerhalb von Kalifornien anzusprechen. |
| RIDA | Roku-ID für Werbung. Diese ID identifiziert Roku-Geräte eindeutig. |  |
| MAID | Microsoft Advertising-ID. Diese ID identifiziert Geräte, auf denen Windows 10 ausgeführt wird, eindeutig. |  |
| Amazon Fire TV ID | Diese ID identifiziert Amazon Fire TVs eindeutig. |  |

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Arten von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die über den Experience Platform-[ (Segmentierungs-Service) generiert ](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Sie exportieren alle Mitglieder einer Zielgruppe in das Google-Ziel. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

## Voraussetzungen {#prerequisites}

### Zulassungsauflistung {#allow-listing}

>[!NOTE]
>
>Die Zulassungsauflistung ist obligatorisch, bevor Sie Ihr erstes [!DNL Google Display & Video 360]-Ziel in Experience Platform einrichten. Stellen Sie sicher, dass der unten beschriebene Zulassungsauflistungsprozess von [!DNL Google] abgeschlossen wurde, bevor Sie ein Ziel erstellen.
>>Die Ausnahme für diese Regel betrifft [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html?lang=de)-Kunden. Wenn Sie bereits eine Verbindung zu diesem Google-Ziel in Audience Manager erstellt haben, ist es nicht erforderlich, den Zulassungsauflistungsprozess erneut zu durchlaufen. Sie können mit den nächsten Schritten fortfahren.

Bevor Sie das [!DNL Google Display & Video 360]-Ziel in Experience Platform erstellen, müssen Sie sich an Google wenden und darum bitten, dass Adobe in die Liste der zulässigen Datenanbieter aufgenommen wird und Ihr Konto der Zulassungsliste hinzugefügt wird. Kontaktieren Sie Google und machen Sie folgende Angaben:

* **Konto-ID**: Dies ist die Konto-ID von Adobe bei Google. Konto-ID: 87933855.
* **Kunden-ID**: Dies ist die Kundenkonto-ID von Adobe bei Google. Kunden-ID: 89690775.
* **Ihr Kontotyp**: Verwenden Sie **[!DNL Invite advertiser]**, um die Freigabe von Zielgruppen nur für eine bestimmte Marke in Ihrem Display &amp; Video 360-Konto zu ermöglichen, oder verwenden Sie **[!DNL Invite partner]**, um die Freigabe von Zielgruppen für alle Marken in Ihrem Display &amp; Video 360-Konto zu ermöglichen.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage Destinations]** Zugriffssteuerungsberechtigungen[. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Geben Sie einen bevorzugten Namen für das Ziel ein.
* **[!UICONTROL Description]**: Optional. Hier können Sie beispielsweise erwähnen, für welche Kampagne Sie dieses Ziel verwenden.
* **[!UICONTROL Account Type]**: Wählen Sie je nach Konto bei Google eine Option aus:
   * Verwenden Sie `Invite Advertiser`, um die Freigabe von Zielgruppen nur für eine bestimmte Marke in Ihrem Display &amp; Video 360-Konto zu ermöglichen.
   * Verwenden Sie `Invite Partner`, um die Freigabe von Zielgruppen für alle Marken in Ihrem Display &amp; Video 360-Konto zu ermöglichen.
* **[!UICONTROL Account ID]**: Geben Sie Ihre **[!DNL Invite partner]**- oder **[!DNL Invite advertiser]**-Konto-ID bei Google ein. In der Regel ist dies eine sechsstellige oder siebenstellige ID.

>[!NOTE]
>
>Wenden Sie sich beim Einrichten eines [!DNL Google Display & Video 360]-Ziels an Ihren [!DNL Google Account Manager] oder Adobe-Support-Mitarbeiter, um zu erfahren, welchen Kontotyp Sie haben.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Streaming-Zielgruppen-Exportziele](../../ui/activate-segment-streaming-destinations.md).

## Exportierte Daten

Um sich zu vergewissern, dass die Daten erfolgreich in das [!DNL Google Display & Video 360]-Ziel exportiert wurden, überprüfen Sie Ihr [!DNL Google Display & Video 360]-Konto. Wenn die Aktivierung erfolgreich war, werden in Ihrem Konto Zielgruppen ausgefüllt.

## Fehlerbehebung {#troubleshooting}

### Fehlermeldung „400 Fehlerhafte Anfrage“ {#bad-request}

Beim Konfigurieren dieses Ziels wird möglicherweise der folgende Fehler angezeigt:

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Dieser Fehler tritt auf, wenn Kundenkonten die [Voraussetzungen](#prerequisites) nicht erfüllen. Wenden Sie sich zur Behebung dieses Problems an Google und stellen Sie sicher, dass Ihr Konto auf der Zulassungsliste steht.