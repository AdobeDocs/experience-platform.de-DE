---
title: Übersicht über Auditprotokolle
description: Erfahren Sie, wie Sie mithilfe von Auditprotokollen sehen können, wer welche Aktionen in Adobe Experience Platform durchgeführt hat.
exl-id: 00baf615-5b71-4e0a-b82a-ca0ce8566e7f
source-git-commit: df269a30251cb17e337ec25787d6a1eed41e9c0b
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 5%

---

# Auditprotokolle (Beta)

>[!IMPORTANT]
>
>Die Funktion für Prüfprotokolle in Adobe Experience Platform befindet sich derzeit in der Beta-Phase. Die in dieser Dokumentation beschriebene Funktionalität kann sich ändern.

Um die Transparenz und Sichtbarkeit der im System durchgeführten Aktivitäten zu erhöhen, ermöglicht es Ihnen Adobe Experience Platform, die Benutzeraktivität für verschiedene Dienste und Funktionen in Form von &quot;Auditprotokollen&quot;zu überprüfen. Diese Protokolle bilden ein Audit-Protokoll, das Ihnen bei der Fehlerbehebung in Platform helfen und Ihrem Unternehmen helfen kann, die Richtlinien der Unternehmensdatenverwaltung und die gesetzlichen Anforderungen effektiv zu erfüllen.

Grundsätzlich gibt ein Auditprotokoll **Wer** **was** und **wann** ausgeführt hat. Jede in einem Protokoll aufgezeichnete Aktion enthält Metadaten, die den Aktionstyp, das Datum und die Uhrzeit, die E-Mail-ID des Benutzers, der die Aktion ausgeführt hat, und zusätzliche Attribute für den Aktionstyp angeben.

In diesem Dokument werden Auditprotokolle in Platform behandelt, einschließlich der Anzeige und Verwaltung in der Benutzeroberfläche oder API.

## Von Prüfprotokollen erfasste Ereignistypen

In der folgenden Tabelle sind die Aktionen aufgeführt, für die Ressourcen in Auditprotokollen aufgezeichnet werden:

| Ressource | Aktionen |
| --- | --- |
| [Sandbox](../../../sandboxes/home.md) | <ul><li>Erstellung</li><li>Update</li><li>Zurücksetzen</li><li>Löschen</li></ul> |
| [Datensatz](../../../catalog/datasets/overview.md) | <ul><li>Erstellung</li><li>Aktualisieren</li><li>Löschen</li><li>Aktivieren für [Echtzeit-Kundenprofil](../../../profile/home.md)</li></ul> |
| [Schema](../../../xdm/schema/composition.md) | <ul><li>Erstellung</li><li>Aktualisieren</li><li>Löschen</li></ul> |
| [Feldergruppe](../../../xdm/schema/composition.md#field-group) | <ul><li>Erstellung</li><li>Aktualisieren</li><li>Löschen</li></ul> |
| [Ziel](../../../destinations/home.md) | <ul><li>Aktivieren</li></ul> |

## Zugriff auf Prüfprotokolle

Wenn die Funktion für Ihr Unternehmen aktiviert ist, werden bei auftretenden Aktivitäten automatisch Prüfprotokolle erfasst. Sie müssen die Protokollerfassung nicht manuell aktivieren.

Um Prüfprotokolle anzeigen und exportieren zu können, müssen Sie über die Zugriffssteuerungsberechtigung &quot;Audit-Protokolle anzeigen&quot;verfügen (zu finden unter der Kategorie &quot;Data Governance&quot;). Informationen zum Verwalten individueller Berechtigungen für Platform-Funktionen finden Sie in der [Dokumentation zur Zugriffskontrolle](../../../access-control/home.md).

## Verwalten von Prüfprotokollen in der Benutzeroberfläche

Über den Arbeitsbereich **[!UICONTROL Audits]** in der Platform-Benutzeroberfläche können Sie Prüfprotokolle für verschiedene Experience Platform-Funktionen anzeigen. Der Arbeitsbereich zeigt eine Liste der aufgezeichneten Protokolle an, die standardmäßig von der letzten zur letzten sortiert sind.

![Dashboard &quot;Audit logs&quot;](../../images/audit-logs/audits.png)

Das System zeigt nur Prüfprotokolle aus dem letzten Jahr an. Alle Protokolle, die diese Beschränkung überschreiten, werden automatisch aus dem System entfernt.

Wählen Sie ein Ereignis aus der Liste aus, um seine Details in der rechten Leiste anzuzeigen.

![Ereignisdetails](../../images/audit-logs/select-event.png)

<!-- (Planned for post-beta release)
### Export an audit log

Select **[!UICONTROL Download log]** to export an audit log.
-->

## Verwalten von Auditprotokollen in der API

Alle Aktionen, die Sie in der Benutzeroberfläche ausführen können, können auch über API-Aufrufe ausgeführt werden. Weitere Informationen finden Sie im [API-Referenzdokument](https://www.adobe.io/experience-platform-apis/references/audit-query/) .

## Verwalten von Auditprotokollen für Adobe Admin Console

Informationen zum Verwalten von Auditprotokollen für Aktivitäten in Adobe Admin Console finden Sie im folgenden [Dokument](https://helpx.adobe.com/enterprise/using/audit-logs.html).

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Prüfprotokolle in Experience Platform verwaltet werden. Weitere Informationen zum Überwachen von Platform-Aktivitäten finden Sie in der Dokumentation zu [Observability Insights](../../../observability/home.md) und [Überwachung der Datenerfassung](../../../ingestion/quality/monitor-data-ingestion.md).
