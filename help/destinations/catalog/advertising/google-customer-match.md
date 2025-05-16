---
keywords: Google Customer Match; Google Customer Match; Google Customer Match
title: Google Customer Match-Verbindung
description: Mit Google Customer Match können Sie Ihre Online- und Offline-Daten verwenden, um Ihre Kundinnen und Kunden in den von Google verwalteten und betriebenen Eigenschaften wie Search, Shopping und Gmail zu erreichen und erneut mit ihnen zu interagieren.
exl-id: 8209b5eb-b05c-4ef7-9fdc-22a528d5f020
source-git-commit: ce205622260f4252d1a7db7c5011366fb2ed4d3c
workflow-type: tm+mt
source-wordcount: '2410'
ht-degree: 15%

---

# [!DNL Google Customer Match]-Verbindung

>[!IMPORTANT]
>
> Google veröffentlicht Änderungen an der [Google Ads API](https://developers.google.com/google-ads/api/docs/start), [Customer Match](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) und der [Display &amp; Video 360 API](https://developers.google.com/display-video/api/guides/getting-started/overview), um die Compliance- und Zustimmungsanforderungen zu unterstützen, die im [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA) in der Europäischen Union definiert sind ([EU-Richtlinie zur ](https://www.google.com/about/company/user-consent-policy/)). Die Durchsetzung dieser Änderungen an den Einverständnisanforderungen ist ab dem 6. März 2024 aktiv.
><br/>
>Um die EU-Richtlinie zur Benutzerzustimmung einzuhalten und weiterhin Zielgruppenlisten für Nutzer im Europäischen Wirtschaftsraum (EWR) zu erstellen, müssen Werbetreibende und Partner sicherstellen, dass sie beim Hochladen von Zielgruppendaten die Zustimmung der Endnutzer weitergeben. Als Google-Partner stellt Adobe Ihnen die erforderlichen Tools zur Verfügung, um diese Zustimmungsanforderungen gemäß dem DMA in der Europäischen Union zu erfüllen.
><br/>
>Kunden, die Adobe Privacy &amp; Security Shield erworben und eine [Einverständnisrichtlinie“ ](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) haben, um nicht einverstandene Profile herauszufiltern, müssen keine Maßnahmen ergreifen.
><br/>
>Kunden, die Adobe Privacy &amp; Security Shield nicht erworben haben, müssen die [Segmentdefinition](../../../segmentation/home.md#segment-definitions)-Funktionen in [Segment Builder](../../../segmentation/ui/segment-builder.md) verwenden, um nicht einverstandene Profile herauszufiltern, damit die bestehenden Real-Time CDP Google-Ziele ohne Unterbrechung weiter verwendet werden können.

[[!DNL Google Customer Match]](https://support.google.com/google-ads/answer/6379332?hl=en) können Sie Ihre Online- und Offline-Daten verwenden, um Ihre Kunden über die von Google verwalteten und betriebenen Eigenschaften wie [!DNL Search], [!DNL Shopping] und [!DNL Gmail] zu erreichen und erneut mit ihnen zu interagieren.

>[!TIP]
>
>Um Kunden mit [!DNL YouTube] Inventar zu erreichen, verwenden Sie das Ziel [Google Customer Match + DV360](/help/destinations/catalog/advertising/google-customer-match-dv360.md), das die Google Audience Partner-API verwendet.

![Ziel von Google Customer Match in der Adobe Experience Platform-Benutzeroberfläche.](../../assets/catalog/advertising/google-customer-match/catalog.png)

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das [!DNL Google Customer Match]-Ziel verwenden, finden Sie hier einige Beispielanwendungsfälle, die Kundinnen und Kunden von Adobe Experience Platform mit dieser Funktion bewältigen können.

### Anwendungsfall #1

Eine Sportbekleidungsmarke möchte bestehende Kunden über [!DNL Google Search] und [!DNL Google Shopping] erreichen, um Angebote und Artikel basierend auf ihren früheren Käufen und dem Navigationsverlauf zu personalisieren. Die Bekleidungsmarke kann E-Mail-Adressen aus dem eigenen CRM in Experience Platform aufnehmen und Zielgruppen aus eigenen Offline-Daten erstellen. Anschließend können diese Zielgruppen an [!DNL Google Customer Match] gesendet und über [!DNL Search] und [!DNL Shopping] hinweg verwendet werden, wodurch die Werbeausgaben optimiert werden.

### Anwendungsfall #2

>[!TIP]
>
>Um dieses Anwendungsbeispiel für [!DNL YouTube] Inventar auszuführen, verwenden Sie das neue Ziel [Google Customer Match + DV360](/help/destinations/catalog/advertising/google-customer-match-dv360.md), das die Google Audience Partner-API verwendet.

Ein prominentes Technologieunternehmen brachte ein neues Telefon auf den Markt. Um dieses neue Telefonmodell zu bewerben, möchten sie das Bewusstsein für die neuen Funktionen und Möglichkeiten des Telefons auf Kunden lenken, die frühere Modelle ihres Telefons besitzen.

Um die Veröffentlichung zu bewerben, laden sie E-Mail-Adressen aus ihrer CRM-Datenbank in Experience Platform hoch, wobei sie die E-Mail-Adressen als Kennungen verwenden. Zielgruppen werden basierend auf Kunden erstellt, die ältere Telefonmodelle besitzen. Dann werden die Zielgruppen an [!DNL Google Customer Match] gesendet, damit das Unternehmen aktuelle Kunden, Kunden, die Inhaber älterer Telefonmodelle sind, und ähnliche Kunden auf [!DNL YouTube] ansprechen kann.

## Data Governance für [!DNL Google Customer Match] Ziele {#data-governance}

Für einige Ziele in Experience Platform gelten bestimmte Regeln und Verpflichtungen für Daten, die an die Zielplattform gesendet oder von dieser empfangen werden. Sie sind dafür verantwortlich, sich über die Beschränkungen und Verpflichtungen, die mit Ihren Daten einhergehen, sowie über die Verwendung dieser Daten in Adobe Experience Platform und der Zielplattform zu informieren. Adobe Experience Platform bietet Data-Governance-Tools, mit denen Sie einige dieser Datennutzungsverpflichtungen verwalten können. [Weitere Informationen](../../../data-governance/labels/overview.md) über Data Governance-Tools und -Richtlinien.

## Unterstützte Identitäten {#supported-identities}

[!DNL Google Customer Match] unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| `GAID` | GOOGLE ADVERTISING ID | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| `IDFA` | Apple-ID für Werbetreibende | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein IDFA-Namespace ist. |
| `phone_sha256_e.164` | Telefonnummern im E164-Format, gehasht mit dem SHA256-Algorithmus | Es werden sowohl einfache als auch SHA256-Hash-Telefonnummern von Adobe Experience Platform unterstützt. Befolgen Sie die Anweisungen im Abschnitt [ID-](#id-matching-requirements-id-matching-requirements)-Anforderungen“ und verwenden Sie die entsprechenden Namespaces für Nur-Text- bzw. Hash-Telefonnummern. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Experience Platform] die Daten bei Aktivierung automatisch hasht. |
| `email_lc_sha256` | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Es werden sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen von Adobe Experience Platform unterstützt. Befolgen Sie die Anweisungen im Abschnitt [ID-](#id-matching-requirements-id-matching-requirements)-Anforderungen“ und verwenden Sie die entsprechenden Namespaces für Nur-Text- bzw. Hash-E-Mail-Adressen. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Experience Platform] die Daten bei Aktivierung automatisch hasht. |
| `user_id` | Benutzerdefinierte Benutzer-IDs | Wählen Sie diese Zielidentität aus, wenn Ihre Quellidentität ein benutzerdefinierter Namespace ist. |
| `address_info_first_name` | Vorname des Benutzers | Diese Zielidentität soll zusammen mit `address_info_last_name`, `address_info_country_code` und `address_info_postal_code` verwendet werden, wenn Sie Daten zu Postanschriften an Ihr Ziel senden möchten. <br><br>Um sicherzustellen, dass Google mit der Adresse übereinstimmt, müssen Sie alle vier Adressfelder (`address_info_first_name`, `address_info_last_name`, `address_info_country_code` und `address_info_postal_code`) zuordnen und sicherstellen, dass in keinem dieser Felder Daten in den exportierten Profilen fehlen. <br> Wenn ein Feld entweder nicht zugeordnet ist oder fehlende Daten enthält, stimmt Google nicht mit der Adresse überein. |
| `address_info_last_name` | Nachname des Benutzers | Diese Zielidentität soll zusammen mit `address_info_first_name`, `address_info_country_code` und `address_info_postal_code` verwendet werden, wenn Sie Daten zu Postanschriften an Ihr Ziel senden möchten. <br><br>Um sicherzustellen, dass Google mit der Adresse übereinstimmt, müssen Sie alle vier Adressfelder (`address_info_first_name`, `address_info_last_name`, `address_info_country_code` und `address_info_postal_code`) zuordnen und sicherstellen, dass in keinem dieser Felder Daten in den exportierten Profilen fehlen. <br> Wenn ein Feld entweder nicht zugeordnet ist oder fehlende Daten enthält, stimmt Google nicht mit der Adresse überein. |
| `address_info_country_code` | Ländercode der Benutzeradresse | Diese Zielidentität soll zusammen mit `address_info_first_name`, `address_info_last_name` und `address_info_postal_code` verwendet werden, wenn Sie Daten zu Postanschriften an Ihr Ziel senden möchten. <br><br>Um sicherzustellen, dass Google mit der Adresse übereinstimmt, müssen Sie alle vier Adressfelder (`address_info_first_name`, `address_info_last_name`, `address_info_country_code` und `address_info_postal_code`) zuordnen und sicherstellen, dass in keinem dieser Felder Daten in den exportierten Profilen fehlen. <br> Wenn ein Feld entweder nicht zugeordnet ist oder fehlende Daten enthält, stimmt Google nicht mit der Adresse überein. <br><br>Akzeptiertes Format: 2-Buchstaben-Ländercodes in Kleinbuchstaben im [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2)-Format. |
| `address_info_postal_code` | Postleitzahl der Benutzeradresse | Diese Zielidentität soll zusammen mit `address_info_first_name`, `address_info_last_name` und `address_info_country_code` verwendet werden, wenn Sie Daten zu Postanschriften an Ihr Ziel senden möchten. <br><br>Um sicherzustellen, dass Google mit der Adresse übereinstimmt, müssen Sie alle vier Adressfelder (`address_info_first_name`, `address_info_last_name`, `address_info_country_code` und `address_info_postal_code`) zuordnen und sicherstellen, dass in keinem dieser Felder Daten in den exportierten Profilen fehlen. <br> Wenn ein Feld entweder nicht zugeordnet ist oder fehlende Daten enthält, stimmt Google nicht mit der Adresse überein. |

{style="table-layout:auto"}

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
---------|----------|---------|
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (Name, Telefonnummer und sonstiges), die im [!DNL Google Customer Match]-Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Voraussetzungen für [!DNL Google Customer Match] Konto {#google-account-prerequisites}

Bevor Sie ein [!DNL Google Customer Match] Ziel in Experience Platform einrichten, stellen Sie sicher, dass Sie die Richtlinie von Google zur Verwendung von [!DNL Customer Match] lesen und befolgen, die in der [Dokumentation zum Google-Support beschrieben ](https://support.google.com/google-ads/answer/6299717).

Stellen Sie als Nächstes sicher, dass Ihr [!DNL Google]-Konto für eine [!DNL Standard] oder höhere Berechtigungsstufe konfiguriert ist. Weitere Informationen finden Sie in der Dokumentation zu {](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1)}Google Ads .[

### Zulassungsliste {#allowlist}

Bevor Sie das [!DNL Google Customer Match]-Ziel in Experience Platform erstellen, stellen Sie sicher, dass Ihr [!DNL Google Ads]-Konto mit der [[!DNL Google Customer Match] Richtlinie“ ](https://support.google.com/google-ads/answer/6299717/customer-match-policy).

Kunden mit konformen Konten werden automatisch von Google auf die Zulassungsliste gesetzt.

## Anforderungen für den ID-Abgleich {#id-matching-requirements}

[!DNL Google] erfordert, dass keine personenbezogenen Daten (PII) in klarer Form gesendet werden. Daher können die für [!DNL Google Customer Match] aktivierten Zielgruppen als Hash-*(*) verschlüsselt werden, z. B. E-Mail-Adressen oder Telefonnummern.

Je nach Typ der IDs, die Sie in Adobe Experience Platform aufnehmen, müssen Sie die entsprechenden Anforderungen erfüllen.

### Hashing-Anforderungen für Telefonnummern {#phone-number-hashing-requirements}

Es gibt zwei Methoden zum Aktivieren von Telefonnummern in [!DNL Google Customer Match]:

* **Aufnehmen von rohen Telefonnummern**: Sie können rohe Telefonnummern im [!DNL E.164]-Format in [!DNL Experience Platform] aufnehmen, und sie werden bei der Aktivierung automatisch gehasht. Wenn Sie diese Option wählen, stellen Sie sicher, dass Sie immer Ihre unformatierten Telefonnummern in den `Phone_E.164`-Namespace aufnehmen.
* **Aufnehmen von Hash** Telefonnummern: Sie können Ihre Telefonnummern vor der Aufnahme in [!DNL Experience Platform] vorab hashen. Wenn Sie diese Option wählen, stellen Sie sicher, dass Sie immer Ihre gehashten Telefonnummern in den `PHONE_SHA256_E.164`-Namespace aufnehmen.

>[!NOTE]
>
>Telefonnummern, die in den `Phone`-Namespace aufgenommen wurden, können in [!DNL Google Customer Match] nicht aktiviert werden.

### Hash-Anforderungen für E-Mails {#hashing-requirements}

Sie können E-Mail-Adressen hashen, bevor Sie sie in Adobe Experience Platform aufnehmen, oder E-Mail-Adressen in Clear in Experience Platform verwenden und bei der Aktivierung hashen [!DNL Experience Platform].

Weitere Informationen zu den Hash-Anforderungen von Google und anderen Aktivierungsbeschränkungen finden Sie in den folgenden Abschnitten der Dokumentation zu Google:

* [[!DNL Customer Match] mit E-Mail-Adresse, Adresse oder Benutzer-ID](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] Überlegungen](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_considerations)
* [[!DNL Customer Match] mit Telefonnummer](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_phone_number)
* [[!DNL Customer Match] mit IDs für Mobilgeräte](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_mobile_device_ids)


Weitere Informationen zum Aufnehmen von E-Mail-Adressen in Experience Platform finden Sie unter [Übersicht über die Batch](../../../ingestion/batch-ingestion/overview.md)Aufnahme und [Streaming-Aufnahme - Übersicht](../../../ingestion/streaming-ingestion/overview.md).

Wenn Sie sich dafür entscheiden, die E-Mail-Adressen selbst zu hashen, stellen Sie sicher, dass Sie die Anforderungen von Google erfüllen, die in den obigen Links beschrieben werden.

### Hashing-Anforderungen für Felder adressieren {#address-field-hashing}

Beim Zuordnen von adressbezogenen Feldern zu [!DNL Google Customer Match] **Experience Platform die `address_info_first_name`- und `address_info_last_name`-Werte** automatisch hasht, bevor sie an Google gesendet werden. Dieser automatische Hash ist erforderlich, um die Sicherheits- und Datenschutzanforderungen von Google zu erfüllen.

Geben **nicht** vorab gehashte Werte für `address_info_first_name` oder `address_info_last_name` an. Wenn Sie bereits Hash-Werte angeben, schlägt der Abgleichprozess fehl.

### Verwenden benutzerdefinierter Namespaces {#custom-namespaces}

Bevor Sie den `User_ID`-Namespace zum Senden von Daten an Google verwenden können, müssen Sie Ihre eigenen Kennungen mithilfe von [!DNL gTag] synchronisieren. Detaillierte Informationen finden Sie in der offiziellen Dokumentation ](https://support.google.com/google-ads/answer/9199250) [Google .

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Experience Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Experience Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

<!-- ## Configure destination - video walkthrough {#video}

The video below demonstrates the steps to configure a [!DNL Google Customer Match] destination and activate audiences. The steps are also laid out sequentially in the next sections.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng) -->

## Videoüberblick {#video-overview}

Sehen Sie sich das folgende Video an, um eine Erläuterung der Vorteile und der Aktivierung von Daten für den Google-Kundenabgleich zu erhalten.

>[!VIDEO](https://video.tv.adobe.com/v/38180/)

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung mit dem Ziel herzustellen, benötigen Sie **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Geben Sie einen Namen für diese Zielverbindung an
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für diese Zielverbindung an.
* **[!UICONTROL Konto-]**: Ihre [Google Ads-Kunden-ID](https://support.google.com/google-ads/answer/1704344?hl=en). Das Format der ID lautet xxx-xxx-xxxx. Wenn Sie die [!DNL Google Ads Manager Account (My Client Center)] verwenden, verwenden Sie nicht Ihre Manager-Konto-ID. Verwenden Sie stattdessen die [Google Ads](https://support.google.com/google-ads/answer/1704344?hl=en)Kunden-ID.

>[!IMPORTANT]
>
> * Die **[!UICONTROL Mit PII kombinieren]** Marketing-Aktion ist für das [!DNL Google Customer Match] Ziel standardmäßig ausgewählt und kann nicht entfernt werden.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**[Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* an Ziele benötigen Sie die Berechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffssteuerung](/help/access-control/home.md#permissions) <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Streaming-Zielgruppen-Exportziele](../../ui/activate-segment-streaming-destinations.md).

Im Schritt **[!UICONTROL Segmentzeitplan]** müssen Sie die [!UICONTROL App-ID] angeben, wenn Sie [!DNL IDFA] oder [!DNL GAID] Zielgruppen an [!DNL Google Customer Match] senden.

Das Feld &quot;![ID der Google Customer Match App“ wird im Schritt „Segmentplan“ des Aktivierungs-Workflows hervorgehoben.](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

Weitere Informationen zum Auffinden der [!DNL App ID] finden Sie in der [offiziellen Google-Dokumentation](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid) oder wenden Sie sich an Ihren Google-Support-Mitarbeiter.

### Zuordnungsbeispiel: Aktivieren von Zielgruppendaten in [!DNL Google Customer Match] {#example-gcm}

Dies ist ein Beispiel für eine korrekte Identitätszuordnung beim Aktivieren von Zielgruppendaten in [!DNL Google Customer Match].

Auswahl der Quellfelder:

* Wählen Sie den `Email` Namespace als Quellidentität aus, wenn die von Ihnen verwendeten E-Mail-Adressen nicht in einen Hash-Wert umgewandelt werden.
* Wählen Sie den `Email_LC_SHA256`-Namespace als Quellidentität aus, wenn Sie die E-Mail-Adressen von Kunden bei der Datenaufnahme in [!DNL Experience Platform] gemäß den [!DNL Google Customer Match]E[Mail-Hash-Anforderungen](#hashing-requirements) gehasht haben.
* Wählen Sie den `PHONE_E.164`-Namespace als Quellidentität aus, wenn Ihre Daten aus nicht gehashten Telefonnummern bestehen. [!DNL Experience Platform] werden die Telefonnummern hashen, um [!DNL Google Customer Match] Anforderungen zu erfüllen.
* Wählen Sie den `Phone_SHA256_E.164`-Namespace als Quellidentität aus, wenn Sie Telefonnummern bei der Datenaufnahme in [!DNL Experience Platform] gemäß [!DNL Facebook] Anforderungen zum Hashing [ Telefonnummern ](#phone-number-hashing-requirements).
* Wählen Sie den `IDFA` Namespace als Quellidentität aus, wenn Ihre Daten aus [!DNL Apple] Geräte-IDs bestehen.
* Wählen Sie den `GAID` Namespace als Quellidentität aus, wenn Ihre Daten aus [!DNL Android] Geräte-IDs bestehen.
* Wählen Sie den `Custom` Namespace als Quellidentität aus, wenn Ihre Daten aus anderen Kennungstypen bestehen.

Auswählen der Zielfelder:

* Wählen Sie den `Email_LC_SHA256`-Namespace als Zielidentität aus, wenn Ihre Quell-Namespaces entweder `Email` oder `Email_LC_SHA256` sind.
* Wählen Sie den `Phone_SHA256_E.164`-Namespace als Zielidentität aus, wenn Ihre Quell-Namespaces entweder `PHONE_E.164` oder `Phone_SHA256_E.164` sind.
* Wählen Sie die `IDFA` oder `GAID` Namespaces als Zielidentität aus, wenn Ihre Quell-Namespaces `IDFA` oder `GAID` sind.
* Wählen Sie den `User_ID` Namespace als Zielidentität aus, wenn Ihr Quell-Namespace ein benutzerdefinierter Namespace ist.

![Identitätszuordnung zwischen Quell- und Zielfeldern, die im Zuordnungsschritt des Aktivierungs-Workflows angezeigt wird.](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm.png)

Daten aus nicht gehashten Namespaces werden von [!DNL Experience Platform] bei der Aktivierung automatisch gehasht.

Attributquelldaten werden nicht automatisch gehasht. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Umwandlung anwenden]**, damit [!DNL Experience Platform] die Daten bei Aktivierung automatisch hasht.

![hervorgehobenes Steuerelement „Umwandlung anwenden“ im Schritt „Zuordnung“ des Aktivierungs-Workflows.](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm-transformation.png)

## Ziel überwachen {#monitor-destination}

Nachdem Sie eine Verbindung zum Ziel hergestellt und einen Ziel-Datenfluss eingerichtet haben, können Sie die [Überwachungsfunktion](/help/dataflows/ui/monitor-destinations.md) in Real-Time CDP verwenden, um ausführliche Informationen über die Profildatensätze zu erhalten, die in jeder Datenflussausführung für Ihr Ziel aktiviert wurden.

>[!IMPORTANT]
>
>Wenn Sie die vier adressbezogenen Zielidentitäten (`address_info_first_name`, `address_info_last_name`, `address_info_country_code` und `address_info_postal_code`) zuordnen, werden sie für jedes Profil auf der Seite zur Datenflussüberwachung als separate individuelle Identitäten gezählt.

## Überprüfen, ob die Zielgruppenaktivierung erfolgreich war {#verify-activation}

Wechseln Sie nach Abschluss des Aktivierungsflusses zu Ihrem **[!UICONTROL Google Ads]**-Konto. Die aktivierten Zielgruppen werden in Ihrem Google-Konto als Kundenlisten angezeigt. Abhängig von Ihrer Zielgruppengröße werden einige Zielgruppen erst dann gefüllt, wenn mehr als 100 aktive Benutzende bereitgestellt werden.

Beim Zuordnen einer Zielgruppe zu [!DNL IDFA] und [!DNL GAID] mobilen IDs erstellt [!DNL Google Customer Match] für jede ID-Zuordnung eine separate Zielgruppe. Ihr [!DNL Google Ads]-Konto zeigt zwei verschiedene Segmente an: eines für die [!DNL IDFA] und eines für die [!DNL GAID].

## Fehlerbehebung {#troubleshooting}

### Fehlermeldung „400 Fehlerhafte Anfrage“ {#bad-request}

Beim Konfigurieren dieses Ziels wird möglicherweise der folgende Fehler angezeigt:

`{"message":"Google Customer Match Error: OperationAccessDenied.ACTION_NOT_PERMITTED","code":"400 BAD_REQUEST"}`

Dieser Fehler tritt auf, wenn Kundenkonten die [Voraussetzungen](#google-account-prerequisites) nicht erfüllen. Wenden Sie sich zur Behebung dieses Problems an Google und stellen Sie sicher, dass Ihr Konto auf der Zulassungsliste steht und für eine [!DNL Standard] oder höhere Berechtigungsstufe konfiguriert ist. Weitere Informationen finden Sie in der Dokumentation zu {](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1)}Google Ads .[