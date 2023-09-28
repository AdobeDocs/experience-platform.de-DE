---
title: Abfrageprotokolle
description: Abfrageprotokolle werden automatisch bei jeder Ausführung einer Abfrage generiert und stehen über die Benutzeroberfläche zur Verfügung, um die Fehlerbehebung zu unterstützen. In diesem Dokument wird beschrieben, wie Sie den Abschnitt "Query Service Logs"der Benutzeroberfläche verwenden und darin navigieren.
exl-id: 929e9fba-a9ba-4bf9-a363-ca8657a84f75
source-git-commit: 88498a1382202bed057b8dc52d09359ba02748ea
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 3%

---

# Abfrageprotokolle

>[!IMPORTANT]
>
>Bestimmte Abfrageprotokollfunktionen sind derzeit in einer eingeschränkten Version verfügbar und stehen nicht allen Kunden zur Verfügung. Ihre Benutzeroberfläche wird möglicherweise ohne Bearbeitungssymbol etwas anders angezeigt. Außerdem kann die Auswahl eines Abfragenamens dazu führen, dass anstelle von [!UICONTROL Details zum Abfrage-Protokoll] anzeigen.

Adobe Experience Platform verwaltet ein Protokoll aller Abfrageereignisse, die sowohl über die API als auch über die Benutzeroberfläche auftreten. Diese Informationen sind in der Query Service-Benutzeroberfläche über die [!UICONTROL Protokolle] Registerkarte.

Die Protokolldateien werden automatisch von jedem Abfrageereignis generiert und enthalten Informationen wie die verwendete SQL-Datei, den Status der Abfrage, die Dauer und die letzte Laufzeit. Sie können Abfrageprotokolldaten als leistungsstarkes Tool zur Fehlerbehebung bei ineffizienten oder problematischen Abfragen verwenden. Umfassendere Protokollinformationen werden im Rahmen der Funktion zum Auditprotokoll gespeichert und sind im Abschnitt [Auditprotokolldokumentation](../../landing/governance-privacy-security/audit-logs/overview.md).

## Abfrage-Logs überprüfen

Um die Abfrageprotokolle zu überprüfen, wählen Sie [!UICONTROL Abfragen] Navigieren Sie zum Arbeitsbereich &quot;Query Service&quot;und wählen Sie [!UICONTROL Protokoll] aus den verfügbaren Optionen.

![Die Platform-Benutzeroberfläche mit hervorgehobenen Abfragen und Protokollen.](../images/ui/query-log/logs.png)

## Anpassen und Suchen {#customize-and-search}

Die Query Service-Logs werden in einem anpassbaren Tabellenformat dargestellt. Um die Tabellenspalten anzupassen, wählen Sie das Einstellungssymbol (![Ein Einstellungssymbol.](../images/ui/query-log/settings-icon.png)) rechts vom Bildschirm. A [!UICONTROL Tabelle anpassen] angezeigt, in dem die Auswahl der einzelnen Spalten aufgehoben werden kann.

Sie können auch nach Protokollen suchen, die sich auf bestimmte Abfragevorlagen beziehen, indem Sie den Vorlagennamen in das Suchfeld eingeben.

![Der Arbeitsbereich &quot;Abfrageprotokoll&quot;mit der Suchleiste und dem Dropdown-Menü zur Spaltenverwaltung wurde hervorgehoben.](../images/ui/query-log/customize-logs.png)

A [Beschreibung der einzelnen Protokolltabellenspalten](./overview.md#log) finden Sie in der Query Service-Übersicht im Abschnitt Protokoll .

## Ermitteln von Protokolldaten

Jede Zeile stellt Protokolldaten für eine Abfrageausführung dar, die mit einer Abfragevorlage verknüpft ist. Wählen Sie eine beliebige Zeile aus der Tabelle aus, um die rechte Seitenleiste mit Protokolldaten für diese Ausführung zu füllen.

![Der Arbeitsbereich &quot;Abfrage-Protokoll&quot;mit einer ausgewählten Zeile und die Protokolldaten in der rechten Seitenleiste wurden hervorgehoben.](../images/ui/query-log/log-details.png)

Im Bereich &quot;Protokolldetails&quot;können Sie einen neuen Ausgabedatensatz auswählen und die vollständige SQL-Abfrage, die in der Ausführung verwendet wurde, anzeigen oder kopieren.

![Der Arbeitsbereich &quot;Abfrage-Protokoll&quot;mit einer ausgewählten Zeile und der Ausgabedatensatz und die SQL-Abfrage hervorgehoben.](../images/ui/query-log/edit-output-dataset.png)

>[!IMPORTANT]
>
>Bestimmte Abfrageprotokollfunktionen sind derzeit in einer eingeschränkten Version verfügbar und stehen nicht allen Kunden zur Verfügung.

Sie können auch einen Namen für eine Abfragevorlage aus dem [!UICONTROL Name] -Spalte, um direkt zur [!UICONTROL Details zum Abfrage-Protokoll] anzeigen.

>[!NOTE]
>
>Wenn die Abfrage mit der API erstellt wurde und während der Initialisierung kein Vorlagenname angegeben wurde, werden stattdessen die ersten Dutzend Zeichen der SQL-Abfrage angezeigt.

![Die Detailansicht des Abfrageprotokolls.](../images/ui/query-log/query-log-details.png)

## Protokolle bearbeiten {#edit-logs}

Neben dem Vorlagennamen jeder Zeile oder einem SQL-Snippet befindet sich ein Stiftsymbol (![Ein Bleistiftsymbol.](../images/ui/query-log/edit-icon.png)), mit denen Sie zum Abfrage-Editor navigieren können. Die Abfrage wird dann im Editor zur Bearbeitung vorausgefüllt.

![Der Arbeitsbereich &quot;Abfrage-Protokoll&quot;mit einem hervorgehobenen Stiftsymbol.](../images/ui/query-log/edit-query.png)

## Filter-Logs {#filter-logs}

Sie können die Liste der Abfrageprotokolle anhand verschiedener Einstellungen filtern. Wählen Sie das Filtersymbol (![Das Filtersymbol.](../images/ui/query-log/filter-icon.png)) oben links im Arbeitsbereich, um eine Reihe von Filteroptionen in der linken Leiste zu öffnen.

![Der Arbeitsbereich &quot;Abfrage-Protokoll&quot;mit hervorgehobenem Filtersymbol.](../images/ui/query-log/log-filter.png)

Die Liste der verfügbaren Filter wird angezeigt.

![Der Arbeitsbereich &quot;Abfrage-Protokoll&quot;mit den angezeigten und hervorgehobenen Filteroptionen.](../images/ui/query-log/log-filter-settings.png)

Die folgende Tabelle enthält eine Beschreibung der einzelnen Filter.

| Filter | Beschreibung |
| ------ | ----------- |
| [!UICONTROL Dashboard-Abfragen ausschließen] | Dieses Kontrollkästchen ist standardmäßig aktiviert und schließt Protokolle aus, die von den Abfragen generiert wurden, mit denen Einblicke generiert wurden. Diese Abfragen werden systemgeneriert und verschleiern die Datensätze von benutzergenerierten Protokollen, die zur Überwachung, Verwaltung und Fehlerbehebung erforderlich sind. Um vom System generierte Protokolle anzuzeigen, deaktivieren Sie das Kontrollkästchen. |
| [!UICONTROL Startdatum] | Um die Protokolle nach Abfragen zu filtern, die in einem bestimmten Zeitraum erstellt wurden, legen Sie die [!UICONTROL Starten] und [!UICONTROL Ende] Daten in [!UICONTROL Startdatum] Abschnitt. |
| [!UICONTROL Abgeschlossenes Datum] | Um die Protokolle nach Abfragen zu filtern, die in einem bestimmten Zeitraum abgeschlossen wurden, legen Sie die [!UICONTROL Starten] und [!UICONTROL Ende] Daten in [!UICONTROL Abgeschlossenes Datum] Abschnitt. |
| [!UICONTROL Status] | So filtern Sie die Protokolle nach [!UICONTROL Status] Wählen Sie das entsprechende Optionsfeld aus. Zu den verfügbaren Optionen gehören [!UICONTROL Gesendet], [!UICONTROL Gestartet], [!UICONTROL Erfolg], und [!UICONTROL Fehlgeschlagen]. Sie können Protokolle nur nach einer Statusbedingung filtern. |
| [!UICONTROL Client] | Um die Logs nach dem verwendeten Abfrageclient zu filtern, geben Sie einen der folgenden zulässigen Werte in das Feld für den freien Text ein: `API`, `Adobe Query Service UI`oder `QsAccel`. |
| [!UICONTROL Meine Abfragen] | Verwenden Sie die [!UICONTROL Meine Abfragen] umschalten, um die Protokolle nach von Ihnen ausgeführten Abfragen zu filtern. |
| [!UICONTROL Abfragelog-ID] | Um nach der eindeutigen Logkennung einer Abfrage zu filtern, geben Sie die Logkennung in das Feld für den freien Text ein. Diese Informationen finden Sie im Abschnitt [!UICONTROL Protokolldetails]. |

Alle angewendeten Filter werden oberhalb der gefilterten Protokollergebnisse angezeigt.

![Die Registerkarte Protokoll im Arbeitsbereich Abfragen , wobei die Liste der angewendeten Filter hervorgehoben ist.](../images/ui/query-log/applied-log-filters.png)

## Nächste Schritte

Durch Lesen dieses Dokuments können Sie jetzt besser verstehen, wie auf Abfrageprotokolle in der Benutzeroberfläche von Query Service zugegriffen und diese verwendet werden.

Weitere Informationen über die Funktionen des Abfrage-Services finden Sie in der [Benutzeroberflächen-Übersicht](./overview.md) oder im [Handbuch zur Abfrage-Service-API](../api/getting-started.md).

Siehe [Überwachungsabfragendokument](./monitor-queries.md) , um zu erfahren, wie Query Service die Sichtbarkeit geplanter Abfrageausführungen verbessert.
