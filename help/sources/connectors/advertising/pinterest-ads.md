---
keywords: Experience Platform; Startseite; beliebte Themen; Pinterest-Anzeigen;
title: Pinterest Ads Source Overview
description: Erfahren Sie, wie Sie Pinterest Ads über APIs oder die Benutzeroberfläche mit Adobe Experience Platform verbinden.
badge: Beta
hide: true
hidefromtoc: true
exl-id: 8edbcb26-0a18-47f1-8012-ca209d99d7a6
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 13%

---

# [!DNL Pinterest Ads]

>[!NOTE]
>
>Die [!DNL Pinterest Ads]-Quelle befindet sich in der Beta-Phase. Lesen Sie die [Quellen - Übersicht](../../home.md#terms-and-conditions) Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectoren.

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform ermöglicht die Aufnahme von Daten aus Werbesystemen von Drittanbietern. Die Unterstützung für Werbetreibende umfasst [!DNL Pinterest Ads].

[[!DNL Pinterest]](https://www.pinterest.com) ist eine visuelle Suchmaschine, mit der Sie Rezepte, Innendekorationen, Stilinspirierungen und andere Ideen im Internet finden können. Diese werden in kleinem Maßstab mit Bildern, animierten GIF und Videos in Pinnwänden präsentiert. [[!DNL Pinterest Ads]](https://ads.pinterest.com/) ermöglicht Ihnen, Ihr Geschäft auszubauen und 400 Millionen Menschen zu erreichen, indem Sie [!DNL Pinterest].

Mit [!DNL Pinterest Ads]können Sie Benutzer über gezielte Werbung erreichen, um Ihre Produkte zu entdecken und zu kaufen. Stifte aus [!DNL Pinterest Ads] werden gesponsert, um eine zusätzliche Belichtung in relevanten Suchergebnissen zu erhalten. Benutzer, die sich für [!DNL Pinterest Business] Sie können vorhandene Pins mit der besten Leistung bewerben, ein neues Bild oder Video erstellen oder sogar ein Bild bewerben, das von einer Website veröffentlicht wurde. [!DNL Pinterest Ads] bietet verschiedene Anzeigenformate, mit denen Sie Ihre spezifischen Kampagnenziele erreichen können.

## [!DNL Pinterest] APIs {#pinterest-apis}

Die [!DNL Pinterest Ads] -Quelle verwendet die [!DNL Pinterest] APIs zum Abrufen Ihrer [!DNL Pinterest Ads] Daten sowie allen Leistungs- und Metriken. Folgende API-Endpunkte werden unterstützt:

* [Campaign Analytics](https://developers.pinterest.com/docs/api/v5/#operation/campaigns/analytics)
* [Anzeigengruppenanalysen](https://developers.pinterest.com/docs/api/v5/#operation/ad_groups/analytics)
* [Anzeigenanalyse](https://developers.pinterest.com/docs/api/v5/#operation/ads/analytics)

Verwenden Sie die [!DNL Pinterest Ads] Quelle, aus der Ihre Daten übertragen werden [!DNL Pinterest] zur Experience Platform, wo Sie dann Datenanalysen ausführen können. Daten werden ab dem Datum der Aufnahme für einen rückdatierten Zeitraum von 90 Tagen zurückgegeben. [!DNL Pinterest Ads] verwendet Trägertoken als Authentifizierungsmechanismus für die Kommunikation mit dem [!DNL Pinterest] APIs.

## Voraussetzungen {#prerequisites}

Der erste Schritt beim Erstellen eines [!DNL Pinterest Ads] -Quellverbindung besteht darin sicherzustellen, dass Sie über ein Pinterest-Entwicklerkonto verfügen. Wenn Sie noch keine haben, rufen Sie die Seite [anmelden](https://www.pinterest.com/business/create/?next=https://developers.pinterest.com/account-setup/) Seite, um sich zu registrieren und Ihr Konto zu erstellen.

### Einrichtung [!DNL Pinterest] App und Zugriffstoken generieren {#create-app-and-generate-token}

>[!IMPORTANT]
>
>Es wird empfohlen, die [!DNL Pinterest] APIs zum Generieren Ihres Zugriffstokens, da das Generieren Ihres Zugriffstokens in der Benutzeroberfläche einen eingeschränkten Zugriff bietet. Über die Benutzeroberfläche können Sie nur auf die folgenden Bereiche zugreifen: `pins:read`, `boards:read` und `user_accounts:read`. Diese Einschränkung ist für die Verwendung mit den Analytics-Endpunkten der Variablen [!DNL Pinterest] API.

Lesen Sie zum Generieren Ihres Zugriffstokens den Abschnitt [!DNL Pinterest] Handbücher [App einrichten](https://developers.pinterest.com/docs/getting-started/set-up-app/) und [Authentifizierung mit OAuth 2.0](https://developers.pinterest.com/docs/getting-started/authentication/).

### Sammeln erforderlicher Anmeldeinformationen {#gather-required-credentials}

Um eine Verbindung zwischen [!DNL Pinterest Ads] und Platform herzustellen, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| --- | --- |
| Zugriffstoken | Die [!DNL Pinterest Ads] Zugriffstoken für Ihr Benutzerkonto. Das Benutzerkonto des Tokens muss entweder Eigentümer des angegebenen sein [!DNL Pinterest Ad] über Business Access einer der erforderlichen Rollen zugewiesen werden können: Admin, Analyst oder Campaign Manager. Weitere Informationen zum Zugriffstoken finden Sie im Abschnitt [[!DNL Pinterest] Handbuch zum Generieren Ihres Zugriffstokens](https://developers.pinterest.com/docs/getting-started/set-up-app/). |
| Anzeigen-Konto-ID | Die verwandten [!DNL Pinterest Ads] Anzeigen-Konto-ID für Ihren Geschäftsbereich. Informationen zum Abrufen Ihrer Anzeigenkonto-ID. Besuchen Sie die [[!DNL Pinterest] Handbuch zum Suchen von IDs in Ads Manager](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager). |
| Kampagnen-, Anzeigengruppen- oder Anzeigen-ID | Die `campaign`, `ad group`oder `ad` IDs, die Ihrer Anzeigenkonto-ID entsprechen. Um die erforderlichen IDs abzurufen, navigieren Sie zum [!DNL Pinterest] Seite für **Pinterest Business Hub** > **Anzeigenkontozusammenfassung** > **Kampagnen** / **Anzeigengruppen** / **Anzeigen** und kopieren Sie die erforderlichen IDs, die direkt unter jedem Namen erwähnt werden. |

>[!NOTE]
>
>Die [!DNL Pinterest] Die API stellt individuelle APIs zum Abrufen von mit jeder ID verknüpften Daten bereit. Dementsprechend müssen Sie nur die entsprechenden IDs für den gewünschten ID-Typ übergeben.

## Leitplanken {#guardrails}

Die folgenden Abschnitte enthalten Informationen zu Datensicherungen für [!DNL Pinterest].

### [!DNL Pinterest] Datumsbereich {#pinterest-date-range}

Die [!DNL Pinterest] API unterstützt beide `start_date` und `end_date` Parameter zum Abrufen von Analysedaten zwischen einem bestimmten Datumsbereich.

* Die `start_date` darf nicht länger als 90 Tage vor dem aktuellen Datum liegen.
* Die `end_date` darf nicht mehr als 90 Tage nach dem `start_date`.

Bei der Planung Ihres Datenflusses müssen Sie eine der folgenden Häufigkeits- und Intervalleinstellungen konfigurieren:

| Häufigkeit | Intervall |
| --- | --- |
| `Day` | 1 |
| `Hour` | 24 |

Wenn beispielsweise die Aufnahme am 15. März 2023 mit einer Häufigkeit und einem Intervall festgelegt ist, die auf `Day=1` oder `Hour=24`, dann [!DNL Pinterest] Die API würde nur Daten ab dem 15. Dezember 2022 abrufen, da die Berechnung für 90 Tage zurückdatiert ist.

### [!DNL Pinterest] Zeitraum {#pinterest-time-range}

Die [!DNL Pinterest] Die API unterstützt verschiedene Arten von Zeitgranularität für das Abrufen von Daten:

| Zeitgranularität | Beschreibung |
| --- | --- |
| **INSGESAMT** | Die Datenmetriken werden über einen bestimmten Datumsbereich aggregiert. |
| **TAG** | Die Datenmetriken werden täglich aufgeschlüsselt. |
| **STUNDE** | Die Datenmetriken werden stündlich aufgeschlüsselt. |
| **WÖCHENTLICH** | Die Datenmetriken werden wöchentlich aufgeschlüsselt. |
| **MONATLICH** | Die Datenmetriken werden monatlich aufgeschlüsselt. |

Für Platform wird die [!DNL Pinterest Ads] -Quelle intern konfiguriert ist, um `Day`, d. h. die Daten werden täglich aggregiert. Verwenden Sie beispielsweise `impressions recorded` als Metrik, da die Granularität als `DAY`, erhalten Sie `xx` Impressionen auf `day 1`, `yy` Impressionen auf `day 2` und so weiter.

>[!IMPORTANT]
>
>Pinterest begrenzt die API täglich auf 1000 API-Aufrufe, um Informationen aus Anzeigen, Anzeigengruppen oder Anzeigenkampagnen zu lesen. Informationen zu den Ratenbeschränkungen für zugrunde liegende API-Aufrufe finden Sie im Abschnitt [[!DNL Pinterest] Dokumentation zu Quotenbeschränkungen](https://developers.pinterest.com/docs/reference/ratelimits/).

## Verbinden von [!DNL Pinterest Ads] mit Platform {#connect-to-platform}

Die folgende Dokumentation enthält Informationen zur Verbindung von [!DNL Pinterest Ads] mit Platform mithilfe von APIs oder der Benutzeroberfläche:

### Verbinden von [!DNL Pinterest Ads] mit Platform mithilfe von APIs {#connect-to-platform-using-api}

* [Erstellen einer Pinterest-Basisverbindung mit der Flow Service-API](../../tutorials/api/create/advertising/pinterest-ads.md)
* [Erkunden von Datentabellen mithilfe der Flow Service-API](../../tutorials/api/explore/tabular.md)
* [Erstellen eines Datenflusses für eine Werbequelle mithilfe der Flow Service-API](../../tutorials/api/collect/advertising.md)

### Verbinden von [!DNL Pinterest Ads] mit Platform über die Benutzeroberfläche {#connect-to-platform-using-ui}

* [Erstellen einer Pinterest-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/advertising/pinterest-ads.md)
* [Erstellen eines Datenflusses für eine Verbindung mit einer Werbequelle in der Benutzeroberfläche](../../tutorials/ui/dataflow/advertising.md)
