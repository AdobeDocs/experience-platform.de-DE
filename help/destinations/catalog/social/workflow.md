---
keywords: Facebook;Facebook;Social-Netzwerk;Social-Netzwerk;Social-Netzwerkauthentifizierung;Social-Netzwerkauthentifizierung
title: Social-Netzwerkziel erstellen
type: Tutorial
description: Erfahren Sie, wie Sie eine Verbindung zu Ihren Social-Netzwerk-Anzeigenkonten in Adobe Experience Platform herstellen.
translation-type: tm+mt
source-git-commit: 19e38faa84d365682e97c2ec1c6352d127c0ac29
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 52%

---


# Social-Netzwerkziel {#social-network-destinations-workflow} erstellen

Dieses Lernprogramm verwendet [!DNL Facebook] als Beispiel, aber der Adobe Experience Platform-Arbeitsablauf ist für alle Social-Netzwerkziele gleich.

Führen Sie in **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]** einen Bildlauf zur Kategorie **[!UICONTROL Social]** durch. Wählen Sie Ihr bevorzugtes soziales Netzwerkziel und dann **[!UICONTROL Konfigurieren]**.

![Verbindung zum sozialen Netzwerk-Ziel](../../assets/catalog/social/workflow/catalog.png)

>[!NOTE]
>
>Wenn bereits eine Verbindung zu diesem Ziel besteht, wird auf der Zielkarte die Schaltfläche **[!UICONTROL Aktivieren]** angezeigt. Weitere Informationen zum Unterschied zwischen **[!UICONTROL Aktivieren]** und **[!UICONTROL Konfigurieren]** finden Sie im Abschnitt [Katalog](../../ui/destinations-workspace.md#catalog) der Dokumentation zum Zielarbeitsbereich.

Wenn Sie im Schritt **Authentifizieren** zuvor eine Verbindung zu Ihrem Ziel in einem sozialen Netzwerk eingerichtet haben, wählen Sie **[!UICONTROL Vorhandenes Konto]** und Ihre bestehende Verbindung aus. Sie können auch **[!UICONTROL Neues Konto]** auswählen, um eine neue Verbindung zu Ihrem Ziel in einem sozialen Netzwerk einzurichten. Wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus. Dadurch gelangen Sie zum ausgewählten Ziel in einem sozialen Netzwerk, um sich anzumelden und Adobe Experience Cloud mit Ihrem Anzeigenkonto für das soziale Netzwerk zu verbinden.

>[!NOTE]
>
>Plattform unterstützt die Berechtigungsüberprüfung im Authentifizierungsprozess und zeigt eine Fehlermeldung an, wenn Sie falsche Anmeldeinformationen in Ihre Social-Netzwerk-Konto-ID eingeben. Dadurch wird sichergestellt, dass Sie den Workflow nicht mit falschen Anmeldedaten ausführen.

![Verbindung zum Ziel in einem sozialen Netzwerk herstellen – Authentifizierungsschritt](../../assets/catalog/social/workflow/pre-connect.png)

Nachdem Sie Ihre Anmeldedaten bestätigt haben und Adobe Experience Cloud mit Ihrem sozialen Netzwerk verbunden ist, können Sie **[!UICONTROL Weiter]** auswählen, um mit dem **[!UICONTROL Setup-Schritt]** fortzufahren.

![Anmeldedaten bestätigt](../../assets/catalog/social/workflow/post-connect.png)

Geben Sie im **[!UICONTROL Setup-Schritt]** einen [!UICONTROL Namen] und eine [!UICONTROL Beschreibung] für die Aktivierung ein und geben Sie die [!UICONTROL Kontokennung] Ihres Anzeigenkontos für das soziale Netzwerk ein.

>[!IMPORTANT]
>
> Bei [!DNL Facebook]-Zielen ist **[!UICONTROL Konto-ID]** Ihre [!DNL Facebook Ad Account ID]. Sie finden diese ID im [!DNL Facebook Ads Manager]. Stellen Sie der ID `act_` wie folgt voran:

![Verbindung zum Ziel in einem sozialen Netzwerk herstellen – Setup-Schritt](../../assets/catalog/social/workflow/setup.png)

>[!IMPORTANT]
>
> Bei [!DNL LinkedIn]-Zielen ist **[!UICONTROL Konto-ID]** Ihre [!DNL LinkedIn Campaign Manager Account ID]. Sie finden diese ID im [!DNL LinkedIn Campaign Manager].

In diesem Schritt können Sie auch eine beliebige **[!UICONTROL Marketingaktion]** auswählen, die auf dieses Ziel angewendet werden soll. Marketingaktionen geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von der Adobe definierten Marketingaktionen auswählen oder eine eigene Marketingaktion erstellen. Weitere Informationen zu Marketingaktionen finden Sie unter [Übersicht über Datenverwendungsrichtlinien](../../../data-governance/policies/overview.md).

Wählen Sie **[!UICONTROL Ziel erstellen]** aus, nachdem Sie die obigen Felder ausgefüllt haben.

Ihr Ziel wird jetzt erstellt. Sie können **[!UICONTROL Speichern und beenden]** auswählen, wenn Sie Segmente später aktivieren möchten, oder Sie können **[!UICONTROL Weiter]** wählen, um den Workflow fortzusetzen und Segmente zur Aktivierung auszuwählen. In beiden Fällen sehen Sie sich den nächsten Abschnitt [Aktivieren von Segmenten für soziale Netzwerke](#activate-segments) an, in dem der restliche Workflow erläutert wird.

## Aktivieren von Segmenten für soziale Netzwerke {#activate-segments}

Anweisungen zum Aktivieren von Segmenten für soziale Netzwerke finden Sie unter [Daten für Ziele aktivieren](../../ui/activate-destinations.md).