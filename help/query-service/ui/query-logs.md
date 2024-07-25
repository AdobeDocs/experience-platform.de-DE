---
title: Abfrageprotokolle
description: Abfrageprotokolle werden automatisch bei jeder Ausführung einer Abfrage generiert und stehen über die Benutzeroberfläche zur Verfügung, um die Fehlerbehebung zu unterstützen. In diesem Dokument wird beschrieben, wie Sie den Abschnitt "Query Service Logs"der Benutzeroberfläche verwenden und darin navigieren.
exl-id: 929e9fba-a9ba-4bf9-a363-ca8657a84f75
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 3%

---

# Abfrageprotokolle

>[!IMPORTANT]
>
>Bestimmte Abfrageprotokollfunktionen sind derzeit in einer eingeschränkten Version verfügbar und stehen nicht allen Kunden zur Verfügung. Ihre Benutzeroberfläche wird möglicherweise ohne Bearbeitungssymbol etwas anders angezeigt. Außerdem können Sie beim Auswählen eines Abfragennamens anstelle der Ansicht [!UICONTROL Details des Abfragenprotokolls] zum Abfrage-Editor navigieren.

Adobe Experience Platform verwaltet ein Protokoll aller Abfrageereignisse, die sowohl über die API als auch über die Benutzeroberfläche auftreten. Diese Informationen sind in der Benutzeroberfläche von Query Service auf der Registerkarte [!UICONTROL Protokolle] verfügbar.

Die Protokolldateien werden automatisch von jedem Abfrageereignis generiert und enthalten Informationen wie die verwendete SQL-Datei, den Status der Abfrage, die Dauer und die letzte Laufzeit. Sie können Abfrageprotokolldaten als leistungsstarkes Tool zur Fehlerbehebung bei ineffizienten oder problematischen Abfragen verwenden. Umfassendere Protokollinformationen werden im Rahmen der Funktion &quot;Auditprotokoll&quot;aufbewahrt und finden Sie in der [Dokumentation zum Auditprotokoll](../../landing/governance-privacy-security/audit-logs/overview.md).

## Abfrage-Logs überprüfen {#check-query-logs}

Um die Abfrageprotokolle zu überprüfen, wählen Sie [!UICONTROL Abfragen] , um zum Arbeitsbereich &quot;Query Service&quot;zu navigieren, und wählen Sie [!UICONTROL Protokoll] aus den verfügbaren Optionen aus.

>[!NOTE]
>
>Sowohl Systemabfragen als auch Dashboard-Abfragen sind standardmäßig ausgeschlossen. Informationen dazu, wie Sie die angezeigten Protokolle anhand Ihrer Einstellungen verfeinern, finden Sie im Abschnitt [Filter](#filter-logs) .

![Die Platform-Benutzeroberfläche mit hervorgehobenen Abfragen und Protokollen.](../images/ui/query-log/logs.png)

## Anpassen und Suchen {#customize-and-search}

Die Query Service-Logs werden in einem anpassbaren Tabellenformat dargestellt. Um die Tabellenspalten anzupassen, wählen Sie das Einstellungssymbol (![Einstellungssymbol) aus.](/help/images/icons/column-settings.png)) rechts neben dem Bildschirm. Ein Dialogfeld [!UICONTROL Tabelle anpassen] wird angezeigt, in dem die Auswahl jeder Spalte aufgehoben werden kann.

Sie können auch nach Protokollen suchen, die sich auf bestimmte Abfragevorlagen beziehen, indem Sie den Vorlagennamen in das Suchfeld eingeben.

![Der Arbeitsbereich &quot;Abfrageprotokoll&quot;mit der Dropdown-Liste &quot;Suchleiste und Spaltentabelle verwalten&quot;wurde hervorgehoben.](../images/ui/query-log/customize-logs.png)

Eine [Beschreibung für die einzelnen Protokolltabellenspalten](./overview.md#log) finden Sie im Abschnitt Protokoll der Query Service-Übersicht.

## Ermitteln von Protokolldaten

Jede Zeile stellt Protokolldaten für eine Abfrageausführung dar, die mit einer Abfragevorlage verknüpft ist. Wählen Sie eine beliebige Zeile aus der Tabelle aus, um die rechte Seitenleiste mit Protokolldaten für diese Ausführung zu füllen.

![Der Arbeitsbereich &quot;Abfrage-Protokoll&quot;mit einer ausgewählten Zeile und die Protokolldaten in der rechten Seitenleiste sind hervorgehoben.](../images/ui/query-log/log-details.png)

Im Bereich &quot;Protokolldetails&quot;können Sie verschiedene Aktionen durchführen. Sie können die Abfrage als CTAS ausführen, das einen neuen Ausgabedatensatz erstellt, die vollständige SQL-Abfrage, die in der Ausführung verwendet wurde, anzeigen oder kopieren oder die Abfrage löschen.

>[!NOTE]
>
>Die Option [!UICONTROL Als CTAS ausführen] ist nur für eine SELECT-Abfrage verfügbar.

![Der Arbeitsbereich &quot;Abfrage-Protokoll&quot;mit einer ausgewählten Zeile, &quot;Als CTAS ausführen&quot;, &quot;Abfrage löschen&quot;und das Symbol &quot;SQL kopieren&quot;hervorgehoben.](../images/ui/query-log/edit-output-dataset.png)

>[!IMPORTANT]
>
>Bestimmte Abfrageprotokollfunktionen sind derzeit in einer eingeschränkten Version verfügbar und stehen nicht allen Kunden zur Verfügung.

Sie können auch einen Namen für eine Abfragevorlage aus der Spalte [!UICONTROL Name] auswählen, um direkt zur Ansicht [!UICONTROL Details des Abfrageprotokolls] zu navigieren.

>[!NOTE]
>
>Wenn die Abfrage mit der API erstellt wurde und während der Initialisierung kein Vorlagenname angegeben wurde, werden stattdessen die ersten Dutzend Zeichen der SQL-Abfrage angezeigt.

![Die Detailansicht des Abfrageprotokolls.](../images/ui/query-log/query-log-details.png)

## Protokolle bearbeiten {#edit-logs}

Neben dem Vorlagennamen jeder Zeile oder einem SQL-Snippet befindet sich ein Stiftsymbol (![Ein Stiftsymbol).](/help/images/icons/edit.png)), mit denen Sie zum Abfrage-Editor navigieren können. Die Abfrage wird dann im Editor zur Bearbeitung vorausgefüllt.

![Der Arbeitsbereich &quot;Abfrage-Protokoll&quot;mit einem hervorgehobenen Stiftsymbol.](../images/ui/query-log/edit-query.png)

## Filter-Logs {#filter-logs}

Sie können die Liste der Abfrageprotokolle anhand verschiedener Einstellungen filtern. Wählen Sie das Filtersymbol (![Filtersymbol) aus.](/help/images/icons/filter.png)) oben links im Arbeitsbereich, um eine Reihe von Filteroptionen in der linken Leiste zu öffnen.

![Der Arbeitsbereich &quot;Abfrage-Protokoll&quot;mit hervorgehobenem Filtersymbol.](../images/ui/query-log/log-filter.png)

Die Liste der verfügbaren Filter wird angezeigt.

![Der Arbeitsbereich &quot;Abfrage-Protokoll&quot;mit den angezeigten und hervorgehobenen Filteroptionen.](../images/ui/query-log/log-filter-settings.png)

Die folgende Tabelle enthält eine Beschreibung der einzelnen Filter.

| Filter | Beschreibung |
| ------ | ----------- |
| [!UICONTROL Dashboard-Abfragen ausschließen] | Dieses Kontrollkästchen ist standardmäßig aktiviert und schließt Protokolle aus, die von den Abfragen generiert wurden, mit denen Einblicke generiert wurden. Diese Abfragen werden systemgeneriert und verschleiern die Datensätze von benutzergenerierten Protokollen, die zur Überwachung, Verwaltung und Fehlerbehebung erforderlich sind. Um vom System generierte Protokolle anzuzeigen, deaktivieren Sie das Kontrollkästchen. |
| [!UICONTROL Systemabfragen ausschließen] | Dieses Kontrollkästchen ist standardmäßig aktiviert und schließt vom System erstellte Protokolle aus. Systemgenerierte Abfragen umfassen häufig Hintergrundaufgaben oder Wartungsaufgaben, die für die Benutzerüberwachung, Verwaltung oder Fehlerbehebung möglicherweise nicht relevant sind. Wenn Sie systemgenerierte Protokolle überprüfen müssen, deaktivieren Sie dieses Kontrollkästchen, um sie in Ihre Protokollansicht aufzunehmen. |
| [!UICONTROL Startdatum] | Um die Protokolle nach Abfragen zu filtern, die in einem bestimmten Zeitraum erstellt wurden, legen Sie die Datumsangaben [!UICONTROL Start] und [!UICONTROL Ende] im Abschnitt [!UICONTROL Startdatum] fest. |
| [!UICONTROL Abgeschlossenes Datum] | Um die Protokolle nach Abfragen zu filtern, die in einem bestimmten Zeitraum abgeschlossen wurden, legen Sie die Datumsangaben [!UICONTROL Start] und [!UICONTROL Ende] im Abschnitt [!UICONTROL Abgeschlossen Datum] fest. |
| [!UICONTROL Status] | Um Protokolle anhand des [!UICONTROL Status] der Abfrage zu filtern, wählen Sie das entsprechende Optionsfeld aus. Zu den verfügbaren Optionen gehören [!UICONTROL Gesendet], [!UICONTROL Gestartet], [!UICONTROL Erfolg] und [!UICONTROL Fehlgeschlagen]. Sie können Protokolle nur nach einer Statusbedingung filtern. |
| [!UICONTROL Client] | Um die Protokolle nach dem verwendeten Abfrageclient zu filtern, geben Sie einen der folgenden zulässigen Werte in das Feld für den freien Text ein: `API`, `Adobe Query Service UI` oder `QsAccel`. |
| [!UICONTROL Meine Abfragen] | Mit dem Umschalter [!UICONTROL Meine Abfragen] können Sie die Protokolle nach von Ihnen ausgeführten Abfragen filtern. |
| [!UICONTROL Abfrageprotokoll-ID] | Um nach der eindeutigen Logkennung einer Abfrage zu filtern, geben Sie die Logkennung in das Feld für den freien Text ein. Diese Informationen finden Sie in den [!UICONTROL Protokolldetails]. |

Alle angewendeten Filter werden oberhalb der gefilterten Protokollergebnisse angezeigt.

![Die Registerkarte Protokoll des Arbeitsbereichs &quot;Abfragen&quot;, wobei die Liste der angewendeten Filter hervorgehoben ist.](../images/ui/query-log/applied-log-filters.png)

## Nächste Schritte

Durch Lesen dieses Dokuments können Sie jetzt besser verstehen, wie auf Abfrageprotokolle in der Benutzeroberfläche von Query Service zugegriffen und diese verwendet werden.

Weitere Informationen über die Funktionen des Abfrage-Services finden Sie in der [Benutzeroberflächen-Übersicht](./overview.md) oder im [Handbuch zur Abfrage-Service-API](../api/getting-started.md).

Im Dokument [Abfragen überwachen](./monitor-queries.md) erfahren Sie, wie Query Service die Sichtbarkeit geplanter Abfrageausführungen verbessert.
