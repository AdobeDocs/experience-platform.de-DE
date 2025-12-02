---
title: Einstellungen für die Datenstromkonfiguration
description: Konfigurieren Sie den Datenstrom, um Daten mithilfe der Tag-Erweiterung „Web SDK" an zu senden.
source-git-commit: 46e5d007b27eaa67c9ee49e35a711424de383d68
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 1%

---

# Einstellungen für die Datenstromkonfiguration

In diesem Konfigurationsabschnitt können Sie festlegen, an welchen [Datenstrom](/help/datastreams/overview.md) Sie Daten senden möchten. **Für alle Daten, die an Edge Network gesendet werden, ist eine Datenstrom-ID erforderlich.**

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei ](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Extensions]** und wählen Sie **[!UICONTROL Configure]** auf der [!UICONTROL Adobe Experience Platform Web SDK] aus.
1. Scrollen Sie nach unten zum Abschnitt **[!UICONTROL Datastreams]** .

![Bild mit den Datenstromeinstellungen der Tag-Erweiterung „Web SDK&quot; in der Tags-Benutzeroberfläche](../assets/web-sdk-ext-datastreams.png)

Bei der Auswahl von Datenströmen können Sie dies für jede [Umgebung](/help/tags/ui/publishing/environments.md) ([!UICONTROL Development], [!UICONTROL Staging] und [!UICONTROL Production]) tun. Diese Felder sind nützlich, wenn Sie Daten trennen möchten, die zwischen Entwicklungs-, Staging- und Produktionsumgebungen gesendet werden. Dies ermöglicht einen praktischen Workflow, bei dem Sie sich keine Gedanken darüber machen müssen, Daten an den falschen Datenstrom zu senden, solange Sie den richtigen Tag-Loader in der jeweiligen Umgebung installieren.

Sie können Datenstrom-IDs mit einer der folgenden Methoden ausfüllen:

* **[!UICONTROL Choose from list]**: Jede Umgebung enthält zwei Dropdown-Menüs, über die Sie die Sandbox und den Datenstrom für die ausgewählte Umgebung auswählen können. Die Werte in den einzelnen Dropdown-Menüs hängen von Ihren konfigurierten [Datenströmen](/help/datastreams/overview.md) innerhalb der jeweiligen [Sandbox](/help/sandboxes/ui/overview.md) ab.

* **[!UICONTROL Enter values]**: Alternativ zur Verwendung von Dropdown-Menüs zur Auswahl des gewünschten Datenstroms können Sie die gewünschte Datenstrom-ID manuell direkt angeben. Jede Umgebung ermöglicht die direkte Eingabe einer Datenstrom-ID oder das Ausfüllen dieses Felds mithilfe eines [Datenelements](/help/tags/ui/managing-resources/data-elements.md).
