---
keywords: Facebook;facebook;Social-Netzwerk;Social-Netzwerk;Social-Authentifizierung;Social-Netzwerkauthentifizierung
title: Social-Ziel erstellen
type: Tutorial
description: Erfahren Sie, wie Sie eine Verbindung zu Ihren Social-Advertising-Konten in Adobe Experience Platform herstellen.
exl-id: a0cdf2b7-b1e8-4a8e-9d5b-58a118e7b689
translation-type: tm+mt
source-git-commit: e2af4fcfe232889f3f928c00c9f9b37cf9754ca1
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 11%

---

# Erstellen eines sozialen Ziels {#social-network-destinations-workflow}

## Übersicht {#overview}

Dieses Lernprogramm verwendet [!DNL Facebook] als Beispiel, aber der Adobe Experience Platform-Arbeitsablauf ist für alle Social-Ziele gleich.

## Social-Ziel konfigurieren - Videoanleitung {#video}

Das folgende Video zeigt, wie Sie ein soziales Ziel konfigurieren und Segmente in Adobe Experience Platform aktivieren. Die Schritte werden auch in den nächsten Abschnitten sequenziell dargestellt.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

## Social-Ziel {#select-destination} auswählen

Führen Sie in **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]** einen Bildlauf zur Kategorie **[!UICONTROL Social]** durch. Wählen Sie Ihr bevorzugtes soziales Ziel und dann **[!UICONTROL Konfigurieren]**.

![Herstellen einer Verbindung zum sozialen Ziel](../../assets/catalog/social/workflow/catalog.png)

>[!NOTE]
>
>Wenn bereits eine Verbindung zu diesem Ziel besteht, wird auf der Zielkarte die Schaltfläche **[!UICONTROL Aktivieren]** angezeigt. Weitere Informationen zum Unterschied zwischen **[!UICONTROL Aktivieren]** und **[!UICONTROL Konfigurieren]** finden Sie im Abschnitt [Katalog](../../ui/destinations-workspace.md#catalog) der Dokumentation zum Zielarbeitsbereich.

## Kontoschritt {#account}

Wenn Sie im Schritt **Konto** zuvor eine Verbindung zu Ihrem sozialen Ziel eingerichtet haben, wählen Sie **[!UICONTROL Vorhandenes Konto]** und wählen Sie Ihre bestehende Verbindung aus. Sie können auch **[!UICONTROL Neues Konto]** auswählen, um eine neue Verbindung zu Ihrem Social-Ziel einzurichten. Wählen Sie **[!UICONTROL Verbindung mit Ziel]** herstellen. Dadurch gelangen Sie zum ausgewählten Social-Ziel, um sich anzumelden und Adobe Experience Cloud mit Ihrem Social-Anzeigenkonto zu verbinden.

>[!NOTE]
>
>Plattform unterstützt die Berechtigungsüberprüfung im Authentifizierungsprozess und zeigt eine Fehlermeldung an, wenn Sie falsche Anmeldeinformationen in Ihre Social-Konto-ID eingeben. Dadurch wird sichergestellt, dass Sie den Workflow nicht mit falschen Anmeldedaten ausführen.

![Verbindung zum sozialen Ziel herstellen - Authentifizierungsschritt](../../assets/catalog/social/workflow/pre-connect.png)

Nachdem Sie Ihre Anmeldedaten bestätigt haben und Adobe Experience Cloud mit Ihrem sozialen Netzwerk verbunden ist, können Sie **[!UICONTROL Weiter]** auswählen, um mit dem Schritt **[!UICONTROL Authentifizierung]** fortzufahren.

![Anmeldedaten bestätigt](../../assets/catalog/social/workflow/post-connect.png)

## Authentifizierungsschritt {#authentication}

Geben Sie im Schritt **[!UICONTROL Authentication]** einen [!UICONTROL Name] und einen [!UICONTROL Description] für Ihre Aktivierung ein und füllen Sie [!UICONTROL Konto-ID] Ihres Social-Netzwerk-Anzeigenkontos aus.

>[!IMPORTANT]
>
> * Bei [!DNL Facebook]-Zielen ist **[!UICONTROL Konto-ID]** Ihre [!DNL Facebook Ad Account ID]. Sie finden diese ID im [!DNL Facebook Ads Manager]. Präfix der ID mit `act_`, wie in der Abbildung unten dargestellt.
> * Bei [!DNL LinkedIn]-Zielen ist **[!UICONTROL Konto-ID]** Ihre [!DNL LinkedIn Campaign Manager Account ID]. Sie finden diese ID im [!DNL LinkedIn Campaign Manager].


![Verbindung zum sozialen Ziel herstellen - Authentifizierungsschritt](../../assets/catalog/social/workflow/authentication.png)

In diesem Schritt können Sie auch eine beliebige **[!UICONTROL Marketingaktion]** auswählen, die auf dieses Ziel angewendet werden soll. Marketingaktionen geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von der Adobe definierten Marketingaktionen auswählen oder eine eigene Marketingaktion erstellen. Weitere Informationen zu Marketingaktionen finden Sie unter [Übersicht über Datenverwendungsrichtlinien](../../../data-governance/policies/overview.md).

Wählen Sie **[!UICONTROL Ziel erstellen]** aus, nachdem Sie die obigen Felder ausgefüllt haben.

Ihr Ziel wird jetzt erstellt. Sie können **[!UICONTROL Speichern und beenden]** auswählen, wenn Sie Segmente später aktivieren möchten, oder Sie können **[!UICONTROL Weiter]** wählen, um den Workflow fortzusetzen und Segmente zur Aktivierung auszuwählen. In beiden Fällen finden Sie im nächsten Abschnitt [Aktivieren von Segmenten in sozialen Zielen](#activate-segments) Informationen zum Rest des Workflows.

## Aktivieren von Segmenten zu sozialen Zielen {#activate-segments}

Anweisungen zum Aktivieren von Segmenten in sozialen Zielen finden Sie unter [Daten in Ziele aktivieren](../../ui/activate-destinations.md).
