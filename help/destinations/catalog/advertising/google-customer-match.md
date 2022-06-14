---
keywords: Google-Kundenabgleich;Google-Kundenabgleich;Google-Kundenabgleich
title: Google Customer Match-Verbindung
description: Mit Google-Kundenabgleich können Sie Ihre Online- und Offline-Daten verwenden, um Ihre Kunden über die eigenen und betriebenen Eigenschaften von Google wie Suche, Shopping, Gmail und YouTube zu erreichen und erneut mit ihnen zu interagieren.
exl-id: 8209b5eb-b05c-4ef7-9fdc-22a528d5f020
source-git-commit: 23828fcbb1257fa093c1e114ee4c2fcb2162d9d6
workflow-type: tm+mt
source-wordcount: '1715'
ht-degree: 4%

---

# [!DNL Google Customer Match]-Verbindung

## Übersicht {#overview}

[Google-Kundenabgleich](https://support.google.com/google-ads/answer/6379332?hl=en) ermöglicht Ihnen die Verwendung Ihrer Online- und Offline-Daten, um Ihre Kunden über die eigenen und betriebenen Eigenschaften von Google zu erreichen und erneut mit ihnen zu interagieren, z. B.: [!DNL Search], [!DNL Shopping], [!DNL Gmail]und [!DNL YouTube].

![Google Customer Match-Ziel in der Benutzeroberfläche von Adobe Experience Platform](../../assets/catalog/advertising/google-customer-match/catalog.png)

## Anwendungsfälle {#use-cases}

So können Sie besser verstehen, wie und wann die Variable [!DNL Google Customer Match] Ziel, hier finden Sie Beispielanwendungsfälle, die Adobe Experience Platform-Kunden mit dieser Funktion lösen können.

### Anwendungsfall 1

Eine Sportbekleidungsmarke möchte bestehende Kunden über erreichen [!DNL Google Search] und [!DNL Google Shopping] , um Angebote und Artikel basierend auf ihren bisherigen Käufen und dem Browser-Verlauf zu personalisieren. Die Bekleidungsmarke kann E-Mail-Adressen aus ihrem eigenen CRM-System in die Experience Platform aufnehmen und aus ihren eigenen Offline-Daten Segmente erstellen. Anschließend können sie diese Segmente an senden [!DNL Google Customer Match] verwendet werden [!DNL Search] und [!DNL Shopping], wodurch ihre Werbeausgaben optimiert werden.

### Anwendungsfall 2

Ein renommiertes Technologieunternehmen startete ein neues Telefon. Um dieses neue Telefonmodell zu bewerben, möchten sie Kunden, die Inhaber früherer Modelle ihrer Telefone sind, für die neuen Funktionen des Telefons sensibilisieren.

Um die Veröffentlichung zu bewerben, laden sie E-Mail-Adressen aus ihrer CRM-Datenbank in Experience Platform hoch und verwenden dabei die E-Mail-Adressen als Kennungen. Segmente werden basierend auf Kunden erstellt, die ältere Telefonmodelle besitzen. Anschließend werden Segmente an gesendet [!DNL Google Customer Match], damit das Unternehmen aktuelle Kunden, Kunden, die Inhaber älterer Telefonmodelle sind, und ähnliche Kunden in ansprechen kann [!DNL YouTube].

## Data Governance für [!DNL Google Customer Match] Ziele {#data-governance}

Für einige Ziele in der Experience Platform gelten bestimmte Regeln und Pflichten für Daten, die an die Zielplattform gesendet oder von dieser empfangen werden. Sie sind dafür verantwortlich, die Einschränkungen und Pflichten Ihrer Daten zu verstehen und zu verstehen, wie Sie diese Daten in Adobe Experience Platform und der Zielplattform verwenden. Adobe Experience Platform bietet Data Governance-Tools, mit denen Sie einige dieser Datennutzungsverpflichtungen verwalten können. [Weitere Infos](../../../data-governance/labels/overview.md) über Data Governance-Tools und -Richtlinien.

## Unterstützte Identitäten {#supported-identities}

[!DNL Google Customer Match] unterstützt die Aktivierung der in der folgenden Tabelle beschriebenen Identitäten. Weitere Informationen [identities](/help/identity-service/namespaces.md).

| Zielgruppenidentität | Beschreibung | Zu beachten |
|---|---|---|
| GAID | Google Advertising ID | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| IDFA | Apple ID für Advertiser | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein IDFA-Namespace ist. |
| phone_sha256_e.164 | Telefonnummern im E164-Format, gehasht mit dem SHA256-Algorithmus | Sowohl einfache als auch SHA256-Hash-Telefonnummern werden von Adobe Experience Platform unterstützt. Befolgen Sie die Anweisungen im Abschnitt [Anforderungen an die ID-Übereinstimmung](#id-matching-requirements-id-matching-requirements) und verwenden Sie die entsprechenden Namespaces für Klartext- bzw. Hash-Telefonnummern. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die **[!UICONTROL Umwandlung anwenden]** -Option, um [!DNL Platform] die Daten bei Aktivierung automatisch hash. |
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen werden von Adobe Experience Platform unterstützt. Befolgen Sie die Anweisungen im Abschnitt [Anforderungen an die ID-Übereinstimmung](#id-matching-requirements-id-matching-requirements) und verwenden Sie die entsprechenden Namespaces für Nur-Text- bzw. Hash-E-Mail-Adressen. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die **[!UICONTROL Umwandlung anwenden]** -Option, um [!DNL Platform] die Daten bei Aktivierung automatisch hash. |
| user_id | Benutzerdefinierte Benutzer-IDs | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein benutzerdefinierter Namespace ist. |

{style=&quot;table-layout:auto&quot;}

## Exportart und -frequenz {#export-type-frequency}

Informationen zum Zielexporttyp und zur Häufigkeit finden Sie in der unten stehenden Tabelle.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Segmentexport]** | Sie exportieren alle Mitglieder eines Segments (Zielgruppe) mit den IDs (Name, Telefonnummer und andere), die im [!DNL Google Customer Match] Ziel. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind &quot;immer auf&quot;-API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentbewertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Mehr dazu [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## [!DNL Google Customer Match] Kontovoraussetzungen {#google-account-prerequisites}

Vor der Einrichtung einer [!DNL Google Customer Match] Ziel in Experience Platform lesen und beachten Sie die Google-Richtlinie zur Verwendung von [!DNL Customer Match], die im Abschnitt [Dokumentation zur Google-Unterstützung](https://support.google.com/google-ads/answer/6299717).

Stellen Sie als Nächstes sicher, dass Ihre [!DNL Google] -Konto für eine [!DNL Standard] oder einer höheren Berechtigungsebene. Siehe [Dokumentation zu Google Ads](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) für Details.

### Zulassungsliste {#allowlist}

Vor der Erstellung [!DNL Google Customer Match] Ziel in Experience Platform, stellen Sie sicher, dass Ihre [!DNL Google Ads] das Konto erfüllt [Google-Richtlinie zur Kundenabstimmung](https://support.google.com/google-ads/answer/6299717/customer-match-policy).

Kunden mit kompatiblen Konten werden von Google automatisch auf die Zulassungsliste gesetzt.

## Anforderungen an die ID-Übereinstimmung {#id-matching-requirements}

[!DNL Google] erfordert, dass keine personenbezogenen Daten (PII) klar übermittelt werden. Daher werden die Zielgruppen für [!DNL Google Customer Match] kann deaktiviert werden *Hash* Kennungen wie E-Mail-Adressen oder Telefonnummern.

Abhängig vom Typ der IDs, die Sie in Adobe Experience Platform erfassen, müssen Sie die entsprechenden Anforderungen erfüllen.

### Hash-Anforderungen für Telefonnummern {#phone-number-hashing-requirements}

Es gibt zwei Methoden zum Aktivieren von Telefonnummern in [!DNL Google Customer Match]:

* **Rohe Telefonnummern erfassen**: Sie können rohe Telefonnummern in der [!DNL E.164] in [!DNL Platform]und sie werden bei Aktivierung automatisch gehasht. Wenn Sie diese Option wählen, achten Sie darauf, Ihre rohen Telefonnummern immer in die `Phone_E.164` Namespace.
* **Hash-Telefonnummern erfassen**: Sie können Ihre Telefonnummern vor der Erfassung in [!DNL Platform]. Wenn Sie diese Option wählen, achten Sie darauf, Ihre Hash-Telefonnummern immer in die `PHONE_SHA256_E.164` Namespace.

>[!NOTE]
>
>Telefonnummern, die in die `Phone` Namespace kann nicht in aktiviert werden [!DNL Google Customer Match].

### Anforderungen an das E-Mail-Hashing {#hashing-requirements}

Sie können E-Mail-Adressen hash, bevor Sie sie in Adobe Experience Platform aufnehmen, oder eindeutige E-Mail-Adressen in Experience Platform verwenden und [!DNL Platform] Hash sie bei Aktivierung.

Weitere Informationen zu den Hash-Anforderungen von Google und anderen Aktivierungsbeschränkungen finden Sie in den folgenden Abschnitten der Google-Dokumentation:

* [[!DNL Customer Match] mit E-Mail-Adresse, -Adresse oder Benutzer-ID](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] considerations](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_considerations)
* [Kundenabgleich mit Telefonnummer](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_phone_number)
* [Kundenabgleich mit Mobilgeräte-IDs](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_mobile_device_ids)


Informationen zur Aufnahme von E-Mail-Adressen in Experience Platform finden Sie in der [Batch-Erfassung - Übersicht](../../../ingestion/batch-ingestion/overview.md) und [Streaming-Erfassung - Übersicht](../../../ingestion/streaming-ingestion/overview.md).

Wenn Sie sich dafür entscheiden, die E-Mail-Adressen selbst zu hash, stellen Sie sicher, dass Sie die Anforderungen von Google erfüllen, wie in den obigen Links beschrieben.

### Verwenden benutzerdefinierter Namespaces {#custom-namespaces}

Bevor Sie die `User_ID` Namespace zum Senden von Daten an Google verwenden, stellen Sie sicher, dass Sie Ihre eigenen Kennungen mit [!DNL gTag]. Siehe Abschnitt [Offizielle Dokumentation zu Google](https://support.google.com/google-ads/answer/9199250) für detaillierte Informationen.

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

<!-- ## Configure destination - video walkthrough {#video}

The video below demonstrates the steps to configure a [!DNL Google Customer Match] destination and activate segments. The steps are also laid out sequentially in the next sections.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng) -->

## Herstellen einer Verbindung mit der Datenbank {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele verwalten]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Namen für diese Zielverbindung angeben
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für diese Zielverbindung ein
* **[!UICONTROL Konto-ID]**: Ihre [Google Ads-Kunden-ID](https://support.google.com/google-ads/answer/1704344?hl=en). Das Format der ID ist xxx-xxx-xxxx. Wenn Sie die [!DNL Google Ads Manager Account (My Client Center)]verwenden Sie nicht Ihre Manager-Konto-ID. Verwenden Sie die [Google Ads-Kunden-ID](https://support.google.com/google-ads/answer/1704344?hl=en) anstatt.

>[!IMPORTANT]
>
> * Die **[!UICONTROL Kombinieren mit PII]** Marketing-Aktion ist standardmäßig für die [!DNL Google Customer Match] Ziel und kann nicht entfernt werden.


## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Siehe [Aktivieren von Zielgruppendaten für Streaming-Segmentexportziele](../../ui/activate-segment-streaming-destinations.md) für Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel.

Im **[!UICONTROL Segmentplan]** Schritt, müssen Sie die [!UICONTROL App-ID] beim Senden [!DNL IDFA] oder [!DNL GAID] Segmente in [!DNL Google Customer Match].

![Google-Kunden-Match-App-ID](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

Weitere Informationen zum Auffinden der [!DNL App ID], siehe [Offizielle Dokumentation zu Google](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid).

### Zuordnungsbeispiel: Aktivieren von Zielgruppendaten in [!DNL Google Customer Match] {#example-gcm}

Dies ist ein Beispiel für die korrekte Identitätszuordnung bei der Aktivierung von Zielgruppendaten in [!DNL Google Customer Match].

Auswählen von Quellfeldern:

* Wählen Sie die `Email` Namespace als Quellidentität verwenden, wenn die von Ihnen verwendeten E-Mail-Adressen nicht gehasht sind.
* Wählen Sie die `Email_LC_SHA256` Namespace als Quellidentität verwenden, wenn Sie bei der Datenerfassung in einen Hash-Wert für E-Mail-Adressen von Kunden [!DNL Platform]gemäß [!DNL Google Customer Match] [Anforderungen an das E-Mail-Hashing](#hashing-requirements).
* Wählen Sie die `PHONE_E.164` Namespace als Quellkennung verwenden, wenn Ihre Daten aus nicht gehashten Telefonnummern bestehen. [!DNL Platform] Hash die Telefonnummern, um die [!DNL Google Customer Match] Anforderungen.
* Wählen Sie die `Phone_SHA256_E.164` Namespace als Quellidentität, wenn Sie bei der Datenerfassung in [!DNL Platform]gemäß [!DNL Facebook] [Hash-Anforderungen für Telefonnummern](#phone-number-hashing-requirements).
* Wählen Sie die `IDFA` Namespace als Quellidentität, wenn Ihre Daten aus [!DNL Apple] Geräte-IDs.
* Wählen Sie die `GAID` Namespace als Quellidentität, wenn Ihre Daten aus [!DNL Android] Geräte-IDs.
* Wählen Sie die `Custom` Namespace als Quellidentität verwenden, wenn Ihre Daten aus einem anderen Kennungstyp bestehen.

Zielgruppenfelder auswählen:

* Wählen Sie die `Email_LC_SHA256` Namespace als Zielidentität verwenden, wenn Ihre Quell-Namespaces `Email` oder `Email_LC_SHA256`.
* Wählen Sie die `Phone_SHA256_E.164` Namespace als Zielidentität verwenden, wenn Ihre Quell-Namespaces `PHONE_E.164` oder `Phone_SHA256_E.164`.
* Wählen Sie die `IDFA` oder `GAID` Namespaces als Zielidentität verwenden, wenn Ihre Quell-Namespaces `IDFA` oder `GAID`.
* Wählen Sie die `User_ID` Namespace als Zielidentität verwenden, wenn Ihr Quell-Namespace ein benutzerdefinierter ist.

![Identitätszuordnung](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm.png)

Daten aus nicht gehashten Namespaces werden automatisch von [!DNL Platform] bei Aktivierung.

Attributquellendaten werden nicht automatisch gehasht. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die **[!UICONTROL Umwandlung anwenden]** -Option, um [!DNL Platform] die Daten bei Aktivierung automatisch hash.

![Identity Mapping Transformation](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm-transformation.png)

## Überprüfen, ob die Segmentaktivierung erfolgreich war {#verify-activation}

Wechseln Sie nach Abschluss des Aktivierungsvorgangs zu Ihrer **[!UICONTROL Google Ads]** -Konto. Die aktivierten Segmente werden in Ihrem Google-Konto als Kundenlisten angezeigt. Beachten Sie, dass je nach Segmentgröße einige Zielgruppen nur dann gefüllt werden, wenn mehr als 100 aktive Benutzer zur Verfügung stehen.

Beim Zuordnen eines Segments zu [!DNL IDFA] und [!DNL GAID] mobile IDs, [!DNL Google Customer Match] erstellt für jede ID-Zuordnung ein eigenes Segment. Ihre [!DNL Google Ads] zeigt zwei verschiedene Segmente an: eines für die [!DNL IDFA]und einer für die [!DNL GAID] Zuordnung.

## Fehlerbehebung {#troubleshooting}

### 400 Fehlermeldung &quot;Bad Request&quot; {#bad-request}

Beim Konfigurieren dieses Ziels wird möglicherweise der folgende Fehler angezeigt:

`{"message":"Google Customer Match Error: OperationAccessDenied.ACTION_NOT_PERMITTED","code":"400 BAD_REQUEST"}`

Dieser Fehler tritt auf, wenn Kundenkonten die [Voraussetzungen](#google-account-prerequisites). Wenden Sie sich zur Behebung dieses Problems an Google und stellen Sie sicher, dass Ihr Konto auf der Zulassungsliste steht und für eine [!DNL Standard] oder einer höheren Berechtigungsebene. Siehe [Dokumentation zu Google Ads](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) für Details.

## Weitere Ressourcen {#additional-resources}

* [Google-Kundenabgleich integrieren - Video-Tutorial](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html)

