---
title: Brand Concierge-Konfigurationseinstellungen
description: Konfigurieren Sie Sitzungspersistenz und Stream-Timeouts für den Brand Concierge-Chat.
exl-id: d5c0bdf7-563d-4e0e-9b1b-71e2fa783e29
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 11%

---

# Brand Concierge-Konfigurationseinstellungen {#brand-concierge}

>[!AVAILABILITY]
>
>Brand Concierge für das Web SDK befindet sich derzeit in der **Beta**. Die Funktionalität und Dokumentation können sich ändern.

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_brandconcierge"
>title="Brand Concierge"
>abstract="Konfigurationseinstellungen bei Verwendung von Brand Concierge in Ihrer Eigenschaft."

Im Abschnitt **[!UICONTROL Brand Concierge]** können Sie steuern, wie sich Brand Concierge-Chat-Sitzungen in der Tag-Erweiterung „Web SDK&quot; verhalten.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei ](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Extensions]** und wählen Sie **[!UICONTROL Configure]** auf der [!UICONTROL Adobe Experience Platform Web SDK] aus.
1. Scrollen Sie nach unten zum Abschnitt **[!UICONTROL Brand Concierge]** .

Die folgenden Optionen sind verfügbar:

## [!UICONTROL Sticky conversation session]

Ein Kontrollkästchen, das Brand Concierge-Sitzungen über Seiten hinweg speichert und ein Sitzungs-Cookie verwendet. Diese Option ist standardmäßig deaktiviert. Anleitungen zum Festlegen dieses Werts finden Sie unter [`conversation`](/help/collection/js/commands/configure/conversation.md) in der Dokumentation zur JavaScript-Bibliothek .

## [!UICONTROL Stream timeout (seconds)]

Die maximale Zeit in Sekunden, die auf Konversations-Stream-Blöcke gewartet wird, bevor ein Zeitüberschreitungsfehler ausgelöst wird. Der Standardwert ist `10` Sekunden.
