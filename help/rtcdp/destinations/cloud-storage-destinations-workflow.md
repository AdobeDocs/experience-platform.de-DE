---
title: Arbeitsablauf für Cloud-Datenspeicherung-Ziele
seo-title: Arbeitsablauf für Cloud-Datenspeicherung-Ziele
description: Anleitung zum Herstellen einer Verbindung mit Ihren Cloud-Datenspeicherung
seo-description: Anleitung zum Herstellen einer Verbindung mit Ihren Cloud-Datenspeicherung
translation-type: tm+mt
source-git-commit: 9221c11a30bda3a155d73afec16be55ef8f5d133

---


# Arbeitsablauf zum Erstellen von Cloud-Datenspeicherung-Zielen

## Übersicht

Auf dieser Seite wird erläutert, wie Sie eine Verbindung zu Cloud-Datenspeicherung in der Adobe Echtzeit-Kundendatenplattform herstellen können.

1. Wählen Sie unter **[!UICONTROL Verbindungen > Ziele]** Ihr bevorzugtes Cloud-Datenspeicherung-Ziel und wählen Sie dann **[!UICONTROL Connect-Ziel]**.

   ![Verbindung zum Cloud-Datenspeicherung-Ziel](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

2. Wenn Sie im Schritt **Authentifizierung** zuvor eine Verbindung zu Ihrem Cloud-Datenspeicherung-Ziel eingerichtet haben, wählen Sie &quot; **[!UICONTROL Vorhandenes Konto]** &quot;und wählen Sie Ihre bestehende Verbindung aus. Sie können auch &quot; **[!UICONTROL Neues Konto]** &quot;auswählen, um eine neue Verbindung mit Ihrem Cloud-Datenspeicherung-Ziel einzurichten. Geben Sie die Anmeldeinformationen für die Kontoauthentifizierung ein und wählen Sie **[!UICONTROL Verbindung mit Ziel]** herstellen.

   >[!NOTE]
   >
   >Adobe Echtzeit-CDP unterstützt die Berechtigungsprüfung im Authentifizierungsprozess und zeigt eine Fehlermeldung an, wenn Sie falsche Anmeldeinformationen in Ihre Cloud-Datenspeicherung eingeben. Dadurch wird sichergestellt, dass Sie den Workflow nicht mit falschen Anmeldeinformationen abschließen.

   ![Verbindungsziel für die Cloud-Datenspeicherung - Authentifizierungsschritt](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

3. Geben Sie im Schritt **[!UICONTROL Einrichten]** einen **[!UICONTROL Namen]** und eine **[!UICONTROL Beschreibung]** für die Aktivierung ein.
   1. Geben Sie für Amazon S3-Ziele den **[!UICONTROL Behälternamen]** und den **[!UICONTROL Ordnerpfad]** in das Ziel der Cloud-Datenspeicherung ein, an das die Dateien gesendet werden sollen. Wählen Sie Ziel **[!UICONTROL erstellen]** , nachdem Sie die oben stehenden Felder ausgefüllt haben.
   2. Fügen Sie bei SFTP-Zielen den **[!UICONTROL Ordnerpfad ein.]**
   ![Verbindungsziel für die Cloud-Datenspeicherung - Authentifizierungsschritt](/help/rtcdp/destinations/assets/cloud-destinations-setup-step.png)

4. Ihr Ziel wurde jetzt erstellt. Sie können &quot; **[!UICONTROL Speichern und beenden]** &quot;auswählen, wenn Sie Segmente später aktivieren möchten, oder Sie können **[!UICONTROL Weiter]** wählen, um den Workflow fortzusetzen und Segmente zur Aktivierung auszuwählen. In beiden Fällen finden Sie weitere Informationen zum Exportieren von Daten im nächsten Abschnitt [Aktivieren von Segmenten](#activate-segments).

## Aktivieren von Segmenten {#activate-segments}

Informationen zum Arbeitsablauf für die SegmentAktivierung finden Sie unter Profil und Segmente an ein Ziel [](/help/rtcdp/destinations/activate-destinations.md) aktivieren.