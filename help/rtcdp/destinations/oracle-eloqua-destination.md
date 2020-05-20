---
title: Oracle Eloqua-Ziel
seo-title: Oracle Eloqua-Ziel
description: Oracle Eloqua ist eine Software-as-a-Service (SaaS)-Plattform für Marketing-Automatisierung von Oracle, die B2B-Marketer und -Teams bei der Verwaltung von Marketing-Kampagnen und Lead-Generierung für den Vertrieb unterstützt.
seo-description: Oracle Eloqua ist eine Software-as-a-Service (SaaS)-Plattform für Marketing-Automatisierung von Oracle, die B2B-Marketer und -Teams bei der Verwaltung von Marketing-Kampagnen und Lead-Generierung für den Vertrieb unterstützt.
translation-type: tm+mt
source-git-commit: 50e6b39c1eb0bda4f3b30991515fb1c13fa9ff87
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 81%

---


# Oracle Eloqua

## Übersicht

[Eloqua](https://www.oracle.com/marketingcloud/products/marketing-automation/) ist eine Software-as-a-Service (SaaS)-Plattform für Marketing-Automatisierung von Oracle, die B2B-Marketer und -Teams bei der Verwaltung von Marketing-Kampagnen und Lead-Generierung für den Vertrieb unterstützt.

Um Segmentdaten an Oracle Eloqua zu senden, müssen Sie zunächst in der Echtzeit-Kundendatenplattform von Adobe das [Ziel verbinden](#connect-destination) und dann einen [Datenimport einrichten](#import-data-into-eloqua) von Ihrem Speicherort zu Oracle Eloqua.

## Mit Ziel verbinden {#connect-destination}

1. Wählen Sie unter **[!UICONTROL Verbindungen > Ziele]** die Option „Oracle Eloqua“ und dann **[!UICONTROL Ziel verbinden]**.

   ![Mit Eloqua verbinden](/help/rtcdp/destinations/assets/connect-oracle-eloqua.png)

2. In the **[!UICONTROL Authentication]** step, if you had previously set up a connection to your cloud storage destination, select **[!UICONTROL Existing Account]** and select one of your existing connections. Sie können auch &quot; **[!UICONTROL Neues Konto]** &quot;auswählen, um eine neue Verbindung einzurichten. Geben Sie die Anmeldeinformationen für die Kontoauthentifizierung ein und wählen Sie **[!UICONTROL Mit Ziel verbinden]**. Bei Oracle Eloqua können Sie zwischen **[!UICONTROL SFTP mit Passwort]** und **[!UICONTROL SFTP mit SSH-Schlüssel]** wählen. Fill in the information below, depending on your connection type, and select **[!UICONTROL Connect to destination]**.

   Bei Verbindungen des Typs **[!UICONTROL SFTP mit Passwort]** müssen Sie Domäne, Port, Benutzernamen und Kennwort angeben.
Bei Verbindungen des Typs **[!UICONTROL SFTP mit SSH-Schlüssel]** müssen Sie Domäne, Port, Benutzernamen und SSH-Schlüssel angeben.

   ![Assistent zum Einrichten von Eloqua](/help/rtcdp/destinations/assets/eloqua-authentication.png)

3. In the **[!UICONTROL Setup]** step, fill in the relevant information for your destination as shown below:
   * **[!UICONTROL Name]**: Wählen Sie einen passenden Namen für Ihr Ziel.
   * **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für Ihr Ziel ein.
   * **[!UICONTROL Ordnerpfad]**: Geben Sie den Pfad Ihres Speicherorts an, an dem die Echtzeit-Kundendatenplattform Ihre Exportdaten als CSV- oder tabulatorgetrennte Dateien hinterlegen wird.
   * **[!UICONTROL Dateiformat]**: **CSV** oder **TAB_DELIMITED**. Wählen Sie das Dateiformat aus, mit dem Sie an Ihren Speicherort exportieren möchten.
   ![Eloqua-Basisinformationen](/help/rtcdp/destinations/assets/eloqua-basic-information.png)

4. Klicken Sie auf Ziel **[!UICONTROL erstellen]** , nachdem Sie die oben stehenden Felder ausgefüllt haben. Your destination is now created and you can [activate segments](/help/rtcdp/destinations/activate-destinations.md) to the destination.

## Zielattribute

Beim [Aktivieren von Segmenten](/help/rtcdp/destinations/activate-destinations.md) für das Oracle Eloqua-Ziel empfehlen wir, eine eindeutige Kennung aus Ihrem [Vereinigungsschema](../../profile/home.md#profile-fragments-and-union-schemas) auszuwählen. Wählen Sie die eindeutige Kennung und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten. Weiterführende Informationen finden Sie unter [Auswählen, welche Schemafelder in Ihren exportierten Dateien als Zielattribute verwendet werden sollen](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) (in E-Mail-Marketing-Zielen).

## Datenimport in Oracle Eloqua einrichten {#import-data-into-eloqua}

Nachdem Sie die Echtzeit-Kundendatenplattform mit Ihrem Amazon S3- oder SFTP-Speicher verbunden haben, müssen Sie den Datenimport von Ihrem Speicherort zu Oracle Eloqua einrichten. Weiterführende Informationen finden Sie im Oracle Eloqua Help Center unter [Kontakte oder Konten importieren](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm).