---
title: Erweiterte Konfigurationeinstellungen
description: Konfigurieren Sie die erweiterten Einstellungen für die Tag-Erweiterung „Web SDK".
exl-id: d830a210-77ab-4823-b5fa-c1194a01bea3
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 3%

---

# Erweiterte Konfigurationeinstellungen {#advanced}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_advanced"
>title="Erweiterte Einstellungen"
>abstract="Erweiterte Konfigurationseinstellungen. Adobe empfiehlt, diese Optionen für die meisten Implementierungen unverändert zu lassen."

In diesem Konfigurationsabschnitt können Sie erweiterte Einstellungen ändern. Adobe empfiehlt, diese Optionen für die meisten Implementierungen unverändert zu lassen.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei ](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Extensions]** und wählen Sie **[!UICONTROL Configure]** auf der [!UICONTROL Adobe Experience Platform Web SDK] aus.
1. Scrollen Sie nach unten zum Abschnitt **[!UICONTROL Advanced Settings]** .

![Abbildung mit den erweiterten Einstellungen auf der Seite mit den Tag-Erweiterungen für Web SDK](../assets/advanced-settings.png)

Derzeit ist eine Option verfügbar.

## [!UICONTROL Edge base path]

Verwenden Sie dieses Feld, um den Basispfad zu ändern, der für die Interaktion mit der Edge Network verwendet wird. Adobe fordert Sie möglicherweise auf, dieses Feld zu ändern, wenn Sie an bestimmten Alpha- oder Betatests teilnehmen. Andernfalls empfiehlt Adobe, das Feld auf dem Standardwert `ee` zu belassen.

Dieses Feld entspricht dem -Tag-[`edgeBasePath`](/help/collection/js/commands/configure/edgebasepath.md) beim Konfigurieren der JavaScript-Bibliothek.
