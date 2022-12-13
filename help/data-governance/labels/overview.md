---
keywords: Experience Platform;Startseite;beliebte Themen;Datenverwaltung;Datennutzungsbeschriftungs-API;Richtlinien-Service-API;Übersicht zu Datennutzungsbeschriftungen
solution: Experience Platform
title: Datennutzungsbeschriftungen – Übersicht
topic-legacy: labels
description: Erfahren Sie, wie Datennutzungsbezeichnungen verwendet werden, um die Einhaltung von Data Governance in Adobe Experience Platform zu erzwingen.
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
source-git-commit: 7e4c2ef8089276829604c9d8a8dd20a122b18c7a
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 67%

---

# Datennutzungsbeschriftungen – Übersicht

Mit Adobe Experience Platform können Sie Datennutzungsbezeichnungen auf Datensätze und Felder anwenden und sie entsprechend den jeweiligen [Data Governance-Richtlinien](../policies/overview.md) und [Zugriffskontrollrichtlinien](../../access-control/abac/ui/policies.md).

Dieses Dokument bietet eine Übersicht über Datennutzungsbeschriftungen in [!DNL Experience Platform].

## Verstehen von Datennutzungsbeschriftungen

Mit Datennutzungsbezeichnungen können Sie Datensätze und Felder entsprechend den für diese Daten geltenden Governance-Richtlinien kategorisieren. Beschriftungen können jederzeit angewendet werden, was eine flexible Handhabung der Daten ermöglicht. Best Practices legen nahe, Daten direkt bei ihrer Aufnahme in [!DNL Experience Platform] oder ab dem Zeitpunkt ihrer Nutzbarkeit in [!DNL Platform] mit einer Beschriftung zu versehen.

Datennutzungsbeschriftungen, die auf Datensatzebene angewendet werden, werden für alle Felder des Datensatzes übernommen. Außerdem können Beschriftungen direkt auf einzelne Felder (Spaltenüberschriften) in einem Datensatz angewendet werden, ohne dass eine Übernahme erfolgt.

[!DNL Platform] bietet mehrere standardmäßige „Kern“-Datennutzungsbeschriftungen, die eine Vielzahl von allgemeinen Einschränkungen für die Datenverwaltung abdecken. Weitere Informationen zu diesen Bezeichnungen und den Governance-Richtlinien, die sie darstellen, finden Sie im Handbuch unter [Kerndatenverwendungsbezeichnungen](reference.md).

Zusätzlich zu den von Adobe bereitgestellten Beschriftungen können Sie auch eigene benutzerdefinierte Beschriftungen für Ihr Unternehmen definieren. Weitere Informationen finden Sie im Abschnitt [Verwalten von Beschriftungen](#manage-labels).

## Beschriftungsvererbung für Zielgruppensegmente

Alle von [Adobe Experience Platform Segmentation Service](../../segmentation/home.md) erstellten Zielgruppensegmente übernehmen die Nutzungsbeschriftungen der zugehörigen Datensätze. Dadurch kann Experience Platform bei der Aktivierung von Segmenten für Ziele eine automatische Richtliniendurchsetzung bereitstellen.

Neben der Vererbung von Beschriftungen auf Datensatzebene übernehmen Segmente standardmäßig alle Beschriftungen auf Feldebene aus den zugehörigen Datensätzen. Daher können Sie leichter identifizieren, welche Attribute bei Ihren Segmenten ausgeschlossen werden sollen, und so verhindern, dass die Segmente Beschriftungen von ausgeschlossenen Feldern übernehmen.

Weitere Informationen zur Funktionsweise der automatischen Durchsetzung in Platform finden Sie in der Übersicht über [automatische Richtliniendurchsetzung](../enforcement/auto-enforcement.md).

### Vererbung von Adobe Audience Manager-Datenexportsteuerelementen

[!DNL Experience Platform] hat die Möglichkeit, Segmente für Adobe Audience Manager freizugeben. Alle Datenexportsteuerelemente, die auf Audience Manager-Segmente angewendet wurden, werden in entsprechende Kennzeichnungen und Marketing-Aktionen übersetzt, die von [!DNL Experience Platform] Data Governance erkannt werden.

Informationen dazu, wie bestimmte Datenexportsteuerelemente den Datennutzungskennzeichnungen in [!DNL Platform] zugeordnet werden, finden Sie in der [Audience Manager-Dokumentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=de#aam-data-export-control-in-aep).

## Verwalten von Datennutzungsbeschriftungen in [!DNL Experience Platform] {#manage-labels}

Sie können Datennutzungsbeschriftungen mit [!DNL Experience Platform]-APIs oder der Benutzeroberfläche verwalten. Einzelheiten finden Sie in den nachfolgenden Abschnitten.

### Verwenden der Benutzeroberfläche

Der Arbeitsbereich **[!UICONTROL Richtlinien]** in der Benutzeroberfläche von [!DNL Experience Platform] ermöglicht die Ansicht und Verwaltung von Kern- und benutzerdefinierten Beschriftungen für Ihr Unternehmen. Sie können die **[!UICONTROL Schemas]** Arbeitsbereich zu [Anwenden von Bezeichnungen auf Ihre Experience-Datenmodell (XDM)-Schemas](../../xdm/tutorials/labels.md)oder Sie können die **[!DNL Datasets]** Arbeitsbereich zu [Anwenden von Bezeichnungen auf Datensätze](./user-guide.md) anstatt.

>[!NOTE]
>
>Das Anwenden von Bezeichnungen auf Datensatzebene wird nur für Data Governance-Anwendungsfälle unterstützt. Wenn Sie Zugriffsrichtlinien für die Daten erstellen möchten, müssen Sie Beschriftungen auf das Schema anwenden, auf dem der Datensatz basiert. Siehe Übersicht unter [attributbasierte Zugriffssteuerung](../../access-control/abac/overview.md) für weitere Informationen.

### Verwenden von APIs

Der `/labels`-Endpunkt in der [Richtlinien-Service-API](https://www.adobe.io/experience-platform-apis/references/policy-service/) ermöglicht Ihnen die programmgesteuerte Verwaltung von Datennutzungsbeschriftungen einschließlich des Erstellens benutzerdefinierter Beschriftungen. Weitere Informationen finden Sie im [Beschriftungsendpunkt-Handbuch](../api/labels.md).

Die [Datensatz-Service-API](https://www.adobe.io/experience-platform-apis/references/dataset-service/) wird verwendet, um Beschriftungen für Datensätze und Felder zu verwalten. Weitere Informationen finden Sie im Handbuch zum [Verwalten von Datensatzbeschriftungen](./dataset-api.md).

>[!NOTE]
>
>Das Anwenden von Bezeichnungen auf Datensatzebene wird nur für Data Governance-Anwendungsfälle unterstützt. Wenn Sie Zugriffsrichtlinien für die Daten erstellen möchten, müssen Sie [Anwenden von Bezeichnungen auf das Schema](../../xdm/tutorials/labels.md) , auf dem der Datensatz basiert. Siehe Übersicht unter [attributbasierte Zugriffssteuerung](../../access-control/abac/overview.md) für weitere Informationen.

## Nächste Schritte

In diesem Dokument wurden Datennutzungsbeschriftungen und ihre Rolle im Rahmen der Data Governance vorgestellt. Weitere Informationen zur Verwaltung von Beschriftungen in [!DNL Experience Platform] finden Sie in der Dokumentation, auf die an mehreren Stellen in diesem Handbuch verwiesen wird.
