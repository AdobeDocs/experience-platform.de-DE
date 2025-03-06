---
title: Abfrageprotokolle
description: Abfrageprotokolle werden automatisch bei jeder Ausführung einer Abfrage generiert und stehen über die Benutzeroberfläche zur Fehlerbehebung zur Verfügung. In diesem Dokument wird beschrieben, wie Sie den Abschnitt Query Service-Protokolle der Benutzeroberfläche verwenden und darin navigieren.
exl-id: 929e9fba-a9ba-4bf9-a363-ca8657a84f75
source-git-commit: db0ba3bb32b5458ab3a32525c3c63939fe804ab4
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 3%

---

# Abfrageprotokolle

Adobe Experience Platform führt ein Protokoll aller Abfrageereignisse, die sowohl über die API als auch über die Benutzeroberfläche auftreten. Diese Informationen sind in der Benutzeroberfläche des Abfrage-Service auf der Registerkarte [!UICONTROL Protokolle] verfügbar.

Die Protokolldateien werden automatisch von jedem Abfrageereignis generiert und enthalten Informationen wie die verwendete SQL, den Status der Abfrage, die Dauer und die letzte Laufzeit. Sie können Abfrageprotokolldaten als leistungsstarkes Tool zur Fehlerbehebung bei ineffizienten oder problematischen Abfragen verwenden. Umfassendere Protokollinformationen werden als Teil der Administratorprotokoll-Funktion gespeichert und finden Sie in der [Administratorprotokoll-Dokumentation](../../landing/governance-privacy-security/audit-logs/overview.md).

## Abfrageprotokolle überprüfen {#check-query-logs}

Um die Abfrageprotokolle zu überprüfen, wählen Sie [!UICONTROL Abfragen] aus, um zum Arbeitsbereich Abfrage-Service zu navigieren, und wählen Sie [!UICONTROL Protokoll] aus den verfügbaren Optionen aus.

>[!NOTE]
>
>Systemabfragen und Dashboard-Abfragen sind standardmäßig ausgeschlossen. Im Abschnitt [Filter](#filter-logs) finden Sie Informationen dazu, wie Sie die angezeigten Protokolle basierend auf Ihren Einstellungen verfeinern können.

![Die Platform-Benutzeroberfläche mit hervorgehobenen Abfragen und hervorgehobenem Protokoll.](../images/ui/query-log/logs.png)

## Anpassen und Suchen {#customize-and-search}

Abfrage-Service-Protokolle werden in einem anpassbaren Tabellenformat angezeigt. Um die Tabellenspalten anzupassen, klicken Sie auf das Einstellungssymbol (![A Einstellungssymbol).](/help/images/icons/column-settings.png)) auf der rechten Seite des Bildschirms. Es [!UICONTROL  ein Dialogfeld „Tabelle anpassen] angezeigt, in dem jede Spalte deaktiviert werden kann.

Sie können auch nach Protokollen suchen, die sich auf bestimmte Abfragevorlagen beziehen, indem Sie den Vorlagennamen in das Suchfeld eingeben.

![Der Arbeitsbereich „Abfrageprotokoll“ mit hervorgehobener Dropdown-Liste „Suchleiste“ und „Spaltentabelle verwalten“.](../images/ui/query-log/customize-logs.png)

Eine [Beschreibung für jede der Protokolltabellenspalten](./overview.md#log) finden Sie im Abschnitt „Protokoll“ der Übersicht über den Abfrage-Service.

## Ermitteln von Protokolldaten

Jede Zeile stellt Protokolldaten für eine Abfrageausführung dar, die mit einer Abfragevorlage verknüpft ist. Wählen Sie eine beliebige Zeile aus der Tabelle aus, um die rechte Seitenleiste mit Protokolldaten für diese Ausführung zu füllen.

![Der Arbeitsbereich „Abfrageprotokoll“ mit einer ausgewählten Zeile und den hervorgehobenen Protokolldaten in der rechten Seitenleiste.](../images/ui/query-log/log-details.png)

Im Bedienfeld Protokolldetails können Sie eine Vielzahl von Aktionen ausführen. Sie können die Abfrage als CTAS ausführen, wodurch ein neuer Ausgabedatensatz erstellt wird. Sie können die vollständige SQL-Abfrage, die bei der Ausführung verwendet wurde, anzeigen oder kopieren oder die Abfrage löschen.

>[!NOTE]
>
>Die Option [!UICONTROL Als CTAS ausführen] ist nur für eine SELECT-Abfrage verfügbar.

![Der Arbeitsbereich „Abfrageprotokoll“ mit einer ausgewählten Zeile, „Als CTAS ausführen“, „Abfrage löschen“ und dem hervorgehobenen Symbol „SQL kopieren“.](../images/ui/query-log/edit-output-dataset.png)

Sie können auch einen Namen für die Abfragevorlage aus der Spalte [!UICONTROL Name] auswählen, um direkt zur Ansicht [!UICONTROL Details zum Abfrageprotokoll] zu navigieren.

>[!NOTE]
>
>Wenn die Abfrage mit der API erstellt wurde und bei der Initialisierung kein Vorlagenname angegeben wurde, werden stattdessen die ersten paar Dutzend Zeichen der SQL-Abfrage angezeigt.

![Die Detailansicht des Abfrageprotokolls.](../images/ui/query-log/query-log-details.png)

## Protokolle bearbeiten {#edit-logs}

Neben dem Vorlagennamen oder SQL-Snippet jeder Zeile befindet sich ein Bleistiftsymbol (![Bleistiftsymbol).](/help/images/icons/edit.png)), mit dem Sie zum Abfrage-Editor navigieren können. Die Abfrage wird dann zur Bearbeitung im Editor vorausgefüllt.

![Der Arbeitsbereich „Abfrageprotokoll“ mit einem hervorgehobenen Stiftsymbol.](../images/ui/query-log/edit-query.png)

## Protokolle filtern {#filter-logs}

Sie können die Liste der Abfrageprotokolle nach verschiedenen Einstellungen filtern. Wählen Sie das Filtersymbol (![Das Filtersymbol.](/help/images/icons/filter.png)) oben links im Arbeitsbereich, um einen Satz von Filteroptionen in der linken Leiste zu öffnen.

![Der Arbeitsbereich „Abfrageprotokoll“ mit hervorgehobenem Filtersymbol.](../images/ui/query-log/log-filter.png)

Die Liste der verfügbaren Filter wird angezeigt.

![Der Arbeitsbereich „Abfrageprotokoll“ mit den angezeigten und hervorgehobenen Filteroptionen.](../images/ui/query-log/log-filter-settings.png)

Die folgende Tabelle enthält eine Beschreibung jedes Filters.

| Filter | Beschreibung |
| ------ | ----------- |
| [!UICONTROL Dashboard-Abfragen ausschließen] | Dieses Kontrollkästchen ist standardmäßig aktiviert und schließt Protokolle aus, die von den Abfragen zum Generieren von Insights generiert wurden. Diese Abfragen werden vom System generiert und verdecken die Aufzeichnungen benutzergenerierter Protokolle, die für die Überwachung, Verwaltung und Fehlerbehebung erforderlich sind. Deaktivieren Sie das Kontrollkästchen, um die systemgenerierten Protokolle anzuzeigen. |
| [!UICONTROL Systemabfragen ausschließen] | Dieses Kontrollkästchen ist standardmäßig aktiviert und schließt vom System generierte Protokolle aus. Systemgenerierte Abfragen umfassen häufig Hintergrundaufgaben oder Wartungsvorgänge, die für die Benutzerüberwachung, -verwaltung oder Fehlerbehebung möglicherweise nicht relevant sind. Wenn Sie systemgenerierte Protokolle überprüfen müssen, deaktivieren Sie dieses Kontrollkästchen, um sie in Ihre Protokollansicht aufzunehmen. |
| [!UICONTROL Startdatum] | Um die Protokolle nach Abfragen zu filtern, die während eines bestimmten Zeitraums erstellt wurden, legen Sie die [!UICONTROL Start] und [!UICONTROL Ende] im Abschnitt [!UICONTROL Startdatum] fest. |
| [!UICONTROL Abschlussdatum] | Um die Protokolle nach Abfragen zu filtern, die während eines bestimmten Zeitraums abgeschlossen wurden, legen Sie die [!UICONTROL Start] und [!UICONTROL Ende] im Abschnitt [!UICONTROL Abschlussdatum] fest. |
| [!UICONTROL Status] | Um Protokolle nach dem [!UICONTROL Status] der Abfrage zu filtern, wählen Sie das entsprechende Optionsfeld aus. Zu den verfügbaren Optionen gehören [!UICONTROL Gesendet], [!UICONTROL In ], [!UICONTROL Erfolg] und [!UICONTROL Fehlgeschlagen]. Sie können Protokolle nur jeweils nach einer Statusbedingung filtern. |
| [!UICONTROL Client] | Um Protokolle nach dem verwendeten Abfrage-Client zu filtern, geben Sie einen der folgenden akzeptierten Werte in das freie Textfeld ein: `API`, `Adobe Query Service UI` oder `QsAccel`. |
| [!UICONTROL Meine Abfragen] | Verwenden Sie den Umschalter [!UICONTROL Meine Abfragen], um die Protokolle nach von Ihnen ausgeführten Abfragen zu filtern. |
| [!UICONTROL ID des Abfrageprotokolls] | Um nach der eindeutigen Protokoll-ID einer Abfrage zu filtern, geben Sie die Protokoll-ID in das freie Textfeld ein. Diese Informationen finden Sie im Abschnitt [!UICONTROL Protokolldetails]. |

Alle angewendeten Filter werden über den gefilterten Protokollergebnissen angezeigt.

![Die Registerkarte „Protokoll“ des Arbeitsbereichs „Abfragen“ mit hervorgehobener Liste der angewendeten Filter.](../images/ui/query-log/applied-log-filters.png)

## Nächste Schritte

Durch das Lesen dieses Dokuments können Sie jetzt besser verstehen, wie in der Benutzeroberfläche von Query Service auf Abfrageprotokolle zugegriffen wird und wie sie verwendet werden.

Weitere Informationen über die Funktionen des Abfrage-Services finden Sie in der [Benutzeroberflächen-Übersicht](./overview.md) oder im [Handbuch zur Abfrage-Service-API](../api/getting-started.md).

Im Dokument [Überwachen von Abfragen](./monitor-queries.md) erfahren Sie, wie der Abfrage-Service die Sichtbarkeit geplanter Abfrageausführungen verbessert.
