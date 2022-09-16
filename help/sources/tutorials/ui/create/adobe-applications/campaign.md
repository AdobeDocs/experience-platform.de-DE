---
keywords: Experience Platform;Startseite;beliebte Themen;Quellen;Connectoren;Quell-Connectoren;Kampagne;Kampagnenverwaltete Services
title: Erstellen einer Managed Services-Quellverbindung mit Adobe Campaign über die Platform-Benutzeroberfläche
description: Erfahren Sie, wie Sie über die Platform-Benutzeroberfläche eine Verbindung zwischen Adobe Experience Platform und Managed Services in Adobe Campaign herstellen.
hide: true
hidefromtoc: true
exl-id: 067ed558-b239-4845-8c85-3bf9b1d4caed
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 100%

---

# Erstellen einer Managed Services-Quellverbindung mit Adobe Campaign über die Platform-Benutzeroberfläche

In diesem Tutorial erfahren Sie, wie Sie einen Quell-Connector erstellen, um Ihre Managed Services-Daten von Adobe Campaign in Adobe Experience Platform zu übertragen.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Experience Platform voraus:

* [Quellen](../../../../home.md): Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, eingehende Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

## Verbinden von Managed Services in Adobe Campaign mit Platform

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Quellen]** in der linken Navigationsleiste, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Sie können auch die Suchleiste verwenden, um die angezeigten Quellen einzugrenzen.

Wählen Sie unter der Kategorie **[!UICONTROL Adobe-Programme]** die Option **[!UICONTROL Adobe Campaign Managed Services]** und anschließend die Option **[!UICONTROL Daten hinzufügen]**.

### Auswählen von Daten {#select-data}

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_instance"
>title="ACC-Instanz"
>abstract="Der Name der Adobe Campaign Classic-Umgebung, die Sie verwenden möchten."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_mapping"
>title="Zielgruppenzuordnung"
>abstract="Zielgruppenzuordnungen sind technische Objekte, die von Campaign zum Versand von Nachrichten verwendet werden und alle technischen Einstellungen enthalten, die für den Versand erforderlich sind (Adressen, Telefonnummern, Opt-in-Indikatoren, zusätzliche Kennungen usw.)."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_campaign_schema"
>title="Schemaname"
>abstract="Der Name der in der Adobe Campaign-Datenbank definierten Entität."
>text="Learn more in documentation"

Der Schritt [!UICONTROL Daten auswählen] wird angezeigt und bietet Ihnen eine Schnittstelle zur Konfiguration von Werten für Ihre [!UICONTROL Adobe Campaign-Instanz], [!UICONTROL Zielgruppenzuordnung] und [!UICONTROL Schemaname].
