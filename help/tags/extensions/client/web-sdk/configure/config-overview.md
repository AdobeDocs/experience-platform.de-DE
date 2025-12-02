---
title: Übersicht über Konfigurationseinstellungen
description: Erfahren Sie mehr über die verfügbaren Optionen beim Konfigurieren der Tag-Erweiterung „Web SDK".
source-git-commit: 5f0203cfff3cb5c8b892142ff9b1c121925c3c46
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 1%

---

# Übersicht über Konfigurationseinstellungen

Die Tag-Erweiterung &quot;Adobe Experience Platform Web SDK&quot; bietet mehrere Optionen, die Sie anpassen können. Diese Konfigurationseinstellungen entsprechen der Verwendung des Befehls [`configure`](/help/collection/js/commands/configure/overview.md) in der JavaScript-Bibliothek.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei &#x200B;](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Extensions]** und wählen Sie **[!UICONTROL Configure]** auf der [!UICONTROL Adobe Experience Platform Web SDK] aus.

## Benutzerdefinierte Build-Komponenten

Wenn die Optimierung der Build-Größe für Ihr Unternehmen eine Priorität darstellt, können Sie bestimmte Funktionen deaktivieren, die Sie nicht verwenden, um die Build-Größe der Erweiterung zu verringern. Weitere Informationen [&#x200B; Sie unter &#x200B;](custom-build-components.md)Benutzerdefinierte Build-Komponenten“.

## SDK-Instanzen

Die meisten Implementierungen benötigen in der Regel eine einzige SDK-Instanz. Wenn für Ihr Unternehmen jedoch mehrere Tracking-Instanzen von Web SDK erforderlich sind, können Sie die Schaltfläche **[!UICONTROL Add instance]** verwenden. Die folgenden übergeordneten Abschnitte sind bei der Konfiguration jeder Tag-Instanz von Web SDK verfügbar:

* [**[!UICONTROL SDK instance]**](general.md): Allgemeine Einstellungen für die Instanz. Alle Felder in diesem Abschnitt sind erforderlich.
* [**[!UICONTROL Datastreams]**](datastreams.md): Wohin die Daten für die einzelnen Tag-Umgebungen gehen sollen.
* [**[!UICONTROL Consent]**](consent.md): Standardmäßige Einverständniseinstellungen für die Erweiterung.
* [**[!UICONTROL Identity]**](identity.md): Einstellungen für Cookie- und Besuchermigration.
* [**[!UICONTROL Personalization]**](personalization.md): Personalisieren des Besuchererlebnisses auf individueller Ebene.
* [**[!UICONTROL Data collection]**](data-collection.md): Einschließen oder auslassen, was automatisch erfasst wird.
* [**[!UICONTROL Streaming media]**](streaming-media.md): Spezifische Einstellungen für die Streaming-Mediensammlung.
* [**[!UICONTROL Datastream configuration overrides]**](configuration-overrides.md): Ändern von Konfigurationseinstellungen, wenn bestimmte Bedingungen erfüllt sind.
* [**[!UICONTROL Advanced settings]**](advanced-settings.md): Geben Sie den Basispfad für die Edge Network an.
