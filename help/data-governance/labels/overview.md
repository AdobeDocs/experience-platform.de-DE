---
keywords: Experience Platform;Startseite;beliebte Themen;Datenverwaltung;Datennutzungsbeschriftungs-API;Richtlinien-Service-API;Übersicht zu Datennutzungsbeschriftungen
solution: Experience Platform
title: Datennutzungsbeschriftungen – Übersicht
topic-legacy: labels
description: Mit Adobe Experience Platform Data Governance können Sie Datennutzungsbeschriftungen auf Datensätze und Felder anwenden und diese entsprechend den für sie geltenden Nutzungsrichtlinien kategorisieren. Dieses Dokument bietet einen Überblick über Datennutzungsbeschriftungen in Experience Platform.
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 100%

---

# Datennutzungsbeschriftungen – Übersicht

Mit Adobe Experience Platform Data Governance können Sie Datennutzungskennzeichnungen auf Datensätze und Felder anwenden und diese so entsprechend den für sie geltenden Nutzungsrichtlinien kategorisieren.

Dieses Dokument bietet eine Übersicht über Datennutzungsbeschriftungen in [!DNL Experience Platform]. Bevor Sie dieses Handbuch lesen, finden Sie in der [Übersicht zu Data Governance](../home.md) eine solidere Einführung in das Data Governance-Framework.

## Verstehen von Datennutzungsbeschriftungen

Mit Datennutzungsbeschriftungen können Sie Datensätze anhand der für diese Daten geltenden Nutzungsrichtlinien kategorisieren. Beschriftungen können jederzeit angewendet werden, was eine flexible Handhabung der Daten ermöglicht. Best Practices legen nahe, Daten direkt bei ihrer Aufnahme in [!DNL Experience Platform] oder ab dem Zeitpunkt ihrer Nutzbarkeit in [!DNL Platform] mit einer Beschriftung zu versehen.

Datennutzungsbeschriftungen, die auf Datensatzebene angewendet werden, werden für alle Felder des Datensatzes übernommen. Außerdem können Beschriftungen direkt auf einzelne Felder (Spaltenüberschriften) in einem Datensatz angewendet werden, ohne dass eine Übernahme erfolgt.

[!DNL Platform] bietet mehrere standardmäßige „Kern“-Datennutzungsbeschriftungen, die eine Vielzahl von allgemeinen Einschränkungen für die Datenverwaltung abdecken. Weitere Informationen zu diesen Beschriftungen und den von ihnen dargestellten Nutzungsrichtlinien finden Sie im Handbuch zu [Kerndatennutzungsbeschriftungen](reference.md).

Zusätzlich zu den von Adobe bereitgestellten Beschriftungen können Sie auch eigene benutzerdefinierte Beschriftungen für Ihr Unternehmen definieren. Weitere Informationen finden Sie im Abschnitt [Verwalten von Beschriftungen](#manage-labels).

## Beschriftungsvererbung für Zielgruppensegmente

Alle von [Adobe Experience Platform Segmentation Service](../../segmentation/home.md) erstellten Zielgruppensegmente übernehmen die Nutzungsbeschriftungen der zugehörigen Datensätze. Dies ermöglicht Experience Platform, bei der Aktivierung von Segmenten für Ziele eine automatische Durchsetzung der Datennutzungsrichtlinie zu gewährleisten.

Neben der Vererbung von Beschriftungen auf Datensatzebene übernehmen Segmente standardmäßig alle Beschriftungen auf Feldebene aus den zugehörigen Datensätzen. Daher können Sie leichter identifizieren, welche Attribute bei Ihren Segmenten ausgeschlossen werden sollen, und so verhindern, dass die Segmente Beschriftungen von ausgeschlossenen Feldern übernehmen.

Weitere Informationen zur Funktionsweise der automatischen Durchsetzung in Platform finden Sie in der Übersicht über [automatische Richtliniendurchsetzung](../enforcement/auto-enforcement.md).

### Vererbung von Adobe Audience Manager-Datenexportsteuerelementen

[!DNL Experience Platform] hat die Möglichkeit, Segmente für Adobe Audience Manager freizugeben. Alle Datenexportsteuerelemente, die auf Audience Manager-Segmente angewendet wurden, werden in entsprechende Kennzeichnungen und Marketing-Aktionen übersetzt, die von [!DNL Experience Platform] Data Governance erkannt werden.

Informationen dazu, wie bestimmte Datenexportsteuerelemente den Datennutzungskennzeichnungen in [!DNL Platform] zugeordnet werden, finden Sie in der [Audience Manager-Dokumentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=de#aam-data-export-control-in-aep).

## Verwalten von Datennutzungsbeschriftungen in [!DNL Experience Platform] {#manage-labels}

Sie können Datennutzungsbeschriftungen mit [!DNL Experience Platform]-APIs oder der Benutzeroberfläche verwalten. Einzelheiten finden Sie in den nachfolgenden Abschnitten.

### Verwenden der Benutzeroberfläche

Der Arbeitsbereich **[!UICONTROL Richtlinien]** in der Benutzeroberfläche von [!DNL Experience Platform] ermöglicht die Ansicht und Verwaltung von Kern- und benutzerdefinierten Beschriftungen für Ihr Unternehmen. Im Arbeitsbereich **[!DNL Datasets]** können Sie Beschriftungen auf Datensätze und Felder anwenden. Weitere Informationen finden Sie im [Benutzerhandbuch zu Beschriftungen](user-guide.md).

### Verwenden von APIs

Der `/labels`-Endpunkt in der [Richtlinien-Service-API](https://www.adobe.io/experience-platform-apis/references/policy-service/) ermöglicht Ihnen die programmgesteuerte Verwaltung von Datennutzungsbeschriftungen einschließlich des Erstellens benutzerdefinierter Beschriftungen. Weitere Informationen finden Sie im [Beschriftungsendpunkt-Handbuch](../api/labels.md).

Die [Datensatz-Service-API](https://www.adobe.io/experience-platform-apis/references/dataset-service/) wird verwendet, um Beschriftungen für Datensätze und Felder zu verwalten. Weitere Informationen finden Sie im Handbuch zum [Verwalten von Datensatzbeschriftungen](./dataset-api.md).

## Nächste Schritte

In diesem Dokument wurden Datennutzungsbeschriftungen und ihre Rolle im Rahmen der Data Governance vorgestellt. Weitere Informationen zur Verwaltung von Beschriftungen in [!DNL Experience Platform] finden Sie in der Dokumentation, auf die an mehreren Stellen in diesem Handbuch verwiesen wird.
