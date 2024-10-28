---
keywords: Google-Kundenabgleich;Google-Kundenabgleich;Google-Kundenabgleich
title: Google Customer Match-Verbindung
description: Mit Google-Kundenabgleich können Sie Ihre Online- und Offline-Daten verwenden, um Ihre Kunden über die eigenen und betriebenen Eigenschaften von Google wie Suche, Shopping, Gmail und YouTube zu erreichen und erneut mit ihnen zu interagieren.
exl-id: 8209b5eb-b05c-4ef7-9fdc-22a528d5f020
source-git-commit: 25dc27d890cb2e0e23f8fa797ac9edea929164fd
workflow-type: tm+mt
source-wordcount: '2100'
ht-degree: 18%

---

# [!DNL Google Customer Match]-Verbindung

>[!IMPORTANT]
>
> Google veröffentlicht Änderungen an der [Google Ads API](https://developers.google.com/google-ads/api/docs/start), der [Kundenabgleich](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) und der [Display &amp; Video 360 API](https://developers.google.com/display-video/api/guides/getting-started/overview), um die Compliance- und Zustimmungsanforderungen zu unterstützen, die im [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA) in der Europäischen Union ([EU-Benutzerzustimmungsrichtlinie](https://www.google.com/about/company/user-consent-policy/)) definiert sind. Die Durchsetzung dieser Änderungen an den Zustimmungsanforderungen ist ab 6. März 2024 verfügbar.
><br/>
>Um die EU-Politik zur Einwilligung von Nutzern einzuhalten und im Europäischen Wirtschaftsraum (EWR) weiterhin Zielgruppenlisten für Benutzer zu erstellen, müssen Werbetreibende und Partner sicherstellen, dass sie beim Hochladen von Zielgruppendaten die Einwilligung der Endnutzer weitergeben. Als Google-Partner bietet Ihnen Adobe die nötigen Tools, um diese Zustimmungsanforderungen gemäß DMA in der Europäischen Union zu erfüllen.
><br/>
>Kunden, die Adobe Privacy &amp; Security Shield erworben und eine [Zustimmungsrichtlinie](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) konfiguriert haben, um Profile ohne Zustimmung herauszufiltern, müssen keine Maßnahmen ergreifen.
><br/>
>Kunden, die keine Adobe Privacy &amp; Security Shield erworben haben, müssen die Funktion [Segmentdefinition](../../../segmentation/home.md#segment-definitions) in [Segment Builder](../../../segmentation/ui/segment-builder.md) verwenden, um Profile ohne Zustimmung herauszufiltern, damit sie die bestehenden Real-Time CDP Google-Ziele ohne Unterbrechung weiterhin verwenden können.

Mit [[!DNL Google Customer Match]](https://support.google.com/google-ads/answer/6379332?hl=en) können Sie Ihre Online- und Offline-Daten verwenden, um Ihre Kunden über die eigenen und betriebenen Eigenschaften von Google zu erreichen und erneut anzusprechen, z. B.: [!DNL Search], [!DNL Shopping], [!DNL Gmail] und [!DNL YouTube].

![Google-Kundenabgleichziel in der Adobe Experience Platform-Benutzeroberfläche.](../../assets/catalog/advertising/google-customer-match/catalog.png)

## Anwendungsfälle {#use-cases}

Um Ihnen zu helfen, besser zu verstehen, wie und wann das [!DNL Google Customer Match]-Ziel verwendet werden soll, finden Sie hier Beispielanwendungsfälle, die Adobe Experience Platform-Kunden mit dieser Funktion lösen können.

### Anwendungsfall 1

Eine Marke für Sportbekleidung möchte Bestandskunden über [!DNL Google Search] und [!DNL Google Shopping] erreichen, um Angebote und Artikel auf der Grundlage ihrer früheren Käufe und des Browserverlaufs zu personalisieren. Die Bekleidungsmarke kann E-Mail-Adressen aus ihrem eigenen CRM-System auf Experience Platform erfassen und Zielgruppen aus eigenen Offline-Daten erstellen. Anschließend können sie diese Zielgruppen an [!DNL Google Customer Match] senden, um sie für [!DNL Search] und [!DNL Shopping] zu verwenden und so ihre Werbeausgaben zu optimieren.

### Anwendungsfall 2

Ein renommiertes Technologieunternehmen startete ein neues Telefon. Um dieses neue Telefonmodell zu bewerben, möchten sie Kunden, die Inhaber früherer Modelle ihrer Telefone sind, für die neuen Funktionen des Telefons sensibilisieren.

Um die Veröffentlichung zu bewerben, laden sie E-Mail-Adressen aus ihrer CRM-Datenbank unter Verwendung der E-Mail-Adressen als Kennungen in Experience Platform hoch. Zielgruppen werden basierend auf Kunden erstellt, die Inhaber älterer Telefonmodelle sind. Anschließend werden Zielgruppen an [!DNL Google Customer Match] gesendet, sodass das Unternehmen aktuelle Kunden, Kunden, die Inhaber älterer Telefonmodelle sind, und ähnliche Kunden mit [!DNL YouTube] ansprechen kann.

## Data Governance für [!DNL Google Customer Match] -Ziele {#data-governance}

Einige Ziele in Experience Platform haben bestimmte Regeln und Pflichten für Daten, die an die Zielplattform gesendet oder von ihr empfangen werden. Sie sind dafür verantwortlich, die Einschränkungen und Pflichten Ihrer Daten zu verstehen und zu verstehen, wie Sie diese Daten in Adobe Experience Platform und der Zielplattform verwenden. Adobe Experience Platform bietet Data Governance-Tools, mit denen Sie einige dieser Datennutzungsverpflichtungen verwalten können. [Erfahren Sie mehr ](../../../data-governance/labels/overview.md) über Data Governance-Tools und -Richtlinien.

## Unterstützte Identitäten {#supported-identities}

[!DNL Google Customer Match] unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| IDFA | Apple ID für Advertiser | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein IDFA-Namespace ist. |
| phone_sha256_e.164 | Telefonnummern im E164-Format, gehasht mit dem SHA256-Algorithmus | Es werden sowohl einfache als auch SHA256-Hash-Telefonnummern von Adobe Experience Platform unterstützt. Befolgen Sie die Anweisungen im Abschnitt [ID-Abgleich-Anforderungen](#id-matching-requirements-id-matching-requirements) und verwenden Sie die entsprechenden Namespaces für Klartext- bzw. Hash-Telefonnummern. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Platform] die Daten bei Aktivierung automatisch hasht. |
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Es werden sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen von Adobe Experience Platform unterstützt. Befolgen Sie die Anweisungen im Abschnitt [ID-Übereinstimmungsanforderungen](#id-matching-requirements-id-matching-requirements) und verwenden Sie die entsprechenden Namespaces für Nur-Text- bzw. Hash-E-Mail-Adressen. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Platform] die Daten bei Aktivierung automatisch hasht. |
| user_id | Benutzerdefinierte Benutzer-IDs | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein benutzerdefinierter Namespace ist. |

{style="table-layout:auto"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Zielgruppentypen Sie an dieses Ziel exportieren können.

| Audience Origin | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die durch den Experience Platform [Segmentierungsdienst](../../../segmentation/home.md) generiert wurden. |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (Name, Telefonnummer und andere), die im [!DNL Google Customer Match]-Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## [!DNL Google Customer Match] Kontovoraussetzungen {#google-account-prerequisites}

Bevor Sie ein [!DNL Google Customer Match] -Ziel in Experience Platform einrichten, sollten Sie die Google-Richtlinie zur Verwendung von [!DNL Customer Match] lesen und einhalten, wie in der [Google-Support-Dokumentation](https://support.google.com/google-ads/answer/6299717) beschrieben.

Stellen Sie als Nächstes sicher, dass Ihr [!DNL Google]-Konto für eine Berechtigungsebene von [!DNL Standard] oder höher konfiguriert ist. Weitere Informationen finden Sie in der Dokumentation zu Google Ads](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) .[

### Zulassungsliste {#allowlist}

Bevor Sie das Ziel [!DNL Google Customer Match] in Experience Platform erstellen, stellen Sie sicher, dass Ihr [!DNL Google Ads]-Konto die [[!DNL Google Customer Match] Richtlinie](https://support.google.com/google-ads/answer/6299717/customer-match-policy) erfüllt.

Kunden mit kompatiblen Konten werden automatisch von Google auf die Zulassungsliste gesetzt.

## Anforderungen an die ID-Übereinstimmung {#id-matching-requirements}

[!DNL Google] erfordert, dass keine personenbezogenen Daten (PII) klar gesendet werden. Daher können die für [!DNL Google Customer Match] aktivierten Zielgruppen aus *Hash*-Identifikatoren wie E-Mail-Adressen oder Telefonnummern abgeleitet werden.

Abhängig vom Typ der IDs, die Sie in Adobe Experience Platform erfassen, müssen Sie die entsprechenden Anforderungen erfüllen.

### Hash-Anforderungen für Telefonnummern {#phone-number-hashing-requirements}

Es gibt zwei Methoden zum Aktivieren von Telefonnummern in [!DNL Google Customer Match]:

* **Aufnahme von rohen Telefonnummern**: Sie können rohe Telefonnummern im Format [!DNL E.164] in [!DNL Platform] aufnehmen und sie werden bei Aktivierung automatisch gehasht. Wenn Sie diese Option wählen, achten Sie darauf, Ihre rohen Telefonnummern immer in den Namespace `Phone_E.164` aufzunehmen.
* **Hash-Telefonnummern erfassen**: Sie können Ihre Telefonnummern vorab hash, bevor Sie sie in [!DNL Platform] aufnehmen. Wenn Sie diese Option wählen, achten Sie darauf, Ihre Hash-Telefonnummern immer in den Namespace `PHONE_SHA256_E.164` aufzunehmen.

>[!NOTE]
>
>Telefonnummern, die in den Namespace `Phone` aufgenommen werden, können in [!DNL Google Customer Match] nicht aktiviert werden.

### Anforderungen an das E-Mail-Hashing {#hashing-requirements}

Sie können E-Mail-Adressen vor der Aufnahme in Adobe Experience Platform hash-Adressen oder eindeutige E-Mail-Adressen in Experience Platform verwenden und diese bei der Aktivierung mit [!DNL Platform] hash lassen.

Weitere Informationen zu den Hash-Anforderungen von Google und anderen Aktivierungsbeschränkungen finden Sie in den folgenden Abschnitten der Google-Dokumentation:

* [[!DNL Customer Match]  mit E-Mail-Adresse, -Adresse oder Benutzer-ID](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] considerations](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_considerations)
* [[!DNL Customer Match] mit Telefonnummer](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_phone_number)
* [[!DNL Customer Match] mit Mobilgeräte-IDs](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_mobile_device_ids)


Weiterführende Informationen zur Aufnahme von E-Mail-Adressen in Experience Platform finden Sie in der [Batch-Erfassungsübersicht](../../../ingestion/batch-ingestion/overview.md) und der [Streaming-Erfassungsübersicht](../../../ingestion/streaming-ingestion/overview.md).

Wenn Sie sich dafür entscheiden, die E-Mail-Adressen selbst zu hash, stellen Sie sicher, dass Sie die Anforderungen von Google erfüllen, wie in den obigen Links beschrieben.

### Verwenden benutzerdefinierter Namespaces {#custom-namespaces}

Bevor Sie den Namespace `User_ID` zum Senden von Daten an Google verwenden können, müssen Sie Ihre eigenen Kennungen mit [!DNL gTag] synchronisieren. Detaillierte Informationen finden Sie in der [offiziellen Google-Dokumentation](https://support.google.com/google-ads/answer/9199250) .

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

<!-- ## Configure destination - video walkthrough {#video}

The video below demonstrates the steps to configure a [!DNL Google Customer Match] destination and activate audiences. The steps are also laid out sequentially in the next sections.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng) -->

## Videoüberblick {#video-overview}

Sehen Sie sich das folgende Video an, um eine Erläuterung der Vorteile und wie Sie Daten für die Google-Kundenabstimmung aktivieren.

>[!VIDEO](https://video.tv.adobe.com/v/38180/)

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Geben Sie einen Namen für diese Zielverbindung an
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für diese Zielverbindung ein.
* **[!UICONTROL Konto-ID]**: Ihre [Google Ads-Kunden-ID](https://support.google.com/google-ads/answer/1704344?hl=en). Das Format der ID ist xxx-xxx-xxxx. Verwenden Sie bei Verwendung von [!DNL Google Ads Manager Account (My Client Center)] nicht Ihre Manager-Konto-ID. Verwenden Sie stattdessen die Google Ads-Kunden-ID](https://support.google.com/google-ads/answer/1704344?hl=en).[

>[!IMPORTANT]
>
> * Die Marketing-Aktion **[!UICONTROL Mit PII kombinieren]** ist standardmäßig für das Ziel [!DNL Google Customer Match] ausgewählt und kann nicht entfernt werden.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Um *Identitäten* in Ziele zu exportieren, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [ ](/help/access-control/home.md#permissions) <br>. ![Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Streaming-Zielgruppen-Exportziele](../../ui/activate-segment-streaming-destinations.md).

Im Schritt **[!UICONTROL Segmentplan]** müssen Sie die [!UICONTROL App-ID] angeben, wenn Sie [!DNL IDFA] oder [!DNL GAID] Zielgruppen an [!DNL Google Customer Match] senden.

![Google Customer Match App ID -Feld im Schritt Segmentzeitplan des Aktivierungs-Workflows hervorgehoben.](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

Weitere Informationen zum Auffinden des [!DNL App ID] finden Sie in der [offiziellen Google-Dokumentation](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid) oder bei Ihrem Google-Support-Mitarbeiter.

### Zuordnungsbeispiel: Aktivieren von Zielgruppendaten in [!DNL Google Customer Match] {#example-gcm}

Dies ist ein Beispiel für die korrekte Identitätszuordnung bei der Aktivierung von Zielgruppendaten in [!DNL Google Customer Match].

Quellfelder auswählen:

* Wählen Sie den Namespace `Email` als Quellidentität aus, wenn die von Ihnen verwendeten E-Mail-Adressen nicht gehasht werden.
* Wählen Sie den Namespace `Email_LC_SHA256` als Quellidentität aus, wenn Sie Kunden-E-Mail-Adressen bei der Datenerfassung gemäß den Anforderungen für den E-Mail-Hashing [!DNL Google Customer Match] [E-Mail-Hashing](#hashing-requirements) in [!DNL Platform] gehasht haben.
* Wählen Sie den Namespace `PHONE_E.164` als Quellkennung aus, wenn Ihre Daten aus nicht gehashten Telefonnummern bestehen. [!DNL Platform] hasst die Telefonnummern, um die [!DNL Google Customer Match]-Anforderungen zu erfüllen.
* Wählen Sie den Namespace `Phone_SHA256_E.164` als Quellidentität aus, wenn Sie bei der Datenerfassung Telefonnummern gemäß den Anforderungen für das Hashing der Telefonnummer [!DNL Facebook] [4 bei der Erfassung der Daten in [!DNL Platform] gehasht haben.](#phone-number-hashing-requirements)
* Wählen Sie den Namespace `IDFA` als Quellidentität aus, wenn Ihre Daten aus [!DNL Apple] Geräte-IDs bestehen.
* Wählen Sie den Namespace `GAID` als Quellidentität aus, wenn Ihre Daten aus [!DNL Android] Geräte-IDs bestehen.
* Wählen Sie den Namespace `Custom` als Quellidentität aus, wenn Ihre Daten aus anderen Kennungen bestehen.

Zielgruppenfelder auswählen:

* Wählen Sie den Namespace `Email_LC_SHA256` als Zielidentität aus, wenn Ihre Quell-Namespaces entweder `Email` oder `Email_LC_SHA256` sind.
* Wählen Sie den Namespace `Phone_SHA256_E.164` als Zielidentität aus, wenn Ihre Quell-Namespaces entweder `PHONE_E.164` oder `Phone_SHA256_E.164` sind.
* Wählen Sie die Namespaces `IDFA` oder `GAID` als Zielidentität aus, wenn Ihre Quell-Namespaces `IDFA` oder `GAID` sind.
* Wählen Sie den Namespace `User_ID` als Zielidentität aus, wenn Ihr Quellnamespace ein benutzerdefinierter Namespace ist.

![Identitätszuordnung zwischen Quell- und Zielfeldern, die im Schritt &quot;Zuordnung&quot;des Aktivierungs-Workflows angezeigt werden.](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm.png)

Daten aus nicht gehashten Namespaces werden bei Aktivierung automatisch von [!DNL Platform] gehasht.

Attributquellendaten werden nicht automatisch gehasht. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Platform] die Daten bei Aktivierung automatisch hasht.

![Wenden Sie die Transformationssteuerung an, die im Schritt &quot;Zuordnung&quot;des Aktivierungs-Workflows hervorgehoben ist.](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm-transformation.png)

## Ziel überwachen {#monitor-destination}

Nachdem Sie eine Verbindung zum Ziel hergestellt und einen Ziel-Datenfluss eingerichtet haben, können Sie die [Überwachungsfunktion](/help/dataflows/ui/monitor-destinations.md) in Real-Time CDP verwenden, um umfassende Informationen über die Profildatensätze zu erhalten, die in jedem Datenfluss für Ihr Ziel aktiviert wurden.

>[!IMPORTANT]
>
> Ab Oktober 2024 führt Adobe eine Aktualisierung durch, um die Berichtsgenauigkeit für Streaming-Ziele zu erhöhen. Diese Verbesserung sorgt für eine bessere Abstimmung zwischen der Berichterstellung für Experience Platform und Zielplattformen.
>
> Vor dieser Aktualisierung umfasste **[!UICONTROL fehlgeschlagene Identitäten]** alle Aktivierungsversuche. Nach dieser Aktualisierung ist nur der letzte Aktivierungsversuch in der Gesamtanzahl enthalten.
>
> Diese Verbesserung gilt derzeit für das Ziel [Google-Kundenabgleich](google-customer-match.md) , wird jedoch schrittweise für andere Experience Platform-Streaming-Ziele eingeführt.
> Nach dieser Verbesserung sehen Benutzer dieses Ziels möglicherweise einen erwarteten Rückgang ihrer Anzahl von **[!UICONTROL Identitäten fehlgeschlagen]**.


## Überprüfen, ob die Zielgruppenaktivierung erfolgreich war {#verify-activation}

Wechseln Sie nach Abschluss des Aktivierungsvorgangs zu Ihrem Konto für **[!UICONTROL Google Ads]**. Die aktivierten Zielgruppen werden in Ihrem Google-Konto als Kundenlisten angezeigt. Abhängig von der Größe Ihrer Zielgruppe füllen sich einige Zielgruppen nur aus, wenn mehr als 100 aktive Benutzer zur Verfügung stehen.

Wenn eine Zielgruppe sowohl [!DNL IDFA] als auch [!DNL GAID] mobile IDs zugeordnet wird, erstellt [!DNL Google Customer Match] für jede ID-Zuordnung eine separate Zielgruppe. Ihr [!DNL Google Ads] -Konto zeigt zwei verschiedene Segmente an: eines für die [!DNL IDFA] und eines für die [!DNL GAID] -Zuordnung.

## Fehlerbehebung {#troubleshooting}

### Fehlermeldung „400 Fehlerhafte Anfrage“ {#bad-request}

Beim Konfigurieren dieses Ziels wird möglicherweise der folgende Fehler angezeigt:

`{"message":"Google Customer Match Error: OperationAccessDenied.ACTION_NOT_PERMITTED","code":"400 BAD_REQUEST"}`

Dieser Fehler tritt auf, wenn Kundenkonten nicht den [Voraussetzungen](#google-account-prerequisites) entsprechen. Um dieses Problem zu beheben, wenden Sie sich an Google und stellen Sie sicher, dass Ihr Konto auf der Zulassungsliste steht und für eine [!DNL Standard] oder eine höhere Berechtigungsstufe konfiguriert ist. Weitere Informationen finden Sie in der Dokumentation zu Google Ads](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) .[