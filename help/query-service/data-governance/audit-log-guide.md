---
title: Auditprotokollintegration für Query Service
description: Die Auditprotokolle von Query Service enthalten Aufzeichnungen zu verschiedenen Benutzeraktionen, um ein Audit-Protokoll zur Fehlerbehebung bei Problemen oder zur Einhaltung von Richtlinien zur Unternehmensdatenverwaltung und Regulierungsanforderungen zu erstellen. Dieses Tutorial bietet einen Überblick über die Auditprotokollfunktionen, die speziell für Query Service gelten.
exl-id: 5fdc649f-3aa1-4337-965f-3f733beafe9d
source-git-commit: 40de87ae407884d4ec7c75215fc7319721fbe1d0
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 2%

---

# [!DNL Query Service] Auditprotokollintegration

Die Adobe Experience Platform [!DNL Query Service] Die Integration von Auditprotokollen liefert Datensätze zu abfragenbezogenen Benutzeraktionen. Auditprotokolle sind ein wesentliches Tool zur Fehlerbehebung und Einhaltung von Corporate Data Governance-Richtlinien und Regulierungsanforderungen. Mit dieser Funktion können Sie ein Aktionsprotokoll für viele Ereignistypen zurückgeben und die Datensätze filtern und exportieren. Die Protokolle können entweder über die Platform-Benutzeroberfläche oder die [Audit Query API](https://www.adobe.io/experience-platform-apis/references/audit-query/) und im CSV- oder JSON-Dateiformat heruntergeladen wurden.

Weitere Informationen zur Benutzeroberfläche der Prüfprotokolle finden Sie im Abschnitt [Audit logs - Überblick](../../landing/governance-privacy-security/audit-logs/overview.md). Weiterführende Informationen zum Aufrufen von Platform-APIs finden Sie im Abschnitt [API-Handbuch zu Auditprotokollen](../../landing/api-guide.md).

## Voraussetzungen

Sie müssen über die [!DNL Data Governance] [!UICONTROL Protokoll zu Benutzeraktivitäten anzeigen] -Berechtigung zum Anzeigen des Auditprotokoll-Dashboards in der Platform-Benutzeroberfläche aktiviert. Die Berechtigung wird über die Adobe aktiviert [Admin Console](https://adminconsole.adobe.com/). Wenden Sie sich an den Administrator Ihrer Organisation, wenn Sie keine Administratorberechtigungen haben, um diese Berechtigung zu aktivieren. Weitere Informationen finden Sie in der Dokumentation zur Zugriffskontrolle für [Vollständige Anweisungen zum Hinzufügen von Berechtigungen über die Admin Console](../../access-control/home.md).

## [!DNL Query Service] Prüfprotokollkategorien {#audit-log-categories}

Die von [!DNL Query Service] sind wie folgt.

| Kategorie | Beschreibung |
|---|---|
| [!UICONTROL Abfrage] | In dieser Kategorie können Sie Abfrageausführungen überprüfen. |
| [!UICONTROL Abfragevorlage] | In dieser Kategorie können Sie die verschiedenen Aktionen (Erstellen, Aktualisieren und Löschen) einer Abfragevorlage überprüfen. |
| [!UICONTROL Geplante Abfrage] | In dieser Kategorie können Sie die Zeitpläne überprüfen, die in [!DNL Query Service]. |

## Führen Sie eine [!DNL Query Service] Auditprotokoll {#perform-an-audit-log}

So führen Sie eine Prüfung für [!DNL Query Service] Aktivitäten, wählen Sie **[!UICONTROL Prüfungen]** aus der linken Navigation, gefolgt vom Trichtersymbol (![Ein Filtersymbol.](../images/audit-log/filter.png)), um eine Liste von Filtersteuerelementen anzuzeigen, die die Eingrenzung der Ergebnisse unterstützen.

![Das Auditprotokoll-Dashboard der Platform-Benutzeroberfläche mit &quot;Audits&quot;im linken Navigations- und Filtersteuerelement markiert.](../images/audit-log/filter-controls.png)

Aus dem [!UICONTROL Prüfungen] Dashboard [!UICONTROL Aktivitätsprotokoll] auf, können Sie alle aufgezeichneten Platform-Aktionen nach einem der [!DNL Query Service] Kategorien. Die Protokollergebnisse können nach dem Zeitraum, in dem sie ausgeführt wurden, der ausgeführten Aktion/Funktion oder dem Benutzer, der die Abfrage durchgeführt hat, weiter gefiltert werden. Weitere Informationen finden Sie in der Dokumentation zum Auditprotokoll für [Vollständige Anweisungen zum Filtern der Protokolle nach Kategorie, Aktion, Benutzer und Status](../../landing/governance-privacy-security/audit-logs/overview.md#managing-audit-logs-in-the-ui).

Die zurückgegebenen Auditprotokolldaten enthalten die folgenden Informationen zu allen Abfragen, die Ihre ausgewählten Filterkriterien erfüllen.

| Spaltenname | Beschreibung |
|---|---|
| [!UICONTROL Zeitstempel] | Datum und Uhrzeit der in einem `month/day/year hour:minute AM/PM` Format. |
| [!UICONTROL Asset-Name] | Der Wert für [!UICONTROL Asset-Name] -Feld hängt von der als Filter ausgewählten Kategorie ab. Bei Verwendung von [!UICONTROL Geplante Abfrage] -Kategorie, die dies ist **Planungsname**. Bei Verwendung von [!UICONTROL Abfragevorlage] -Kategorie, ist dies die **Vorlagenname**. Bei Verwendung von [!UICONTROL Abfrage] -Kategorie, ist dies die **session ID** |
| [!UICONTROL Kategorie] | Dieses Feld entspricht der von Ihnen im Filter -Dropdown-Menü ausgewählten Kategorie. |
| [!UICONTROL Aktion] | Dies kann entweder erstellt, gelöscht, aktualisiert oder ausgeführt werden. Die verfügbaren Aktionen hängen von der als Filter ausgewählten Kategorie ab. |
| [!UICONTROL Benutzer] | Dieses Feld enthält die Benutzer-ID, die die Abfrage ausgeführt hat. |

![Das Dashboard &quot;Prüfungen&quot;mit dem gefilterten Aktivitätsprotokoll wird hervorgehoben.](../images/audit-log/filtered-activity.png)

>[!NOTE]
>
>Durch das Herunterladen der Protokollergebnisse im CSV- oder JSON-Dateiformat werden mehr Abfragedetails bereitgestellt als standardmäßig im Dashboard des Auditprotokolls angezeigt.

## Detailbereich

Wählen Sie eine beliebige Zeile mit Auditprotokollergebnissen aus, um einen Detailbereich rechts vom Bildschirm zu öffnen.

![Registerkarte &quot;Protokoll der Dashboard-Aktivität&quot;mit dem Detailbereich hervorgehoben.](../images/audit-log/details-panel.png)

Im Detailbereich können Sie die [!UICONTROL Asset-ID] und [!UICONTROL Ereignisstatus].

Der Wert der [!UICONTROL Asset-ID] ändert sich je nach der in der Prüfung verwendeten Kategorie.

* Bei Verwendung von [!UICONTROL Abfrage] Kategorie, [!UICONTROL Asset-ID] ist die  **session ID**.
* Bei Verwendung von [!UICONTROL Abfragevorlage] Kategorie, [!UICONTROL Asset-ID] ist die **template ID** und mit dem Präfix `[!UICONTROL templateID:]`.
* Bei Verwendung von [!UICONTROL Geplante Abfrage] Kategorie, [!UICONTROL Asset-ID] ist die  **Zeitplan-ID** und mit dem Präfix `[!UICONTROL scheduleID:]`.

Der Wert der [!UICONTROL Ereignisstatus] ändert sich je nach der in der Prüfung verwendeten Kategorie.

* Bei Verwendung von [!UICONTROL Abfrage] Kategorie, [!UICONTROL Ereignisstatus] enthält eine Liste aller **Abfrage-IDs** vom Benutzer innerhalb dieser Sitzung ausgeführt werden.
* Bei Verwendung von [!UICONTROL Abfragevorlage] Kategorie, [!UICONTROL Ereignisstatus] -Feld bietet die **Vorlagenname** als Präfix für den Ereignisstatus.
* Bei Verwendung von [!UICONTROL Abfrageplan] Kategorie, [!UICONTROL Ereignisstatus] -Feld bietet die **Planungsname** als Präfix für den Ereignisstatus.

## Verfügbare Filter für [!DNL Query Service] Prüfprotokollkategorien {#available-filters}

Die verfügbaren Filter variieren je nach der im Dropdown-Menü ausgewählten Kategorie. In der folgenden Tabelle werden die für [[!DNL Query Service] Prüfprotokollkategorien](#audit-log-categories).

| Filter | Beschreibung |
|---|---|
| Kategorie | Siehe [[!DNL Query Service] Prüfprotokollkategorien](#audit-log-categories) für eine vollständige Liste der verfügbaren Kategorien. |
| Aktion | Wenn auf [!DNL Query Service] Audit-Kategorien, Aktualisierung ist eine **Änderung am vorhandenen Formular**, ist Löschen der Wert **Entfernung des Zeitplans oder der Vorlage**, erstellen ist **Erstellen eines neuen Zeitplans oder einer neuen Vorlage**, und die Ausführung lautet **Ausführen einer Abfrage**. |
| Benutzer | Geben Sie die vollständige Benutzer-ID ein (z. B. johndoe@acme.com), um nach Benutzer zu filtern. |
| Status | Die [!UICONTROL Zulassen], [!UICONTROL Erfolg]und [!UICONTROL Fehlgeschlagen] -Optionen filtern die Protokolle nach &quot;Status&quot;oder &quot;Ereignisstatus&quot;, während die [!UICONTROL Ablehnen] Option wird ausgefiltert **all** Protokolle. |
| Datum | Wählen Sie ein Startdatum und/oder ein Enddatum aus, um einen Datumsbereich zu definieren, nach dem die Ergebnisse gefiltert werden sollen. |

## Nächste Schritte

Durch Lesen dieses Dokuments erhalten Sie ein besseres Verständnis für die [!DNL Query Service] Auditprotokollfunktion und wie sie zum Filtern Ihrer [!DNL Query Service] Benutzeraktionen.

Wenn Sie die [!DNL Query Service] Auditprotokollfunktion zur Fehlerbehebung wird empfohlen, die [Handbuch zur Fehlerbehebung](../troubleshooting-guide.md).
