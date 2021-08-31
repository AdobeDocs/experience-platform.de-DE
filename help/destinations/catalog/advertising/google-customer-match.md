---
keywords: Google-Kundenabgleich;Google-Kundenabgleich;Google-Kundenabgleich
title: Google-Kundenabgleich-Verbindung
description: Mit Google-Kundenabgleich können Sie Ihre Online- und Offline-Daten verwenden, um Ihre Kunden über die von Google verwalteten und betriebenen Eigenschaften wie Suche, Shopping, Gmail und YouTube zu erreichen und erneut mit ihnen zu interagieren.
exl-id: 8209b5eb-b05c-4ef7-9fdc-22a528d5f020
source-git-commit: d0112cb26fcb85ad91ba403f81ee7f11d0889046
workflow-type: tm+mt
source-wordcount: '1557'
ht-degree: 1%

---

# [!DNL Google Customer Match] connection

## Übersicht {#overview}

[Google-Kundendaten ](https://support.google.com/google-ads/answer/6379332?hl=en) verwenden Sie Ihre Online- und Offline-Daten, um Ihre Kunden über die von Google verwalteten und betriebenen Eigenschaften hinweg zu erreichen und erneut mit ihnen zu interagieren, z. B.:  [!DNL Search],  [!DNL Shopping],  [!DNL Gmail] und  [!DNL YouTube].

![Google-Kundenabgleich-Ziel in der Adobe Experience Platform-Benutzeroberfläche](../../assets/catalog/advertising/google-customer-match/catalog.png)

## Anwendungsfälle

Um Ihnen zu helfen, besser zu verstehen, wie und wann das [!DNL Google Customer Match]-Ziel verwendet werden sollte, finden Sie hier Beispielanwendungsfälle, die Adobe Experience Platform-Kunden mit dieser Funktion lösen können.

### Anwendungsfall 1

Eine Marke für Sportbekleidung möchte Bestandskunden über [!DNL Google Search] und [!DNL Google Shopping] erreichen, um Angebote und Artikel auf der Grundlage ihrer früheren Käufe und des Browserverlaufs zu personalisieren. Die Bekleidungsmarke kann E-Mail-Adressen aus ihrem eigenen CRM-System in die Experience Platform aufnehmen und aus ihren eigenen Offline-Daten Segmente erstellen. Anschließend können sie diese Segmente an [!DNL Google Customer Match] senden, um sie über [!DNL Search] und [!DNL Shopping] hinweg zu verwenden und so ihre Werbeausgaben zu optimieren.

### Anwendungsfall 2

Ein renommiertes Technologieunternehmen startete ein neues Telefon. Um dieses neue Telefonmodell zu bewerben, möchten sie Kunden, die Inhaber früherer Modelle ihrer Telefone sind, für die neuen Funktionen des Telefons sensibilisieren.

Um die Veröffentlichung zu bewerben, laden sie E-Mail-Adressen aus ihrer CRM-Datenbank in Experience Platform hoch und verwenden dabei die E-Mail-Adressen als Kennungen. Segmente werden basierend auf Kunden erstellt, die ältere Telefonmodelle besitzen. Anschließend werden Segmente an [!DNL Google Customer Match] gesendet, sodass das Unternehmen aktuelle Kunden, Kunden, die ältere Telefonmodelle besitzen, und ähnliche Kunden mit [!DNL YouTube] ansprechen kann.

## Data Governance für [!DNL Google Customer Match]-Ziele {#data-governance}

Für einige Ziele in der Experience Platform gelten bestimmte Regeln und Pflichten für Daten, die an die Zielplattform gesendet oder von dieser empfangen werden. Sie sind dafür verantwortlich, die Einschränkungen und Pflichten Ihrer Daten zu verstehen und zu verstehen, wie Sie diese Daten in Adobe Experience Platform und der Zielplattform verwenden. Adobe Experience Platform bietet Data Governance-Tools, mit denen Sie einige dieser Datennutzungsverpflichtungen verwalten können. [Erfahren Sie ](../../../data-governance/labels/overview.md) mehr über Data Governance-Tools und -Richtlinien.

## Unterstützte Identitäten {#supported-identities}

[!DNL Google Customer Match] unterstützt die Aktivierung der in der folgenden Tabelle beschriebenen Identitäten. Erfahren Sie mehr über [identities](/help/identity-service/namespaces.md).

| Zielgruppenidentität | Beschreibung | Zu beachten |
|---|---|---|
| GAID | Google Advertising ID | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| IDFA | Apple ID für Advertiser | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein IDFA-Namespace ist. |
| phone_sha256_e.164 | Telefonnummern im E164-Format, gehasht mit dem SHA256-Algorithmus | Sowohl einfache als auch SHA256-Hash-Telefonnummern werden von Adobe Experience Platform unterstützt. Befolgen Sie die Anweisungen im Abschnitt [Anforderungen an die ID-Zuordnung](#id-matching-requirements-id-matching-requirements) und verwenden Sie die entsprechenden Namespaces für einfache Text- bzw. Hash-Telefonnummern. Wenn Ihr Quellfeld ungehashte Attribute enthält, aktivieren Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Platform] die Daten bei Aktivierung automatisch hash. |
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen werden von Adobe Experience Platform unterstützt. Befolgen Sie die Anweisungen im Abschnitt [Anforderungen an die ID-Zuordnung](#id-matching-requirements-id-matching-requirements) und verwenden Sie die entsprechenden Namespaces für Nur-Text- bzw. Hash-E-Mail-Adressen. Wenn Ihr Quellfeld ungehashte Attribute enthält, aktivieren Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Platform] die Daten bei Aktivierung automatisch hash. |
| user_id | Benutzerdefinierte Benutzer-IDs | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein benutzerdefinierter Namespace ist. |

## Exporttyp {#export-type}

**Segmentexport** : Sie exportieren alle Mitglieder eines Segments (Zielgruppe) mit den IDs (Name, Telefonnummer und andere), die im  [!DNL Google Customer Match] Ziel verwendet werden.

## [!DNL Google Customer Match] Kontovoraussetzungen {#google-account-prerequisites}

Bevor Sie ein [!DNL Google Customer Match]-Ziel in Experience Platform einrichten, sollten Sie die Google-Richtlinien zur Verwendung von [!DNL Customer Match] lesen und einhalten, die in der [Google-Support-Dokumentation](https://support.google.com/google-ads/answer/6299717) beschrieben sind.

Stellen Sie als Nächstes sicher, dass Ihr [!DNL Google]-Konto für eine [!DNL Standard] oder eine höhere Berechtigungsebene konfiguriert ist. Weitere Informationen finden Sie in der [Dokumentation zu Google Ads](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1).

### Zulassungsliste {#allowlist}

Bevor Sie das [!DNL Google Customer Match]-Ziel in Experience Platform erstellen, stellen Sie sicher, dass Ihr [!DNL Google Ads]-Konto die [Google-Kundenübereinstimmungsrichtlinie](https://support.google.com/google-ads/answer/6299717/customer-match-policy) erfüllt.

Kunden mit kompatiblen Konten werden von Google automatisch auf die Zulassungsliste gesetzt.

## Anforderungen an die ID-Übereinstimmung {#id-matching-requirements}

[!DNL Google] erfordert, dass keine personenbezogenen Daten (PII) klar übermittelt werden. Daher können die für [!DNL Google Customer Match] aktivierten Zielgruppen von *Hash*-Identifikatoren wie E-Mail-Adressen oder Telefonnummern abgeleitet werden.

Abhängig vom Typ der IDs, die Sie in Adobe Experience Platform erfassen, müssen Sie die entsprechenden Anforderungen erfüllen.

## Hash-Anforderungen für Telefonnummern {#phone-number-hashing-requirements}

Es gibt zwei Methoden zum Aktivieren von Telefonnummern in [!DNL Google Customer Match]:

* **Rohe Telefonnummern** erfassen: Sie können rohe Telefonnummern im  [!DNL E.164] Format in aufnehmen und  [!DNL Platform]werden bei Aktivierung automatisch gehasht. Wenn Sie diese Option wählen, achten Sie darauf, Ihre rohen Telefonnummern immer in den Namespace `Phone_E.164` aufzunehmen.
* **Hash-Telefonnummern** erfassen: Sie können Ihre Telefonnummern vorab hash, bevor Sie sie in  [!DNL Platform]aufnehmen. Wenn Sie diese Option wählen, achten Sie darauf, Ihre Hash-Telefonnummern immer in den Namespace `PHONE_SHA256_E.164` aufzunehmen.

>[!NOTE]
>
>Telefonnummern, die in den Namespace `Phone` aufgenommen werden, können in [!DNL Google Customer Match] nicht aktiviert werden.

## Anforderungen an das E-Mail-Hashing {#hashing-requirements}

Sie können E-Mail-Adressen vor der Aufnahme in Adobe Experience Platform hash-Adressen oder in der Experience Platform eindeutige E-Mail-Adressen verwenden und [!DNL Platform] bei Aktivierung hash-Adressen einrichten.

Weitere Informationen zu den Hash-Anforderungen von Google und anderen Aktivierungsbeschränkungen finden Sie in den folgenden Abschnitten der Google-Dokumentation:

* [[!DNL Customer Match] mit E-Mail-Adresse, -Adresse oder Benutzer-ID](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] considerations](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_considerations)
* [Kundenabgleich mit Telefonnummer](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_phone_number)
* [Kundenabgleich mit Mobilgeräte-IDs](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_mobile_device_ids)


Weitere Informationen zur Aufnahme von E-Mail-Adressen in Experience Platform finden Sie unter [Batch-Erfassung - Übersicht](../../../ingestion/batch-ingestion/overview.md) und [Streaming-Erfassung - Übersicht](../../../ingestion/streaming-ingestion/overview.md).

Wenn Sie sich dafür entscheiden, die E-Mail-Adressen selbst zu hash, stellen Sie sicher, dass Sie die Anforderungen von Google erfüllen, wie in den obigen Links beschrieben.

## Verwenden benutzerdefinierter Namespaces {#custom-namespaces}

Bevor Sie den Namespace `User_ID` verwenden können, um Daten an Google zu senden, stellen Sie sicher, dass Sie Ihre eigenen Kennungen mit [!DNL gTag] synchronisieren. Ausführliche Informationen finden Sie in der [offiziellen Google-Dokumentation](https://support.google.com/google-ads/answer/9199250).

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

<!-- ## Configure destination - video walkthrough {#video}

The video below demonstrates the steps to configure a [!DNL Google Customer Match] destination and activate segments. The steps are also laid out sequentially in the next sections.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng) -->

## Mit Ziel verbinden {#connect}

Um eine Verbindung zu diesem Ziel herzustellen, führen Sie die Schritte aus, die im Tutorial [Zielkonfiguration](../../ui/connect-destination.md) beschrieben sind.

### Verbindungsparameter {#parameters}

Während [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Namen für diese Zielverbindung angeben
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für diese Zielverbindung ein
* **[!UICONTROL Konto-ID]**: Ihre Google-Kunden-ID. Das Format der ID ist xxx-xxx-xxxx.

>[!IMPORTANT]
>
> * Die Marketing-Aktion **[!UICONTROL Kombinieren mit PII]** ist standardmäßig für das [!DNL Google Customer Match]-Ziel ausgewählt und kann nicht entfernt werden.


## Aktivieren von Segmenten für dieses Ziel {#activate}

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Streaming-Segmentexportziele](../../ui/activate-segment-streaming-destinations.md) .

Im Schritt **[!UICONTROL Segment schedule]** müssen Sie die [!UICONTROL App-ID] angeben, wenn Sie [!DNL IDFA]- oder [!DNL GAID]-Segmente an [!DNL Google Customer Match] senden.

![Google-Kundenabgleich-App-ID](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

Weitere Informationen zum Auffinden des [!DNL App ID] finden Sie in der [offiziellen Google-Dokumentation](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid).

### Zuordnungsbeispiel: Aktivieren von Zielgruppendaten in [!DNL Google Customer Match] {#example-gcm}

Dies ist ein Beispiel für die korrekte Identitätszuordnung bei der Aktivierung von Zielgruppendaten in [!DNL Google Customer Match].

Auswählen von Quellfeldern:

* Wählen Sie den Namespace `Email` als Quellidentität aus, wenn die von Ihnen verwendeten E-Mail-Adressen nicht gehasht sind.
* Wählen Sie den Namespace `Email_LC_SHA256` als Quellidentität aus, wenn Sie Kunden-E-Mail-Adressen bei der Datenerfassung in [!DNL Platform] gehasht haben, gemäß [!DNL Google Customer Match] [E-Mail-Hashing-Anforderungen](#hashing-requirements).
* Wählen Sie den Namespace `PHONE_E.164` als Quellkennung aus, wenn Ihre Daten aus nicht gehashten Telefonnummern bestehen. [!DNL Platform] werden die Telefonnummern hash, um die  [!DNL Google Customer Match] Anforderungen zu erfüllen.
* Wählen Sie den Namespace `Phone_SHA256_E.164` als Quellidentität aus, wenn Sie bei der Datenerfassung Telefonnummern gemäß [!DNL Facebook] [ [!DNL Platform]Anforderungen an das Hashing von Telefonnummern](#phone-number-hashing-requirements) gehasht haben.
* Wählen Sie den Namespace `IDFA` als Quellidentität aus, wenn Ihre Daten aus [!DNL Apple] Geräte-IDs bestehen.
* Wählen Sie den Namespace `GAID` als Quellidentität aus, wenn Ihre Daten aus [!DNL Android] Geräte-IDs bestehen.
* Wählen Sie den Namespace `Custom` als Quellidentität aus, wenn Ihre Daten aus einem anderen Kennungstyp bestehen.

Zielgruppenfelder auswählen:

* Wählen Sie den Namespace `Email_LC_SHA256` als Zielidentität aus, wenn Ihre Quell-Namespaces entweder `Email` oder `Email_LC_SHA256` lauten.
* Wählen Sie den Namespace `Phone_SHA256_E.164` als Zielidentität aus, wenn Ihre Quell-Namespaces entweder `PHONE_E.164` oder `Phone_SHA256_E.164` lauten.
* Wählen Sie die Namespaces `IDFA` oder `GAID` als Zielidentität aus, wenn Ihre Quell-Namespaces `IDFA` oder `GAID` lauten.
* Wählen Sie den Namespace `User_ID` als Zielidentität aus, wenn Ihr Quellnamespace ein benutzerdefinierter Namespace ist.

![Identitätszuordnung](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm.png)

Daten aus nicht gehashten Namespaces werden bei Aktivierung automatisch von [!DNL Platform] gehasht.

Attributquellendaten werden nicht automatisch gehasht. Wenn Ihr Quellfeld ungehashte Attribute enthält, aktivieren Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Platform] die Daten bei Aktivierung automatisch hash.

![Identity Mapping Transformation](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm-transformation.png)

## Überprüfen, ob die Segmentaktivierung erfolgreich war {#verify-activation}

Wechseln Sie nach Abschluss des Aktivierungsvorgangs zu Ihrem **[!UICONTROL Google Ads]**-Konto. Die aktivierten Segmente werden in Ihrem Google-Konto als Kundenlisten angezeigt. Beachten Sie, dass je nach Segmentgröße einige Zielgruppen nur dann gefüllt werden, wenn mehr als 100 aktive Benutzer zur Verfügung stehen.

Wenn Sie ein Segment sowohl [!DNL IDFA] als auch [!DNL GAID] mobile IDs zuordnen, erstellt [!DNL Google Customer Match] für jede ID-Zuordnung ein eigenes Segment. Ihr [!DNL Google Ads]-Konto zeigt zwei verschiedene Segmente an, eines für [!DNL IDFA] und eines für das [!DNL GAID]-Mapping.

## Fehlerbehebung {#troubleshooting}

### 400 Fehlermeldung &quot;Bad Request&quot; {#bad-request}

Beim Konfigurieren dieses Ziels wird möglicherweise der folgende Fehler angezeigt:

`{"message":"Google Customer Match Error: OperationAccessDenied.ACTION_NOT_PERMITTED","code":"400 BAD_REQUEST"}`

Dieser Fehler tritt auf, wenn Kundenkonten die [Voraussetzungen](#google-account-prerequisites) nicht erfüllen. Um dieses Problem zu beheben, wenden Sie sich an Google und stellen Sie sicher, dass Ihr Konto auf der Zulassungsliste steht und für eine [!DNL Standard] oder höhere Berechtigungsstufe konfiguriert ist. Weitere Informationen finden Sie in der [Dokumentation zu Google Ads](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1).

## Zusätzliche Ressourcen {#additional-resources}

* [Google-Kundenabgleich integrieren - Video-Tutorial](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html)

