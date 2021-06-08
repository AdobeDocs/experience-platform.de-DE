---
keywords: Google-Kundenabgleich;Google-Kundenabgleich;Google-Kundenabgleich
title: Google-Kundenabgleich-Verbindung
description: Mit Google-Kundenabgleich können Sie Ihre Online- und Offline-Daten verwenden, um Ihre Kunden über die von Google verwalteten und betriebenen Eigenschaften wie Suche, Shopping, Gmail und YouTube zu erreichen und erneut mit ihnen zu interagieren.
exl-id: 8209b5eb-b05c-4ef7-9fdc-22a528d5f020
source-git-commit: 6c4e68e2f347cadaf3bf36de73c74e1240ed975b
workflow-type: tm+mt
source-wordcount: '1521'
ht-degree: 3%

---

# [!DNL Google Customer Match] connection

## Übersicht {#overview}

[Google-Kundendaten ](https://support.google.com/google-ads/answer/6379332?hl=en) verwenden Sie Ihre Online- und Offline-Daten, um Ihre Kunden über die von Google verwalteten und betriebenen Eigenschaften hinweg zu erreichen und erneut mit ihnen zu interagieren, z. B.:  [!DNL Search],  [!DNL Shopping],  [!DNL Gmail] und  [!DNL YouTube].

![Google-Kundenabgleich-Ziel in der Adobe Experience Platform-Benutzeroberfläche](../../assets/catalog/advertising/google-customer-match/catalog.png)

## Anwendungsbeispiele

Um Ihnen zu helfen, besser zu verstehen, wie und wann das [!DNL Google Customer Match]-Ziel verwendet werden sollte, finden Sie hier Beispielanwendungsfälle, die Adobe Experience Platform-Kunden mit dieser Funktion lösen können.

### Anwendungsfall 1

Eine Marke für Sportbekleidung möchte Bestandskunden über [!DNL Google Search] und [!DNL Google Shopping] erreichen, um Angebote und Artikel auf der Grundlage ihrer früheren Käufe und des Browserverlaufs zu personalisieren. Die Bekleidungsmarke kann E-Mail-Adressen aus ihrem eigenen CRM-System in die Experience Platform aufnehmen und aus ihren eigenen Offline-Daten Segmente erstellen. Anschließend können sie diese Segmente an [!DNL Google Customer Match] senden, um sie über [!DNL Search] und [!DNL Shopping] hinweg zu verwenden und so ihre Werbeausgaben zu optimieren.

### Anwendungsfall 2

Ein renommiertes Technologieunternehmen startete ein neues Telefon. Um dieses neue Telefonmodell zu bewerben, möchten sie Kunden, die Inhaber früherer Modelle ihrer Telefone sind, für die neuen Funktionen des Telefons sensibilisieren.

Um die Veröffentlichung zu bewerben, laden sie E-Mail-Adressen aus ihrer CRM-Datenbank in Experience Platform hoch und verwenden dabei die E-Mail-Adressen als Kennungen. Segmente werden basierend auf Kunden erstellt, die ältere Telefonmodelle besitzen. Anschließend werden Segmente an [!DNL Google Customer Match] gesendet, sodass das Unternehmen aktuelle Kunden, Kunden, die ältere Telefonmodelle besitzen, und ähnliche Kunden mit [!DNL YouTube] ansprechen kann.

## Data Governance für [!DNL Google Customer Match]-Ziele {#data-governance}

Für einige Ziele in der Experience Platform gelten bestimmte Regeln und Pflichten für Daten, die an die Zielplattform gesendet oder von dieser empfangen werden. Sie sind dafür verantwortlich, die Einschränkungen und Pflichten Ihrer Daten zu verstehen und zu verstehen, wie Sie diese Daten in Adobe Experience Platform und der Zielplattform verwenden. Adobe Experience Platform bietet Data Governance-Tools, mit denen Sie einige dieser Datennutzungsverpflichtungen verwalten können. [Erfahren Sie ](../../..//data-governance/labels/overview.md) mehr über Data Governance-Tools und -Richtlinien.

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

## [!DNL Google Customer Match] Kontovoraussetzungen  {#google-account-prerequisites}

Bevor Sie ein [!DNL Google Customer Match]-Ziel in Experience Platform einrichten, sollten Sie die Google-Richtlinien zur Verwendung von [!DNL Customer Match] lesen und einhalten, die in der [Google-Support-Dokumentation](https://support.google.com/google-ads/answer/6299717) beschrieben sind.

### Zulassungsliste {#allowlist}

Bevor Sie das [!DNL Google Customer Match]-Ziel in Experience Platform erstellen, stellen Sie sicher, dass Ihr [!DNL Google Ads]-Konto die [Google-Kundenübereinstimmungsrichtlinie](https://support.google.com/google-ads/answer/6299717/customer-match-policy) erfüllt.

Kunden mit kompatiblen Konten werden von Google automatisch auf die Zulassungsliste gesetzt.

## Anforderungen an die ID-Übereinstimmung {#id-matching-requirements}

[!DNL Google] erfordert, dass keine personenbezogenen Daten (PII) klar übermittelt werden. Daher können die für [!DNL Google Customer Match] aktivierten Zielgruppen von *Hash*-Identifikatoren wie E-Mail-Adressen oder Telefonnummern abgeleitet werden.

Abhängig vom Typ der IDs, die Sie in Adobe Experience Platform erfassen, müssen Sie die entsprechenden Anforderungen erfüllen.

## Anforderungen an das Hashing von Telefonnummern {#phone-number-hashing-requirements}

Es gibt zwei Methoden zum Aktivieren von Telefonnummern in [!DNL Google Customer Match]:

* **Rohe Telefonnummern** erfassen: Sie können rohe Telefonnummern im  [!DNL E.164] Format in aufnehmen und  [!DNL Platform]werden bei Aktivierung automatisch gehasht. Wenn Sie diese Option wählen, achten Sie darauf, Ihre rohen Telefonnummern immer in den Namespace `Phone_E.164` aufzunehmen.
* **Hash-Telefonnummern** erfassen: Sie können Ihre Telefonnummern vorab hash, bevor Sie sie in  [!DNL Platform]aufnehmen. Wenn Sie diese Option wählen, achten Sie darauf, Ihre Hash-Telefonnummern immer in den Namespace `PHONE_SHA256_E.164` aufzunehmen.

>[!NOTE]
>
>Telefonnummern, die in den Namespace `Phone` aufgenommen werden, können in [!DNL Google Customer Match] nicht aktiviert werden.

## Anforderungen an den E-Mail-Hashing {#hashing-requirements}

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

## Ziel konfigurieren - Videoeinführung {#video}

Das folgende Video zeigt die Schritte zum Konfigurieren eines [!DNL Google Customer Match]-Ziels und zum Aktivieren von Segmenten. Die Schritte werden auch nacheinander in den nächsten Abschnitten beschrieben.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

## Mit Ziel verbinden {#connect-destination}

Scrollen Sie in **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]** zur Kategorie **[!UICONTROL Werbung]**. Wählen Sie [!DNL Google Customer Match] und dann **[!UICONTROL Konfigurieren]** aus.

![Verbindung zum Google-Kundenabgleichziel herstellen](../../assets/catalog/advertising/google-customer-match/connect.png)

>[!NOTE]
>
>Wenn eine Verbindung mit diesem Ziel vorhanden ist, können Sie auf der Zielkarte die Schaltfläche **[!UICONTROL Aktivieren]** sehen. Weitere Informationen zum Unterschied zwischen **[!UICONTROL Activate]** und **[!UICONTROL Configure]** finden Sie im Abschnitt [Catalog](../../ui/destinations-workspace.md#catalog) der Dokumentation zum Ziel-Workspace.

Wenn Sie im Schritt **Konto** zuvor eine Verbindung zu Ihrem [!DNL Google Customer Match]-Ziel eingerichtet haben, wählen Sie **[!UICONTROL Vorhandenes Konto]** und wählen Sie Ihre vorhandene Verbindung aus. Sie können auch **[!UICONTROL Neues Konto]** auswählen, um eine neue Verbindung zu [!DNL Google Customer Match] einzurichten. Um sich anzumelden und Adobe Experience Cloud mit Ihrem [!DNL Google Ad]-Konto zu verbinden, wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

>[!NOTE]
>
>Experience Platform unterstützt die Berechtigungsprüfung im Authentifizierungsprozess. Es wird eine Fehlermeldung angezeigt, wenn Sie falsche Anmeldeinformationen in Ihr [!DNL Google Ad]-Konto eingeben, um sicherzustellen, dass Sie den Workflow nicht mit falschen Anmeldeinformationen abschließen.

![Verbindung zum Google-Kundenabgleich-Ziel herstellen - Authentifizierungsschritt](../../assets/catalog/advertising/google-customer-match/connection.png)

Nachdem Ihre Anmeldedaten bestätigt wurden und Adobe Experience Cloud mit Ihrem Google-Konto verbunden ist, können Sie **[!UICONTROL Weiter]** auswählen, um mit dem Schritt **[!UICONTROL Authentifizierung]** fortzufahren.

![Anmeldedaten bestätigt](../../assets/catalog/advertising/google-customer-match/connection-success.png)

Geben Sie im Schritt **[!UICONTROL Authentifizierung]** einen **[!UICONTROL Namen]** und eine **[!UICONTROL Beschreibung]** für Ihren Aktivierungsfluss ein und geben Sie Ihre Google **[!UICONTROL Konto-ID]** ein.

In diesem Schritt können Sie auch beliebige **[!UICONTROL Marketing-Aktionen]** auswählen, die für dieses Ziel gelten. Marketing-Aktionen geben den Intent an, für den die Daten an das Ziel exportiert werden. Sie können aus von der Adobe definierten Marketing-Aktionen auswählen oder eine eigene Marketing-Aktion erstellen. Weitere Informationen zu Marketing-Aktionen finden Sie unter [Datennutzungsrichtlinien - Übersicht](../../../data-governance/policies/overview.md).

Wählen Sie **[!UICONTROL Ziel erstellen]** aus, nachdem Sie die obigen Felder ausgefüllt haben.

>[!IMPORTANT]
>
> * Die Marketing-Aktion **[!UICONTROL Kombinieren mit PII]** ist standardmäßig für das [!DNL Google Customer Match]-Ziel ausgewählt und kann nicht entfernt werden.
> * Für [!DNL Google Customer Match] -Ziele. **[!UICONTROL Kontokennung]** ist Ihre Kunden-ID bei Google. Das Format der ID ist xxx-xxx-xxxx.


![Google-Kundenabgleich verbinden - Authentifizierungsschritt](../../assets/catalog/advertising/google-customer-match/authentication.png)

Ihr Ziel wird jetzt erstellt. Sie können **[!UICONTROL Speichern und beenden]** auswählen, wenn Sie Segmente später aktivieren möchten, oder Sie können **[!UICONTROL Weiter]** wählen, um den Workflow fortzusetzen und Segmente zur Aktivierung auszuwählen. In beiden Fällen sehen Sie sich den nächsten Abschnitt [Aktivieren von Segmenten für  [!DNL Google Customer Match]](#activate-segments) an, in dem der restliche Workflow beschrieben wird.

## Aktivieren von Segmenten für [!DNL Google Customer Match] {#activate-segments}

Anweisungen zum Aktivieren von Segmenten für [!DNL Google Customer Match] finden Sie unter [Daten für Ziele aktivieren](../../ui/activate-destinations.md).


Im Schritt **[!UICONTROL Segment schedule]** müssen Sie die [!UICONTROL App-ID] angeben, wenn Sie [!DNL IDFA]- oder [!DNL GAID]-Segmente an [!DNL Google Customer Match] senden.

![Google-Kundenabgleich-App-ID](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

Weitere Informationen zum Auffinden des [!DNL App ID] finden Sie in der [offiziellen Google-Dokumentation](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid).

## Überprüfen, ob die Segmentaktivierung erfolgreich war {#verify-activation}

Wechseln Sie nach Abschluss des Aktivierungsvorgangs zu Ihrem **[!UICONTROL Google Ads]**-Konto. Die aktivierten Segmente werden in Ihrem Google-Konto als Kundenlisten angezeigt. Beachten Sie, dass je nach Segmentgröße einige Zielgruppen nur dann gefüllt werden, wenn mehr als 100 aktive Benutzer zur Verfügung stehen.

Wenn Sie ein Segment sowohl [!DNL IDFA] als auch [!DNL GAID] mobile IDs zuordnen, erstellt [!DNL Google Customer Match] für jede ID-Zuordnung ein eigenes Segment. Ihr [!DNL Google Ads]-Konto zeigt zwei verschiedene Segmente an, eines für [!DNL IDFA] und eines für das [!DNL GAID]-Mapping.

## Zusätzliche Ressourcen {#additional-resources}

* [Google-Kundenabgleich integrieren - Video-Tutorial](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html)
