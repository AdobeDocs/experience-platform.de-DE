---
title: Einstellungen zum Überschreiben der Datenstromkonfiguration
description: Ändern Sie Konfigurationseinstellungen, wenn bestimmte Bedingungen erfüllt sind.
source-git-commit: 46e5d007b27eaa67c9ee49e35a711424de383d68
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 3%

---

# Einstellungen zum Überschreiben der Datenstromkonfiguration

Mit Datenstrom-Überschreibungen können Sie zusätzliche Konfigurationen für Ihre Datenströme definieren, die über die Web-SDK an die Edge Network übergeben werden. Mit dieser Funktion können Sie bedingt verschiedene Verhaltensweisen von Datenströmen Trigger werden, ohne einen neuen Datenstrom zu erstellen oder Ihre bestehenden Einstellungen zu ändern.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei &#x200B;](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Extensions]** und wählen Sie **[!UICONTROL Configure]** auf der [!UICONTROL Adobe Experience Platform Web SDK] aus.
1. Scrollen Sie nach unten zum Abschnitt **[!UICONTROL Datastream configuration overrides]** .

Das Überschreiben der Datenstromkonfiguration besteht aus zwei Schritten:

1. Zunächst müssen Sie in der Datenstrom-Benutzeroberfläche [&#x200B; Überschreiben der Datenstromkonfiguration definieren](/help/datastreams/configure.md) wenn Sie einen Datenstrom konfigurieren. Anweisungen [&#x200B; Konfigurieren von Überschreibungen finden Sie &#x200B;](/help/datastreams/overrides.md)Überschreibungen der Datenstromkonfiguration“ in der Dokumentation zu Datenströmen.
1. Nachdem Sie die Datenstrom-Überschreibung in der Datenstrom-Benutzeroberfläche konfiguriert haben, können Sie die Tag-Erweiterung konfigurieren.

Datenstrom-Überschreibungen müssen pro Umgebung konfiguriert werden. Die Entwicklungs-, Staging- und Produktionsumgebungen haben jeweils separate Überschreibungen. Sie können die Überschreibungseinstellungen in eine beliebige Umgebung kopieren:

![Bild, das die Überschreibungen der Datenstromkonfiguration mithilfe der Tag-Erweiterungs-Seite von Web SDK zeigt.](../assets/datastream-overrides.png)

Standardmäßig sind Überschreibungen der Datenstromkonfiguration deaktiviert. Die Option **[!UICONTROL Match datastream configuration]** ist standardmäßig ausgewählt.

![Benutzeroberfläche der Tag-Erweiterung von Web SDK, auf der die Datenstromkonfiguration angezeigt wird, überschreibt die Standardeinstellung.](../assets/datastream-override-default.png)

Um Datenstrom-Überschreibungen in der Tag-Erweiterung zu aktivieren, wählen Sie **[!UICONTROL Enabled]** aus dem Dropdown-Menü aus.

![Benutzeroberfläche der Tag-Erweiterung von Web SDK mit der Einstellung „Überschreibungen der Datenstromkonfiguration aktiviert“.](../assets/datastream-override-enabled.png)

Nachdem Sie die Überschreibungen der Datenstromkonfiguration aktiviert haben, können Sie die Überschreibungen für jeden Service konfigurieren, der unten beschrieben wird. Diese Datenstromüberschreibungseinstellungen setzen alle Server-seitigen Datenstromkonfigurationen und -regeln für die ausgewählte Umgebung außer Kraft.

## Adobe Analytics

Überschreiben des Daten-Routings zum Adobe Analytics-Service.

![UI-Bild der Web SDK-Tag-Erweiterung mit den Einstellungen für die Überschreibung des Adobe Analytics-Datenstroms.](../assets/datastream-override-analytics.png)

* **[!UICONTROL Enabled]**/**[!UICONTROL Disabled]**: Aktivieren oder deaktivieren Sie das Daten-Routing zu Adobe Analytics.
* **[!UICONTROL Report suites]**: Die IDs für die Ziel-Report Suites in Adobe Analytics. Der Wert muss eine vorkonfigurierte Report Suite (oder eine kommagetrennte Liste von Report Suites) aus Ihrer Datenstromkonfiguration sein. Diese Einstellung überschreibt die primären Report Suites.
* **[!UICONTROL Add Report Suite]**: Wählen Sie diese Option, um weitere Report Suites hinzuzufügen.

## Adobe Audience Manager

Überschreiben des Daten-Routings zu Adobe Audience Manager.

![UI-Bild der Web SDK-Tag-Erweiterung mit den Einstellungen für die Überschreibung des Adobe Audience Manager-Datenstroms.](../assets/datastream-override-audience-manager.png)

* **[!UICONTROL Enabled]**/**[!UICONTROL Disabled]**: Aktivieren oder deaktivieren Sie das Daten-Routing zu Adobe Audience Manager.
* **[!UICONTROL Third-party ID sync container]**: Die ID für den Ziel-Synchronisierungs-Container für Drittanbieter-IDs in Audience Manager. Der Wert muss ein vorkonfigurierter sekundärer Container aus Ihrer Datenstromkonfiguration sein und überschreibt den primären Container.

## Adobe Experience Platform

Überschreiben des Daten-Routings zu Adobe Experience Platform.

![UI-Bild der Web SDK-Tag-Erweiterung mit den Einstellungen für die Überschreibung des Adobe Experience Platform-Datenstroms.](../assets/datastream-override-experience-platform.png)

* **[!UICONTROL Enabled]**/**[!UICONTROL Disabled]**: Aktivieren oder deaktivieren Sie das Daten-Routing zu Adobe Experience Platform.
* **[!UICONTROL Event dataset]**: Die ID für den Zielereignis-Datensatz in der Adobe Experience Platform. Der Wert muss ein vorkonfigurierter sekundärer Datensatz aus Ihrer Datenstromkonfiguration sein.
* **[!UICONTROL Offer Decisioning]**: Aktivieren oder deaktivieren Sie das Daten-Routing zum [!DNL Offer Decisioning]-Service.
* **[!UICONTROL Edge Segmentation]**: Aktivieren oder deaktivieren Sie das Daten-Routing zum [!DNL Edge Segmentation]-Service.
* **[!UICONTROL Personalization Destinations]**: Aktivieren oder Deaktivieren des Daten-Routings zu Personalisierungszielen.
* **[!UICONTROL Adobe Journey Optimizer]**: Aktivieren oder deaktivieren Sie das Daten-Routing zu [!DNL Adobe Journey Optimizer].

## Serverseitige Ereignisweiterleitung für Adobe

Überschreiben des Daten-Routings für den Server-seitigen Ereignisweiterleitungs-Service von Adobe.

![Bild der Tag-Erweiterung der Web SDK-Benutzeroberfläche mit den Überschreibungseinstellungen für den Datenstrom der Server-seitigen Ereignisweiterleitung von Adobe.](../assets/datastream-override-ssf.png)

* **[!UICONTROL Enabled]**/**[!UICONTROL Disabled]**: Aktivieren oder deaktivieren Sie das Daten-Routing zum Server-seitigen Ereignisweiterleitungs-Service von Adobe.

## Adobe Target {#target}

Überschreiben des Daten-Routings zu Adobe Target.

![UI-Bild der Web SDK-Tag-Erweiterung mit den Einstellungen für die Überschreibung des Adobe Target-Datenstroms.](../assets/datastream-override-target.png)

* **[!UICONTROL Enabled]**/**[!UICONTROL Disabled]**: Aktivieren oder deaktivieren Sie das Daten-Routing zu Adobe Target.
