---
keywords: Experience Platform;Startseite;beliebte Themen;Datenverwaltung;Datenverwendungsbeschriftung API;Policy-Dienst-API;Datenverwendungsbeschriftungen - Übersicht
solution: Experience Platform
title: Übersicht über Datenverwendungs-Bezeichnungen
topic-legacy: labels
description: Mit der Adobe Experience Platform-Datenverwaltung können Sie Datenverwendungsbeschriftungen auf Datensätze und Felder anwenden und diese entsprechend den jeweiligen Datenverwendungsrichtlinien kategorisieren. Dieses Dokument bietet einen Überblick über die Beschriftungen für die Datenverwendung in der Experience Platform.
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 14%

---

# Datennutzungsbezeichnungen – Übersicht

Mit Adobe Experience Platform [!DNL Data Governance] können Sie Datenverwendungsbezeichnungen auf Datensätze und Felder anwenden und diese entsprechend den entsprechenden Datenverwendungsrichtlinien kategorisieren.

Dieses Dokument bietet eine Übersicht über die Beschriftungen für die Datenverwendung in [!DNL Experience Platform]. Bevor Sie dieses Handbuch lesen, finden Sie in der [Übersicht über die Datenverwaltung](../home.md) eine solidere Einführung in das Data Governance-Framework.

## Informationen zu den Datenverwendungsbeschreibungen

Mit Datennutzungsbeschriftungen können Sie Daten anhand der für diese Daten geltenden Nutzungsrichtlinien kategorisieren. Beschriftungen können jederzeit angewendet werden, was eine flexible Handhabung der Daten ermöglicht. Bewährte Verfahren fördern die Kennzeichnung von Daten, sobald diese in [!DNL Experience Platform] aufgenommen werden oder sobald Daten für die Verwendung in [!DNL Platform] verfügbar sind.

Datennutzungsbeschriftungen, die auf Datensatzebene angewendet werden, werden für alle Felder des Datensatzes übernommen. Außerdem können Beschriftungen direkt auf einzelne Felder (Spaltenüberschriften) in einem Datensatz angewendet werden, ohne dass eine Übernahme erfolgt.

[!DNL Platform] bietet mehrere standardmäßige &quot;Kern&quot;-Datenverwendungsbezeichnungen, die eine Vielzahl von allgemeinen Einschränkungen für die Datenverwaltung abdecken. Weitere Informationen zu diesen Beschriftungen und den von ihnen dargestellten Nutzungsrichtlinien finden Sie im Handbuch [Beschriftungen für die Verwendung von Kerndaten](reference.md).

Zusätzlich zu den von der Adobe bereitgestellten Bezeichnungen können Sie auch eigene benutzerdefinierte Bezeichnungen für Ihr Unternehmen definieren. Weitere Informationen finden Sie im Abschnitt [Verwalten von Bezeichnungen](#manage-labels).

## Beschriftungsvererbung für Audiencen

Alle von [Adobe Experience Platform Segmentation Service](../../segmentation/home.md) erstellten Segmentsegmente übernehmen die Gebrauchsbeschriftungen der zugehörigen Datensätze. Dies ermöglicht die Experience Platform, bei der Aktivierung von Segmenten an Zielen eine automatische Durchsetzung der Datenverwendungsrichtlinie zu gewährleisten.

Neben der Vererbung von Bezeichnungen auf Datensatzebene übernehmen Segmente standardmäßig alle Bezeichnungen auf Feldebene aus den zugehörigen Datensätzen. Daher können Sie leichter identifizieren, welche Attribute aus Ihren Segmenten ausgeschlossen werden sollen, und verhindern, dass sie Beschriftungen von ausgeschlossenen Feldern übernehmen.

Weitere Informationen zur Funktionsweise der automatischen Durchsetzung in Platform finden Sie im Überblick über [automatische Richtliniendurchsetzung](../enforcement/auto-enforcement.md).

### Vererbung von Adobe Audience Manager Data Export Controls

[!DNL Experience Platform] hat die Möglichkeit, Segmente für Adobe Audience Manager freizugeben. Alle Datenexportsteuerelemente, die auf Audience Manager angewendet wurden, werden in entsprechende Beschriftungen und Marketingaktionen übersetzt, die von [!DNL Experience Platform] [!DNL Data Governance] erkannt werden.

Eine Referenz dazu, wie bestimmte Datenexportsteuerelemente den Datenverwendungsbeschriftungen in [!DNL Platform] zugeordnet sind, finden Sie in der [Audience Manager-Dokumentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep).

## Verwalten von Datenverwendungsbeschriftungen in [!DNL Experience Platform] {#manage-labels}

Sie können Datenverwendungsbeschriftungen mit [!DNL Experience Platform]-APIs oder der Benutzeroberfläche verwalten. Einzelheiten zu den einzelnen Unterabschnitten finden Sie in den folgenden Abschnitten.

### Verwenden der UI

Der Arbeitsbereich **[!UICONTROL Richtlinien]** in der [!DNL Experience Platform]-Benutzeroberfläche ermöglicht die Ansicht und Verwaltung von Kern- und benutzerdefinierten Beschriftungen für Ihr Unternehmen. Im Arbeitsbereich **[!DNL Datasets]** können Sie Beschriftungen auf Datensätze und Felder anwenden. Weitere Informationen finden Sie im Benutzerhandbuch [Beschriftungen](user-guide.md).

### APIs verwenden

Der `/labels`-Endpunkt in der [Policy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) ermöglicht Ihnen die programmgesteuerte Verwaltung von Datenverwendungsbeschriftungen, einschließlich der Erstellung benutzerdefinierter Bezeichnungen. Weitere Informationen finden Sie im Endpunktleitfaden [Beschriftungen](../api/labels.md).

Die [DataSet-Dienst-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml) wird verwendet, um Beschriftungen für Dataset und Felder zu verwalten. Weitere Informationen finden Sie im Handbuch [Verwalten von Datenbezeichnungen](./dataset-api.md).

## Nächste Schritte

In diesem Dokument wurden die Bezeichnungen der Datenverwendung und ihre Rolle im Rahmen der Datenverwaltung vorgestellt. Weitere Informationen zur Verwaltung von Beschriftungen in [!DNL Experience Platform] finden Sie in der Dokumentation, die mit diesem Handbuch verknüpft ist.
