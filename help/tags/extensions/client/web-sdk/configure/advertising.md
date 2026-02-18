---
title: Adobe Advertising-Konfigurationseinstellungen
description: Aktivieren oder deaktivieren Sie die Funktion der Demand-Side-Plattform.
exl-id: 594fd75d-bb13-4146-9105-1398e24c4c16
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 7%

---

# Adobe Advertising-Konfigurationseinstellungen {#advertising}

>[!AVAILABILITY]
>
>Adobe Advertising für das Web SDK befindet sich derzeit in der **Beta**. Die Funktionalität und Dokumentation können sich ändern.

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_advertising"
>title="Adobe Advertising"
>abstract="Konfigurieren Sie Einstellungen für Adobe Advertising-Integrationen. Beachten Sie, dass keine Werbekonfiguration erforderlich ist, um eine Clickthrough-Messung zu ermöglichen. Kunden von Search, Social und Commerce müssen keine weiteren Maßnahmen ergreifen. Benutzer von Demand-Side Platform (DSP) müssen jedoch Advertiser in diesem Abschnitt konfigurieren, um Durchsichtskonversionen zu messen."

Im **[!UICONTROL Adobe Advertising]** Abschnitt können Sie die Funktion Demand-Side Platform (DSP) aktivieren oder deaktivieren, wenn sie in Ihrer Implementierung verwendet wird. Sie müssen dieses Feld nur festlegen, wenn Ihre Implementierung eine DSP verwendet.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei ](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Extensions]** und wählen Sie **[!UICONTROL Configure]** auf der [!UICONTROL Adobe Experience Platform Web SDK] aus.
1. Scrollen Sie nach unten zum Abschnitt **[!UICONTROL Adobe Advertising]** .

Derzeit ist eine Option verfügbar.

## [!UICONTROL Adobe Advertising DSP]

Ein Dropdown-Menü, das die DSP-Funktionen für Adobe Advertising aktiviert oder deaktiviert.

* **[!UICONTROL Enabled]**: Aktiviert das View-Through-Tracking.
* **[!UICONTROL Disabled]**: Deaktiviert das View-Through-Tracking.

Wenn diese Option aktiviert ist, sind die folgenden Einstellungen verfügbar:

* **[!UICONTROL Advertisers]**: Die Werbetreibenden, für die das View-Through-Tracking aktiviert werden soll.
* **[!UICONTROL ID5 partner ID]**: Optional. Die ID5-Partner-ID Ihres Unternehmens. Mit dieser Einstellung kann der Web-SDK universelle ID5-IDs erfassen.
* **[!UICONTROL RampID JavaScript path]**: Optional. Der Pfad zum [!DNL LiveRamp RampID] JavaScript-Code (`ats.js`) Ihres Unternehmens.  Mit dieser Einstellung kann die Web-SDK universelle IDs [!DNL RampID].
