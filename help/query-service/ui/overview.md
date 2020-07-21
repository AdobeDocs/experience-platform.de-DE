---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handbuch zur Benutzeroberfläche der Adobe Experience Platform Abfrage Service
topic: guide
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 3%

---


# [!DNL Query Service] guide

Die Adobe Experience Platform [!DNL Query Service] bietet eine Benutzeroberfläche, die zum Schreiben und Ausführen von Abfragen, zur Ansicht von zuvor ausgeführten Abfragen und zum Zugriff auf Abfragen verwendet werden kann, die von Benutzern in Ihrem IMS-Unternehmen gespeichert wurden. Um die Benutzeroberfläche innerhalb der [Adobe Experience Platform][platform-ui]aufzurufen, wählen Sie im linken Navigationsbereich die Option &quot; **[!UICONTROL Abfragen]** &quot;aus.

## [!DNL Query Editor]

Mit dem [!DNL Query Editor] können Sie Abfragen ohne Verwendung eines externen Clients schreiben und ausführen. Klicken Sie auf Abfrage **** erstellen, um die Datei zu öffnen [!DNL Query Editor] und eine neue Abfrage zu erstellen. Sie können auch auf die [!DNL Query Editor] Seite zugreifen, indem Sie auf den Registerkarten &quot; *[!UICONTROL Protokoll]* &quot;oder &quot; *[!UICONTROL Durchsuchen]* &quot;eine Abfrage auswählen. Wenn Sie eine zuvor ausgeführte oder gespeicherte Abfrage auswählen, wird die Datei geöffnet [!DNL Query Editor] und die SQL-Datei für die ausgewählte Abfrage angezeigt.

![Bild](../images/queries/ui-overview/overview.png)

[!DNL Query Editor] bietet Bearbeitungsbereich, in dem Sie mit der Eingabe einer Abfrage beginnen können. Während der Eingabe vervollständigt der Editor automatisch SQL-reservierte Wörter, Tabellen und Feldnamen in Tabellen. Wenn Sie Ihre Abfrage fertig geschrieben haben, klicken Sie auf die Schaltfläche **Abspielen** , um die Abfrage auszuführen. Auf der Registerkarte &quot; *[!UICONTROL Konsole]* &quot;unter dem Editor wird angezeigt, was gerade ausgeführt [!DNL Query Service] wird, und es wird angezeigt, wann eine Abfrage zurückgegeben wurde. Auf der Registerkarte &quot; *[!UICONTROL Ergebnis]* &quot;neben der Konsole werden die Ergebnisse der Abfrage angezeigt. Weitere Informationen zur Verwendung des [Abfrage-Editors finden Sie im Handbuch][query-editor] zum [!DNL Query Editor].

![Bild](../images/queries/ui-overview/query-editor.png)

## Durchsuchen

Auf der Registerkarte &quot; *[!UICONTROL Durchsuchen]* &quot;werden Abfragen angezeigt, die von Benutzern in Ihrem Unternehmen gespeichert wurden. Es ist sinnvoll, diese als Abfragen zu betrachten, da die hier gespeicherten Abfragen möglicherweise noch im Bau sind. Abfragen, die auf der Registerkarte &quot; *[!UICONTROL Durchsuchen]* &quot;angezeigt werden, werden auch als ausgeführte Abfragen auf der Registerkarte &quot; *[!UICONTROL Protokoll]* &quot;angezeigt, wenn sie zuvor von ausgeführt wurden [!DNL Query Service].

![Bild](../images/queries/ui-overview/browse.png)

| Spalte | Beschreibung |
| --- | --- |
| Name | Der vom Benutzer erstellte Abfragen-Name. Sie können auf den Namen klicken, um die Abfrage im [!DNL Query Editor]. Sie können auch die Suchleiste verwenden, um nach dem Namen einer Abfrage zu suchen. Bei Suchvorgängen wird zwischen Groß- und Kleinschreibung unterschieden. |
| SQL | Die ersten Zeichen der SQL-Abfrage. Wenn Sie den Mauszeiger über den Code bewegen, wird die vollständige Abfrage angezeigt. |
| Geändert von | Der letzte Benutzer, der die Abfrage geändert hat. Jeder Benutzer in Ihrer Organisation, der Zugriff auf [!DNL Query Service] die Abfragen hat, kann diese ändern. |
| Zuletzt geändert | Datum und Uhrzeit der letzten Änderung der Abfrage in der Zeitzone des Browsers. |

## Protokoll

Auf der Registerkarte &quot; *[!UICONTROL Protokoll]* &quot;finden Sie eine Liste der Abfragen, die zuvor ausgeführt wurden. Standardmäßig werden die Abfragen im Protokoll in umgekehrter Chronologie Liste.

![Bild](../images/queries/ui-overview/log.png)

| Spalte | Beschreibung |
| --- | --- |
| **[!UICONTROL Name]** | Der Name der Abfrage, bestehend aus den ersten Zeichen der SQL-Abfrage. Wenn Sie auf den Namen klicken, wird die Abfrage geöffnet [!DNL Query Editor]und Sie können sie bearbeiten. In der Suchleiste können Sie nach dem Namen einer Abfrage suchen. Bei Suchvorgängen wird zwischen Groß- und Kleinschreibung unterschieden. |
| **[!UICONTROL Erstellt von]** | Der Name der Person, die die Abfrage erstellt hat. |
| **[!UICONTROL Client]** | Der für die Abfrage verwendete Client. |
| **[!UICONTROL Datensatz]** | Der von der Abfrage verwendete Eingabedatensatz. Klicken Sie auf den Datensatz, um zum Anzeigebereich &quot;Eingabedatensetdetails&quot;zu gelangen. |
| **[!UICONTROL Status]** | Der aktuelle Status der Abfrage. |
| **[!UICONTROL Letzte Ausführung]** | Als die Abfrage zuletzt ausgeführt wurde. Sie können die Liste in auf- oder absteigender Reihenfolge sortieren, indem Sie auf den Pfeil über dieser Spalte klicken. |
| **[!UICONTROL Laufzeit]** | Die Zeitdauer, die zum Ausführen der Abfrage erforderlich war. |

## Berechtigungen

Auf der Registerkarte &quot; *[!UICONTROL Berechtigungen]* &quot;werden Ihre [!DNL Postgres] Anmeldeinformationen angezeigt. Klicken Sie auf das Symbol &quot; **[!UICONTROL Kopieren]** &quot;neben einem Feld, um dessen Inhalt in Ihrem Tastaturpuffer zu speichern. Weitere Informationen zur Verwendung dieser Anmeldedaten für die Verbindung mit externen Clients finden Sie im [Verbindungshandbuch][connect-clients].

![Bild](../images/queries/ui-overview/credentials.png)

## Nächste Schritte

Da Sie mit der [!DNL Query Service] [!DNL Platform][!DNL Query Editor] Benutzeroberfläche auf vertraut sind, können Sie auf Beginn zugreifen, die Ihre eigenen Abfragen erstellen, um sie mit anderen Benutzern in Ihrem Unternehmen zu teilen. Weitere Informationen zum Erstellen und Ausführen von Abfragen in [!DNL Query Editor]finden Sie im [Abfragen-Editor-Benutzerhandbuch][query-editor].

[platform-ui]: https://platform.adobe.com
[query-editor]: user-guide.md
[connect-clients]: ../clients/overview.md
