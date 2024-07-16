---
title: Jupyter Notebook mit Query Service verbinden
description: Erfahren Sie, wie Sie Jupyter Notebook mit Adobe Experience Platform Query Service verbinden.
exl-id: 358eab67-538f-4ada-931f-783b92db4a1c
source-git-commit: 1af89160cbf5b689396921869fec6c30a5bcfff0
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 4%

---

# Verbinden von [!DNL Jupyter Notebook] mit dem Abfrage-Service

In diesem Dokument werden die Schritte beschrieben, die zum Verbinden von [!DNL Jupyter Notebook] mit dem Adobe Experience Platform Query Service erforderlich sind.

## Erste Schritte

Dieses Handbuch setzt voraus, dass Sie bereits Zugriff auf [!DNL Jupyter Notebook] haben und mit der zugehörigen Benutzeroberfläche vertraut sind. Weitere Informationen zum Herunterladen von [!DNL Jupyter Notebook] oder finden Sie in der [offiziellen [!DNL Jupyter Notebook] Dokumentation](https://jupyter.org/).

Um die erforderlichen Anmeldeinformationen zum Verbinden von [!DNL Jupyter Notebook] mit Experience Platform zu erhalten, müssen Sie auf den Arbeitsbereich [!UICONTROL Abfragen] in der Platform-Benutzeroberfläche zugreifen können. Wenden Sie sich an Ihren Organisationsadministrator, wenn Sie derzeit keinen Zugriff auf den Arbeitsbereich [!UICONTROL Abfragen] haben.

>[!TIP]
>
>[!DNL Anaconda Navigator] ist eine grafische Desktop-Benutzeroberfläche (GUI), die eine einfachere Möglichkeit bietet, gängige [!DNL Python]-Programme wie [!DNL Jupyter Notebook] zu installieren und zu starten. Es hilft auch, Pakete, Umgebungen und Kanäle zu verwalten, ohne Befehlszeilenbefehle zu verwenden.
>Folgen Sie dem geleiteten Installationsprozess auf ihrer Website, um [Ihre bevorzugte Version der Anwendung zu installieren](https://docs.anaconda.com/anaconda/install/).
>Wählen Sie im Startbildschirm des Anaconda Navigators in der Liste der unterstützten Anwendungen die Option **[!DNL Jupyter Notebook]** aus, um das Programm zu starten.
>Weitere Informationen finden Sie in der [offiziellen Anaconda-Dokumentation](https://docs.anaconda.com/anaconda/navigator/).

Die offizielle Jupyter-Dokumentation enthält Anweisungen zum [Ausführen des Notebooks über die Befehlszeilenschnittstelle](https://docs.jupyter.org/en/latest/running.html#how-do-i-open-a-specific-notebook) (CLI).

## Launch [!DNL Jupyter Notebook]

Nachdem Sie eine neue [!DNL Jupyter Notebook] -Webanwendung geöffnet haben, wählen Sie in der Benutzeroberfläche das Dropdown-Menü **[!DNL New]** aus, gefolgt von **[!DNL Python 3]**, um ein neues Notebook zu erstellen. Der Editor [!DNL Notebook] wird angezeigt.

Geben Sie in der ersten Zeile des [!DNL Notebook]-Editors den folgenden Wert ein: `pip install psycopg2-binary` und wählen Sie **[!DNL Run]** in der Befehlsleiste aus. Eine Erfolgsmeldung wird unter der Eingabefelder angezeigt.

>[!IMPORTANT]
>
>Im Rahmen dieses Prozesses müssen Sie **[!DNL Run]** auswählen, um jede Codezeile auszuführen.

Importieren Sie als Nächstes einen [!DNL PostgreSQL] Datenbankadapter für [!DNL Python]. Geben Sie den Wert ein: `import psycopg2`und wählen Sie **[!DNL Run]** aus. Für diesen Prozess gibt es keine Erfolgsmeldung. Wenn keine Fehlermeldung vorhanden ist, fahren Sie mit dem nächsten Schritt fort.

Sie müssen jetzt Ihre Adobe Experience Platform-Anmeldeinformationen angeben, indem Sie den Wert eingeben: `conn = psycopg2.connect("{YOUR_CREDENTIALS}")`. Ihre Verbindungsberechtigungen finden Sie im Abschnitt [!UICONTROL Abfragen] auf der Registerkarte [!UICONTROL Anmeldedaten] der Platform-Benutzeroberfläche. Detaillierte Anweisungen finden Sie in der Dokumentation zum Auffinden Ihrer Organisationsberechtigungen ](../ui/credentials.md) .[

Die Verwendung von nicht ablaufenden Anmeldeinformationen wird empfohlen, wenn Sie Clients von Drittanbietern verwenden, um das wiederholte Eingeben Ihrer Details zu vermeiden. Anweisungen zum Generieren und Verwenden von nicht ablaufenden Anmeldedaten finden Sie in der Dokumentation [.](../ui/credentials.md#non-expiring-credentials)

>[!IMPORTANT]
>
>Beim Kopieren von Anmeldeinformationen aus der Platform-Benutzeroberfläche ist keine zusätzliche Formatierung der Anmeldeinformationen erforderlich. Sie können in einer Zeile angegeben werden, wobei zwischen den Eigenschaften und Werten nur ein Leerzeichen steht. Die Anmeldeinformationen sind in Anführungszeichen und durch Kommas getrennt **nicht**.

```python
conn = psycopg2.connect('''sslmode=require host=<YOUR_HOST_CREDENTIAL> port=80 dbname=prod:all user=<YOUR_ORGANIZATION_ID> password=<YOUR_PASSWORD>''')"
```

Ihre [!DNL Jupyter Notebook] -Instanz ist jetzt mit Query Service verbunden.

## Beispielabfrageausführung

Nachdem Sie [!DNL Jupyter Notebook] mit Query Service verbunden haben, können Sie mithilfe Ihrer [!DNL Notebook] -Eingaben Abfragen an Ihren Datensätzen durchführen. Im folgenden Beispiel wird eine einfache Abfrage verwendet, um den Prozess zu demonstrieren.

Geben Sie die folgenden Werte ein:

```python
cur = conn.cursor()
cur.execute('''<YOUR_QUERY_HERE>''')
data = [r for r in cur]
```

Rufen Sie als Nächstes den Parameter (`data` im obigen Beispiel) auf, um die Abfrageergebnisse in einer unformatierten Antwort anzuzeigen.

Verwenden Sie die folgenden Befehle, um die Ergebnisse für Menschen lesbarer zu formatieren:

- `colnames = [desc[0] for desc in cur.description]`
- `import pandas as pd`
- `import numpy as np`
- `df = pd.DataFrame(samples,columns=colnames)`
- `df.fillna(0,inplace=True)`

Diese Befehle generieren keine Erfolgsmeldung. Wenn keine Fehlermeldung angezeigt wird, können Sie eine Funktion verwenden, um die Ergebnisse Ihrer SQL-Abfrage in einem Tabellenformat auszugeben.

Geben Sie die Funktion `df.head()` ein und führen Sie sie aus, um die tabellarisierten Abfrageergebnisse anzuzeigen.

## Nächste Schritte

Nachdem Sie mit Query Service verbunden sind, können Sie mit [!DNL Jupyter Notebook] Abfragen schreiben. Weitere Informationen dazu, wie Sie Abfragen formulieren und ausführen, finden Sie im Handbuch zum Thema [Ausführen von Abfragen](../best-practices/writing-queries.md).
