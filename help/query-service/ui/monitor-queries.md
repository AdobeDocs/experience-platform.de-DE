---
title: Überwachen geplanter Abfragen
description: Erfahren Sie, wie Sie Abfragen über die Benutzeroberfläche des Abfrage-Service überwachen.
exl-id: 4640afdd-b012-4768-8586-32f1b8232879
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '2454'
ht-degree: 26%

---

# Überwachen von geplanten Abfragen 

Adobe Experience Platform bietet über die Benutzeroberfläche eine verbesserte Sichtbarkeit für den Status aller Abfrageaufträge. Auf der Registerkarte [!UICONTROL Geplante Abfragen] finden Sie jetzt wichtige Informationen zur Ausführung Ihrer Abfragen, darunter den Status, Details zum Zeitplan sowie Fehlermeldungen und -Codes, falls eine Abfrage fehlschlägt. Sie können über die Benutzeroberfläche auf der Registerkarte [!UICONTROL Geplante Abfragen] für jede dieser Abfragen auch Benachrichtigungen für Abfragen basierend auf ihrem Status abonnieren.

## [!UICONTROL Geplante Abfragen]

Die [!UICONTROL Geplante Abfragen] bietet einen Überblick über alle Ihre geplanten CTAS- und ITAS-Abfragen. Sie finden Ausführungsdetails für alle geplanten Abfragen sowie Fehler-Codes und Meldungen für fehlgeschlagene Abfragen.

Um zur Registerkarte [!UICONTROL Geplante Abfragen] zu navigieren, wählen Sie **[!UICONTROL Abfragen]** in der linken Navigationsleiste und anschließend **[!UICONTROL Geplante Abfragen]**

![Die Registerkarte „Geplante Abfragen“ im Arbeitsbereich „Abfragen“ mit hervorgehobenen Optionen „Geplante Abfragen“ und „Abfragen“.](../images/ui/monitor-queries/scheduled-queries.png)

In der folgenden Tabelle werden die einzelnen verfügbaren Spalten beschrieben.

>[!NOTE]
>
>Das Symbol für Warnhinweis-Abonnements ![Ein Symbol für Warnhinweis-Abonnements.](/help/images/icons/alert-add.png)) in jeder Zeile in einer unbenannten Spalte enthalten ist. Weitere Informationen finden Sie im Abschnitt [Abonnements von Warnhinweisen](#alert-subscription).

| Spalte | Beschreibung |
|---|---|
| **[!UICONTROL Name]** | Das Namensfeld enthält entweder den Namen der Vorlage oder die ersten Zeichen Ihrer SQL-Abfrage. Jede Abfrage, die über die Benutzeroberfläche mit dem Abfrage-Editor erstellt wurde, wird zu Beginn benannt. Wenn die Abfrage über die API erstellt wurde, wird ihr Name zu einem Ausschnitt der ursprünglichen SQL, die zur Erstellung der Abfrage verwendet wurde. Um eine Liste aller mit der Abfrage verknüpften Ausführungen anzuzeigen, wählen Sie ein Element aus der Spalte [!UICONTROL Name] aus. Weitere Informationen finden Sie im Abschnitt [Zeitplandetails für Abfrageausführungen](#query-runs). |
| **[!UICONTROL Vorlage]** | Der Name der Abfragevorlage. Klicken Sie auf einen Vorlagennamen, um zum Abfrage-Editor zu navigieren. Die Abfragevorlage wird aus praktischen Gründen im Abfrage-Editor angezeigt. Wenn kein Vorlagenname vorhanden ist, wird die Zeile mit einem Bindestrich markiert und es ist nicht möglich, zum Abfrage-Editor umzuleiten, um die Abfrage anzuzeigen. |
| **[!UICONTROL SQL]** | Ein Ausschnitt der SQL-Abfrage. |
| **[!UICONTROL Ausführungshäufigkeit]** | Die Kadenz, mit der Ihre Abfrage ausgeführt werden soll. Die verfügbaren Werte sind `Run once` und `Scheduled`. |
| **[!UICONTROL Erstellt von]** | Der Name der Person, die die Abfrage erstellt hat. |
| **[!UICONTROL Erstellt]** | Der Zeitstempel der Erstellung der Abfrage im UTC-Format. |
| **[!UICONTROL Zeitstempel der letzten Ausführung]** | Der Zeitstempel der letzten Ausführung der Abfrage. Diese Spalte zeigt, ob eine Abfrage gemäß ihrem aktuellen Zeitplan ausgeführt wurde. |
| **[!UICONTROL Status des letzten Durchgangs]** | Der Status der letzten Abfrageausführung. Die Statuswerte sind: `Success`, `Failed`, `In progress` und `No runs`. |
| **[!UICONTROL Zeitplanstatus]** | Der aktuelle Status der geplanten Abfrage. Es gibt sechs potenzielle Werte[!UICONTROL &#x200B; „Registrieren], [!UICONTROL Aktiv], [!UICONTROL Inaktiv], [!UICONTROL Gelöscht], einen Bindestrich und [!UICONTROL Quarantäne].<ul><li>Der **[!UICONTROL Registrieren]** gibt an, dass das System noch mit der Erstellung des neuen Zeitplans für die Abfrage beschäftigt ist. Hinweis: Sie können eine geplante Abfrage während der Registrierung nicht deaktivieren oder löschen.</li><li>Der **[!UICONTROL Aktiv]**-Status gibt an, dass die geplante Abfrage **Abschlussdatum und** Abschlusszeit noch nicht verstrichen ist.</li><li>Der Status **[!UICONTROL Inaktiv]** gibt an, dass die geplante Abfrage **Abschlussdatum und** Abschlusszeit verstrichen) oder von einem Benutzer als inaktiv markiert wurde.</li><li>Der **[!UICONTROL Deleted]**-Status gibt an, dass der Abfragezeitplan gelöscht wurde.</li><li>Der Bindestrich zeigt an, dass es sich bei der geplanten Abfrage um eine einmalige, nicht wiederkehrende Abfrage handelt.</li><li>Der Status **[!UICONTROL In Quarantäne]** gibt an, dass die Abfrage zehn aufeinander folgende Durchläufe fehlgeschlagen ist, und erfordert Ihr Eingreifen, bevor weitere Ausführungen durchgeführt werden können.</li></ul> |

>[!TIP]
>
>Wenn Sie zum Abfrage-Editor navigieren, können Sie **[!UICONTROL Abfragen]** auswählen, um zur Registerkarte [!UICONTROL Vorlagen] zurückzukehren.

## Anpassen von Tabelleneinstellungen für geplante Abfragen {#customize-table}

Sie können die Spalten auf der Registerkarte [!UICONTROL Geplante Abfragen] gemäß Ihren Anforderungen anpassen. Um den Dialog &quot;[!UICONTROL Tabelle anpassen] zu öffnen und verfügbare Spalten zu bearbeiten, wählen Sie das Einstellungssymbol (![Einstellungssymbol) aus.](/help/images/icons/column-settings.png)) in der oberen rechten Ecke des Bildschirms.

>[!NOTE]
>
>Die Spalte [!UICONTROL Erstellt], die sich auf das Datum bezieht, an dem der Zeitplan erstellt wurde, ist standardmäßig ausgeblendet.

![Die Registerkarte „Geplante Abfragen“ mit hervorgehobenem Symbol „Tabelleneinstellungen anpassen“.](../images/ui/monitor-queries/customze-table-settings-icon.png)

Aktivieren bzw. deaktivieren Sie die entsprechenden Kontrollkästchen, um eine Tabellenspalte zu entfernen oder hinzuzufügen. Klicken Sie dann auf **[!UICONTROL Übernehmen]**, um Ihre Auswahl zu bestätigen.

>[!NOTE]
>
>Jede Abfrage, die über die Benutzeroberfläche erstellt wurde, wird als Teil des Erstellungsprozesses zu einer benannten Vorlage. Der Vorlagenname wird in der Vorlagenspalte angezeigt. Wenn die Abfrage über die API erstellt wurde, ist die Vorlagenspalte leer.

![Der Dialog „Tabelleneinstellungen anpassen“.](../images/ui/monitor-queries/customize-table-dialog.png)

## Verwalten geplanter Abfragen mit Inline-Aktionen {#inline-actions}

Die [!UICONTROL Geplante Abfragen] bietet verschiedene Inline-Aktionen, um alle Ihre geplanten Abfragen von einem Ort aus zu verwalten. Inline-Aktionen werden in jeder Zeile mit Auslassungspunkten angezeigt. Klicken Sie auf die Auslassungspunkte einer geplanten Abfrage, die Sie verwalten möchten, um die verfügbaren Optionen in einem Popup-Menü anzuzeigen. Zu den verfügbaren Optionen gehören [[!UICONTROL Zeitplan deaktivieren]](#disable) oder [!UICONTROL Zeitplan aktivieren], [[!UICONTROL Zeitplan löschen]](#delete), [[!UICONTROL Abonnieren]](#alert-subscription) Abfragen von Warnhinweisen und [Aktivieren oder [!UICONTROL Quarantäne deaktivieren]](#quarantined-queries).

![Die Registerkarte „Geplante Abfragen“ mit Hervorhebung der Auslassungszeichen für Inline-Aktionen und des Popup-Menüs.](../images/ui/monitor-queries/inline-actions.png)

### Deaktivieren oder Aktivieren einer geplanten Abfrage {#disable}

Um eine geplante Abfrage zu deaktivieren, wählen Sie die Auslassungspunkte für die geplante Abfrage aus, die Sie verwalten möchten, und wählen Sie dann **[!UICONTROL Zeitplan deaktivieren]** aus den Optionen im Popup-Menü aus. Ein Dialogfeld wird angezeigt, um Ihre Aktion zu bestätigen. Wählen **[!UICONTROL Deaktivieren]**, um die Einstellung zu bestätigen.

Sobald eine geplante Abfrage deaktiviert wurde, können Sie den Zeitplan über denselben Prozess aktivieren. Klicken Sie auf die Auslassungszeichen und wählen Sie **[!UICONTROL Zeitplan aktivieren]** aus den verfügbaren Optionen aus.

>[!NOTE]
>
>Wenn eine Abfrage unter Quarantäne gestellt wurde, sollten Sie die SQL-Daten der Vorlage überprüfen, bevor Sie ihren Zeitplan aktivieren. Dadurch wird die Verschwendung von Rechenstunden vermieden, wenn die Vorlagenabfrage weiterhin Probleme aufweist.

### Löschen einer geplanten Abfrage {#delete}

Um eine geplante Abfrage zu löschen, klicken Sie auf die Auslassungszeichen für die geplante Abfrage, die Sie verwalten möchten, und wählen Sie dann **[!UICONTROL Zeitplan löschen]** aus den Optionen im Popup-Menü aus. Ein Dialogfeld wird angezeigt, um Ihre Aktion zu bestätigen. Klicken Sie **[!UICONTROL Löschen]**, um Ihre Einstellung zu bestätigen.

Nachdem eine geplante Abfrage gelöscht wurde, wird sie **nicht** aus der Liste der geplanten Abfragen entfernt. Die von den Auslassungspunkten bereitgestellten Inline-Aktionen werden entfernt und durch das ausgegraute Symbol Warnhinweis-Abonnement hinzufügen ersetzt. Für den gelöschten Zeitplan können keine Warnhinweise abonniert werden. Die Zeile verbleibt in der Benutzeroberfläche, um Informationen zu Ausführungen bereitzustellen, die im Rahmen der geplanten Abfrage durchgeführt wurden.

![Die Registerkarte „Geplante Abfragen“ mit hervorgehobenem Symbol für gelöschte geplante Abfragen und ausgegrauten Warnhinweis-Abonnements.](../images/ui/monitor-queries/post-delete.png)

Wenn Sie Ausführungen für diese Abfragevorlage planen möchten, wählen Sie den Vorlagennamen aus der entsprechenden Zeile aus, um zum Abfrage-Editor zu navigieren, und befolgen Sie dann die [Anweisungen zum Hinzufügen eines Zeitplans zu einer Abfrage](./query-schedules.md#create-schedule) wie in der Dokumentation beschrieben.

### Warnhinweise abonnieren {#alert-subscription}

Um Warnhinweise für geplante Abfrageausführungen zu abonnieren, wählen Sie entweder das `...` (Auslassungszeichen) oder das Warnhinweis-Abonnementsymbol ![Warnhinweis-Abonnementsymbol.](/help/images/icons/alert-add.png)) für die geplante Abfrage, die Sie verwalten möchten. Das Dropdown-Menü Inline-Aktionen wird angezeigt. Wählen Sie anschließend **[!UICONTROL Abonnieren]** aus den verfügbaren Optionen aus.

![Der Arbeitsbereich für geplante Abfragen mit Auslassungszeichen, dem Warnhinweis-Abonnementsymbol und dem hervorgehobenen Dropdown-Menü für Inline-Aktionen.](../images/ui/monitor-queries/subscribe.png)

Der [!UICONTROL Warnhinweise] wird geöffnet. Mit dem [!UICONTROL Warnhinweise] werden sowohl Warnhinweise in der Benutzeroberfläche als auch über E-Mail abonniert. Es stehen verschiedene Abonnementoptionen für Warnhinweise zur Verfügung: `start`, `success`, `failure`, `quarantine` und `delay`. Aktivieren Sie die entsprechenden Kontrollkästchen und klicken Sie auf **[!UICONTROL Speichern]**, um zu abonnieren.

![Der Dialog zu Warnhinweis-Abonnements.](../images/ui/monitor-queries/alert-subscription-dialog.png)

In der folgenden Tabelle werden die unterstützten Warnhinweistypen für Abfragen erläutert:

| Warnhinweistyp | Beschreibung |
|---|---|
| `start` | Dieser Warnhinweis informiert Sie, wenn eine geplante Abfrageausführung initiiert wird oder mit der Verarbeitung beginnt. |
| `success` | Dieser Warnhinweis informiert Sie, wenn eine geplante Abfrage erfolgreich ausgeführt wurde, und gibt an, dass die Abfrage fehlerfrei ausgeführt wurde. |
| `failed` | Dieser Warnhinweis Trigger, wenn bei der Ausführung einer geplanten Abfrage ein Fehler auftritt oder sie nicht erfolgreich ausgeführt werden kann. So können Sie Probleme schnell identifizieren und beheben. |
| `quarantine` | Dieser Warnhinweis wird aktiviert, wenn eine geplante Abfrageausführung in den Quarantänestatus versetzt wird. Wenn Abfragen in der [Quarantänefunktion) registriert sind](#quarantined-queries) wird jede geplante Abfrage, die zehn aufeinander folgende Ausführungen fehlschlägt, automatisch in einen [!UICONTROL Quarantänestatus] versetzt. Sie benötigen dann Ihr Eingreifen, bevor weitere Hinrichtungen stattfinden können. |
| `delay` | Dieser Warnhinweis informiert Sie, wenn das [ einer Abfrageausführung einen bestimmten Schwellenwert überschreitet](#query-run-delay). Sie können einen benutzerdefinierten Trigger festlegen, der den Warnhinweis auslöst, wenn die Abfrage für diesen Zeitraum ausgeführt wird, ohne dass entweder der Abschluss erfolgt oder ein Fehler auftritt. |

>[!NOTE]
>
>Um über in Quarantäne befindliche Abfrageausführungen informiert zu werden, müssen Sie zunächst die geplanten Abfrageausführungen in der [Quarantänefunktion) ](#quarantined-queries).

Weitere Informationen finden [ in der ](../api/alert-subscriptions.md) zur Warnhinweis-Abonnement-API .

### Anzeigen der Abfragedetails {#query-details}

Wählen Sie das Informationssymbol (![Informationssymbol) aus.](/help/images/icons/info.png)), um das Detailbedienfeld für die Abfrage anzuzeigen. Das Bedienfeld Details enthält alle relevanten Informationen zur Abfrage, die über die in der Tabelle Geplante Abfragen enthaltenen Fakten hinausgehen. Zu den zusätzlichen Informationen gehören die Abfrage-ID, das Datum der letzten Änderung, der SQL-Code der Abfrage, die Zeitplan-ID und der aktuell festgelegte Zeitplan.

![Die Registerkarte „Geplante Abfragen“ mit hervorgehobenem Informationssymbol und hervorgehobenem Detailbereich.](../images/ui/monitor-queries/details-panel.png)

## Quarantäneabfragen {#quarantined-queries}

>[!NOTE]
>
>Der Quarantäne-Warnhinweis ist für Ad-hoc-Abfragen vom Typ „Einmal ausgeführt“ nicht verfügbar. Der Quarantäne-Warnhinweis gilt nur für geplante Batch-Abfragen (CTAS und ITAS).

Bei der Registrierung in der Quarantänefunktion wird jede geplante Abfrage, die zehn aufeinander folgende Ausführungen fehlschlägt, automatisch in einen [!UICONTROL Quarantänestatus] versetzt. Eine Abfrage mit diesem Status wird inaktiv und wird nicht in der geplanten Kadenz ausgeführt. Es erfordert dann Ihr Eingreifen, bevor weitere Ausführungen stattfinden können. Dadurch werden die Systemressourcen geschützt, da Sie die Probleme mit Ihrer SQL überprüfen und korrigieren müssen, bevor weitere Ausführungen erfolgen.

Um eine geplante Abfrage für die Quarantänefunktion zu aktivieren, wählen Sie im angezeigten Dropdown-Menü die Auslassungspunkte (`...`) und [!UICONTROL Quarantäne aktivieren] aus.

![Die Registerkarte „Geplante Abfragen“ mit Auslassungszeichen und der hervorgehobenen Option „Quarantäne aktivieren“ im Dropdown-Menü „Inline-Aktionen“.](../images/ui/monitor-queries/inline-enable.png)

Abfragen können auch während des Erstellungsprozesses des Zeitplans in der Quarantänefunktion registriert werden. Weitere Informationen finden [ in der ](./query-schedules.md#quarantine) zu Abfragezeitplänen .

## Verzögerung der Ausführung der Abfrage {#query-run-delay}

Überwachen Sie Ihre Compute-Stunden, indem Sie Warnhinweise für Abfrageverzögerungen festlegen. Sie können die Abfrageleistung überwachen und Benachrichtigungen erhalten, wenn der Status einer Abfrage nach einem bestimmten Zeitraum unverändert bleibt. Verwenden Sie den Warnhinweis [!UICONTROL Verzögerung der Abfrageausführung], um benachrichtigt zu werden, wenn eine Abfrage nach einem bestimmten Zeitraum weiter verarbeitet wird, ohne abgeschlossen zu werden.

Wenn Sie [Warnhinweise abonnieren](#alert-subscription) für geplante Abfrageausführungen verwenden, ist einer der verfügbaren Warnhinweise die [!UICONTROL Verzögerung der Abfrageausführung]. Für diesen Warnhinweis müssen Sie einen Schwellenwert für die Ausführungszeit festlegen. Zu diesem Zeitpunkt werden Sie über die Verzögerung bei der Verarbeitung informiert.

Um eine Schwellenwertzeit auszuwählen, mit der die Benachrichtigung Trigger werden soll, geben Sie entweder eine Zahl in das Texteingabefeld ein oder verwenden Sie die Pfeile nach oben und unten, um den Wert in Schritten von einer Minute zu erhöhen. Da der Schwellenwert in Minuten festgelegt ist, beträgt die maximale Dauer für das Beobachten einer Verzögerung bei der Abfrageausführung 1.440 Minuten (24 Stunden). Der Standardzeitraum für eine Laufverzögerung beträgt 150 Minuten.

>[!NOTE]
>
>Eine Abfrageausführung kann nur eine Laufzeitverzögerung haben. Wenn Sie den Verzögerungsschwellenwert ändern, wird er für Benutzende, die den Warnhinweis abonniert haben, und für Ihre gesamte Organisation geändert.

![Das Dialogfeld „Warnhinweise“ auf der Registerkarte „Geplante Abfragen“ mit hervorgehobenem Eingabefeld für die Verzögerung bei der Abfrageausführung.](../images/ui/monitor-queries/query-run-delay-input.png)

Im Abschnitt Abonnieren von Warnhinweisen erfahren Sie, wie Sie Warnhinweise [abonnieren[!UICONTROL Verzögerung bei der Abfrageausführung]abonnieren](#alert-subscription).

## Filtern von Abfragen {#filter}

Sie können Abfragen nach der Ausführungsfrequenz filtern. Wählen Sie dazu über die Registerkarte [!UICONTROL Geplante Abfragen] das Filtersymbol (![Filtersymbol](/help/images/icons/filter.png)) aus, um die Filter-Seitenleiste zu öffnen.

![Die Registerkarte „Geplante Abfragen“ mit hervorgehobenem Filtersymbol.](../images/ui/monitor-queries/filter-queries.png)

Um die Liste der Abfragen nach ihrer Ausführungshäufigkeit zu filtern, aktivieren Sie entweder das Kontrollkästchen **[!UICONTROL Geplant]** oder **[!UICONTROL Einmal ausgeführt]**.

>[!NOTE]
>
>Jede Abfrage, die ausgeführt, aber nicht geplant wurde, gilt als [!UICONTROL Einmal ausgeführt].

![Die Registerkarte „Geplante Abfragen“ mit hervorgehobener Filter-Seitenleiste.](../images/ui/monitor-queries/filter-sidebar.png)

Nachdem Sie Ihre Filterkriterien aktiviert haben, wählen Sie **[!UICONTROL Filter ausblenden]** aus, um den Filterbereich zu schließen.

## Zeitplandetails für Abfrageausführungen {#query-runs}

Um die Seite mit den Zeitplandetails zu öffnen, wählen Sie einen Abfragenamen auf der Registerkarte [!UICONTROL Geplante Abfragen] aus. Diese Ansicht enthält eine Liste aller im Rahmen dieser geplanten Abfrage ausgeführten Durchläufe. Die bereitgestellten Informationen umfassen die Anfangs- und Endzeit, den Status und den verwendeten Datensatz.

![Die Seite mit den Zeitplandetails.](../images/ui/monitor-queries/schedule-details.png)

Diese Informationen werden in einer fünfspaltigen Tabelle bereitgestellt. Jede Zeile bezeichnet die Ausführung einer Abfrage.

| Spaltenname | Beschreibung |
|---|---|
| **[!UICONTROL ID der Abfrageausführung]** | Die ID der Abfrageausführung für die tägliche Ausführung. Wählen Sie die **[!UICONTROL ID der Abfrageausführung]** aus, um zur [!UICONTROL Übersicht der Abfrageausführung] zu navigieren. |
| **[!UICONTROL Start der Abfrageausführung]** | Der Zeitstempel, wann die Abfrage ausgeführt wurde. Der Zeitstempel ist im UTC-Format. |
| **[!UICONTROL Abfrageausführung abgeschlossen]** | Der Zeitstempel, wann die Abfrage abgeschlossen wurde. Der Zeitstempel ist im UTC-Format. |
| **[!UICONTROL Status]** | Der Status der letzten Abfrageausführung. Die Statuswerte sind: `Success`, `Failed`, `In progress` oder `Quarantined`. |
| **[!UICONTROL Datensatz]** | Der an der Ausführung beteiligte Datensatz. |

Details zur geplanten Abfrage finden Sie im Bedienfeld [!UICONTROL Eigenschaften]. Dieses Bedienfeld enthält die anfängliche Abfrage-ID, den Client-Typ, den Vorlagennamen, die Abfrage-SQL und die Kadenz des Zeitplans.

![Die Seite mit den Zeitplandetails mit hervorgehobenem Eigenschaftenbereich.](../images/ui/monitor-queries/properties-panel.png)

Wählen Sie eine ID für die Abfrageausführung aus, um zur Seite mit den Ausführungsdetails zu navigieren und Abfrageinformationen anzuzeigen.

![Der Bildschirm mit den Zeitplandetails mit einer hervorgehobenen Ausführungs-ID.](../images/ui/monitor-queries/navigate-to-run-details.png)

## Übersicht der Abfrageausführung {#query-run-overview}

Die [!UICONTROL Übersicht über die Abfrageausführung] enthält Informationen zu den einzelnen Ausführungen für diese geplante Abfrage und eine detailliertere Aufschlüsselung des Ausführungsstatus. Auf dieser Seite finden Sie auch die Client-Informationen und Details zu Fehlern, die möglicherweise zum Fehlschlagen der Abfrage geführt haben.

![Der Bildschirm mit den Ausführungsdetails mit hervorgehobenem Übersichtsabschnitt.](../images/ui/monitor-queries/query-run-details.png)

Der Abschnitt „Abfragestatus“ enthält den Fehler-Code und die Fehlermeldung, falls die Abfrage fehlschlägt.

![Der Bildschirm mit den Ausführungsdetails mit hervorgehobenem Fehlerabschnitt.](../images/ui/monitor-queries/failed-query.png)

Sie können die Abfrage-SQL aus dieser Ansicht in die Zwischenablage kopieren. Um die Abfrage zu kopieren, wählen Sie das Kopiersymbol oben rechts im SQL-Snippet aus. Eine Popup-Meldung bestätigt, dass der Code kopiert wurde.

![Der Bildschirm mit den Ausführungsdetails mit hervorgehobenem Symbol „SQL-Kopie“.](../images/ui/monitor-queries/copy-sql.png)

### Ausführungsdetails für Abfragen mit anonymen Block {#anonymous-block-queries}

Abfragen, die anonyme Blöcke verwenden, um ihre SQL-Anweisungen zu enthalten, werden in ihre einzelnen Unterabfragen aufgeteilt. Durch die Aufteilung in Unterabfragen können Sie die Ausführungsdetails für jeden Abfrageblock einzeln überprüfen.

>[!NOTE]
>
>Die Ausführungsdetails eines anonymen Blocks, der den DROP-Befehl verwendet **werden** als separate Unterabfrage gemeldet. Für CTAS-Abfragen, ITAS-Abfragen und COPY-Anweisungen, die als anonyme Block-Unterabfragen verwendet werden, sind separate Ausführungsdetails verfügbar. Ausführungsdetails für den DROP-Befehl werden derzeit nicht unterstützt.

Anonyme Blöcke werden durch die Verwendung eines `$$`-Präfixes vor der Abfrage gekennzeichnet. Weitere Informationen zu anonymen Blöcken in Query Service finden Sie im [Dokument zu anonymen Blöcken](../key-concepts/anonymous-block.md).

Unterabfragen des anonymen Blocks verfügen über Registerkarten links neben dem Ausführungsstatus. Wählen Sie eine Registerkarte aus, um die Ausführungsdetails anzuzeigen.

![Die Übersicht über die Abfrageausführung mit einer anonymen Blockabfrage. Die mehreren Abfrage-Registerkarten sind hervorgehoben.](../images/ui/monitor-queries/anonymous-block-overview.png)

Falls eine anonyme Blockabfrage fehlschlägt, können Sie den Fehlercode für diesen bestimmten Block über diese Benutzeroberfläche finden.

![Die Übersicht der Abfrageausführung mit einer anonymen Blockabfrage mit hervorgehobenem Fehlercode für einen einzelnen Block.](../images/ui/monitor-queries/anonymous-block-failed-query.png)

Wählen Sie **[!UICONTROL Abfrage]** aus, um zum Bildschirm mit den Zeitplandetails zurückzukehren, oder wählen Sie **[!UICONTROL Geplante Abfragen]** aus, um zur Registerkarte [!UICONTROL Geplante Abfragen] zurückzukehren.

![Der Bildschirm mit den Ausführungsdetails mit hervorgehobener Abfrage.](../images/ui/monitor-queries/return-navigation.png)
