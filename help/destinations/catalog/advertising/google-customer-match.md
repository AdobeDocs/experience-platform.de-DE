---
keywords: Google-Kundenübereinstimmungen;Google-Kundenübereinstimmung;Google-Kundenübereinstimmung
title: Google-Kundenabgleich-Verbindung
description: Mit Google Customer Match können Sie Ihre Online- und Offline-Daten verwenden, um Ihre Kunden über die eigenen und betriebenen Eigenschaften wie Search, Shopping, Gmail und YouTube zu erreichen und erneut mit ihnen zu interagieren.
translation-type: tm+mt
source-git-commit: 950dc24e44a32cfd3e0cdde0fee967cb687c572e
workflow-type: tm+mt
source-wordcount: '1608'
ht-degree: 4%

---


# [!DNL Google Customer Match] connection

[Google-Kunden-](https://support.google.com/google-ads/answer/6379332?hl=en) Matchlets verwenden Sie Ihre Online- und Offlinedaten, um Ihre Kunden über die eigenen und betriebenen Eigenschaften von Google zu erreichen und erneut zu kontaktieren, z. B.:  [!DNL Search],  [!DNL Shopping],  [!DNL Gmail]und  [!DNL YouTube].

![Google Customer Match-Ziel in der Adobe Experience Platform-Benutzeroberfläche](../../assets/catalog/advertising/google-customer-match/catalog.png)

## Nutzungsszenarien

Damit Sie besser verstehen können, wie und wann Sie das [!DNL Google Customer Match]-Ziel verwenden sollten, finden Sie hier Beispiele für Anwendungsfälle, die Adobe Experience Platform-Kunden mit dieser Funktion lösen können.

### Verwendungsfall Nr. 1

Eine Sportbekleidungsmarke möchte Bestandskunden über [!DNL Google Search] und [!DNL Google Shopping] erreichen, um Angebot und Artikel auf der Grundlage ihrer bisherigen Käufe und Browsergeschichte zu personalisieren. Die Bekleidungsmarke kann E-Mail-Adressen aus ihrem eigenen CRM-System in die Experience Platform aufnehmen, Segmente aus ihren eigenen Offlinedaten erstellen und diese Segmente an [!DNL Google Customer Match] senden, um sie über [!DNL Search] und [!DNL Shopping] hinweg zu verwenden und so ihre Werbeausgaben zu optimieren.

### Verwendungsfall Nr. 2

Eine prominente Technologie-Firma hat gerade ein neues Handy veröffentlicht. In dem Bemühen, dieses neue Telefonmodell zu fördern, versuchen sie, das Bewusstsein für die neuen Funktionen des Telefons zu fördern, Kunden, die Inhaber früherer Modelle ihrer Telefone.

Um die Veröffentlichung zu bewerben, laden sie E-Mail-Adressen aus ihrer CRM-Datenbank in die Experience Platform hoch und verwenden dabei die E-Mail-Adressen als Bezeichner. Segmente werden basierend auf Kunden erstellt, die ältere Telefonmodelle besitzen und an [!DNL Google Customer Match] gesendet werden, damit sie aktuelle Kunden, Kunden, die ältere Telefonmodelle besitzen, sowie ähnliche Kunden mit [!DNL YouTube] Zielgruppe erhalten.

## Datenverwaltung für [!DNL Google Customer Match]-Ziele {#data-governance}

Die in der Experience Platform befindlichen Ziele können bestimmte Vorschriften und Pflichten für Daten haben, die an die Zielplattform gesendet oder von dieser empfangen werden. Sie sind dafür verantwortlich, die Einschränkungen und Pflichten Ihrer Daten zu verstehen und zu verstehen, wie Sie diese Daten in Adobe Experience Platform und der Zielplattform verwenden. Adobe Experience Platform bietet Tools zur Datenverwaltung, mit denen Sie einige dieser Datenverwendungsverpflichtungen verwalten können. [Erfahren Sie ](../../..//data-governance/labels/overview.md) mehr über Tools und Richtlinien zur Datenverwaltung.

## Unterstützte Identitäten {#supported-identities}

[!DNL Google Customer Match] unterstützt die Aktivierung der Identitäten, die in der folgenden Tabelle beschrieben sind. Erfahren Sie mehr über [identities](/help/identity-service/namespaces.md).

| Zielgruppe | Beschreibung | Zu beachten |
|---|---|---|
| GAID | Google Advertising ID | Wählen Sie diese Zielgruppen-ID aus, wenn Ihre Quellidentität ein GAID-Namensraum ist. |
| IDFA | Apple-ID für Werbetreibende | Wählen Sie diese Zielgruppen-ID aus, wenn Ihre Quellidentität ein IDFA-Namensraum ist. |
| phone_sha256_e.164 | Telefonnummern im Format E164, mit dem SHA256-Algorithmus gehasht | Sowohl Normaltext- als auch SHA256-Hash-Telefonnummern werden von Adobe Experience Platform unterstützt. Befolgen Sie die Anweisungen im Abschnitt [Anforderungen für die ID-Zuordnung](#id-matching-requirements-id-matching-requirements) und verwenden Sie die entsprechenden Namensraum für einfache und hash-Telefonnummern. Wenn Ihr Quellfeld ungehackte Attribute enthält, aktivieren Sie die Option **[!UICONTROL Transformation]** anwenden, damit [!DNL Platform] die Daten bei Aktivierung automatisch hash. |
| email_lc_sha256 | Mit dem SHA256-Algorithmus verfasste E-Mail-Adressen | Sowohl einfache als auch SHA256-Hash-E-Mail-Adressen werden von Adobe Experience Platform unterstützt. Befolgen Sie die Anweisungen im Abschnitt [Anforderungen für die ID-Zuordnung](#id-matching-requirements-id-matching-requirements) und verwenden Sie die entsprechenden Namensraum für E-Mail-Adressen mit Standardtext bzw. Hash-E-Mail-Adressen. Wenn Ihr Quellfeld ungehackte Attribute enthält, aktivieren Sie die Option **[!UICONTROL Transformation]** anwenden, damit [!DNL Platform] die Daten bei Aktivierung automatisch hash. |
| user_id | Benutzerdefinierte Benutzer-IDs | Wählen Sie diese Zielgruppen-ID aus, wenn Ihre Quellidentität ein benutzerdefinierter Namensraum ist. |

## Exporttyp {#export-type}

**Segmentexport** : Sie exportieren alle Segmentmitglieder (Audience) mit den Bezeichnern (Name, Telefonnummer usw.) wird im [!DNL Google Customer Match]-Ziel verwendet.

## [!DNL Google Customer Match] Kontovoraussetzungen  {#google-account-prerequisites}

Bevor Sie ein [!DNL Google Customer Match]-Ziel in der Experience Platform einrichten, sollten Sie die Google-Richtlinien für die Verwendung von [!DNL Customer Match] lesen und beachten, die in der [Google-Supportdokumentation](https://support.google.com/google-ads/answer/6299717) beschrieben sind.

### Zulassungsliste {#allowlist}

>[!NOTE]
>
>Es ist obligatorisch, der Google-Zulassungsliste hinzugefügt zu werden, bevor Sie Ihr erstes [!DNL Google Customer Match]-Ziel in der Experience Platform einrichten. Vergewissern Sie sich bitte, dass der unten beschriebene Vorgang der Zulassungsliste von Google abgeschlossen wurde, bevor Sie ein Ziel erstellen.

Bevor Sie das [!DNL Google Customer Match]-Ziel in der Experience Platform erstellen, müssen Sie sich an Google wenden und den Anweisungen zur Zulassungsliste unter [Verwenden Sie die Kundenabstimmungspartner, um Ihre Daten](https://support.google.com/google-ads/answer/7361372?hl=en&amp;ref_topic=6296507) in der Google-Dokumentation hochzuladen.

Darüber hinaus gibt es eine zweite Google-Zulassungsliste, der Sie Ihr Konto hinzufügen müssen, wenn Sie planen, Daten mit der Google [User_ID](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id) hochzuladen. Wenden Sie sich an Ihren Google-Kundenbetreuer, um sicherzustellen, dass Sie zu den Zulassungslisten hinzugefügt werden.

### Anforderungen für die ID-Übereinstimmung {#id-matching-requirements}

[!DNL Google] verlangt, dass keine personenbezogenen Daten (PII) klar übermittelt werden. Daher können die für [!DNL Google Customer Match] aktivierten Audiencen anhand von *Hash*-IDs wie E-Mail-Adressen oder Telefonnummern ausgewertet werden.

Abhängig von der Art der IDs, die Sie in Adobe Experience Platform eingeben, müssen Sie die entsprechenden Anforderungen erfüllen.

#### Hashanforderungen für Telefonnummern {#phone-number-hashing-requirements}

Es gibt zwei Methoden zum Aktivieren von Telefonnummern in [!DNL Google Customer Match]:

* **Rohe Telefonnummern** eingehen: Sie können rohe Telefonnummern im  [!DNL E.164] Format in  [!DNL Platform]aufnehmen, die bei der Aktivierung automatisch mit Hashing versehen werden. Wenn Sie diese Option wählen, achten Sie darauf, Ihre rohen Telefonnummern immer in den `Phone_E.164`-Namensraum einzugeben.
* **Hash-Telefonnummern** eingehen: Sie können Ihre Telefonnummern vorab hash, bevor Sie  [!DNL Platform]einsteigen. Wenn Sie diese Option wählen, vergewissern Sie sich, dass Sie stets Ihre Hash-Telefonnummern in den `PHONE_SHA256_E.164`-Namensraum eingeben.

>[!NOTE]
>
>Telefonnummern, die in den `Phone`-Namensraum aufgenommen werden, können in [!DNL Google Customer Match] nicht aktiviert werden.

#### Anforderungen für das E-Mail-Hashing {#hashing-requirements}

Sie können E-Mail-Adressen vor der Einbindung in Adobe Experience Platform als Hash-E-Mail-Adressen festlegen oder Sie können in Experience Platform mit E-Mail-Adressen arbeiten und sie von unserem Algorithmus auf Aktivierung hash lassen.

Weitere Informationen zu den Hashing-Anforderungen von Google und anderen Einschränkungen der Aktivierung finden Sie in den folgenden Abschnitten der Google-Dokumentation:

* [[!DNL Customer Match] mit E-Mail-Adresse, -Adresse oder -Benutzer-ID](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] Überlegungen](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_considerations)
* [Kundenabgleich mit Telefonnummer](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_phone_number)
* [Kunden-Übereinstimmung mit Mobilgerät-IDs](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_mobile_device_ids)


Weitere Informationen zum Eingeben von E-Mail-Adressen in Experience Platformen finden Sie unter [Überblick über die Stapelverarbeitung](../../../ingestion/batch-ingestion/overview.md) und [Übersicht über die Streaming-Erfassung](../../../ingestion/streaming-ingestion/overview.md).

Wenn Sie sich dafür entscheiden, die E-Mail-Adressen selbst zu hash, stellen Sie sicher, dass die Anforderungen von Google, wie in den Links oben beschrieben.

#### Verwenden benutzerdefinierter Namensraum {#custom-namespaces}

Bevor Sie den Namensraum `User_ID` verwenden können, um Daten an Google zu senden, müssen Sie sicherstellen, dass Sie Ihre eigenen IDs mit [!DNL gTag] synchronisieren. Ausführliche Informationen finden Sie in der [offiziellen Google-Dokumentation](https://support.google.com/google-ads/answer/9199250).

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

## Mit Ziel verbinden {#connect-destination}

Führen Sie in **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]** einen Bildlauf zur Kategorie **[!UICONTROL Werbung]** durch. Wählen Sie [!DNL Google Customer Match] und dann **[!UICONTROL Konfigurieren]**.

![Verbindung zum Google-Kunden-Übereinstimmungsziel herstellen](../../assets/catalog/advertising/google-customer-match/connect.png)

>[!NOTE]
>
>Wenn bereits eine Verbindung zu diesem Ziel besteht, wird auf der Zielkarte die Schaltfläche **[!UICONTROL Aktivieren]** angezeigt. Weitere Informationen zum Unterschied zwischen **[!UICONTROL Aktivieren]** und **[!UICONTROL Konfigurieren]** finden Sie im Abschnitt [Katalog](../../ui/destinations-workspace.md#catalog) der Dokumentation zum Zielarbeitsbereich.

Wenn Sie im Schritt **Konto** zuvor eine Verbindung zu Ihrem [!DNL Google Customer Match]-Ziel eingerichtet haben, wählen Sie **[!UICONTROL Vorhandenes Konto]** und wählen Sie Ihre bestehende Verbindung aus. Sie können auch **[!UICONTROL Neues Konto]** auswählen, um eine neue Verbindung zu [!DNL Google Customer Match] einzurichten. Wählen Sie **[!UICONTROL Mit Ziel]** verbinden, um sich anzumelden und Adobe Experience Cloud mit Ihrem [!DNL Google Ad]-Konto zu verbinden.

>[!NOTE]
>
>Experience Platform unterstützt die Berechtigungsüberprüfung im Authentifizierungsprozess und zeigt eine Fehlermeldung an, wenn Sie falsche Berechtigungen in Ihr [!DNL Google Ad]-Konto eingeben. Dadurch wird sichergestellt, dass Sie den Workflow nicht mit falschen Anmeldedaten ausführen.

![Verbindung zum Google-Kundenübereinstimmungsziel herstellen - Authentifizierungsschritt](../../assets/catalog/advertising/google-customer-match/connection.png)

Nachdem Sie Ihre Anmeldedaten bestätigt haben und Adobe Experience Cloud mit Ihrem Google-Konto verbunden ist, können Sie **[!UICONTROL Weiter]** auswählen, um mit dem Schritt **[!UICONTROL Authentifizierung]** fortzufahren.

![Anmeldedaten bestätigt](../../assets/catalog/advertising/google-customer-match/connection-success.png)

Geben Sie im Schritt **[!UICONTROL Authentication]** einen **[!UICONTROL und einen**[!UICONTROL  Description ]**für Ihre Aktivierung ein und füllen Sie die Google**[!UICONTROL  Konto-ID ]**aus.]**

In diesem Schritt können Sie auch alle **[!UICONTROL Marketingaktionen]** auswählen, die für dieses Ziel gelten sollen. Marketingaktionen geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von der Adobe definierten Marketingaktionen auswählen oder eine eigene Marketingaktion erstellen. Weitere Informationen zu Marketingaktionen finden Sie unter [Übersicht über Datenverwendungsrichtlinien](../../../data-governance/policies/overview.md).

Wählen Sie **[!UICONTROL Ziel erstellen]** aus, nachdem Sie die obigen Felder ausgefüllt haben.

>[!IMPORTANT]
>
> * Die Marketingaktion **[!UICONTROL Mit PII]** kombinieren ist standardmäßig für das [!DNL Google Customer Match]-Ziel ausgewählt und kann nicht entfernt werden.
> * Für [!DNL Google Customer Match]-Ziele. **[!UICONTROL Die Konto-]** ID ist Ihre Kunden-Client-ID bei Google. Das Format der ID ist xxx-xxx-xxxx.


![Google-Kundenabgleich - Authentifizierungsschritt](../../assets/catalog/advertising/google-customer-match/authentication.png)

Ihr Ziel wird jetzt erstellt. Sie können **[!UICONTROL Speichern und beenden]** auswählen, wenn Sie Segmente später aktivieren möchten, oder Sie können **[!UICONTROL Weiter]** wählen, um den Workflow fortzusetzen und Segmente zur Aktivierung auszuwählen. In beiden Fällen finden Sie im nächsten Abschnitt [Aktivieren von Segmenten nach [!DNL Google Customer Match]](#activate-segments) Informationen zum Rest des Workflows.

## Aktivieren von Segmenten nach [!DNL Google Customer Match] {#activate-segments}

Anweisungen zum Aktivieren von Segmenten in [!DNL Google Customer Match] finden Sie unter [Daten in Ziele aktivieren](../../ui/activate-destinations.md).


Im Schritt **[!UICONTROL Segmentplan]** müssen Sie die [!UICONTROL App-ID] angeben, wenn Sie [!DNL IDFA]- oder [!DNL GAID]-Segmente an [!DNL Google Customer Match] senden.

![Google Customer Match-App-ID](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

Weitere Informationen zum Suchen der [!DNL App ID] finden Sie in der [offiziellen Google-Dokumentation](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid).







<!-- 
To activate segments to [!DNL Google Customer Match], follow the steps below: 

In **[!UICONTROL Destinations > Browse]**, select the [!DNL Google Customer Match] destination where you want to activate your segments.

Click the name of the destination. This takes you to the Activate flow.

![activate-flow](../../assets/catalog/advertising/google-customer-match/activate-flow.png)

Note that if an activation flow already exists for a destination, you can see the segments that are currently being sent to the destination. Select **[!UICONTROL Edit activation]** in the right rail and follow the steps below to modify the activation details.

Select **[!UICONTROL Activate]**. In the **[!UICONTROL Activate destination]** workflow, on the **[!UICONTROL Select Segments]** page, select which segments to send to [!DNL Google Customer Match].

![segments-to-destination](../../assets/catalog/advertising/google-customer-match/activate-segments.png)

In the **[!UICONTROL Identity mapping]** step, select which attributes to be included as an identity in this destination. Select **[!UICONTROL Add new mapping]** and browse your schema, select email and/or hashed email, and map them to the corresponding target identity.

![identity mapping initial screen](../../assets/catalog/advertising/google-customer-match/identity-mapping.png) 

**Plain text email address as primary identity**: If you have plain text (unhashed) email addresses as primary identity in your schema, select the email field in your **[!UICONTROL Source Attributes]** and map to the Email field in the right column under **[!UICONTROL Target Identities]**, as shown below:

![select plain text emails identity](../../assets/catalog/advertising/google-customer-match/raw-email.gif) 

**Hashed email address as primary identity**: If you have hashed email addresses as primary identity in your schema, select the hashed email field in your **[!UICONTROL Source Attributes]** and map to the Email_LC_SHA256 field in the right column under **[!UICONTROL Target Identities]**, as shown below:

![select hashed emails identity](../../assets/catalog/advertising/google-customer-match/hashed-emails.gif)

On the **[!UICONTROL Segment schedule]** page, you can set the start date for sending data to the destination.

On the **[!UICONTROL Review]** page, you can see a summary of your selection. Select **[!UICONTROL Cancel]** to break up the flow, **[!UICONTROL Back]** to modify your settings, or **[!UICONTROL Finish]** to confirm your selection and start sending data to the destination.

>[!IMPORTANT]
>
>In this step, Real-time CDP checks for data usage policy violations. Shown below is an example where a policy is violated. You cannot complete the segment activation workflow until you have resolved the violation. For information on how to resolve policy violations, see [Policy enforcement](../../../rtcdp/privacy/data-governance-overview.md#enforcement) in the data governance documentation section.
 
![confirm-selection](../../assets/common/data-policy-violation.png)

If no policy violations have been detected, select **[!UICONTROL Finish]** to confirm your selection and start sending data to the destination.

![confirm-selection](../../assets/catalog/advertising/google-customer-match/review.png) -->

## Überprüfen, ob die Segmentaktivierung erfolgreich war {#verify-activation}

Wechseln Sie nach Abschluss der Aktivierung zu Ihrem **[!UICONTROL Google Ads]**-Konto. Die aktivierten Segmente werden jetzt in Ihrem Google-Konto als Listen angezeigt. Beachten Sie, dass je nach Segmentgröße einige Audiencen nur dann gefüllt werden, wenn mehr als 100 aktive Benutzer zur Verfügung stehen.

Wenn Sie ein Segment sowohl mit [!DNL IDFA]- als auch mit [!DNL GAID]-Mobil-IDs verknüpfen, erstellt [!DNL Google Customer Match] für jede ID-Zuordnung ein separates Segment. Ihr [!DNL Google Ads]-Konto zeigt zwei verschiedene Segmente an, eines für das [!DNL IDFA]-Segment und eines für die [!DNL GAID]-Zuordnung.

## Zusätzliche Ressourcen {#additional-resources}

* [Google-Kundenabgleich integrieren - Video-Lernprogramm](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html)