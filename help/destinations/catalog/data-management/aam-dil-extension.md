---
keywords: Audience Manager DIL Extension;Ziel-Audience-Manager;dil-Erweiterung
title: Audience Manager DIL-Erweiterung
description: Die Audience Manager DIL Extension ist ein DMP-Ziel (Data Management Platform) in Adobe Experience Platform. Weitere Informationen zur Funktionalität der Erweiterung finden Sie auf der Seite der Erweiterung auf Adobe Exchange.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 30%

---


# Audience Manager DIL-Erweiterung {#aam-dil-extension}

## Übersicht {#overview}

Dies ist die Adobe Audience Manager Data Integration Library-Erweiterung (Client-seitige Implementierung). Hinweis: Diese Erweiterung ist nicht für die Server-seitige Weiterleitung (Server-Side Forwarding, SSF) von Adobe Analytics-Daten vorgesehen. Nutzen Sie für SSF die Adobe Analytics-Erweiterung. Wichtig: Ab Version 8.0 ist DIL stark vom [!DNL Experience Cloud] ID-Dienst, Version 3.3 oder höher, abhängig. Implementieren Sie für vollständige [!DNL Audience Manager]-Datenintegrationsfunktionen sowohl den ID-Dienst als auch die DIL.[!DNL Experience Cloud]

[!DNL Audience Manager] DIL ist eine DMP-Erweiterung (Data Management Platform) in Adobe Experience Platform. Weiterführende Informationen zur Erweiterungsfunktion finden Sie auf der Seite [Audience Manager-Erweiterung](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/adobe-audience-manager-extension.html) in der Experience Platform Launch-Dokumentation.

Dieses Ziel ist eine [!DNL Experience Platform Launch]-Erweiterung. Weitere Informationen zur Funktionsweise von Starterweiterungen in der Plattform finden Sie unter [Übersicht über Experience Platform Launch-Erweiterungen](../launch-extensions/overview.md).

![Audience Manager DIL-Erweiterung](../../assets/catalog/data-management-platform/aam-dil-extension/configure.png)

## Voraussetzungen  {#prerequisites}

Diese Erweiterung ist im Katalog [!DNL Destinations] für alle Kunden verfügbar, die Platform gekauft haben.

Um diese Erweiterung verwenden zu können, benötigen Sie Zugriff auf [!DNL Adobe Experience Platform Launch]. [!DNL Platform Launch] wird Adobe Experience Cloud-Kunden als eine zusätzliche Funktion angeboten. Wenden Sie sich an Ihren Unternehmensadministrator, um Zugriff auf [!DNL Platform Launch] zu erhalten, und bitten Sie ihn, Ihnen die **[!UICONTROL manage_properties]**-Berechtigung zu erteilen, damit Sie Erweiterungen installieren können.

## Installieren einer Erweiterung {#install-extension}

So installieren Sie die DIL-Erweiterung [!DNL Audience Manager]:

Wechseln Sie in der [Plattform-Schnittstelle](http://platform.adobe.com/) zu **[!UICONTROL Ziele]** > **[!UICONTROL Katalog]**.

Wählen Sie die Erweiterung aus dem Katalog aus oder verwenden Sie die Suchleiste.

Klicken Sie auf das Ziel, um es hervorzuheben, und wählen Sie dann **[!UICONTROL Konfigurieren]** in der rechten Leiste aus. Wenn das Steuerelement **[!UICONTROL Configure]** ausgegraut ist, fehlt Ihnen die Berechtigung **[!UICONTROL manage_properties]**. Siehe [Voraussetzungen](#prerequisites).

Wählen Sie im Fenster **[!UICONTROL Select available Launch property]** die [!DNL Launch]-Eigenschaft aus, in der Sie die Erweiterung installieren möchten. Sie können auch eine neue Eigenschaft in Launch erstellen. Eine Eigenschaft ist eine Sammlung von Regeln, Datenelementen, konfigurierten Erweiterungen, Umgebungen und Bibliotheken. Weitere Informationen zu Eigenschaften finden Sie im Abschnitt [Seite &quot;Eigenschaften&quot;der [!DNL Launch]-Dokumentation.](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page)

Der Arbeitsablauf führt Sie zu [!DNL Launch], um die Installation abzuschließen.

Informationen zu den Erweiterungskonfigurationsoptionen finden Sie auf der [Audience Manager-Erweiterungsseite](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/adobe-audience-manager-extension.html) in der [!DNL Experience Launch]-Dokumentation.

Sie können die Erweiterung auch direkt in der [Adobe Experience Platform Launch-Schnittstelle](https://launch.adobe.com/) installieren. Siehe [Hinzufügen einer neuen Erweiterung](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension) in der [!DNL Platform Launch]-Dokumentation.

## Verwenden der Erweiterung {#how-to-use}

Nachdem Sie die Erweiterung installiert haben, können Sie Beginn zum Einrichten von Regeln für diese Erweiterung direkt in [!DNL Platform Launch] erstellen.

Unter [!DNL Platform Launch] können Sie Regeln für Ihre installierten Erweiterungen einrichten, um Ereignis-Daten nur in bestimmten Situationen an das Erweiterungsziel zu senden. Weitere Informationen zum Einrichten von Regeln für Erweiterungen finden Sie in der [Regeldokumentation](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html).

## Konfigurieren, Aktualisieren und Löschen von Erweiterungen {#configure-upgrade-delete}

Sie können Erweiterungen in der [!DNL Platform Launch]-Schnittstelle konfigurieren, aktualisieren und löschen.

>[!TIP]
>
>Wenn die Erweiterung bereits auf einer Ihrer Eigenschaften installiert ist, zeigt die Plattform-Benutzeroberfläche für die Erweiterung weiterhin **[!UICONTROL Install]** an. Starten Sie den Installations-Workflow, wie unter [Installieren einer Erweiterung](#install-extension) beschrieben, um zu zu wechseln und Ihre Erweiterung zu konfigurieren oder zu löschen.[!DNL Platform Launch]

Informationen zum Aktualisieren Ihrer Erweiterung finden Sie unter [Extension-Aktualisierung](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html) in der [!DNL Platform Launch]-Dokumentation.



