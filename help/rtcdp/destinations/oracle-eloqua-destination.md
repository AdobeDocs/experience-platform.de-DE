---
title: Oracle Eloqua-Ziel
seo-title: Oracle Eloqua-Ziel
description: Oracle Eloqua ist eine Software als Service-Plattform (SaaS) für die Marketingautomatisierung von Oracle, die B2B-Marketingexperten und -organisationen bei der Verwaltung von Marketingkampagnen und der Interessentenanwerbung für den Vertrieb unterstützen soll.
seo-description: Oracle Eloqua ist eine Software als Service-Plattform (SaaS) für die Marketingautomatisierung von Oracle, die B2B-Marketingexperten und -organisationen bei der Verwaltung von Marketingkampagnen und der Interessentenanwerbung für den Vertrieb unterstützen soll.
translation-type: tm+mt
source-git-commit: 3b9584cca8943c52bb3d8e4512d327d3dbeb9e04

---


# Oracle Eloqua

## Übersicht

[Eloqua](https://www.oracle.com/marketingcloud/products/marketing-automation/) ist eine Software als Service-Plattform (SaaS) für die Marketingautomatisierung von Oracle, die B2B-Marketingfachleuten und -organisationen helfen soll, Marketingkampagnen und die Interessentenanwerbung zu verwalten.

Um Segmentdaten an Oracle Eloqua zu senden, müssen Sie zunächst das Ziel[ in der Adobe Echtzeit-Kundendatenplattform ](#connect-destination)verbinden und dann einen Datenimport[ von Ihrem Speicherort nach Oracle Eloqua ](#import-data-into-eloqua)einrichten.

## Mit Ziel verbinden {#connect-destination}

1. Wählen Sie unter **[!UICONTROL Verbindungen > Ziele]** die Option Oracle Eloqua und dann **[!UICONTROL Connect-Ziel]**.

   ![Verbindung zu Eloqua](/help/rtcdp/destinations/assets/connect-oracle-eloqua.png)

1. Wählen Sie im Verbindungsziel-Assistenten den **[!UICONTROL Verbindungstyp]** für Ihren Speicherort aus. Bei Oracle Eloqua können Sie zwischen **SFTP mit Kennwort** und **SFTP mit SSH-Schlüssel** wählen. Füllen Sie die folgenden Informationen je nach Verbindungstyp aus und wählen Sie **[!UICONTROL Verbinden]**.

   ![Einrichten des Assistenten &quot;Eloqua&quot;](/help/rtcdp/destinations/assets/eloqua-wizard.png)

   Für **SFTP mit Passwortverbindungen** müssen Sie Domäne, Port, Benutzername und Passwort angeben.
Für **SFTP mit SSH-Key** -Verbindungen müssen Sie Domäne, Port, Benutzername und SSH-Schlüssel angeben.

   ![Eloqua-Informationen ausfüllen](/help/rtcdp/destinations/assets/eloqua-step2.png)

1. Geben Sie in den **Basisinformationen** die relevanten Informationen für Ihr Ziel wie folgt ein:
   * **Name**: Wählen Sie einen relevanten Namen für Ihr Ziel.
   * **Beschreibung**: Geben Sie eine Beschreibung für Ihr Ziel ein.
   * **Ordnerpfad**: Geben Sie den Pfad in Ihrem Speicherort an, in dem CDP Ihre Exportdaten in Echtzeit als CSV- oder tabulatorgetrennte Dateien hinterlegt.
   * **Dateiformat**: **CSV** oder **TAB_DELIMITED**. Wählen Sie das Dateiformat aus, das Sie an Ihren Speicherort exportieren möchten.
   ![Basisinformationen](/help/rtcdp/destinations/assets/eloqua-basic-information.png)

1. Klicken Sie auf **Erstellen** , nachdem Sie die Felder in den **Grundinformationen** ausgefüllt haben. Ihr Ziel ist nun verbunden und Sie können Segmente[ an das Ziel ](/help/rtcdp/destinations/activate-destinations.md)aktivieren.

## Zielattribute

Beim [Aktivieren von Segmenten](/help/rtcdp/destinations/activate-destinations.md) in das Oracle Eloqua-Ziel sollten Sie eine eindeutige Kennung aus Ihrem [Gewerkschaftsschema](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)auswählen. Wählen Sie den eindeutigen Bezeichner und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten. Weitere Informationen finden Sie unter [Auswählen, welche Schemafelder als Zielattribute in Ihren exportierten Dateien](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) in E-Mail-Marketing-Zielen verwendet werden sollen.

## Datenimport in Oracle Eloqua einrichten {#import-data-into-eloqua}

Nachdem Sie die Echtzeit-CDP mit Ihrem Amazon S3- oder SFTP-Speicher verbunden haben, müssen Sie den Datenimport von Ihrem Speicherort in Oracle Eloqua einrichten. Weitere Informationen dazu finden Sie unter [Importieren von Kontakten oder Konten](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) im Oracle Eloqua Help Center.