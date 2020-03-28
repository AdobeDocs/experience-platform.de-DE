---
title: Oracle Eloqua-Ziel
seo-title: Oracle Eloqua-Ziel
description: Oracle Eloqua ist eine Software-as-a-Service (SaaS)-Plattform für Marketing-Automatisierung von Oracle, die B2B-Marketer und -Teams bei der Verwaltung von Marketing-Kampagnen und Lead-Generierung für den Vertrieb unterstützt.
seo-description: Oracle Eloqua ist eine Software-as-a-Service (SaaS)-Plattform für Marketing-Automatisierung von Oracle, die B2B-Marketer und -Teams bei der Verwaltung von Marketing-Kampagnen und Lead-Generierung für den Vertrieb unterstützt.
translation-type: tm+mt
source-git-commit: 336aa90cf1e059a92a36dd0ef3222ef6a6f5123b

---


# Oracle Eloqua

## Übersicht

[Eloqua](https://www.oracle.com/marketingcloud/products/marketing-automation/) ist eine Software-as-a-Service (SaaS)-Plattform für Marketing-Automatisierung von Oracle, die B2B-Marketer und -Teams bei der Verwaltung von Marketing-Kampagnen und Lead-Generierung für den Vertrieb unterstützt.

Um Segmentdaten an Oracle Eloqua zu senden, müssen Sie zunächst in der Echtzeit-Kundendatenplattform von Adobe das [Ziel verbinden](#connect-destination) und dann einen [Datenimport einrichten](#import-data-into-eloqua) von Ihrem Speicherort zu Oracle Eloqua.

## Mit Ziel verbinden {#connect-destination}

1. Wählen Sie **[!UICONTROL Connections > Destinations]** in Oracle Eloqua und dann **[!UICONTROL Connect destination]**.

   ![Mit Eloqua verbinden](/help/rtcdp/destinations/assets/connect-oracle-eloqua.png)

2. Wenn Sie zuvor eine Verbindung zum Ziel Ihrer Cloud-Datenspeicherung eingerichtet haben, wählen Sie **[!UICONTROL Authentication]** im Schritt eine der vorhandenen Verbindungen aus **[!UICONTROL Existing Account]** und wählen Sie sie aus. Sie können auch eine neue Verbindung einrichten **[!UICONTROL New Account]** . Geben Sie Ihre Kontoauthentifizierungsdaten ein und wählen Sie **[!UICONTROL Connect to destination]**. Bei Oracle Eloqua können Sie zwischen **[!UICONTROL SFTP with Password]** und **[!UICONTROL SFTP with SSH Key]** wählen. Fill in the information below, depending on your connection type, and select **[!UICONTROL Connect to destination]**.

   For **[!UICONTROL SFTP with Password]** connections, you must provide Domain, Port, Username, and Password.
Für **[!UICONTROL SFTP with SSH Key]** Verbindungen müssen Sie Domäne, Anschluss, Benutzername und SSH-Schlüssel angeben.

   ![Assistent zum Einrichten von Eloqua](/help/rtcdp/destinations/assets/eloqua-authentication.png)

3. In the **[!UICONTROL Setup]** step, fill in the relevant information for your destination as shown below:
   * **[!UICONTROL Name]**: Wählen Sie einen passenden Namen für Ihr Ziel.
   * **[!UICONTROL Description]**: Geben Sie eine Beschreibung für Ihr Ziel ein.
   * **[!UICONTROL Folder Path]**: Geben Sie den Pfad in Ihrer Datenspeicherung an, in dem CDP Ihre Exportdaten als CSV- oder tabulatorgetrennte Dateien hinterlegt.
   * **[!UICONTROL File Format]**: **CSV** oder **TAB_DELIMITED**. Wählen Sie das Dateiformat aus, mit dem Sie an Ihren Speicherort exportieren möchten.
   ![Eloqua-Basisinformationen](/help/rtcdp/destinations/assets/eloqua-basic-information.png)

4. Klicken Sie auf **[!UICONTROL Create destination]** , nachdem Sie die oben stehenden Felder ausgefüllt haben. Your destination is now created and you can [activate segments](/help/rtcdp/destinations/activate-destinations.md) to the destination.

## Zielattribute

Beim [Aktivieren von Segmenten](/help/rtcdp/destinations/activate-destinations.md) für das Oracle Eloqua-Ziel empfehlen wir, eine eindeutige Kennung aus Ihrem [Vereinigungsschema](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md) auszuwählen. Wählen Sie die eindeutige Kennung und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten. Weiterführende Informationen finden Sie unter [Auswählen, welche Schemafelder in Ihren exportierten Dateien als Zielattribute verwendet werden sollen](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) (in E-Mail-Marketing-Zielen).

## Datenimport in Oracle Eloqua einrichten {#import-data-into-eloqua}

Nachdem Sie die Echtzeit-Kundendatenplattform mit Ihrem Amazon S3- oder SFTP-Speicher verbunden haben, müssen Sie den Datenimport von Ihrem Speicherort zu Oracle Eloqua einrichten. Weiterführende Informationen finden Sie im Oracle Eloqua Help Center unter [Kontakte oder Konten importieren](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm).