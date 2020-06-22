---
title: Arbeitsablauf für Social-Netzwerkziele
seo-title: Arbeitsablauf für Social-Netzwerkziele
description: Anleitung zum Herstellen einer Verbindung zu Ihren Social-Netzwerk-Anzeigenkonten
seo-description: Anleitung zum Herstellen einer Verbindung zu Ihren Social-Netzwerk-Anzeigenkonten
translation-type: tm+mt
source-git-commit: 3c598454a868139b7604c5c7ca2b98fa0f1bb961
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 11%

---


# Authentifizierungsarbeitsablauf für Social-Netzwerkziele {#social-network-destinations-workflow}

## Arbeitsablauf zum Erstellen von Social-Netzwerk-Zielen

In diesem Lernprogramm wird Facebook als Beispiel verwendet, aber der Arbeitsablauf in der Adobe Echtzeit-Platform &quot;Kundendaten&quot;ist für alle Social-Netzwerkziele gleich, sobald dem Produkt weitere hinzugefügt werden.

1. Blättern Sie unter **[!UICONTROL Ziele > Katalog]** zur **[!UICONTROL Social]** -Kategorie. Wählen Sie Ihr bevorzugtes Social-Netzwerk-Ziel und dann **[!UICONTROL Connect-Ziel]**.

   ![Verbindung zum Social-Netzwerk-Ziel](/help/rtcdp/destinations/assets/facebook-catalog-view.png)

2. In the **Authentication** step, if you had previously set up a connection to your social network destination, select **[!UICONTROL Existing Account]** and select your existing connection. Or, you can select **[!UICONTROL New Account]** to set up a new connection to your social network destination. Wählen Sie **[!UICONTROL Mit Ziel]** verbinden. Dadurch gelangen Sie zum ausgewählten Social-Netzwerk-Ziel, um sich anzumelden und Adobe Experience Cloud mit Ihrem Social-Netzwerk-Anzeigenkonto zu verbinden.

   >[!NOTE]
   >
   >Adobe Echtzeit-CDP unterstützt die Berechtigungsüberprüfung im Authentifizierungsprozess und zeigt eine Fehlermeldung an, wenn Sie falsche Anmeldeinformationen in Ihre Social-Netzwerk-Konto-ID eingeben. Dadurch wird sichergestellt, dass Sie den Workflow nicht mit falschen Anmeldeinformationen abschließen.

   ![Verbindung zum Ziel des sozialen Netzwerks herstellen - Authentifizierungsschritt](/help/rtcdp/destinations/assets/facebook-pre-connect-view.png)

3. Nachdem Sie Ihre Anmeldedaten bestätigt haben und Adobe Experience Cloud mit Ihrem sozialen Netzwerk verbunden ist, können Sie &quot; **[!UICONTROL Weiter]** &quot;wählen, um mit dem Schritt &quot; **[!UICONTROL Setup]** &quot;fortzufahren.

   ![Anmeldeinformationen bestätigt](/help/rtcdp/destinations/assets/facebook-post-connection-view.png)

4. Geben Sie im Schritt **[!UICONTROL Einrichtung]** einen **[!UICONTROL Namen]** und eine **[!UICONTROL Beschreibung]** für die Aktivierung ein und geben Sie die **[!UICONTROL Konto-ID]** Ihres Social-Netzwerk-Anzeigenkontos ein. <br> In diesem Schritt können Sie auch einen beliebigen **[!UICONTROL Marketing-Anwendungsfall]** auswählen, der für dieses Ziel gelten soll. Anwendungsfälle für das Marketing geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von Adobe definierten Anwendungsfällen für das Marketing auswählen oder einen eigenen Anwendungsfall für das Marketing erstellen. Weitere Informationen zu Anwendungsfällen für das Marketing finden Sie auf der Seite [Datenverwaltung in Echtzeit-CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) . Informationen zu den einzelnen von Adobe definierten Anwendungsfällen für Marketing finden Sie in der Übersicht über die [Datenverwendungsrichtlinien](/help/data-governance/policies/overview.md#core-actions). <br> Wählen Sie **[!UICONTROL Ziel erstellen]**, nachdem Sie die obigen Felder ausgefüllt haben.

   >[!IMPORTANT]
   >
   > * Der Anwendungsfall *Single Identity Personalization* Marketing ist standardmäßig für Social Network-Ziele ausgewählt und kann nicht entfernt werden.
   > * Für Facebook-Ziele. **[!UICONTROL Die Konto-ID]** ist Ihre Facebook-Konto-ID. Sie finden diese ID im Facebook Ads Manager. Präfix der ID `act_` wie unten gezeigt:


   ![Verbindung zum Ziel des sozialen Netzwerks herstellen - Setup-Schritt](/help/rtcdp/destinations/assets/social-networks-setup-step.png)

5. Ihr Ziel wird jetzt erstellt. Sie können **[!UICONTROL Speichern und beenden]** auswählen, wenn Sie Segmente später aktivieren möchten, oder Sie können **[!UICONTROL Weiter]** wählen, um den Workflow fortzusetzen und Segmente zur Aktivierung auszuwählen. In either case, see the next section, [Activate segments to social networks](#activate-segments), for the rest of the workflow.

## Aktivieren von Segmenten in sozialen Netzwerken {#activate-segments}

For instructions on how to activate segments to social networks, see [Activate Data to Destinations](/help/rtcdp/destinations/activate-destinations.md).