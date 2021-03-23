---
keywords: E-Mail;E-Mail;E-Mail-Ziele;oracle eloqua;oracle
title: Oracle Eloqua-Verbindung
description: Oracle Eloqua ist eine Software-as-a-Service (SaaS)-Plattform für Marketing-Automatisierung von Oracle, die B2B-Marketer und -Teams bei der Verwaltung von Marketing-Kampagnen und Lead-Generierung für den Vertrieb unterstützt.
translation-type: tm+mt
source-git-commit: 02754055e2be8a45a0699386cb559dad8f25717c
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 31%

---


# [!DNL Oracle Eloqua] connection

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/)[!DNL Oracle] ist eine Software-as-a-Service (SaaS)-Plattform für Marketing-Automatisierung von , die B2B-Marketer und -Teams bei der Verwaltung von Marketing-Kampagnen und Lead-Generierung für den Vertrieb unterstützt.

Um Segmentdaten an [!DNL Oracle Eloqua] zu senden, müssen Sie zunächst [das Ziel](#connect-destination) in Adobe Experience Platform verbinden und dann [einen Datenimport](#import-data-into-eloqua) von Ihrem Speicherort in [!DNL Oracle Eloqua] einrichten.

## Exporttyp {#export-type}

**Profil-basiert** : Sie exportieren alle Segmentmitglieder zusammen mit den gewünschten Segmentfeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm &quot;Attribute auswählen&quot;des Arbeitsablaufs für die  [Ziel-Aktivierung](../../ui/activate-destinations.md#select-attributes) ausgewählt.

## Mit Ziel verbinden {#connect-destination}

Wählen Sie unter **[!UICONTROL Verbindungen]** > **[!UICONTROL Ziele]** [!DNL Oracle Eloqua] und dann **[!UICONTROL Konfigurieren]**.

>[!NOTE]
>
>Wenn bereits eine Verbindung zu diesem Ziel besteht, wird auf der Zielkarte die Schaltfläche **[!UICONTROL Aktivieren]** angezeigt. Weitere Informationen zum Unterschied zwischen [!UICONTROL Aktivieren] und [!UICONTROL Konfigurieren] finden Sie im Abschnitt [Katalog](../../ui/destinations-workspace.md#catalog) der Dokumentation zum Zielarbeitsbereich.

![Mit Eloqua verbinden](../../assets/catalog/email-marketing/oracle-eloqua/catalog.png)

Wenn Sie im Schritt **[!UICONTROL Konto]** bereits eine Verbindung zu Ihrem Cloud-Datenspeicherung-Ziel eingerichtet haben, wählen Sie **[!UICONTROL Vorhandenes Konto]** und wählen Sie eine Ihrer bestehenden Verbindungen aus. Sie können auch **[!UICONTROL Neues Konto]** auswählen, um eine neue Verbindung einzurichten. Geben Sie die Anmeldedaten für die Kontoauthentifizierung ein und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus. Für [!DNL Oracle Eloqua] können Sie zwischen **[!UICONTROL SFTP mit Kennwort]** und **[!UICONTROL SFTP mit SSH-Schlüssel]** wählen.

![Eloqua-Konto verbinden](../../assets/catalog/email-marketing/oracle-eloqua/connection-type.png)

Füllen Sie je nach Verbindungstyp die folgenden Informationen aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

- Bei Verbindungen mit **[!UICONTROL SFTP mit Kennwort]** müssen Sie [!UICONTROL Domäne], [!UICONTROL Port], [!UICONTROL Benutzername] und [!UICONTROL Kennwort] angeben.
- Bei Verbindungen mit **[!UICONTROL SFTP mit SSH-Schlüssel]** müssen Sie [!UICONTROL Domäne], [!UICONTROL Port], [!UICONTROL Benutzername] und [!UICONTROL SSH-Schlüssel] angeben.

Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um unter dem Abschnitt **[!UICONTROL Schlüssel]** eine Verschlüsselung mit PGP/GPG zu Ihren exportierten Dateien hinzuzufügen. Ihr öffentlicher Schlüssel muss als [!DNL Base64] kodierte Zeichenfolge geschrieben werden.

![Eloqua-Verbindung zum Ziel](../../assets/catalog/email-marketing/oracle-eloqua/account-info.png)

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

![Eloqua-Basisinformationen](../../assets/catalog/email-marketing/oracle-eloqua/basic-information.png)

Klicken Sie auf **[!UICONTROL Ziel erstellen]**, nachdem Sie die oben stehenden Felder ausgefüllt haben. Ihr Ziel wird jetzt erstellt und Sie können [Segmente](../../ui/activate-destinations.md) bis zum Ziel aktivieren.

## Aktivieren von Segmenten {#activate-segments}

Informationen zum Workflow für die Segmentaktivierung finden Sie unter [Profile und Segmente für ein Ziel aktivieren](../../ui/activate-destinations.md).

## Zielattribute {#destination-attributes}

Wenn Sie [segmente](../../ui/activate-destinations.md) in das [!DNL Oracle Eloqua]-Ziel aktivieren, empfiehlt Adobe, im [Vereinigung-Schema](../../../profile/home.md#profile-fragments-and-union-schemas) einen eindeutigen Bezeichner auszuwählen. Wählen Sie die eindeutige Kennung und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten. Weitere Informationen finden Sie unter [Wählen Sie, welche Schema-Felder als Zielattribute in den exportierten Dateien verwendet werden sollen](./overview.md#destination-attributes).

## Exportierte Daten {#exported-data}

Für [!DNL Oracle Eloqua]-Ziele erstellt Platform eine tabulatorgetrennte `.txt`- oder `.csv`-Datenspeicherung im angegebenen Speicherort. Weitere Informationen zu den Aktivierungen finden Sie unter [E-Mail-Marketing-Ziele und Cloud-Datenspeicherung-Ziele](../../ui/activate-destinations.md#esp-and-cloud-storage) im Tutorial zur Segmentbildung.

## Einrichten des Datenimports in [!DNL Oracle Eloqua] {#import-data-into-eloqua}

Nachdem Sie [!DNL Platform] mit Ihrer SFTP-Datenspeicherung verbunden haben, müssen Sie den Datenimport von Ihrem Speicherort in [!DNL Oracle Eloqua] einrichten. Weitere Informationen dazu finden Sie unter [Importieren von Kontakten oder Konten](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) in [!DNL Oracle Eloqua Help Center].