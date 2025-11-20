---
keywords: Experience Platform;Startseite;beliebte Themen;Data Governance;Datennutzungsbeschriftungs-API;Richtlinien-Service-API;Übersicht zu Datennutzungsbeschriftungen
solution: Experience Platform
title: Datennutzungs-Labels – Übersicht
description: Erfahren Sie, wie Datennutzungs-Labels verwendet werden, um die Einhaltung von Data-Governance-Richtlinien in Adobe Experience Platform durchzusetzen.
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
source-git-commit: 916eb01ea7878366620b859c1d6a667a88b850c9
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 88%

---

# Datennutzungs-Labels – Übersicht {#overview}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_description"
>title="Kontrollieren des Zugriff auf vertrauliche und geschützte Daten"
>abstract="<h2>Beschreibung</h2><p>Kontrollieren Sie den Zugriff auf bestimmte Datenattribute und/oder Segmente, sodass Sie flexible Workflows für die verschiedenen Profile und Teams erstellen können, die Anwendungsfälle in Experience Platform betreiben.</p>"

Mit Adobe Experience Platform können Sie Datennutzungs-Labels auf Datensätze und Felder anwenden und diese entsprechend den zugehörigen [Data-Governance-Richtlinien](../policies/overview.md) und [Zugriffssteuerungsrichtlinien](../../access-control/abac/ui/policies.md) kategorisieren.

Dieses Dokument bietet eine Übersicht über Datennutzungs-Labels in [!DNL Experience Platform].

## Verstehen von Datennutzungs-Labels

Mit Datennutzungs-Labels können Sie Datensätze anhand der für diese Daten geltenden Governance-Richtlinien kategorisieren. Labels können jederzeit angewendet werden, was eine flexible Handhabung der Daten ermöglicht. Best Practices legen nahe, Daten direkt bei ihrer Aufnahme in [!DNL Experience Platform] oder ab dem Zeitpunkt ihrer Nutzbarkeit in [!DNL Experience Platform] mit einer Beschriftung zu versehen.

Datennutzungs-Labels, die auf Datensatzebene angewendet werden, werden für alle Felder des Datensatzes übernommen. Außerdem können Labels direkt auf einzelne Felder (Spaltenüberschriften) in einem Datensatz angewendet werden, ohne dass eine Übernahme erfolgt.

[!DNL Experience Platform] bietet mehrere standardmäßige „Kern“-Datennutzungs-Labels, die eine Vielzahl von allgemeinen Einschränkungen für die Data Governance abdecken. Weitere Informationen zu diesen Kennzeichnungen und zu den Governance-Richtlinien, für die sie stehen, finden Sie im Handbuch zu den [grundlegenden Datennutzungskennzeichnungen](reference.md).

Zusätzlich zu den von Adobe bereitgestellten Labels können Sie auch eigene benutzerdefinierte Labels für Ihr Unternehmen definieren. Weitere Informationen finden Sie im Abschnitt [Verwalten von Labels](#manage-labels).

## Label-Vererbung für Zielgruppensegmente

Alle von [Adobe Experience Platform Segmentation Service](../../segmentation/home.md) erstellten Zielgruppensegmente übernehmen die Nutzungs-Labels der zugehörigen Datensätze. Dies ermöglicht Experience Platform, bei der Aktivierung von Segmenten für Ziele eine automatische Durchsetzung der Richtlinie zu gewährleisten.

Neben der Vererbung von Labels auf Datensatzebene übernehmen Segmente standardmäßig alle Labels auf Feldebene aus den zugehörigen Datensätzen. Daher können Sie leichter identifizieren, welche Attribute bei Ihren Segmenten ausgeschlossen werden sollen, und so verhindern, dass die Segmente Labels von ausgeschlossenen Feldern übernehmen.

Weitere Informationen zur Funktionsweise der automatischen Durchsetzung in Experience Platform finden Sie in der Übersicht über [automatische Richtliniendurchsetzung](../enforcement/auto-enforcement.md).

### Vererbung von Adobe Audience Manager-Datenexportsteuerelementen

[!DNL Experience Platform] hat die Möglichkeit, Segmente für Adobe Audience Manager freizugeben. Alle Datenexportsteuerelemente, die auf Audience Manager-Segmente angewendet wurden, werden in entsprechende Labels und Marketing-Aktionen übersetzt, die von [!DNL Experience Platform] Data Governance erkannt werden.

Informationen dazu, wie bestimmte Datenexportsteuerelemente den Datennutzungs-Labels in [!DNL Experience Platform] zugeordnet werden, finden Sie in der [Audience Manager-Dokumentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=de#aam-data-export-control-in-aep).

## Verwalten von Datennutzungs-Labels in [!DNL Experience Platform] {#manage-labels}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_instructions"
>title="Anleitung"
>abstract="<ul><li>Kennzeichnen Sie XDM-Felder und Segmente, um die Felder und Segmente zu klassifizieren, auf die Sie den Zugriff beschränken möchten.</li><li>Kennzeichnen von Rollen: Durch Hinzufügen von Kennzeichnungen zu einer Rolle können Sie festlegen, für welche Kennzeichnungen Beschränkungen für Personen mit dieser Rolle gelten sollen.</li><li>Richtlinien erstellen: Eine Richtlinie schafft eine Beziehung zwischen den Kennzeichnungen für gekennzeichnete Objekte wie XDM-Feldern und Segmenten und den Kennzeichnungen für Rollen. Wenn die Labels übereinstimmen, kann entweder eine Zugriffserlaubnis oder ein eingeschränkter Zugriff definiert werden.</li></ul>"

Sie können Datennutzungs-Labels mit [!DNL Experience Platform]-APIs oder der Benutzeroberfläche verwalten. Einzelheiten finden Sie in den nachfolgenden Abschnitten.

### Verwenden der Benutzeroberfläche

Der **[!UICONTROL Policies]** Arbeitsbereich in der [!DNL Experience Platform]-Benutzeroberfläche ermöglicht die Ansicht und Verwaltung von Kern- und benutzerdefinierten Beschriftungen für Ihr Unternehmen. Sie können den **[!UICONTROL Schemas]**-Arbeitsbereich verwenden, um [Kennzeichnungen auf Ihre Experience-Datenmodell (XDM)-Schemata anzuwenden](../../xdm/tutorials/labels.md) oder zu erfahren, wie Sie [benutzerdefinierte Kennzeichnungen in der **[!UICONTROL Policies]**-Benutzeroberfläche erstellen und verwalten](./user-guide.md) indem Sie stattdessen das Benutzerhandbuch zu Datennutzungskennzeichnungen lesen.

>[!IMPORTANT]
>
>Labels können auf Datensatzebene nicht mehr auf Felder angewendet werden. Dieser Workflow wurde zugunsten von Labels auf Schemaebene aufgegeben. Alle Kennzeichnungen, die zuvor auf der Datensatzobjektebene angewendet wurden, werden bis zum 31. Mai 2024 weiterhin über die Experience Platform-Benutzeroberfläche unterstützt. Damit Ihre Labels schemaübergreifend konsistent sind, müssen alle Labels, die zuvor auf Felder auf Datensatzebene angewendet wurden, von Ihnen im Laufe des kommenden Jahres auf Schemaebene migriert werden. Anweisungen hierzu finden Sie im Abschnitt zum [Migrieren zuvor angewendeter Labels](../e2e.md#migrate-labels).

### Verwenden von APIs

Der `/labels`-Endpunkt in der [Richtlinien-Service-API](https://www.adobe.io/experience-platform-apis/references/policy-service/) ermöglicht Ihnen die programmgesteuerte Verwaltung von Datennutzungs-Labels einschließlich des Erstellens benutzerdefinierter Labels. Weitere Informationen finden Sie im [Label-Endpunkt-Handbuch](../api/labels.md).

Die [Datensatz-Service-API](https://www.adobe.io/experience-platform-apis/references/dataset-service/) wird verwendet, um Labels für Datensätze und Felder zu verwalten. Weitere Informationen finden Sie im Handbuch zum [Verwalten von Datensatz-Labels](./dataset-api.md).

## Nächste Schritte

In diesem Dokument wurden Datennutzungs-Labels und ihre Rolle im Rahmen der Data Governance vorgestellt. Weitere Informationen zur Verwaltung von Labels in [!DNL Experience Platform] finden Sie in der Dokumentation, auf die an mehreren Stellen in diesem Handbuch verwiesen wird.
