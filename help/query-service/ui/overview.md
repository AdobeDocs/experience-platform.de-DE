---
keywords: Experience Platform;Home;beliebte Themen;Abfrage-Dienst;Abfrage-Dienst;Abfrage;Abfrage-Editor;Abfrage-Editor;Abfrage-Editor;
solution: Experience Platform
title: Handbuch zur Benutzeroberfläche des Abfrage Service
topic-legacy: guide
description: Der Adobe Experience Platform Abfrage Service bietet eine Benutzeroberfläche, die zum Schreiben und Ausführen von Abfragen, Ansichten, die zuvor ausgeführt wurden, und zum Zugriff auf Abfragen verwendet werden kann, die von Benutzern in Ihrem IMS-Unternehmen gespeichert wurden.
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 3%

---

# [!DNL Query Service] guide

Das Adobe Experience Platform [!DNL Query Service] stellt eine Benutzeroberfläche bereit, die zum Schreiben und Ausführen von Abfragen, zur Ansicht zuvor ausgeführter Abfragen und zum Zugriff auf Abfragen verwendet werden kann, die von Benutzern in Ihrem IMS-Unternehmen gespeichert wurden. Um auf die Benutzeroberfläche von [Adobe Experience Platform][platform-ui] zuzugreifen, wählen Sie **[!UICONTROL Abfragen]** in der linken Navigation aus.

## [!DNL Query Editor]

Mit dem [!DNL Query Editor] können Sie Abfragen schreiben und ausführen, ohne einen externen Client zu verwenden. Klicken Sie auf **[!UICONTROL Abfrage erstellen]**, um [!DNL Query Editor] zu öffnen und eine neue Abfrage zu erstellen. Sie können auch auf das [!DNL Query Editor] zugreifen, indem Sie auf den Registerkarten **[!UICONTROL Log]** oder **[!UICONTROL Browse]** eine Abfrage auswählen. Wenn Sie eine zuvor ausgeführte oder gespeicherte Abfrage auswählen, wird das [!DNL Query Editor] geöffnet und die SQL für die ausgewählte Abfrage angezeigt.

![Bild](../images/queries/ui-overview/overview.png)

[!DNL Query Editor] bietet Bearbeitungsbereich, in dem Sie mit der Eingabe einer Abfrage beginnen können. Während der Eingabe vervollständigt der Editor automatisch SQL-reservierte Wörter, Tabellen und Feldnamen in Tabellen. Wenn Sie mit dem Schreiben der Abfrage fertig sind, klicken Sie auf die Schaltfläche **Abspielen**, um die Abfrage auszuführen. Die Registerkarte **[!UICONTROL Console]** unter dem Editor zeigt an, was [!DNL Query Service] derzeit tut, und gibt an, wann eine Abfrage zurückgegeben wurde. Auf der Registerkarte **[!UICONTROL Result]** neben der Konsole werden die Ergebnisse der Abfrage angezeigt. Weitere Informationen zur Verwendung von [!DNL Query Editor] finden Sie im Handbuch [Abfrage-Editor][query-editor].

![Bild](../images/queries/ui-overview/query-editor.png)

## Durchsuchen

Die Registerkarte **[!UICONTROL Durchsuchen]** zeigt Abfragen an, die von Benutzern in Ihrem Unternehmen gespeichert wurden. Es ist sinnvoll, diese als Abfragen zu betrachten, da die hier gespeicherten Abfragen möglicherweise noch im Bau sind. Abfragen, die auf der Registerkarte **[!UICONTROL Durchsuchen]** angezeigt werden, werden auch als ausgeführte Abfragen auf der Registerkarte **[!UICONTROL Protokoll]** angezeigt, wenn sie zuvor von [!DNL Query Service] ausgeführt wurden.

![Bild](../images/queries/ui-overview/browse.png)

| Spalte | Beschreibung |
| --- | --- |
| Name | Der vom Benutzer erstellte Abfragen-Name. Sie können auf den Namen klicken, um die Abfrage im [!DNL Query Editor] zu öffnen. Sie können auch die Suchleiste verwenden, um nach dem Namen einer Abfrage zu suchen. Bei Suchvorgängen wird zwischen Groß- und Kleinschreibung unterschieden. |
| SQL | Die ersten Zeichen der SQL-Abfrage. Wenn Sie den Mauszeiger über den Code bewegen, wird die vollständige Abfrage angezeigt. |
| Geändert von | Der letzte Benutzer, der die Abfrage geändert hat. Jeder Benutzer in Ihrem Unternehmen mit Zugriff auf [!DNL Query Service] kann Abfragen ändern. |
| Zuletzt geändert | Datum und Uhrzeit der letzten Änderung der Abfrage in der Zeitzone des Browsers. |

## Protokoll

Die Registerkarte **[!UICONTROL Protokoll]** enthält eine Liste der Abfragen, die zuvor ausgeführt wurden. Standardmäßig werden die Abfragen im Protokoll in umgekehrter Chronologie Liste.

![Bild](../images/queries/ui-overview/log.png)

| Spalte | Beschreibung |
| --- | --- |
| **[!UICONTROL Name]** | Der Name der Abfrage, bestehend aus den ersten Zeichen der SQL-Abfrage. Durch Klicken auf den Namen wird das [!DNL Query Editor] geöffnet, sodass Sie die Abfrage bearbeiten können. In der Suchleiste können Sie nach dem Namen einer Abfrage suchen. Bei Suchvorgängen wird zwischen Groß- und Kleinschreibung unterschieden. |
| **[!UICONTROL Erstellt von]** | Der Name der Person, die die Abfrage erstellt hat. |
| **[!UICONTROL Client]** | Der für die Abfrage verwendete Client. |
| **[!UICONTROL Datensatz]** | Der von der Abfrage verwendete Eingabedatensatz. Klicken Sie auf den Datensatz, um zum Anzeigebereich &quot;Eingabedatensetdetails&quot;zu gelangen. |
| **[!UICONTROL Status]** | Der aktuelle Status der Abfrage. |
| **[!UICONTROL Letzte Ausführung]** | Als die Abfrage zuletzt ausgeführt wurde. Sie können die Liste in auf- oder absteigender Reihenfolge sortieren, indem Sie auf den Pfeil über dieser Spalte klicken. |
| **[!UICONTROL Laufzeit]** | Die Zeitdauer, die zum Ausführen der Abfrage erforderlich war. |

## Berechtigungen

Auf der Registerkarte **[!UICONTROL Anmeldeinformationen]** werden Ihre [!DNL Postgres]-Anmeldeinformationen angezeigt. Klicken Sie auf das Symbol **[!UICONTROL Kopieren]** neben einem Feld, um dessen Inhalt in Ihrem Tastaturpuffer zu speichern. Weitere Informationen dazu, wie Sie diese Anmeldeinformationen für die Verbindung mit externen Clients verwenden, finden Sie im Handbuch [Verbindung mit Clients herstellen][connect-clients].

![Bild](../images/queries/ui-overview/credentials.png)

## Nächste Schritte

Nachdem Sie sich mit der [!DNL Query Service]-Benutzeroberfläche auf [!DNL Platform] vertraut gemacht haben, können Sie [!DNL Query Editor] aufrufen, um Beginn zu erstellen, die Ihre eigenen Abfrage-Projekte erstellen, um sie für andere Benutzer in Ihrem Unternehmen freizugeben. Weitere Informationen zum Erstellen und Ausführen von Abfragen in [!DNL Query Editor] finden Sie im [Abfrage Editor Benutzerhandbuch][query-editor].

[platform-ui]: https://platform.adobe.com
[query-editor]: user-guide.md
[connect-clients]: ../clients/overview.md
