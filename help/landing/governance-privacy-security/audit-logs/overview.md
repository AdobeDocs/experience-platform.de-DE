---
title: Übersicht über Auditprotokolle
description: Erfahren Sie, wie Sie mithilfe von Audit-Protokollen sehen können, wer welche Aktionen in Adobe Experience Platform durchgeführt hat.
role: Admin,Developer
feature: Audits
exl-id: 00baf615-5b71-4e0a-b82a-ca0ce8566e7f
source-git-commit: f6e413d2d8b644775b6714739113174f5d9cb0d9
workflow-type: tm+mt
source-wordcount: '1388'
ht-degree: 37%

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

Grundsätzlich teilt ein Prüfprotokoll **Wer** **was** und **wann** mit. Jede in einem Protokoll aufgezeichnete Aktion enthält Metadaten, die den Aktionstyp, das Datum und die Uhrzeit, die E-Mail-ID des Benutzers, der die Aktion ausgeführt hat, und zusätzliche Attribute für den Aktionstyp angeben.

>[!NOTE]
>
> Die Metadaten für die Aktionen **Benutzer hinzufügen** und **Benutzer entfernen** innerhalb der Ressource **Rolle** enthalten nicht die E-Mail-ID des Benutzers, der die Aktion ausgeführt hat. Stattdessen zeigen die Protokolle die vom System generierte E-Mail-ID an (system@adobe.com).

In diesem Dokument werden Auditprotokolle in Platform behandelt, einschließlich der Anzeige und Verwaltung in der Benutzeroberfläche oder API.

## Von Audit-Protokollen erfasste Ereignistypen {#category}

In der folgenden Tabelle sind die Aktionen aufgeführt, für die Ressourcen in Auditprotokollen aufgezeichnet werden:

| Ressource | Aktionen |
| --- | --- |
| [Zugriffssteuerungsrichtlinie (attributbasierte Zugriffskontrolle)](../../../access-control/home.md) | <ul><li>Erstellen</li><li>Update</li><li>Löschen</li></ul> |
| [Konto (Adobe)](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>Erstellen</li><li>Update</li><li>Löschen</li></ul> |
| [Attribution AI-Instanz](../../../intelligent-services/attribution-ai/overview.md) | <ul><li>Erstellen</li><li>Update</li><li>Löschen</li><li>Aktivieren</li><li>Deaktivieren</li></ul> |
| [Administratorprotokolle](../../../landing/governance-privacy-security/audit-logs/overview.md) | <ul><li>Exportieren</li></ul> |
| [Klasse](../../../xdm/schema/composition.md#class) | <ul><li>Erstellen</li><li>Update</li><li>Löschen</li></ul> |
| Berechnetes Attribut | <ul><li>Erstellen</li><li>Update</li><li>Löschen</li></ul> |
| [Customer AI-Instanz](../../../intelligent-services/customer-ai/overview.md) | <ul><li>Erstellen</li><li>Update</li><li>Löschen</li><li>Aktivieren</li><li>Deaktivieren</li></ul> |
| [Datensatz](../../../catalog/datasets/overview.md) | <ul><li>Erstellen</li><li>Update</li><li>Löschen</li><li>Aktivieren für [Echtzeit-Kundenprofil](../../../profile/home.md)</li><li>Für Profil deaktivieren</li><li>Daten hinzufügen</li><li>Batch löschen</li></ul> |
| [Datastream](../../../datastreams/overview.md) | <ul><li>Erstellen</li><li>Update</li><li>Löschen</li><li>Aktivieren</li><li>Deaktivieren</li><li>[Zuordnung bearbeiten](../../../datastreams/data-prep.md)</li></ul> |
| [Datentypen](../../../xdm/schema/composition.md#data-type) | <ul><li>Erstellen</li><li>Update</li><li>Löschen</li></ul> |
| [Ziel](../../../destinations/home.md) | <ul><li>Erstellen</li><li>Update</li><li>Löschen</li><li>Aktivieren</li><li>Deaktivieren</li><li>Datensatzaktivierung</li><li>Datensatzentfernung</li><li>Profilaktivierung</li><li>Profilentfernung</li></ul> |
| [Feldergruppe](../../../xdm/schema/composition.md#field-group) | <ul><li>Erstellen</li><li>Update</li><li>Löschen</li></ul> |
| [Identitätsdiagramm](../../../identity-service/features/identity-graph-viewer.md) | <ul><li>Ansicht</li></ul> |
| [Identitäts-Namespace](../../../identity-service/features/namespaces.md) | <ul><li>Erstellen</li><li>Update</li></ul> |
| [Zusammenführungsrichtlinie](../../../profile/merge-policies/overview.md) | <ul><li>Erstellen</li><li>Update</li><li>Löschen</li></ul> |
| [Produktprofil](../../../access-control/home.md) | <ul><li>Erstellen</li><li>Update</li><li>Löschen</li></ul> |
| [Abfrage](../../../query-service/ui/overview.md) | <ul><li>Execute</li></ul> |
| [Abfragevorlage](../../../query-service/ui/overview.md) | <ul><li>Erstellen</li><li>Update</li><li>Löschen</li></ul> |
| [Rolle (attributbasierte Zugriffssteuerung)](../../../access-control/home.md) | <ul><li>Erstellen</li><li>Update</li><li>Löschen</li><li>Benutzer hinzufügen</li><li>Benutzer entfernen</li></ul> |
| [Sandbox](../../../sandboxes/home.md) | <ul><li>Erstellen</li><li>Update</li><li>Zurücksetzen</li><li>Löschen</li></ul> |
| [Geplante Abfrage](../../../query-service/ui/overview.md) | <ul><li>Erstellen</li><li>Update</li><li>Löschen</li></ul> |
| [Schema](../../../xdm/schema/composition.md) | <ul><li>Erstellen</li><li>Update</li><li>Löschen</li><li>Für Profile aktivieren</li></ul> |
| [Segment](../../../segmentation/home.md) | <ul><li>Erstellen</li><li>Löschen</li><li>Segmentaktivierung</li><li>Segmententfernung</li></ul> |
| [Source-Datenfluss](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>Erstellen</li><li>Update</li><li>Löschen</li><li>Aktivieren</li><li>Deaktivieren</li><li>Datensatzaktivierung</li><li>Datensatzentfernung</li><li>Profilaktivität</li><li>Profilentfernung</li></ul> |
| [Arbeitsreihenfolge](../../../hygiene/home.md) | <ul><li>Erstellen</li></ul> |

## Zugriff auf Prüfprotokolle

Wenn die Funktion für Ihr Unternehmen aktiviert ist, werden bei auftretenden Aktivitäten automatisch Prüfprotokolle erfasst. Sie müssen die Datenerfassung in Audit-Protokollen nicht manuell aktivieren.

Um Prüfprotokolle anzeigen und exportieren zu können, müssen Sie über die Zugriffssteuerungsberechtigung **[!UICONTROL Benutzeraktivitätsprotokoll anzeigen]** verfügen (zu finden unter der Kategorie [!UICONTROL Data Governance] ). Informationen zum Verwalten individueller Berechtigungen für Platform-Funktionen finden Sie in der Dokumentation zur [Zugriffskontrolle](../../../access-control/home.md) .

## Verwalten von Audit-Protokollen in der Benutzeroberfläche {#managing-audit-logs-in-the-ui}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_instructions"
>title="Anweisungen"
>abstract="<ul><li>Wählen Sie <b>Audits</b> in der linken Navigation aus. Der Arbeitsbereich „Audits“ zeigt eine Liste der aufgezeichneten Protokolle an, die standardmäßig absteigend nach ihrer Aktualität sortiert sind.</li>   <li> HINWEIS: Audit-Protokolle werden 365 Tage lang aufbewahrt und danach aus dem System gelöscht. Daher können Sie nur für einen Zeitraum von maximal 365 Tagen zurückgehen. Wenn Sie auf Daten zurückgreifen müssen, die älter als 365 Tage sind, sollten Sie Protokolle regelmäßig exportieren, um Ihre internen Richtlinienanforderungen zu erfüllen. </li><li>Wählen Sie ein Ereignis aus der Liste aus, um seine Details in der rechten Leiste anzuzeigen. </li><li>Wählen Sie das Trichtersymbol aus, um eine Liste von Filterfeldern anzuzeigen, mit denen die Ergebnisse eingegrenzt werden können. Unabhängig von den ausgewählten Filtern werden nur die letzten 1.000 Datensätze angezeigt. </li><li>Um die aktuelle Liste der Audit-Prüfprotokolle zu exportieren, wählen Sie **Protokoll herunterladen** aus.</li><li>Weitere Hilfe zu dieser Funktion finden Sie im Abschnitt <a href="https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/audit-logs/overview.html?lang=de">Übersicht über Audit-Protokolle</a> auf Experience League.</li></ul>"

Sie können Prüfprotokolle für verschiedene Experience Platform-Funktionen im Arbeitsbereich **[!UICONTROL Audits]** der Platform-Benutzeroberfläche anzeigen. Der Arbeitsbereich zeigt eine Liste der aufgezeichneten Protokolle an, die standardmäßig von der letzten zur letzten sortiert sind.

![Das Dashboard &quot;Prüfungen&quot;zur Hervorhebung von Audits im linken Menü.](../../images/audit-logs/audits.png)

Prüfprotokolle werden 365 Tage lang aufbewahrt, danach werden sie aus dem System gelöscht. Daher können Sie nur für einen Zeitraum von maximal 365 Tagen zurückgehen. Wenn Sie Daten von mehr als 365 Tagen benötigen, sollten Sie Protokolle regelmäßig exportieren, um Ihre internen Richtlinienanforderungen zu erfüllen.

Wählen Sie ein Ereignis aus der Liste aus, um seine Details in der rechten Leiste anzuzeigen.

![Audits Dashboard-Aktivitätsprotokoll , wobei der Bereich mit Ereignisdetails hervorgehoben ist.](../../images/audit-logs/select-event.png)

### Auditprotokolle filtern

>[!NOTE]
>
>Da es sich hierbei um eine neue Funktion handelt, gehen die angezeigten Daten nur bis März 2022 zurück. Je nach ausgewählter Ressource stehen möglicherweise frühere Daten ab Januar 2022 zur Verfügung.


Wählen Sie das Trichtersymbol (![Filtersymbol](/help/images/icons/filter.png)) aus, um eine Liste mit Filtersteuerelementen anzuzeigen, mit denen die Ergebnisse eingegrenzt werden können. Unabhängig von den ausgewählten Filtern werden nur die letzten 1000 Datensätze angezeigt.

![Das Dashboard &quot;Prüfungen&quot;mit dem gefilterten Aktivitätsprotokoll ist hervorgehoben.](../../images/audit-logs/filters.png)

Die folgenden Filter sind für Prüfereignisse in der Benutzeroberfläche verfügbar:

| Filter | Beschreibung |
| --- | --- |
| [!UICONTROL Kategorie] | Verwenden Sie das Dropdown-Menü, um die angezeigten Ergebnisse nach [Kategorie](#category) zu filtern. |
| [!UICONTROL Aktion] | Nach Aktion filtern. Die für jeden Dienst verfügbaren Aktionen finden Sie in der obigen Ressourcentabelle. |
| [!UICONTROL Benutzer] | Geben Sie die vollständige Benutzer-ID ein (z. B. `johndoe@acme.com`), die nach Benutzer gefiltert werden soll. |
| [!UICONTROL Status] | Filtern Sie danach, ob die Aktion zulässig (abgeschlossen) oder aufgrund fehlender [Zugriffssteuerungsberechtigungen](../../../access-control/home.md) verweigert wurde. |
| [!UICONTROL Datum] | Wählen Sie ein Startdatum und/oder ein Enddatum aus, um einen Datumsbereich zu definieren, nach dem die Ergebnisse gefiltert werden sollen. Daten können mit einem Lookback-Zeitraum von 90 Tagen exportiert werden (z. B. 2021-12-15-2022-03-15). Dies kann je nach Ereignistyp unterschiedlich sein. |

Um einen Filter zu entfernen, klicken Sie auf das „X“ auf dem Symbol für den betreffenden Filter, oder wählen Sie **[!UICONTROL Alle löschen]** aus, um alle Filter zu entfernen.

![Das Dashboard &quot;Prüfungen&quot;mit hervorgehobenem leeren Filter.](../../images/audit-logs/clear-filters.png)

Die zurückgegebenen Auditprotokolldaten enthalten die folgenden Informationen zu allen Abfragen, die Ihre ausgewählten Filterkriterien erfüllen.

| Spaltenname | Beschreibung |
|---|---|
| [!UICONTROL Zeitstempel] | Das genaue Datum und die Uhrzeit der im Format `month/day/year hour:minute AM/PM` durchgeführten Aktion. |
| [!UICONTROL Asset-Name] | Der Wert für das Feld [!UICONTROL Asset-Name] hängt von der Kategorie ab, die als Filter ausgewählt wurde. |
| [!UICONTROL Kategorie] | Dieses Feld entspricht der im Dropdown-Menü Filter ausgewählten Kategorie. |
| [!UICONTROL Aktion] | Die verfügbaren Aktionen hängen von der als Filter ausgewählten Kategorie ab. |
| [!UICONTROL Benutzer] | Dieses Feld enthält die Benutzer-ID, die die Abfrage ausgeführt hat. |

![Das Dashboard &quot;Prüfungen&quot;mit dem gefilterten Aktivitätsprotokoll ist hervorgehoben.](../../images/audit-logs/filtered.png)

### Auditprotokolle exportieren

Um die aktuelle Liste der Audit-Prüfprotokolle zu exportieren, wählen Sie **[!UICONTROL Protokoll herunterladen]** aus.

![Das Dashboard &quot;Prüfungen&quot;mit dem hervorgehobenen [!UICONTROL Download-Protokoll].](../../images/audit-logs/download.png)

Wählen Sie im angezeigten Dialogfeld Ihr bevorzugtes Format (entweder **[!UICONTROL CSV]** oder **[!UICONTROL JSON]**) und dann **[!UICONTROL Download]** aus. Der Browser lädt die generierte Datei herunter und speichert sie auf Ihrem Computer.

![Das Dialogfeld für die Dateiformatauswahl mit der Markierung [!UICONTROL Download].](../../images/audit-logs/select-download-format.png)

## Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Prüfwarnungen aktivieren, um Benachrichtigungen für die folgenden Regeln zu erhalten:

* Zielgruppenerstellung
* Zielgruppenaktualisierung
* Zielgruppenlöschung
* Datensatz erstellen
* Datensatz-Update
* Datensatz löschen
* Schema erstellen
* Schemaaktualisierung
* Schemalöschen

Wählen Sie den gewünschten Warnhinweis aus der Liste aus, um sich für den Erhalt von Benachrichtigungen anzumelden. Weitere Informationen zu Warnungen finden Sie im Handbuch zum [Abonnieren von Warnungen über die Benutzeroberfläche](../../../observability/alerts/ui.md).

## Verwalten von Auditprotokollen in der API

Alle Aktionen, die Sie in der Benutzeroberfläche ausführen können, können auch über API-Aufrufe ausgeführt werden. Weitere Informationen finden Sie im [API-Referenzdokument](https://www.adobe.io/experience-platform-apis/references/audit-query/) .

## Verwalten von Auditprotokollen für Adobe Admin Console

Informationen zum Verwalten von Prüfprotokollen für Aktivitäten in Adobe Admin Console finden Sie im folgenden [Dokument](https://helpx.adobe.com/enterprise/using/audit-logs.html).

## Nächste Schritte und zusätzliche Ressourcen

In diesem Handbuch wurde beschrieben, wie Prüfprotokolle in Experience Platform verwaltet werden. Weitere Informationen zum Überwachen von Platform-Aktivitäten finden Sie in der Dokumentation zu [Observability Insights](../../../observability/home.md) und [zur Überwachung der Datenerfassung](../../../ingestion/quality/monitor-data-ingestion.md).

Sehen Sie sich das folgende Video an, um Ihr Verständnis der Auditprotokolle in Experience Platform zu verbessern:

>[!VIDEO](https://video.tv.adobe.com/v/341450?quality=12&learn=on)
