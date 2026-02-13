---
title: Build-Optionen
description: Erstellen Sie einen benutzerdefinierten Web-SDK-Build, der Funktionen zur Verringerung der Build-Größe deaktiviert.
exl-id: 853e0a6c-0953-4e08-9a7d-334aab022583
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 1%

---

# Build-Optionen {#build-options}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_buildoptions"
>title="Build-Optionen"
>abstract="Sie können Module selektiv aus der JavaScript-Bibliothek einbeziehen oder ausschließen, wodurch die Bibliotheksgröße verringert und die Leistung verbessert wird."

Die Web SDK-Bibliothek enthält mehrere Module für verschiedene Funktionen wie Personalisierung, Identitätsnachverfolgung, Linktracking und mehr. Je nach Anwendungsfällen benötigen Sie möglicherweise nur bestimmte Funktionen anstelle der gesamten Bibliothek. Durch das Deaktivieren von Build-Komponenten können Sie nur die benötigten Module verwenden, die Bibliotheksgröße reduzieren und die Leistung verbessern.

Wenn Sie eine Komponente deaktivieren, können Sie die Einstellungen dieser Komponente nicht mehr bearbeiten. Wenn Sie mehrere Web SDK-Instanzen verwenden, werden die ausgewählten Build-Komponenten auf alle Instanzen angewendet.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei &#x200B;](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Extensions]** und wählen Sie **[!UICONTROL Configure]** auf der [!UICONTROL Adobe Experience Platform Web SDK] aus.
1. Erweitern Sie oben das Akkordeon **[!UICONTROL Custom build components]** .

>[!WARNING]
>
>Eine falsche Änderung dieser Einstellungen kann zu unerwünschten Ergebnissen führen, einschließlich Datenverlust. Testen Sie Ihre Implementierung gründlich in einer Entwicklungsumgebung, bevor Sie diese Änderungen in der Produktionsumgebung veröffentlichen.

Adobe bietet die Möglichkeit, die folgenden Web-SDK-Build-Komponenten zu deaktivieren:

| Komponente erstellen | Beschreibung | Abhängige Funktionen |
| --- | --- | --- |
| **[!UICONTROL Activity collector]** | Ermöglicht die automatische Link-Erfassung und Activity Map-Verfolgung. | |
| **[!UICONTROL Advertising]** | Ermöglicht die Integration von Adobe Advertising mit Customer Journey Analytics. | |
| **[!UICONTROL Audiences]** | Unterstützt die Integration mit Adobe Audience Manager, z. B. ID-Synchronisierungen. | |
| **[!UICONTROL Brand concierge]** | Ermöglicht die Integration mit Brand Concierge. |
| **[!UICONTROL Consent]** | Ermöglicht die Verwendung von Einverständnisfunktionen. | [[!UICONTROL Set consent]](../actions/set-consent.md) |
| **[!UICONTROL Event merge]** | Veraltet. | [[!UICONTROL Event merge ID]](../data-element-types.md) Datenelement (veraltet)<br>[[!UICONTROL Reset event merge ID]](../actions/reset-event-merge-id.md) Aktion (veraltet) |
| **[!UICONTROL Media Analytics bridge]** | Unterstützt die Integration mit älteren Media Analytics-Versionen. | [[!UICONTROL Get media analytics tracker]](../actions/get-media-analytics-tracker.md) |
| **[!UICONTROL Personalization]** | Unterstützt Integrationen mit Adobe Target und Adobe Journey Optimizer. | [[!UICONTROL Apply propositions]](../actions/apply-propositions.md) |
| **[!UICONTROL Push notifications]** | Aktiviert Web-Push-Benachrichtigungen für Adobe Journey Optimizer. | [[!UICONTROL Send push subscription]](../actions/send-push-subscription.md) |
| **[!UICONTROL Rules engine]** | Aktiviert die Geräteentscheidung mit Adobe Journey Optimizer. | [[!UICONTROL Evaluate rulsets]](../actions/evaluate-rulesets.md) Aktion<br> [[!UICONTROL Subscribe ruleset items]](../event-types.md#subscribe-ruleset-items)-Ereignis |
| **[!UICONTROL Streaming media]** | Unterstützt die Integration mit der Streaming-Mediensammlung. | [[!UICONTROL Send media event]](../actions/send-media-event.md) |
