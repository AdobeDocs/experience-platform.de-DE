---
title: Arbeitsablauf für Cloud-Datenspeicherung-Ziele
seo-title: Arbeitsablauf für Cloud-Datenspeicherung-Ziele
description: Anleitung zum Herstellen einer Verbindung mit Ihren Cloud-Datenspeicherung
seo-description: Anleitung zum Herstellen einer Verbindung mit Ihren Cloud-Datenspeicherung
translation-type: tm+mt
source-git-commit: c3fe5753fb23f99076f9c85b4e07af2d25a121a9

---


# Arbeitsablauf zum Erstellen von Cloud-Datenspeicherung-Zielen

## Übersicht

Auf dieser Seite wird erläutert, wie Sie eine Verbindung zu Cloud-Datenspeicherung in der Adobe Echtzeit-Kundendatenplattform herstellen können.

1. Wählen Sie **[!UICONTROL Connections > Destinations]** im Menü Ihr bevorzugtes Cloud-Datenspeicherung-Ziel und dann **[!UICONTROL Connect destination]**.

   ![Verbindung zum Cloud-Datenspeicherung-Ziel](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

2. Wenn Sie im Schritt **Authentifizierung** zuvor eine Verbindung zu Ihrem Cloud-Datenspeicherung-Ziel eingerichtet haben, wählen Sie Ihre bestehende Verbindung aus **[!UICONTROL Existing Account]** und wählen Sie sie aus. Sie können auch eine neue Verbindung **[!UICONTROL New Account]** zum Ziel Ihrer Cloud-Datenspeicherung einrichten. Geben Sie Ihre Kontoauthentifizierungsdaten ein und wählen Sie **[!UICONTROL Connect to destination]**. Weitere Informationen zu den Anmeldeinformationen im Schritt [Authentifizierung finden Sie unter](/help/rtcdp/destinations/amazon-s3-destination.md) Amazon S3-Ziel [- und](/help/rtcdp/destinations/sftp-destination.md) SFTP-Ziel **** .

   >[!NOTE]
   >
   >Adobe Echtzeit-CDP unterstützt die Berechtigungsprüfung im Authentifizierungsprozess und zeigt eine Fehlermeldung an, wenn Sie falsche Anmeldeinformationen in Ihre Cloud-Datenspeicherung eingeben. Dadurch wird sichergestellt, dass Sie den Workflow nicht mit falschen Anmeldeinformationen abschließen.

   ![Verbindungsziel für die Cloud-Datenspeicherung - Authentifizierungsschritt](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

3. Geben Sie im **[!UICONTROL Setup]** Schritt einen **[!UICONTROL Name]** und einen **[!UICONTROL Description]** Wert für die Aktivierung ein. <br>
Geben Sie für Amazon S3-Ziele den **[!UICONTROL Bucket name]** und den **[!UICONTROL Folder path]** in das Cloud-Datenspeicherung-Ziel ein, an das die Dateien gesendet werden sollen. Wählen Sie diese Option, **[!UICONTROL Create Destination]** nachdem Sie die oben stehenden Felder ausgefüllt haben.

   ![Verbindung mit Amazon S3 Cloud-Datenspeicherung-Ziel - Authentifizierungsschritt](/help/rtcdp/destinations/assets/cloud-destinations-setup-step.png)

   Geben Sie für SFTP-Ziele die **[!UICONTROL Folder path]** Stelle ein, an die die Dateien gesendet werden sollen.

   ![Verbindungsziel für die SFTP-Cloud-Datenspeicherung - Authentifizierungsschritt](/help/rtcdp/destinations/assets/sftp-destinations-setup-step.png)

4. Ihr Ziel wurde jetzt erstellt. Sie können auswählen, **[!UICONTROL Save & Exit]** ob Sie Segmente später aktivieren möchten, oder Sie können wählen, ob Sie den Workflow fortsetzen und Segmente zur Aktivierung auswählen **[!UICONTROL Next]** möchten. In beiden Fällen finden Sie weitere Informationen zum Exportieren von Daten im nächsten Abschnitt [Aktivieren von Segmenten](#activate-segments).

## Aktivieren von Segmenten {#activate-segments}

Informationen zum Arbeitsablauf für die SegmentAktivierung finden Sie unter Profil und Segmente an ein Ziel [](/help/rtcdp/destinations/activate-destinations.md) aktivieren.