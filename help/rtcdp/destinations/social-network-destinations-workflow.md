---
title: Arbeitsablauf für Social-Netzwerkziele
seo-title: Arbeitsablauf für Social-Netzwerkziele
description: Anleitung zum Herstellen einer Verbindung zu Ihren Social-Netzwerk-Anzeigenkonten
seo-description: Anleitung zum Herstellen einer Verbindung zu Ihren Social-Netzwerk-Anzeigenkonten
translation-type: tm+mt
source-git-commit: bfcbc56f05fa1c3b5fafd57b1166e50130b6007d

---


# (Beta) Authentifizierungsarbeitsablauf für Social-Netzwerkziele {#social-network-destinations-workflow}


>[!IMPORTANT]
>
>Der Arbeitsablauf zum Erstellen von Social-Netzwerk-Zielen in Adobe Echtzeit-CDP befindet sich derzeit in der Betaphase und steht nicht allen Benutzern zur Verfügung. Die Dokumentation und Funktionalität können sich ändern.

## Arbeitsablauf zum Erstellen von Cloud-Datenspeicherung-Zielen

In diesem Lernprogramm wird Facebook als Beispiel verwendet, aber der Arbeitsablauf in der Adobe Echtzeit-Kundendatenplattform ist für alle Social-Netzwerk-Ziele gleich, sobald dem Produkt weitere hinzugefügt werden.

1. Führen Sie **[!UICONTROL Connections > Destinations]** einen Bildlauf zur **[!UICONTROL Social]** Kategorie durch. Wählen Sie Ihr bevorzugtes Social-Netzwerk-Ziel und dann **[!UICONTROL Connect destination]**.

   ![Verbindung zum Social-Netzwerk-Ziel](/help/rtcdp/destinations/assets/facebook-catalog-view.png)

2. Wenn Sie im Schritt **Authentifizierung** zuvor eine Verbindung zu Ihrem Social-Netzwerkziel eingerichtet haben, wählen Sie Ihre bestehende Verbindung aus **[!UICONTROL Existing Account]** und wählen Sie sie aus. Sie können auch eine neue Verbindung **[!UICONTROL New Account]** zum Ziel des sozialen Netzwerks einrichten. Wählen Sie diese Option **[!UICONTROL Connect to destination]** und führen Sie zum ausgewählten Social-Netzwerk-Ziel, um sich anzumelden und Adobe Experience Cloud mit Ihrem Social-Netzwerk-Anzeigenkonto zu verbinden.

   >[!NOTE]
   >
   >Adobe Echtzeit-CDP unterstützt die Berechtigungsüberprüfung im Authentifizierungsprozess und zeigt eine Fehlermeldung an, wenn Sie falsche Anmeldeinformationen in Ihre Social-Netzwerk-Konto-ID eingeben. Dadurch wird sichergestellt, dass Sie den Workflow nicht mit falschen Anmeldeinformationen abschließen.

   ![Verbindung zum Ziel des sozialen Netzwerks herstellen - Authentifizierungsschritt](/help/rtcdp/destinations/assets/facebook-pre-connect-view.png)

3. Nachdem Sie Ihre Anmeldedaten bestätigt haben und Adobe Experience Cloud mit Ihrem sozialen Netzwerk verbunden ist, können Sie **[!UICONTROL Next]** mit dem **[!UICONTROL Setup]** Schritt fortfahren.

   ![Anmeldeinformationen bestätigt](/help/rtcdp/destinations/assets/facebook-post-connection-view.png)

4. Geben Sie im **[!UICONTROL Setup]** Schritt einen **[!UICONTROL Name]** und einen **[!UICONTROL Description]** für den Ablauf Ihrer Aktivierung ein und füllen Sie das Feld **[!UICONTROL Account ID]** &quot;Social-Netzwerk-Anzeigenkonto&quot;aus. Wählen Sie diese Option, **[!UICONTROL Create Destination]** nachdem Sie die oben stehenden Felder ausgefüllt haben.

   >[!IMPORTANT]
   >
   >Für Facebook-Ziele. **[!UICONTROL Account ID]** ist Ihre Facebook-Anzeigenkonto-ID. Sie finden diese ID im Facebook Ads Manager. Präfix der ID `act_` wie unten gezeigt:

   ![Verbindung zum Ziel des sozialen Netzwerks herstellen - Setup-Schritt](/help/rtcdp/destinations/assets/social-network-step.png)

5. Ihr Ziel wurde jetzt erstellt. Sie können auswählen, **[!UICONTROL Save & Exit]** ob Sie Segmente später aktivieren möchten, oder Sie können wählen, ob Sie den Workflow fortsetzen und Segmente zur Aktivierung auswählen **[!UICONTROL Next]** möchten. In beiden Fällen finden Sie den Rest des Workflows im nächsten Abschnitt [Aktivieren von Segmenten in sozialen Netzwerken](#activate-segments).

## Aktivieren von Segmenten in sozialen Netzwerken {#activate-segments}

For instructions on how to activate segments to social networks, see [Activate Data to Destinations](/help/rtcdp/destinations/activate-destinations.md).