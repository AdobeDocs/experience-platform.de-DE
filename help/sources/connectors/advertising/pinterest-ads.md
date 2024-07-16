---
keywords: Experience Platform;home;popular topics;Pinterest Ads;
title: Übersicht über pinterest Ads Source
description: Erfahren Sie, wie Sie Pinterest Ads über APIs oder die Benutzeroberfläche mit Adobe Experience Platform verbinden.
badge: Beta
hide: true
hidefromtoc: true
exl-id: 8edbcb26-0a18-47f1-8012-ca209d99d7a6
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 14%

---

# [!DNL Pinterest Ads]

>[!NOTE]
>
>Die [!DNL Pinterest Ads]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta-gekennzeichneten Connectoren finden Sie in der [Übersicht über Quellen](../../home.md#terms-and-conditions) .

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform ermöglicht die Aufnahme von Daten aus Werbesystemen von Drittanbietern. Die Unterstützung für Werbetreibende umfasst [!DNL Pinterest Ads].

[[!DNL Pinterest]](https://www.pinterest.com) ist eine visuelle Suchmaschine, mit der Sie Rezepte, Innendekorationen, Stilinspirierungen und andere Ideen im Internet finden können. Diese werden in kleinem Maßstab mit Bildern, animierten GIF und Videos in Pinnwänden präsentiert. [[!DNL Pinterest Ads]](https://ads.pinterest.com/) ermöglicht es Ihnen, Ihr Geschäft auszubauen und mit [!DNL Pinterest] 400 Millionen Menschen zu erreichen.

Mit [!DNL Pinterest Ads] können Sie Benutzer über gezielte Werbung erreichen, um Ihre Produkte zu entdecken und zu kaufen. Pins von [!DNL Pinterest Ads] werden gesponsert, um eine zusätzliche Belichtung in relevanten Suchergebnissen zu erhalten. Benutzer, die sich für [!DNL Pinterest Business] angemeldet haben, können vorhandene Pins mit der besten Leistung bewerben, ein neues Bild oder Video erstellen oder sogar ein Bild bewerben, das von einer Website veröffentlicht wurde. [!DNL Pinterest Ads] bietet verschiedene Anzeigenformate, die Ihnen bei der Erreichung Ihrer spezifischen Kampagnenziele helfen.

## [!DNL Pinterest] APIs {#pinterest-apis}

Die Quelle [!DNL Pinterest Ads] nutzt die [!DNL Pinterest] -APIs, um Ihre [!DNL Pinterest Ads] -Daten abzurufen, zusammen mit allen Leistungs- und Metriken. Folgende API-Endpunkte werden unterstützt:

* [Kampagnenanalyse](https://developers.pinterest.com/docs/api/v5/#operation/campaigns/analytics)
* [Anzeigengruppenanalysen](https://developers.pinterest.com/docs/api/v5/#operation/ad_groups/analytics)
* [Anzeigen-Analyse](https://developers.pinterest.com/docs/api/v5/#operation/ads/analytics)

Verwenden Sie die [!DNL Pinterest Ads]-Quelle, um Ihre Daten von [!DNL Pinterest] auf die Experience Platform zu übertragen, wo Sie dann Datenanalysen ausführen können. Daten werden ab dem Datum der Aufnahme für einen rückdatierten Zeitraum von 90 Tagen zurückgegeben. [!DNL Pinterest Ads] verwendet Trägertoken als Authentifizierungsmechanismus für die Kommunikation mit den [!DNL Pinterest] -APIs.

## Voraussetzungen {#prerequisites}

Der erste Schritt beim Erstellen einer Quellverbindung mit dem Wert [!DNL Pinterest Ads] besteht darin, sicherzustellen, dass Sie über ein Pinterest-Entwicklerkonto verfügen. Wenn Sie noch kein Konto haben, besuchen Sie die Seite [Registrieren](https://www.pinterest.com/business/create/?next=https://developers.pinterest.com/account-setup/) , um sich zu registrieren und Ihr Konto zu erstellen.

### App [!DNL Pinterest] einrichten und Zugriffstoken generieren {#create-app-and-generate-token}

>[!IMPORTANT]
>
>Es wird empfohlen, die [!DNL Pinterest] -APIs zu verwenden, um Ihr Zugriffstoken zu generieren, da die Generierung Ihres Zugriffstokens in der Benutzeroberfläche einen eingeschränkten Zugriff bietet. Über die Benutzeroberfläche können Sie nur auf die folgenden Bereiche zugreifen: `pins:read`, `boards:read` und `user_accounts:read`. Diese Einschränkung eignet sich nicht für die Verwendung mit den Analytics-Endpunkten der [!DNL Pinterest] -API.

Um Ihr Zugriffstoken zu generieren, lesen Sie die [!DNL Pinterest] Handbücher für [Einrichten der App](https://developers.pinterest.com/docs/getting-started/set-up-app/) und [Authentifizierung mit OAuth 2.0](https://developers.pinterest.com/docs/getting-started/authentication/).

### Sammeln erforderlicher Anmeldeinformationen {#gather-required-credentials}

Um eine Verbindung zwischen [!DNL Pinterest Ads] und Platform herzustellen, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| --- | --- |
| Zugriffs-Token | Das Zugriffstoken [!DNL Pinterest Ads] für Ihr Benutzerkonto. Das Benutzerkonto des Tokens muss entweder Inhaber des angegebenen [!DNL Pinterest Ad]-Kontos sein oder über Business Access einer der erforderlichen Rollen zugewiesen werden: Admin, Analyst oder Campaign Manager. Weiterführende Informationen zum Zugriffstoken finden Sie im [[!DNL Pinterest] Handbuch zum Generieren Ihres Zugriffstokens](https://developers.pinterest.com/docs/getting-started/set-up-app/). |
| Anzeigen-Konto-ID | Die zugehörige [!DNL Pinterest Ads] Anzeigen-Konto-ID für Ihren Geschäftsbereich. Informationen zum Abrufen Ihrer Anzeigenkonto-ID. Lesen Sie das [[!DNL Pinterest] -Handbuch zum Suchen von IDs im Anzeigen-Manager](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager). |
| Kampagnen-, Anzeigengruppen- oder Anzeigen-ID | Die IDs `campaign`, `ad group` oder `ad`, die Ihrer Anzeigenkonto-ID entsprechen. Um die erforderlichen IDs abzurufen, navigieren Sie zur Seite &quot;[!DNL Pinterest]&quot;für **Pinterest Business Hub** > **Ad Account Summary** > **Kampagnen** / **Anzeigengruppen** / **Anzeigen**&quot;und kopieren Sie die erforderlichen IDs direkt unter jeden ihrer Namen. |

>[!NOTE]
>
>Die [!DNL Pinterest] -API stellt einzelne APIs zum Abrufen der mit jeder ID verknüpften Daten bereit. Dementsprechend müssen Sie nur die entsprechenden IDs für den gewünschten ID-Typ übergeben.

## Leitplanken {#guardrails}

Die folgenden Abschnitte enthalten Informationen zu Datensicherungen für [!DNL Pinterest].

### [!DNL Pinterest] Datumsbereich {#pinterest-date-range}

Die [!DNL Pinterest] -API unterstützt sowohl einen `start_date` als auch einen `end_date` -Parameter zum Abrufen von Analysedaten zwischen einem bestimmten Datumsbereich.

* Der `start_date` darf nicht länger als 90 Tage vor dem aktuellen Datum sein.
* Die `end_date` darf nicht länger als 90 Tage nach der `start_date` sein.

Bei der Planung Ihres Datenflusses müssen Sie eine der folgenden Häufigkeits- und Intervalleinstellungen konfigurieren:

| Häufigkeit | Intervall |
| --- | --- |
| `Day` | 1 |
| `Hour` | 24 |

Wenn beispielsweise die Aufnahme am 15. März 2023 mit einer Häufigkeit und einem Intervall festgelegt ist, die auf `Day=1` oder `Hour=24` konfiguriert sind, ruft die API [!DNL Pinterest] nur Daten ab, die bis zum 15. Dezember 2022 zurückliegen, da die Berechnung für 90 Tage zurückdatiert ist.

### [!DNL Pinterest] Zeitraum {#pinterest-time-range}

Die [!DNL Pinterest] -API unterstützt verschiedene Arten von Zeitgranularität, um zu erfahren, wie Daten abgerufen werden können:

| Zeitgranularität | Beschreibung |
| --- | --- |
| **INSGESAMT** | Die Datenmetriken werden über einen bestimmten Datumsbereich aggregiert. |
| **TAG** | Die Datenmetriken werden täglich aufgeschlüsselt. |
| **STUNDE** | Die Datenmetriken werden stündlich aufgeschlüsselt. |
| **WEEKLY** | Die Datenmetriken werden wöchentlich aufgeschlüsselt. |
| **MONTHLY** | Die Datenmetriken werden monatlich aufgeschlüsselt. |

Für Platform ist die Quelle [!DNL Pinterest Ads] intern auf `Day` konfiguriert, was bedeutet, dass Daten täglich aggregiert werden. Wenn Sie beispielsweise `impressions recorded` als Metrik verwenden, erhalten Sie, da die Granularität als `DAY` konfiguriert ist, `xx` Impressionen auf `day 1`, `yy` Impressionen auf `day 2` usw.

>[!IMPORTANT]
>
>Pinterest begrenzt die API täglich auf 1000 API-Aufrufe, um Informationen aus Anzeigen, Anzeigengruppen oder Anzeigenkampagnen zu lesen. Informationen zu den Ratenbeschränkungen für zugrunde liegende API-Aufrufe finden Sie in der [[!DNL Pinterest] Dokumentation zu Ratenbeschränkungen](https://developers.pinterest.com/docs/reference/ratelimits/).

## Verbinden von [!DNL Pinterest Ads] mit Platform {#connect-to-platform}

Die folgende Dokumentation enthält Informationen zur Verbindung von [!DNL Pinterest Ads] mit Platform mithilfe von APIs oder der Benutzeroberfläche:

### Verbinden von [!DNL Pinterest Ads] mit Platform mithilfe von APIs {#connect-to-platform-using-api}

* [Erstellen einer Pinterest-Basisverbindung mit der Flow Service-API](../../tutorials/api/create/advertising/pinterest-ads.md)
* [Erkunden von Datentabellen mithilfe der Flow Service-API](../../tutorials/api/explore/tabular.md)
* [Erstellen eines Datenflusses für eine Werbequelle mithilfe der Flow Service-API](../../tutorials/api/collect/advertising.md)

### Verbinden von [!DNL Pinterest Ads] mit Platform über die Benutzeroberfläche {#connect-to-platform-using-ui}

* [Erstellen einer Pinterest-Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/advertising/pinterest-ads.md)
* [Erstellen eines Datenflusses für eine Verbindung mit einer Werbequelle in der Benutzeroberfläche](../../tutorials/ui/dataflow/advertising.md)
