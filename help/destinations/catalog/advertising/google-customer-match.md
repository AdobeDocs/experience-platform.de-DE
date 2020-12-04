---
keywords: google customer match;Google customer match;Google Customer Match
title: Google-Kundenübereinstimmungsziel
seo-title: Google-Kundenübereinstimmungsziel
description: Mit Google Customer Match können Sie Ihre Online- und Offline-Daten verwenden, um Ihre Kunden über die eigenen und betriebenen Eigenschaften wie Search, Shopping, Gmail und YouTube zu erreichen und erneut mit ihnen zu interagieren.
seo-description: Mit Google Customer Match können Sie Ihre Online- und Offline-Daten verwenden, um Ihre Kunden über die eigenen und betriebenen Eigenschaften wie Search, Shopping, Gmail und YouTube zu erreichen und erneut mit ihnen zu interagieren.
translation-type: tm+mt
source-git-commit: f2fdc3b75d275698a4b1e4c8969b1b840429c919
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 9%

---


# Google-Kundenübereinstimmungsziel

## Übersicht {#overview}

[Mit der Google-Kundenübereinstimmung](https://support.google.com/google-ads/answer/6379332?hl=en) können Sie Ihre Online- und Offlinedaten verwenden, um Ihre Kunden über die eigenen und betriebenen Eigenschaften von Google zu erreichen und erneut zu kontaktieren, z. B.: [!DNL Search], [!DNL Shopping], [!DNL Gmail]und [!DNL YouTube].

![Google Customer Match-Ziel in der CDP-Benutzeroberfläche in Echtzeit](../../assets/catalog/advertising/google-customer-match/catalog.png)

## Nutzungsszenarien

Damit Sie besser verstehen können, wie und wann Sie das [!DNL Google Customer Match] Ziel verwenden sollten, finden Sie hier Beispiele für Verwendungsfälle, die Kunden mit der Echtzeit-Datenplattform mithilfe dieser Funktion lösen können.

### Verwendungsfall Nr. 1

Eine Sportbekleidungsmarke möchte Bestandskunden erreichen [!DNL Google Search] und Angebot und Artikel anhand ihrer bisherigen Käufe und Browsergeschichte personalisieren [!DNL Google Shopping] und personalisieren. Die Bekleidungsmarke kann E-Mail-Adressen aus ihrem eigenen CRM-System in Echtzeit-CDP erfassen, Segmente aus ihren eigenen Offlinedaten erstellen und diese Segmente senden, um sie [!DNL Google Customer Match] zur Verwendung über [!DNL Search] und [!DNL Shopping]zur Optimierung ihrer Werbeausgaben zu nutzen.

### Verwendungsfall Nr. 2

Eine prominente Technologie-Firma hat gerade ein neues Handy veröffentlicht. In dem Bemühen, dieses neue Telefonmodell zu fördern, versuchen sie, das Bewusstsein für die neuen Funktionen des Telefons zu fördern, Kunden, die Inhaber früherer Modelle ihrer Telefone.

Um die Veröffentlichung zu bewerben, laden sie E-Mail-Adressen aus ihrer CRM-Datenbank in Echtzeit-CDP hoch und verwenden dabei die E-Mail-Adressen als Bezeichner. Segmente werden auf der Grundlage von Kunden erstellt, die ältere Telefonmodelle besitzen, und an [!DNL Google Customer Match] die sie gesendet werden, damit sie aktuelle Kunden, Kunden, die Inhaber älterer Telefonmodelle sind, sowie ähnliche Kunden auf Zielgruppe bringen können [!DNL YouTube].

## Datenverwaltung für [!DNL Google Customer Match] Ziele {#data-governance}

Die Ziele in Echtzeit-CDP können bestimmte Regeln und Pflichten für Daten haben, die an die Zielplattform gesendet oder von dieser empfangen werden. Sie sind dafür verantwortlich, die Einschränkungen und Pflichten Ihrer Daten zu verstehen und zu verstehen, wie Sie diese Daten in Adobe Experience Platform und der Zielplattform verwenden. Adobe Experience Platform bietet Tools zur Datenverwaltung, mit denen Sie einige dieser Datenverwendungsverpflichtungen verwalten können. [Erfahren Sie mehr](../../..//data-governance/labels/overview.md) über Tools und Richtlinien zur Datenverwaltung.

## Exporttyp und Identitäten {#export-type}

**Segmentexport** : Sie exportieren alle Segmentmitglieder (Audience) mit den Bezeichnern (Name, Telefonnummer usw.) used in the [!DNL Google Customer Match] destination.

**Identitäten** - Sie können rohe oder hash-E-Mails als Kunden-IDs in Google verwenden

## [!DNL Google Customer Match] Kontovoraussetzungen {#google-account-prerequisites}

Bevor Sie ein [!DNL Google Customer Match] Ziel in Echtzeit-CDP einrichten, sollten Sie die Google-Nutzungsrichtlinie lesen und beachten, die in der Dokumentation [!DNL Customer Match]zum [](https://support.google.com/google-ads/answer/6299717)Google-Support beschrieben ist.

### Zulassungsliste {#allowlist}

>[!NOTE]
>
>Es ist obligatorisch, der Zulassungsliste von Google hinzugefügt zu werden, bevor Sie Ihr erstes [!DNL Google Customer Match] Ziel in Echtzeit-CDP einrichten. Vergewissern Sie sich bitte, dass der unten beschriebene Vorgang der Zulassungsliste von Google abgeschlossen wurde, bevor Sie ein Ziel erstellen.

Bevor Sie das [!DNL Google Customer Match] Ziel in Echtzeit-CDP erstellen, müssen Sie sich an Google wenden und die Anweisungen zur Zulassungsliste unter Kunden-Match-Partner [verwenden befolgen, um Ihre Daten](https://support.google.com/google-ads/answer/7361372?hl=en&amp;ref_topic=6296507) in der Google-Dokumentation hochzuladen.


### Anforderungen für das E-Mail-Hashing {#hashing-requirements}

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

Weitere Informationen zum Eingeben von E-Mail-Adressen in der Experience Platform finden Sie in der Übersicht über die [Stapelverarbeitung](../../../ingestion/batch-ingestion/overview.md) und in der Übersicht über die [Erfassung](../../../ingestion/streaming-ingestion/overview.md)des Streamings.

Wenn Sie sich dafür entscheiden, die E-Mail-Adressen selbst zu hash, stellen Sie sicher, dass die Anforderungen von Google, wie in den Links oben beschrieben.


>[!IMPORTANT]
>
>Wenn Sie sich dafür entscheiden, keine E-Mail-Adressen zu hash, wird dies von CDP in Echtzeit für Sie ausgeführt, wenn Sie Segmente aktivieren in [!DNL Google Customer Match]. Wählen Sie im Arbeitsablauf für die [Aktivierung](#activate-segments) (siehe Schritt 5) die `Email` Option wie unten für *E-Mail-Adressen* und `Email_LC_SHA256` für *Hash-E-Mail-Adressen* dargestellt.

![Hashing bei der Aktivierung](../../assets/catalog/advertising/google-customer-match/identity-mapping.png)

## Mit Ziel verbinden {#connect-destination}

Blättern Sie unter **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]** zur **[!UICONTROL Advertising]** -Kategorie. Wählen Sie [!DNL Google Customer Match]und dann **[!UICONTROL Konfigurieren]**.

![Verbindung zum Google-Kunden-Übereinstimmungsziel herstellen](../../assets/catalog/advertising/google-customer-match/connect.png)

>[!NOTE]
>
>Wenn bereits eine Verbindung zu diesem Ziel besteht, wird auf der Zielkarte die Schaltfläche &quot; **[!UICONTROL Aktivieren]** &quot;angezeigt. Weitere Informationen zum Unterschied zwischen **[!UICONTROL Aktivieren]** und **[!UICONTROL Konfigurieren]** finden Sie im Abschnitt &quot; [Katalog](../../ui/destinations-workspace.md#catalog) &quot;der Dokumentation zum Zielarbeitsbereich.

In the **Account** step, if you had previously set up a connection to your [!DNL Google Customer Match] destination, select **[!UICONTROL Existing Account]** and select your existing connection. Or, you can select **[!UICONTROL New Account]** to set up a new connection to [!DNL Google Customer Match]. Wählen Sie **[!UICONTROL Mit Ziel]** verbinden, um sich anzumelden und Adobe Experience Cloud mit Ihrem [!DNL Google Ad] Konto zu verbinden.

>[!NOTE]
>
>Real-time CDP supports credentials validation in the authentication process and displays an error message if you input incorrect credentials to your [!DNL Google Ad] account. Dadurch wird sichergestellt, dass Sie den Workflow nicht mit falschen Anmeldedaten ausführen.

![Verbindung zum Google-Kundenübereinstimmungsziel herstellen - Authentifizierungsschritt](../../assets/catalog/advertising/google-customer-match/connection.png)

Once your credentials are confirmed and Adobe Experience Cloud is connected to your Google account, you can select **[!UICONTROL Next]** to proceed to the **[!UICONTROL Setup]** step.

![Anmeldedaten bestätigt](../../assets/catalog/advertising/google-customer-match/connection-success.png)

Geben Sie im Schritt **[!UICONTROL Authentifizierung]** einen [!UICONTROL Namen] und eine [!UICONTROL Beschreibung] für die Aktivierung ein und füllen Sie Google die [!UICONTROL Konto-ID]aus.

In diesem Schritt können Sie auch einen beliebigen **[!UICONTROL Marketing-Anwendungsfall]** auswählen, der für dieses Ziel gelten soll. Anwendungsfälle für das Marketing geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von der Adobe definierten Anwendungsfällen für das Marketing auswählen oder einen eigenen Anwendungsfall für das Marketing erstellen. Weitere Informationen zu Anwendungsfällen für das Marketing finden Sie auf der Seite [Datenverwaltung in Echtzeit-CDP](../../../rtcdp/privacy/data-governance-overview.md#destinations) . Informationen zu den einzelnen Anwendungsfällen für Marketingzwecke, die von der Adobe definiert wurden, finden Sie in der Übersicht über [Datenverwendungsrichtlinien](../../../data-governance/policies/overview.md#core-actions).

Wählen Sie **[!UICONTROL Ziel erstellen]** aus, nachdem Sie die obigen Felder ausgefüllt haben.

>[!IMPORTANT]
>
> * Der Anwendungsfall **[!UICONTROL Kombinieren mit PII]** -Marketing ist standardmäßig für das Ziel ausgewählt und kann nicht entfernt werden [!DNL Google Customer Match] .
> * Für [!DNL Google Customer Match] Ziele. **[!UICONTROL Die Konto-ID]** ist Ihre Kunden-Client-ID bei Google. Das Format der ID ist xxx-xxx-xxxx.


![Google-Kundenabgleich - Authentifizierungsschritt](../../assets/catalog/advertising/google-customer-match/authentication.png)

Ihr Ziel wird jetzt erstellt. Sie können **[!UICONTROL Speichern und beenden]** auswählen, wenn Sie Segmente später aktivieren möchten, oder Sie können **[!UICONTROL Weiter]** wählen, um den Workflow fortzusetzen und Segmente zur Aktivierung auszuwählen. In either case, see the next section, [Activate segments to [!DNL Google Customer Match]](#activate-segments), for the rest of the workflow.

## Activate segments to [!DNL Google Customer Match] {#activate-segments}

Gehen Sie wie folgt vor, um Segmente zu aktivieren [!DNL Google Customer Match]:

Wählen Sie unter **[!UICONTROL Ziele > Durchsuchen]** das Ziel aus, an dem Sie Ihre Segmente aktivieren möchten.[!DNL Google Customer Match]

Klicken Sie auf den Namen des Ziels. So gelangen Sie zum Aktivierungsfluss.

![activate-flow](../../assets/catalog/advertising/google-customer-match/activate-flow.png)

Beachten Sie, dass, wenn für ein Ziel bereits ein Seitenfluss vorhanden ist, die Aktivierungen angezeigt werden, die derzeit an das Ziel gesendet werden. Wählen Sie in der rechten Leiste die Option **[!UICONTROL Aktivierung bearbeiten]** und führen Sie die unten beschriebenen Schritte aus, um die Aktivierungsdetails zu ändern.

Select **[!UICONTROL Activate]**. In the **[!UICONTROL Activate destination]** workflow, on the **[!UICONTROL Select Segments]** page, select which segments to send to [!DNL Google Customer Match].

![Segment an Ziel](../../assets/catalog/advertising/google-customer-match/activate-segments.png)

Wählen Sie im Schritt **[!UICONTROL Identitätszuordnung]** aus, welche Attribute als Identität in dieses Ziel aufgenommen werden sollen. Wählen Sie **[!UICONTROL Hinzufügen neue Zuordnung]** aus und durchsuchen Sie Ihr Schema, wählen Sie E-Mail und/oder Hash-E-Mail und ordnen Sie sie der entsprechenden Zielgruppe zu.

![Anfangsbildschirm zur Identitätszuordnung](../../assets/catalog/advertising/google-customer-match/identity-mapping.png)

**Einfache Text-E-Mail-Adresse als primäre Identität**: Wenn Sie in Ihrem Schema als primäre Identität Nur-Text-E-Mail-Adressen (ohne Hashing) verwenden, wählen Sie das E-Mail-Feld in Ihren **[!UICONTROL Quellattributen]** aus und ordnen Sie es wie unten gezeigt in der rechten Spalte unter &quot; **[!UICONTROL Zielgruppen-IDs]**&quot;dem Feld &quot;E-Mail&quot;zu:

![E-Mail-Identität für einfachen Text auswählen](../../assets/catalog/advertising/google-customer-match/raw-email.gif)

**Hash-E-Mail-Adresse als primäre Identität**: Wenn Sie in Ihrem Schema als primäre Identität Hash-E-Mail-Adressen verwendet haben, wählen Sie das Feld Hash-E-Mail in Ihren **[!UICONTROL Quellattributen]** aus und ordnen Sie es wie unten dargestellt dem Feld Email_LC_SHA256 in der rechten Spalte unter &quot; **[!UICONTROL Zielgruppen-IDs]**&quot;zu:

![Hash-E-Mail-Identität auswählen](../../assets/catalog/advertising/google-customer-match/hashed-emails.gif)

Auf der Seite &quot; **[!UICONTROL Segmentplan]** &quot;können Sie das Datum des Beginns für das Senden der Daten an das Ziel festlegen.

Auf der Seite **[!UICONTROL Überprüfen]** können Sie eine Zusammenfassung Ihrer Auswahl sehen. Wählen Sie **[!UICONTROL Abbrechen]**, um den Fluss abzubrechen, **[!UICONTROL Zurück]**, um die Einstellungen zu ändern, oder **[!UICONTROL Fertig stellen]**, um Ihre Auswahl zu bestätigen und mit dem Senden von Daten an das Ziel zu beginnen.

>[!IMPORTANT]
>
>In diesem Schritt sucht CDP in Echtzeit nach Verstößen gegen die Datenverwendungsrichtlinie. Unten sehen Sie ein Beispiel, bei dem eine Richtlinie verletzt wird. Sie können den Segmentarbeitsablauf erst dann abschließen, wenn Sie die Aktivierung gelöst haben. Informationen zum Beheben von Richtlinienverletzungen finden Sie unter [Richtliniendurchsetzung](../../../rtcdp/privacy/data-governance-overview.md#enforcement) im Abschnitt zur Datenverwaltung.

![Auswahl bestätigen](../../assets/common/data-policy-violation.png)

Wenn keine Richtlinienverletzungen festgestellt wurden, wählen Sie **[!UICONTROL Fertig stellen]** , um Ihre Auswahl zu bestätigen und den Beginn, der Daten an das Ziel sendet, zu bestätigen.

![Auswahl bestätigen](../../assets/catalog/advertising/google-customer-match/review.png)

## Überprüfen, ob die Segmentaktivierung erfolgreich war {#verify-activation}

Wechseln Sie nach Abschluss der Aktivierung zu Ihrem **[!UICONTROL Google Ads]** -Konto. Die aktivierten Segmente werden jetzt in Ihrem Google-Konto als Listen angezeigt. Beachten Sie, dass je nach Segmentgröße einige Audiencen nur dann gefüllt werden, wenn mehr als 100 aktive Benutzer zur Verfügung stehen.

## Zusätzliche Ressourcen {#additional-resources}

* [Google-Kundenabgleich integrieren - Video-Lernprogramm](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html)