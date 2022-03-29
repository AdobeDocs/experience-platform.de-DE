---
title: Übersicht über Auditprotokolle
description: Erfahren Sie, wie Sie mithilfe von Auditprotokollen sehen können, wer welche Aktionen in Adobe Experience Platform durchgeführt hat.
exl-id: 00baf615-5b71-4e0a-b82a-ca0ce8566e7f
source-git-commit: d726576a4d1f29d83f3b7cf72c9f5c5d4ff114d3
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 8%

---

# Auditprotokolle

Um die Transparenz und Sichtbarkeit der im System durchgeführten Aktivitäten zu erhöhen, ermöglicht es Ihnen Adobe Experience Platform, die Benutzeraktivität für verschiedene Dienste und Funktionen in Form von &quot;Auditprotokollen&quot;zu überprüfen. Diese Protokolle bilden ein Audit-Protokoll, das Ihnen bei der Fehlerbehebung in Platform helfen und Ihrem Unternehmen helfen kann, die Richtlinien der Unternehmensdatenverwaltung und die gesetzlichen Anforderungen effektiv zu erfüllen.

In einem Prüfprotokoll wird **who** ausgeführt **what** Aktion und **when**. Jede in einem Protokoll aufgezeichnete Aktion enthält Metadaten, die den Aktionstyp, das Datum und die Uhrzeit, die E-Mail-ID des Benutzers, der die Aktion ausgeführt hat, und zusätzliche Attribute für den Aktionstyp angeben.

In diesem Dokument werden Auditprotokolle in Platform behandelt, einschließlich der Anzeige und Verwaltung in der Benutzeroberfläche oder API.

## Von Prüfprotokollen erfasste Ereignistypen {#category}

In der folgenden Tabelle sind die Aktionen aufgeführt, für die Ressourcen in Auditprotokollen aufgezeichnet werden:

| Ressource | Aktionen |
| --- | --- |
| [Datensatz](../../../catalog/datasets/overview.md) | <ul><li>Erstellung</li><li>Update</li><li>Löschen</li><li>Aktivieren für [Echtzeit-Kundenprofil](../../../profile/home.md)</li><li>Profil deaktivieren</li></ul> |
| [Schema](../../../xdm/schema/composition.md) | <ul><li>Erstellung</li><li>Aktualisieren</li><li>Löschen</li><li>Profil aktivieren</li></ul> |
| [Klasse](../../../xdm/schema/composition.md#class) | <ul><li>Erstellung</li><li>Aktualisieren</li><li>Löschen</li></ul> |
| [Feldergruppe](../../../xdm/schema/composition.md#field-group) | <ul><li>Erstellung</li><li>Aktualisieren</li><li>Löschen</li></ul> |
| [Datentyp](../../../xdm/schema/composition.md#data-type) | <ul><li>Erstellung</li><li>Aktualisieren</li><li>Löschen</li></ul> |
| [Sandbox](../../../sandboxes/home.md) | <ul><li>Erstellung</li><li>Aktualisieren</li><li>Zurücksetzen</li><li>Löschen</li></ul> |
| [Ziel](../../../destinations/home.md) | <ul><li>Erstellung</li><li>Aktualisieren</li><li>Löschen</li><li>Aktivieren</li><li>Deaktivieren</li><li>Datensatz aktivieren</li><li>Datensatz entfernen</li><li>Profil aktivieren</li><li>Profil löschen</li></ul> |
| [Segment](../../../segmentation/home.md) | <ul><li>Erstellung</li><li>Löschen</li><li>Segmentaktivierung</li><li>Segment entfernen</li></ul> |
| [Zusammenführungsrichtlinie](../../../profile/merge-policies/overview.md) | <ul><li>Erstellung</li><li>Aktualisieren</li><li>Löschen</li></ul> |
| [Berechnetes Attribut](../../../profile/computed-attributes/overview.md) | <ul><li>Erstellung</li><li>Aktualisieren</li><li>Löschen</li></ul> |
| [Produktprofile](../../../access-control/home.md) | <ul><li>Erstellung</li><li>Aktualisieren</li><li>Löschen</li></ul> |
| [Konto (Adobe)](../../../access-control/home.md) | <ul><li>Erstellung</li><li>Aktualisieren</li><li>Löschen</li></ul> |

## Zugriff auf Prüfprotokolle

Wenn die Funktion für Ihr Unternehmen aktiviert ist, werden bei auftretenden Aktivitäten automatisch Prüfprotokolle erfasst. Sie müssen die Protokollerfassung nicht manuell aktivieren.

Um Prüfprotokolle anzeigen und exportieren zu können, benötigen Sie die **[!UICONTROL Protokoll zu Benutzeraktivitäten anzeigen]** Zugriffskontrollberechtigung erteilt (zu finden unter [!UICONTROL Data Governance] Kategorie). Informationen zum Verwalten individueller Berechtigungen für Platform-Funktionen finden Sie im Abschnitt [Zugriffssteuerungsdokumentation](../../../access-control/home.md).

## Verwalten von Prüfprotokollen in der Benutzeroberfläche

Sie können Prüfprotokolle für verschiedene Funktionen der Experience Platform im **[!UICONTROL Prüfungen]** Arbeitsbereich in der Platform-Benutzeroberfläche. Der Arbeitsbereich zeigt eine Liste der aufgezeichneten Protokolle an, die standardmäßig von der letzten zur letzten sortiert sind.

![Dashboard &quot;Audit logs&quot;](../../images/audit-logs/audits.png)

Prüfprotokolle werden 365 Tage lang aufbewahrt, danach werden sie aus dem System gelöscht. Daher können Sie nur für einen Zeitraum von maximal 365 Tagen zurückkehren.

Wählen Sie ein Ereignis aus der Liste aus, um seine Details in der rechten Leiste anzuzeigen.

![Ereignisdetails](../../images/audit-logs/select-event.png)

### Auditprotokolle filtern

>[!NOTE]
>
>Da es sich hierbei um eine neue Funktion handelt, gehen die angezeigten Daten nur bis März 2022 zurück. Je nach ausgewählter Ressource stehen möglicherweise frühere Daten ab Januar 2022 zur Verfügung.


Wählen Sie das Trichtersymbol (![Filtersymbol](../../images/audit-logs/icon.png)), um eine Liste von Filtersteuerelementen anzuzeigen, die die Eingrenzung der Ergebnisse unterstützen. Unabhängig von den ausgewählten Filtern werden nur die letzten 1000 Datensätze angezeigt.

![Filter](../../images/audit-logs/filters.png)

Die folgenden Filter sind für Prüfereignisse in der Benutzeroberfläche verfügbar:

| Filter | Beschreibung |
| --- | --- |
| [!UICONTROL Kategorie] | Verwenden Sie das Dropdown-Menü, um die angezeigten Ergebnisse nach [category](#category). |
| [!UICONTROL Aktion] | Nach Aktion filtern. Derzeit nur [!UICONTROL Erstellen] und [!UICONTROL Löschen] -Aktionen gefiltert werden. |
| [!UICONTROL Benutzer] | Geben Sie die vollständige Benutzer-ID ein (z. B. `johndoe@acme.com`), um nach Benutzer zu filtern. |
| [!UICONTROL Status] | Filtern Sie nach, ob die Aktion zulässig (abgeschlossen) oder verweigert wurde, weil [Zugriffskontrolle](../../../access-control/home.md) Berechtigungen. |
| [!UICONTROL Datum] | Wählen Sie ein Startdatum und/oder ein Enddatum aus, um einen Datumsbereich zu definieren, nach dem die Ergebnisse gefiltert werden sollen. Daten können mit einem Lookback-Zeitraum von 90 Tagen exportiert werden (z. B. 2021-12-15-2022-03-15). Dies kann je nach Ereignistyp unterschiedlich sein. |

Um einen Filter zu entfernen, wählen Sie das &quot;X&quot;auf dem Pillensymbol für den betreffenden Filter aus oder wählen Sie **[!UICONTROL Alle löschen]** um alle Filter zu entfernen.

![Filter löschen](../../images/audit-logs/clear-filters.png)

### Audit-Protokolle exportieren

Um die aktuelle Liste der Prüfprotokolle zu exportieren, wählen Sie **[!UICONTROL Protokoll herunterladen]**.

![Protokoll herunterladen](../../images/audit-logs/download.png)

Wählen Sie im angezeigten Dialogfeld Ihr bevorzugtes Format aus (entweder **[!UICONTROL CSV]** oder **[!UICONTROL JSON]**), wählen Sie **[!UICONTROL Download]**. Der Browser lädt die generierte Datei herunter und speichert sie auf Ihrem Computer.

![Download-Format auswählen](../../images/audit-logs/select-download-format.png)

## Verwalten von Auditprotokollen in der API

Alle Aktionen, die Sie in der Benutzeroberfläche ausführen können, können auch über API-Aufrufe ausgeführt werden. Siehe [API-Referenzdokument](https://www.adobe.io/experience-platform-apis/references/audit-query/) für weitere Informationen.

## Verwalten von Auditprotokollen für Adobe Admin Console

Informationen zum Verwalten von Auditprotokollen für Aktivitäten in Adobe Admin Console finden Sie in den folgenden Abschnitten. [Dokument](https://helpx.adobe.com/enterprise/using/audit-logs.html).

## Nächste Schritte und zusätzliche Ressourcen

In diesem Handbuch wurde beschrieben, wie Prüfprotokolle in Experience Platform verwaltet werden. Weitere Informationen zum Überwachen von Platform-Aktivitäten finden Sie in der Dokumentation zu [Observability Insights](../../../observability/home.md) und [Überwachen der Datenerfassung](../../../ingestion/quality/monitor-data-ingestion.md).

Sehen Sie sich das folgende Video an, um Ihr Verständnis der Auditprotokolle in Experience Platform zu verbessern:

>[!VIDEO](https://video.tv.adobe.com/v/341450?quality=12&learn=on)
