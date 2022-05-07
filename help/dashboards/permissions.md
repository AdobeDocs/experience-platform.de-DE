---
solution: Experience Platform
title: Erhalten & Gewähren von Zugriffsberechtigungen für Experience Platform-Dashboards
type: Documentation
description: Gewähren Sie Benutzern die Möglichkeit, Experience Platform-Dashboards mithilfe von Adobe Admin Console anzuzeigen, zu bearbeiten und zu aktualisieren.
exl-id: 2e50790f-b3ab-4851-a9a5-7cb98bf98ce3
source-git-commit: 052e365c6127961363b7b5333cb0f4f82ab5479a
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 32%

---

# Zugriffsberechtigungen für Dashboards

Damit Benutzer Dashboards anzeigen, bearbeiten und aktualisieren können, müssen Sie zunächst Berechtigungen aktivieren. In Adobe Experience Platform wird die Zugriffskontrolle über die [Adobe Admin Console](https://adminconsole.adobe.com/). Benutzer werden über Produktprofile in der [!DNL Admin Console].

Dieses Dokument bietet eine Zusammenfassung der verfügbaren Berechtigungen für Dashboards, einschließlich der Funktionen, auf die sie Zugriff gewähren, und der Benutzerfunktionen, die sie aktivieren. Ausführliche Informationen zum Abrufen und Zuweisen von Zugriffsberechtigungen finden Sie in der [Übersicht zur Zugriffskontrolle](../access-control/home.md).

## Voraussetzungen

Zum Konfigurieren der Zugriffssteuerung für [!DNL Experience Platform] müssen Sie Administratorrechte für ein Unternehmen haben, das über eine [!DNL Experience Platform]-Produktintegration verfügt. Weitere Informationen zu [Administratorrollen](https://helpx.adobe.com/de/enterprise/using/admin-roles.html) finden Sie im Adobe Help Center-Artikel.

## Verfügbare Dashboard-Berechtigungen {#available-permissions}

Die [!DNL Dashboards] -Dienst bietet drei Berechtigungen, die, wenn sie kombiniert werden, uneingeschränkten Zugriff auf die [!UICONTROL Profile], [!UICONTROL Segmente], [!UICONTROL Ziele]und [!UICONTROL Lizenzverwendung] Dashboards in Adobe Experience Platform. Diese Berechtigungen sind:

| Berechtigung | Beschreibung |
|---|---|
| **Standard-Dashboards verwalten** | Diese Berechtigung ist eine **globale Lese- und Schreibberechtigungen**. Damit können Sie [Erstellen benutzerdefinierter Widgets](./customize/custom-widgets.md) und [Widget-Schema bearbeiten](./customize/edit-schema.md) durch [!UICONTROL Widget-Bibliothek]. |
| **Standard-Dashboards anzeigen** | Diese **schreibgeschützt** -Funktion [!UICONTROL Profile], [!UICONTROL Ziele]und [!UICONTROL Segmente] Dashboards verwenden und über die linke Navigation von Platform Zugriff auf diese zulassen. Außerdem wird [!UICONTROL Dashboards] zur linken Navigation und Zugriff auf die [!UICONTROL Dashboards] Registerkarte &quot;Inventar und Integrationen&quot;. |
| **Anzeigen des Dashboards zur Lizenznutzung** | Diese Berechtigung ermöglicht Benutzern **schreibgeschützt** Zugriff auf [das Dashboard zur Lizenznutzung](./guides/license-usage.md) in der Experience Platform-Benutzeroberfläche. |

Es gibt fünf Berechtigungen, die nicht im [!DNL Dashboard] -Kategorie, die je nach Ihren Anforderungen möglicherweise erforderlich ist. In der folgenden Tabelle sind die Kategoriestandorte in der Admin Console aufgeführt:

>[!IMPORTANT]
>
>Beide **[!DNL Manage Standard Dashboards]** und **[!DNL View Standard Dashboards]** Berechtigungen **erfordern** die Berechtigung &quot;Ansicht&quot;oder &quot;Verwalten&quot;aus der [!DNL Profile Management] oder [!DNL Destinations] in der Admin Console, um die entsprechenden Bereiche in der Platform-Benutzeroberfläche zu aktivieren.

| Berechtigung | Speicherort der Admin Console-Kategorie |
|---|---|
| [!DNL View Profiles] | [!DNL Profile Management] |
| [!DNL View Segments] | [!DNL Profile Management] |
| [!DNL View Destinations] | [!DNL Destinations] |
| [!DNL Manage Queries] | [!DNL Query Service] |
| [!DNL Manage Sandboxes] | [!DNL Sandbox Administration] |

## Zugriffssteuerungsmatrix

Die folgende Zugriffssteuerungsmatrix zeigt, welche Berechtigungen erforderlich sind und welche Funktionen sie für den Zugriff auf die verschiedenen Dashboard-Funktionen bereitstellen. Berechtigungen werden in der oberen horizontalen Zeile aufgelistet und der Platform UI-Arbeitsbereich wird entlang der linken Spalte aufgeführt.

|  | [!UICONTROL Standard-Dashboard anzeigen] ODER [!UICONTROL Standard-Dashboard verwalten] | [!UICONTROL Profile anzeigen],<br/>[!UICONTROL Segmente anzeigen],<br/> [!UICONTROL Anzeigen von Zielen] | [!UICONTROL Abfragen verwalten] &amp; [!UICONTROL Verwalten von Sandboxes] | [!UICONTROL Anzeigen des Dashboards zur Lizenznutzung] |
|---|---|---|---|---|
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] in der linken Navigation. | K. A. | **Die Berechtigung &quot;Ansicht&quot;oder &quot;Verwalten&quot;ist ERFORDERLICH.** für jedes Dashboard. | K. A. | K. A. |
| [!DNL Dashboards] in der linken Navigation. | AKTIVIERT | **Mindestens ein ERFORDERLICHER**. | K. A. | K. A. |
| [!DNL Dashboards] [!DNL Inventory] <br/>(Registerkarte &quot;Durchsuchen&quot;) | AKTIVIERT | K. A. | K. A. | K. A. |
| [!DNL Dashboards] [!DNL Integrations] tab <br/>(zur Installation von Power BI verwendet) | AKTIVIERT | **Mindestens ein ERFORDERLICHER** | K. A. | K. A. |
| Schaltfläche &quot;Power BI installieren&quot;und Workflow | AKTIVIERT | K. A. | **ERFORDERLICH** | K. A. |
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] Dashboards.<br/>Die Möglichkeit, Widget-Schemata zu bearbeiten und neue Attribute zur Widget-Anpassung hinzuzufügen | **ERFORDERLICHES Dashboard verwalten** | **ERFORDERLICH (für jedes Dashboard)** | K. A. | K. A. |
| [!DNL License Usage Dashboard] | K. A. | K. A. | K. A. | AKTIVIERT |

{style=&quot;table-layout:auto&quot;}

## Berechtigungen zu Ihrem Produktprofil hinzufügen

Verwenden Sie die oben angegebenen Informationen, um Ihrem Produktprofil die entsprechenden Berechtigungen hinzuzufügen. Vollständige Anweisungen finden Sie in der Dokumentation unter [Hinzufügen von Berechtigungen über die Benutzeroberfläche der Zugriffskontrolle](../access-control/ui/permissions.md).

Beschreibungen der Berechtigungen finden Sie im Abschnitt [Verfügbare Berechtigungen](#available-permissions) weiter oben in diesem Dokument.

>[!NOTE]
>
>Sie müssen nicht alle Berechtigungen für alle Benutzer aktivieren. Abhängig von der Struktur Ihres Unternehmens möchten Sie möglicherweise separate Produktprofile für bestimmte Benutzer erstellen und eingeschränkten Zugriff gewähren (z. B. schreibgeschützt). Weitere Informationen finden Sie in der Dokumentation zum Verwalten von Benutzern für ein Produktprofil . [Zuweisen von Berechtigungen für bestimmte Benutzer](../access-control/ui/users.md).

Nachdem Sie die erforderlichen Zugriffsberechtigungen hinzugefügt haben, können Benutzer in Ihrem Unternehmen Dashboards in der Experience Platform-Benutzeroberfläche anzeigen und andere Aktionen ausführen, die auf den von Ihnen zugewiesenen Berechtigungen basieren.
