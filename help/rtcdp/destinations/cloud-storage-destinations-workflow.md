---
title: Arbeitsablauf für Cloud-Datenspeicherung-Ziele
seo-title: Arbeitsablauf für Cloud-Datenspeicherung-Ziele
description: Anleitung zum Herstellen einer Verbindung mit Ihren Cloud-Datenspeicherung
seo-description: Anleitung zum Herstellen einer Verbindung mit Ihren Cloud-Datenspeicherung
translation-type: tm+mt
source-git-commit: 225f18bd0d092bdae7b4cc99c278e850be9cfd56

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

3. Geben Sie im Schritt **[!UICONTROL Einrichten]** einen **[!UICONTROL Namen]** und ein **[!UICONTROL Ziel]** für die Aktivierung ein und fügen Sie den **[!UICONTROL Ordnerpfad]** in das Ziel Ihrer Cloud-Datenspeicherung ein, an dem die Dateien bereitgestellt werden sollen. Wählen Sie Ziel **[!UICONTROL erstellen]** , nachdem Sie die oben stehenden Felder ausgefüllt haben.

   ![Verbindungsziel für die Cloud-Datenspeicherung - Authentifizierungsschritt](/help/rtcdp/destinations/assets/cloud-destinations-setup-step.png)

4. Ihr Ziel wurde jetzt erstellt. Sie können &quot; **[!UICONTROL Speichern und beenden]** &quot;auswählen, wenn Sie Segmente später aktivieren möchten, oder Sie können **[!UICONTROL Weiter]** wählen, um den Workflow fortzusetzen und Segmente zur Aktivierung auszuwählen. In beiden Fällen sehen Sie sich den nächsten Abschnitt [Aktivieren von Segmenten](#activate-segments)für den Rest des Workflows an.

## Aktivieren von Segmenten {#activate-segments}

Informationen zum Arbeitsablauf für die SegmentAktivierung finden Sie unter Profil und Segmente an ein Ziel [](/help/rtcdp/destinations/activate-destinations.md) aktivieren.