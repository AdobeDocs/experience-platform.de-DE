---
keywords: cloud storage destination;cloud storage
title: Workflow für Cloud-Speicher-Ziele
seo-title: Workflow für Cloud-Speicher-Ziele
type: Tutorial
description: Anleitung zum Herstellen einer Verbindung zu Ihren Cloud-Speichern
seo-description: Anleitung zum Herstellen einer Verbindung zu Ihren Cloud-Speichern
translation-type: tm+mt
source-git-commit: 7903d6c715747dfc298a5e4a4615d8ecbbe5d359
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 39%

---


# Workflow zum Erstellen von Cloud-Speicher-Zielen

## Übersicht

Auf dieser Seite wird erläutert, wie Sie eine Verbindung zu Cloud-Datenspeicherung in der Echtzeit-Kundendatenplattform herstellen können.

1. In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, select your preferred cloud storage destination, then select **[!UICONTROL Configure]**.

   ![Verbindung zum Cloud-Speicher-Ziel herstellen](./assets/connect-cloud-destination.png)

   >[!NOTE]
   >
   >Wenn bereits eine Verbindung zu diesem Ziel besteht, wird auf der Zielkarte die Schaltfläche &quot; **[!UICONTROL Aktivieren]** &quot;angezeigt. Weitere Informationen zum Unterschied zwischen **[!UICONTROL Aktivieren]** und **[!UICONTROL Konfigurieren]** finden Sie im Abschnitt &quot; [Katalog](/help/rtcdp/destinations/destinations-workspace.md#catalog) &quot;der Dokumentation zum Zielarbeitsbereich.

2. Wenn Sie im Schritt **[!UICONTROL Authentifizieren]** zuvor eine Verbindung zu Ihrem Cloud-Speicher-Ziel eingerichtet haben, wählen Sie **[!UICONTROL Vorhandenes Konto]** und wählen Sie Ihre bestehende Verbindung aus. Sie können auch **[!UICONTROL Neues Konto]** auswählen, um eine neue Verbindung zu Ihrem Cloud-Speicher-Ziel einzurichten. Geben Sie die Anmeldedaten für die Kontoauthentifizierung ein und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus. Optional können Sie im Abschnitt **[!UICONTROL Encryption PGP/GPG]** Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um eine Verschlüsselung mit PGP/GPG zu Ihren exportierten Dateien hinzuzufügen. Beachten Sie, dass dieser öffentliche Schlüssel als Base64-kodierte Zeichenfolge geschrieben werden **muss** . <br> Weitere Informationen zur Eingabe von Anmeldeinformationen im Schritt [Authentifizierung finden Sie unter](/help/rtcdp/destinations/amazon-s3-destination.md) Amazon S3 [[!DNL Amazon Kinesis]](/help/rtcdp/destinations/amazon-kinesis-destination.md) -Ziel, [[!DNL Azure Event Hubs]](/help/rtcdp/destinations/azure-event-hubs-destination.md) Ziel, [Ziel und](/help/rtcdp/destinations/sftp-destination.md) SFTP **-Ziel** .

   >[!NOTE]
   >
   >Die Adobe Echtzeit-CDP unterstützt die Berechtigungsprüfung im Authentifizierungsprozess und zeigt eine Fehlermeldung an, wenn Sie falsche Anmeldeinformationen für Ihren Cloud-Speicher eingeben. Dadurch wird sichergestellt, dass Sie den Workflow nicht mit falschen Anmeldeinformationen abschließen.

   ![Mit dem Cloud-Speicher-Ziel verbinden – Authentifizierungsschritt](./assets/csdw/destination-account.png)

3. Geben Sie im Schritt **[!UICONTROL Einrichten]** einen **[!UICONTROL Namen]** und eine **[!UICONTROL Beschreibung]** für die Aktivierung ein. <br>
In diesem Schritt können Sie auch einen beliebigen **[!UICONTROL Marketing-Anwendungsfall]** auswählen, der für dieses Ziel gelten soll. Anwendungsfälle für das Marketing geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von der Adobe definierten Anwendungsfällen für das Marketing auswählen oder einen eigenen Anwendungsfall für das Marketing erstellen. Weitere Informationen zu Anwendungsfällen für das Marketing finden Sie auf der Seite [Datenverwaltung in Echtzeit-CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) . Informationen zu den einzelnen Anwendungsfällen für Marketingzwecke, die von der Adobe definiert wurden, finden Sie in der Übersicht über [Datenverwendungsrichtlinien](/help/data-governance/policies/overview.md#core-actions). <br>
Geben Sie für Amazon S3-Ziele den **[!UICONTROL Behälternamen]** und den **[!UICONTROL Ordnerpfad]** in das Cloud-Datenspeicherung-Ziel ein, an das die Dateien gesendet werden sollen. Wählen Sie **[!UICONTROL Ziel erstellen]** aus, nachdem Sie die obigen Felder ausgefüllt haben.

   ![Verbindung zum Amazon S3 Cloud-Datenspeicherung-Ziel - Authentifizierungsschritt](./assets/amazon-s3-setup-step.png)

   Geben Sie für SFTP-Ziele den **[!UICONTROL Ordnerpfad]** ein, unter dem die Dateien bereitgestellt werden sollen. Wählen Sie **[!UICONTROL Ziel erstellen]** aus, nachdem Sie die obigen Felder ausgefüllt haben.

   ![Verbindungsziel für die SFTP-Cloud-Datenspeicherung - Authentifizierungsschritt](./assets/sftp-destinations-setup-step.png)

   Geben Sie für [!DNL Amazon Kinesis] Ziele den Namen Ihres vorhandenen Datenstroms in Ihrem [!DNL Amazon Kinesis] Konto an. Adobe Echtzeit-CDP exportiert Daten in diesen Stream. Wählen Sie **[!UICONTROL Ziel erstellen]** aus, nachdem Sie die obigen Felder ausgefüllt haben.

   ![Verbindungsziel für die Kinesis Cloud-Datenspeicherung - Authentifizierungsschritt](./assets/kinesis-destinations-setup-step.png)

   Geben Sie für [!DNL Azure Event Hubs] Ziele den Namen Ihres vorhandenen Datenstroms in Ihrem [!DNL Amazon Kinesis] Konto an. Adobe Echtzeit-CDP exportiert Daten in diesen Stream. Wählen Sie **[!UICONTROL Ziel erstellen]** aus, nachdem Sie die obigen Felder ausgefüllt haben.

   ![Verbindungsziel für die Kinesis Cloud-Datenspeicherung - Authentifizierungsschritt](./assets/eventhubs-destinations-setup-step.png)

4. Ihr Ziel wird jetzt erstellt. Sie können **[!UICONTROL Speichern und beenden]** auswählen, wenn Sie Segmente später aktivieren möchten, oder Sie können **[!UICONTROL Weiter]** wählen, um den Workflow fortzusetzen und Segmente zur Aktivierung auszuwählen. In either case, see the next section, [Activate segments](#activate-segments), for the rest of the workflow to export data.

## Aktivieren von Segmenten {#activate-segments}

Informationen zum Workflow für die Segmentaktivierung finden Sie unter [Profile und Segmente für ein Ziel aktivieren](/help/rtcdp/destinations/activate-destinations.md).