---
keywords: Experience Platform;home;popular topics;data governance;data usage label api;policy service api;data usage labels overview
solution: Experience Platform
title: Datennutzungsbezeichnungen – Übersicht
topic: labels
description: Data Usage Labeling and Enforcement (DULE) ist der zentrale Mechanismus zur Umsetzung von Data Governance in Adobe Experience Platform. Mit den im Rahmen von DULE bereitgestellten Funktionen lassen sich Datensätze und Felder anhand von Beschriftungen für die Datennutzung entsprechend den für sie geltenden Nutzungsrichtlinien kategorisieren. Dieses Dokument bietet einen Überblick über die Beschriftungen für die Datenverwendung (auch als DULE-Beschriftungen bezeichnet) in der Experience Platform.
translation-type: tm+mt
source-git-commit: cddc559dfb65ada888bb367d6265863091a9b2a1
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 20%

---


# Datennutzungsbezeichnungen – Übersicht

Adobe Experience Platform [!DNL Data Governance] allows you to apply data usage labels to datasets and fields, categorizing each according to related data usage policies.

Dieses Dokument bietet eine Übersicht über die Beschriftungen für die Datenverwendung in [!DNL Experience Platform]. Bevor Sie dieses Handbuch lesen, lesen Sie sich die Übersicht über die [Datenverwaltung](../home.md) durch, um eine solidere Einführung in das Data Governance-Framework zu erhalten.

## Informationen zu den Datenverwendungsbeschreibungen

Mit Datennutzungsbeschriftungen können Sie Daten anhand der für diese Daten geltenden Nutzungsrichtlinien kategorisieren. Beschriftungen können jederzeit angewendet werden, was eine flexible Handhabung der Daten ermöglicht. Best practices encourage labeling data as soon as it is ingested into [!DNL Experience Platform], or as soon as data becomes available for use in [!DNL Platform].

Datennutzungsbeschriftungen, die auf Datensatzebene angewendet werden, werden für alle Felder des Datensatzes übernommen. Außerdem können Beschriftungen direkt auf einzelne Felder (Spaltenüberschriften) in einem Datensatz angewendet werden, ohne dass eine Übernahme erfolgt.

[!DNL Platform] bietet mehrere standardmäßige &quot;Kern&quot;-Datenverwendungsbezeichnungen, die eine Vielzahl von allgemeinen Einschränkungen für die Datenverwaltung abdecken. Weitere Informationen zu diesen Beschriftungen und den von ihnen dargestellten Nutzungsrichtlinien finden Sie im Handbuch zu den [Gebrauchsbeschriftungen](reference.md)der Kerndaten.

Zusätzlich zu den von der Adobe bereitgestellten Bezeichnungen können Sie auch eigene benutzerdefinierte Bezeichnungen für Ihr Unternehmen definieren. Weitere Informationen finden Sie im Abschnitt zum [Verwalten von Bezeichnungen](#manage-labels) .

## Beschriftungsvererbung für Audiencen

Alle vom [Adobe Experience Platform Segmentation Service](../../segmentation/home.md) erstellten Segmentsegmente übernehmen die Gebrauchsbeschriftungen der zugehörigen Datensätze. Dies ermöglicht Anwendungen, die auf [!DNL Experience Platform] (z. B. [!DNL Real-time Customer Data Platform]) aufbauen, eine automatische Durchsetzung der Datenverwendungsrichtlinien bei der Aktivierung von Segmenten an Ziele zu ermöglichen.

Neben der Vererbung von Bezeichnungen auf Datensatzebene übernehmen Segmente standardmäßig alle Bezeichnungen auf Feldebene aus den zugehörigen Datensätzen. Je nachdem, wie Ihre [!DNL Platform]basierte Anwendung Segmente verbraucht, können Sie potenziell angeben, welche Felder verwendet werden, wodurch verhindert wird, dass das Segment Beschriftungen aus ausgeschlossenen Feldern erbt.

Weitere Informationen zur Funktionsweise der automatischen Durchsetzung in Echtzeit-CDP finden Sie in der Übersicht zur [Datenverwaltung in Echtzeit-CDP](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance).

### Vererbung von Adobe Audience Manager Data Export Controls

[!DNL Experience Platform] hat die Möglichkeit, Segmente für Adobe Audience Manager freizugeben. Alle Datenexportsteuerelemente, die auf Audience Manager angewendet wurden, werden in entsprechende Beschriftungen und Marketingaktionen übersetzt, die von [!DNL Experience Platform][!DNL Data Governance]erkannt werden.

Eine Referenz dazu, wie bestimmte Datenexportsteuerelemente den Datenverwendungsbeschriftungen in zugeordnet werden, [!DNL Platform]finden Sie in der Dokumentation zum [Audience Manager](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep).

## Verwalten von Datenverwendungsbeschriftungen in [!DNL Experience Platform] {#manage-labels}

Sie können Datenverwendungsbeschriftungen mit [!DNL Experience Platform] APIs oder der Benutzeroberfläche verwalten. Einzelheiten zu den einzelnen Unterabschnitten finden Sie in den folgenden Abschnitten.

### Verwenden der UI

Der Arbeitsbereich &quot; **[!UICONTROL Richtlinien]** &quot;in der [!DNL Experience Platform] Benutzeroberfläche ermöglicht die Ansicht und Verwaltung von Kern- und benutzerdefinierten Beschriftungen für Ihr Unternehmen. Im **[!DNL Datasets]** Arbeitsbereich können Sie Beschreibungen auf Datensätze und Felder anwenden. Weitere Informationen finden Sie im Benutzerhandbuch für [Beschriftungen](user-guide.md).

### APIs verwenden

Der `/labels` Endpunkt in der [Policy Service-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) ermöglicht es Ihnen, Datenverwendungsbeschriftungen programmgesteuert zu verwalten, einschließlich der Erstellung benutzerdefinierter Bezeichnungen. Weitere Informationen finden Sie in der [Endpunktanleitung](../api/labels.md) für Beschriftungen.

Die [DataSet-Dienst-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml) wird verwendet, um Beschriftungen für Dataset und Felder zu verwalten. Weitere Informationen finden Sie im Handbuch zur [Verwaltung von Datenbezeichnungen](./dataset-api.md) .

## Nächste Schritte

In diesem Dokument wurden die Bezeichnungen der Datenverwendung und ihre Rolle im Rahmen der Datenverwaltung vorgestellt. Weitere Informationen zum Verwalten von Etiketten in finden Sie in der Dokumentation, die mit diesem Handbuch verknüpft ist [!DNL Experience Platform].