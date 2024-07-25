---
title: Überwachung geplanter Abfragen
description: Erfahren Sie, wie Sie Abfragen über die Benutzeroberfläche des Abfrage-Service überwachen.
exl-id: 4640afdd-b012-4768-8586-32f1b8232879
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '2454'
ht-degree: 26%

---

# Überwachen von geplanten Abfragen 

Adobe Experience Platform bietet über die Benutzeroberfläche eine verbesserte Sichtbarkeit für den Status aller Abfrageaufträge. Auf der Registerkarte [!UICONTROL Geplante Abfragen] finden Sie jetzt wichtige Informationen zu Ihren Abfrageausführungen, die Status, Planungsdetails und Fehlermeldungen/-codes enthalten, falls sie fehlschlagen. Sie können über die Benutzeroberfläche auf der Registerkarte [!UICONTROL Geplante Abfragen] für jede dieser Abfragen auch Benachrichtigungen für Abfragen basierend auf ihrem Status abonnieren.

## [!UICONTROL Geplante Abfragen]

Die Registerkarte [!UICONTROL Geplante Abfragen] bietet einen Überblick über alle geplanten CTAS- und ITAS-Abfragen. Ausführungsdetails finden Sie für alle geplanten Abfragen sowie Fehlercodes und Meldungen für fehlgeschlagene Abfragen.

Um zur Registerkarte [!UICONTROL Geplante Abfragen] zu navigieren, wählen Sie **[!UICONTROL Abfragen]** in der linken Navigationsleiste und anschließend **[!UICONTROL Geplante Abfragen]**

![Die Registerkarte &quot;Geplante Abfragen&quot;im Arbeitsbereich &quot;Abfragen&quot;mit hervorgehobenen Geplanten Abfragen und Abfragen.](../images/ui/monitor-queries/scheduled-queries.png)

In der folgenden Tabelle werden die einzelnen verfügbaren Spalten beschrieben.

>[!NOTE]
>
>Symbol für Warnhinweis-Abonnements (![Ein Symbol für Warnhinweise-Abonnements ).](/help/images/icons/alert-add.png)) in jeder Zeile einer unbenannten Spalte enthalten ist. Weitere Informationen finden Sie im Abschnitt [Abonnements von Warnhinweisen](#alert-subscription).

| Spalte | Beschreibung |
|---|---|
| **[!UICONTROL Name]** | Das Namensfeld enthält entweder den Namen der Vorlage oder die ersten Zeichen Ihrer SQL-Abfrage. Jede Abfrage, die über die Benutzeroberfläche mit dem Abfrage-Editor erstellt wurde, wird zu Beginn benannt. Wenn die Abfrage über die API erstellt wurde, wird ihr Name zu einem Snippet der ursprünglichen SQL, die zur Erstellung der Abfrage verwendet wurde. Um eine Liste aller mit der Abfrage verknüpften Ausführungen anzuzeigen, wählen Sie ein Element aus der Spalte [!UICONTROL Name] aus. Weitere Informationen finden Sie im Abschnitt [Abfrage führt Planungsdetails aus](#query-runs) . |
| **[!UICONTROL Vorlage]** | Der Name der Abfragevorlage. Klicken Sie auf einen Vorlagennamen, um zum Abfrage-Editor zu navigieren. Die Abfragevorlage wird aus praktischen Gründen im Abfrage-Editor angezeigt. Wenn kein Vorlagenname vorhanden ist, wird die Zeile mit einem Bindestrich markiert und es ist nicht möglich, zum Abfrage-Editor umzuleiten, um die Abfrage anzuzeigen. |
| **[!UICONTROL SQL]** | Ein Ausschnitt der SQL-Abfrage. |
| **[!UICONTROL Ausführungsfrequenz]** | Die Häufigkeit, mit der Ihre Abfrage ausgeführt werden soll. Die verfügbaren Werte sind `Run once` und `Scheduled`. |
| **[!UICONTROL Erstellt von]** | Der Name der Person, die die Abfrage erstellt hat. |
| **[!UICONTROL Erstellt]** | Der Zeitstempel der Erstellung der Abfrage im UTC-Format. |
| **[!UICONTROL Zeitstempel der letzten Ausführung]** | Der Zeitstempel der letzten Ausführung der Abfrage. Diese Spalte zeigt, ob eine Abfrage gemäß ihrem aktuellen Zeitplan ausgeführt wurde. |
| **[!UICONTROL Letzter Ausführungsstatus]** | Der Status der letzten Abfrageausführung. Die Statuswerte sind: `Success`, `Failed`, `In progress` und `No runs`. |
| **[!UICONTROL Planstatus]** | Der aktuelle Status der geplanten Abfrage. Es gibt sechs potenzielle Werte: [!UICONTROL Registering], [!UICONTROL Active], [!UICONTROL Inaktiv], [!UICONTROL Gelöscht], einen Bindestrich und [!UICONTROL In Quarantäne].<ul><li>Der Status **[!UICONTROL Registering]** gibt an, dass das System die Erstellung des neuen Zeitplans für die Abfrage noch verarbeitet. Beachten Sie, dass Sie eine geplante Abfrage während der Registrierung nicht deaktivieren oder löschen können.</li><li>Der Status **[!UICONTROL Aktiv]** zeigt an, dass die geplante Abfrage **ihr Abschlussdatum und ihre Endzeit noch nicht überschritten hat**.</li><li>Der Status **[!UICONTROL Inaktiv]** zeigt an, dass die geplante Abfrage **ihr Abschlussdatum und ihre Endzeit überschritten hat oder von einem Benutzer als inaktiv markiert wurde.**</li><li>Der Status **[!UICONTROL Gelöscht]** zeigt an, dass der Abfragezeitplan gelöscht wurde.</li><li>Der Bindestrich zeigt an, dass es sich bei der geplanten Abfrage um eine einmalige, nicht wiederkehrende Abfrage handelt.</li><li>Der Status **[!UICONTROL In Quarantäne]** zeigt an, dass die Abfrage zehn aufeinander folgende Ausführungen fehlgeschlagen ist, und erfordert Ihre Intervention, bevor weitere Ausführungen durchgeführt werden können.</li></ul> |

>[!TIP]
>
>Wenn Sie zum Abfrage-Editor navigieren, können Sie **[!UICONTROL Abfragen]** auswählen, um zur Registerkarte [!UICONTROL Vorlagen] zurückzukehren.

## Anpassen von Tabelleneinstellungen für geplante Abfragen {#customize-table}

Sie können die Spalten auf der Registerkarte [!UICONTROL Geplante Abfragen] gemäß Ihren Anforderungen anpassen. Um das Dialogfeld [!UICONTROL Tabellen-Einstellungen anpassen] zu öffnen und verfügbare Spalten zu bearbeiten, wählen Sie das Einstellungssymbol (![Einstellungssymbol) aus.](/help/images/icons/column-settings.png)) oben rechts auf dem Bildschirm.

>[!NOTE]
>
>Die Spalte [!UICONTROL Erstellt] , die sich auf das Datum bezieht, an dem der Zeitplan erstellt wurde, ist standardmäßig ausgeblendet.

![Die Registerkarte &quot;Geplante Abfragen&quot;mit dem Symbol Tabelleneinstellungen anpassen ist hervorgehoben.](../images/ui/monitor-queries/customze-table-settings-icon.png)

Aktivieren bzw. deaktivieren Sie die entsprechenden Kontrollkästchen, um eine Tabellenspalte zu entfernen oder hinzuzufügen. Klicken Sie dann auf **[!UICONTROL Übernehmen]**, um Ihre Auswahl zu bestätigen.

>[!NOTE]
>
>Jede Abfrage, die über die Benutzeroberfläche erstellt wurde, wird als Teil des Erstellungsprozesses zu einer benannten Vorlage. Der Vorlagenname wird in der Vorlagenspalte angezeigt. Wenn die Abfrage über die API erstellt wurde, ist die Vorlagenspalte leer.

![Der Dialog „Tabelleneinstellungen anpassen“.](../images/ui/monitor-queries/customize-table-dialog.png)

## Geplante Abfragen mit Inline-Aktionen verwalten {#inline-actions}

Die Ansicht [!UICONTROL Geplante Abfragen] bietet verschiedene Inline-Aktionen, um alle Ihre geplanten Abfragen von einem Ort aus zu verwalten. Inline-Aktionen werden in jeder Zeile mit Auslassungspunkten angezeigt. Wählen Sie die Auslassungspunkte einer geplanten Abfrage aus, die Sie verwalten möchten, um die verfügbaren Optionen in einem Popup-Menü anzuzeigen. Zu den verfügbaren Optionen gehören [[!UICONTROL Zeitplan deaktivieren]](#disable) oder [!UICONTROL Zeitplan aktivieren], [[!UICONTROL Zeitplan löschen]](#delete), [[!UICONTROL Abonnieren]](#alert-subscription) für Abfragen von Warnhinweisen und [Aktivieren oder [!UICONTROL Quarantäne deaktivieren]](#quarantined-queries).

![Die Registerkarte &quot;Geplante Abfragen&quot;mit den Ellipsen für die Inline-Aktion und dem Popup-Menü wurde hervorgehoben.](../images/ui/monitor-queries/inline-actions.png)

### Geplante Abfrage deaktivieren oder aktivieren {#disable}

Um eine geplante Abfrage zu deaktivieren, wählen Sie die Auslassungszeichen für die geplante Abfrage aus, die Sie verwalten möchten, und wählen Sie dann **[!UICONTROL Zeitplan deaktivieren]** aus den Optionen im Popup-Menü aus. Es wird ein Dialogfeld angezeigt, in dem Sie Ihre Aktion bestätigen können. Wählen Sie **[!UICONTROL Deaktivieren]** aus, um Ihre Einstellung zu bestätigen.

Nachdem eine geplante Abfrage deaktiviert wurde, können Sie den Zeitplan über denselben Prozess aktivieren. Wählen Sie die Auslassungszeichen aus und wählen Sie dann **[!UICONTROL Zeitplan aktivieren]** aus den verfügbaren Optionen aus.

>[!NOTE]
>
>Wenn eine Abfrage in Quarantäne gestellt wurde, sollten Sie die SQL-Anweisung der Vorlage lesen, bevor Sie deren Planung aktivieren. Dadurch wird verhindert, dass Rechenzeiten verschwendet werden, wenn die Vorlagenabfrage weiterhin Probleme hat.

### Geplante Abfrage löschen {#delete}

Um eine geplante Abfrage zu löschen, wählen Sie die Auslassungszeichen für die geplante Abfrage aus, die Sie verwalten möchten, und wählen Sie dann **[!UICONTROL Zeitplan löschen]** aus den Optionen im Popup-Menü aus. Es wird ein Dialogfeld angezeigt, in dem Sie Ihre Aktion bestätigen können. Wählen Sie **[!UICONTROL Löschen]** aus, um Ihre Einstellung zu bestätigen.

Nachdem eine geplante Abfrage gelöscht wurde, wird sie **nicht** aus der Liste der geplanten Abfragen entfernt. Die von den Ellipsen bereitgestellten Inline-Aktionen werden entfernt und durch das ausgegraute Symbol Warnhinweis-Abonnement hinzufügen ersetzt. Sie können keine Warnungen für den gelöschten Zeitplan abonnieren. Die Zeile verbleibt in der Benutzeroberfläche, um Informationen über die im Rahmen der geplanten Abfrage durchgeführten Ausführungen bereitzustellen.

![Die Registerkarte &quot;Geplante Abfragen&quot;mit einer gelöschten geplanten Abfrage und dem Abmeldesymbol für Warnhinweise, die ausgegraut wurden, wurde hervorgehoben.](../images/ui/monitor-queries/post-delete.png)

Wenn Sie die Ausführung dieser Abfragevorlage planen möchten, wählen Sie den Vorlagennamen aus der entsprechenden Zeile aus, um zum Abfrage-Editor zu navigieren, und befolgen Sie dann die [Anweisungen zum Hinzufügen eines Zeitplans zu einer Abfrage](./query-schedules.md#create-schedule), wie in der Dokumentation beschrieben.

### Warnhinweise abonnieren {#alert-subscription}

Um Warnhinweise für geplante Abfrageausführungen zu abonnieren, wählen Sie entweder das Symbol &quot;`...`&quot;(mit Auslassungszeichen) oder das Abonnementsymbol für Warnhinweise (![Ein Warnhinweis-Abonnementsymbol.).](/help/images/icons/alert-add.png)) für die geplante Abfrage, die Sie verwalten möchten. Das Dropdown-Menü für Inline-Aktionen wird angezeigt. Wählen Sie als Nächstes **[!UICONTROL Abonnieren]** aus den verfügbaren Optionen aus.

![Der Arbeitsbereich für geplante Abfragen mit Auslassungspunkten, das Symbol für die Anmeldung mit Warnhinweisen und das Dropdown-Menü für Inline-Aktionen wurden hervorgehoben.](../images/ui/monitor-queries/subscribe.png)

Das Dialogfeld [!UICONTROL Warnhinweise] wird geöffnet. Das Dialogfeld [!UICONTROL Warnungen] meldet Sie sowohl für Benutzeroberflächenbenachrichtigungen als auch für E-Mail-Warnungen. Es stehen mehrere Optionen für die Warnung-Anmeldung zur Verfügung: `start`, `success`, `failure`, `quarantine` und `delay`. Aktivieren Sie die entsprechenden Kontrollkästchen und klicken Sie auf **[!UICONTROL Speichern]**, um zu abonnieren.

![Der Dialog zu Warnhinweis-Abonnements.](../images/ui/monitor-queries/alert-subscription-dialog.png)

In der folgenden Tabelle werden die unterstützten Abfragewarnungstypen erläutert:

| Warnhinweistyp | Beschreibung |
|---|---|
| `start` | Dieser Warnhinweis benachrichtigt Sie, wenn eine geplante Abfrage gestartet wird oder mit der Verarbeitung beginnt. |
| `success` | Dieser Warnhinweis informiert Sie darüber, wenn eine geplante Abfrage erfolgreich ausgeführt wurde, und zeigt an, dass die Abfrage fehlerfrei ausgeführt wurde. |
| `failed` | Dieser Warnhinweis wird Trigger, wenn eine geplante Abfrage einen Fehler auftritt oder nicht erfolgreich ausgeführt werden kann. Dies hilft Ihnen, Probleme schnell zu identifizieren und zu beheben. |
| `quarantine` | Dieser Warnhinweis wird aktiviert, wenn eine geplante Abfrage unter Quarantäne gestellt wird. Wenn Abfragen in die [Quarantäne-Funktion](#quarantined-queries) aufgenommen werden, wird jede geplante Abfrage, die zehn aufeinander folgende Ausführungen nicht bestehen kann, automatisch in den Status [!UICONTROL In Quarantäne] versetzt. Danach müssen Sie eingreifen, bevor weitere Ausführungen erfolgen können. |
| `delay` | Dieser Warnhinweis benachrichtigt Sie, wenn das Ergebnis einer Abfrageausführung ](#query-run-delay) eine [Verzögerung über einen festgelegten Schwellenwert hinaus aufweist. Sie können einen benutzerdefinierten Zeitpunkt festlegen, zu dem der Warnhinweis Trigger wird, wenn die Abfrage für diesen Zeitraum ausgeführt wird, ohne dass ein Abschluss oder ein Fehler auftritt. |

>[!NOTE]
>
>Um darüber informiert zu werden, dass Abfragen unter Quarantäne gestellt werden, müssen Sie zunächst die geplanten Abfragen in der Funktion [Quarantäne](#quarantined-queries) registrieren.

Weitere Informationen finden Sie in der Dokumentation zur API für Warnhinweise](../api/alert-subscriptions.md) .[

### Anzeigen der Abfragedetails {#query-details}

Wählen Sie das Informationssymbol (![Ein Informationssymbol.](/help/images/icons/info.png)), um das Detailbedienfeld für die Abfrage anzuzeigen. Das Bedienfeld &quot;Details&quot;enthält alle relevanten Informationen über die Abfrage, die über die in der Tabelle der geplanten Abfragen enthaltenen Informationen hinausgehen. Zu den zusätzlichen Informationen gehören die Abfrage-ID, das Datum der letzten Änderung, die SQL der Abfrage, die Zeitplan-ID und der aktuelle Zeitplan.

![Die Registerkarte &quot;Geplante Abfragen&quot;mit dem Informationssymbol und dem Detailbereich, der hervorgehoben ist.](../images/ui/monitor-queries/details-panel.png)

## Quarantäne-Abfragen {#quarantined-queries}

>[!NOTE]
>
>Der Quarantäne-Warnhinweis ist nicht für Ad-hoc-Abfragen zur einmaligen Ausführung verfügbar. Der Quarantäne-Warnhinweis gilt nur für geplante Batch-Abfragen (CTAS und ITAS).

Bei der Registrierung für die Quarantänefunktion wird jede geplante Abfrage, die zehn aufeinander folgende Ausführungen fehlschlägt, automatisch in den Status [!UICONTROL In Quarantäne gestellt] versetzt. Eine Abfrage mit diesem Status wird inaktiv und wird nicht in der geplanten Häufigkeit ausgeführt. Danach müssen Sie eingreifen, bevor weitere Ausführungen erfolgen können. Dadurch werden Systemressourcen geschützt, da Sie die Probleme mit Ihrer SQL vor weiteren Ausführungen überprüfen und korrigieren müssen.

Um eine geplante Abfrage für die Quarantänefunktion zu aktivieren, wählen Sie die Auslassungszeichen (`...`) gefolgt von [!UICONTROL Quarantäne aktivieren] aus dem angezeigten Dropdown-Menü aus.

![Die Registerkarte &quot;Geplante Abfragen&quot;mit den Auslassungspunkten und &quot;Quarantäne aktivieren&quot;wurde im Dropdown-Menü für Inline-Aktionen hervorgehoben.](../images/ui/monitor-queries/inline-enable.png)

Abfragen können während der Erstellung eines Zeitplans auch in die Quarantänefunktion aufgenommen werden. Weitere Informationen finden Sie in der Dokumentation zu [Abfrageplänen](./query-schedules.md#quarantine) .

## Verzögerung bei Abfrage-Ausführung {#query-run-delay}

Halten Sie die Kontrolle über Ihre Berechnungszeiten, indem Sie Warnhinweise für Abfrageverzögerungen einrichten. Sie können die Abfrageleistung überwachen und Benachrichtigungen empfangen, wenn der Status einer Abfrage nach einem bestimmten Zeitraum unverändert bleibt. Verwenden Sie den Warnhinweis &quot;[!UICONTROL Abfragelaufverzögerung]&quot;, um benachrichtigt zu werden, wenn eine Abfrage nach einem bestimmten Zeitraum weiter verarbeitet wird, ohne abgeschlossen zu sein.

Wenn Sie [Warnhinweise abonnieren](#alert-subscription) für geplante Abfrageausführungen, ist einer der verfügbaren Warnhinweise die [!UICONTROL Verzögerung bei der Abfrageausführung]. Für diesen Warnhinweis müssen Sie einen Schwellenwert für die auszuführende Zeit festlegen. An diesem Punkt werden Sie über die Verzögerung bei der Verarbeitung informiert.

Um eine Schwellendauer festzulegen, für die die Benachrichtigung Trigger wird, geben Sie entweder eine Zahl in das Texteingabefeld ein oder erhöhen Sie mithilfe der Nach-oben- und Nach-unten-Pfeile um eine Minute. Da der Schwellenwert in Minuten festgelegt wird, beträgt die maximale Dauer für die Beobachtung einer Ausführungsverzögerung einer Abfrage 1440 Minuten (24 Stunden). Der Standardzeitraum für eine Laufzeitverzögerung beträgt 150 Minuten.

>[!NOTE]
>
>Eine Abfrage kann nur eine einzige Laufzeitverzögerung aufweisen. Wenn Sie die Verzögerungsschwelle ändern, wird sie für Benutzer, die sich für den Warnhinweis angemeldet haben, und für Ihre gesamte Organisation geändert.

![Das Dialogfeld &quot;Warnhinweise&quot;auf der Registerkarte &quot;Geplante Abfragen&quot;, auf der das Eingabefeld für die Verzögerung der Abfrageausführung hervorgehoben ist.](../images/ui/monitor-queries/query-run-delay-input.png)

Im Abschnitt Warnhinweise abonnieren erfahren Sie, wie Sie [Warnhinweise abonnieren[!UICONTROL Verzögerung bei der Abfrageausführung]](#alert-subscription)}.

## Filtern von Abfragen {#filter}

Sie können Abfragen nach der Ausführungsfrequenz filtern. Wählen Sie dazu über die Registerkarte [!UICONTROL Geplante Abfragen] das Filtersymbol (![Filtersymbol](/help/images/icons/filter.png)) aus, um die Filter-Seitenleiste zu öffnen.

![Die Registerkarte „Geplante Abfragen“ mit hervorgehobenem Filtersymbol.](../images/ui/monitor-queries/filter-queries.png)

Um die Liste der Abfragen nach ihrer Ausführungsfrequenz zu filtern, aktivieren Sie entweder die Kontrollkästchen **[!UICONTROL Geplant]** oder **[!UICONTROL Einmal ausführen]** .

>[!NOTE]
>
>Jede Abfrage, die ausgeführt, aber nicht geplant wurde, gilt als [!UICONTROL Einmal ausgeführt].

![Die Registerkarte „Geplante Abfragen“ mit hervorgehobener Filter-Seitenleiste.](../images/ui/monitor-queries/filter-sidebar.png)

Nachdem Sie Ihre Filterkriterien aktiviert haben, wählen Sie **[!UICONTROL Filter ausblenden]** aus, um den Filterbereich zu schließen.

## Zeitplandetails für Abfragen {#query-runs}

Um die Seite mit den Zeitplandetails zu öffnen, wählen Sie auf der Registerkarte [!UICONTROL Geplante Abfragen] einen Abfragenamen aus. Diese Ansicht enthält eine Liste aller im Rahmen dieser geplanten Abfrage ausgeführten Durchläufe. Die bereitgestellten Informationen umfassen die Anfangs- und Endzeit, den Status und den verwendeten Datensatz.

![Die Seite mit den Zeitplandetails.](../images/ui/monitor-queries/schedule-details.png)

Diese Informationen werden in einer fünfspaltigen Tabelle bereitgestellt. Jede Zeile bezeichnet die Ausführung einer Abfrage.

| Spaltenname | Beschreibung |
|---|---|
| **[!UICONTROL Kennung der Abfrage-Ausführung]** | Die Kennung der täglichen Ausführung der Abfrage. Wählen Sie die **[!UICONTROL Kennung der Abfrage-Ausführung]** aus, um zur [!UICONTROL Übersicht der Abfrage-Ausführung] zu navigieren. |
| **[!UICONTROL Start der Abfrage-Ausführung]** | Der Zeitstempel, wann die Abfrage ausgeführt wurde. Der Zeitstempel hat das UTC-Format. |
| **[!UICONTROL Abschluss der Abfrage-Ausführung]** | Der Zeitstempel, wann die Abfrage abgeschlossen wurde. Der Zeitstempel hat das UTC-Format. |
| **[!UICONTROL Status]** | Der Status der letzten Abfrageausführung. Die Statuswerte sind: `Success`, `Failed`, `In progress` oder `Quarantined`. |
| **[!UICONTROL Datensatz]** | Der an der Ausführung beteiligte Datensatz. |

Details zur geplanten Abfrage finden Sie im Bedienfeld [!UICONTROL Eigenschaften]. Dieses Bedienfeld enthält die anfängliche Abfrage-ID, den Client-Typ, den Vorlagennamen, die Abfrage-SQL und die Kadenz des Zeitplans.

![Die Seite mit den Zeitplandetails mit hervorgehobenem Eigenschaftenbereich.](../images/ui/monitor-queries/properties-panel.png)

Wählen Sie eine ID für die Abfrageausführung aus, um zur Seite mit den Ausführungsdetails zu navigieren und Abfrageinformationen anzuzeigen.

![Der Bildschirm mit den Zeitplandetails mit einer hervorgehobenen Ausführungs-ID.](../images/ui/monitor-queries/navigate-to-run-details.png)

## Übersicht der Abfrageausführung {#query-run-overview}

Die [!UICONTROL Übersicht über die Abfrage-Ausführung] enthält Informationen zu den einzelnen Ausführungen für diese geplante Abfrage und eine detailliertere Aufschlüsselung des Ausführungsstatus. Auf dieser Seite finden Sie außerdem die Client-Informationen und Details zu Fehlern, die dazu geführt haben, dass die Abfrage fehlschlägt.

![Der Bildschirm mit den Ausführungsdetails mit hervorgehobenem Übersichtsabschnitt.](../images/ui/monitor-queries/query-run-details.png)

Der Abschnitt „Abfragestatus“ enthält den Fehler-Code und die Fehlermeldung, falls die Abfrage fehlschlägt.

![Der Bildschirm mit den Ausführungsdetails mit hervorgehobenem Fehlerabschnitt.](../images/ui/monitor-queries/failed-query.png)

Sie können die Abfrage-SQL aus dieser Ansicht in die Zwischenablage kopieren. Um die Abfrage zu kopieren, wählen Sie das Kopiersymbol oben rechts im SQL-Snippet aus. Eine Popup-Meldung bestätigt, dass der Code kopiert wurde.

![Der Bildschirm mit den Ausführungsdetails mit hervorgehobenem Symbol „SQL-Kopie“.](../images/ui/monitor-queries/copy-sql.png)

### Ausführliche Informationen zu Abfragen mit anonymen Bausteinen {#anonymous-block-queries}

Abfragen, die anonyme Bausteine verwenden, um ihre SQL-Anweisungen zu enthalten, werden in ihre einzelnen Unterabfragen unterteilt. Durch die Trennung in Unterabfragen können Sie die Ausführungsdetails für jeden Abfrageblock einzeln überprüfen.

>[!NOTE]
>
>Die Ausführungsdetails eines anonymen Blocks, der den DROP-Befehl verwendet, werden als separate Unterabfrage **nicht** gemeldet. Separate Ausführungsdetails sind für CTAS-Abfragen, ITAS-Abfragen und COPY-Anweisungen verfügbar, die als anonyme Block-Subabfragen verwendet werden. Ausführungsdetails für den DROP-Befehl werden derzeit nicht unterstützt.

Anonyme Bausteine werden durch das Präfix &quot;`$$`&quot; vor der Abfrage gekennzeichnet. Weitere Informationen zu anonymen Bausteinen im Abfragedienst finden Sie im Dokument [Anonymer Baustein](../key-concepts/anonymous-block.md) .

Unterabfragen anonymer Bausteine verfügen über Registerkarten links neben dem Ausführungsstatus. Wählen Sie eine Registerkarte aus, um die Ausführungsdetails anzuzeigen.

![Die Übersicht über die Abfrage-Ausführung mit einer anonymen Blockabfrage. Die Tabs für mehrere Abfragen sind hervorgehoben.](../images/ui/monitor-queries/anonymous-block-overview.png)

Wenn eine anonyme Blockabfrage fehlschlägt, können Sie über diese Benutzeroberfläche den Fehlercode für diesen Baustein finden.

![Die Übersicht über den Abfragenablauf mit einer anonymen Blockabfrage, wobei der Fehlercode für einen einzelnen Block hervorgehoben ist.](../images/ui/monitor-queries/anonymous-block-failed-query.png)

Wählen Sie **[!UICONTROL Abfrage]** aus, um zum Bildschirm mit den Zeitplandetails zurückzukehren, oder wählen Sie **[!UICONTROL Geplante Abfragen]** aus, um zur Registerkarte [!UICONTROL Geplante Abfragen] zurückzukehren.

![Der Bildschirm mit den Ausführungsdetails mit hervorgehobener Abfrage.](../images/ui/monitor-queries/return-navigation.png)
