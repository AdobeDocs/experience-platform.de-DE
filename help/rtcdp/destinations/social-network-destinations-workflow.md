---
title: Arbeitsablauf für Social-Netzwerkziele
seo-title: Arbeitsablauf für Social-Netzwerkziele
description: Anleitung zum Herstellen einer Verbindung zu Ihren Social-Netzwerk-Anzeigenkonten
seo-description: Anleitung zum Herstellen einer Verbindung zu Ihren Social-Netzwerk-Anzeigenkonten
translation-type: tm+mt
source-git-commit: ab53e2efffed536e8028beabd64aee843d1eeee8
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 13%

---


# Authentifizierungsarbeitsablauf für Social-Netzwerkziele {#social-network-destinations-workflow}

## Arbeitsablauf zum Erstellen von Social-Netzwerk-Zielen

In diesem Lernprogramm wird Facebook als Beispiel verwendet, aber der Arbeitsablauf in der Adobe Echtzeit-Kundendatenplattform ist für alle Social-Netzwerk-Ziele gleich, sobald dem Produkt weitere hinzugefügt werden.

1. Blättern Sie unter **[!UICONTROL Ziele > Katalog]** zur **[!UICONTROL Social]** -Kategorie. Wählen Sie Ihr bevorzugtes Social-Netzwerk-Ziel und dann **[!UICONTROL Connect-Ziel]**.

   ![Verbindung zum Social-Netzwerk-Ziel](/help/rtcdp/destinations/assets/facebook-catalog-view.png)

2. In the **Authentication** step, if you had previously set up a connection to your social network destination, select **[!UICONTROL Existing Account]** and select your existing connection. Or, you can select **[!UICONTROL New Account]** to set up a new connection to your social network destination. Wählen Sie **[!UICONTROL Mit Ziel]** verbinden. Dadurch gelangen Sie zum ausgewählten Social-Netzwerk-Ziel, um sich anzumelden und Adobe Experience Cloud mit Ihrem Social-Netzwerk-Anzeigenkonto zu verbinden.

   >[!NOTE]
   >
   >Adobe Echtzeit-CDP unterstützt die Berechtigungsüberprüfung im Authentifizierungsprozess und zeigt eine Fehlermeldung an, wenn Sie falsche Anmeldeinformationen in Ihre Social-Netzwerk-Konto-ID eingeben. Dadurch wird sichergestellt, dass Sie den Workflow nicht mit falschen Anmeldeinformationen abschließen.

   ![Verbindung zum Ziel des sozialen Netzwerks herstellen - Authentifizierungsschritt](/help/rtcdp/destinations/assets/facebook-pre-connect-view.png)

3. Nachdem Sie Ihre Anmeldedaten bestätigt haben und Adobe Experience Cloud mit Ihrem sozialen Netzwerk verbunden ist, können Sie &quot; **[!UICONTROL Weiter]** &quot;wählen, um mit dem Schritt &quot; **[!UICONTROL Setup]** &quot;fortzufahren.

   ![Anmeldeinformationen bestätigt](/help/rtcdp/destinations/assets/facebook-post-connection-view.png)

4. Geben Sie im Schritt **[!UICONTROL Einrichtung]** einen **[!UICONTROL Namen]** und eine **[!UICONTROL Beschreibung]** für die Aktivierung ein und geben Sie die **[!UICONTROL Konto-ID]** Ihres Social-Netzwerk-Anzeigenkontos ein. Wählen Sie alle Anwendungsfälle für das Marketing aus, die für dieses Ziel gelten sollen. Wählen Sie **[!UICONTROL Ziel erstellen]**, nachdem Sie die obigen Felder ausgefüllt haben.

   >[!IMPORTANT]
   >
   > Für Facebook-Ziele. **[!UICONTROL Die Konto-ID]** ist Ihre Facebook-Konto-ID. Sie finden diese ID im Facebook Ads Manager. Präfix der ID `act_` wie unten gezeigt:

   ![Verbindung zum Ziel des sozialen Netzwerks herstellen - Setup-Schritt](/help/rtcdp/destinations/assets/social-network-setup-step.png)

5. Ihr Ziel wird jetzt erstellt. Sie können **[!UICONTROL Speichern und beenden]** auswählen, wenn Sie Segmente später aktivieren möchten, oder Sie können **[!UICONTROL Weiter]** wählen, um den Workflow fortzusetzen und Segmente zur Aktivierung auszuwählen. In either case, see the next section, [Activate segments to social networks](#activate-segments), for the rest of the workflow.

## Aktivieren von Segmenten in sozialen Netzwerken {#activate-segments}

For instructions on how to activate segments to social networks, see [Activate Data to Destinations](/help/rtcdp/destinations/activate-destinations.md).


<!--

// update IMPORTANT note in step 4 after marketing use cases are released for RTCDP

    >[!IMPORTANT]
    >
    > * The *Single Identity Personalization* marketing use case is selected by default for social network destinations and cannot be removed. 
    > * For Facebook destinations. **[!UICONTROL Account ID]** is your Facebook Ad Account ID. You can find this ID in the Facebook Ads Manager. Prefix the ID with `act_` as shown below: 

    ![Connect to social network destination - setup step](/help/rtcdp/destinations/assets/social-networks-setup-step.png)