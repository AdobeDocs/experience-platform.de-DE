---
title: Integration des Administratorprotokolls in Query Service
description: In den Audit-Protokollen des Abfrage-Service werden Datensätze für verschiedene Benutzeraktionen gespeichert, um ein Audit-Protokoll zur Fehlerbehebung bei Problemen oder zur Einhaltung von Unternehmensrichtlinien für die Datenverwaltung und gesetzlichen Anforderungen zu bilden. Dieses Tutorial bietet einen Überblick über die Administratorprotokoll-Funktionen, die für den Abfrage-Service spezifisch sind.
exl-id: 5fdc649f-3aa1-4337-965f-3f733beafe9d
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 8%

---

# Integration [!DNL Query Service] Auditprotokolls

Die Integration des Administratorprotokolls in Adobe Experience Platform [!DNL Query Service] stellt Datensätze zu abfragebezogenen Benutzeraktionen bereit. Audit-Protokolle sind ein wichtiges Tool zur Fehlerbehebung und zur Einhaltung von Unternehmensrichtlinien für die Datenverwaltung und gesetzlichen Anforderungen. Mit der Funktion können Sie ein Aktionsprotokoll für viele Ereignistypen zurückgeben und die Datensätze filtern und exportieren. Auf die Protokolle kann entweder über die Platform-Benutzeroberfläche oder die [Audit-Abfrage-API](https://www.adobe.io/experience-platform-apis/references/audit-query/) zugegriffen und sie in CSV- oder JSON-Dateiformaten heruntergeladen werden.

Weitere Informationen zur Benutzeroberfläche für Auditprotokolle finden Sie im Dokument [Übersicht über Auditprotokolle](../../landing/governance-privacy-security/audit-logs/overview.md). Weitere Informationen zum Aufrufen von Platform-APIs finden Sie im [Handbuch zur Audit-Protokoll-API](../../landing/api-guide.md).

## Voraussetzungen

Die Berechtigung [!DNL Data Governance]Benutzeraktivitätsprotokoll anzeigen[!UICONTROL  muss aktiviert ], damit das Administratorprotokoll-Dashboard in der Platform-Benutzeroberfläche angezeigt werden kann. Die Berechtigung wird über die Adobe [Admin Console](https://adminconsole.adobe.com/) aktiviert. Bitte wenden Sie sich an den Admin Ihrer Organisation, wenn Sie keine Administratorberechtigungen haben, um diese Berechtigung zu aktivieren. In der Dokumentation zur Zugriffskontrolle finden Sie [vollständige Anweisungen zum Hinzufügen von Berechtigungen über die Admin Console](../../access-control/home.md).

## [!DNL Query Service] Auditprotokollkategorien {#audit-log-categories}

Die von [!DNL Query Service] bereitgestellten Auditprotokollkategorien lauten wie folgt.

| Kategorie | Beschreibung |
|---|---|
| [!UICONTROL Abfrage] | Mit dieser Kategorie können Sie Abfrageausführungen überprüfen. |
| [!UICONTROL Abfragevorlage] | In dieser Kategorie können Sie die verschiedenen Aktionen (Erstellen, Aktualisieren und Löschen) prüfen, die bei einer Abfragevorlage durchgeführt wurden. |
| [!UICONTROL Geplante Abfrage] | Mit dieser Kategorie können Sie die Zeitpläne prüfen, die in [!DNL Query Service] erstellt, aktualisiert oder gelöscht wurden. |

## Durchführen eines [!DNL Query Service] Auditprotokolls {#perform-an-audit-log}

Um eine Prüfung für [!DNL Query Service] Aktivitäten durchzuführen, wählen Sie **[!UICONTROL Prüfungen]** im linken Navigationsbereich aus, gefolgt vom Trichtersymbol (![Filtersymbol).](/help/images/icons/filter.png)), um eine Liste von Filterfeldern anzuzeigen, mit denen die Ergebnisse eingegrenzt werden können.

![Das Dashboard des Administratorprotokolls der Platform-Benutzeroberfläche mit hervorgehobenen Steuerelementen „Prüfungen“ im linken Navigationsbereich und hervorgehobenen Filterfeldern.](../images/audit-log/filter-controls.png)

Über die Registerkarte [!UICONTROL Audits]-Dashboard [!UICONTROL Aktivitätsprotokoll] können Sie alle aufgezeichneten Platform-Aktionen nach einer der [!DNL Query Service] Kategorien filtern. Die Protokollergebnisse können weiter gefiltert werden, basierend auf dem Zeitraum, in dem sie ausgeführt wurden, der durchgeführten Aktion/Funktion oder dem Benutzer, der die Abfrage durchgeführt hat. Siehe die Dokumentation zum Auditprotokoll für [vollständige Anweisungen zum Filtern der Protokolle nach Kategorie, Aktion, Benutzer und Status](../../landing/governance-privacy-security/audit-logs/overview.md#managing-audit-logs-in-the-ui).

Die zurückgegebenen Auditprotokolldaten enthalten die folgenden Informationen zu allen Abfragen, die Ihren ausgewählten Filterkriterien entsprechen.

| Spaltenname | Beschreibung |
|---|---|
| [!UICONTROL Zeitstempel] | Das genaue Datum und die genaue Uhrzeit der Aktion, die in einem `month/day/year hour:minute AM/PM` Format ausgeführt wird. |
| [!UICONTROL Asset-Name] | Der Wert für das [!UICONTROL Asset-Name]-Feld hängt von der als Filter ausgewählten Kategorie ab. Bei Verwendung der Kategorie [!UICONTROL Geplante Abfrage] ist dies der **Name des Zeitplans**. Bei Verwendung der Kategorie [!UICONTROL Abfragevorlage] ist dies der **Vorlagenname**. Bei Verwendung der Kategorie [!UICONTROL Abfrage] ist dies die **Sitzungs-ID** |
| [!UICONTROL Kategorie] | Dieses Feld entspricht der Kategorie, die Sie im Filter-Dropdown-Menü ausgewählt haben. |
| [!UICONTROL Aktion] | Dies kann entweder erstellt, gelöscht, aktualisiert oder ausgeführt werden. Die verfügbaren Aktionen hängen von der als Filter ausgewählten Kategorie ab. |
| [!UICONTROL Benutzer] | Dieses Feld gibt die Benutzer-ID an, die die Abfrage ausgeführt hat. |

![Das Audits-Dashboard mit hervorgehobenem gefiltertem Aktivitätsprotokoll.](../images/audit-log/filtered-activity.png)

>[!NOTE]
>
>Durch Herunterladen der Protokollergebnisse in CSV- oder JSON-Dateiformaten werden mehr Abfragedetails bereitgestellt, als standardmäßig im Administratorprotokoll-Dashboard angezeigt werden.

## Detailfenster

Wählen Sie eine beliebige Zeile mit Auditprotokollergebnissen aus, um einen Detailbereich rechts neben dem Bildschirm zu öffnen.

![Registerkarte „Aktivitätsprotokoll“ des Audits-Dashboards mit hervorgehobenem Detailbereich.](../images/audit-log/details-panel.png)

Das Detailbedienfeld kann verwendet werden, um die [!UICONTROL Asset-ID] und den [!UICONTROL Ereignisstatus] zu finden.

Der Wert der [!UICONTROL Asset-ID] ändert sich je nach der beim Audit verwendeten Kategorie.

* Bei Verwendung der Kategorie [!UICONTROL Abfrage] ist [!UICONTROL Asset-ID] die **Sitzungs-ID**.
* Bei Verwendung der Kategorie [!UICONTROL Abfragevorlage] ist die [!UICONTROL Asset-ID] die **Vorlagen-ID** und mit dem Präfix `[!UICONTROL templateID:]`.
* Bei Verwendung der Kategorie [!UICONTROL Geplante Abfrage] ist die [!UICONTROL Asset-ID] die **Zeitplan-ID** und mit dem Präfix `[!UICONTROL scheduleID:]`.

Der Wert von [!UICONTROL Ereignisstatus] ändert sich je nach der beim Audit verwendeten Kategorie.

* Bei Verwendung der Kategorie [!UICONTROL Abfrage] liefert das Feld [!UICONTROL Ereignisstatus] eine Liste aller **Abfrage-IDs**, die der Benutzer in dieser Sitzung ausgeführt hat.
* Bei Verwendung der Kategorie [!UICONTROL Abfragevorlage] liefert das Feld [!UICONTROL Ereignisstatus] den **Vorlagennamen** als Präfix für den Ereignisstatus.
* Bei Verwendung der Kategorie [!UICONTROL Abfragezeitplan] liefert das Feld [!UICONTROL Ereignisstatus] den **Zeitplannamen** als Präfix für den Ereignisstatus.

## Verfügbare Filter für [!DNL Query Service] Administratorprotokoll-Kategorien {#available-filters}

Die verfügbaren Filter variieren je nach der im Dropdown-Menü ausgewählten Kategorie. In der folgenden Tabelle sind die Filter aufgeführt, die für [[!DNL Query Service] Auditprotokollkategorien“ verfügbar ](#audit-log-categories).

| Filter | Beschreibung |
|---|---|
| Kategorie | Eine vollständige Liste [[!DNL Query Service]  verfügbaren Kategorien finden Sie ](#audit-log-categories) Abschnitt „Auditprotokollkategorien“. |
| Aktion | Wenn Sie sich auf [!DNL Query Service] Auditkategorien beziehen, handelt es sich bei der Aktualisierung um **Änderung am vorhandenen Formular**, beim Löschen **Entfernen des Zeitplans oder der**), beim Erstellen **Erstellen eines neuen Zeitplans oder einer neuen Vorlage** und beim Ausführen **eine Abfrage**. |
| Benutzer | Geben Sie die vollständige Benutzer-ID ein (z. B. johndoe@acme.com), um nach Benutzer zu filtern. |
| Status | Die Optionen [!UICONTROL Zulassen], [!UICONTROL Erfolg] und [!UICONTROL Fehler] filtern die Protokolle auf der Grundlage des „Status“ oder „Ereignisstatus“, während die Option [!UICONTROL Ablehnen] **alle**-Protokolle herausfiltert. |
| Datum | Wählen Sie ein Startdatum und/oder ein Enddatum aus, um einen Datumsbereich zu definieren, nach dem die Ergebnisse gefiltert werden sollen. |

## Nächste Schritte

Durch dieses Dokument erhalten Sie ein besseres Verständnis der Funktion des [!DNL Query Service]-Administratorprotokolls und dessen Verwendung zum Filtern Ihrer [!DNL Query Service] Benutzeraktionen.

Wenn Sie die [!DNL Query Service] Auditprotokollfunktion zur Fehlerbehebung verwenden, wird empfohlen, das [Handbuch zur Fehlerbehebung](../troubleshooting-guide.md) zu lesen.
