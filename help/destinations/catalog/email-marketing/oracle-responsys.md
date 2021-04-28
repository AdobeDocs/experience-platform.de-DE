---
keywords: E-Mail;E-Mail;E-Mail;E-Mail-Ziele;Ziel der oracle-Antwort
title: Oracle Responsys-Verbindung
description: Responsys ist ein Enterprise-E-Mail-Marketing-Tool für kanalübergreifende Marketing-Kampagnen, das von Oracle angeboten wird und der Personalisierung von Interaktionen über E-Mail, Mobile, Display und Social Media hinweg dient.
exl-id: 70f2f601-afee-4315-bf7a-ed2c92397ebe
translation-type: tm+mt
source-git-commit: 29b4eaca06e2f1032584a0b4720490934a6e1fa7
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 28%

---

# [!DNL Oracle Responsys] connection

## Übersicht {#overview}

[Responsys](https://www.oracle.com/cx/marketing/campaign-management/)[!DNL Oracle] ist ein Enterprise-E-Mail-Marketing-Tool für kanalübergreifende Marketing-Kampagnen, das von angeboten wird und der Personalisierung von Interaktionen über E-Mail, Mobile, Display und Social Media hinweg dient.

Um Segmentdaten an [!DNL Oracle Responsys] zu senden, müssen Sie zunächst [eine Verbindung zum Ziel](#connect-destination) in Adobe Experience Platform herstellen und dann [einen Datenimport](#import-data-into-responsys) von Ihrem Speicherort in [!DNL Oracle Responsys] einrichten.

## Exporttyp {#export-type}

**Profil-basiert** : Sie exportieren alle Segmentmitglieder zusammen mit den gewünschten Segmentfeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm &quot;Attribute auswählen&quot;des Arbeitsablaufs für die  [Ziel-Aktivierung](../../ui/activate-destinations.md#select-attributes) ausgewählt.

## IP-Adresse Zulassungsliste {#allow-list}

Beim Einrichten von E-Mail-Marketingzielen mit der SFTP-Datenspeicherung empfiehlt Adobe, bestimmte IP-Bereiche zu Ihrer Zulassungsliste hinzuzufügen.

Informationen zum Hinzufügen von IPs zur Zulassungsliste finden Sie unter [IP-Adresse für Cloud-Datenspeicherung-Ziele](../cloud-storage/ip-address-allow-list.md).

## Ziel verbinden {#connect-destination}

Wählen Sie unter **[!UICONTROL Verbindungen]** > **[!UICONTROL Ziele]** [!DNL Oracle Responsys] und dann **[!UICONTROL Verbindungsziel]**.

![Mit Responsys verbinden](../../assets/catalog/email-marketing/oracle-responsys/catalog.png)

Wenn Sie im Schritt **[!UICONTROL Konto]** bereits eine Verbindung zu Ihrem Cloud-Datenspeicherung-Ziel eingerichtet haben, wählen Sie **[!UICONTROL Vorhandenes Konto]** und wählen Sie eine Ihrer bestehenden Verbindungen aus. Sie können auch **[!UICONTROL Neues Konto]** auswählen, um eine neue Verbindung einzurichten. Geben Sie die Anmeldedaten für die Kontoauthentifizierung ein und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus. Für [!DNL Oracle Responsys] können Sie zwischen **[!UICONTROL SFTP mit Kennwort]** und **[!UICONTROL SFTP mit SSH-Schlüssel]** wählen.

![Konto &quot;Antworten verbinden&quot;](../../assets/catalog/email-marketing/oracle-responsys/connection-type.png)

Füllen Sie die folgenden Informationen je nach Verbindungstyp aus und wählen Sie **[!UICONTROL Konfigurieren]**.

- Bei Verbindungen mit **[!UICONTROL SFTP mit Kennwort]** müssen Sie [!UICONTROL Domäne], [!UICONTROL Port], [!UICONTROL Benutzername] und [!UICONTROL Kennwort] angeben.
- Bei Verbindungen mit **[!UICONTROL SFTP mit SSH-Schlüssel]** müssen Sie [!UICONTROL Domäne], [!UICONTROL Port], [!UICONTROL Benutzername] und [!UICONTROL SSH-Schlüssel] angeben.

Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um unter dem Abschnitt **[!UICONTROL Schlüssel]** eine Verschlüsselung mit PGP/GPG zu Ihren exportierten Dateien hinzuzufügen. Ihr öffentlicher Schlüssel muss als [!DNL Base64] kodierte Zeichenfolge geschrieben werden.

![Responsys-Informationen ausfüllen](../../assets/catalog/email-marketing/oracle-responsys/account-info.png)

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

![Responsys-Basisinformationen](../../assets/catalog/email-marketing/oracle-responsys/basic-information.png)

Klicken Sie auf **[!UICONTROL Ziel erstellen]**, nachdem Sie die oben stehenden Felder ausgefüllt haben. Ihr Ziel ist nun verbunden und Sie können für das Ziel [Segmente aktivieren](../../ui/activate-destinations.md).

## Aktivieren von Segmenten {#activate-segments}

Informationen zum Workflow für die Segmentaktivierung finden Sie unter [Profile und Segmente für ein Ziel aktivieren](../../ui/activate-destinations.md).

## Zielattribute {#destination-attributes}

Wenn Sie [segmente](../../ui/activate-destinations.md) in das [!DNL Oracle Responsys]-Ziel aktivieren, empfiehlt Adobe, im [Vereinigung-Schema](../../../profile/home.md#profile-fragments-and-union-schemas) einen eindeutigen Bezeichner auszuwählen. Wählen Sie die eindeutige Kennung und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten. Weitere Informationen finden Sie unter [Wählen Sie, welche Schema-Felder als Zielattribute in den exportierten Dateien verwendet werden sollen](./overview.md#destination-attributes).

## Exportierte Daten {#exported-data}

Für [!DNL Oracle Responsys]-Ziele erstellt Platform eine tabulatorgetrennte `.txt`- oder `.csv`-Datenspeicherung im angegebenen Speicherort. Weitere Informationen zu den Aktivierungen finden Sie unter [E-Mail-Marketing-Ziele und Cloud-Datenspeicherung-Ziele](../../ui/activate-destinations.md#esp-and-cloud-storage) im Tutorial zur Segmentbildung.

## Einrichten des Datenimports in [!DNL Oracle Responsys] {#import-data-into-responsys}

Nachdem Sie [!DNL Platform] mit Ihrer SFTP-Datenspeicherung verbunden haben, müssen Sie den Datenimport von Ihrem Speicherort in [!DNL Oracle Responsys] einrichten. Weitere Informationen dazu finden Sie unter [Importieren von Kontakten oder Konten](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) in [!DNL Oracle Responsys Help Center].
