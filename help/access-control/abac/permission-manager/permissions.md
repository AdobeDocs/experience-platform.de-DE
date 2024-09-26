---
title: Berechtigungsmanager für attributbasierte Zugriffssteuerung
description: Erfahren Sie, wie Sie mit dem Berechtigungs-Manager in Adobe Experience Platform Berichte erstellen und Zugriffsberechtigungen überprüfen können.
exl-id: 4c2b8b8e-ac4f-4c6e-a23f-66f658bb6e24
source-git-commit: 7e65e88bc49ea28d567e8204db877d22ddb8d9a6
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 9%

---

# Berechtigungs-Manager

>[!NOTE]
>
>Um auf den [!UICONTROL Berechtigungs-Manager] zugreifen zu können, müssen Sie Produktadministrator sein. Wenn Sie keine Administratorrechte haben, wenden Sie sich an Ihren Systemadministrator, um Zugriff zu erhalten.

Verwenden Sie einfache Abfragen im [!UICONTROL Berechtigungs-Manager], um knappe Berichte zu erstellen, die Ihnen helfen, die Zugriffsverwaltung zu verstehen und Zeit zu sparen, indem Sie Zugriffsberechtigungen für viele Workflows und Granularitätsstufen überprüfen. Sie können [!UICONTROL Berechtigungs-Manager] verwenden, um Benutzer zu finden, die zu einer Benutzergruppe gehören und über bestimmte Zugriffsberechtigungen verfügen, sowie Rollen mit bestimmten Bezeichnungen.

## Suchen nach Benutzerinnen und Benutzern innerhalb einer angegebenen Benutzergruppe {#search-users}

>[!CONTEXTUALHELP]
>id="platform_permission_manager"
>title="Berechtigungs-Manager"
>abstract="Verwenden Sie die Dropdown-Auswahl auf der Seite, um Berichte auf Zugriffsebene mit unterschiedlichen Granularitätsstufen für Benutzende und Rollen zu erhalten."
<!-- >additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-manager/permissions.html" text="Permission manager" -->

Wählen Sie über die Dropdown-Liste das Attribut **[!UICONTROL Benutzer]** aus.

![Das Dropdown-Menü &quot;Attribut&quot;zur Hervorhebung von Benutzern.](../../images/permission-manager/users-select.png)

Wählen Sie als Nächstes die **[!UICONTROL Benutzergruppe]** aus, nach der Sie über die Dropdown-Liste suchen möchten.

>[!INFO]
>
>[!UICONTROL Benutzergruppe] ist kein Pflichtfeld. Sie können für jeden Bericht nur eine Benutzergruppe auswählen.

![Die Dropdown-Liste Benutzergruppe wurde hervorgehoben.](../../images/permission-manager/user-group-select.png)

Für einen detaillierteren Bericht können Sie die Ressource mit Aktionen in einer bestimmten Sandbox angeben. Wählen Sie mithilfe der Dropdown-Liste die Optionen **[!UICONTROL Ressource]**, **[!UICONTROL Aktionen]** und **[!UICONTROL Sandboxes]** aus und wählen Sie dann **[!UICONTROL Ergebnisse anzeigen]** aus.

>[!INFO]
>
>[!UICONTROL Resource], [!UICONTROL Aktionen] und [!UICONTROL Sandboxes] sind keine Pflichtfelder. Eine Aktion oder Sandbox kann nach dem Hinzufügen entfernt werden, indem Sie die **&#39;x&#39;** neben der Auswahl auswählen, die Sie entfernen möchten.

![Die Dropdown-Listen Ressource, Aktionen, Sandboxes und Ergebnisse anzeigen hervorgehoben](../../images/permission-manager/users-additional-attributes-select.png)

Eine Liste der Benutzer und ihre E-Mail-Adresse werden anhand der ausgewählten Kriterien gemeldet. Verwenden Sie das Filtermenü links, um die Attribute und Ergebnisse zu aktualisieren. Wählen Sie für weitere Informationen zu einem bestimmten Benutzer den Benutzernamen aus der Liste aus.

![Der generierte Bericht basierend auf den ausgewählten Attributen hervorgehoben](../../images/permission-manager/users-report.png)

## Suchen nach Rollen mit bestimmten Beschriftungen {#search-roles}

Wählen Sie über die Dropdown-Liste das Attribut **[!UICONTROL Roles]** aus.

>[!INFO]
>
>[!UICONTROL Beschriftungen] ist kein Pflichtfeld. Sie können mehrere Beschriftungen auswählen, die nach Auswahl unter dieser Dropdown-Liste aufgeführt werden. Eine Beschriftung kann nach dem Hinzufügen entfernt werden, indem Sie die **&#39;x&#39;** neben der Aktion auswählen.

![ Das Dropdown-Menü zur Hervorhebung von Rollen.](../../images/permission-manager/roles-select.png)

Wählen Sie als Nächstes die **[!UICONTROL Beschriftungen]** aus, nach denen Sie über die Dropdown-Liste suchen möchten.

![Das Dropdown-Menü &quot;Bezeichnungen&quot;wurde hervorgehoben.](../../images/permission-manager/roles-labels-select.png)

Für einen detaillierteren Bericht können Sie die Ressource mit Aktionen in einer bestimmten Sandbox angeben. Wählen Sie mithilfe der Dropdown-Liste die Optionen **[!UICONTROL Ressource]**, **[!UICONTROL Aktionen]** und **[!UICONTROL Sandboxes]** aus und wählen Sie dann **[!UICONTROL Ergebnisse anzeigen]** aus.

>[!INFO]
>
>[!UICONTROL Resource], [!UICONTROL Aktionen] und [!UICONTROL Sandboxes] sind keine Pflichtfelder. Für jeden Bericht kann nur eine [!UICONTROL Ressource] ausgewählt werden. Eine Aktion oder Sandbox kann nach dem Hinzufügen entfernt werden, indem Sie die **&#39;x&#39;** neben der Auswahl auswählen, die Sie entfernen möchten.

![Die Dropdown-Listen Ressource, Aktionen, Sandboxes und Ergebnisse anzeigen hervorgehoben](../../images/permission-manager/roles-additional-attributes-select.png)

Basierend auf den ausgewählten Kriterien wird eine Liste der Rollen angezeigt. Verwenden Sie das Filtermenü links, um die Attribute und Ergebnisse zu aktualisieren. Um weitere Informationen zu einer bestimmten Rolle zu erhalten, wählen Sie die Rolle aus der Liste aus.

Die folgenden Informationen werden für jede Rolle angezeigt, die Ihren Kriterien entspricht:

| Attribut | Beschreibung |
| --- | --- |
| Beschreibung | Eine kurze Beschreibung der Rolle. |
| Beschriftungen | Eine Liste der mit der Rolle verknüpften Bezeichnungen. |
| Sandboxes | Eine Liste der Sanboxes, die diese Rolle enthalten. |
| Geändert am | Datum und Zeitstempel der letzten Aktualisierung der Rolle. |
| Erstellung: | Datum und Zeitstempel der Erstellung der Rolle. |
| Erstellt von | Details zum Ersteller der Rolle. |

![Der generierte Bericht basierend auf den ausgewählten Attributen hervorgehoben](../../images/permission-manager/roles-report.png)

## Nächste Schritte

Jetzt haben Sie gelernt, wie Sie Berichte für Benutzer und Rollen erstellen. Weitere Informationen zur attributbasierten Zugriffskontrolle finden Sie in der [Übersicht über die attributbasierte Zugriffssteuerung](../overview.md).
