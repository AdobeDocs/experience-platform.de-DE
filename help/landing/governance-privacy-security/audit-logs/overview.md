---
title: Übersicht über Auditprotokolle
description: Erfahren Sie, wie Sie mithilfe von Audit-Protokollen sehen können, wer welche Aktionen in Adobe Experience Platform durchgeführt hat.
exl-id: 00baf615-5b71-4e0a-b82a-ca0ce8566e7f
source-git-commit: 8f61840ad60b7d24c980b218b6f742485f5ebfdd
workflow-type: tm+mt
source-wordcount: '1156'
ht-degree: 57%

---

# Audit-Protokolle {#audit-logs}

>[!CONTEXTUALHELP]
>id="platform_audits_privacyconsole_actions"
>title="Häufigste Aktionen"
>abstract="Dieses Widget zeigt die häufigsten Arten von Aktionen an, die innerhalb des ausgewählten Zeitraums in Experience Platform ausgeführt wurden. Um die vollständige Liste der aufgezeichneten Aktionen in Platform anzuzeigen, wählen Sie in der linken Navigationsleiste **Audits**."

>[!CONTEXTUALHELP]
>id="platform_audits_privacyconsole_users"
>title="Am häufigsten anwesende Benutzende"
>abstract="Dieses Widget zeigt die Benutzenden an, die innerhalb des ausgewählten Zeitraums die meisten Aktionen in Experience Platform ausgeführt haben. Um die vollständige Liste der aufgezeichneten Aktionen in Platform anzuzeigen, wählen Sie in der linken Navigationsleiste **Audits**."

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_description"
>title="Überwachen von Benutzeraktivitäten in Platform"
>abstract="<h2>Beschreibung</h2><p>Sie können die Benutzeraktivität für verschiedene Platform-Dienste und -Funktionen in Form von Audit-Protokollen überwachen. Diese Protokolle bilden ein Audit-Protokoll, in dem verzeichnet wird, <b>wer</b> <b>welche</b> Aktion <b>wann</b> ausgeführt hat. Audit-Protokolle können die Fehlerbehebung in Platform erleichtern und Ihrem Unternehmen helfen, die Richtlinien zur Unternehmensdatenverwaltung und die gesetzlichen Anforderungen effektiv zu erfüllen.</p>"

Um die Transparenz und Sichtbarkeit der im System durchgeführten Aktivitäten zu erhöhen, ermöglicht es Ihnen Adobe Experience Platform, die Benutzeraktivität für verschiedene Dienste und Funktionen in Form von &quot;Auditprotokollen&quot;zu überprüfen. Diese Protokolle bilden ein Audit-Protokoll, das Ihnen bei der Fehlerbehebung in Platform helfen und Ihrem Unternehmen helfen kann, die Richtlinien der Unternehmensdatenverwaltung und die gesetzlichen Anforderungen effektiv zu erfüllen.

In einem Auditprotokoll wird festgehalten, **wer** **welche** Aktion **wann** ausgeführt hat. Jede in einem Protokoll aufgezeichnete Aktion enthält Metadaten, die den Aktionstyp, das Datum und die Uhrzeit, die E-Mail-ID der oder des Benutzenden, die oder der die Aktion durchgeführt hat, und weitere für den Aktionstyp relevante Attribute angeben.

In diesem Dokument werden Auditprotokolle in Platform behandelt, einschließlich der Anzeige und Verwaltung in der Benutzeroberfläche oder API.

## Von Audit-Protokollen erfasste Ereignistypen {#category}

In der folgenden Tabelle sind die Aktionen aufgeführt, für die Ressourcen in Auditprotokollen aufgezeichnet werden:

| Ressource | Aktionen |
| --- | --- |
| [Zugriffskontrollrichtlinie (attributbasierte Zugriffskontrolle)](../../../access-control/home.md) | <ul><li>Erstellen von</li><li>Update</li><li>Löschen</li></ul> |
| [Konto (Adobe)](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>Erstellen von</li><li>Update</li><li>Löschen</li></ul> |
| [Attributions-KI-Instanz](../../../intelligent-services/attribution-ai/overview.md) | <ul><li>Erstellen von</li><li>Update</li><li>Löschen</li><li>Aktivieren</li><li>Deaktivieren</li></ul> |
| [Administratorprotokolle](../../../landing/governance-privacy-security/audit-logs/overview.md) | <ul><li>Exportieren</li></ul> |
| [Klasse](../../../xdm/schema/composition.md#class) | <ul><li>Erstellen von</li><li>Update</li><li>Löschen</li></ul> |
| Berechnetes Attribut | <ul><li>Erstellen von</li><li>Update</li><li>Löschen</li></ul> |
| [Kunden-KI-Instanz](../../../intelligent-services/customer-ai/overview.md) | <ul><li>Erstellen von</li><li>Update</li><li>Löschen</li><li>Aktivieren</li><li>Deaktivieren</li></ul> |
| [Datensatz](../../../catalog/datasets/overview.md) | <ul><li>Erstellen von</li><li>Update</li><li>Löschen</li><li>Aktivieren für [Echtzeit-Kundenprofil](../../../profile/home.md)</li><li>Profil deaktivieren</li><li>Daten hinzufügen</li><li>Batch löschen</li></ul> |
| [Datenstrom](../../../edge/datastreams/overview.md) | <ul><li>Erstellen von</li><li>Update</li><li>Löschen</li><li>Aktivieren</li><li>Deaktivieren</li><li>[Zuordnung bearbeiten](../../../edge/datastreams/data-prep.md)</li></ul> |
| [Datentypen](../../../xdm/schema/composition.md#data-type) | <ul><li>Erstellen von</li><li>Update</li><li>Löschen</li></ul> |
| [Ziel](../../../destinations/home.md) | <ul><li>Erstellen von</li><li>Update</li><li>Löschen</li><li>Aktivieren</li><li>Deaktivieren</li><li>Datensatz aktivieren</li><li>Datensatz entfernen</li><li>Profil aktivieren</li><li>Profil löschen</li></ul> |
| [Feldergruppe](../../../xdm/schema/composition.md#field-group) | <ul><li>Erstellen von</li><li>Update</li><li>Löschen</li></ul> |
| [Identitätsdiagramm](../../../identity-service/ui/identity-graph-viewer.md) | <ul><li>Ansicht</li></ul> |
| [Identity-Namespace](../../../identity-service/ui/identity-graph-viewer.md) | <ul><li>Erstellen von</li><li>Update</li></ul> |
| [Zusammenführungsrichtlinie](../../../profile/merge-policies/overview.md) | <ul><li>Erstellen von</li><li>Update</li><li>Löschen</li></ul> |
| [Produktprofile](../../../access-control/home.md) | <ul><li>Erstellen von</li><li>Update</li><li>Löschen</li></ul> |
| [Abfrage](../../../query-service/ui/overview.md) | <ul><li>Execute</li></ul> |
| [Abfragevorlage](../../../query-service/ui/overview.md) | <ul><li>Erstellen von</li><li>Update</li><li>Löschen</li></ul> |
| [Rolle (attributbasierte Zugriffssteuerung)](../../../access-control/home.md) | <ul><li>Erstellen von</li><li>Update</li><li>Löschen</li><li>Benutzer hinzufügen</li><li>Benutzer löschen</li></ul> |
| [Sandbox](../../../sandboxes/home.md) | <ul><li>Erstellen von</li><li>Update</li><li>Zurücksetzen</li><li>Löschen</li></ul> |
| [Geplante Abfrage](../../../query-service/ui/overview.md) | <ul><li>Erstellen von</li><li>Update</li><li>Löschen</li></ul> |
| [Schema](../../../xdm/schema/composition.md) | <ul><li>Erstellen von</li><li>Update</li><li>Löschen</li><li>Aktivieren Sie es für das Profil</li></ul> |
| [Segment](../../../segmentation/home.md) | <ul><li>Erstellen von</li><li>Löschen</li><li>Segmentaktivierung</li><li>Segment entfernen</li></ul> |
| [Quelldatenfluss](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>Erstellen von</li><li>Update</li><li>Löschen</li><li>Aktivieren</li><li>Deaktivieren</li><li>Datensatz aktivieren</li><li>Datensatz entfernen</li><li>Profilaktivität</li><li>Profil entfernen</li></ul> |
| [Arbeitsauftrag](../../../hygiene/home.md) | <ul><li>Erstellen von</li></ul> |

## Zugriff auf Auditprotokolle

Wenn diese Funktion für Ihr Unternehmen aktiviert ist, werden bei Aktivitäten automatisch Auditprotokolle aufgezeichnet. Sie müssen die Datenerfassung in Audit-Protokollen nicht manuell aktivieren.

Um Prüfprotokolle anzeigen und exportieren zu können, benötigen Sie die **[!UICONTROL Protokoll zu Benutzeraktivitäten anzeigen]** Zugriffskontrollberechtigung erteilt (zu finden unter [!UICONTROL Data Governance] Kategorie). Informationen zum Verwalten individueller Berechtigungen für Platform-Funktionen finden Sie im Abschnitt [Zugriffssteuerungsdokumentation](../../../access-control/home.md).

## Verwalten von Prüfprotokollen in der Benutzeroberfläche {#managing-audit-logs-in-the-ui}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_instructions"
>title="Anleitung"
>abstract="<ul><li>Wählen Sie <b>Audits</b> in der linken Navigation aus. Der Arbeitsbereich „Audits“ zeigt eine Liste der aufgezeichneten Protokolle an, die standardmäßig absteigend nach ihrer Aktualität sortiert sind.</li>   <li> HINWEIS: Audit-Protokolle werden 365 Tage lang aufbewahrt und danach aus dem System gelöscht. Daher können Sie nur für einen Zeitraum von maximal 365 Tagen zurückgehen. Wenn Sie auf Daten zurückgreifen müssen, die älter als 365 Tage sind, sollten Sie Protokolle regelmäßig exportieren, um Ihre internen Richtlinienanforderungen zu erfüllen. </li><li>Wählen Sie ein Ereignis aus der Liste aus, um seine Details in der rechten Leiste anzuzeigen. </li><li>Wählen Sie das Trichtersymbol aus, um eine Liste von Filterfeldern anzuzeigen, mit denen die Ergebnisse eingegrenzt werden können. Unabhängig von den ausgewählten Filtern werden nur die letzten 1.000 Datensätze angezeigt. </li><li>Um die aktuelle Liste der Audit-Prüfprotokolle zu exportieren, wählen Sie **Protokoll herunterladen** aus.</li><li>Weitere Hilfe zu dieser Funktion finden Sie im Abschnitt <a href="https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/audit-logs/overview.html?lang=de">Übersicht über Audit-Protokolle</a> auf Experience League.</li></ul>"

Sie können Prüfprotokolle für verschiedene Funktionen der Experience Platform im **[!UICONTROL Prüfungen]** Arbeitsbereich in der Platform-Benutzeroberfläche. Der Arbeitsbereich „“ zeigt eine Liste der aufgezeichneten Protokolle an, die standardmäßig absteigend nach ihrer Aktualität sortiert sind.

![Dashboard &quot;Audit logs&quot;](../../images/audit-logs/audits.png)

Prüfprotokolle werden 365 Tage lang aufbewahrt, danach werden sie aus dem System gelöscht. Daher können Sie nur für einen Zeitraum von maximal 365 Tagen zurückgehen. Wenn Sie Daten von mehr als 365 Tagen benötigen, sollten Sie Protokolle regelmäßig exportieren, um Ihre internen Richtlinienanforderungen zu erfüllen.

Wählen Sie ein Ereignis aus der Liste aus, um seine Details in der rechten Leiste anzuzeigen.

![Ereignisdetails](../../images/audit-logs/select-event.png)

### Filtern von Auditprotokollen

>[!NOTE]
Da es sich hierbei um eine neue Funktion handelt, gehen die angezeigten Daten nur bis März 2022 zurück. Je nach ausgewählter Ressource stehen möglicherweise frühere Daten ab Januar 2022 zur Verfügung.


Wählen Sie das Trichtersymbol (![Filtersymbol](../../images/audit-logs/icon.png)) aus, um eine Liste von Filterfeldern anzuzeigen, mit denen die Ergebnisse eingegrenzt werden können. Unabhängig von den ausgewählten Filtern werden nur die letzten 1000 Datensätze angezeigt.

![Filter](../../images/audit-logs/filters.png)

Die Benutzeroberfläche verfügt für Protokolle über folgende Filter:

| Filter | Beschreibung |
| --- | --- |
| [!UICONTROL Kategorie] | Verwenden Sie das Dropdown-Menü, um die angezeigten Ergebnisse nach [category](#category). |
| [!UICONTROL Aktion] | Nach Aktion filtern. Derzeit nur [!UICONTROL Erstellen] und [!UICONTROL Löschen] -Aktionen gefiltert werden. |
| [!UICONTROL Benutzer] | Geben Sie die vollständige Benutzer-ID ein (z. B. `johndoe@acme.com`), um nach Benutzer zu filtern. |
| [!UICONTROL Status] | Filtern Sie nach, ob die Aktion zulässig (abgeschlossen) oder verweigert wurde, weil [Zugriffskontrolle](../../../access-control/home.md) Berechtigungen. |
| [!UICONTROL Datum] | Wählen Sie ein Startdatum und/oder ein Enddatum aus, um einen Datumsbereich zu definieren, nach dem die Ergebnisse gefiltert werden sollen. Daten können mit einem Lookback-Zeitraum von 90 Tagen exportiert werden (z. B. 2021-12-15-2022-03-15). Dies kann je nach Ereignistyp unterschiedlich sein. |

Um einen Filter zu entfernen, klicken Sie auf das „X“ auf dem Symbol für den betreffenden Filter, oder wählen Sie **[!UICONTROL Alle löschen]** aus, um alle Filter zu entfernen.

![Filter löschen](../../images/audit-logs/clear-filters.png)

### Auditprotokolle exportieren

Um die aktuelle Liste der Audit-Prüfprotokolle zu exportieren, wählen Sie **[!UICONTROL Protokoll herunterladen]** aus.

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
