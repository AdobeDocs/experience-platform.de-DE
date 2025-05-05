---
title: Berechtigungs-Manager für die attributbasierte Zugriffssteuerung
description: Erfahren Sie, wie Sie den Berechtigungs-Manager in Adobe Experience Platform zum Generieren von Berichten und Überprüfen von Zugriffsberechtigungen verwenden.
exl-id: 4c2b8b8e-ac4f-4c6e-a23f-66f658bb6e24
source-git-commit: 7e65e88bc49ea28d567e8204db877d22ddb8d9a6
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 9%

---

# Berechtigungs-Manager

>[!NOTE]
>
>Um auf [!UICONTROL Berechtigungs-Manager] zugreifen zu können, müssen Sie ein Produktadministrator sein. Wenn Sie keine Administratorrechte haben, wenden Sie sich an Ihren Systemadministrator, um Zugriff zu erhalten.

Verwenden Sie einfache Abfragen im [!UICONTROL Berechtigungs-Manager], um präzise Berichte zu erstellen, die Ihnen das Verständnis der Zugriffsverwaltung erleichtern und Zeit bei der Überprüfung von Zugriffsberechtigungen für viele Workflows und Granularitätsstufen sparen. Sie können [!UICONTROL Berechtigungs-Manager] verwenden, um Benutzer zu finden, die zu einer Benutzergruppe gehören und bestimmte Zugriffsberechtigungen sowie Rollen mit bestimmten Beschriftungen haben.

## Suchen nach Benutzerinnen und Benutzern innerhalb einer angegebenen Benutzergruppe {#search-users}

>[!CONTEXTUALHELP]
>id="platform_permission_manager"
>title="Berechtigungs-Manager"
>abstract="Verwenden Sie die Dropdown-Auswahl auf der Seite, um Berichte auf Zugriffsebene mit unterschiedlichen Granularitätsstufen für Benutzende und Rollen zu erhalten."
<!-- >additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-manager/permissions.html?lang=de" text="Permission manager" -->

Wählen Sie über die Dropdown-Liste das Attribut **[!UICONTROL Benutzer]** aus.

![Die Dropdown-Liste mit hervorgehobenen Benutzern.](../../images/permission-manager/users-select.png)

Wählen Sie als Nächstes die **[!UICONTROL Benutzergruppe]**, nach der Sie über die Dropdown-Liste suchen möchten.

>[!INFO]
>
>[!UICONTROL Benutzergruppe] ist kein Pflichtfeld. Für jeden Bericht kann nur eine Benutzergruppe ausgewählt werden.

![Das Dropdown-Menü „Benutzergruppe“ ist hervorgehoben.](../../images/permission-manager/user-group-select.png)

Für einen detaillierteren Bericht können Sie die Ressource mit Aktionen in einer bestimmten Sandbox angeben. Wählen Sie die **[!UICONTROL Ressource]**, **[!UICONTROL Aktionen]** und **[!UICONTROL Sandboxes]** über die Dropdown-Liste aus und klicken Sie dann auf **[!UICONTROL Ergebnisse anzeigen]**.

>[!INFO]
>
>[!UICONTROL Ressource], [!UICONTROL Aktionen] und [!UICONTROL Sandboxes] sind keine Pflichtfelder. Eine Aktion oder Sandbox kann entfernt werden, sobald sie hinzugefügt wurde, indem **neben der Auswahl, die Sie entfernen möchten,** x ausgewählt wird.

![Die Dropdown-Listen „Ressource“, „Aktionen“, „Sandboxes“ und „Ergebnisse anzeigen“ sind hervorgehoben](../../images/permission-manager/users-additional-attributes-select.png)

Eine Liste der Benutzer und ihre E-Mail-Adresse werden anhand der ausgewählten Kriterien gemeldet. Verwenden Sie das Filtermenü auf der linken Seite, um die Attribute und Ergebnisse zu aktualisieren. Um weitere Informationen zu einem bestimmten Benutzer zu erhalten, wählen Sie den Benutzernamen aus der Liste aus.

![Der generierte Bericht basierend auf den ausgewählten Attributen](../../images/permission-manager/users-report.png)

## Nach Rollen mit bestimmten Kennzeichnungen suchen {#search-roles}

Wählen Sie über die Dropdown-Liste das Attribut **[!UICONTROL Rollen]** aus.

>[!INFO]
>
>[!UICONTROL Kennzeichnungen] ist kein Pflichtfeld. Sie können mehrere Bezeichnungen auswählen, die unterhalb dieser Dropdown-Liste angezeigt werden, sobald Sie sie auswählen. Ein Label kann entfernt werden, sobald es hinzugefügt wurde, indem **&#39;x&#39; neben** Aktion ausgewählt wird.

![Die Dropdown-Liste mit hervorgehobenen Rollen.](../../images/permission-manager/roles-select.png)

Wählen Sie anschließend die **[!UICONTROL Kennzeichnungen]**, nach denen Sie mithilfe der Dropdown-Liste suchen möchten.

![Das Dropdown-Menü „Kennzeichnungen“ ist hervorgehoben.](../../images/permission-manager/roles-labels-select.png)

Für einen detaillierteren Bericht können Sie die Ressource mit Aktionen in einer bestimmten Sandbox angeben. Wählen Sie die **[!UICONTROL Ressource]**, **[!UICONTROL Aktionen]** und **[!UICONTROL Sandboxes]** über die Dropdown-Liste aus und klicken Sie dann auf **[!UICONTROL Ergebnisse anzeigen]**.

>[!INFO]
>
>[!UICONTROL Ressource], [!UICONTROL Aktionen] und [!UICONTROL Sandboxes] sind keine Pflichtfelder. Für [!UICONTROL &#x200B; Bericht kann nur &#x200B;] Ressource ausgewählt werden. Eine Aktion oder Sandbox kann entfernt werden, sobald sie hinzugefügt wurde, indem **neben der Auswahl, die Sie entfernen möchten,** x ausgewählt wird.

![Die Dropdown-Listen „Ressource“, „Aktionen“, „Sandboxes“ und „Ergebnisse anzeigen“ sind hervorgehoben](../../images/permission-manager/roles-additional-attributes-select.png)

Basierend auf den ausgewählten Kriterien wird eine Liste der Rollen angezeigt. Verwenden Sie das Filtermenü auf der linken Seite, um die Attribute und Ergebnisse zu aktualisieren. Um weitere Informationen zu einer bestimmten Rolle zu erhalten, wählen Sie die Rolle in der Liste aus.

Die folgenden Informationen werden für jede Rolle angezeigt, die Ihren Kriterien entspricht:

| Attribut | Beschreibung |
| --- | --- |
| Beschreibung | Eine kurze Beschreibung der Rolle. |
| Beschriftungen | Eine Liste von Beschriftungen, die mit der Rolle verknüpft sind. |
| Sandboxes | Eine Liste von Sandboxes, die diese Rolle enthalten. |
| Geändert um | Datum und Zeitstempel der letzten Aktualisierung der Rolle. |
| Erstellung: | Datum und Zeitstempel der Erstellung der Rolle. |
| Erstellt von | Details des Erstellers der Rolle. |

![Der generierte Bericht basierend auf den ausgewählten Attributen](../../images/permission-manager/roles-report.png)

## Nächste Schritte

Sie haben jetzt gelernt, wie Sie Berichte für Benutzer und Rollen erstellen. Weitere Informationen zur attributbasierten Zugriffssteuerung finden Sie unter &quot;[ Zugriffssteuerung - Übersicht](../overview.md).
