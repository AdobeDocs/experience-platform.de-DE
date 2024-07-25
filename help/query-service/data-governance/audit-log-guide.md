---
title: Auditprotokollintegration für Query Service
description: Die Auditprotokolle von Query Service enthalten Aufzeichnungen zu verschiedenen Benutzeraktionen, um ein Audit-Protokoll zur Fehlerbehebung bei Problemen oder zur Einhaltung von Richtlinien zur Unternehmensdatenverwaltung und Regulierungsanforderungen zu erstellen. Dieses Tutorial bietet einen Überblick über die Auditprotokollfunktionen, die speziell für Query Service gelten.
exl-id: 5fdc649f-3aa1-4337-965f-3f733beafe9d
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 8%

---

# [!DNL Query Service] Integration des Auditprotokolls

Die Auditprotokollintegration von Adobe Experience Platform [!DNL Query Service] enthält Datensätze zu abfragebezogenen Benutzeraktionen. Auditprotokolle sind ein wesentliches Tool zur Fehlerbehebung und Einhaltung von Corporate Data Governance-Richtlinien und Regulierungsanforderungen. Mit dieser Funktion können Sie ein Aktionsprotokoll für viele Ereignistypen zurückgeben und die Datensätze filtern und exportieren. Der Zugriff auf die Protokolle erfolgt entweder über die Platform-Benutzeroberfläche oder die [Audit-Abfrage-API](https://www.adobe.io/experience-platform-apis/references/audit-query/) und erfolgt im CSV- oder JSON-Dateiformat.

Weitere Informationen zur Benutzeroberfläche der Prüfprotokolle finden Sie im Dokument [Prüfprotokolle - Übersicht](../../landing/governance-privacy-security/audit-logs/overview.md) . Weitere Informationen zum Aufrufen von Platform-APIs finden Sie im [API-Handbuch für Auditprotokolle](../../landing/api-guide.md).

## Voraussetzungen

Sie müssen über die Berechtigung [!DNL Data Governance] [!UICONTROL Protokoll zur Benutzeraktivität anzeigen] verfügen, um das Audit-Protokoll-Dashboard in der Platform-Benutzeroberfläche anzuzeigen. Die Berechtigung wird über die Adobe [Admin Console](https://adminconsole.adobe.com/) aktiviert. Bitte wenden Sie sich an den Admin Ihrer Organisation, wenn Sie keine Administratorberechtigungen haben, um diese Berechtigung zu aktivieren. In der Dokumentation zur Zugriffskontrolle finden Sie [vollständige Anweisungen zum Hinzufügen von Berechtigungen über die Admin Console](../../access-control/home.md).

## [!DNL Query Service] Audit log categories {#audit-log-categories}

Die von [!DNL Query Service] bereitgestellten Auditprotokollkategorien lauten wie folgt.

| Kategorie | Beschreibung |
|---|---|
| [!UICONTROL Abfrage] | In dieser Kategorie können Sie Abfrageausführungen überprüfen. |
| [!UICONTROL Abfragevorlage] | In dieser Kategorie können Sie die verschiedenen Aktionen (Erstellen, Aktualisieren und Löschen) einer Abfragevorlage überprüfen. |
| [!UICONTROL Geplante Abfrage] | Mit dieser Kategorie können Sie die Zeitpläne überprüfen, die innerhalb von [!DNL Query Service] erstellt, aktualisiert oder gelöscht wurden. |

## Durchführen eines [!DNL Query Service]-Auditprotokolls {#perform-an-audit-log}

Um eine Prüfung für [!DNL Query Service] -Aktivitäten durchzuführen, wählen Sie **[!UICONTROL Audits]** aus der linken Navigation, gefolgt vom Trichtersymbol (![Filtersymbol).](/help/images/icons/filter.png)), um eine Liste von Filtersteuerelementen anzuzeigen, mit deren Hilfe Ergebnisse eingegrenzt werden können.

![Das Auditprotokoll-Dashboard der Platform-Benutzeroberfläche mit &quot;Audits&quot;im linken Navigations- und Filtersteuerelement hervorgehoben.](../images/audit-log/filter-controls.png)

Auf der Registerkarte [!UICONTROL Audits] Dashboard [!UICONTROL Aktivitätsprotokoll] können Sie alle aufgezeichneten Platform-Aktionen nach einer der [!DNL Query Service] Kategorien filtern. Die Protokollergebnisse können nach dem Zeitraum, in dem sie ausgeführt wurden, der ausgeführten Aktion/Funktion oder dem Benutzer, der die Abfrage durchgeführt hat, weiter gefiltert werden. Eine vollständige Anleitung zum Filtern der Protokolle nach Kategorie, Aktion, Benutzer und Status finden Sie in der Dokumentation zum Auditprotokoll [ .](../../landing/governance-privacy-security/audit-logs/overview.md#managing-audit-logs-in-the-ui)

Die zurückgegebenen Auditprotokolldaten enthalten die folgenden Informationen zu allen Abfragen, die Ihre ausgewählten Filterkriterien erfüllen.

| Spaltenname | Beschreibung |
|---|---|
| [!UICONTROL Zeitstempel] | Das genaue Datum und die Uhrzeit der im Format `month/day/year hour:minute AM/PM` durchgeführten Aktion. |
| [!UICONTROL Asset-Name] | Der Wert für das Feld [!UICONTROL Asset-Name] hängt von der Kategorie ab, die als Filter ausgewählt wurde. Bei Verwendung der Kategorie [!UICONTROL Geplante Abfrage] ist dies der **Planungsname**. Bei Verwendung der Kategorie [!UICONTROL Abfragevorlage] ist dies der **Vorlagenname**. Bei Verwendung der Kategorie [!UICONTROL Abfrage] ist dies die **Sitzungs-ID** |
| [!UICONTROL Kategorie] | Dieses Feld entspricht der von Ihnen im Filter -Dropdown-Menü ausgewählten Kategorie. |
| [!UICONTROL Aktion] | Dies kann entweder erstellt, gelöscht, aktualisiert oder ausgeführt werden. Die verfügbaren Aktionen hängen von der als Filter ausgewählten Kategorie ab. |
| [!UICONTROL Benutzer] | Dieses Feld enthält die Benutzer-ID, die die Abfrage ausgeführt hat. |

![Das Dashboard &quot;Prüfungen&quot;mit dem gefilterten Aktivitätsprotokoll ist hervorgehoben.](../images/audit-log/filtered-activity.png)

>[!NOTE]
>
>Durch das Herunterladen der Protokollergebnisse im CSV- oder JSON-Dateiformat werden mehr Abfragedetails bereitgestellt als standardmäßig im Dashboard des Auditprotokolls angezeigt.

## Detailbereich

Wählen Sie eine beliebige Zeile mit Auditprotokollergebnissen aus, um einen Detailbereich rechts vom Bildschirm zu öffnen.

![Audits Dashboard-Aktivitätsprotokoll , wobei der Detailbereich hervorgehoben ist.](../images/audit-log/details-panel.png)

Im Detailbereich können Sie die [!UICONTROL Asset-ID] und den [!UICONTROL Ereignisstatus] finden.

Der Wert der [!UICONTROL Asset-ID] ändert sich je nach der bei der Prüfung verwendeten Kategorie.

* Bei Verwendung der Kategorie [!UICONTROL Abfrage] ist die [!UICONTROL Asset-ID] die **Sitzungs-ID**.
* Bei Verwendung der Kategorie [!UICONTROL Abfragevorlage] entspricht die [!UICONTROL Asset-ID] der **Vorlagen-ID** und dem Präfix `[!UICONTROL templateID:]`.
* Bei Verwendung der Kategorie [!UICONTROL Geplante Abfrage] ist die [!UICONTROL Asset-ID] die **Zeitplan-ID** und hat das Präfix `[!UICONTROL scheduleID:]`.

Der Wert des [!UICONTROL Ereignisstatus] ändert sich je nach der in der Prüfung verwendeten Kategorie.

* Bei Verwendung der Kategorie [!UICONTROL Abfrage] stellt das Feld [!UICONTROL Ereignisstatus] eine Liste aller vom Benutzer innerhalb dieser Sitzung ausgeführten **Abfrage-IDs** bereit.
* Bei Verwendung der Kategorie [!UICONTROL Abfragevorlage] stellt das Feld [!UICONTROL Ereignisstatus] den **Vorlagennamen** als Präfix für den Ereignisstatus bereit.
* Bei Verwendung der Kategorie [!UICONTROL Abfrageplan] stellt das Feld [!UICONTROL Ereignisstatus] den **Planungsnamen** als Präfix für den Ereignisstatus bereit.

## Verfügbare Filter für [!DNL Query Service] Auditprotokollkategorien {#available-filters}

Die verfügbaren Filter variieren je nach der im Dropdown-Menü ausgewählten Kategorie. In der folgenden Tabelle werden die für [[!DNL Query Service] Prüfprotokollkategorien](#audit-log-categories) verfügbaren Filter aufgeführt.

| Filter | Beschreibung |
|---|---|
| Kategorie | Eine vollständige Liste der verfügbaren Kategorien finden Sie im Abschnitt [[!DNL Query Service] Auditprotokollkategorien](#audit-log-categories) . |
| Aktion | Wenn Sie auf [!DNL Query Service] Prüfkategorien verweisen, ist &quot;Aktualisieren&quot;eine **Änderung am vorhandenen Formular**, &quot;Löschen&quot;ist die **Entfernung des Zeitplans oder der Vorlage**, &quot;Erstellen&quot;ist **Erstellen eines neuen Zeitplans oder einer neuen Vorlage** und &quot;Ausführen&quot;ist **Ausführen einer Abfrage**. |
| Benutzer | Geben Sie die vollständige Benutzer-ID ein (z. B. johndoe@acme.com), um nach Benutzer zu filtern. |
| Status | Die Optionen [!UICONTROL Zulassen], [!UICONTROL Erfolg] und [!UICONTROL Fehler] filtern die Protokolle nach &quot;Status&quot;oder &quot;Ereignisstatus&quot;, während die Option [!UICONTROL Ablehnen] die **alle** Protokolle herausfiltert. |
| Datum | Wählen Sie ein Startdatum und/oder ein Enddatum aus, um einen Datumsbereich zu definieren, nach dem die Ergebnisse gefiltert werden sollen. |

## Nächste Schritte

Durch Lesen dieses Dokuments erhalten Sie ein besseres Verständnis der [!DNL Query Service]-Auditprotokollfunktion und der Verwendung dieser Funktion zum Filtern Ihrer [!DNL Query Service]-Benutzeraktionen.

Wenn Sie die Funktion [!DNL Query Service] des Auditprotokolls zur Fehlerbehebung verwenden, sollten Sie das [Handbuch zur Fehlerbehebung](../troubleshooting-guide.md) lesen.
