---
keywords: Experience Platform; Startseite; beliebte Themen; Quellen; Connectoren; Quell-Connectoren; Kampagne; Kampagnenverwaltete Dienste
title: Erstellen einer Adobe Campaign Managed Services-Quellverbindung über die Platform-Benutzeroberfläche
description: Erfahren Sie, wie Sie über die Platform-Benutzeroberfläche eine Verbindung zwischen Adobe Experience Platform und Adobe Campaign Managed Services herstellen.
hide: true
hidefromtoc: true
source-git-commit: 24d7a549e83245fc363bd76f26ba58130e980c6c
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 4%

---


# Erstellen einer Adobe Campaign Managed Services-Quellverbindung über die Platform-Benutzeroberfläche

In diesem Tutorial erfahren Sie, wie Sie einen Quell-Connector erstellen, um Ihre Adobe Campaign Managed Services-Daten in Adobe Experience Platform zu übertragen.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Experience Platform voraus:

* [Quellen](../../../../home.md): Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten zu strukturieren, zu beschriften und zu erweitern, indem [!DNL Platform] Dienste.
* [Sandboxes](../../../../../sandboxes/home.md): Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen aufteilen, um die Entwicklung und Weiterentwicklung von Programmen für digitale Erlebnisse zu erleichtern.

## Verbinden von Adobe Campaign Managed Services mit Platform

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Quellen]** über die linke Navigationsleiste auf [!UICONTROL Quellen] Arbeitsbereich. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Sie können auch die Suchleiste verwenden, um die angezeigten Quellen einzugrenzen.

Unter dem **[!UICONTROL Adobe Apps]** category, select **[!UICONTROL Adobe Campaign Managed Services]** und wählen Sie **[!UICONTROL Daten hinzufügen]**.

### Daten auswählen

Die [!UICONTROL Daten auswählen] -Schritt angezeigt wird und Sie eine Oberfläche zum Konfigurieren von Werten für Ihre [!UICONTROL Adobe Campaign-Instanz], [!UICONTROL Zielgruppen-Mapping]und [!UICONTROL Schemaname].

#### Kampagneninstanz auswählen {#select-campaign-instance}

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_instance"
>title="Kampagneninstanz auswählen"
>abstract="Der Name der Adobe Campaign Classic-Umgebung, die Sie verwenden möchten."
>text="Learn more in documentation"

#### Kampagnenzuordnung auswählen {#select-campaign-mapping}

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_mapping"
>title="Zielgruppen-Mapping der Kampagne auswählen"
>abstract="Zielgruppen-Mappings sind technische Objekte, die von Campaign zum Versand von Nachrichten verwendet werden und alle technischen Einstellungen enthalten, die für den Versand erforderlich sind (Adressen, Telefonnummern, Opt-in-Indikatoren, zusätzliche Kennungen usw.)."
>text="Learn more in documentation"

#### Kampagnenschema auswählen {#select-campaign-schema}

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_schema"
>title="Name des Kampagnenschemas auswählen"
>abstract="Der Name der in der Adobe Campaign-Datenbank definierten Entität."
>text="Learn more in documentation"
