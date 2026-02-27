---
title: Verwalten von Query Service-Sitzungen in Adobe Experience Platform
description: Erfahren Sie, wie Admins aktive Sitzungen des Abfrage-Service anzeigen, überwachen und beenden können, um Leerlaufkapazitäten freizugeben und zuverlässige Data Distiller-Workflows zu erhalten.
keywords: Experience Platform;Abfrage-Service;Sitzungen;Sitzungsverwaltung;Daten-Distiller;Admin
solution: Experience Platform
source-git-commit: 1d2a8ef649c4454da7cf0949192b8b1eb3696e5a
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 1%

---

# Verwalten von Query Service-Sitzungen

Verwenden Sie dieses Handbuch, um aktive Sitzungen des Abfrage-Service über die Benutzeroberfläche von Adobe Experience Platform zu verwalten. Die Sitzungsverwaltung hilft Admins, gleichzeitige Abfrage-Editor-Sitzungen in allen Sandboxes und die freie Kapazität zu überwachen, wenn Benutzende Sitzungen offen lassen.

## Für die Sitzungsverwaltung erforderliche Berechtigungen {#permissions}

>[!AVAILABILITY]
>
>Die Sitzungsverwaltung ist nur für Organisationen mit Berechtigungen für Data Distiller verfügbar.

>[!IMPORTANT]
>
>Diese Funktion ist für Administratoren gedacht. Endbenutzer, die Abfragen ausführen, können Sitzungen nicht verwalten.

Zum Anzeigen und Beenden von Sitzungen müssen Sie zu einer Organisation mit Zugriff auf Data Distiller gehören und über die **[!UICONTROL Manage Query Session]** Berechtigung verfügen. Benutzende ohne die erforderlichen Berechtigungen können auf den Abfrage-Service zugreifen, aktive Sitzungen jedoch nicht anzeigen oder verwalten.

## Aktive Sitzungen anzeigen {#view-active-sessions}

Administratoren können alle aktiven Sitzungen des Abfrage-Service in Sandboxes in Ihrer Organisation anzeigen. Wählen Sie in Experience Platform im linken Navigationsbereich die Option **[!UICONTROL Queries]** aus, um den Arbeitsbereich Abfrage-Service zu öffnen, und wählen Sie dann die Registerkarte **[!UICONTROL Admin]** aus, um auf die Sitzungsverwaltung zuzugreifen.

![Der Arbeitsbereich „Abfrage-Service“ mit ausgewählter Registerkarte „Admin“. Die Tabelle Sitzungsverwaltung wird angezeigt und listet aktive und inaktive Sitzungen in mehreren Sandboxes in Ihrer Organisation auf.](../images/ui/session-management/session-management-admin-tab.png)

Die Tabelle zur Sitzungsverwaltung wird automatisch in Echtzeit aktualisiert und listet alle Sitzungen auf, die derzeit die Kapazität für gleichzeitige Sitzungen mit Query Service beanspruchen, welche Ihrem Unternehmen zugewiesen sind. Jede Zeile stellt eine einzelne Sitzung dar, die im Abfrage-Editor geöffnet wurde.

## Sitzungsstatus und Inaktivitätsdauer {#session-status}

Die Tabelle Sitzung enthält Informationen dazu, wie Sie entscheiden können, ob eine Sitzung sicher beendet werden kann.

| Spalte | Beschreibung |
| --- | --- |
| Benutzer-ID | Die Adobe ID des Benutzers, dem die Sitzung gehört |
| Benutzername | Der mit der Adobe ID verknüpfte Name |
| Sandbox | Gibt die Sandbox an, in der die Sitzung ausgeführt wird |
| Sitzungsstatus | Zeigt an, ob die Sitzung **[!UICONTROL Active]** oder **[!UICONTROL Inactive]** ist |
| Inaktivitätsdauer | Zeigt an, wie lange die Sitzung ohne Interaktion geöffnet war |
| Verbleibende Sitzungszeit | Gibt an, wie lange die Sitzung vor dem automatischen Ablauf geöffnet bleiben kann |

### Sitzungsstatus

**[!UICONTROL Inactive]** gibt an, dass der Benutzer keine aktive Abfrage ausführt. Diese Sitzungen können beendet werden. **[!UICONTROL Active]** gibt an, dass eine Abfrage derzeit ausgeführt wird. Das **[!UICONTROL End session]**-Steuerelement ist erst verfügbar, wenn die Ausführung der Abfrage abgeschlossen ist.

### Inaktivitätsdauer und verbleibende Sitzungsdauer

Inaktivitätsdauer gibt an, wie lange eine Sitzung ohne Benutzerinteraktion geöffnet war. Die verbleibende Sitzungszeit gibt an, wie lange die Sitzung offen bleiben kann, bevor sie automatisch vom System geschlossen wird. Sitzungen laufen automatisch nach der maximal zulässigen Dauer ab (zwei Stunden ohne Aktivität). Diese Dauer ist systemdefiniert und kann nicht konfiguriert werden.

## Inaktive Sitzungen beenden {#end-idle-sessions}

Sie können inaktive Sitzungen beenden, um anderen Benutzern die Kapazität gleichzeitiger Sitzungen freizugeben. Erwägen, Sitzungen mit hoher Inaktivitätsdauer zu beenden, wenn Benutzende nicht mehr aktiv arbeiten.

Wählen Sie in der Tabelle Sitzungsverwaltung die Option **[!UICONTROL End session]** aus, um die inaktive Sitzung auszuwählen, die Sie beenden möchten.

![Tabelle „Sitzungsverwaltung“ mit hervorgehobener Option „Inaktive Sitzung“ und „Sitzung beenden“](../images/ui/session-management/end-session.png)

Ein Bestätigungsdialogfeld wird angezeigt, um eine versehentliche Beendigung zu verhindern. Wählen Sie **[!UICONTROL End session]** im Dialogfeld aus, um die Aktion zu bestätigen.

![Das Bestätigungsdialogfeld zum Beenden einer Sitzung mit einer Warnmeldung und hervorgehobener Option „Sitzung beenden“](../images/ui/session-management/end-session-confirmation-dialog.png)

Nach dem Ende der Sitzung wird die Sitzung aus der Tabelle entfernt, die Kapazität wird sofort verfügbar, und die Aktion wird für das Auditing aufgezeichnet.

>[!NOTE]
>
>Sitzungen mit dem Status **[!UICONTROL Active]** können nicht beendet werden. Diese Sicherung verhindert Unterbrechungen von laufenden Arbeitslasten.

## Sitzungsverhalten nach Beendigung {#session-behavior-after-termination}

Wenn ein Administrator eine Sitzung beendet, bleibt der Code des betroffenen Benutzers im Editor, ohne dass Arbeit verloren geht. Wenn der/die Benutzende versucht, nach der Beendigung eine Abfrage auszuführen, erkennt das System die beendete Sitzung, stellt die Verbindung automatisch wieder her und behält den Inhalt des Abfrage-Editors bei.

Dadurch wird sichergestellt, dass Benutzende keine im Editor geschriebene Arbeit verlieren und fortfahren können, sobald eine neue Sitzung eingerichtet wurde.

## Auditprotokolle für das Sitzungsmanagement {#audit-logs}

Das System protokolliert Sitzungsverwaltungsaktionen, um Sichtbarkeit und Verantwortlichkeit zu gewährleisten. Auditprotokolle zeichnen die Sitzungs-ID, den Benutzer, dessen Sitzung beendet wurde, den Administrator, der die Aktion ausgeführt hat, und den Zeitpunkt der Aktion auf.

Verwenden Sie Auditprotokolle, um den Verlauf der Sitzungsbeendigungen zu überprüfen und unerwartete Verbindungen zu untersuchen.

Weitere Informationen zum Anzeigen von Auditprotokollen finden Sie im [Handbuch zum Auditprotokoll für Query Service](../data-governance/audit-log-guide.md).

## Nächste Schritte {#next-steps}

Beachten Sie die folgenden Ressourcen, um Ihre Verwendung von Query Service und Data Distiller zu erweitern:

* [Im Benutzerhandbuch zum Abfrage-Editor erfahren Sie, wie Benutzende Abfragen erstellen und ausführen.](user-guide.md)
* [Überwachen geplanter Workloads mithilfe der Dokumentation zur Überwachung geplanter Abfragen](monitor-queries.md)

