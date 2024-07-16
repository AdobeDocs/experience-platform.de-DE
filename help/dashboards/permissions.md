---
solution: Experience Platform
title: Erhalten & Gewähren von Zugriffsberechtigungen für Experience Platform-Dashboards
type: Documentation
description: Gewähren Sie Benutzern die Möglichkeit, Experience Platform-Dashboards mithilfe von Adobe Admin Console anzuzeigen, zu bearbeiten und zu aktualisieren.
exl-id: 2e50790f-b3ab-4851-a9a5-7cb98bf98ce3
source-git-commit: fa4fc154f57243250dec9bdf9557db13ef7768e8
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 28%

---

# Zugriffsberechtigungen für Dashboards

Damit Benutzer Dashboards anzeigen, bearbeiten und aktualisieren können, müssen Sie zunächst Berechtigungen aktivieren. In Adobe Experience Platform wird die Zugriffskontrolle über den [Adobe Admin Console](https://adminconsole.adobe.com/) bereitgestellt. Benutzer werden über Produktprofile in der &quot;[!DNL Admin Console]&quot;mit Berechtigungen und Sandboxes verknüpft.

Dieses Dokument bietet eine Zusammenfassung der verfügbaren Berechtigungen für Dashboards, einschließlich der Funktionen, auf die sie Zugriff gewähren, und der Benutzerfunktionen, die sie aktivieren. Ausführliche Informationen zum Abrufen und Zuweisen von Zugriffsberechtigungen finden Sie in der [Übersicht zur Zugriffskontrolle](../access-control/home.md).

## Voraussetzungen

Zum Konfigurieren der Zugriffssteuerung für [!DNL Experience Platform] müssen Sie Administratorrechte für ein Unternehmen haben, das über eine [!DNL Experience Platform]-Produktintegration verfügt. Weitere Informationen zu [Administratorrollen](https://helpx.adobe.com/de/enterprise/using/admin-roles.html) finden Sie im Adobe Help Center-Artikel.

## Verfügbare Dashboard-Berechtigungen {#available-permissions}

Der Dienst [!DNL Dashboards] bietet drei Berechtigungen, die, wenn sie kombiniert werden, uneingeschränkten Zugriff auf die Dashboards [!UICONTROL Profile], [!UICONTROL Segmente], [!UICONTROL Ziele] und [!UICONTROL Lizenznutzung] in Adobe Experience Platform bieten. Diese Berechtigungen sind:

| Berechtigung | Beschreibung |
|---|---|
| **Standard-Dashboards verwalten** | Diese Berechtigung ist eine **globale Lese- und Schreibberechtigung**. Dadurch können Sie [benutzerdefinierte Widgets erstellen](./customize/custom-widgets.md) und [das Widget-Schema bearbeiten](./customize/edit-schema.md), indem Sie die [!UICONTROL Widget-Bibliothek] verwenden. |
| **Standard-Dashboards anzeigen** | Dies bietet die Funktion **schreibgeschützt** für die Dashboards [!UICONTROL Profile], [!UICONTROL Ziele] und [!UICONTROL Segmente] und ermöglicht den Zugriff darauf über die linke Navigation von Platform. Außerdem wird [!UICONTROL Dashboards] zur linken Navigation hinzugefügt und der Zugriff auf die Registerkarte [!UICONTROL Dashboards] Inventar und Integrationen erfolgt. |
| **Anzeigen des Dashboards zur Lizenznutzung** | Diese Berechtigung ermöglicht Benutzern, die **schreibgeschützt** haben, Zugriff auf [das Lizenzverwendungs-Dashboard](./guides/license-usage.md) in der Experience Platform-Benutzeroberfläche. |

Es gibt fünf Berechtigungen, die nicht in der Kategorie [!DNL Dashboard] enthalten sind und je nach Ihren Anforderungen möglicherweise erforderlich sind. In der folgenden Tabelle sind die Kategoriestandorte in der Admin Console aufgeführt:

>[!IMPORTANT]
>
>Sowohl die **[!DNL Manage Standard Dashboards]**- als auch die **[!DNL View Standard Dashboards]**-Berechtigungen **erfordern** die Berechtigung &quot;Ansicht&quot;oder &quot;Verwalten&quot;aus der Kategorie [!DNL Profile Management] oder [!DNL Destinations] in der Admin Console, um die entsprechenden Bereiche in der Platform-Benutzeroberfläche zu aktivieren.

| Berechtigung | Speicherort der Admin Console |
|---|---|
| [!DNL View Profiles] | [!DNL Profile Management] |
| [!DNL View Segments] | [!DNL Profile Management] |
| [!DNL View Destinations] | [!DNL Destinations] |
| [!DNL Manage Queries] | [!DNL Query Service] |
| [!DNL Manage Sandboxes] | [!DNL Sandbox Administration] |

## Zugriffssteuerungsmatrix

Die folgende Zugriffssteuerungsmatrix zeigt, welche Berechtigungen erforderlich sind und welche Funktionen sie für den Zugriff auf die verschiedenen Dashboard-Funktionen bereitstellen. Berechtigungen werden in der oberen horizontalen Zeile aufgelistet und der Platform UI-Arbeitsbereich wird entlang der linken Spalte aufgeführt.

|   | [!UICONTROL Standard-Dashboard anzeigen] ODER [!UICONTROL Standard-Dashboard verwalten] | [!UICONTROL Anzeigen von Profilen],<br/>[!UICONTROL Anzeigen von Segmenten],<br/> [!UICONTROL Anzeigen von Zielen] | [!UICONTROL Abfragen verwalten] und [!UICONTROL Sandboxes verwalten] | [!UICONTROL Anzeigen des Dashboards zur Lizenznutzung] |
|---|---|---|---|---|
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] in der linken Navigation. | K. A. | **Für jedes Dashboard ist eine Berechtigung zum Anzeigen oder Verwalten erforderlich.** | K. A. | K. A. |
| [!DNL Dashboards] in der linken Navigation. | Aktiviert | **Mindestens ein erforderlicher**. | K. A. | K. A. |
| [!DNL Dashboards] [!DNL Inventory] <br/> (die Registerkarte &quot;Durchsuchen&quot;) | Aktiviert | K. A. | K. A. | K. A. |
| [!DNL Dashboards] [!DNL Integrations] tab <br/> (zur Installation von Power BI verwendet) | Aktiviert | **Mindestens ein erforderlicher** | K. A. | K. A. |
| Schaltfläche &quot;Power BI installieren&quot;und Workflow | Aktiviert | K. A. | **ERFORDERLICH** | K. A. |
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] Dashboards.<br/>Die Möglichkeit, Widget-Schemata zu bearbeiten und neue Attribute zur Widget-Anpassung hinzuzufügen | **ERFORDERLICHES Standard-Dashboard verwalten** | **ERFORDERLICH (für jedes Dashboard)** | K. A. | K. A. |
| [!DNL License Usage Dashboard] | K. A. | K. A. | K. A. | Aktiviert |

{style="table-layout:auto"}

## Berechtigungen zu Ihrem Produktprofil hinzufügen

Verwenden Sie die oben angegebenen Informationen, um Ihrem Produktprofil die entsprechenden Berechtigungen hinzuzufügen. Vollständige Anweisungen zum Hinzufügen von Berechtigungen über die Benutzeroberfläche der Zugriffskontrolle finden Sie in der Dokumentation [.](../access-control/ui/permissions.md)

Beschreibungen der Berechtigungen finden Sie im Abschnitt [Verfügbare Berechtigungen](#available-permissions) weiter oben in diesem Dokument.

>[!NOTE]
>
>Sie müssen nicht alle Berechtigungen für alle Benutzer aktivieren. Abhängig von der Struktur Ihres Unternehmens möchten Sie möglicherweise separate Produktprofile für bestimmte Benutzer erstellen und eingeschränkten Zugriff gewähren (z. B. schreibgeschützt). Weitere Informationen zum Zuweisen von Berechtigungen für bestimmte Benutzer finden Sie in der Dokumentation zum Verwalten von Benutzern für ein Produktprofil [.](../access-control/ui/users.md)

Nachdem Sie die erforderlichen Zugriffsberechtigungen hinzugefügt haben, können Benutzer in Ihrem Unternehmen Dashboards in der Experience Platform-Benutzeroberfläche anzeigen und basierend auf den von Ihnen zugewiesenen Berechtigungen weitere Aktionen durchführen.
