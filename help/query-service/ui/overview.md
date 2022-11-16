---
keywords: Experience Platform; Startseite; beliebte Themen; Abfragedienst; Query Service; Abfrage; Abfrageeditor; Abfrage-Editor; Abfrage-Editor;
solution: Experience Platform
title: UI-Anleitung für Query Service
topic-legacy: guide
description: Adobe Experience Platform Query Service bietet eine Benutzeroberfläche, über die Abfragen geschrieben und ausgeführt, zuvor ausgeführte Abfragen angezeigt und auf Abfragen zugegriffen werden kann, die von Benutzern in Ihrer IMS-Organisation gespeichert wurden.
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: 3b6862dd3bb770df4a1549275f911dd81a178002
workflow-type: tm+mt
source-wordcount: '1095'
ht-degree: 3%

---

# Handbuch für die [!DNL Query Service]-Benutzeroberfläche

Die Adobe Experience Platform [!DNL Query Service] bietet eine Benutzeroberfläche, die zum Schreiben und Ausführen von Abfragen, zum Anzeigen zuvor ausgeführter Abfragen und zum Zugriff auf Abfragen verwendet werden kann, die von Benutzern in Ihrer IMS-Organisation gespeichert wurden. So greifen Sie auf die Benutzeroberfläche in zu [Adobe Experience Platform](https://platform.adobe.com)auswählen **[!UICONTROL Abfragen]** in der linken Navigation.

## [!DNL Query Editor]

Die [!DNL Query Editor] ermöglicht Ihnen das Schreiben und Ausführen von Abfragen ohne Verwendung eines externen Clients. Auswählen **[!UICONTROL Abfrage erstellen]** , um [!DNL Query Editor] und erstellen Sie eine neue Abfrage. Sie können auch auf die [!DNL Query Editor] durch Auswahl einer Abfrage aus der **[!UICONTROL Protokoll]** oder **[!UICONTROL Vorlagen]** Registerkarten. Wenn Sie eine zuvor ausgeführte oder gespeicherte Abfrage auswählen, wird die [!DNL Query Editor] und zeigen Sie die SQL für die ausgewählte Abfrage an.

![Das Abfrage-Dashboard mit hervorgehobener Option Abfrage erstellen .](../images/ui/overview/overview.png)

[!DNL Query Editor] bietet Bearbeitungsraum, in den Sie mit der Eingabe einer Abfrage beginnen können. Während der Eingabe vervollständigt der Editor automatisch SQL-reservierte Wörter, Tabellen und Feldnamen in Tabellen. Wenn Sie die Abfrage fertig geschrieben haben, wählen Sie die **Play** -Schaltfläche, um die Abfrage auszuführen. Die **[!UICONTROL Konsole]** wird auf der Registerkarte unter dem Editor angezeigt, was [!DNL Query Service] ist derzeit aktiv und gibt an, wann eine Abfrage zurückgegeben wurde. Die **[!UICONTROL Ergebnis]** neben der Konsole, zeigt die Abfrageergebnisse an. Siehe [Anleitung zum Abfrage-Editor](./user-guide.md) Weitere Informationen zur Verwendung der [!DNL Query Editor].

![Zoomt mit Blick auf die [!DNL Query Editor].](../images/ui/overview/query-editor.png)

## Geplante Abfragen {#scheduled-queries}

Abfragen, die bereits als Vorlage gespeichert wurden, können so geplant werden, dass sie regelmäßig ausgeführt werden. Bei der Planung einer Abfrage können Sie die Ausführungsfrequenz, das Start- und Enddatum, den Wochentag, an dem die geplante Abfrage ausgeführt wird, sowie den Datensatz auswählen, in den die Abfrage exportiert werden soll. Abfragezeitpläne werden mit dem Abfrage-Editor festgelegt.

Informationen zum Planen einer Abfrage über die Benutzeroberfläche finden Sie unter [Handbuch zu geplanten Abfragen](./user-guide.md#scheduled-queries). Informationen zum Hinzufügen von Zeitplänen mithilfe der API finden Sie im Abschnitt [Endpunktleitfaden für geplante Abfragen](../api/scheduled-queries.md).

Sobald eine Abfrage geplant wurde, wird sie in der Liste der geplanten Abfragen auf der [!UICONTROL Geplante Abfragen] Registerkarte. Umfassende Informationen zu Abfrage, Ausführungen, Ersteller und Timings finden Sie durch Auswahl einer geplanten Abfrage aus der Liste.

![Der Arbeitsbereich Abfragen mit der Registerkarte Geplante Abfragen wurde hervorgehoben und zeigt Zeilen der Abfragezeitpläne an.](../images/ui/overview/scheduled-queries.png)

| Spalte | Beschreibung |
| --- | --- |
| **[!UICONTROL Name]** | Das Namensfeld ist entweder der Vorlagenname oder die ersten Zeichen Ihrer SQL-Abfrage. Jede Abfrage, die über die Benutzeroberfläche mit dem Abfrage-Editor erstellt wurde, wird zu Beginn benannt. Wenn die Abfrage über die API erstellt wurde, ist der Name der Abfrage ein Snippet der ursprünglichen SQL, die zur Erstellung der Abfrage verwendet wurde. |
| **[!UICONTROL Vorlage]** | Der Vorlagenname der Abfrage. Wählen Sie einen Vorlagennamen aus, um zum Abfrage-Editor zu navigieren. Die Abfragevorlage wird aus praktischen Gründen im Abfrage-Editor angezeigt. Wenn kein Vorlagenname vorhanden ist, wird die Zeile mit einem Bindestrich markiert und es ist nicht möglich, zum Abfrage-Editor umzuleiten, um die Abfrage anzuzeigen. |
| **[!UICONTROL SQL]** | Ein Ausschnitt der SQL-Abfrage. |
| **[!UICONTROL Ausführungsfrequenz]** | Dies ist die Kadenz, in der Ihre Abfrage ausgeführt werden soll. Die verfügbaren Werte sind `Run once` und `Scheduled`. Abfragen können entsprechend ihrer Ausführungsfrequenz gefiltert werden. |
| **[!UICONTROL Erstellt von]** | Der Name des Benutzers, der die Abfrage erstellt hat. |
| **[!UICONTROL Erstellt]** | Der Zeitstempel der Erstellung der Abfrage im UTC-Format. |
| **[!UICONTROL Zeitstempel der letzten Ausführung]** | Der letzte Zeitstempel, mit dem die Abfrage ausgeführt wurde. Diese Spalte zeigt, ob eine Abfrage gemäß ihrem aktuellen Zeitplan ausgeführt wurde. |
| **[!UICONTROL Letzter Ausführungsstatus]** | Der Status der letzten Abfrageausführung. Die drei Statuswerte sind: `successful` `failed` oder `in progress`. |

Weitere Informationen zum [Abfragen über die Query Service-Benutzeroberfläche überwachen](../monitor-queries.md).

## Vorlagen {#browse}

Die **[!UICONTROL Vorlagen]** zeigt Abfragen an, die von Benutzern in Ihrer Organisation gespeichert wurden. Es ist nützlich, diese als Abfrageprojekte zu betrachten, da die hier gespeicherten Abfragen möglicherweise noch im Aufbau sind. Auf der Seite **[!UICONTROL Vorlagen]** -Registerkarte auch als Ausführungsabfragen in **[!UICONTROL Protokoll]** , wenn sie zuvor von [!DNL Query Service].

![Zoomt im Tab Abfragen-Dashboard-Vorlagen , um mehrere gespeicherte Abfragen anzuzeigen.](../images/ui/overview/templates.png)

| Spalte | Beschreibung |
| --- | --- |
| **[!UICONTROL Name]** | Das Feld name ist entweder der vom Benutzer erstellte Abfragename oder die ersten Zeichen Ihrer SQL-Abfrage. Jede Abfrage, die über die Benutzeroberfläche mit dem Abfrage-Editor erstellt wurde, wird zu Beginn benannt. Wenn die Abfrage über die API erstellt wurde, ist der Name der Abfrage ein Snippet der ursprünglichen SQL, die zur Erstellung der Abfrage verwendet wurde. Sie können den Namen der Abfrage auswählen, um die Abfrage im [!DNL Query Editor]. Sie können auch die Suchleiste verwenden, um nach der [!UICONTROL Name] einer Abfrage. Bei Suchen wird zwischen Groß- und Kleinschreibung unterschieden. |
| **[!UICONTROL SQL]** | Die ersten Zeichen der SQL-Abfrage. Wenn Sie den Mauszeiger über den Code bewegen, wird die vollständige Abfrage angezeigt. |
| **[!UICONTROL Modified by]** | Der letzte Benutzer, der die Abfrage geändert hat. Jeder Benutzer in Ihrer Organisation, der Zugriff auf [!DNL Query Service] kann Abfragen ändern. |
| **[!UICONTROL Zuletzt geändert]** | Datum und Uhrzeit der letzten Änderung der Abfrage in der Zeitzone des Browsers. |

## Protokoll

Die **[!UICONTROL Protokoll]** bietet eine Liste der Abfragen, die bereits ausgeführt wurden. Standardmäßig werden die Abfragen im Protokoll in umgekehrter Chronologie aufgelistet.

![Zoomte Ansicht des Dashboard-Tabs Abfrage-Protokoll , die eine Liste von Abfragen in umgekehrter chronologischer Reihenfolge anzeigt.](../images/ui/overview/log.png)

| Spalte | Beschreibung |
| --- | --- |
| **[!UICONTROL Name]** | Der Abfragename, bestehend aus den ersten Zeichen der SQL-Abfrage. Wenn Sie den Namen auswählen, wird der [!DNL Query Editor], sodass Sie die Abfrage bearbeiten können. Sie können die Suchleiste verwenden, um nach dem Namen einer Abfrage zu suchen. Bei Suchen wird zwischen Groß- und Kleinschreibung unterschieden. |
| **[!UICONTROL Erstellt von]** | Der Name der Person, die die Abfrage erstellt hat. |
| **[!UICONTROL Client]** | Der für die Abfrage verwendete Client. |
| **[!UICONTROL Datensatz]** | Der von der Abfrage verwendete Eingabedatensatz. Wählen Sie den Datensatz aus, um zum Bildschirm mit den Details des Eingabedatasets zu gelangen. |
| **[!UICONTROL Status]** | Der aktuelle Status der Abfrage. |
| **[!UICONTROL Letzte Ausführung]** | Wann die Abfrage zuletzt ausgeführt wurde. Sie können die Liste in auf- oder absteigender Reihenfolge sortieren, indem Sie den Pfeil über dieser Spalte auswählen. |
| **[!UICONTROL Laufzeit]** | Die Zeit, die zum Ausführen der Abfrage benötigt wurde. |

## Anmeldeinformationen

Die **[!UICONTROL Anmeldeinformationen]** -Tab zeigt sowohl Ihre ablaufenden als auch nicht ablaufenden Anmeldedaten an. Weitere Informationen zur Verwendung dieser Anmeldedaten für die Verbindung mit externen Clients finden Sie in der [Handbuch zu Anmeldeinformationen](../clients/overview.md).

![Das Dashboard Abfragen mit der Registerkarte Anmeldedaten wurde hervorgehoben.](../images/ui/overview/credentials.png)

## Nächste Schritte

Jetzt kennen Sie [!DNL Query Service] Benutzeroberfläche auf [!DNL Platform]können Sie [!DNL Query Editor] , um eigene Abfrageprojekte zu erstellen, die für andere Benutzer in Ihrer Organisation freigegeben werden können. Weitere Informationen zum Erstellen und Ausführen von Abfragen finden Sie unter [!DNL Query Editor], siehe [[!DNL Query Editor] Benutzerhandbuch](./user-guide.md).