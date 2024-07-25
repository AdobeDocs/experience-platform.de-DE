---
keywords: Experience Platform;Startseite;beliebte Themen;Abfrage-Service;Abfrage-Service;Abfrage;Abfrageeditor;Abfrage-Editor;Abfrage-Editor;
solution: Experience Platform
title: Handbuch zur Abfrage-Service-Benutzeroberfläche
description: Adobe Experience Platform Query Service bietet eine Benutzeroberfläche, mit der Sie Abfragen schreiben und ausführen, zuvor ausgeführte Abfragen anzeigen und auf Abfragen zugreifen können, die von Benutzern in Ihrer Organisation gespeichert wurden.
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 71%

---

# Handbuch für die [!DNL Query Service]-Benutzeroberfläche

Adobe Experience Platform [!DNL Query Service] bietet eine Benutzeroberfläche, über die Abfragen geschrieben und ausgeführt, zuvor ausgeführte Abfragen angezeigt und auf Abfragen zugegriffen werden kann, die von Benutzern in Ihrem Unternehmen gespeichert wurden. Um auf die Benutzeroberfläche in [Adobe Experience Platform](https://platform.adobe.com) zuzugreifen, wählen Sie in der linken Navigationsleiste **[!UICONTROL Abfragen]** aus.

## [!DNL Query Editor]

Der [!DNL Query Editor] ermöglicht Ihnen, Abfragen ohne Verwendung eines externen Clients zu schreiben und auszuführen. Wählen Sie **[!UICONTROL Abfrage erstellen]** aus, um den [!DNL Query Editor] zu öffnen und eine neue Abfrage zu erstellen. Sie können auf den [!DNL Query Editor] auch zugreifen, indem Sie auf der Registerkarte **[!UICONTROL Protokoll]** oder **[!UICONTROL Vorlagen]** eine Abfrage auswählen. Wenn Sie eine zuvor ausgeführte oder gespeicherte Abfrage auswählen, wird der [!DNL Query Editor] geöffnet und der SQL-Code für die ausgewählte Abfrage angezeigt.

![Das Abfrage-Dashboard mit hervorgehobener Option „Abfrage erstellen“.](../images/ui/overview/overview.png)

[!DNL Query Editor] bietet einen Bearbeitungsbereich, in dem Sie mit der Eingabe einer Abfrage beginnen können. Während der Eingabe vervollständigt der Editor automatisch reservierte SQL-Wörter, Tabellen und Feldnamen in Tabellen. Wenn Sie die Abfrage fertig geschrieben haben, klicken Sie auf die Schaltfläche **Play**, um die Abfrage auszuführen. Die Registerkarte **[!UICONTROL Konsole]** unter dem Editor zeigt, was [!DNL Query Service] derzeit ausführt und gibt an, wann eine Abfrage zurückgegeben wurde. Auf der Registerkarte **[!UICONTROL Ergebnis]** neben der Konsole werden die Abfrageergebnisse angezeigt. Im [Handbuch zum Abfrage-Editor](./user-guide.md) finden Sie weitere Informationen zur Verwendung von [!DNL Query Editor].

![Eine vergrößerte Ansicht von [!DNL Query Editor].](../images/ui/overview/query-editor.png)

## Geplante Abfragen {#scheduled-queries}

Abfragen, die bereits als Vorlage gespeichert wurden, können so geplant werden, dass sie regelmäßig ausgeführt werden. Bei der Planung einer Abfrage können Sie die Ausführungsfrequenz, das Start- und Enddatum, den Wochentag der geplanten Abfrage sowie den Datensatz auswählen, in den die Abfrage exportiert werden soll. Abfragezeitpläne werden mit dem Abfrage-Editor festgelegt.

Informationen zum Planen einer Abfrage über die Benutzeroberfläche finden Sie im [Handbuch zu geplanten Abfragen](./user-guide.md#scheduled-queries). Informationen zum Hinzufügen von Zeitplänen mithilfe der API finden Sie im [Handbuch zu Endpunkten für geplante Abfragen](../api/scheduled-queries.md).

Nachdem eine Abfrage geplant wurde, wird sie auf der Registerkarte [!UICONTROL Geplante Abfragen] in der Liste der geplanten Abfragen angezeigt. Umfassende Informationen zu Abfrage, Ausführungen, Ersteller und Timings finden Sie, indem Sie eine geplante Abfrage aus der Liste auswählen.

![Der Arbeitsbereich &quot;Abfragen&quot;mit der Registerkarte &quot;Geplante Abfragen&quot;wurde hervorgehoben und zeigt Zeilen der Abfragezeitpläne an.](../images/ui/overview/scheduled-queries.png)

| Spalte | Beschreibung |
| --- | --- |
| **[!UICONTROL Name]** | Das Namensfeld enthält entweder den Namen der Vorlage oder die ersten Zeichen Ihrer SQL-Abfrage. Jede Abfrage, die über die Benutzeroberfläche mit dem Abfrage-Editor erstellt wurde, wird zu Beginn benannt. Wenn die Abfrage über die API erstellt wurde, ist der Name der Abfrage ein Ausschnitt des ursprünglichen SQL-Codes, der zum Erstellen der Abfrage verwendet wurde. |
| **[!UICONTROL Vorlage]** | Der Name der Abfragevorlage. Klicken Sie auf einen Vorlagennamen, um zum Abfrage-Editor zu navigieren. Die Abfragevorlage wird aus praktischen Gründen im Abfrage-Editor angezeigt. Wenn kein Vorlagenname vorhanden ist, wird die Zeile mit einem Bindestrich markiert und es ist nicht möglich, zum Abfrage-Editor umzuleiten, um die Abfrage anzuzeigen. |
| **[!UICONTROL SQL]** | Ein Ausschnitt der SQL-Abfrage. |
| **[!UICONTROL Ausführungsfrequenz]** | Dies ist die Kadenz, in der Ihre Abfrage ausgeführt werden soll. Die unterstützten Werte sind `Run once` und `Scheduled`. Abfragen können entsprechend ihrer Ausführungshäufigkeit gefiltert werden. |
| **[!UICONTROL Erstellt von]** | Der Name der Person, die die Abfrage erstellt hat. |
| **[!UICONTROL Erstellt]** | Der Zeitstempel der Erstellung der Abfrage im UTC-Format. |
| **[!UICONTROL Zeitstempel der letzten Ausführung]** | Der Zeitstempel der letzten Ausführung der Abfrage. Diese Spalte zeigt, ob eine Abfrage gemäß ihrem aktuellen Zeitplan ausgeführt wurde. |
| **[!UICONTROL Letzter Ausführungsstatus]** | Der Status der letzten Abfrageausführung. Die drei Statuswerte sind `successful`, `failed` oder `in progress`. |

Weitere Informationen zum Überwachen von Abfragen über die Query Service-Benutzeroberfläche finden Sie in der Dokumentation[.](./monitor-queries.md)

## Vorlagen {#browse}

Die Registerkarte **[!UICONTROL Vorlagen]** enthält Abfragen, die von Benutzenden in Ihrer Organisation gespeichert wurden. Es ist nützlich, sie als Abfrageprojekte zu betrachten, da die hier gespeicherten Abfragen noch im Aufbau begriffen sein können. Abfragen, die auf der Registerkarte **[!UICONTROL Vorlagen]** angezeigt werden, werden auch auf der Registerkarte **[!UICONTROL Protokoll]** als ausgeführte Abfragen aufgeführt, wenn sie zuvor von [!DNL Query Service] ausgeführt wurden.

![Eine vergrößerte Ansicht der Registerkarte „Vorlagen“ im Abfragen-Dashboard, auf der mehrere gespeicherte Abfragen angezeigt werden.](../images/ui/overview/templates.png)

| Spalte | Beschreibung |
| --- | --- |
| **[!UICONTROL Name]** | Das Namensfeld enthält entweder den vom Benutzer erstellten Abfragenamen oder die ersten Zeichen Ihrer SQL-Abfrage. Jede Abfrage, die über die Benutzeroberfläche mit dem Abfrage-Editor erstellt wurde, wird zu Beginn benannt. Wenn die Abfrage über die API erstellt wurde, ist der Name der Abfrage ein Ausschnitt des ursprünglichen SQL-Codes, der zum Erstellen der Abfrage verwendet wurde. Sie können den Namen der Abfrage auswählen, um die Abfrage im [!DNL Query Editor] zu öffnen. Sie können auch die Suchleiste verwenden, um nach dem [!UICONTROL Namen] einer Abfrage zu suchen. Bei Suchen wird zwischen Groß- und Kleinschreibung unterschieden. |
| **[!UICONTROL SQL]** | Die ersten Zeichen der SQL-Abfrage. Wenn Sie den Mauszeiger über den Code bewegen, wird die vollständige Abfrage angezeigt. |
| **[!UICONTROL Geändert von]** | Der letzte Benutzer, der die Abfrage geändert hat. Jeder Benutzer in Ihrer Organisation, der Zugriff auf [!DNL Query Service] hat, kann Abfragen ändern. |
| **[!UICONTROL Zuletzt geändert]** | Datum und Uhrzeit der letzten Änderung der Abfrage in der Zeitzone des Browsers. |

Weitere Informationen zu Vorlagen in der Platform-Benutzeroberfläche finden Sie in der Dokumentation zu [Abfragevorlagen](./query-templates.md) .

## Protokoll {#log}

Die Registerkarte **[!UICONTROL Protokoll]** enthält eine Liste der Abfragen, die bereits ausgeführt wurden. Standardmäßig werden die Abfragen im Protokoll in umgekehrter chronologischer Reihenfolge aufgelistet.

![Vergrößerte Ansicht der Registerkarte „Protokoll“ im Abfragen-Dashboard mit einer Liste von Abfragen in umgekehrter chronologischer Reihenfolge.](../images/ui/overview/log.png)

| Spalte | Beschreibung |
| --- | --- |
| **[!UICONTROL Name]** | Der Abfragename, der aus den ersten Zeichen der SQL-Abfrage besteht. Wählen Sie den Vorlagennamen aus, um die Ansicht [!UICONTROL Details des Abfrageprotokolls] für diesen Lauf zu öffnen. Sie können die Suchleiste verwenden, um nach dem Namen einer Abfrage zu suchen. Bei Suchen wird zwischen Groß- und Kleinschreibung unterschieden. |
| **[!UICONTROL Startzeit]** | Der Zeitpunkt der Ausführung der Abfrage. |
| **[!UICONTROL Abschlusszeit]** | Die Zeit, zu der die Abfrage ausgeführt wurde. |
| **[!UICONTROL Status]** | Der aktuelle Status der Abfrage. |
| **[!UICONTROL Datensatz]** | Der von der Abfrage verwendete Eingabedatensatz. Wählen Sie den Datensatz aus, um zum Bildschirm mit den Details des Eingabedatensatzes zu gelangen. |
| **[!UICONTROL Client]** | Der für die Abfrage verwendete Client. |
| **[!UICONTROL Erstellt von]** | Der Name der Person, die die Abfrage erstellt hat. |

>
>
>Wählen Sie das Stiftsymbol (![Ein Stiftsymbol) aus.](/help/images/icons/edit.png)) aus einer beliebigen Zeile des Abfrageprotokolls, um zum [!DNL Query Editor] zu navigieren. Die Abfrage wird vorab ausgefüllt, um die Bearbeitung zu erleichtern.

Weitere Informationen zu den Protokolldateien, die automatisch von einem Abfrageereignis generiert werden, finden Sie in der Dokumentation zu [Abfrageprotokollen](./query-logs.md) .

## Anmeldedaten

Die Registerkarte **[!UICONTROL Anmeldedaten]** zeigt sowohl Ihre ablaufenden als auch Ihre nicht ablaufenden Anmeldedaten an. Weitere Informationen zur Verwendung dieser Anmeldedaten für die Verbindung mit externen Clients finden Sie im [Handbuch zu Anmeldedaten](../clients/overview.md).

![Das Dashboard „Abfragen“ mit hervorgehobener Registerkarte „Anmeldedaten“.](../images/ui/overview/credentials.png)

## Nächste Schritte

Da Sie nun mit der Benutzeroberfläche des [!DNL Query Service] in [!DNL Platform] vertraut sind, können Sie auf [!DNL Query Editor] zugreifen, um Ihre eigenen Abfrageprojekte zu erstellen und diese für andere Benutzende in Ihrer Organisation freizugeben. Weitere Informationen zum Erstellen und Ausführen von Abfragen in [!DNL Query Editor] finden Sie im [[!DNL Query Editor] Benutzerhandbuch](./user-guide.md).
