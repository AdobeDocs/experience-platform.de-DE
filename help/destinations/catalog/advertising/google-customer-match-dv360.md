---
title: Google Customer Match + Display & Video 360-Verbindung
description: Mit dem Ziel-Connector für Google Customer Match + Display & Video 360 können Sie Ihre Online- und Offline-Daten aus Experience Platform verwenden, um Ihre Kundinnen und Kunden in den von Google verwalteten und betriebenen Objekten wie Search, Shopping, Gmail und YouTube zu erreichen und erneut mit ihnen zu interagieren.
badge: Eingeschränkte Verfügbarkeit
exl-id: f6da3eae-bf3f-401a-99a1-2cca9a9058d2
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '2345'
ht-degree: 15%

---

# [!DNL Google Customer Match + Display & Video 360]-Verbindung

>[!NOTE]
>
>**Eingeschränkte Verfügbarkeit des Connectors für Google Customer Match + Display &amp; Video 360**<br> Während wir bei dieser Integration mit Google den gesamten Lebenszyklus der Reife durchlaufen, sehen wir Daten, die auf Schwächen in der Implementierung hinweisen, die korrigiert werden müssen, bevor sie in größerem Umfang angewendet werden können. Angesichts dieser Bedenken hat Adobe die Sichtbarkeit dieses Ziels auf eine begrenzte Anzahl von Kunden reduziert. Wir führen intensive Gespräche mit Google, um das Produkterlebnis zu verbessern. Wir verstehen, dass dies enttäuschende Nachrichten sein können, aber wir glauben, dass es der verantwortliche Ansatz ist, unseren Kunden ein qualitativ hochwertiges, zuverlässiges Erlebnis zu gewährleisten.</br>

Verwenden Sie dieses Ziel, um Ihre PII-basierten [[!DNL Google Customer Match]](https://support.google.com/google-ads/answer/6379332?hl=en)-Listen von Erstanbietern direkt für [!DNL Google Display & Video 360] Eigenschaften wie [!DNL Search], [!DNL YouTube], [!DNL Gmail] und [!DNL Google Display Network] zu aktivieren.

Bestimmte in Google integrierte Drittanbieter wie Adobe Real-Time CDP können die [!DNL Google Audience Partner API] verwenden, um [!DNL Customer Match] Zielgruppen direkt im [!DNL Display & Video 360]-Konto der Kundinnen und Kunden zu erstellen.

Mit der neu eingeführten Funktion, [!DNL Customer Matched] Zielgruppen [!DNL Display & Video 360] nutzen zu können, können Sie jetzt Zielgruppen in einer erweiterten Liste von Inventarquellen ansprechen.

![Ziel von Google Customer Match und DV360 in der Adobe Experience Platform-Benutzeroberfläche.](/help/destinations/assets/catalog/advertising/gcm-dv360/catalog.png)

## Wichtiger Hinweis zu Änderungen an Google-Zielen im Zusammenhang mit aktualisierten Zustimmungsanforderungen in der Europäischen Union

>[!IMPORTANT]
>
> Google veröffentlicht Änderungen an der [Google Ads API](https://developers.google.com/google-ads/api/docs/start), [Customer Match](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) und der [Display &amp; Video 360 API](https://developers.google.com/display-video/api/guides/getting-started/overview), um die Compliance- und Zustimmungsanforderungen zu unterstützen, die im [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA) in der Europäischen Union definiert sind ([EU-Richtlinie zur ](https://www.google.com/about/company/user-consent-policy/)). Die Durchsetzung dieser Änderungen an den Einverständnisanforderungen ist ab dem 6. März 2024 aktiv.
><br/>
>Um die EU-Richtlinie zur Benutzerzustimmung einzuhalten und weiterhin Zielgruppenlisten für Nutzer im Europäischen Wirtschaftsraum (EWR) zu erstellen, müssen Werbetreibende und Partner sicherstellen, dass sie beim Hochladen von Zielgruppendaten die Zustimmung der Endnutzer weitergeben. Als Google-Partner stellt Adobe Ihnen die erforderlichen Tools zur Verfügung, um diese Zustimmungsanforderungen gemäß dem DMA in der Europäischen Union zu erfüllen.
><br/>
>Kunden, die Adobe Systems Privacy &amp; Security Shield erworben und eine [Einwilligungs Regel](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) konfiguriert haben, um Profile ohne Zustimmung herauszufiltern, müssen keine Maßnahmen ergreifen.
><br/>
>Kunden, die Adobe Systems Privacy &amp; Security Shield nicht erworben haben, müssen die [Segment-Definitionsfunktionen](../../../segmentation/home.md#segment-definitions) innerhalb Segment Builder [](../../../segmentation/ui/segment-builder.md) verwenden, um nicht genehmigte Profile herauszufiltern, bestellen die bestehenden Real-Zeit CDP Google Destinations ohne Unterbrechung weiter nutzen zu können.

## Verwendung dieses Ziels

Im Zielkatalog sind mehrere Integrationen mit Google verfügbar, und es kann schwierig sein, zu verstehen, wann die einzelnen verfügbaren Google-Ziele verwendet werden. Machen Sie sich mit den verschiedenen Anwendungsfällen vertraut, indem Sie die Informationen in der folgenden Tabelle lesen:

| [Google-Kundenabgleich](/help/destinations/catalog/advertising/google-customer-match.md) | [Google Display &amp; Video 360](/help/destinations/catalog/advertising/google-dv360.md) | [!DNL Google Customer Match] + [!DNL Display & Video 360] (dieser Konnektor) |
|---------|----------|---------|
| Exportieren Sie Ihre PII-basierten Zielgruppen und erreichen Sie sie auf Warenbestand verfügbar in [!DNL Google Customer Match]. | Erreichen Sie Cookie-basierte Zielgruppen in allen Warenbestand, die über [!DNL Google Display & Video 360], auf Google-eigenen und von Google betriebenen Websites liken Youtube und [!DNL Search]darüber hinaus verfügbar sind. | Erstellen PII-basierte Zielgruppen ein [!DNL Google Customer Match] und erreichen Sie sie auf der Warenbestand verfügbar in [!DNL Google Display & Video 360], die sich ausschließlich in Google-eigenen und -betriebenen Properties befinden. |

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie dieses Ziel verwenden, finden Sie hier einige Beispielanwendungsfälle, die Kundinnen und Kunden von Adobe Experience Platform mit dieser Funktion bewältigen können.

### Anwendungsfall #1

Eine Sportbekleidungsmarke möchte bestehende Kunden über [!DNL Google Search] und [!DNL Google Shopping] erreichen, um Angebote und Artikel basierend auf ihren früheren Käufen und dem Navigationsverlauf zu personalisieren. Die Bekleidungsmarke kann E-Mail-Adressen aus dem eigenen CRM in Experience Platform aufnehmen und Zielgruppen aus eigenen Offline-Daten erstellen. Anschließend können sie diese Zielgruppen an das [!DNL Google Customer Match + Display & Video 360]-Ziel senden, um sie über [!DNL Google Display & Video 360] Eigenschaften wie [!DNL Search], [!DNL YouTube], [!DNL Gmail] und [!DNL Google Display Network] hinweg zu verwenden.

### Anwendungsfall #2

Eine prominente Technologie Firma hat ein neues Telefon auf den Markt gebracht. Um für dieses neue Telefonmodell zu werben, möchten sie Kunden, die frühere Modelle ihrer Telefone besitzen, voranbringen Aufmerksamkeit der neuen Funktionen und Funktionen des Telefons.

Um die Veröffentlichung zu bewerben, Upload sie E-Mail-Adressen aus ihrer CRM-Datenbank in Experience Platform, wobei sie die E-Mail-Adressen als Bezeichner verwenden. Audiences werden basierend auf Kunden erstellt, die ältere Smartphonemodelle besitzen. Anschließend werden Zielgruppen an [!DNL Google Customer Match]gesendet, sodass die Firma aktuelle Kunden, Kunden mit älteren Smartphonemodellen und ähnliche Kunden auf [!DNL Google Display & Video 360] Eigenschaften wie [!DNL Search], [!DNL YouTube], [!DNL Gmail]und die [!DNL Google Display Network]Target-Komponente kann.

## Unterstützte Identitäten {#supported-identities}

[!DNL Google Customer Match] unterstützt die Aktivierung von Identitäten, die in der folgenden Tabelle beschrieben sind. Erhalten Sie weitere Informationen zu [Identitäten](/help/identity-service/features/namespaces.md).

| Ziel-Identität | Beschreibung | Zu beachten |
|---|---|---|
| GAID | Google-Werbe-ID | Wählen Sie die GAID-Zielidentität aus, wenn Ihre Quellidentität ein GAID-Namespace ist. |
| IDFA | Apple-ID für Werbetreibende | Wählen Sie die IDFA-Zielidentität aus, wenn Ihre Quellidentität ein IDFA-Namespace ist. |
| phone_sha256_e.164 | Telefonnummern im E164-Format, gehasht mit dem SHA256-Algorithmus | Es werden sowohl einfache als auch SHA256-Hash-Telefonnummern von Adobe Experience Platform unterstützt. Befolgen Sie die Anweisungen im Abschnitt [ID-](#id-matching-requirements-id-matching-requirements)-Anforderungen“ und verwenden Sie die entsprechenden Namespaces für Nur-Text- bzw. Hash-Telefonnummern. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Apply transformation]** , damit die Daten bei Aktivierung automatisch gehasht [!DNL Experience Platform]. |
| email_lc_sha256 | E-Mail-Adressen, die mit dem SHA-256-Algorithmus gehasht wurden | Es werden sowohl Nur-Text- als auch SHA256-Hash-E-Mail-Adressen von Adobe Experience Platform unterstützt. Befolgen Sie die Anweisungen im Abschnitt [ID-](#id-matching-requirements-id-matching-requirements)-Anforderungen“ und verwenden Sie die entsprechenden Namespaces für Nur-Text- bzw. Hash-E-Mail-Adressen. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Apply transformation]** , damit die Daten bei Aktivierung automatisch gehasht [!DNL Experience Platform]. |

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
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Audience export]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (Name, Telefonnummer und sonstiges), die im [!DNL Google Customer Match]-Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Voraussetzungen für [!DNL Google Customer Match] Konto {#google-account-prerequisites}

Bevor Sie ein [!DNL Google Customer Match] Ziel in Experience Platform einrichten, stellen Sie sicher, dass Sie die Richtlinie von Google zur Verwendung von [!DNL Customer Match] lesen und befolgen, die in der [Dokumentation zum Google-Support beschrieben ](https://support.google.com/google-ads/answer/6299717).

Stellen Sie als Nächstes sicher, dass Ihr [!DNL Google]-Konto für eine [!DNL Standard] oder höhere Berechtigungsstufe konfiguriert ist. Weitere Informationen finden Sie in der [Google Ads-Dokumentation](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&rd=1) .

### Anforderungen an die Kontoverknüpfung {#linking}

Bevor Sie diesen Ziel-Connector konfigurieren, müssen Sie Ihre Google-Konto-ID mit der Google-Konto-ID von Adobe verknüpfen: `4641108541`.

Datenexporte schlagen fehl, wenn Ihr Google-Konto nicht ordnungsgemäß mit der Adobe-Konto-ID verknüpft ist.

>[!NOTE]
>
>Für Kunden, die am Beta-Programm für diesen Connector teilgenommen haben: Adobe hat die Google-Partnerkonto-ID von `6219889373` auf `4641108541` aktualisiert.
>
>**Wenn Sie am Beta-Programm für den Google Customer Match + Display &amp; Video 360-Connector teilgenommen haben und Ihr Google-Konto derzeit mit der alten Adobe-Partnerkonto-ID (`6219889373`) verknüpft ist, führen Sie die folgenden Schritte aus:**
>
>1. Heben Sie die Verknüpfung Ihres Google-Kontos mit der alten Adobe-Partnerkonto-ID auf (`6219889373`)
>2. Verknüpfen Ihres Google-Kontos mit der neuen Adobe-Partnerkonto-ID (`4641108541`)
>3. Entfernen Sie alle Zielgruppen aus Ihren vorhandenen Datenflüssen
>4. Erstellen neuer Datenflüsse und Zuordnen Ihrer Zielgruppen
>
>Wenn Ihr Google-Konto bereits mit der neuen Adobe-Partnerkonto-ID (`4641108541`) verknüpft ist, ist keine Aktion erforderlich, um diesen Connector zu verwenden.

**Für Organisationen mit Manager-Konten:**

Wenn Ihr Unternehmen ein [manager [!DNL Google] account](https://support.google.com/google-ads/answer/6139186) verwendet, um mehrere Client-Konten zu verwalten, befolgen Sie die folgenden spezifischen Verknüpfungsanforderungen:

* **In ein bestimmtes Client-Konto exportieren:** Verknüpfen Sie dieses einzelne Client-Konto (nicht das Manager-Konto) mit der Google-Konto-ID von Adobe: `4641108541`
* **Die Kontoverknüpfung von Manager allein ist nicht ausreichend** und führt zu Fehlern beim Datenexport

### Zulassungsliste {#allowlist}

Bevor Sie das [!DNL Google Customer Match]-Ziel in Experience Platform erstellen, stellen Sie sicher, dass Ihr [!DNL Google Ads]-Konto mit der [[!DNL Google Customer Match] Richtlinie“ ](https://support.google.com/google-ads/answer/6299717/customer-match-policy).

Kunden mit kompatiblen Konten werden automatisch von Google auf die Zulassungsliste gesetzt.

## Anforderungen an den ID-Abgleich {#id-matching-requirements}

[!DNL Google] erfordert, dass keine personenbezogenen Daten unverschlüsselt gesendet werden. Daher müssen die aktivierten Zielgruppen [!DNL Google Customer Match] aus *gehashten* Identifikatoren wie gehashten E-Mail-Adressen oder Telefonnummern stammen.

Abhängig vom Typ der IDs, die Sie in Adobe Experience Platform aufnehmen, müssen Sie die entsprechenden Anforderungen erfüllen.

### Hashing-Anforderungen für Telefonnummern {#phone-number-hashing-requirements}

Es gibt zwei Methoden zum Aktivieren von Telefonnummern in [!DNL Google Customer Match]:

* **Aufnehmen von rohen Telefonnummern**: Sie können rohe Telefonnummern im [!DNL E.164]-Format in [!DNL Experience Platform] aufnehmen, und sie werden bei der Aktivierung automatisch gehasht. Wenn Sie diese Option wählen, stellen Sie sicher, dass Sie immer Ihre unformatierten Telefonnummern in den `Phone_E.164`-Namespace aufnehmen.
* **Aufnehmen von Hash** Telefonnummern: Sie können Ihre Telefonnummern vor der Aufnahme in [!DNL Experience Platform] vorab hashen. Wenn Sie diese Option wählen, stellen Sie sicher, dass Sie immer Ihre gehashten Telefonnummern in den `PHONE_SHA256_E.164`-Namespace aufnehmen.

>[!NOTE]
>
>Telefon in die Namespace aufgenommenen `Phone` Nummern können nicht für das [!DNL Google Customer Match + DV360] Ziel aktiviert werden.

### Hash-Anforderungen für E-Mails {#hashing-requirements}

Sie können E-Mail-Adressen hashen, bevor Sie sie in Adobe Experience Platform aufnehmen, oder E-Mail-Adressen in Clear in Experience Platform verwenden und bei der Aktivierung hashen [!DNL Experience Platform].

Weitere Informationen zu den Hash-Anforderungen von Google und anderen Aktivierungsbeschränkungen finden Sie in den folgenden Abschnitten der Dokumentation zu Google:

* [[!DNL Customer Match] mit E-Mail-Adresse, Adresse oder Benutzer-ID](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] Überlegungen](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_considerations)
* [[!DNL Customer Match] mit Telefonnummer](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_phone_number)
* [[!DNL Customer Match] mit IDs für Mobilgeräte](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_mobile_device_ids)

Weitere Informationen zum Aufnehmen von E-Mail-Adressen in Experience Platform finden Sie unter [Übersicht über die Batch](../../../ingestion/batch-ingestion/overview.md)Aufnahme und [Streaming-Aufnahme - Übersicht](../../../ingestion/streaming-ingestion/overview.md).

Wenn Sie sich dafür entscheiden, die E-Mail-Adressen selbst zu hashen, stellen Sie sicher, dass Sie die Anforderungen von Google erfüllen, die in den obigen Links beschrieben werden.

<!-- ### Using custom namespaces {#custom-namespaces}

Before you can use the `User_ID` namespace to send data to Google, make sure you synchronize your own identifiers using [!DNL gTag]. Refer to the [Google official documentation](https://support.google.com/google-ads/answer/9199250) for detailed information. -->

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Experience Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Experience Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

<!-- ## Configure destination - video walkthrough {#video}

The video below demonstrates the steps to configure a [!DNL Google Customer Match] destination and activate audiences. The steps are also laid out sequentially in the next sections.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng) -->

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_gcm_dv360_accountID"
>title="Verknüpfen von Google- und Adobe-Konten"
>abstract="Stellen Sie sicher, dass die hier eingegebene Google-Konto-ID bereits mit Ihrem Adobe-Konto verknüpft ist. Wenn Sie über ein Google-Manager-Konto mit mehreren Client-Konten verfügen und Daten aus Experience Platform in ein bestimmtes Client-Konto exportieren möchten, müssen Sie dieses Client-Konto mit Ihrem Adobe-Konto verknüpfen und die Account-ID hier eingeben."

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage Destinations]** Zugriffssteuerungsberechtigungen[. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Name]**: Geben Sie einen Namen für diese Zielverbindung an
* **[!UICONTROL Description]**: Geben Sie eine Beschreibung für diese Zielverbindung an
* **[!UICONTROL Account ID]**: Ihre [Google Ads-Kunden-ID](https://support.google.com/google-ads/answer/1704344?hl=en). Das Format der ID lautet xxx-xxx-xxxx. Wenn Sie die [!DNL Google Ads Manager Account (My Client Center)] verwenden, verwenden Sie nicht Ihre Manager-Konto-ID. Verwenden Sie stattdessen die [Google Ads](https://support.google.com/google-ads/answer/1704344?hl=en)Kunden-ID.
* **[!UICONTROL Account type]**: Ihr Google-Kontotyp. Wählen Sie je nach Art Ihres Werbekontos bei Google eine Option aus:
   * **[!UICONTROL Display Video Partner]**
   * **[!UICONTROL Display Video Advertiser]**

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Um *Identitäten* an Ziele zu exportieren, benötigen Sie die **[!UICONTROL View Identity Graph]**[ Zugriffssteuerungsberechtigung](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](../../assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Streaming-Zielgruppen-Exportziele](../../ui/activate-segment-streaming-destinations.md).

<!-- In the **[!UICONTROL Segment schedule]** step, you must provide the [!UICONTROL App ID] when sending [!DNL IDFA] or [!DNL GAID] audiences to [!DNL Google Customer Match].

![Google Customer Match App ID field highlighted in the Segment schedule step of the activation workflow.](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

For details on how to find the [!DNL App ID], refer to the [Google official documentation](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid) or ask your Google representative. -->

### Zuordnungsbeispiel: Aktivieren von Zielgruppendaten in [!DNL Google Customer Match + Display & Video 360] {#example-gcm}

Dies ist ein Beispiel für eine korrekte Identitätszuordnung beim Aktivieren von Zielgruppendaten in [!DNL Google Customer Match + Display & Video 360].

Auswahl der Quellfelder:

* Wählen Sie den `Email` Namespace als Quellidentität aus, wenn die von Ihnen verwendeten E-Mail-Adressen nicht in einen Hash-Wert umgewandelt werden.
* Wählen Sie den `Email_LC_SHA256`-Namespace als Quellidentität aus, wenn Sie die E-Mail-Adressen von Kunden bei der Datenaufnahme in [!DNL Experience Platform] gemäß den [!DNL Google Customer Match]E[Mail-Hash-Anforderungen](#hashing-requirements) gehasht haben.
* Wählen Sie den `PHONE_E.164`-Namespace als Quellidentität aus, wenn Ihre Daten aus nicht gehashten Telefonnummern bestehen. [!DNL Experience Platform] werden die Telefonnummern hashen, um [!DNL Google Customer Match] Anforderungen zu erfüllen.
* Wählen Sie den `Phone_SHA256_E.164`-Namespace als Quellidentität aus, wenn Sie Telefonnummern bei der Datenaufnahme in [!DNL Experience Platform] gemäß [!DNL Facebook] Anforderungen zum Hashing [ Telefonnummern ](#phone-number-hashing-requirements).

Auswählen der Zielfelder:

* Wählen Sie den `Email_LC_SHA256`-Namespace als Zielidentität aus, wenn Ihre Quell-Namespaces entweder `Email` oder `Email_LC_SHA256` sind.
* Wählen Sie den `Phone_SHA256_E.164`-Namespace als Zielidentität aus, wenn Ihre Quell-Namespaces entweder `PHONE_E.164` oder `Phone_SHA256_E.164` sind.

![Identitätszuordnung zwischen Quell- und Zielfeldern, die im Zuordnungsschritt des Aktivierungs-Workflows angezeigt wird.](../../assets/catalog/advertising/google-customer-match-dv360/identity-mapping-gcm-dv360.png)

Daten aus nicht gehashten Namespaces werden von [!DNL Experience Platform] bei der Aktivierung automatisch gehasht.

Attributquelldaten werden nicht automatisch gehasht. Wenn Ihr Quellfeld ungehashte Attribute enthält, überprüfen Sie die Option **[!UICONTROL Apply transformation]** , damit die Daten bei Aktivierung automatisch gehasht [!DNL Experience Platform].

![hervorgehobenes Steuerelement „Umwandlung anwenden“ im Schritt „Zuordnung“ des Aktivierungs-Workflows.](../../assets/catalog/advertising/google-customer-match-dv360/transformation.png)

## Ziel überwachen {#monitor-destination}

Nachdem Sie eine Verbindung zum Ziel hergestellt und einen Ziel-Datenfluss eingerichtet haben, können Sie die [Überwachungsfunktion](/help/dataflows/ui/monitor-destinations.md) in Real-Time CDP verwenden, um ausführliche Informationen über die Profildatensätze zu erhalten, die in jeder Datenflussausführung für Ihr Ziel aktiviert wurden.

Die Überwachungsinformationen für die [!DNL Google Customer Match + Display & Video 360] Verbindung umfassen Informationen auf Zielgruppe-Ebene in Bezug auf aktivierte, ausgeschlossene und fehlgeschlagene Identitäten in jedem Datenfluss und jeder Datenflussausführung. [Lesen Sie mehr](/help/dataflows/ui/monitor-destinations.md#segment-level-view) über die Funktionen.

## Überprüfen, ob Zielgruppe Aktivierung erfolgreich war {#verify-activation}

Wechseln Sie nach Abschluss des Aktivierung Flows zu Ihrem **[!UICONTROL Google Ads]** Konto. Die aktivierten Zielgruppen werden in Ihrer Google-Konto als Kundenlisten angezeigt. Abhängig von Ihrer Zielgruppengröße werden einige Zielgruppen erst dann gefüllt, wenn mehr als 1.000 aktive Benutzende bereitgestellt werden. Weitere Informationen finden Sie in der [Dokumentation zu Google Audience Partner](https://developers.google.com/audience-partner/api/docs/customer-match/get-started#verify-list). Beachten Sie, dass Sie Google um Zugriff auf die Dokumentation im Link bitten müssen.

## Data Governance

Für einige Ziele in Experience Platform gelten bestimmte Regeln und Verpflichtungen für Daten, die an die Zielplattform gesendet oder von dieser empfangen werden. Sie sind dafür verantwortlich, sich über die Beschränkungen und Verpflichtungen, die mit Ihren Daten einhergehen, sowie über die Verwendung dieser Daten in Adobe Experience Platform und der Zielplattform zu informieren. Adobe Experience Platform bietet Data-Governance-Tools, mit denen Sie einige dieser Datennutzungsverpflichtungen verwalten können. [Weitere Informationen](../../../data-governance/labels/overview.md) über Data Governance-Tools und -Richtlinien.

## Fehlerbehebung {#troubleshooting}

### Fehlermeldung „400 Fehlerhafte Anfrage“ {#bad-request}

Beim Konfigurieren dieses Ziels wird möglicherweise der folgende Fehler angezeigt:

`{"message":"Google Customer Match Error: OperationAccessDenied.ACTION_NOT_PERMITTED","code":"400 BAD_REQUEST"}`

Dieser Fehler tritt auf, wenn Kundenkonten die [Voraussetzungen](#google-account-prerequisites) nicht erfüllen. Wenden Sie sich zur Behebung dieses Problems an Google und stellen Sie sicher, dass Ihr Konto auf der Zulassungsliste steht und für eine [!DNL Standard] oder höhere Berechtigungsstufe konfiguriert ist. Weitere Informationen finden Sie in der Dokumentation zu {[}Google Ads .](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&rd=1)
