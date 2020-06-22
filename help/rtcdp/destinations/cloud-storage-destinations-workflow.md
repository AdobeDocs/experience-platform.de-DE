---
title: Workflow für Cloud-Speicher-Ziele
seo-title: Workflow für Cloud-Speicher-Ziele
description: Anleitung zum Herstellen einer Verbindung zu Ihren Cloud-Speichern
seo-description: Anleitung zum Herstellen einer Verbindung zu Ihren Cloud-Speichern
translation-type: tm+mt
source-git-commit: 3c598454a868139b7604c5c7ca2b98fa0f1bb961
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 49%

---


# Workflow zum Erstellen von Cloud-Speicher-Zielen

## Übersicht

Auf dieser Seite wird erläutert, wie Sie in der Adobe-Echtzeit-Kundendatenplattform eine Verbindung zu Cloud-Speichern herstellen können.

1. Wählen Sie unter **[!UICONTROL Verbindungen > Ziele]** Ihr bevorzugtes Cloud-Speicher-Ziel und wählen Sie dann **[!UICONTROL Ziel verbinden]**.

   ![Verbindung zum Cloud-Speicher-Ziel herstellen](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

2. Wenn Sie im Schritt **[!UICONTROL Authentifizieren]** zuvor eine Verbindung zu Ihrem Cloud-Speicher-Ziel eingerichtet haben, wählen Sie **[!UICONTROL Vorhandenes Konto]** und wählen Sie Ihre bestehende Verbindung aus. Sie können auch **[!UICONTROL Neues Konto]** auswählen, um eine neue Verbindung zu Ihrem Cloud-Speicher-Ziel einzurichten. Geben Sie die Anmeldeinformationen für die Kontoauthentifizierung ein und wählen Sie **[!UICONTROL Mit Ziel verbinden]**. <br> Weitere Informationen zu den Anmeldeinformationen im Schritt [Authentifizierung finden Sie unter](/help/rtcdp/destinations/amazon-s3-destination.md) Amazon S3 [-Ziel, Ziel der](/help/rtcdp/destinations/amazon-kinesis-destination.md) Amazon-Kinesis [-API, Ziel der](/help/rtcdp/destinations/azure-event-hubs-destination.md) Amazon-Ereignis-Hubs [und](/help/rtcdp/destinations/sftp-destination.md) SFTP **-Ziel** .

   >[!NOTE]
   >
   >Die Adobe Echtzeit-CDP unterstützt die Berechtigungsprüfung im Authentifizierungsprozess und zeigt eine Fehlermeldung an, wenn Sie falsche Anmeldeinformationen für Ihren Cloud-Speicher eingeben. Dadurch wird sichergestellt, dass Sie den Workflow nicht mit falschen Anmeldeinformationen abschließen.

   ![Mit dem Cloud-Speicher-Ziel verbinden – Authentifizierungsschritt](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

3. Geben Sie im Schritt **[!UICONTROL Einrichten]** einen **[!UICONTROL Namen]** und eine **[!UICONTROL Beschreibung]** für die Aktivierung ein. <br>
In diesem Schritt können Sie auch einen beliebigen **[!UICONTROL Marketing-Anwendungsfall]** auswählen, der für dieses Ziel gelten soll. Anwendungsfälle für das Marketing geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von Adobe definierten Anwendungsfällen für das Marketing auswählen oder einen eigenen Anwendungsfall für das Marketing erstellen. Weitere Informationen zu Anwendungsfällen für das Marketing finden Sie auf der Seite [Datenverwaltung in Echtzeit-CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) . Informationen zu den einzelnen von Adobe definierten Anwendungsfällen für Marketing finden Sie in der Übersicht über die [Datenverwendungsrichtlinien](/help/data-governance/policies/overview.md#core-actions). <br>
Geben Sie für Amazon S3-Ziele den **[!UICONTROL Behälternamen]** und den **[!UICONTROL Ordnerpfad]** in das Ziel der Cloud-Datenspeicherung ein, an das die Dateien gesendet werden sollen. Wählen Sie **[!UICONTROL Ziel erstellen]**, nachdem Sie die obigen Felder ausgefüllt haben.

   ![Verbindung mit Amazon S3 Cloud-Datenspeicherung-Ziel - Authentifizierungsschritt](/help/rtcdp/destinations/assets/amazon-s3-setup-step.png)

   Geben Sie für SFTP-Ziele den **[!UICONTROL Ordnerpfad]** ein, unter dem die Dateien bereitgestellt werden sollen. Wählen Sie **[!UICONTROL Ziel erstellen]**, nachdem Sie die obigen Felder ausgefüllt haben.

   ![Verbindungsziel für die SFTP-Cloud-Datenspeicherung - Authentifizierungsschritt](/help/rtcdp/destinations/assets/sftp-destinations-setup-step.png)

   Geben Sie für Amazon Kinesis-Ziele den Namen Ihres vorhandenen Datenstroms in Ihrem [!DNL Amazon Kinesis] Konto ein. Adobe Echtzeit-CDP exportiert Daten in diesen Stream. Wählen Sie **[!UICONTROL Ziel erstellen]**, nachdem Sie die obigen Felder ausgefüllt haben.

   ![Verbindung zum Ziel der Kinesis Cloud-Datenspeicherung herstellen - Authentifizierungsschritt](/help/rtcdp/destinations/assets/kinesis-destinations-setup-step.png)

   Geben Sie für die FLUVAN-Ereignis-Hubs-Ziele den Namen Ihres vorhandenen Datenstroms in Ihrem [!DNL Amazon Kinesis] Konto ein. Adobe Echtzeit-CDP exportiert Daten in diesen Stream. Wählen Sie **[!UICONTROL Ziel erstellen]**, nachdem Sie die obigen Felder ausgefüllt haben.

   ![Verbindung zum Ziel der Kinesis Cloud-Datenspeicherung herstellen - Authentifizierungsschritt](/help/rtcdp/destinations/assets/eventhubs-destinations-setup-step.png)

4. Ihr Ziel wird jetzt erstellt. Sie können **[!UICONTROL Speichern und beenden]** auswählen, wenn Sie Segmente später aktivieren möchten, oder Sie können **[!UICONTROL Weiter]** wählen, um den Workflow fortzusetzen und Segmente zur Aktivierung auszuwählen. In either case, see the next section, [Activate segments](#activate-segments), for the rest of the workflow to export data.

## Aktivieren von Segmenten {#activate-segments}

Informationen zum Workflow für die Segmentaktivierung finden Sie unter [Profile und Segmente für ein Ziel aktivieren](/help/rtcdp/destinations/activate-destinations.md).