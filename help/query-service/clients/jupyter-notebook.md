---
title: Jupyter Notebook mit Query Service verbinden
description: Erfahren Sie, wie Sie Jupyter Notebook mit Adobe Experience Platform Query Service verbinden.
source-git-commit: f910deca43ac49d3a3452b8dbafda20ffdf3bf48
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 3%

---

# Verbinden [!DNL Jupyter Notebook] zu Query Service

In diesem Dokument werden die zum Verbinden erforderlichen Schritte beschrieben. [!DNL Jupyter Notebook] mit Adobe Experience Platform Query Service.

## Erste Schritte

Für dieses Handbuch benötigen Sie bereits Zugriff auf [!DNL Jupyter Notebook] und sind mit der Benutzeroberfläche vertraut. Zum Herunterladen [!DNL Jupyter Notebook] Weitere Informationen finden Sie unter [offiziell [!DNL Jupyter Notebook] Dokumentation](https://jupyter.org/).

So erwerben Sie die erforderlichen Anmeldeinformationen zum Herstellen einer Verbindung [!DNL Jupyter Notebook] zur Experience Platform benötigen Sie Zugriff auf die [!UICONTROL Abfragen] Arbeitsbereich in der Platform-Benutzeroberfläche. Wenden Sie sich an Ihren Organisationsadministrator, wenn Sie derzeit keinen Zugriff auf die [!UICONTROL Abfragen] Arbeitsbereich.

>[!TIP]
>
>[!DNL Anaconda Navigator] ist eine grafische Desktop-Benutzeroberfläche (GUI), die eine einfachere Möglichkeit bietet, allgemeine [!DNL Python] Programme wie [!DNL Jupyter Notebook]. Es hilft auch, Pakete, Umgebungen und Kanäle zu verwalten, ohne Befehlszeilenbefehle zu verwenden.
>Sie können [die von Ihnen bevorzugte Version des Programms installieren](https://docs.anaconda.com/anaconda/install/) von ihrer Website aus.
>Folgen Sie dem geleiteten Installationsprozess. Wählen Sie auf dem Startbildschirm des Anaconda Navigators die Option **[!DNL Jupyter Notebook]** aus der Liste der unterstützten Anwendungen, um das Programm zu starten.
>![Die [!DNL Anaconda Navigator] Startbildschirm mit [!DNL Jupyter Notebook] hervorgehoben.](../images/clients/jupyter-notebook/anaconda-navigator-home.png)
>Weitere Informationen finden Sie in der [amtliche Dokumentation](https://docs.anaconda.com/anaconda/navigator/).

## Launch [!DNL Jupyter Notebook]

Nachdem Sie eine neue [!DNL Jupyter Notebook] Webanwendung, wählen Sie die **[!DNL New]** Dropdown-Liste, gefolgt von **[!DNL Python 3]** , um ein neues Notebook zu erstellen. Die [!DNL Notebook] Editor angezeigt.

![Die [!DNL Jupiter Notebook] Registerkarte Datei mit der [!DNL New dropdown] und [!DNL Python] 3 hervorgehoben.](../images/clients/jupyter-notebook/new-notebook.png)

In der ersten Zeile des [!DNL Notebook] den folgenden Wert eingeben: `pip install psycopg2-binary` und wählen Sie **[!DNL Run]** über die Befehlszeile. Eine Erfolgsmeldung wird unter der Eingabefelder angezeigt.

>[!IMPORTANT]
>
>Um eine Verbindung herzustellen, müssen Sie im Rahmen dieses Prozesses die Option **[!DNL Run]** um jede Codezeile auszuführen.

![Die [!DNL Notebook] Benutzeroberfläche mit hervorgehobenem Befehl &quot;Installationsbibliotheken&quot;.](../images/clients/jupyter-notebook/install-library.png)

Importieren Sie anschließend eine [!DNL PostgreSQL] Datenbankadapter für [!DNL Python]. Geben Sie den Wert ein: `import psycopg2`und wählen Sie **[!DNL Run]**. Für diesen Prozess gibt es keine Erfolgsmeldung. Wenn keine Fehlermeldung vorhanden ist, fahren Sie mit dem nächsten Schritt fort.

![Die [!DNL Notebook] Benutzeroberfläche mit hervorgehobenem Code des Importdatenbank-Treibers.](../images/clients/jupyter-notebook/import-dbdriver.png)

Sie müssen jetzt Ihre Adobe Experience Platform-Anmeldeinformationen angeben, indem Sie den Wert eingeben: `conn = psycopg2.connect("{YOUR_CREDENTIALS}")`. Ihre Anmeldedaten für die Verbindung finden Sie im [!UICONTROL Abfragen] unter [!UICONTROL Anmeldeinformationen] Registerkarte der Platform-Benutzeroberfläche. Weitere Informationen finden Sie in der Dokumentation [Organisationsberechtigungen finden](../ui/credentials.md) für detaillierte Anweisungen.

Die Verwendung von nicht ablaufenden Anmeldeinformationen wird empfohlen, wenn Sie Clients von Drittanbietern verwenden, um das wiederholte Eingeben Ihrer Details zu vermeiden. Anweisungen finden Sie in der Dokumentation zu [Generieren und Verwenden von nicht ablaufenden Anmeldedaten](../ui/credentials.md#non-expiring-credentials).

>[!IMPORTANT]
>
>Stellen Sie beim Kopieren von Anmeldeinformationen aus der Platform-Benutzeroberfläche sicher, dass keine zusätzliche Formatierung der Anmeldeinformationen vorhanden ist. Sie sollten sich alle in einer Zeile befinden, mit einem einzigen Leerzeichen zwischen den Eigenschaften und Werten. Die Anmeldeinformationen sind in Anführungszeichen gesetzt und **not** durch Kommas getrennt.

![Die [!DNL Notebook] Benutzeroberfläche mit hervorgehobenen Verbindungsanmeldedaten.](../images/clients/jupyter-notebook/provide-credentials.png)

Ihre [!DNL Jupyter Notebook] -Instanz ist jetzt mit Query Service verbunden.

## Beispielabfrageausführung

Nachdem Sie eine Verbindung hergestellt haben [!DNL Jupyter Notebook] Für Query Service können Sie mithilfe Ihrer [!DNL Notebook] Eingaben. Im folgenden Beispiel wird eine einfache Abfrage verwendet, um den Prozess zu demonstrieren.

Geben Sie die folgenden Werte ein:

```console
cur = conn.cursor()
cur.execute('''{YOUR_QUERY_HERE}''')
data = [r for r in cur]
```

Rufen Sie als Nächstes den Parameter auf (`data` im obigen Beispiel), um die Abfrageergebnisse in einer unformatierten Antwort anzuzeigen.

![Die [!DNL Notebook] Benutzeroberfläche mit Befehlen zum Zurückgeben und Anzeigen von SQL-Ergebnissen im Notebook.](../images/clients/jupyter-notebook/example-query.png)

Verwenden Sie die folgenden Befehle, um die Ergebnisse für Menschen lesbarer zu formatieren:

- `colnames = [desc[0] for desc in cur.description]`
- `import pandas as pd`
- `import numpy as np`

Diese Befehle generieren keine Erfolgsmeldung. Wenn keine Fehlermeldung angezeigt wird, können Sie eine Funktion verwenden, um die Ergebnisse Ihrer SQL-Abfrage in einem Tabellenformat auszugeben.

![Die zum Formatieren der SQL-Ergebnisse erforderlichen Befehle.](../images/clients/jupyter-notebook/format-results-commands.png)

Geben Sie ein und führen Sie die `df.head()` -Funktion, um die tabularisierten Abfrageergebnisse anzuzeigen.

![Tabellarische Ergebnisse Ihrer SQL-Abfrage in [!DNL Jupyter Notebook].](../images/clients/jupyter-notebook/format-results-output.png)

## Nächste Schritte

Nachdem Sie sich mit Query Service verbunden haben, können Sie [!DNL Jupyter Notebook] , um Abfragen zu schreiben. Weitere Informationen dazu, wie Sie Abfragen formulieren und ausführen, finden Sie im Handbuch zum Thema [Ausführen von Abfragen](../best-practices/writing-queries.md).
