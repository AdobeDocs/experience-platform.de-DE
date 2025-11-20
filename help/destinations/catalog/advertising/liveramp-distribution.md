---
title: LiveRamp - Verteilungsanschluss
description: Erfahren Sie, wie Sie mit dem LiveRamp-Verteilungs-Connector Zielgruppen orchestrieren und aktivieren können, die zuvor in LiveRamp integriert wurden, um nachgelagerte Werbeziele zu erreichen.
exl-id: 1b11a743-1ef9-4b01-90ef-cc072bc03c91
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '2645'
ht-degree: 45%

---

# [!DNL LiveRamp - Distribution]-Verbindung

Mit der [!DNL LiveRamp - Distribution] können Sie Zielgruppen von Experience Platform für Premium-Publisher über mobile, Web-, Display- und vernetzte TV-Medien aktivieren.

>[!IMPORTANT]
>
>Dieser Ziel-Connector und diese Dokumentationsseite werden von LiveRamp erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an LiveRamp [hier](mailto:adobertcdp@liveramp.com).

## Unterstützte Ziele {#supported-destinations}

[!DNL LiveRamp - Distribution] unterstützt derzeit die Zielgruppenaktivierung für die folgenden Plattformen:

* [[!DNL 4C Insights]](#insights)
* [[!DNL Acast]](#acast)
* [[!DNL Nexxen]](#nexxen)
* [[!DNL Ampersand.tv]](#ampersand-tv)
* [[!DNL Captify]](#captify)
* [[!DNL Cardlytics]](#cardlytics)
* [[!DNL Disney (Hulu/ESPN/ABC)]](#disney)
* [[!DNL iHeartMedia]](#iheartmedia)
* [[!DNL Index Exchange]](#index-exchange)
* [[!DNL Magnite CTV Platform]](#magnite)
* [[!DNL Magnite DV+ (Rubicon Project)]](#magnite-dv)
* [[!DNL One Fox]](#fox)
* [[!DNL Pandora]](#pandora)
* [[!DNL Reddit]](#reddit)
* [[!DNL Roku]](#roku)
* [[!DNL Spotify]](#spotify)
* [[!DNL Taboola]](#taboola)
* [[!DNL TargetSpot]](#targetspot)
* [[!DNL Teads]](#teads)
* [[!DNL WB Discovery]](#wb-discovery)

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das [!DNL LiveRamp - Distribution]-Ziel verwenden sollten, finden Sie hier ein Anwendungsbeispiel, das für Kundinnen und Kunden von Adobe Experience Platform mit diesem Ziel geeignet ist.

Das Marketing-Team einer Sportbekleidung in retailer verwendete die Verbindung [LiveRamp - Onboarding](liveramp-onboarding.md), um Zielgruppen aus Experience Platform an ihr LiveRamp-Konto zu senden.

Trigger Über die [!DNL LiveRamp - Distribution]-Verbindung können sie jetzt die Aktivierung der integrierten Zielgruppen in die [unterstützten Ziele“ &#x200B;](#supported-destinations). Dann können sie Benutzer auf mobilen, offenen Web-, Social- und [!DNL CTV]-Plattformen ansprechen.

## Onboarden von Zielgruppen für LiveRamp {#onboarding}

Bevor Sie Zielgruppen über die [!DNL LiveRamp - Distribution]-Verbindung aktivieren, verwenden Sie die Verbindung [LiveRamp - Onboarding](liveramp-onboarding.md) , um Ihre Experience Platform-Zielgruppen in LiveRamp zu exportieren.

Nachdem Sie Ihre Zielgruppen in LiveRamp integriert haben, setzen Sie den Aktivierungs-Workflow im Schritt [Verbindung mit dem Ziel](#connect) fort, um Ihre Zielplattformen für die Datenaktivierung auszuwählen und zu konfigurieren.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_identifier_settings"
>title="Identifizierungseinstellungen"
>abstract="Wählen Sie die von Ihrem Ziel unterstützten Kennungen aus. Die vollständige Liste der unterstützten Kennungen für die einzelnen Ziele finden Sie in der Dokumentation."

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage Destinations]** Zugriffssteuerungsberechtigungen[. &#x200B;](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Bei LiveRamp authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Connect to destination]** aus.

![Bild der Experience Platform-Benutzeroberfläche mit dem Bildschirm für die Zielverbindung.l](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-new-connection.png)

* **[!UICONTROL LiveRamp Organization ID]**: Die Organisations-ID Ihres LiveRamp-Kontos (aufgeführt als _owner_org_ in Ihren von LiveRamp bereitgestellten Anmeldeinformationen).
* **[!UICONTROL Password]**: Ihr LiveRamp-Kontokennwort (aufgeführt als _secret_key_ in Ihren LiveRamp-Anmeldedaten).
* **[!UICONTROL Token URL]**: Ihre LiveRamp-Token-URL.
* **[!UICONTROL Username]**: Benutzername Ihres LiveRamp-Kontos (aufgeführt als _account_id_ in Ihren von LiveRamp bereitgestellten Anmeldeinformationen).

### Konfigurieren von Zieldetails {#destination-details}

Geben Sie nach erfolgreicher Verbindung mit Ihrem LiveRamp-Konto die erforderlichen Informationen ein, um eine Verbindung mit dem Ziel herzustellen, für das Sie Zielgruppen aktivieren möchten.

![Bild der Experience Platform-Benutzeroberfläche mit dem Bildschirm mit den Zieldetails.l](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-destination-details.png)

* **[!UICONTROL Name]**: Geben Sie den bevorzugten Namen für Ihre Zielverbindung ein.

>[!NOTE]
>
>Adobe empfiehlt, beim Benennen Ihres Ziels folgendes Format zu verwenden: `LiveRamp - Downstream Destination Name`. Dieses Benennungsmuster hilft Ihnen, Ihre Ziele auf der Registerkarte [Durchsuchen](../../ui/destinations-workspace.md#browse) des Arbeitsbereichs Ziele schnell zu identifizieren.
><br>
>Beispiel: `LiveRamp - Roku`.

* **[!UICONTROL Description]**: Geben Sie eine Beschreibung für Ihr Ziel ein. Verwenden Sie eine Beschreibung, die Ihnen hilft, den Zweck dieses Ziels leicht zu identifizieren.
* **[!UICONTROL Destination]**: Wählen Sie im Dropdown-Menü das Ziel aus, für das Sie Zielgruppen aktivieren möchten. Das hier ausgewählte Ziel wirkt sich direkt auf das aus, was Sie [&#x200B; Bildschirm „Zielspezifische Einstellungen](#destination-settings) sehen.
* **[!UICONTROL Integration]**: Wählen Sie das Integrationskonto aus, das Sie für Ihr Ziel verwenden möchten.
* **[!UICONTROL Identifier]**: Wählen Sie die von Ihrem Ziel unterstützten Kennungen aus. Derzeit sind die unterstützten Kennungen aller Ziele im Dropdown-Menü vorbefüllt.

## Zielspezifische Einstellungen {#destination-settings}

Für jedes der Ziele [unterstützt](#supported-destinations) von [!DNL LiveRamp - Distribution] müssen Sie bestimmte Konfigurationsoptionen angeben.

Detaillierte Anleitungen zum Konfigurieren der einzelnen Ziele finden Sie in den folgenden Abschnitten.

### [!DNL 4C Insights] {#insights}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_4cinsights_profile_id"
>title="4C-Markenprofil-ID"
>abstract="Geben Sie die numerische ID ein, die Ihrem 4C-Markenprofil zugeordnet ist. Wenn Sie diese ID nicht haben, wenden Sie sich an den 4C-Kundendienst."

Um Details für das Ziel zu konfigurieren, füllen Sie die folgenden Felder aus.

![Bild der Experience Platform-Benutzeroberfläche mit den Kundendatenfeldern für das 4C Insights-Ziel.](../../assets/catalog/advertising/liveramp-distribution/LR_4C_DestSpecific.png)

* **[!UICONTROL 4C Brand Profile ID]**: Geben Sie die numerische ID ein, die Ihrem 4C-Markenprofil zugeordnet ist. Wenn Sie diese ID nicht haben, wenden Sie sich an den 4C-Kundendienst.

### [!DNL Acast] {#acast}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_acast_client"
>title="Client-Name"
>abstract="Ihr Advertiser-Kontoname, wie er dem Zielpartner angezeigt werden soll. Verwenden Sie Ihren Unternehmensnamen. Verwenden Sie keine Leerzeichen oder Sonderzeichen."

Um Details für das Ziel zu konfigurieren, füllen Sie die folgenden Felder aus.

![Bild der Experience Platform-Benutzeroberfläche mit den Kundendatenfeldern für das Acast-Ziel.](../../assets/catalog/advertising/liveramp-distribution/LR_Acast_DestSpecific.png)

* **[!UICONTROL Client name]**: Ihr Advertiser-Kontoname, wie er dem Zielpartner angezeigt werden soll. Verwenden Sie Ihren Unternehmensnamen. Verwenden Sie keine Leerzeichen oder Sonderzeichen.

### [!DNL Ampersand.tv] {#ampersand-tv}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_ampersand_company_name"
>title="Ihr Firmenname"
>abstract="Ihr Firmenname, wie er der Zielpartnerin bzw. dem Zielpartner angezeigt werden soll. Verwenden Sie keine Leerzeichen oder Sonderzeichen."

Um Details für das Ziel zu konfigurieren, füllen Sie die folgenden Felder aus.

![Bild der Experience Platform-Benutzeroberfläche mit den Kundendatenfeldern für das Ampersand-Ziel.](../../assets/catalog/advertising/liveramp-distribution/LR_Ampersand_DestSpecific.png)

* **[!UICONTROL Your Company Name]**: Ihr Firmenname, wie er dem Zielpartner angezeigt werden soll. Verwenden Sie keine Leerzeichen oder Sonderzeichen.

### [!DNL Captify] {#captify}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_captify_client"
>title="Client-Name"
>abstract="Ihr Advertiser-Kontoname, wie er dem Zielpartner angezeigt werden soll. Verwenden Sie Ihren Unternehmensnamen. Verwenden Sie keine Leerzeichen oder Sonderzeichen."

Um Details für das Ziel zu konfigurieren, füllen Sie die folgenden Felder aus.

![Bild der Experience Platform-Benutzeroberfläche mit den Kundendatenfeldern für das Captify-Ziel.](../../assets/catalog/advertising/liveramp-distribution/LR_Captify_DestSpecific.png)

* **[!UICONTROL Client name]**: Ihr Advertiser-Kontoname, wie er dem Zielpartner angezeigt werden soll. Verwenden Sie Ihren Unternehmensnamen. Verwenden Sie keine Leerzeichen oder Sonderzeichen.

### [!DNL Cardlytics] {#cardlytics}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_cardlytics_client"
>title="Client-Name"
>abstract="Ihr Advertiser-Kontoname, wie er dem Zielpartner angezeigt werden soll. Verwenden Sie Ihren Unternehmensnamen. Verwenden Sie keine Leerzeichen oder Sonderzeichen."

Um Details für das Ziel zu konfigurieren, füllen Sie die folgenden Felder aus.

![Bild der Experience Platform-Benutzeroberfläche mit den Kundendatenfeldern für das Cardlytics-Ziel.](../../assets/catalog/advertising/liveramp-distribution/LR_Cardlytics_DestSpecific.png)

* **[!UICONTROL Client name]**: Ihr Advertiser-Kontoname, wie er dem Zielpartner angezeigt werden soll. Verwenden Sie Ihren Unternehmensnamen. Verwenden Sie keine Leerzeichen oder Sonderzeichen.

### [!DNL Disney (Hulu/ESPN/ABC)] {#disney}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_agreement"
>title="Vereinbarung über Zielbedingungen für Advertiser-Daten"
>abstract="Geben Sie `I AGREE` ein, um die Kenntnisnahme und das Einverständnis mit den Datenbedingungen für den Disney-Advertiser zu bestätigen."

<!-- >additional-url="<https://www.disneyadvertising.com/ADVERTISER-DATA-DESTINATION-TERMS/>" text="Read the agreement" -->

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_disney_client"
>title="Client-Name"
>abstract="Ihr Advertiser-Kontoname, wie er dem Zielpartner angezeigt werden soll. Verwenden Sie Ihren Unternehmensnamen. Verwenden Sie keine Leerzeichen oder Sonderzeichen."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_disney_email"
>title="Ihre E-Mail-Adresse"
>abstract="Geben Sie eine E-Mail-Adresse ein, die an eine Person gebunden ist. Diese E-Mail-Adresse dient als Signatur zum Vertrag mit den Datennutzerbedingungen. Diese E-Mail-Adresse wird bei Bedarf auch verwendet, um Sie zu kontaktieren."

Um Details für das Ziel zu konfigurieren, füllen Sie die folgenden Felder aus.

![Bild der Experience Platform-Benutzeroberfläche mit den Kundendatenfeldern für das Disney-Ziel.](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-disney-fields.png)

* **[!UICONTROL Advertiser data destination terms agreement]**: Geben Sie `I AGREE` ein, um die Bestätigung und Zustimmung zu den Disney Advertiser-Datenbedingungen zu bestätigen.
* **[!UICONTROL Client name]**: Geben Sie Ihren Firmennamen so ein, wie er dem Zielpartner angezeigt werden soll.
* **[!UICONTROL Email address]**: Geben Sie eine mit einer Person verknüpfte E-Mail-Adresse ein. Diese E-Mail-Adresse dient als Signatur für die Advertiser-Datenvereinbarung.

### [!DNL iHeartMedia] {#iheartmedia}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_iheartmedia_client"
>title="Client-Name"
>abstract="Ihr Advertiser-Kontoname, wie er dem Zielpartner angezeigt werden soll. Verwenden Sie Ihren Unternehmensnamen. Verwenden Sie keine Leerzeichen oder Sonderzeichen."

Um Details für das Ziel zu konfigurieren, füllen Sie die folgenden Felder aus.

![Bild der Experience Platform-Benutzeroberfläche mit den Kundendatenfeldern für das iHeartMedia-Ziel.](../../assets/catalog/advertising/liveramp-distribution/LR_iHeart_DestSpecific.png)

* **[!UICONTROL Client Name]**: Ihr Advertiser-Kontoname, wie er dem Zielpartner angezeigt werden soll. Verwenden Sie Ihren Unternehmensnamen. Verwenden Sie keine Leerzeichen oder Sonderzeichen.

### [!DNL Index Exchange] {#index-exchange}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_index_advertiseraccountname"
>title="Kontoname"
>abstract="Ihr Client-Kontoname bei Index Exchange. Verwenden Sie keine Leerzeichen oder Sonderzeichen."

Um Details für das Ziel zu konfigurieren, füllen Sie die folgenden Felder aus.

![Bild der Experience Platform-Benutzeroberfläche mit den Kundendatenfeldern für das Exchange-Indexziel.](../../assets/catalog/advertising/liveramp-distribution/LR_IndexExchange_DestSpecific.png)

* **[!UICONTROL Account Name]**: Name Ihres Exchange Index-Client-Kontos. Verwenden Sie keine Leerzeichen oder Sonderzeichen.

### [!DNL Magnite CTV Platform] {#magnite}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_magnitectv_client"
>title="Client"
>abstract="Ihr Advertiser-Kontoname, wie er der Zielpartnerin bzw. dem Zielpartner angezeigt werden soll. Verwenden Sie Ihren Unternehmensnamen. Verwenden Sie keine Leerzeichen oder Sonderzeichen."

Um Details für das Ziel zu konfigurieren, füllen Sie die folgenden Felder aus.

![Bild der Experience Platform-Benutzeroberfläche mit den Kundendatenfeldern für das Magnite CTV-Ziel.](../../assets/catalog/advertising/liveramp-distribution/LR_MagniteCTV_DestSpecific.png)

* **[!UICONTROL Client]**: Ihr Client-Name, wie er dem Zielpartner angezeigt werden soll. Verwenden Sie Ihren Unternehmensnamen. Verwenden Sie keine Leerzeichen oder Sonderzeichen.

### [!DNL Magnite DV+ (Rubicon Project)] {#magnite-dv}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_magnitedv+_partnerid"
>title="Partner-ID"
>abstract="Die Partner-ID bei Rubicon Project, die dem Vermarkter zugeordnet ist, dem das Segment/die Daten gehören. Wenden Sie sich an Ihren Rubicon Project-Support-Kontakt, wenn Sie sich nicht sicher sind, welchen Wert Sie verwenden sollten."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_magnitedv+_seatid"
>title="Lizenz-ID"
>abstract="Magnite DV+-Lizenz-ID, die Ihnen von der Magnite-Kundenbetreuung bereitgestellt wurde"

Um Details für das Ziel zu konfigurieren, füllen Sie die folgenden Felder aus.

![Bild der Experience Platform-Benutzeroberfläche mit den Kundendatenfeldern für das Magnite DV+-Ziel.](../../assets/catalog/advertising/liveramp-distribution/LR_MagniteDV_DestSpecific.png)

* **[!UICONTROL Partner ID]**: Die Rubicon-Projektpartner-ID, die mit dem Herausgeber verknüpft ist, dem das Segment/die Daten gehören. Wenden Sie sich an Ihren Rubicon Project-Support-Kontakt, wenn Sie sich nicht sicher sind, welchen Wert Sie verwenden sollten.
* **[!UICONTROL Seat ID]**: Magnite DV+ Sitzplatz-ID von Ihrem Magnite Account Manager

### [!DNL Nexxen (formerly known as [!DNL Amobee])] {#nexxen}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_nexxen_ratetype"
>title="Ratentyp"
>abstract="Der Ratentyp stellt die Art und Weise dar, wie die Datennutzung in Rechnung gestellt werden soll. Alle Raten von 0,00 $ sollten eine Pauschalgebühr sein. Vergewissern Sie sich bei der Nexxen-Kundenbetreuung, wenn Sie sich nicht sicher sind, welcher Ratentyp verwendet werden sollte."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_nexxen_marketid"
>title="Markt-ID"
>abstract="Geben Sie die numerische ID des Marktes ein, wo der Nexxen-Datenvertrag erstellt werden soll. Geben Sie „-1“ ein, wenn Sie die „AlwaysOn“-Syndizierung auf allen Märkten der Nexxen-Plattform durchführen."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_nexxen_advertiserid"
>title="Advertiser-ID"
>abstract="Wenn Sie Daten an einen einzigen Advertiser in der Nexxen-Plattform senden, geben Sie die numerische Amobee-Advertiser-ID ein. Wenn Sie die Daten für alle Advertiser auf einem Markt verfügbar machen möchten oder wenn diese Segmente „AlwaysOn“ sind, geben Sie „-1“ ein."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_nexxen_contactemail"
>title="Kontakt-E-Mail"
>abstract="Geben Sie die E-Mail-Adresse ein, die Nexxen zum Senden von Datenvertragsdetails verwenden sollte. Wahrscheinlich ist dies Ihre eigene E-Mail-Adresse, aber es kann sich auch um einen E-Mail-Alias handeln. Trennen Sie bei mehreren Empfängerinnen bzw. Empfängern durch Kommas (`email1@domain.com`,`email2@domain.com` usw.)."

Um Details für das Ziel zu konfigurieren, füllen Sie die folgenden Felder aus.

![Bild der Experience Platform-Benutzeroberfläche mit den Kundendatenfeldern für das Nexxen-Ziel.](../../assets/catalog/advertising/liveramp-distribution/LR_Nexxen_DestSpecific.png)

* **[!UICONTROL Rate Type]**: Der Tariftyp gibt an, wie die Datennutzung in Rechnung gestellt werden soll. Alle Raten von 0,00 $ sollten eine Pauschalgebühr sein. Vergewissern Sie sich bei der Nexxen-Kundenbetreuung, wenn Sie sich nicht sicher sind, welcher Ratentyp verwendet werden sollte.
* **[!UICONTROL Market ID]**: Geben Sie die numerische Markt-ID ein, unter der der Nexxen-Datenvertrag erstellt werden soll. Geben Sie „-1“ ein, wenn Sie die „AlwaysOn“-Syndizierung auf allen Märkten der Nexxen-Plattform durchführen.
* **[!UICONTROL Advertiser ID]**: Wenn Sie Daten an einen einzelnen Advertiser auf der Nexxen-Plattform senden, geben Sie die numerische Nexxen Advertiser-ID ein. Wenn Sie die Daten für alle Werbetreibenden in einem Markt verfügbar machen möchten oder diese Segmente „AlwaysOn“ sind, geben Sie -1 ein.
* **[!UICONTROL Contact Email]**: Geben Sie die E-Mail-Adresse ein, die Nexxen zum Senden von Vertragsdaten verwenden soll. Wahrscheinlich ist dies Ihre eigene E-Mail-Adresse, aber es kann sich auch um einen E-Mail-Alias handeln. Trennen Sie die Empfänger bei mehreren durch Kommas ( `email1@domain.com`, `email2@domain.com`).

### [!DNL One Fox] {#fox}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_fox_client"
>title="Client"
>abstract="Der Name Ihres Unternehmens-/Vertriebskontos, wie er der Partnerin bzw. dem Partner angezeigt werden soll. Wenden Sie sich an Ihre Partner-Kundenbetreuung, wenn Sie nicht sicher sind, welchen Namen Sie verwenden möchten. Verwenden Sie keine Leerzeichen oder Sonderzeichen."

Um Details für das Ziel zu konfigurieren, füllen Sie die folgenden Felder aus.

![Bild der Experience Platform-Benutzeroberfläche mit den Kundendatenfeldern für das One Fox-Ziel.](../../assets/catalog/advertising/liveramp-distribution/LR_Fox_DestSpecific.png)

* **[!UICONTROL Client]**: Der Name Ihres Unternehmens-/Vertriebskontos, wie er dem Partner angezeigt werden soll. Verwenden Sie standardmäßig Ihren Firmennamen. Wenden Sie sich an Ihre Partner-Kundenbetreuung, wenn Sie nicht sicher sind, welchen Namen Sie verwenden möchten. Verwenden Sie keine Leerzeichen oder Sonderzeichen.

### [!DNL Pandora] {#pandora}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_pandora_account_name"
>title="Kontoname"
>abstract="Der Name Ihres Pandora-Kontos. Wenden Sie sich an Ihren Pandora-Support-Kontakt, wenn Sie sich nicht sicher sind, welchen Kontonamen Sie haben. Verwenden Sie keine Leerzeichen oder Sonderzeichen."

Um Details für das Ziel zu konfigurieren, füllen Sie die folgenden Felder aus.

![Bild der Experience Platform-Benutzeroberfläche mit den Kundendatenfeldern für das Pandora-Ziel.](../../assets/catalog/advertising/liveramp-distribution/LR_Pandora_DestSpecific.png)

* **[!UICONTROL Account name]**: Der Name Ihres Pandora-Kontos. Wenden Sie sich an Ihren Pandora-Support-Kontakt, wenn Sie sich nicht sicher sind, welchen Kontonamen Sie haben. Verwenden Sie keine Leerzeichen oder Sonderzeichen.

### [!DNL Reddit] {#reddit}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_reddit_advertiser_id"
>title="Reddit-Advertiser-ID"
>abstract="Ihre Reddit-Advertiser-ID. Muss mit „t2_“ oder „a2_“ beginnen. Wenden Sie sich an Ihren Reddit-Support-Kontakt, wenn Sie Ihre Advertiser-ID nicht kennen."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_reddit_advertiser_name"
>title="Reddit-Advertiser-Name"
>abstract="Ihr Reddit-Advertiser-Name. Verwenden Sie keine Leerzeichen oder Sonderzeichen."

Um Details für das Ziel zu konfigurieren, füllen Sie die folgenden Felder aus.

![Bild der Experience Platform-Benutzeroberfläche mit den Kundendatenfeldern für das Reddit-Ziel.](../../assets/catalog/advertising/liveramp-distribution/LR_Reddit_DestSpecific.png)

* **[!UICONTROL Reddit advertiser ID]**: Ihre Reddit Advertiser ID. Muss mit „t2_“ oder „a2_“ beginnen. Wenden Sie sich an Ihren Reddit-Support-Kontakt, wenn Sie Ihre Advertiser-ID nicht kennen.
* **[!UICONTROL Reddit advertiser name]**: Ihr Reddit-Advertiser-Name. Verwenden Sie keine Leerzeichen oder Sonderzeichen.

### [!DNL Roku] {#roku}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_roku_email"
>title="E-Mail-Adresse des Roku-Kontos"
>abstract="Geben Sie die mit Ihrem Roku-Konto verknüpfte E-Mail-Adresse ein."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_roku_representative_email"
>title="E-Mail-Adresse des Roku-Support-Kontakts"
>abstract="Geben Sie die E-Mail-Adresse Ihres Roku-Support-Kontakts ein. Diese Adresse wird verwendet, um Taxonomie-Aktualisierungen zu senden. Um mehrere Adressen einzugeben, trennen Sie sie durch Kommas."

Um Details für das Ziel zu konfigurieren, füllen Sie die folgenden Felder aus.

![Bild der Experience Platform-Benutzeroberfläche mit den unterstützten Kennungen für das Roku-Ziel.](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-roku-fields.png)

* **[!UICONTROL Roku account email address]**: Geben Sie die mit Ihrem Roku-Konto verknüpfte E-Mail-Adresse ein.
* **[!UICONTROL Roku account representative email address]**: Geben Sie die E-Mail-Adresse Ihres Roku-Kundenbetreuers ein. Um mehrere Adressen einzugeben, trennen Sie sie durch Kommas.

### [!DNL Spotify] {#spotify}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_spotify_client"
>title="Client-Name"
>abstract="Ihr Advertiser-Kontoname, wie er dem Zielpartner angezeigt werden soll. Verwenden Sie Ihren Unternehmensnamen. Verwenden Sie keine Leerzeichen oder Sonderzeichen."

Um Details für das Ziel zu konfigurieren, füllen Sie die folgenden Felder aus.

![Bild der Experience Platform-Benutzeroberfläche mit den unterstützten Kennungen für das Spotify-Ziel.](../../assets/catalog/advertising/liveramp-distribution/LR_Spotify_DestSpecific.png)

* **[!UICONTROL Client name]**: Ihr Advertiser-Kontoname, wie er dem Zielpartner angezeigt werden soll. Verwenden Sie Ihren Unternehmensnamen. Verwenden Sie keine Leerzeichen oder Sonderzeichen.

### [!DNL Taboola] {#taboola}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_taboola_rep_email"
>title="E-Mail-Adresse der Kundenbetreuung"
>abstract="Die E-Mail-Adresse der Taboola-Kundenbetreuung."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_taboola_seg_type"
>title="Segmenttyp"
>abstract="Der Segmenttyp. Derzeit werden nur Erstanbietersegmente unterstützt."

Um Details für das Ziel zu konfigurieren, füllen Sie die folgenden Felder aus.

![Bild der Experience Platform-Benutzeroberfläche mit den unterstützten Kennungen für das Taboola-Ziel.](../../assets/catalog/advertising/liveramp-distribution/LR_Taboola_DestSpecific.png)

* **[!UICONTROL Account manager email address]**: Die E-Mail-Adresse Ihres Taboola Account Managers.
* **[!UICONTROL Segment type]**: Der Segmenttyp. Derzeit werden nur Erstanbietersegmente unterstützt.

### [!DNL TargetSpot] {#targetspot}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_targetspot_client"
>title="Client-Name"
>abstract="Ihr Advertiser-Kontoname, wie er dem Zielpartner angezeigt werden soll. Verwenden Sie Ihren Unternehmensnamen. Verwenden Sie keine Leerzeichen oder Sonderzeichen."

Um Details für das Ziel zu konfigurieren, füllen Sie die folgenden Felder aus.

![Bild der Experience Platform-Benutzeroberfläche mit den unterstützten Kennungen für das TargetSpot-Ziel.](../../assets/catalog/advertising/liveramp-distribution/LR_TargetSpot_DestSpecific.png)

* **[!UICONTROL Client name]**: Ihr Advertiser-Kontoname, wie er dem Zielpartner angezeigt werden soll. Verwenden Sie Ihren Unternehmensnamen. Verwenden Sie keine Leerzeichen oder Sonderzeichen.

### [!DNL Teads] {#teads}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_teads_teadsid"
>title="Teads-ID"
>abstract="Ihre Teads-ID"

Um Details für das Ziel zu konfigurieren, füllen Sie die folgenden Felder aus.

![Bild der Experience Platform-Benutzeroberfläche mit den unterstützten Kennungen für das TargetSpot-Ziel.](../../assets/catalog/advertising/liveramp-distribution/LR_Teads_DestSpecific.png)

* **[!UICONTROL Teads ID]**: Ihre Reads-ID

### [!DNL WB Discovery] {#wb-discovery}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_wb_client"
>title="Client-Name"
>abstract="Ihr Advertiser-Kontoname, wie er dem Zielpartner angezeigt werden soll. Verwenden Sie Ihren Unternehmensnamen. Verwenden Sie keine Leerzeichen oder Sonderzeichen."

Um Details für das Ziel zu konfigurieren, füllen Sie die folgenden Felder aus.

![Bild der Experience Platform-Benutzeroberfläche mit den unterstützten Kennungen für das Web-Discovery-Ziel.](../../assets/catalog/advertising/liveramp-distribution/LR_WBD_DestSpecific.png)

* **[!UICONTROL Client name]**: Ihr Advertiser-Kontoname, wie er dem Zielpartner angezeigt werden soll. Verwenden Sie Ihren Unternehmensnamen. Verwenden Sie keine Leerzeichen oder Sonderzeichen.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten, wählen Sie einen Warnhinweis aus der Liste aus. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Warnhinweisen zu Zielen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Die [!DNL LiveRamp - Distribution]-Verbindung aktiviert Zielgruppen, die bereits über die Verbindung „LiveRamp - Onboarding“ in [&#x200B; LiveRamp-Konto &#x200B;](liveramp-onboarding.md) wurden.

Um Ihre Zielgruppen erfolgreich zu aktivieren, müssen Sie dieselben **auswählen** die Sie [zuvor eingeführt) &#x200B;](liveramp-onboarding.md) LiveRamp haben.

>[!IMPORTANT]
>
>Bei der Auswahl von Zielgruppen, die noch nicht über die Verbindung [LiveRamp - Onboarding](liveramp-onboarding.md) integriert wurden, tritt beim Onboarding der neuen Zielgruppen kein Trigger auf.

## Exportierte Daten/Datenexport validieren {#exported-data}

Um die Aktivierung Ihrer Zielgruppen zu überprüfen und zu überwachen, melden Sie sich bei Ihrem LiveRamp-Konto an und überprüfen Sie die Aktivierungsmetriken.

Wenden Sie sich bei Fragen zur Zielgruppenaktivierung an Ihren LiveRamp-Kundenbetreuer.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).

## Zusätzliche Ressourcen {#additional-resources}

Weitere Informationen zum Konfigurieren Ihres [!DNL LiveRamp - Onboarding]-Ziels finden Sie in der Dokumentation [LiveRamp - Onboarding](liveramp-onboarding.md).
