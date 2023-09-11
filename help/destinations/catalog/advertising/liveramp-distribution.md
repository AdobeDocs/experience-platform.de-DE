---
title: LiveRamp - Verteilungsverbindung
description: Erfahren Sie, wie Sie mit dem LiveRamp - Distribution-Connector Zielgruppen aktivieren können, die zuvor in LiveRamp integriert wurden, und zwar für andere Werbeziele.
hide: true
hidefromtoc: true
source-git-commit: c04c7ff4f1ab45d944f4ab516d7842df536fae40
workflow-type: tm+mt
source-wordcount: '1475'
ht-degree: 60%

---


# [!DNL LiveRamp - Distribution]-Verbindung {#liveramp-onboarding}

Die [!DNL LiveRamp - Distribution] ermöglicht Ihnen die Aktivierung von Zielgruppen von Experience Platform zu Premium-Herausgebern über mobile, Web-, Display- und vernetzte TV-Medien.

>[!IMPORTANT]
>
>Diese Ziel-Connector- und Dokumentationsseite werden von LiveRamp erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an LiveRamp [here](mailto:example@email.com).

## Unterstützte Ziele {#supported-destinations}

[!DNL LiveRamp - Distribution] unterstützt derzeit die Aktivierung der Zielgruppe für die folgenden Plattformen:

* [!DNL 4C Insights]
* [!DNL Acast]
* [!DNL Amobee]
* [!DNL Ampersand.tv]
* [!DNL Captify]
* [!DNL Cardlytics]
* [[!DNL Disney (Hulu/ESPN/ABC)]](#disney)
* [!DNL iHeartMedia]
* [!DNL Index Exchange]
* [!DNL Magnite CTV Platform]
* [!DNL Magnite DV+ (Rubicon Project)]
* [!DNL One Fox]
* [!DNL Pandora]
* [!DNL Reddit]
* [[!DNL Roku]](#roku)
* [!DNL Spotify]
* [!DNL Taboola]
* [!DNL TargetSpot]
* [!DNL Teads]
* [!DNL WB Discovery]

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das [!DNL LiveRamp - Distribution]-Ziel verwenden sollten, finden Sie hier ein Anwendungsbeispiel, das für Kundinnen und Kunden von Adobe Experience Platform mit diesem Ziel geeignet ist.

Das Marketing-Team eines Sportbekleidungshändlers verwendete die [LiveRamp - Onboarding](liveramp-onboarding.md) -Verbindung, um Zielgruppen von Experience Platform an ihr LiveRamp-Konto zu senden.

Durch die [!DNL LiveRamp - Distribution] -Verbindung können sie nun die Aktivierung der integrierten Zielgruppen zu den oben auf dieser Seite erwähnten Zielen Trigger haben, sodass sie Benutzer auf Mobilgeräten, im Web, in sozialen Netzwerken und in [!DNL CTV] Plattformen.

## Einbinden von Zielgruppen in LiveRamp {#onboarding}

Vor der Aktivierung von Zielgruppen durch die [!DNL LiveRamp - Distribution] Verbindung verwenden, verwenden Sie die [LiveRamp - Onboarding](liveramp-onboarding.md) -Verbindung, um Ihre Experience Platform-Audiences in LiveRamp zu exportieren.

Nachdem Sie Ihre Zielgruppen in LiveRamp integriert haben, fahren Sie mit dem Aktivierungs-Workflow über [Verbindung zum Ziel herstellen](#connect) Schritt.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_identifier_settings"
>title="Identifizierungseinstellungen"
>abstract="Wählen Sie die von Ihrem Ziel unterstützten Kennungen aus. Die vollständige Liste der unterstützten Kennungen für die einzelnen Ziele finden Sie in der Dokumentation."

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Bei LiveRamp authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und klicken Sie auf **[!UICONTROL Mit Ziel verbinden]**.

![Abbildung der Platform-Benutzeroberfläche mit dem Bildschirm für die Zielverbindung.l](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-new-connection.png)

* **[!UICONTROL Token-URL]**: Ihre LiveRamp-Token-URL.
* **[!UICONTROL LiveRamp-Organisations-ID]**: Die Organisations-ID Ihres LiveRamp-Kontos.
* **[!UICONTROL Benutzername]**: Ihr LiveRamp-Konto-Benutzername.
* **[!UICONTROL Passwort]**: Ihr LiveRamp-Kontokennwort.

### Zieldetails konfigurieren {#destination-details}

Nachdem Sie erfolgreich eine Verbindung zu Ihrem LiveRamp-Konto hergestellt haben, geben Sie die erforderlichen Informationen ein, um eine Verbindung mit dem Ziel herzustellen, für das Sie Zielgruppen aktivieren möchten.

![Abbildung der Platform-Benutzeroberfläche mit den Zieldetails screen.l](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-destination-details.png)

* **[!UICONTROL Name]**: Geben Sie den bevorzugten Namen für Ihre Zielverbindung ein.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für das Ziel ein. Verwenden Sie eine Beschreibung, mit der Sie den Zweck dieses Ziels leicht identifizieren können.
* **[!UICONTROL Ziel]**: Wählen Sie über das Dropdown-Menü das Ziel aus, für das Sie Zielgruppen aktivieren möchten. Das hier ausgewählte Ziel wirkt sich direkt auf das aus, was Sie im [Zielspezifische Einstellungen](#destination-settings) angezeigt.
* **[!UICONTROL Integration]**: Wählen Sie das Integrationskonto aus, das Sie für Ihr Ziel verwenden möchten.
* **[!UICONTROL Kennung]**: Wählen Sie die von Ihrem Ziel unterstützten Kennungen aus. Derzeit sind alle Ziele im Dropdown-Menü mit ihren unterstützten Kennungen vorausgefüllt.

## Zielspezifische Einstellungen {#destination-settings}

Jedes Ziel [unterstützt](#supported-destinations) von [!DNL LiveRamp - Onboarding] erfordert das Ausfüllen bestimmter Konfigurationsoptionen.

In den folgenden Abschnitten finden Sie ausführliche Anleitungen zum Konfigurieren der einzelnen Ziele.

### [!DNL 4C Insights] {#insights}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_4cinsights_profile_id"
>title="4C-Markenprofil-ID"
>abstract="Geben Sie die numerische ID ein, die Ihrem 4C-Markenprofil zugeordnet ist. Wenn Sie diese ID nicht haben, wenden Sie sich an Ihre 4C-Kundendienstperson."

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

### [!DNL Acast] {#acast}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_acast_client"
>title="Client-Name"
>abstract="Ihr Advertiser-Kontoname, wie er dem Zielpartner angezeigt werden soll. Verwenden Sie Ihren Unternehmensnamen. Verwenden Sie keine Leerzeichen oder Sonderzeichen."

### [!DNL Amobee] {#amobee}

### [!DNL Ampersand.tv] {#ampersand-tv}

### [!DNL Captify] {#captify}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_captify_client"
>title="Client-Name"
>abstract="Ihr Advertiser-Kontoname, wie er dem Zielpartner angezeigt werden soll. Verwenden Sie Ihren Unternehmensnamen. Verwenden Sie keine Leerzeichen oder Sonderzeichen."

### [!DNL Cardlytics] {#cardlytics}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_cardlytics_client"
>title="Client-Name"
>abstract="Ihr Advertiser-Kontoname, wie er dem Zielpartner angezeigt werden soll. Verwenden Sie Ihren Unternehmensnamen. Verwenden Sie keine Leerzeichen oder Sonderzeichen."

### [!DNL Disney (Hulu/ESPN/ABC)] {#disney}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_agreement"
>title="Vereinbarung über Zielbedingungen für Advertiser-Daten"
>abstract="Geben Sie `I AGREE` ein, um die Kenntnisnahme und das Einverständnis mit den Datenbedingungen für den Disney-Advertiser zu bestätigen."
>additional-url="https://www.disneyadvertising.com/ADVERTISER-DATA-DESTINATION-TERMS/" text="Vereinbarung lesen"

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_disney_client"
>title="Client-Name"
>abstract="Ihr Advertiser-Kontoname, wie er dem Zielpartner angezeigt werden soll. Verwenden Sie Ihren Unternehmensnamen. Verwenden Sie keine Leerzeichen oder Sonderzeichen."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_disney_email"
>title="Ihre E-Mail-Adresse"
>abstract="Geben Sie eine E-Mail-Adresse ein, die an eine Person gebunden ist. Diese E-Mail-Adresse dient als Signatur zum Vertrag mit den Datennutzerbedingungen. Diese E-Mail-Adresse wird bei Bedarf auch verwendet, um Sie zu kontaktieren."

Füllen Sie die unten stehenden Felder aus, um Details für das Ziel zu konfigurieren.

![Platform-UI-Bild, das die Kundendatenfelder für das Disney-Ziel anzeigt.](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-disney-fields.png)

* **[!UICONTROL Vereinbarung über Zielbedingungen für Advertising-Daten]**: Geben Sie ein in `I AGREE` zur Bestätigung der Bestätigung und Zustimmung zu den Disney Advertiser-Datenbedingungen.
* **[!UICONTROL Kundenname]**: Geben Sie Ihren Unternehmensnamen ein, wie er dem Zielpartner angezeigt werden soll.
* **[!UICONTROL Email-Adresse]**: Geben Sie eine E-Mail-Adresse ein, die an eine Person gebunden ist. Diese E-Mail-Adresse dient als Signatur zum Vertrag mit den Datennutzerbedingungen.

### [!DNL iHeartMedia] {#iheartmedia}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_iheartmedia_client"
>title="Client-Name"
>abstract="Ihr Advertiser-Kontoname, wie er dem Zielpartner angezeigt werden soll. Verwenden Sie Ihren Unternehmensnamen. Verwenden Sie keine Leerzeichen oder Sonderzeichen."

### [!DNL Index Exchange] {#index-exchange}

### [!DNL Magnite CTV Platform] {#magnite}

### [!DNL Magnite DV+ (Rubicon Project)] {#magnite-dv}

### [!DNL One Fox] {#fox}

### [!DNL Pandora] {#pandora}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_pandora_data_provider_name"
>title="Name des Daten-Providers"
>abstract="Der Name Ihres Unternehmens, wie er bei Pandora angezeigt werden soll. Der Name kann maximal 40 Kleinbuchstaben und alphanumerische Zeichen enthalten (z. B. Mein_Unternehmen)."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_pandora_rep_email"
>title="E-Mail-Adresse des Konto-Support-Kontakts"
>abstract="Die E-Mail-Adresse Ihres Pandora-Support-Kontakts. Diese Adresse wird verwendet, um Taxonomie-Aktualisierungen zu senden. Um mehrere Adressen einzugeben, trennen Sie sie durch Kommas."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_email"
>title="E-Mail Adresse"
>abstract="Diese Adresse wird verwendet, um Taxonomie-Aktualisierungen zu senden. Um mehrere Adressen einzugeben, trennen Sie sie durch Kommas."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_pandora_account_name"
>title="Kontoname"
>abstract="Der Name Ihres Pandora-Kontos. Wenden Sie sich an Ihren Pandora-Support-Kontakt, wenn Sie sich nicht sicher sind, welchen Kontonamen Sie haben. Verwenden Sie keine Leerzeichen oder Sonderzeichen."

### [!DNL Reddit] {#reddit}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_reddit_advertiser_id"
>title="Reddit-Advertiser-ID"
>abstract="Ihre Reddit-Advertiser-ID. Muss mit „t2_“ oder „a2_“ beginnen. Wenden Sie sich an Ihren Reddit-Support-Kontakt, wenn Sie Ihre Advertiser-ID nicht kennen."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_reddit_advertiser_name"
>title="Reddit-Advertiser-Name"
>abstract="Ihr Reddit-Advertiser-Name. Verwenden Sie keine Leerzeichen oder Sonderzeichen."

### Roku {#roku}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_roku_email"
>title="E-Mail-Adresse des Roku-Kontos"
>abstract="Geben Sie die mit Ihrem Roku-Konto verknüpfte E-Mail-Adresse ein."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_roku_representative_email"
>title="E-Mail-Adresse des Roku-Support-Kontakts"
>abstract="Geben Sie die E-Mail-Adresse Ihres Roku-Support-Kontakts ein. Diese Adresse wird verwendet, um Taxonomie-Aktualisierungen zu senden. Um mehrere Adressen einzugeben, trennen Sie sie durch Kommas."

Füllen Sie die unten stehenden Felder aus, um Details für das Ziel zu konfigurieren.

![Platform-UI-Bild, das die unterstützten Kennungen für das Roku-Ziel anzeigt.](../../assets/catalog/advertising/liveramp-distribution/liveramp-distribution-roku-fields.png)

* **[!UICONTROL E-Mail-Adresse des Roku-Kontos]**: Geben Sie die mit Ihrem Roku-Konto verknüpfte E-Mail-Adresse ein.
* **[!UICONTROL E-Mail-Adresse des Roku-Kundenbetreuers]**: Geben Sie die E-Mail-Adresse Ihres Roku-Kundenbetreuers ein. Um mehrere Adressen einzugeben, trennen Sie sie durch Kommas.

### [!DNL Spotify] {#spotify}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_spotify_client"
>title="Client-Name"
>abstract="Ihr Advertiser-Kontoname, wie er dem Zielpartner angezeigt werden soll. Verwenden Sie Ihren Unternehmensnamen. Verwenden Sie keine Leerzeichen oder Sonderzeichen."

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_spotify_account_token"
>title="Konto-Token"
>abstract="Eine alphanumerische Kennung, die Spotify informiert, wohin die Daten portiert werden sollen und dass Sie für die Verwendung dieses Workflows verifiziert sind. Wenden Sie sich an die Spotify-Kundenbetreuung, um dieses Token zu erhalten."

### [!DNL Taboola] {#taboola}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_taboola_rep_email"
>title="E-Mail-Adresse der Kundenbetreuung"
>abstract="Die E-Mail-Adresse der Taboola-Kundenbetreuung."

### [!DNL TargetSpot] {#targetspot}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_targetspot_client"
>title="Client-Name"
>abstract="Ihr Advertiser-Kontoname, wie er dem Zielpartner angezeigt werden soll. Verwenden Sie Ihren Unternehmensnamen. Verwenden Sie keine Leerzeichen oder Sonderzeichen."

### [!DNL Teads] {#teads}

### [!DNL WB Discovery] {#wb-discovery}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_distribution_wb_client"
>title="Client-Name"
>abstract="Ihr Advertiser-Kontoname, wie er dem Zielpartner angezeigt werden soll. Verwenden Sie Ihren Unternehmensnamen. Verwenden Sie keine Leerzeichen oder Sonderzeichen."

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Warnhinweisen zu Zielen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die [Zugriffskontrollberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Die [!DNL LiveRamp - Distribution] -Verbindung aktiviert Zielgruppen, die bereits über das [LiveRamp - Onboarding](liveramp-onboarding.md) Verbindung herzustellen.

Um Ihre Zielgruppen erfolgreich zu aktivieren, müssen Sie in diesem Schritt die **gleiche Zielgruppen** , die Sie bereits in LiveRamp integriert haben.

>[!IMPORTANT]
>
>Die Auswahl von Zielgruppen, die noch nicht in LiveRamp integriert wurden, Trigger nicht das Einstieg in die neuen Zielgruppen.

## Exportierte Daten/Datenexport validieren {#exported-data}

Um die Aktivierung Ihrer Zielgruppen zu überprüfen und zu überwachen, melden Sie sich bei Ihrem LiveRamp-Konto an und überprüfen Sie die Aktivierungsmetriken.

Wenden Sie sich bei Fragen zur Aktivierung der Zielgruppe an Ihren LiveRamp-Kundenbetreuer.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).

## Zusätzliche Ressourcen {#additional-resources}

Weitere Einzelheiten zur Konfiguration Ihres [!DNL LiveRamp - Onboarding]-Speichers finden Sie in der [offiziellen Dokumentation](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html).
