---
title: Übersicht über Auditprotokolle
description: Erfahren Sie, wie Sie mithilfe von Audit-Protokollen sehen können, wer welche Aktionen in Adobe Experience Platform durchgeführt hat.
role: Admin,Developer
feature: Audits
exl-id: 00baf615-5b71-4e0a-b82a-ca0ce8566e7f
source-git-commit: d6575e44339ea41740fa18af07ce5b893f331488
workflow-type: tm+mt
source-wordcount: '1624'
ht-degree: 33%

---

# Audit-Protokolle {#audit-logs}

>[!CONTEXTUALHELP]
>id="platform_audits_privacyconsole_actions"
>title="Häufigste Aktionen"
>abstract="Dieses Widget zeigt die häufigsten Arten von Aktionen an, die innerhalb des ausgewählten Zeitraums in Experience Platform ausgeführt wurden. Um die vollständige Liste der aufgezeichneten Aktionen in Experience Platform anzuzeigen, wählen Sie im linken Navigationsbereich **Audits** aus."

>[!CONTEXTUALHELP]
>id="platform_audits_privacyconsole_users"
>title="Am häufigsten anwesende Benutzende"
>abstract="Dieses Widget zeigt die Benutzenden an, die innerhalb des ausgewählten Zeitraums die meisten Aktionen in Experience Platform ausgeführt haben. Um die vollständige Liste der aufgezeichneten Aktionen in Experience Platform anzuzeigen, wählen Sie im linken Navigationsbereich **Audits** aus."

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_description"
>title="Überwachen von Benutzeraktivitäten in Experience Platform"
>abstract="<h2>Beschreibung</h2><p>Sie können die Benutzeraktivität für verschiedene Experience Platform-Dienste und -Funktionen in Form von Auditprotokollen überwachen. Diese Protokolle bilden ein Audit-Protokoll, in dem verzeichnet wird, <b>wer</b><b>welche</b> Aktion <b>wann</b> ausgeführt hat. Auditprotokolle können die Fehlerbehebung in Experience Platform erleichtern und Ihrem Unternehmen helfen, die Richtlinien zur Unternehmensdatenverwaltung und die gesetzlichen Anforderungen effektiv zu erfüllen.</p>"

Um die Transparenz und Sichtbarkeit der im System durchgeführten Aktivitäten zu erhöhen, ermöglicht Ihnen Adobe Experience Platform, die Benutzeraktivität für verschiedene Services und Funktionen in Form von „Audit-Protokollen“ zu überprüfen. Diese Protokolle bilden einen Audit-Trail, der Ihnen bei der Fehlerbehebung in Experience Platform helfen kann und Ihrem Unternehmen dabei hilft, die Richtlinien zur Unternehmensdatenverwaltung und die gesetzlichen Anforderungen effektiv zu erfüllen.

In einem Auditprotokoll wird festgehalten **wer** welche **ausgeführt** und **wann**. Jede in einem Protokoll aufgezeichnete Aktion enthält Metadaten, die den Aktionstyp, das Datum und die Uhrzeit, die E-Mail-ID des Benutzers, der die Aktion ausgeführt hat, und zusätzliche Attribute angeben, die für den Aktionstyp relevant sind.

Wenn ein(e) Benutzende(r) eine Aktion ausführt, werden zwei Arten von Audit-Ereignissen aufgezeichnet. Ein Hauptereignis erfasst das Autorisierungsergebnis der Aktion ([!UICONTROL allow] oder [!UICONTROL deny] während ein erweitertes Ereignis das Ausführungsergebnis, [!UICONTROL success] oder [!UICONTROL failure] erfasst. Mehrere erweiterte Ereignisse können mit demselben Hauptereignis verknüpft werden. Beispiel: Beim Aktivieren eines Ziels zeichnet das Kernereignis die Autorisierung der Aktion [!UICONTROL Ziel-Update] auf, während die erweiterten Ereignisse mehrere Aktionen [!UICONTROL Segment aktivieren] aufzeichnen.

>[!NOTE]
>
> Die Metadaten für die Aktionen **Benutzer hinzufügen** und **Benutzer entfernen** innerhalb der **Rolle**-Ressource enthalten nicht die E-Mail-ID des Benutzers, der die Aktion ausgeführt hat. Stattdessen wird in den Protokollen die vom System generierte E-Mail-ID (system@adobe.com) angezeigt.

In diesem Dokument werden Auditprotokolle in Experience Platform behandelt, einschließlich ihrer Anzeige und Verwaltung in der Benutzeroberfläche oder API.

## Von Audit-Protokollen erfasste Ereignistypen {#category}

In der folgenden Tabelle sind die Aktionen aufgeführt, für die Ressourcen in Audit-Protokollen aufgezeichnet werden:

| Ressource | Aktionen |
| --- | --- |
| [Zugriffssteuerungsrichtlinie (attributbasierte Zugriffssteuerung)](../../../access-control/home.md) | <ul><li>Erstellen</li><li>Update</li><li>Löschen</li></ul> |
| [Konto (Adobe)](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>Erstellen</li><li>Update</li><li>Löschen</li></ul> |
| [Attribution AI-Instanz](../../../intelligent-services/attribution-ai/overview.md) | <ul><li>Erstellen</li><li>Update</li><li>Löschen</li><li>Aktivieren</li><li>Deaktivieren</li></ul> |
| [Administratorprotokolle](../../../landing/governance-privacy-security/audit-logs/overview.md) | <ul><li>Exportieren</li></ul> |
| [Klasse](../../../xdm/schema/composition.md#class) | <ul><li>Erstellen</li><li>Update</li><li>Löschen</li></ul> |
| Berechnetes Attribut | <ul><li>Erstellen</li><li>Update</li><li>Löschen</li></ul> |
| [Kunden-KI-Instanz](../../../intelligent-services/customer-ai/overview.md) | <ul><li>Erstellen</li><li>Update</li><li>Löschen</li><li>Aktivieren</li><li>Deaktivieren</li></ul> |
| [Datensatz](../../../catalog/datasets/overview.md) | <ul><li>Erstellen</li><li>Update</li><li>Löschen</li><li>Aktivieren für [Echtzeit-Kundenprofil](../../../profile/home.md)</li><li>Für Profil deaktivieren</li><li>Daten hinzufügen</li><li>Batch löschen</li></ul> |
| [Datenstrom](../../../datastreams/overview.md) | <ul><li>Erstellen</li><li>Update</li><li>Löschen</li><li>Aktivieren</li><li>Deaktivieren</li><li>[Zuordnung bearbeiten](../../../datastreams/data-prep.md)</li></ul> |
| [Datentypen](../../../xdm/schema/composition.md#data-type) | <ul><li>Erstellen</li><li>Update</li><li>Löschen</li></ul> |
| [Ziel](../../../destinations/home.md) | <ul><li>Erstellen</li><li>Update</li><li>Löschen</li><li>Aktivieren</li><li>Deaktivieren</li><li>Datensatzaktivierung</li><li>Datensatzentfernung</li><li>Profilaktivierung</li><li>Profilentfernung</li></ul> |
| [Feldergruppe](../../../xdm/schema/composition.md#field-group) | <ul><li>Erstellen</li><li>Update</li><li>Löschen</li></ul> |
| [Identitätsdiagramm](../../../identity-service/features/identity-graph-viewer.md) | <ul><li>Ansicht</li></ul> |
| [Identity-Namespace](../../../identity-service/features/namespaces.md) | <ul><li>Erstellen</li><li>Update</li></ul> |
| [Zusammenführungsrichtlinie](../../../profile/merge-policies/overview.md) | <ul><li>Erstellen</li><li>Update</li><li>Löschen</li></ul> |
| [Produktprofil](../../../access-control/home.md) | <ul><li>Erstellen</li><li>Update</li><li>Löschen</li></ul> |
| [Abfrage](../../../query-service/ui/overview.md) | <ul><li>Execute</li></ul> |
| [Abfragevorlage](../../../query-service/ui/overview.md) | <ul><li>Erstellen</li><li>Update</li><li>Löschen</li></ul> |
| [Rolle (attributbasierte Zugriffssteuerung)](../../../access-control/home.md) | <ul><li>Erstellen</li><li>Update</li><li>Löschen</li><li>Benutzer hinzufügen</li><li>Benutzer entfernen</li></ul> |
| [Sandbox](../../../sandboxes/home.md) | <ul><li>Erstellen</li><li>Update</li><li>Zurücksetzen</li><li>Löschen</li></ul> |
| [Geplante Abfrage](../../../query-service/ui/overview.md) | <ul><li>Erstellen</li><li>Update</li><li>Löschen</li></ul> |
| [Schema](../../../xdm/schema/composition.md) | <ul><li>Erstellen</li><li>Update</li><li>Löschen</li><li>Für Profile aktivieren</li></ul> |
| [Segment](../../../segmentation/home.md) | <ul><li>Erstellen</li><li>Löschen</li><li>Segmentaktivierung</li><li>Segmententfernung</li></ul> |
| [Source-Datenfluss](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>Erstellen</li><li>Update</li><li>Löschen</li><li>Aktivieren</li><li>Deaktivieren</li><li>Datensatzaktivierung</li><li>Datensatzentfernung</li><li>Profilaktivierung</li><li>Profilentfernung</li></ul> |
| [Arbeitsauftrag](../../../hygiene/home.md) | <ul><li>Erstellen</li></ul> |

## Zugriff auf Auditprotokolle

Wenn die Funktion für Ihr Unternehmen aktiviert ist, werden bei Aktivitäten automatisch Auditprotokolle erfasst. Sie müssen die Datenerfassung in Audit-Protokollen nicht manuell aktivieren.

Um Auditprotokolle anzeigen und exportieren zu können, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Benutzeraktivitätsprotokoll anzeigen]** (in der Kategorie [!UICONTROL Data Governance] ). Informationen zum Verwalten individueller Berechtigungen für Experience Platform-Funktionen finden Sie in der [Dokumentation zur Zugriffssteuerung](../../../access-control/home.md).

## Verwalten von Audit-Protokollen in der Benutzeroberfläche {#managing-audit-logs-in-the-ui}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_instructions"
>title="Anweisungen"
>abstract="<ul><li>Wählen Sie <b>Audits</b> in der linken Navigation aus. Der Arbeitsbereich „Audits“ zeigt eine Liste der aufgezeichneten Protokolle an, die standardmäßig absteigend nach ihrer Aktualität sortiert sind.</li>   <li> HINWEIS: Audit-Protokolle werden 365 Tage lang aufbewahrt und danach aus dem System gelöscht. Daher können Sie nur für einen Zeitraum von maximal 365 Tagen zurückgehen. Wenn Sie auf Daten zurückgreifen müssen, die älter als 365 Tage sind, sollten Sie Protokolle regelmäßig exportieren, um Ihre internen Richtlinienanforderungen zu erfüllen. </li><li>Wählen Sie ein Ereignis aus der Liste aus, um seine Details in der rechten Leiste anzuzeigen. </li><li>Wählen Sie das Trichtersymbol aus, um eine Liste von Filterfeldern anzuzeigen, mit denen die Ergebnisse eingegrenzt werden können. Unabhängig von den ausgewählten Filtern werden nur die letzten 1.000 Einträge angezeigt. </li><li>Um die aktuelle Liste der Audit-Prüfprotokolle zu exportieren, wählen Sie **Protokoll herunterladen** aus.</li><li>Weitere Hilfe zu dieser Funktion finden Sie im Abschnitt <a href="https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/audit-logs/overview.html?lang=de">Übersicht über Audit-Protokolle</a> auf Experience League.</li></ul>"

Sie können Audit-Protokolle für verschiedene Experience Platform-Funktionen im Arbeitsbereich **[!UICONTROL Audits]** in der Experience Platform-Benutzeroberfläche anzeigen. Der Arbeitsbereich zeigt eine Liste der aufgezeichneten Protokolle an, die standardmäßig von der letzten zur letzten sortiert sind.

![Das Audits-Dashboard, in dem Audits im linken Menü hervorgehoben sind.](../../images/audit-logs/audits.png)

Auditprotokolle werden 365 Tage lang aufbewahrt und danach aus dem System gelöscht. Wenn Sie Daten von mehr als 365 Tagen benötigen, sollten Sie Protokolle regelmäßig exportieren, um Ihre internen Richtlinienanforderungen zu erfüllen.

Die Methode zum Anfordern von Auditprotokollen ändert den zulässigen Zeitraum und die Anzahl der Datensätze, auf die Sie Zugriff haben. Mit [Protokolle exportieren](#export-audit-logs) können Sie 365 Tage (in 90-tägigen Intervallen) auf maximal 10.000 Auditprotokolle (entweder Core oder Enhanced) zurückgehen, wobei in der [Aktivitätsprotokoll-](#filter-audit-logs) in Experience Platform die letzten 90 Tage auf maximal 1.000 Hauptereignisse angezeigt werden, von denen jedes mit den entsprechenden erweiterten Ereignissen versehen ist.

Wählen Sie ein Ereignis aus der Liste aus, um seine Details in der rechten Leiste anzuzeigen.

![Registerkarte „Aktivitätsprotokoll“ des Audits-Dashboards mit hervorgehobenem Bereich „Ereignisdetails“.](../../images/audit-logs/select-event.png)

### Auditprotokolle filtern

Wählen Sie das Trichtersymbol (![Filtersymbol](/help/images/icons/filter.png)) aus, um eine Liste von Filterfeldern anzuzeigen, mit denen die Ergebnisse eingegrenzt werden können.

>[!NOTE]
>
>Die Benutzeroberfläche von Experience Platform zeigt nur die letzten 90 Tage bis zu maximal 1.000 Hauptereignisse mit den entsprechenden erweiterten Ereignissen an, unabhängig von den angewendeten Filtern. Wenn Sie Protokolle benötigen, die darüber hinausgehen (bis zu einem Maximum von 365 Tagen), müssen Sie [Ihre Auditprotokolle exportieren](#export-audit-logs).

![Das Audits-Dashboard mit hervorgehobenem gefiltertem Aktivitätsprotokoll.](../../images/audit-logs/filters.png)

Die folgenden Filter sind für Audit-Ereignisse in der Benutzeroberfläche verfügbar:

| Filter | Beschreibung |
| --- | --- |
| [!UICONTROL Kategorie] | Verwenden Sie das Dropdown-Menü, um die angezeigten Ergebnisse nach ([) ](#category) filtern. |
| [!UICONTROL Aktion] | Nach Aktion filtern. Die für jeden Service verfügbaren Aktionen finden Sie in der oben stehenden Ressourcentabelle. |
| [!UICONTROL Benutzer] | Geben Sie die vollständige Benutzer-ID ein (z. B. `johndoe@acme.com`), um nach Benutzer zu filtern. |
| [!UICONTROL Status] | Filtern von Audit-Ereignissen nach Ergebnis: erfolgreich, fehlgeschlagen, zulässig oder verweigert aufgrund fehlender [Zugriffskontrolle](../../../access-control/home.md)-Berechtigungen. Für eine ausgeführte Aktion zeigen die Hauptereignisse [!UICONTROL Zulassen] oder [!UICONTROL Ablehnen]. Wenn das Hauptereignis &quot;[!UICONTROL &quot; &#x200B;], wurden möglicherweise ein oder mehrere erweiterte Ereignisse mit &quot;**[!UICONTROL &quot;]** &quot;**[!UICONTROL &quot;]**. Beispielsweise wird bei einer erfolgreichen Aktion &quot;[!UICONTROL &quot; &#x200B;] Hauptereignis und &quot;[!UICONTROL &quot; &#x200B;] angehängten erweiterten Ereignis angezeigt. |
| [!UICONTROL Datum] | Wählen Sie ein Start- und/oder Enddatum aus, um einen Datumsbereich zu definieren, nach dem die Ergebnisse gefiltert werden sollen. Daten können über einen 90-tägigen Lookback-Zeitraum exportiert werden (z. B. vom 15.12.2021 bis zum 15.03.2022). Dies kann je nach Ereignistyp unterschiedlich sein. |

Um einen Filter zu entfernen, klicken Sie auf das „X“ auf dem Symbol für den betreffenden Filter, oder wählen Sie **[!UICONTROL Alle löschen]** aus, um alle Filter zu entfernen.

![Das Audits-Dashboard mit hervorgehobenem Filter „Löschen“.](../../images/audit-logs/clear-filters.png)

Die zurückgegebenen Auditprotokolldaten enthalten die folgenden Informationen zu allen Abfragen, die Ihren ausgewählten Filterkriterien entsprechen.

| Spaltenname | Beschreibung |
|---|---|
| [!UICONTROL Zeitstempel] | Das genaue Datum und die genaue Uhrzeit der Aktion, die in einem `month/day/year hour:minute AM/PM` Format ausgeführt wird. |
| [!UICONTROL Asset-Name] | Der Wert für das [!UICONTROL Asset-Name]-Feld hängt von der als Filter ausgewählten Kategorie ab. |
| [!UICONTROL Kategorie] | Dieses Feld entspricht der im Filter-Dropdown-Menü ausgewählten Kategorie. |
| [!UICONTROL Aktion] | Die verfügbaren Aktionen hängen von der als Filter ausgewählten Kategorie ab. |
| [!UICONTROL Benutzer] | Dieses Feld gibt die Benutzer-ID an, die die Abfrage ausgeführt hat. |

![Das Audits-Dashboard mit hervorgehobenem gefiltertem Aktivitätsprotokoll.](../../images/audit-logs/filtered.png)

### Auditprotokolle exportieren {#export-audit-logs}

Um die aktuelle Liste der Audit-Prüfprotokolle zu exportieren, wählen Sie **[!UICONTROL Protokoll herunterladen]** aus.

>[!NOTE]
>
>Protokolle können in Intervallen von 90 Tagen bis zu 365 Tagen in der Vergangenheit angefordert werden. Die maximale Anzahl von Protokollen, die während eines einzelnen Exports zurückgegeben werden kann, beträgt jedoch 10.000 Audit-Ereignisse (entweder Core oder Enhanced).

![Das Audits-Dashboard mit hervorgehobenem [!UICONTROL Protokoll herunterladen].](../../images/audit-logs/download.png)

Wählen Sie im angezeigten Dialogfeld Ihr bevorzugtes Format aus (entweder **[!UICONTROL CSV]** oder **[!UICONTROL JSON]**) und klicken Sie dann auf **[!UICONTROL Herunterladen]**. Der Browser lädt die generierte Datei herunter und speichert sie auf Ihrem Computer.

![Das Dialogfeld zur Auswahl des Dateiformats mit hervorgehobener Option [!UICONTROL Herunterladen].](../../images/audit-logs/select-download-format.png)

## Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Audit-Warnhinweise aktivieren, um Benachrichtigungen für die folgenden Regeln zu erhalten:

* Zielgruppe erstellen
* Zielgruppen-Update
* Audience löschen
* Datensatz erstellen
* Datensatzaktualisierung
* Löschen eines Datensatzes
* Schema erstellen
* Schema-Aktualisierung
* Löschen von Schemata

Wählen Sie den gewünschten Warnhinweis aus der Liste, der abonniert werden soll, um Benachrichtigungen zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Warnhinweisen über die Benutzeroberfläche](../../../observability/alerts/ui.md).

## Verwalten von Auditprotokollen in der API

Alle Aktionen, die Sie in der Benutzeroberfläche ausführen können, können auch mithilfe von API-Aufrufen ausgeführt werden. Weitere Informationen finden [ im ](https://www.adobe.io/experience-platform-apis/references/audit-query/)-API-Referenzdokument .

## Verwalten von Auditprotokollen für Adobe Admin Console

Informationen zum Verwalten von Auditprotokollen für Aktivitäten in Adobe Admin Console finden Sie im folgenden [Dokument](https://helpx.adobe.com/de/enterprise/using/audit-logs.html).

## Nächste Schritte und zusätzliche Ressourcen

In diesem Handbuch wurde beschrieben, wie Sie Audit-Protokolle in Experience Platform verwalten. Weitere Informationen zum Überwachen von Experience Platform-Aktivitäten finden Sie in der Dokumentation unter [Observability Insights](../../../observability/home.md) und [Überwachen der Datenaufnahme](../../../ingestion/quality/monitor-data-ingestion.md).

Sehen Sie sich das folgende Video an, um Audit-Protokolle in Experience Platform besser zu verstehen:

>[!VIDEO](https://video.tv.adobe.com/v/341450?quality=12&learn=on)
