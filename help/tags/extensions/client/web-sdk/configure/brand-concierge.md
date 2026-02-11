---
title: Brand Concierge-Konfigurationseinstellungen
description: Konfigurieren Sie Sitzungspersistenz und Stream-Timeouts für den Brand Concierge-Chat.
source-git-commit: 0a45b688243b17766143b950994f0837dc0d0b48
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 11%

---

# Brand Concierge-Konfigurationseinstellungen

>[!AVAILABILITY]
>
>Brand Concierge für das Web SDK befindet sich derzeit in der **Beta**. Die Funktionalität und Dokumentation können sich ändern.

Im Abschnitt **[!UICONTROL Brand Concierge]** können Sie steuern, wie sich Brand Concierge-Chat-Sitzungen in der Tag-Erweiterung „Web SDK&quot; verhalten.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei &#x200B;](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Extensions]** und wählen Sie **[!UICONTROL Configure]** auf der [!UICONTROL Adobe Experience Platform Web SDK] aus.
1. Scrollen Sie nach unten zum Abschnitt **[!UICONTROL Brand Concierge]** .

Die folgenden Optionen sind verfügbar:

## [!UICONTROL Sticky conversation session]

Ein Kontrollkästchen, das Brand Concierge-Sitzungen über Seiten hinweg speichert und ein Sitzungs-Cookie verwendet. Diese Option ist standardmäßig deaktiviert. Anleitungen zum Festlegen dieses Werts finden Sie unter [`conversation`](/help/collection/js/commands/configure/conversation.md) in der Dokumentation zur JavaScript-Bibliothek .

## [!UICONTROL Stream timeout (seconds)]

Die maximale Zeit in Sekunden, die auf Konversations-Stream-Blöcke gewartet wird, bevor ein Zeitüberschreitungsfehler ausgelöst wird. Der Standardwert ist `10` Sekunden.
