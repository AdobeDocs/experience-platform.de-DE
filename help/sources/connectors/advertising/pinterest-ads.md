---
keywords: Experience Platform;Startseite;beliebte Themen;Pinterest Ads;
title: Übersicht über pinterest Ads Source
description: Erfahren Sie, wie Sie Pinterest Ads mithilfe von APIs oder der Benutzeroberfläche mit Adobe Experience Platform verbinden.
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
>Die [!DNL Pinterest Ads]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta[gekennzeichneten Connectoren finden ](../../home.md#terms-and-conditions) unter „Quellen - Übersicht“ .

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Experience Platform ermöglicht die Aufnahme von Daten aus Werbesystemen von Drittanbietern. Der Support für Werbeanbieter umfasst [!DNL Pinterest Ads].

[[!DNL Pinterest]](https://www.pinterest.com) ist eine visuelle Discovery-Engine zum Suchen von Rezepten, Wohnkultur, Stilinspiration und anderen Ideen im Internet. Diese werden in kleinem Maßstab anhand von Bildern, animierten GIF und Videos im Pinnwand-Format präsentiert. [[!DNL Pinterest Ads]](https://ads.pinterest.com/) können Sie Ihr Unternehmen ausbauen und mit [!DNL Pinterest] 400 Millionen Menschen erreichen.

Mit [!DNL Pinterest Ads] können Sie Benutzer über zielgerichtete Anzeigen erreichen, um Ihre Produkte zu entdecken und zu kaufen. Pins von [!DNL Pinterest Ads] werden gesponsert, um zusätzliche Belichtung in relevanten Suchergebnissen zu erhalten. Benutzer, die [!DNL Pinterest Business] abonniert haben, können bestehende Pins mit der besten Leistung weiterleiten, ein neues Bild oder Video erstellen oder sogar ein Bild weiterleiten, das von einer Website angeheftet wurde. [!DNL Pinterest Ads] bietet verschiedene Werbeformate, mit denen Sie Ihre spezifischen Kampagnenziele erreichen können.

## [!DNL Pinterest] APIs {#pinterest-apis}

Die [!DNL Pinterest Ads]-Quelle nutzt die [!DNL Pinterest]-APIs zum Abrufen Ihrer [!DNL Pinterest Ads]-Daten sowie aller Leistungs- und Metriken. Folgende API-Endpunkte werden unterstützt:

* [Campaign-Analyse](https://developers.pinterest.com/docs/api/v5/#operation/campaigns/analytics)
* [Anzeigengruppenanalyse](https://developers.pinterest.com/docs/api/v5/#operation/ad_groups/analytics)
* [Ads Analytics](https://developers.pinterest.com/docs/api/v5/#operation/ads/analytics)

Verwenden Sie die [!DNL Pinterest Ads], um Ihre Daten von [!DNL Pinterest] auf Experience Platform zu übertragen, wo Sie dann Datenanalysen durchführen können. Die Daten werden ab dem Aufnahmedatum für einen Zeitraum von 90 Tagen zurückgegeben. [!DNL Pinterest Ads] verwendet Träger-Token als Authentifizierungsmechanismus für die Kommunikation mit den [!DNL Pinterest]-APIs.

## Voraussetzungen {#prerequisites}

Der erste Schritt beim Erstellen einer [!DNL Pinterest Ads]-Quellverbindung besteht darin, sicherzustellen, dass Sie über ein Pinterest-Entwicklerkonto verfügen. Wenn Sie noch kein Konto haben, besuchen Sie die Seite [Anmelden](https://www.pinterest.com/business/create/?next=https://developers.pinterest.com/account-setup/), um sich zu registrieren und Ihr Konto zu erstellen.

### Einrichten [!DNL Pinterest] App und Generieren des Zugriffstokens {#create-app-and-generate-token}

>[!IMPORTANT]
>
>Es wird empfohlen, die [!DNL Pinterest]-APIs zum Generieren Ihres Zugriffs-Tokens zu verwenden, da das Generieren Ihres Zugriffs-Tokens in der Benutzeroberfläche eingeschränkten Zugriff bietet. Über die Benutzeroberfläche können Sie nur auf die folgenden Bereiche zugreifen: `pins:read`, `boards:read` und `user_accounts:read`. Diese Einschränkung ist für die Verwendung mit den Analytics-Endpunkten der [!DNL Pinterest]-API nicht ausreichend.

Informationen zum Generieren Ihres Zugriffs-Tokens finden Sie in den [!DNL Pinterest] Handbüchern unter [Einrichten der App](https://developers.pinterest.com/docs/getting-started/set-up-app/) und [Authentifizieren mit OAuth 2.0](https://developers.pinterest.com/docs/getting-started/authentication/).

### Sammeln erforderlicher Anmeldedaten {#gather-required-credentials}

Um eine Verbindung zwischen [!DNL Pinterest Ads] und Platform herzustellen, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| --- | --- |
| Zugriffs-Token | Das [!DNL Pinterest Ads] Zugriffstoken für Ihr Benutzerkonto. Das Benutzerkonto des Tokens muss entweder Besitzer des angegebenen [!DNL Pinterest Ad]-Kontos sein oder über eine der erforderlichen Rollen verfügen, die ihm über den Geschäftszugriff gewährt werden: Admin, Analyst oder Campaign Manager. Weitere Informationen zum Zugriffs-Token finden Sie im [[!DNL Pinterest] Handbuch zum Generieren Ihres Zugriffs-Tokens](https://developers.pinterest.com/docs/getting-started/set-up-app/). |
| Werbekonto-ID | Die zugehörige [!DNL Pinterest Ads]-Konto-ID für Ihre Geschäftseinheit. Für Informationen zum Abrufen Ihrer Werbekonto-ID. Besuchen Sie das [[!DNL Pinterest] Handbuch zum Suchen von IDs in Ads Manager](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager). |
| Kampagne, Anzeigengruppe oder Anzeigenkennung | Die `campaign`-, `ad group`- oder `ad`-IDs, die Ihrer Werbekonto-ID entsprechen. Um die erforderlichen IDs zu erhalten, gehen Sie zur Seite [!DNL Pinterest] für **Pinterest Business Hub** > **Anzeigenkontenzusammenfassung** > **Kampagnen** / **Anzeigengruppen** / **Anzeigen** und kopieren Sie die erforderlichen IDs, die direkt unter jedem ihrer Namen erwähnt werden. |

>[!NOTE]
>
>Die [!DNL Pinterest]-API stellt einzelne APIs zum Abrufen von mit jeder ID verknüpften Daten bereit. Dementsprechend müssen Sie nur die entsprechenden IDs für den ID-Typ übergeben, an dem Sie interessiert sind.

## Leitplanken {#guardrails}

Die folgenden Abschnitte enthalten Informationen zu Datenleitplanken für [!DNL Pinterest].

### [!DNL Pinterest] Datumsbereich {#pinterest-date-range}

Die [!DNL Pinterest]-API unterstützt sowohl einen `start_date`- als auch einen `end_date`, um Analytics-Daten zwischen einem bestimmten Datumsbereich abzurufen.

* Das `start_date` darf nicht mehr als 90 Tage vor dem aktuellen Datum liegen.
* Die `end_date` darf 90 Tage nach dem `start_date` nicht überschreiten.

Beim Planen Ihres Datenflusses müssen Sie eine der folgenden Einstellungen für Häufigkeit und Intervall konfigurieren:

| Häufigkeit | Intervall |
| --- | --- |
| `Day` | 1 |
| `Hour` | 24 |

Wenn die Aufnahme beispielsweise am 15. März 2023 mit einer Häufigkeit und einem Intervall eingestellt ist, die auf `Day=1` oder `Hour=24` konfiguriert sind, ruft die [!DNL Pinterest]-API Daten nur ab dem 15. Dezember 2022 ab, da die Berechnung 90 Tage zurückdatiert ist.

### [!DNL Pinterest] {#pinterest-time-range}

Die [!DNL Pinterest]-API unterstützt verschiedene Arten der Zeitgranularität für das Abrufen von Daten:

| Zeitgranularität | Beschreibung |
| --- | --- |
| **INSGESAMT** | Die Datenmetriken werden über einen angegebenen Datumsbereich aggregiert. |
| **TAG** | Die Datenmetriken werden täglich aufgeschlüsselt. |
| **STUNDE** | Die Datenmetriken werden stündlich aufgeschlüsselt. |
| **WÖCHENTLICH** | Die Datenmetriken werden wöchentlich aufgeschlüsselt. |
| **MONATLICH** | Die Datenmetriken werden monatlich aufgeschlüsselt. |

Für Platform ist die [!DNL Pinterest Ads] intern so konfiguriert, dass `Day` Daten aggregiert werden, und zwar täglich. Wenn Sie beispielsweise `impressions recorded` als Metrik verwenden, erhalten Sie, da die Granularität als `DAY` konfiguriert ist, `xx` Impressionen zu `day 1`, `yy` Impressions zu `day 2` usw.

>[!IMPORTANT]
>
>Pinterest begrenzt die Anzahl der API-Aufrufe pro Tag auf 1.000, um Informationen aus Anzeigen, Anzeigengruppen oder Anzeigenkampagnen zu lesen. Informationen zu Ratenbeschränkungen für zugrunde liegende API-Aufrufe finden Sie in der [[!DNL Pinterest] Dokumentation zu ](https://developers.pinterest.com/docs/reference/ratelimits/).

## Verbinden von [!DNL Pinterest Ads] mit Platform {#connect-to-platform}

Die folgende Dokumentation enthält Informationen zur Verbindung von [!DNL Pinterest Ads] mit Platform mithilfe von APIs oder der Benutzeroberfläche:

### Verbinden von [!DNL Pinterest Ads] mit Platform mithilfe von APIs {#connect-to-platform-using-api}

* [Erstellen einer Pinterest-Basisverbindung mithilfe der Flow Service-API](../../tutorials/api/create/advertising/pinterest-ads.md)
* [Erkunden von Datentabellen mithilfe der Flow Service-API](../../tutorials/api/explore/tabular.md)
* [Erstellen eines Datenflusses für eine Werbequelle mithilfe der Flow Service-API](../../tutorials/api/collect/advertising.md)

### Verbinden von [!DNL Pinterest Ads] mit Platform über die Benutzeroberfläche {#connect-to-platform-using-ui}

* [Erstellen einer Pinterest-Quellverbindung über die Benutzeroberfläche](../../tutorials/ui/create/advertising/pinterest-ads.md)
* [Erstellen eines Datenflusses für eine Werbequellenverbindung in der Benutzeroberfläche](../../tutorials/ui/dataflow/advertising.md)
