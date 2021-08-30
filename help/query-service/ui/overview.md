---
keywords: Experience Platform; Startseite; beliebte Themen; Abfragedienst; Query Service; Abfrage; Abfrageeditor; Abfrage-Editor; Abfrage-Editor;
solution: Experience Platform
title: UI-Anleitung für Query Service
topic-legacy: guide
description: Adobe Experience Platform Query Service bietet eine Benutzeroberfläche, über die Abfragen geschrieben und ausgeführt, zuvor ausgeführte Abfragen angezeigt und auf Abfragen zugegriffen werden kann, die von Benutzern in Ihrer IMS-Organisation gespeichert wurden.
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: 30c3ca4aa3e8f42140566c8fdf9fbc855ec72e1b
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 3%

---

# [!DNL Query Service] Handbuch

Die Adobe Experience Platform [!DNL Query Service] bietet eine Benutzeroberfläche, über die Abfragen geschrieben und ausgeführt, zuvor ausgeführte Abfragen angezeigt und auf Abfragen zugegriffen werden kann, die von Benutzern in Ihrer IMS-Organisation gespeichert wurden. Um auf die Benutzeroberfläche von [Adobe Experience Platform](https://platform.adobe.com) zuzugreifen, wählen Sie **[!UICONTROL Abfragen]** im linken Navigationsbereich aus.

## [!DNL Query Editor]

Mit dem [!DNL Query Editor] können Sie Abfragen schreiben und ausführen, ohne einen externen Client zu verwenden. Wählen Sie **[!UICONTROL Abfrage erstellen]** aus, um [!DNL Query Editor] zu öffnen und eine neue Abfrage zu erstellen. Sie können auch auf [!DNL Query Editor] zugreifen, indem Sie eine Abfrage auf den Registerkarten **[!UICONTROL Protokoll]** oder **[!UICONTROL Durchsuchen]** auswählen. Wenn Sie eine zuvor ausgeführte oder gespeicherte Abfrage auswählen, wird der [!DNL Query Editor] geöffnet und die SQL für die ausgewählte Abfrage angezeigt.

![Bild](../images/ui/overview/overview.png)

[!DNL Query Editor] bietet Bearbeitungsraum, in den Sie mit der Eingabe einer Abfrage beginnen können. Während der Eingabe vervollständigt der Editor automatisch SQL-reservierte Wörter, Tabellen und Feldnamen in Tabellen. Wenn Sie die Abfrage fertig geschrieben haben, wählen Sie die Schaltfläche **Abspielen** aus, um die Abfrage auszuführen. Die Registerkarte **[!UICONTROL Konsole]** unter dem Editor zeigt an, was [!DNL Query Service] derzeit tut, und zeigt an, wann eine Abfrage zurückgegeben wurde. Auf der Registerkarte **[!UICONTROL Result]** neben der Konsole werden Abfrageergebnisse angezeigt. Weitere Informationen zur Verwendung von [!DNL Query Editor] finden Sie im [Handbuch zum Abfrage-Editor](./user-guide.md) .

![Bild](../images/ui/overview/query-editor.png)

## Durchsuchen

Die Registerkarte **[!UICONTROL Durchsuchen]** enthält Abfragen, die von Benutzern in Ihrer Organisation gespeichert wurden. Es ist nützlich, diese als Abfrageprojekte zu betrachten, da die hier gespeicherten Abfragen möglicherweise noch im Aufbau sind. Auf der Registerkarte **[!UICONTROL Durchsuchen]** angezeigte Abfragen werden auch als Ausführungsabfragen auf der Registerkarte **[!UICONTROL Protokoll]** angezeigt, wenn sie zuvor von [!DNL Query Service] ausgeführt wurden.

![Bild](../images/ui/overview/browse.png)

| Spalte | Beschreibung |
| --- | --- |
| Name | Der vom Benutzer erstellte Abfragename. Sie können auf dem Namen auswählen, um die Abfrage im [!DNL Query Editor] zu öffnen. Sie können auch die Suchleiste verwenden, um nach dem Namen einer Abfrage zu suchen. Bei Suchen wird zwischen Groß- und Kleinschreibung unterschieden. |
| SQL | Die ersten Zeichen der SQL-Abfrage. Wenn Sie den Mauszeiger über den Code bewegen, wird die vollständige Abfrage angezeigt. |
| Geändert von | Der letzte Benutzer, der die Abfrage geändert hat. Jeder Benutzer in Ihrer Organisation mit Zugriff auf [!DNL Query Service] kann Abfragen ändern. |
| Zuletzt geändert | Datum und Uhrzeit der letzten Änderung der Abfrage in der Zeitzone des Browsers. |

## Protokoll

Der Tab **[!UICONTROL Protokoll]** enthält eine Liste der Abfragen, die bereits ausgeführt wurden. Standardmäßig werden die Abfragen im Protokoll in umgekehrter Chronologie aufgelistet.

![Bild](../images/ui/overview/log.png)

| Spalte | Beschreibung |
| --- | --- |
| **[!UICONTROL Name]** | Der Abfragename, bestehend aus den ersten Zeichen der SQL-Abfrage. Wenn Sie den Namen auswählen, wird der [!DNL Query Editor] geöffnet, sodass Sie die Abfrage bearbeiten können. Sie können die Suchleiste verwenden, um nach dem Namen einer Abfrage zu suchen. Bei Suchen wird zwischen Groß- und Kleinschreibung unterschieden. |
| **[!UICONTROL Erstellt von]** | Der Name der Person, die die Abfrage erstellt hat. |
| **[!UICONTROL Client]** | Der für die Abfrage verwendete Client. |
| **[!UICONTROL Datensatz]** | Der von der Abfrage verwendete Eingabedatensatz. Wählen Sie den Datensatz aus, um zum Bildschirm mit den Details des Eingabedatasets zu gelangen. |
| **[!UICONTROL Status]** | Der aktuelle Status der Abfrage. |
| **[!UICONTROL Letzter Lauf]** | Wann die Abfrage zuletzt ausgeführt wurde. Sie können die Liste in auf- oder absteigender Reihenfolge sortieren, indem Sie den Pfeil über dieser Spalte auswählen. |
| **[!UICONTROL Laufzeit]** | Die Zeit, die zum Ausführen der Abfrage benötigt wurde. |

## Anmeldeinformationen

Auf der Registerkarte **[!UICONTROL Anmeldedaten]** werden Ihre ablaufenden und nicht ablaufenden Anmeldedaten angezeigt. Weitere Informationen zur Verwendung dieser Anmeldedaten für die Verbindung mit externen Clients finden Sie im [Handbuch zu Zugangsdaten](../clients/overview.md).

![Bild](../images/ui/overview/credentials.png)

## Nächste Schritte

Nachdem Sie mit der [!DNL Query Service]-Benutzeroberfläche unter [!DNL Platform] vertraut sind, können Sie [!DNL Query Editor] aufrufen, um Ihre eigenen Abfrageprojekte zu erstellen, die für andere Benutzer in Ihrer Organisation freigegeben werden können. Weitere Informationen zum Erstellen und Ausführen von Abfragen in [!DNL Query Editor] finden Sie im [Benutzerhandbuch für den Abfrage-Editor](./user-guide.md).