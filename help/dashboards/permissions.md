---
solution: Experience Platform
title: Erhalten & Gewähren von Zugriffsberechtigungen für Experience Platform-Dashboards
type: Documentation
description: Gewähren Sie Benutzern die Möglichkeit, Experience Platform-Dashboards mithilfe von Adobe Admin Console anzuzeigen, zu bearbeiten und zu aktualisieren.
exl-id: 2e50790f-b3ab-4851-a9a5-7cb98bf98ce3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 28%

---

# Zugriffsberechtigungen für Dashboards

Damit Benutzer Dashboards anzeigen, bearbeiten und aktualisieren können, müssen Sie zunächst Berechtigungen aktivieren. In Adobe Experience Platform wird die Zugriffssteuerung über die [Adobe Admin Console](https://adminconsole.adobe.com/) bereitgestellt. Benutzende werden über Produktprofile in der [!DNL Admin Console] mit Berechtigungen und Sandboxes verknüpft.

Dieses Dokument bietet eine Zusammenfassung der verfügbaren Berechtigungen für Dashboards, einschließlich der Funktionen, auf die sie Zugriff gewähren, und der Benutzerfunktionen, die sie aktivieren. Ausführliche Informationen zum Abrufen und Zuweisen von Zugriffsberechtigungen finden Sie in der [Übersicht zur Zugriffskontrolle](../access-control/home.md).

## Voraussetzungen

Zum Konfigurieren der Zugriffssteuerung für [!DNL Experience Platform] müssen Sie Administratorrechte für ein Unternehmen haben, das über eine [!DNL Experience Platform]-Produktintegration verfügt. Weitere Informationen zu [Administratorrollen](https://helpx.adobe.com/de/enterprise/using/admin-roles.html) finden Sie im Adobe Help Center-Artikel.

## Verfügbare Dashboard-Berechtigungen {#available-permissions}

Der [!DNL Dashboards]-Service bietet drei Berechtigungen, die kombiniert vollen Zugriff auf die Dashboards [!UICONTROL Profile], [!UICONTROL Segmente], [!UICONTROL Ziele] und [!UICONTROL Lizenznutzung] in Adobe Experience Platform bieten. Diese Berechtigungen sind:

| Berechtigung | Beschreibung |
|---|---|
| **Standard-Dashboards verwalten** | Diese Berechtigung ist eine **globale Lese- und Schreibberechtigung**. Damit können Sie [benutzerdefinierte Widgets erstellen](./customize/custom-widgets.md) und [Widget-Schema bearbeiten](./customize/edit-schema.md) über die [!UICONTROL Widget-Bibliothek]. |
| **Standard-Dashboards anzeigen** | Dies bietet **schreibgeschützte** Funktionen für die [!UICONTROL Profile], [!UICONTROL Ziele] und [!UICONTROL Segmente] Dashboards und ermöglicht den Zugriff darauf über die linke Navigationsleiste von Experience Platform. Außerdem werden [!UICONTROL Dashboards] zur linken Navigation und der Zugriff auf die Registerkarte [!UICONTROL Dashboards] Inventar und Integrationen hinzugefügt. |
| **Anzeigen des Dashboards zur Lizenznutzung** | Diese Berechtigung ermöglicht Benutzenden **schreibgeschützten** Zugriff auf [das Lizenznutzungs-Dashboard](./guides/license-usage.md) in der Experience Platform-Benutzeroberfläche. |

Es gibt fünf Berechtigungen, die nicht in der Kategorie [!DNL Dashboard] enthalten sind und die je nach Bedarf erforderlich sein können. In der folgenden Tabelle sind die Positionen ihrer Kategorien in der Admin Console aufgeführt:

>[!IMPORTANT]
>
>Sowohl die **[!DNL Manage Standard Dashboards]**- als auch die **[!DNL View Standard Dashboards]** Berechtigungen **erfordern** eine Berechtigung zum Anzeigen oder Verwalten“ in der Kategorie [!DNL Profile Management] oder [!DNL Destinations] in der Admin Console, um die entsprechenden Abschnitte in der Experience Platform-Benutzeroberfläche zu aktivieren.

| Berechtigung | Speicherort der Admin Console-Kategorie |
|---|---|
| [!DNL View Profiles] | [!DNL Profile Management] |
| [!DNL View Segments] | [!DNL Profile Management] |
| [!DNL View Destinations] | [!DNL Destinations] |
| [!DNL Manage Queries] | [!DNL Query Service] |
| [!DNL Manage Sandboxes] | [!DNL Sandbox Administration] |

## Matrix zur Zugriffssteuerung

Die folgende Zugriffssteuerungsmatrix bietet eine Aufschlüsselung darüber, welche Berechtigungen erforderlich sind und welche Funktionen sie in Bezug auf den Zugriff auf die verschiedenen Dashboard-Funktionen bereitstellen. Berechtigungen werden in der oberen horizontalen Zeile aufgeführt und der Arbeitsbereich der Experience Platform-Benutzeroberfläche wird in der linken Spalte aufgeführt.

|   | [!UICONTROL Standard-Dashboard anzeigen] ODER [!UICONTROL Standard-Dashboard verwalten] | [!UICONTROL Profile anzeigen],<br/>[!UICONTROL Segmente anzeigen],<br/> [!UICONTROL Anzeigen von Zielen] | [!UICONTROL Verwalten von Abfragen] und [!UICONTROL Verwalten von Sandboxes] | [!UICONTROL Anzeigen des Dashboards zur Lizenznutzung] |
|---|---|---|---|---|
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] im linken Navigationsbereich. | K. A. | **Berechtigung „Anzeigen“ oder „Verwalten“ ist ERFORDERLICH** für jedes entsprechende Dashboard. | K. A. | K. A. |
| [!DNL Dashboards] in der linken Navigationsleiste. | AKTIVIERT | **Mindestens eine erforderlich**. | K. A. | K. A. |
| [!DNL Dashboards] [!DNL Inventory] <br/> (Registerkarte Durchsuchen ) | AKTIVIERT | K. A. | K. A. | K. A. |
| [!DNL Dashboards] [!DNL Integrations] Registerkarte <br/> (zur Installation von Power BI verwendet) | AKTIVIERT | **Mindestens ein erforderlich** | K. A. | K. A. |
| Schaltfläche &quot;Power BI installieren“ und Workflow | AKTIVIERT | K. A. | **ERFORDERLICH** | K. A. |
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] Dashboards.<br/>Die Möglichkeit, Widget-Schemata zu bearbeiten und neue Attribute für die Widget-Anpassung hinzuzufügen | **manage-standard-dashboard REQUIRED** | **ERFORDERLICH (für jedes entsprechende Dashboard)** | K. A. | K. A. |
| [!DNL License Usage Dashboard] | K. A. | K. A. | K. A. | AKTIVIERT |

{style="table-layout:auto"}

## Hinzufügen von Berechtigungen zu Ihrem Produktprofil

Verwenden Sie die oben bereitgestellten Informationen, um Ihrem Produktprofil die entsprechenden Berechtigungen hinzuzufügen. In der Dokumentation finden Sie vollständige Anweisungen [&#x200B; „Hinzufügen von Berechtigungen über die Benutzeroberfläche der Zugriffssteuerung](../access-control/ui/permissions.md).

Beschreibungen der Berechtigungen finden Sie im Abschnitt [Verfügbare Berechtigungen](#available-permissions) weiter oben in diesem Dokument.

>[!NOTE]
>
>Sie müssen nicht alle Berechtigungen für alle Benutzer aktivieren. Je nach Struktur Ihres Unternehmens möchten Sie möglicherweise separate Produktprofile für bestimmte Benutzer erstellen und eingeschränkten Zugriff gewähren (z. B. schreibgeschützt). Informationen zum Zuweisen von Berechtigungen für bestimmte Benutzer finden Sie in der Dokumentation [&#x200B; Verwalten von Benutzern für ein Produktprofil &#x200B;](../access-control/ui/users.md).

Nachdem Sie die erforderlichen Zugriffsberechtigungen hinzugefügt haben, können Benutzende in Ihrem Unternehmen Dashboards in der Experience Platform-Benutzeroberfläche anzeigen und andere Aktionen ausführen, die auf den von Ihnen zugewiesenen Berechtigungen basieren.
