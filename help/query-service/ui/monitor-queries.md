---
title: Überwachung geplanter Abfragen
description: Erfahren Sie, wie Sie Abfragen über die Benutzeroberfläche des Abfrage-Service überwachen.
exl-id: 4640afdd-b012-4768-8586-32f1b8232879
source-git-commit: 95d3604a9589a4d0db7e426dd000ddec9cd4f2ce
workflow-type: tm+mt
source-wordcount: '1230'
ht-degree: 73%

---

# Geplante Abfragen überwachen

Adobe Experience Platform bietet über die Benutzeroberfläche eine verbesserte Sichtbarkeit für den Status aller Abfrageaufträge. Auf der Registerkarte [!UICONTROL Geplante Abfragen] finden Sie jetzt wichtige Informationen zur Ausführung Ihrer Abfragen, darunter den Status, Details zum Zeitplan sowie Fehlermeldungen und -Codes, falls eine Abfrage fehlschlägt. Sie können über die Benutzeroberfläche auf der Registerkarte [!UICONTROL Geplante Abfragen] für jede dieser Abfragen auch Benachrichtigungen für Abfragen basierend auf ihrem Status abonnieren.

## [!UICONTROL Geplante Abfragen]

Die [!UICONTROL Geplante Abfragen] bietet einen Überblick über alle geplanten CTAS- und ITAS-Abfragen. Ausführungsdetails finden Sie für alle geplanten Abfragen sowie Fehlercodes und Meldungen für fehlgeschlagene Abfragen.

Um zur Registerkarte [!UICONTROL Geplante Abfragen] zu navigieren, wählen Sie **[!UICONTROL Abfragen]** in der linken Navigationsleiste und anschließend **[!UICONTROL Geplante Abfragen]**

![Registerkarte „Geplante Abfragen“ im Arbeitsbereich „Abfragen“.](../images/ui/monitor-queries/scheduled-queries.png)

In der folgenden Tabelle werden die einzelnen verfügbaren Spalten beschrieben.

>[!NOTE]
>
>Das Symbol für Abonnements von Warnhinweisen befindet sich in jeder Zeile in einer unbenannten Spalte. Weitere Informationen finden Sie im Abschnitt [Abonnements von Warnhinweisen](#alert-subscription).

| Spalte | Beschreibung |
|---|---|
| **[!UICONTROL Name]** | Das Namensfeld enthält entweder den Namen der Vorlage oder die ersten Zeichen Ihrer SQL-Abfrage. Jede Abfrage, die über die Benutzeroberfläche mit dem Abfrage-Editor erstellt wurde, wird zu Beginn benannt. Wenn die Abfrage über die API erstellt wurde, wird ihr Name zu einem Snippet der ursprünglichen SQL, die zur Erstellung der Abfrage verwendet wurde. Wählen Sie ein Element aus dem [!UICONTROL Name] -Spalte, um eine Liste aller mit der Abfrage verknüpften Ausführungen anzuzeigen. Weitere Informationen finden Sie unter [Zeitplandetails der Abfrage ausführen](#query-runs) Abschnitt. |
| **[!UICONTROL Vorlage]** | Der Name der Abfragevorlage. Klicken Sie auf einen Vorlagennamen, um zum Abfrage-Editor zu navigieren. Die Abfragevorlage wird aus praktischen Gründen im Abfrage-Editor angezeigt. Wenn kein Vorlagenname vorhanden ist, wird die Zeile mit einem Bindestrich markiert und es ist nicht möglich, zum Abfrage-Editor umzuleiten, um die Abfrage anzuzeigen. |
| **[!UICONTROL SQL]** | Ein Ausschnitt der SQL-Abfrage. |
| **[!UICONTROL Ausführungshäufigkeit]** | Dies ist die Kadenz, in der Ihre Abfrage ausgeführt werden soll. Die unterstützten Werte sind `Run once` und `Scheduled`. Abfragen können entsprechend ihrer Ausführungshäufigkeit gefiltert werden. |
| **[!UICONTROL Erstellt von]** | Der Name der Person, die die Abfrage erstellt hat. |
| **[!UICONTROL Erstellt]** | Der Zeitstempel der Erstellung der Abfrage im UTC-Format. |
| **[!UICONTROL Zeitstempel der letzten Ausführung]** | Der Zeitstempel der letzten Ausführung der Abfrage. Diese Spalte zeigt, ob eine Abfrage gemäß ihrem aktuellen Zeitplan ausgeführt wurde. |
| **[!UICONTROL Status der letzten Ausführung]** | Der Status der letzten Abfrageausführung. Die Statuswerte sind: `Success`, `Failed`, `In progress`und `No runs`. |

>[!TIP]
>
>Wenn Sie zum Abfrage-Editor navigieren, können Sie **[!UICONTROL Abfragen]** auswählen, um zur Registerkarte [!UICONTROL Vorlagen] zurückzukehren.

### Anpassen von Tabelleneinstellungen für geplante Abfragen

Sie können die Spalten auf der Registerkarte [!UICONTROL Geplante Abfragen] gemäß Ihren Anforderungen anpassen. Wählen Sie das Einstellungssymbol (![Einstellungssymbol](../images/ui/monitor-queries/settings-icon.png)), um den Dialog [!UICONTROL Tabelleneinstellungen anpassen] zu öffnen und verfügbare Spalten zu bearbeiten.

![Das Symbol „Tabelleneinstellungen anpassen“.](../images/ui/monitor-queries/customze-table-settings-icon.png)

Aktivieren bzw. deaktivieren Sie die entsprechenden Kontrollkästchen, um eine Tabellenspalte zu entfernen oder hinzuzufügen. Klicken Sie dann auf **[!UICONTROL Übernehmen]**, um Ihre Auswahl zu bestätigen.

>[!NOTE]
>
>Jede Abfrage, die über die Benutzeroberfläche erstellt wurde, wird als Teil des Erstellungsprozesses zu einer benannten Vorlage. Der Vorlagenname wird in der Vorlagenspalte angezeigt. Wenn die Abfrage über die API erstellt wurde, ist die Vorlagenspalte leer.

![Der Dialog „Tabelleneinstellungen anpassen“.](../images/ui/monitor-queries/customize-table-dialog.png)

### Warnhinweise abonnieren {#alert-subscription}

Sie können Warnhinweise über die Registerkarte [!UICONTROL Geplante Abfragen] abonnieren. Wählen Sie das Benachrichtigungssymbol für Warnhinweise (![Warnhinweissymbol](../images/ui/monitor-queries/alerts-icon.png)) neben dem Namen einer Abfrage aus, um den Dialog [!UICONTROL Warnhinweise] zu öffnen. Durch den Dialog [!UICONTROL Warnhinweise] werden sowohl Warnhinweise in der Benutzeroberfläche als auch über E-Mail abonniert. Warnhinweise basieren auf dem Status der Abfrage. Dabei stehen drei Optionen zur Verfügung: `start`, `success` und `failure`. Aktivieren Sie die entsprechenden Kontrollkästchen und klicken Sie auf **[!UICONTROL Speichern]**, um zu abonnieren.

![Der Dialog zu Warnhinweis-Abonnements.](../images/ui/monitor-queries/alert-subscription-dialog.png)

Siehe [Dokumentation zur API für Warnhinweise](../api/alert-subscriptions.md) für weitere Informationen.

### Filtern von Abfragen {#filter}

Sie können Abfragen nach der Ausführungsfrequenz filtern. Wählen Sie dazu über die Registerkarte [!UICONTROL Geplante Abfragen] das Filtersymbol (![Filtersymbol](../images/ui/monitor-queries/filter-icon.png)) aus, um die Filter-Seitenleiste zu öffnen.

![Die Registerkarte „Geplante Abfragen“ mit hervorgehobenem Filtersymbol.](../images/ui/monitor-queries/filter-queries.png)

Wählen Sie für die Ausführungshäufigkeit entweder das Kontrollkästchen **[!UICONTROL Geplant]** oder **[!UICONTROL Einmal ausgeführt]** zum Filtern der Abfrageliste aus.

>[!NOTE]
>
>Jede Abfrage, die ausgeführt, aber nicht geplant wurde, gilt als [!UICONTROL Einmal ausgeführt].

![Die Registerkarte „Geplante Abfragen“ mit hervorgehobener Filter-Seitenleiste.](../images/ui/monitor-queries/filter-sidebar.png)

Nachdem Sie Ihre Filterkriterien aktiviert haben, wählen Sie **[!UICONTROL Filter ausblenden]** aus, um den Filterbereich zu schließen.

## Zeitplandetails für Abfragen {#query-runs}

Klicken Sie auf einen Abfragenamen, um zur Seite mit den Zeitplandetails zu navigieren. Diese Ansicht enthält eine Liste aller im Rahmen dieser geplanten Abfrage ausgeführten Durchläufe. Die bereitgestellten Informationen umfassen die Anfangs- und Endzeit, den Status und den verwendeten Datensatz.

![Die Seite mit den Zeitplandetails.](../images/ui/monitor-queries/schedule-details.png)

Diese Informationen werden in einer fünfspaltigen Tabelle bereitgestellt. Jede Zeile bezeichnet die Ausführung einer Abfrage.

| Spaltenname | Beschreibung |
|---|---|
| **[!UICONTROL ID der Abfrageausführung]** | Die ID der Abfrageausführung für die tägliche Ausführung. Wählen Sie die **[!UICONTROL Abfragelaufkennung]** , um zur [!UICONTROL Übersicht über die Ausführung von Abfragen]. |
| **[!UICONTROL Start der Abfrageausführung]** | Der Zeitstempel, wann die Abfrage ausgeführt wurde. Dieser liegt im UTC-Format vor. |
| **[!UICONTROL Abfrageausführung abgeschlossen]** | Der Zeitstempel, wann die Abfrage abgeschlossen wurde. Dieser liegt im UTC-Format vor. |
| **[!UICONTROL Status]** | Der Status der letzten Abfrageausführung. Die drei Statuswerte sind `successful`, `failed` oder `in progress`. |
| **[!UICONTROL Datensatz]** | Der an der Ausführung beteiligte Datensatz. |

Details zur geplanten Abfrage finden Sie im Bedienfeld [!UICONTROL Eigenschaften]. Dieses Bedienfeld enthält die anfängliche Abfrage-ID, den Client-Typ, den Vorlagennamen, die Abfrage-SQL und die Kadenz des Zeitplans.

![Die Seite mit den Zeitplandetails mit hervorgehobenem Eigenschaftenbereich.](../images/ui/monitor-queries/properties-panel.png)

Wählen Sie eine ID für die Abfrageausführung aus, um zur Seite mit den Ausführungsdetails zu navigieren und Abfrageinformationen anzuzeigen.

![Der Bildschirm mit den Zeitplandetails mit einer hervorgehobenen Ausführungs-ID.](../images/ui/monitor-queries/navigate-to-run-details.png)

## Übersicht über die Ausführung von Abfragen {#query-run-overview}

Die [!UICONTROL Übersicht über die Ausführung von Abfragen] enthält Informationen zu einzelnen Ausführungen für diese geplante Abfrage und eine detailliertere Aufschlüsselung des Ausführungsstatus. Auf dieser Seite finden Sie außerdem die Client-Informationen und Details zu Fehlern, die dazu geführt haben, dass die Abfrage fehlschlägt.

![Der Bildschirm mit den Ausführungsdetails mit hervorgehobenem Übersichtsabschnitt.](../images/ui/monitor-queries/query-run-details.png)

Der Abschnitt „Abfragestatus“ enthält den Fehler-Code und die Fehlermeldung, falls die Abfrage fehlschlägt.

![Der Bildschirm mit den Ausführungsdetails mit hervorgehobenem Fehlerabschnitt.](../images/ui/monitor-queries/failed-query.png)

Sie können die Abfrage-SQL aus dieser Ansicht in die Zwischenablage kopieren. Wählen Sie das Kopiersymbol oben rechts im SQL-Snippet aus, um die Abfrage zu kopieren. Eine Popup-Meldung bestätigt, dass der Code kopiert wurde.

![Der Bildschirm mit den Ausführungsdetails mit hervorgehobenem Symbol „SQL-Kopie“.](../images/ui/monitor-queries/copy-sql.png)

### (Eingeschränkte Version) Details für Abfragen mit anonymen Bausteinen ausführen {#anonymous-block-queries}

>[!IMPORTANT]
>
>Die Funktion zur Abfragenüberwachung, die Ausführungsdetails für anonyme Blockabfragen anzeigt, ist derzeit in einer eingeschränkten Version verfügbar und steht nicht allen Kunden zur Verfügung.

Abfragen, die anonyme Bausteine verwenden, um ihre SQL-Anweisungen zu enthalten, werden in ihre einzelnen Abfragen unterteilt. Auf diese Weise können Sie die Ausführungsdetails für jeden Abfrageblock einzeln überprüfen.

Anonyme Bausteine werden mithilfe eines `$$` vor der Abfrage. Siehe [Anonym-Blockdokument](../essential-concepts/anonymous-block.md) um mehr über anonyme Bausteine im Abfragedienst zu erfahren.

Abfragen anonymer Bausteine verfügen über Registerkarten links neben dem Ausführungsstatus. Wählen Sie eine Registerkarte aus, um die Ausführungsdetails anzuzeigen.

![Die Übersicht über die Ausführung von Abfragen mit einer anonymen Blockabfrage. Die Tabs für mehrere Abfragen sind hervorgehoben.](../images/ui/monitor-queries/anonymous-block-overview.png)

Wenn eine anonyme Blockabfrage fehlschlägt, können Sie über diese Benutzeroberfläche den Fehlercode für diesen Baustein finden.

![Die Übersicht über die Abfrage-Ausführung zeigt eine anonyme Blockabfrage an, wobei der Fehlercode für einen einzelnen Block hervorgehoben ist.](../images/ui/monitor-queries/anonymous-block-failed-query.png)

Wählen Sie **[!UICONTROL Abfrage]** aus, um zum Bildschirm mit den Zeitplandetails zurückzukehren, oder wählen Sie **[!UICONTROL Geplante Abfragen]** aus, um zur Registerkarte [!UICONTROL Geplante Abfragen] zurückzukehren.

![Der Bildschirm mit den Ausführungsdetails mit hervorgehobener Abfrage.](../images/ui/monitor-queries/return-navigation.png)
