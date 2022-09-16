---
keywords: foresee; Erweiterung vorsehen; Ziel vorhersehen
title: Foresee-Erweiterungsziel
description: Die Foresee-Erweiterung ist ein Umfrageziel in Adobe Experience Platform. Weitere Informationen zur Funktionalität der Erweiterung finden Sie auf der Seite der Erweiterung auf Adobe Exchange.
exl-id: 3eca9e2e-fd41-4dca-a38f-8e281c45a01b
source-git-commit: b4e869f9bc29122db4fc66ccda752a50c7db729f
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 22%

---

# [!DNL Foresee]-Erweiterung  {#foresee-extension}

## Übersicht {#overview}

Konfigurieren [!DNL ForeSee] Produktbereitstellungen mithilfe von Tags.

[!DNL Foresee] ist eine Umfrageerweiterung in Adobe Experience Platform. Weitere Informationen zur Funktionalität der Erweiterung finden Sie auf der Seite der Erweiterung auf [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.100164.html).

Dieses Ziel ist eine Tag-Erweiterung. Weitere Informationen zur Funktionsweise von Tag-Erweiterungen in Platform finden Sie unter [Tag-Erweiterungen - Übersicht](../launch-extensions/overview.md).

![Foresee-Erweiterung](../../assets/catalog/survey/foresee/catalog.png)

## Voraussetzungen {#prerequisites}

Diese Erweiterung ist im Abschnitt [!DNL Destinations] Katalog für alle Kunden, die Platform erworben haben.

Um diese Erweiterung verwenden zu können, benötigen Sie Zugriff auf Tags in Adobe Experience Platform. Tags werden Adobe Experience Cloud-Kunden als integrierte Mehrwertfunktion angeboten. Wenden Sie sich an Ihren Organisationsadministrator, um Zugriff auf Tags zu erhalten, und bitten Sie ihn, Ihnen die **[!UICONTROL manage_properties]** -Berechtigung, damit Sie Erweiterungen installieren können.

## Installieren einer Erweiterung {#install-extension}

So installieren Sie die [!DNL Foresee] Erweiterung:

Im [Plattform-Benutzeroberfläche](https://platform.adobe.com/), gehen Sie zu **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]**.

Wählen Sie die Erweiterung aus dem Katalog aus oder verwenden Sie die Suchleiste.

Klicken Sie auf das Ziel, um es zu markieren, und wählen Sie dann **[!UICONTROL Konfigurieren]** in der rechten Leiste. Wenn die Variable **[!UICONTROL Konfigurieren]** Kontrolle ausgegraut ist, fehlt die **[!UICONTROL manage_properties]** Berechtigung. Siehe [Voraussetzungen](#prerequisites).

Wählen Sie die Eigenschaft aus, in der Sie die Erweiterung installieren möchten. Sie können auch eine neue Eigenschaft erstellen. Eine Eigenschaft ist eine Sammlung von Regeln, Datenelementen, konfigurierten Erweiterungen, Umgebungen und Bibliotheken. Informationen zu den Eigenschaften in [Eigenschaftenseitenabschnitt](../../../tags/ui/administration/companies-and-properties.md#properties-page) in der Tag-Dokumentation.

Der Workflow führt Sie durch die Schritte zum Abschluss der Installation.

Informationen zu den Konfigurationsoptionen für Erweiterungen finden Sie unter [Foresee-Erweiterungsseite](https://exchange.adobe.com/experiencecloud.details.100164.html) auf Adobe Exchange.

Sie können die Erweiterung auch direkt im [Datenerfassungs-Benutzeroberfläche](https://experience.adobe.com/#/data-collection/). Weitere Informationen finden Sie im Abschnitt zu [Hinzufügen einer neuen Erweiterung](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) in der Tag-Dokumentation.

## Verwenden der Erweiterung {#how-to-use}

Nachdem Sie die Erweiterung installiert haben, können Sie mit der Einrichtung von Regeln beginnen.

Sie können Regeln für Ihre installierten Erweiterungen einrichten, damit nur in bestimmten Situationen Ereignisdaten an das Erweiterungsziel gesendet werden. Weitere Informationen zum Einrichten von Regeln für Ihre Erweiterungen finden Sie unter [Tag-Dokumentation](../../../tags/ui/managing-resources/rules.md).

## Konfigurieren, Aktualisieren und Löschen von Erweiterungen {#configure-upgrade-delete}

Sie können Erweiterungen in der Datenerfassungs-Benutzeroberfläche konfigurieren, aktualisieren und löschen.

>[!TIP]
>
>Wenn die Erweiterung bereits in einer Ihrer Eigenschaften installiert ist, wird die Platform-Benutzeroberfläche weiterhin angezeigt **[!UICONTROL Installieren]** für die Erweiterung. Starten Sie den Installations-Workflow wie unter [Installieren der Erweiterung](#install-extension) , um Ihre Erweiterung zu konfigurieren oder zu löschen.

Informationen zum Aktualisieren Ihrer Erweiterung finden Sie im Handbuch im [Erweiterungs-Upgrade-Prozess](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) in der Tag-Dokumentation.
