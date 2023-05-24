---
keywords: Experience Platform;Startseite;beliebte Themen;Datenverwaltung;Datennutzungsbeschriftungs-API;Richtlinien-Service-API;Übersicht zu Datennutzungsbeschriftungen
solution: Experience Platform
title: Datennutzungskennzeichnungen – Übersicht
description: Erfahren Sie, wie Datennutzungskennzeichnungen verwendet werden, um die Einhaltung von Data-Governance-Richtlinien in Adobe Experience Platform durchzusetzen.
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
source-git-commit: 5d34781e06c0fa8bfd2e52f73e336d92d16192f6
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 83%

---

# Datennutzungskennzeichnungen – Übersicht {#overview}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_description"
>title="Kontrollieren des Zugriff auf vertrauliche und geschützte Daten"
>abstract="<h2>Beschreibung</h2><p>Kontrollieren Sie den Zugriff auf bestimmte Datenattribute und/oder Segmente, sodass Sie flexible Workflows für die verschiedenen Profile und Teams erstellen können, die Anwendungsfälle in Experience Platform betreiben.</p>"

Mit Adobe Experience Platform können Sie Datennutzungskennzeichnungen auf Datensätze und Felder anwenden und diese entsprechend den zugehörigen [Data-Governance-Richtlinien](../policies/overview.md) und [Zugriffssteuerungsrichtlinien](../../access-control/abac/ui/policies.md) kategorisieren.

Dieses Dokument bietet eine Übersicht über Datennutzungskennzeichnungen in [!DNL Experience Platform].

## Verstehen von Datennutzungskennzeichnungen

Mit Datennutzungskennzeichnungen können Sie Datensätze anhand der für diese Daten geltenden Governance-Richtlinien kategorisieren. Beschriftungen können jederzeit angewendet werden, was eine flexible Handhabung der Daten ermöglicht. Best Practices legen nahe, Daten direkt bei ihrer Aufnahme in [!DNL Experience Platform] oder ab dem Zeitpunkt ihrer Nutzbarkeit in [!DNL Platform] mit einer Beschriftung zu versehen.

Datennutzungsbeschriftungen, die auf Datensatzebene angewendet werden, werden für alle Felder des Datensatzes übernommen. Außerdem können Beschriftungen direkt auf einzelne Felder (Spaltenüberschriften) in einem Datensatz angewendet werden, ohne dass eine Übernahme erfolgt.

[!DNL Platform] bietet mehrere standardmäßige „Kern“-Datennutzungsbeschriftungen, die eine Vielzahl von allgemeinen Einschränkungen für die Datenverwaltung abdecken. Weitere Informationen zu diesen Kennzeichnungen und zu den Governance-Richtlinien, für die sie stehen, finden Sie im Handbuch zu den [grundlegenden Datennutzungskennzeichnungen](reference.md).

Zusätzlich zu den von Adobe bereitgestellten Beschriftungen können Sie auch eigene benutzerdefinierte Beschriftungen für Ihr Unternehmen definieren. Weitere Informationen finden Sie im Abschnitt [Verwalten von Beschriftungen](#manage-labels).

## Beschriftungsvererbung für Zielgruppensegmente

Alle von [Adobe Experience Platform Segmentation Service](../../segmentation/home.md) erstellten Zielgruppensegmente übernehmen die Nutzungsbeschriftungen der zugehörigen Datensätze. Dies ermöglicht Experience Platform, bei der Aktivierung von Segmenten für Ziele eine automatische Durchsetzung der Richtlinie zu gewährleisten.

Neben der Vererbung von Beschriftungen auf Datensatzebene übernehmen Segmente standardmäßig alle Beschriftungen auf Feldebene aus den zugehörigen Datensätzen. Daher können Sie leichter identifizieren, welche Attribute bei Ihren Segmenten ausgeschlossen werden sollen, und so verhindern, dass die Segmente Beschriftungen von ausgeschlossenen Feldern übernehmen.

Weitere Informationen zur Funktionsweise der automatischen Durchsetzung in Platform finden Sie in der Übersicht über [automatische Richtliniendurchsetzung](../enforcement/auto-enforcement.md).

### Vererbung von Adobe Audience Manager-Datenexportsteuerelementen

[!DNL Experience Platform] hat die Möglichkeit, Segmente für Adobe Audience Manager freizugeben. Alle Datenexportsteuerelemente, die auf Audience Manager-Segmente angewendet wurden, werden in entsprechende Kennzeichnungen und Marketing-Aktionen übersetzt, die von [!DNL Experience Platform] Data Governance erkannt werden.

Informationen dazu, wie bestimmte Datenexportsteuerelemente den Datennutzungskennzeichnungen in [!DNL Platform] zugeordnet werden, finden Sie in der [Audience Manager-Dokumentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=de#aam-data-export-control-in-aep).

## Verwalten von Datennutzungsbeschriftungen in [!DNL Experience Platform] {#manage-labels}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_instructions"
>title="Anleitung"
>abstract="<ul><li>Kennzeichnen Sie XDM-Felder und Segmente, um die Felder und Segmente zu klassifizieren, auf die Sie den Zugriff beschränken möchten.</li><li>Kennzeichnen von Rollen: Durch Hinzufügen von Kennzeichnungen zu einer Rolle können Sie festlegen, für welche Kennzeichnungen Beschränkungen für Personen mit dieser Rolle gelten sollen.</li><li>Richtlinien erstellen: Eine Richtlinie schafft eine Beziehung zwischen den Kennzeichnungen für gekennzeichnete Objekte wie XDM-Feldern und Segmenten und den Kennzeichnungen für Rollen. Wenn die Kennzeichnungen übereinstimmen, kann entweder eine Zugriffserlaubnis oder ein eingeschränkter Zugriff definiert werden.</li></ul>"

Sie können Datennutzungsbeschriftungen mit [!DNL Experience Platform]-APIs oder der Benutzeroberfläche verwalten. Einzelheiten finden Sie in den nachfolgenden Abschnitten.

### Verwenden der Benutzeroberfläche

Der Arbeitsbereich **[!UICONTROL Richtlinien]** in der Benutzeroberfläche von [!DNL Experience Platform] ermöglicht die Ansicht und Verwaltung von Kern- und benutzerdefinierten Beschriftungen für Ihr Unternehmen. Sie können die **[!UICONTROL Schemas]** Arbeitsbereich zu [Anwenden von Bezeichnungen auf Ihre Experience-Datenmodell (XDM)-Schemas](../../xdm/tutorials/labels.md)oder lernen Sie, wie [Erstellen und Verwalten benutzerdefinierter Bezeichnungen in **[!UICONTROL Richtlinien] Benutzeroberfläche](./user-guide.md) durch Lesen des Benutzerhandbuchs zu Datennutzungsbezeichnungen.

>[!IMPORTANT]
>
>Beschriftungen können nicht mehr auf Felder auf Datensatzebene angewendet werden. Dieser Workflow wird nicht mehr für die Anwendung von Bezeichnungen auf Schemaebene unterstützt. Alle Bezeichnungen, die zuvor auf Datensatzobjektebene angewendet wurden, werden bis zum 31. Mai 2024 weiterhin über die Platform-Benutzeroberfläche unterstützt. Um sicherzustellen, dass Ihre Bezeichnungen über alle Schemas hinweg konsistent sind, müssen alle Bezeichnungen, die zuvor auf Datensatzebene an Felder angehängt wurden, von Ihnen im Laufe des kommenden Jahres auf Schemaebene migriert werden. Siehe Abschnitt zu [Migration zuvor angewendeter Bezeichnungen](../e2e.md#migrate-labels) für Anweisungen dazu.

### Verwenden von APIs

Der `/labels`-Endpunkt in der [Richtlinien-Service-API](https://www.adobe.io/experience-platform-apis/references/policy-service/) ermöglicht Ihnen die programmgesteuerte Verwaltung von Datennutzungsbeschriftungen einschließlich des Erstellens benutzerdefinierter Beschriftungen. Weitere Informationen finden Sie im [Beschriftungsendpunkt-Handbuch](../api/labels.md).

Die [Datensatz-Service-API](https://www.adobe.io/experience-platform-apis/references/dataset-service/) wird verwendet, um Beschriftungen für Datensätze und Felder zu verwalten. Weitere Informationen finden Sie im Handbuch zum [Verwalten von Datensatzbeschriftungen](./dataset-api.md).

## Nächste Schritte

In diesem Dokument wurden Datennutzungsbeschriftungen und ihre Rolle im Rahmen der Data Governance vorgestellt. Weitere Informationen zur Verwaltung von Beschriftungen in [!DNL Experience Platform] finden Sie in der Dokumentation, auf die an mehreren Stellen in diesem Handbuch verwiesen wird.
