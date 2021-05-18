---
keywords: E-Mail;E-Mail;E-Mail-Ziele;E-Mail-Ziele;Verkaufsforce;Verkaufsziel
title: Salesforce-Marketing Cloud-Verbindung
seo-description: Salesforce Marketing Cloud ist eine Digital-Marketing-Suite, die früher als ExactTarget bekannt war und mit der Sie Journeys für Besucher und Kunden erstellen und anpassen können, um deren Erlebnis zu personalisieren.
exl-id: e85049a7-eaed-4f8a-b670-9999d56928f8
source-git-commit: 70be44e919070df910d618af4507b600ad51123c
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 30%

---

# [!DNL Salesforce Marketing Cloud] connection

## Übersicht {#overview}

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/de/products/marketing-cloud/email-marketing/) ist eine Digital-Marketing-Suite, die früher als ExactTarget bekannt war und mit der Sie Journeys für Besucher und Kunden erstellen und anpassen können, um deren Erlebnis zu personalisieren.

Um Segmentdaten an [!DNL Salesforce Marketing Cloud] zu senden, müssen Sie zunächst [das Ziel](#connect-destination) in Plattform verbinden und dann [einen Datenimport](#import-data-into-salesforce) von Ihrer Datenspeicherung nach [!DNL Salesforce Marketing Cloud] einrichten.

## Exporttyp {#export-type}

**Profil-basiert** : Sie exportieren alle Segmentmitglieder zusammen mit den gewünschten Segmentfeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm &quot;Attribute auswählen&quot;des Arbeitsablaufs für die  [Ziel-Aktivierung](../../ui/activate-destinations.md#select-attributes) ausgewählt.

## IP-Adresse Zulassungsliste {#allow-list}

Beim Einrichten von E-Mail-Marketingzielen mit der SFTP-Datenspeicherung empfiehlt Adobe, bestimmte IP-Bereiche zu Ihrer Zulassungsliste hinzuzufügen.

Informationen zum Hinzufügen von IPs zur Zulassungsliste finden Sie unter [IP-Adresse für Cloud-Datenspeicherung-Ziele](../cloud-storage/ip-address-allow-list.md).

## Ziel verbinden {#connect-destination}

Wählen Sie unter **[!UICONTROL Verbindungen]** > **[!UICONTROL Ziele]** [!DNL Salesforce Marketing Cloud] und dann **[!UICONTROL Konfigurieren]**.

![Mit Salesforce verbinden](../../assets/catalog/email-marketing/salesforce/catalog.png)

Wenn Sie im Schritt **[!UICONTROL Konto]** bereits eine Verbindung zu Ihrem Cloud-Datenspeicherung-Ziel eingerichtet haben, wählen Sie **[!UICONTROL Vorhandenes Konto]** und wählen Sie eine Ihrer bestehenden Verbindungen aus. Sie können auch **[!UICONTROL Neues Konto]** auswählen, um eine neue Verbindung einzurichten. Geben Sie die Anmeldedaten für die Kontoauthentifizierung ein und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus. Für [!DNL Salesforce Marketing Cloud] können Sie zwischen **[!UICONTROL SFTP mit Kennwort]** und **[!UICONTROL SFTP mit SSH-Schlüssel]** wählen.

![Salesforce-Marketing Cloud-Konto verbinden](../../assets/catalog/email-marketing/salesforce/connection-type.png)

Füllen Sie die folgenden Informationen je nach Verbindungstyp aus und wählen Sie **[!UICONTROL Konfigurieren]**.

- Bei Verbindungen mit **[!UICONTROL SFTP mit Kennwort]** müssen Sie [!UICONTROL Domäne], [!UICONTROL Port], [!UICONTROL Benutzername] und [!UICONTROL Kennwort] angeben.
- Bei Verbindungen mit **[!UICONTROL SFTP mit SSH-Schlüssel]** müssen Sie [!UICONTROL Domäne], [!UICONTROL Port], [!UICONTROL Benutzername] und [!UICONTROL SSH-Schlüssel] angeben.

Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um unter dem Abschnitt **[!UICONTROL Schlüssel]** eine Verschlüsselung mit PGP/GPG zu Ihren exportierten Dateien hinzuzufügen. Ihr öffentlicher Schlüssel muss als [!DNL Base64] kodierte Zeichenfolge geschrieben werden.

![Salesforce-Informationen ausfüllen](../../assets/catalog/email-marketing/salesforce/account-info.png)

Geben Sie im Schritt **[!UICONTROL Authentifizierung]** die relevanten Informationen für Ihr Ziel wie folgt ein:
- **[!UICONTROL Name]**: Wählen Sie einen passenden Namen für Ihr Ziel.
- **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für Ihr Ziel ein.
- **[!UICONTROL Ordnerpfad]**: Geben Sie den Pfad in Ihrer Datenspeicherung an, in dem die Plattform Ihre Exportdaten als CSV- oder tabulatorgetrennte Dateien hinterlegt.
- **[!UICONTROL Dateiformat]**: **CSV** oder **TAB_DELIMITED**. Wählen Sie das Dateiformat aus, mit dem Sie an Ihren Speicherort exportieren möchten.
- **[!UICONTROL Marketingaktionen]**: Marketingaktionen geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von der Adobe definierten Marketingaktionen auswählen oder eine eigene Marketingaktion erstellen. Weitere Informationen zu Marketingaktionen finden Sie unter [Übersicht über Datenverwendungsrichtlinien](../../../data-governance/policies/overview.md).

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

![Salesforce-Basisinformationen](../../assets/catalog/email-marketing/salesforce/basic-information.png)

Klicken Sie auf **[!UICONTROL Ziel erstellen]**, nachdem Sie die oben stehenden Felder ausgefüllt haben. Ihr Ziel ist nun verbunden und Sie können für das Ziel [Segmente aktivieren](../../ui/activate-destinations.md).

## Aktivieren von Segmenten {#activate-segments}

Informationen zum Workflow für die Segmentaktivierung finden Sie unter [Profile und Segmente für ein Ziel aktivieren](../../ui/activate-destinations.md).

## Zielattribute {#destination-attributes}

Wenn Sie [segmente](../../ui/activate-destinations.md) in das [!DNL Salesforce Marketing Cloud]-Ziel aktivieren, empfiehlt Adobe, im [Vereinigung-Schema](../../../profile/home.md#profile-fragments-and-union-schemas) einen eindeutigen Bezeichner auszuwählen. Wählen Sie die eindeutige Kennung und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten. Weitere Informationen finden Sie unter [Wählen Sie, welche Schema-Felder als Zielattribute in den exportierten Dateien verwendet werden sollen](./overview.md#destination-attributes).

## Exportierte Daten {#exported-data}

Für [!DNL Salesforce Marketing Cloud]-Ziele erstellt Platform eine tabulatorgetrennte `.csv`-Datenspeicherung im angegebenen Speicherort. Weitere Informationen zu den Aktivierungen finden Sie unter [E-Mail-Marketing-Ziele und Cloud-Datenspeicherung-Ziele](../../ui/activate-destinations.md#esp-and-cloud-storage) im Tutorial zur Segmentbildung.

## Einrichten des Datenimports in [!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}

Nachdem Sie [!DNL Platform] mit der [!DNL SFTP]-Datenspeicherung verbunden haben, müssen Sie den Datenimport von Ihrem Speicherort in [!DNL Salesforce Marketing Cloud] einrichten. Informationen dazu finden Sie unter [Importieren von Abonnenten aus einer Datei](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5) in [!DNL Salesforce Help Center].
