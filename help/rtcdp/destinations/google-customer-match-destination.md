---
title: Google-Kundenübereinstimmungsziel
seo-title: Google Customer Match Destination
description: Google Customer Match lets you use your online and offline data to reach and re-engage with your customers across Google's owned and operated properties, such as Search, Shopping, Gmail, and YouTube.
seo-description: Google Customer Match lets you use your online and offline data to reach and re-engage with your customers across Google's owned and operated properties, such as Search, Shopping, Gmail, and YouTube.
translation-type: tm+mt
source-git-commit: 31eb03c6625f820c9729caf5181c56e748e853a5
workflow-type: tm+mt
source-wordcount: '1482'
ht-degree: 11%

---


# Google-Kundenübereinstimmungsziel

## Übersicht {#overview}

[Mit der Google-Kundenübereinstimmung](https://support.google.com/google-ads/answer/6379332?hl=en) können Sie Ihre Online- und Offlinedaten verwenden, um Ihre Kunden über die eigenen und betriebenen Eigenschaften von Google zu erreichen und erneut zu kontaktieren, z. B.: [!DNL Search], [!DNL Shopping], [!DNL Gmail]und [!DNL YouTube].

![Google Customer Match-Ziel in der CDP-Benutzeroberfläche in Echtzeit](/help/rtcdp/destinations/assets/google-customer-match-catalog.png)

## Nutzungsszenarien

Damit Sie besser verstehen können, wie und wann Sie das [!DNL Google Customer Match] Ziel verwenden sollten, finden Sie hier einige Verwendungsbeispiele, die Kunden der Adobe Echtzeit-Kundendatenplattform mit dieser Funktion lösen können.


### Verwendungsfall Nr. 1

Eine Sportbekleidungsmarke möchte Bestandskunden erreichen [!DNL Google Search] und Angebot und Artikel anhand ihrer bisherigen Käufe und Browsergeschichte personalisieren [!DNL Google Shopping] und personalisieren. Die Bekleidungsmarke kann E-Mail-Adressen von ihrem eigenen CRM zur Adobe von CDP in Echtzeit erfassen, Segmente aus ihren eigenen Offlinedaten erstellen und diese Segmente senden, um [!DNL Google Customer Match] zur Verwendung über [!DNL Search] und [!DNL Shopping]Optimierung ihrer Werbeausgaben verwendet zu werden.

### Verwendungsfall Nr. 2

A prominent technology company has just released a new phone. In an effort to promote this new phone model, they are looking to drive awareness of the new features and functionality of the phone to customers who own previous models of their phones.

To promote the release, they upload email addresses from their CRM database into Adobe Real-time CDP, using the email addresses as identifiers. Segments are created based on customers who own older phone models and sent to [!DNL Google Customer Match] so that they can target current customers, customers who own older phone models, as well as similar customers on [!DNL YouTube].

## Datenverwaltung für [!DNL Google Customer Match] Ziele {#data-governance}

Die Ziele in Adobe Echtzeit-CDP können bestimmte Regeln und Pflichten für Daten haben, die an die Zielplattform gesendet oder von dieser empfangen werden. Sie sind dafür verantwortlich, die Einschränkungen und Pflichten Ihrer Daten zu verstehen und zu verstehen, wie Sie diese Daten in Adobe Experience Platform und der Zielplattform verwenden. Adobe Experience Platform bietet Tools zur Datenverwaltung, mit denen Sie einige dieser Datenverwendungsverpflichtungen verwalten können. [Learn more](/help/data-governance/labels/overview.md) about data governance tools and policies.

## Art und Identität der Aktivierung {#activation-type}

**Segmentexport** : Sie exportieren alle Segmentmitglieder (Audience) mit den Bezeichnern (Name, Telefonnummer usw.) used in the [!DNL Google Customer Match] destination.

**Identitäten** - Sie können rohe oder hash-E-Mails als Kunden-IDs in Google verwenden

## [!DNL Google Customer Match] Kontovoraussetzungen {#google-account-prerequisites}

Before setting up a [!DNL Google Customer Match] destination in Adobe Real-time CDP, make sure you read and adhere to Google&#39;s policy for using [!DNL Customer Match], outlined in the [Google support documentation](https://support.google.com/google-ads/answer/6299717).

### Zulassungsliste {#allowlist}

>[!NOTE]
>
>Es ist obligatorisch, zur Zulassungsliste von Google hinzugefügt zu werden, bevor Sie Ihr erstes [!DNL Google Customer Match] Ziel in Adobe Echtzeit CDP einrichten. Vergewissern Sie sich bitte, dass der unten beschriebene Vorgang der Zulassungsliste von Google abgeschlossen wurde, bevor Sie ein Ziel erstellen.

Bevor Sie das [!DNL Google Customer Match] Ziel in Adobe CDP in Echtzeit erstellen, müssen Sie sich an Google wenden und den Anweisungen zur Zulassungsliste unter Kunden-Match-Partner [verwenden folgen, um Ihre Daten](https://support.google.com/google-ads/answer/7361372?hl=en&amp;ref_topic=6296507) in der Google-Dokumentation hochzuladen.


### Email hashing requirements {#hashing-requirements}

<!--

>[!IMPORTANT]
>
> When using mobile device IDs as identifiers, an AppId must be provided in the activation flow. For more information, see step 6 in the [Activate segments](#activate-segments) section of this page.

-->

Google verlangt, dass keine personenbezogenen Daten (PII) klar gesendet werden. Daher [!DNL Google Customer Match] müssen die aktivierten Audiencen von *Hash* -E-Mail-Adressen abgekoppelt werden. Sie können E-Mail-Adressen vor der Einbindung in Adobe Experience Platform als Hash-E-Mail-Adressen festlegen oder Sie können in Experience Platform mit E-Mail-Adressen arbeiten und sie von unserem Algorithmus auf Aktivierung hash lassen.

Weitere Informationen zu den Hashing-Anforderungen von Google und anderen Einschränkungen der Aktivierung finden Sie in den folgenden Abschnitten der Google-Dokumentation:

* [[!DNL Customer Match] mit E-Mail-Adresse, -Adresse oder -Benutzer-ID](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] Überlegungen](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_considerations)

<!--

Links to be added when activation based on phone number and device IDs becomes available.

* [Customer Match with phone number](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_phone_number)
* [Customer Match with mobile device IDs](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_mobile_device_ids)

-->

Weitere Informationen zum Eingeben von E-Mail-Adressen in der Experience Platform finden Sie in der Übersicht über die [Stapelverarbeitung](/help/ingestion/batch-ingestion/overview.md) und in der Übersicht über die [Erfassung](/help/ingestion/streaming-ingestion/overview.md)des Streamings.

Wenn Sie sich dafür entscheiden, die E-Mail-Adressen selbst zu hash, stellen Sie sicher, dass die Anforderungen von Google, wie in den Links oben beschrieben.


>[!IMPORTANT]
>
>Wenn Sie sich dafür entscheiden, keine E-Mail-Adressen zu hash, wird dies von Adobe Echtzeit-CDP für Sie ausgeführt, wenn Sie Segmente aktivieren für [!DNL Google Customer Match]. Wählen Sie im Arbeitsablauf für die [Aktivierung](/help/rtcdp/destinations/google-customer-match-destination.md#activate-segments) (siehe Schritt 5) die `Email` Option wie unten für *E-Mail-Adressen* und `Email_LC_SHA256` für *Hash-E-Mail-Adressen* dargestellt.


![Hashing bei der Aktivierung](/help/rtcdp/destinations/assets/identity-mapping.png)

## Mit Ziel verbinden {#connect-destination}

1. Blättern Sie unter **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]** zur **[!UICONTROL Advertising]** -Kategorie. Wählen Sie [!DNL Google Customer Match]und dann **[!UICONTROL Konfigurieren]**.

   ![Verbindung zum Google-Kunden-Übereinstimmungsziel herstellen](/help/rtcdp/destinations/assets/connect-google-customer-match.png)

2. In the **Account** step, if you had previously set up a connection to your [!DNL Google Customer Match] destination, select **[!UICONTROL Existing Account]** and select your existing connection. Or, you can select **[!UICONTROL New Account]** to set up a new connection to [!DNL Google Customer Match]. Select **[!UICONTROL Connect to destination]** to log in and connect Adobe Experience Cloud to your [!DNL Google Ad] account.

   >[!NOTE]
   >
   >Adobe Real-time CDP supports credentials validation in the authentication process and displays an error message if you input incorrect credentials to your [!DNL Google Ad] account. Dadurch wird sichergestellt, dass Sie den Workflow nicht mit falschen Anmeldedaten ausführen.

   ![Verbindung zum Google-Kundenübereinstimmungsziel herstellen - Authentifizierungsschritt](/help/rtcdp/destinations/assets/google-customer-match-pre-connect-view.png)

3. Once your credentials are confirmed and Adobe Experience Cloud is connected to your Google account, you can select **[!UICONTROL Next]** to proceed to the **[!UICONTROL Setup]** step.

   ![Anmeldedaten bestätigt](/help/rtcdp/destinations/assets/google-customer-match-connection-success.png)

4. Geben Sie im Schritt **[!UICONTROL Authentifizierung]** einen **[!UICONTROL Namen]** und eine **[!UICONTROL Beschreibung]** für die Aktivierung ein und füllen Sie Google die **[!UICONTROL Konto-ID]** aus. <br> In diesem Schritt können Sie auch einen beliebigen **[!UICONTROL Marketing-Anwendungsfall]** auswählen, der für dieses Ziel gelten soll. Anwendungsfälle für das Marketing geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von der Adobe definierten Anwendungsfällen für das Marketing auswählen oder einen eigenen Anwendungsfall für das Marketing erstellen. For more information about marketing use cases, see the [Data Governance in Real-time CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) page. Informationen zu den einzelnen Anwendungsfällen für Marketingzwecke, die von der Adobe definiert wurden, finden Sie in der Übersicht über [Datenverwendungsrichtlinien](/help/data-governance/policies/overview.md#core-actions). <br> Wählen Sie **[!UICONTROL Ziel erstellen]** aus, nachdem Sie die obigen Felder ausgefüllt haben.

   >[!IMPORTANT]
   >
   > Für [!DNL Google Customer Match] Ziele. **[!UICONTROL Account ID]** is your customer client ID with Google. Das Format der ID ist xxx-xxx-xxxx.

   ![Google-Kundenabgleich - Authentifizierungsschritt](/help/rtcdp/destinations/assets/google-customer-match-authentication-step.png)

5. Ihr Ziel wird jetzt erstellt. Sie können **[!UICONTROL Speichern und beenden]** auswählen, wenn Sie Segmente später aktivieren möchten, oder Sie können **[!UICONTROL Weiter]** wählen, um den Workflow fortzusetzen und Segmente zur Aktivierung auszuwählen. In either case, see the next section, [Activate segments to [!DNL Google Customer Match]](#activate-segments), for the rest of the workflow.


## Activate segments to [!DNL Google Customer Match] {#activate-segments}

Gehen Sie wie folgt vor, um Segmente zu aktivieren [!DNL Google Customer Match]:

1. Wählen Sie unter **[!UICONTROL Ziele > Durchsuchen]** das Ziel aus, an dem Sie Ihre Segmente aktivieren möchten.[!DNL Google Customer Match]
2. Klicken Sie auf den Namen des Ziels. So gelangen Sie zum Aktivierungsfluss.
   ![Aktivierungsfluss](/help/rtcdp/destinations/assets/google-customer-match-activate-flow.png)
Beachten Sie, dass sich, wenn für ein Ziel bereits ein Aktivierungsfluss vorhanden ist, die Segmente anzeigen lassen, die derzeit an das Ziel gesendet werden. Wählen Sie in der rechten Leiste die Option **[!UICONTROL Aktivierung bearbeiten]** und führen Sie die unten beschriebenen Schritte aus, um die Aktivierungsdetails zu ändern.
3. Wählen Sie **[!UICONTROL Aktivieren]**.
4. In the **[!UICONTROL Activate destination]** workflow, on the **[!UICONTROL Select Segments]** page, select which segments to send to [!DNL Google Customer Match].
   ![Segment an Ziel](/help/rtcdp/destinations/assets/activate-segments-google-customer-match.png)
5. Wählen Sie im Schritt **[!UICONTROL Identitätszuordnung]** aus, welche Attribute als Identität in dieses Ziel aufgenommen werden sollen. Wählen Sie **[!UICONTROL Hinzufügen neue Zuordnung]** aus und durchsuchen Sie Ihr Schema, wählen Sie E-Mail- und/oder Hash-E-Mail und ordnen Sie sie der entsprechenden Zielgruppen-ID zu.
   ![Anfangsbildschirm zur Identitätszuordnung](/help/rtcdp/destinations/assets/gcm-identity-mapping.png) <br> 
   *Einfache Text-E-Mail-Adresse als primäre Identität*: Wenn Sie in Ihrem Schema als primäre Identität Nur-Text-E-Mail-Adressen (ohne Hashing) verwenden, wählen Sie das E-Mail-Feld in Ihren **[!UICONTROL Quellattributen]** aus und ordnen Sie es wie unten gezeigt in der rechten Spalte unter &quot; **[!UICONTROL Zielgruppen-IDs]**&quot;dem Feld &quot;E-Mail&quot;zu:
   ![E-Mail-Identität für einfachen Text auswählen](/help/rtcdp/destinations/assets/gcm-raw-email.gif) <br> 
   *Hashed email address as primary identity*: If you have hashed email addresses as primary identity in your schema, select the hashed email field in your **[!UICONTROL Source Attributes]** and map to the Email_LC_SHA256 field in the right column under **[!UICONTROL Target Identities]**, as shown below:
   ![select hashed emails identity](/help/rtcdp/destinations/assets/gcm-hashed-emails.gif) <br> 
6. Auf der Seite &quot; **[!UICONTROL Segmentplan]** &quot;können Sie das Datum des Beginns für das Senden der Daten an das Ziel festlegen.
7. Auf der Seite **[!UICONTROL Überprüfen]** können Sie eine Zusammenfassung Ihrer Auswahl sehen. Wählen Sie **[!UICONTROL Abbrechen]**, um den Fluss abzubrechen, **[!UICONTROL Zurück]**, um die Einstellungen zu ändern, oder **[!UICONTROL Fertig stellen]**, um Ihre Auswahl zu bestätigen und mit dem Senden von Daten an das Ziel zu beginnen.

>[!IMPORTANT]
>
>In this step, Real-time CDP checks for data usage policy violations. Shown below is an example where a policy is violated. You cannot complete the segment activation workflow until you have resolved the violation. Informationen zum Beheben von Richtlinienverletzungen finden Sie unter [Richtliniendurchsetzung](/help/rtcdp/privacy/data-governance-overview.md#enforcement) im Abschnitt zur Datenverwaltung.

![Auswahl bestätigen](/help/rtcdp/destinations/assets/data-policy-violation.png)

Wenn keine Richtlinienverletzungen festgestellt wurden, wählen Sie **[!UICONTROL Fertig stellen]** , um Ihre Auswahl zu bestätigen und den Beginn, der Daten an das Ziel sendet, zu bestätigen.

![Auswahl bestätigen](/help/rtcdp/destinations/assets/gcm-review.png)


<!--

Insert in Step 6 when mobile device ID activation is available

    >[!IMPORTANT]
    >
    >If you select mobile device IDs (GAID or IDFA) as primary identity in the Identity mapping step, you must also provide an Application Id in this step. If you selected GAID as identity, see [Set the Application ID](https://developer.android.com/studio/build/application-id) in the Android developer documentation. IF you selected IDFA as identity, see [App ID](https://developer.android.com/studio/build/application-id) in the Apple developer documentation.

    ![segment schedule page](/help/rtcdp/destinations/assets/gcm-segment-schedule.png) 

-->

## Überprüfen, ob die Segmentaktivierung erfolgreich war {#verify-activation}

Wechseln Sie nach Abschluss der Aktivierung zu Ihrem **[!UICONTROL Google Ads]** -Konto. Die aktivierten Segmente werden jetzt in Ihrem Google-Konto als Listen angezeigt. Beachten Sie, dass je nach Segmentgröße einige Audiencen nur dann gefüllt werden, wenn mehr als 100 aktive Benutzer zur Verfügung stehen.