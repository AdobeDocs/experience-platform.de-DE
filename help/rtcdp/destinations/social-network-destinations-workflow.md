---
title: Workflow für soziale Netzwerk-Ziele
seo-title: Workflow für soziale Netzwerk-Ziele
description: Anleitung zum Herstellen einer Verbindung zu Ihren Anzeigenkonten für soziale Netzwerke
seo-description: Anleitung zum Herstellen einer Verbindung zu Ihren Anzeigenkonten für soziale Netzwerke
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 65%

---


# Social Network destinations authentication workflow {#social-network-destinations-workflow}

## Arbeitsablauf zum Erstellen von Social-Netzwerk-Zielen

This tutorial uses [!DNL Facebook] as an example, but the workflow in Adobe Real-time Customer Data Platform will be the same for all social network destinations, once more are added to the product.

1. In **[!UICONTROL Destinations > Catalog]**, scroll to the **[!UICONTROL Social]** category. Wählen Sie Ihr bevorzugtes soziales Netzwerk-Ziel und dann **[!UICONTROL Ziel verbinden]** aus.

   ![Verbindung zum sozialen Netzwerk-Ziel](/help/rtcdp/destinations/assets/facebook-catalog-view.png)

2. Wenn Sie im Schritt **Authentifizieren** zuvor eine Verbindung zu Ihrem sozialen Netzwerk-Ziel eingerichtet haben, wählen Sie **[!UICONTROL Vorhandenes Konto]** und Ihre bestehende Verbindung aus. Sie können auch **[!UICONTROL Neues Konto]** auswählen, um eine neue Verbindung zu Ihrem sozialen Netzwerk-Ziel einzurichten. Wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus. Dadurch gelangen Sie zum ausgewählten sozialen Netzwerk-Ziel, um sich anzumelden und Adobe Experience Cloud mit Ihrem Anzeigenkonto für das soziale Netzwerk zu verbinden.

   >[!NOTE]
   >
   >Die Echtzeit-Kundendatenplattform von Adobe unterstützt die Berechtigungsprüfung im Authentifizierungsprozess und zeigt eine Fehlermeldung an, wenn Sie falsche Anmeldedaten für die Kontokennung des sozialen Netzwerks eingeben. Dadurch wird sichergestellt, dass Sie den Workflow nicht mit falschen Anmeldedaten ausführen.

   ![Verbindung zum sozialen Netzwerk-Ziel herstellen – Authentifizierungsschritt](/help/rtcdp/destinations/assets/facebook-pre-connect-view.png)

3. Nachdem Sie Ihre Anmeldedaten bestätigt haben und Adobe Experience Cloud mit Ihrem sozialen Netzwerk verbunden ist, können Sie **[!UICONTROL Weiter]** auswählen, um mit dem **[!UICONTROL Setup-Schritt]** fortzufahren.

   ![Anmeldedaten bestätigt](/help/rtcdp/destinations/assets/facebook-post-connection-view.png)

4. Geben Sie im **[!UICONTROL Setup-Schritt]** einen **[!UICONTROL Namen]** und eine **[!UICONTROL Beschreibung]** für die Aktivierung ein und geben Sie die **[!UICONTROL Kontokennung]** Ihres Anzeigenkontos für das soziale Netzwerk ein. <br> In diesem Schritt können Sie auch einen beliebigen **[!UICONTROL Marketing-Anwendungsfall]** auswählen, der für dieses Ziel gelten soll. Anwendungsfälle für das Marketing geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von Adobe definierten Anwendungsfällen für das Marketing auswählen oder einen eigenen Anwendungsfall für das Marketing erstellen. Weitere Informationen zu Anwendungsfällen für das Marketing finden Sie auf der Seite [Datenverwaltung in Echtzeit-CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) . Informationen zu den einzelnen von Adobe definierten Anwendungsfällen für Marketing finden Sie in der Übersicht über die [Datenverwendungsrichtlinien](/help/data-governance/policies/overview.md#core-actions). <br> Wählen Sie **[!UICONTROL Ziel erstellen]** aus, nachdem Sie die obigen Felder ausgefüllt haben.

   >[!IMPORTANT]
   >
   > * Der Anwendungsfall *Single Identity Personalization* Marketing ist standardmäßig für Social Network-Ziele ausgewählt und kann nicht entfernt werden.
   > * Für [!DNL Facebook] Ziele. **[!UICONTROL Die Konto-ID]** ist Ihre [!DNL Facebook Ad Account ID]. You can find this ID in the [!DNL Facebook Ads Manager]. Stellen Sie der ID `act_` wie folgt voran:


   ![Verbindung zum sozialen Netzwerk-Ziel herstellen – Setup-Schritt](/help/rtcdp/destinations/assets/social-networks-setup-step.png)

5. Ihr Ziel wird jetzt erstellt. Sie können **[!UICONTROL Speichern und beenden]** auswählen, wenn Sie Segmente später aktivieren möchten, oder Sie können **[!UICONTROL Weiter]** wählen, um den Workflow fortzusetzen und Segmente zur Aktivierung auszuwählen. In beiden Fällen sehen Sie sich den nächsten Abschnitt [Aktivieren von Segmenten für soziale Netzwerke](#activate-segments) an, in dem der restliche Workflow erläutert wird.

## Aktivieren von Segmenten für soziale Netzwerke {#activate-segments}

Anweisungen zum Aktivieren von Segmenten für soziale Netzwerke finden Sie unter [Daten für Ziele aktivieren](/help/rtcdp/destinations/activate-destinations.md).