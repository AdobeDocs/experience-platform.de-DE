---
keywords: Kickfire;Kickfire;Kickfire-Erweiterung;Kickfire-Erweiterung
title: KickFire-Erweiterung
description: Die KickFire-Erweiterung ist ein Personalisierungsziel in Adobe Experience Platform. Weitere Informationen zur Funktionalität der Erweiterung finden Sie auf der Seite zu Erweiterungen auf Adobe Exchange.
exl-id: c2313474-05d5-4c06-8aa5-ed10e9e9226e
source-git-commit: 20427c4c8826905a77fac04d055d523b12a6f739
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 58%

---

# [!DNL KickFire]-Erweiterung {#kickfire-extension}

## Überblick {#overview}

[!DNL KickFire's] IP-Adressanalyse und B2B-firmografische Daten übersetzen IP-Adressen in Unternehmen, identifizieren anonyme Web-Besucher und integrieren Account-Daten in Ihren Technologie-Stack - alles basierend auf der IP-Adresse eines Unternehmens.

[!DNL KickFire] ist eine Personalisierungserweiterung in [!DNL Adobe Experience Platform]. Weitere Informationen zur Erweiterungsfunktion finden Sie auf der [Kickfire-Website](https://www.kickfire.com/).

Dieses Ziel ist eine Tag-Erweiterung. Weitere Informationen zur Funktionsweise von Tag-Erweiterungen in Experience Platform finden Sie unter [Tag-Erweiterungen - Übersicht](../launch-extensions/overview.md).

![Kickfire-Erweiterung](../../assets/catalog/personalization/kickfire/catalog.png)

## Voraussetzungen {#prerequisites}

Diese Erweiterung ist im [!DNL Destinations] für alle Kunden verfügbar, die Experience Platform erworben haben.

Um diese Erweiterung verwenden zu können, benötigen Sie Zugriff auf Tags in [!DNL Adobe Experience Platform]. Tags werden [!DNL Adobe Experience Cloud] Kunden als integrierte Mehrwertfunktion angeboten. Wenden Sie sich an den Admin Ihrer Organisation, um Zugriff auf Tags zu erhalten, und bitten Sie darum, Ihnen die **[!UICONTROL manage_properties]** Berechtigung zu erteilen, damit Sie Erweiterungen installieren können.

## Installieren einer Erweiterung {#install-extension}

So installieren Sie die [!DNL KickFire]-Erweiterung:

Wechseln Sie in der [Experience Platform](https://platform.adobe.com/)Benutzeroberfläche zu **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Wählen Sie die Erweiterung aus dem Katalog aus oder verwenden Sie die Suchleiste.

Wählen Sie das Ziel aus und klicken Sie dann in der rechten Leiste auf **[!UICONTROL Configure]** . Wenn das **[!UICONTROL Configure]** ausgegraut ist, fehlt die **[!UICONTROL manage_properties]**. Siehe [Voraussetzungen](#prerequisites).

Wählen Sie die Eigenschaft aus, in der Sie die Erweiterung installieren möchten. Sie können auch eine neue Eigenschaft erstellen. Eine Eigenschaft ist eine Sammlung von Regeln, Datenelementen, konfigurierten Erweiterungen, Umgebungen und Bibliotheken. Informationen zu Eigenschaften finden Sie im [Eigenschaften-Seitenabschnitt](../../../tags/ui/administration/companies-and-properties.md#properties-page) der Tags-Dokumentation.

Der Workflow führt Sie durch die Schritte zum Abschließen der Installation.

Sie können die Erweiterung auch direkt in der [Datenerfassungs-Benutzeroberfläche](https://experience.adobe.com/#/data-collection/) installieren. Weitere Informationen finden Sie im Abschnitt zum Thema [Hinzufügen einer neuen Erweiterung](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) in der Tag-Dokumentation.

## Verwenden der Erweiterung {#how-to-use}

Nachdem Sie die Erweiterung installiert haben, können Sie mit dem Einrichten von Regeln beginnen.

Sie können Regeln für Ihre installierten Erweiterungen einrichten, damit nur in bestimmten Situationen Ereignisdaten an das Erweiterungsziel gesendet werden. Weitere Informationen zum Einrichten von Regeln für Erweiterungen finden Sie in der [Tags-Dokumentation](../../../tags/ui/managing-resources/rules.md).

## Konfigurieren, Aktualisieren und Löschen von Erweiterungen {#configure-upgrade-delete}

Sie können Erweiterungen in der Datenerfassungs-Benutzeroberfläche konfigurieren, aktualisieren und löschen.

>[!TIP]
>
>Wenn die Erweiterung bereits in einer Ihrer Eigenschaften installiert ist, zeigt die Experience Platform-Benutzeroberfläche weiterhin **[!UICONTROL Install]** für die Erweiterung an. Starten Sie den Installations-Workflow, wie unter [Installieren einer Erweiterung](#install-extension) beschrieben, um Ihre Erweiterung zu konfigurieren oder zu löschen.

Informationen zum Aktualisieren Ihrer Erweiterung finden Sie in der Anleitung zum [Erweiterungs-Upgrade-Prozess](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) in der Tags-Dokumentation.
