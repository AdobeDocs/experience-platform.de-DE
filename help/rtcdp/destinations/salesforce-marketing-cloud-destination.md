---
title: Salesforce Marketing Cloud
seo-title: Salesforce Marketing Cloud
description: Salesforce Marketing Cloud ist eine Digital-Marketing-Suite, die früher als ExactTarget bekannt war und mit der Sie Journeys für Besucher und Kunden erstellen und anpassen können, um deren Erlebnis zu personalisieren.
seo-description: Salesforce Marketing Cloud ist eine Digital-Marketing-Suite, die früher als ExactTarget bekannt war und mit der Sie Journeys für Besucher und Kunden erstellen und anpassen können, um deren Erlebnis zu personalisieren.
translation-type: ht
source-git-commit: 3b9584cca8943c52bb3d8e4512d327d3dbeb9e04

---


# Salesforce Marketing Cloud

## Übersicht

[Salesforce Marketing Cloud](https://www.salesforce.com/products/marketing-cloud/email-marketing/) ist eine Digital-Marketing-Suite, die früher als ExactTarget bekannt war und mit der Sie Journeys für Besucher und Kunden erstellen und anpassen können, um deren Erlebnis zu personalisieren.

Um Segmentdaten an Salesforce Marketing Cloud zu senden, müssen Sie zunächst in der Echtzeit-Kundendatenplattform von Adobe das [Ziel verbinden](#connect-destination) und dann einen [Datenimport einrichten](#import-data-into-salesforce) von Ihrem Speicherort zu Salesforce Marketing Cloud.

## Ziel verbinden {#connect-destination}

1. Wählen Sie unter **[!UICONTROL Verbindungen > Ziele]** die Option „Salesforce Marketing Cloud“ und wählen Sie dann **[!UICONTROL Ziel verbinden]**.

   ![Mit Salesforce verbinden](/help/rtcdp/destinations/assets/connect-salesforce.png)

1. Wählen Sie im Zielverbindungsassistenten den **[!UICONTROL Verbindungstyp]** für Ihren Speicherort aus. Bei Salesforce Marketing Cloud können Sie zwischen **SFTP mit Passwort** und **SFTP mit SSH-Schlüssel** wählen. Füllen Sie je nach Verbindungstyp die folgenden Informationen aus und wählen Sie **[!UICONTROL Verbinden]**.

   ![Assistent zum Einrichten von Salesforce](/help/rtcdp/destinations/assets/salesforce-step1.png)

   Bei Verbindungen des Typs **SFTP mit Passwort** müssen Sie Domäne, Port, Benutzernamen und Kennwort angeben.
Bei Verbindungen des Typs **SFTP mit SSH-Schlüssel** müssen Sie Domäne, Port, Benutzernamen und SSH-Schlüssel angeben.

   ![Salesforce-Informationen ausfüllen](/help/rtcdp/destinations/assets/salesforce-wizard.png)

1. Geben Sie unter **Grundlegende Informationen** die entsprechenden Informationen für Ihr Ziel ein, wie nachfolgend dargestellt:
   * **Name**: Wählen Sie einen passenden Namen für Ihr Ziel.
   * **Beschreibung**: Geben Sie eine Beschreibung für Ihr Ziel ein.
   * **Ordnerpfad**: Geben Sie den Pfad Ihres Speicherorts an, an dem die Echtzeit-Kundendatenplattform Ihre Exportdaten als CSV- oder tabulatorgetrennte Dateien hinterlegen wird.
   * **Dateiformat**: **CSV** oder **TAB_DELIMITED**. Wählen Sie das Dateiformat aus, mit dem Sie an Ihren Speicherort exportieren möchten.
   ![Salesforce-Basisinformationen](/help/rtcdp/destinations/assets/salesforce-basic-information.png)

1. Klicken Sie auf **Erstellen**, nachdem Sie die Felder unter **Grundlegende Informationen** ausgefüllt haben. Ihr Ziel ist nun verbunden und Sie können für das Ziel [Segmente aktivieren](/help/rtcdp/destinations/activate-destinations.md).

## Zielattribute {#destination-attributes}

Beim [Aktivieren von Segmenten](/help/rtcdp/destinations/activate-destinations.md) für das Salesforce Marketing Cloud-Ziel empfehlen wir, eine eindeutige Kennung aus Ihrem [Vereinigungsschema](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md) auszuwählen. Wählen Sie die eindeutige Kennung und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten. Weiterführende Informationen finden Sie unter [Auswählen, welche Schemafelder in Ihren exportierten Dateien als Zielattribute verwendet werden sollen](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) (in E-Mail-Marketing-Zielen).

## Datenimport in Salesforce Marketing Cloud einrichten {#import-data-into-salesforce}

Nachdem Sie die Echtzeit-Kundendatenplattform mit Ihrem Amazon S3- oder SFTP-Speicher verbunden haben, müssen Sie den Datenimport von Ihrem Speicherort zu Salesforce Marketing Cloud einrichten. Weiterführende Informationen finden Sie im Salesforce Help Center unter [Abonnenten aus einer Datei in Marketing Cloud importieren](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5).