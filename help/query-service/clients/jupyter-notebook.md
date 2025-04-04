---
title: Verbinden von Jupyter Notebook mit dem Abfrage-Service
description: Erfahren Sie, wie Sie Jupyter Notebook mit dem Abfrage-Service von Adobe Experience Platform verbinden.
exl-id: 358eab67-538f-4ada-931f-783b92db4a1c
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 4%

---

# Verbinden von [!DNL Jupyter Notebook] mit dem Abfrage-Service

In diesem Dokument werden die Schritte beschrieben, die zum Verbinden von [!DNL Jupyter Notebook] mit dem Abfrage-Service von Adobe Experience Platform erforderlich sind.

## Erste Schritte

Für dieses Handbuch müssen Sie bereits Zugriff auf [!DNL Jupyter Notebook] haben und mit dessen Benutzeroberfläche vertraut sein. Informationen zum Herunterladen von [!DNL Jupyter Notebook] oder weitere Informationen finden Sie unter [Official [!DNL Jupyter Notebook] Documentation](https://jupyter.org/).

Um die erforderlichen Anmeldeinformationen zum Verbinden von [!DNL Jupyter Notebook] mit Experience Platform zu erhalten, benötigen Sie Zugriff auf den Arbeitsbereich [!UICONTROL Abfragen] in der Experience Platform-Benutzeroberfläche. Wenden Sie sich an den Admin Ihrer Organisation, wenn Sie derzeit keinen Zugriff auf den Arbeitsbereich [!UICONTROL Abfragen] haben.

>[!TIP]
>
>[!DNL Anaconda Navigator] ist eine grafische Benutzeroberfläche (GUI) für Desktops, die eine einfachere Möglichkeit bietet, gängige [!DNL Python] wie [!DNL Jupyter Notebook] zu installieren und zu starten. Außerdem können Pakete, Umgebungen und Kanäle ohne Verwendung von Befehlszeilenbefehlen verwaltet werden.
>Folgen Sie dem geführten Installationsprozess auf der Website von [installieren Sie Ihre bevorzugte Version des Programms](https://docs.anaconda.com/anaconda/install/).
>Wählen Sie im Anaconda Navigator-Startbildschirm die Option **[!DNL Jupyter Notebook]** aus der Liste der unterstützten Programme, um das Programm zu starten.
>Weitere Informationen finden Sie in der [offiziellen Anaconda-Dokumentation](https://docs.anaconda.com/anaconda/navigator/).

Die offizielle Jupyter-Dokumentation enthält Anweisungen zum [Ausführen des Notebooks über die Befehlszeilenschnittstelle](https://docs.jupyter.org/en/latest/running.html#how-do-i-open-a-specific-notebook) (CLI).

## Launch [!DNL Jupyter Notebook]

Nachdem Sie eine neue [!DNL Jupyter Notebook]-Web-Anwendung geöffnet haben, wählen Sie das Dropdown-Menü **[!DNL New]** in der Benutzeroberfläche und dann **[!DNL Python 3]** aus, um ein neues Notebook zu erstellen. Der [!DNL Notebook] wird angezeigt.

Geben Sie in der ersten Zeile des [!DNL Notebook]-Editors den folgenden Wert ein: `pip install psycopg2-binary` und wählen Sie **[!DNL Run]** in der Befehlsleiste aus. Unterhalb der Eingabezeile wird eine Erfolgsmeldung angezeigt.

>[!IMPORTANT]
>
>Im Rahmen dieses Verbindungsprozesses müssen Sie **[!DNL Run]** auswählen, um jede Codezeile auszuführen.

Importieren Sie als Nächstes einen [!DNL PostgreSQL] Datenbankadapter für [!DNL Python]. Geben Sie den Wert ein: `import psycopg2`und wählen Sie **[!DNL Run]** aus. Es gibt keine Erfolgsmeldung für diesen Prozess. Wenn keine Fehlermeldung angezeigt wird, fahren Sie mit dem nächsten Schritt fort.

Sie müssen jetzt Ihre Adobe Experience Platform-Anmeldeinformationen angeben, indem Sie den Wert eingeben: `conn = psycopg2.connect("{YOUR_CREDENTIALS}")`. Ihre Anmeldeinformationen für die Verbindung finden Sie [!UICONTROL  Abschnitt ]Abfragen“ auf der Registerkarte [!UICONTROL Anmeldeinformationen] der Experience Platform-Benutzeroberfläche. Detaillierte Anweisungen finden Sie in der Dokumentation [ Suchen der ](../ui/credentials.md) Ihres Unternehmens .

Die Verwendung nicht ablaufender Anmeldeinformationen wird empfohlen, wenn Sie Drittanbieter-Clients verwenden, um sich die wiederholte Eingabe Ihrer Details zu ersparen. In der Dokumentation finden [ Anweisungen zum Generieren und Verwenden nicht ablaufender Anmeldeinformationen](../ui/credentials.md#non-expiring-credentials).

>[!IMPORTANT]
>
>Beim Kopieren von Anmeldeinformationen aus der Experience Platform-Benutzeroberfläche ist keine zusätzliche Formatierung der Anmeldeinformationen erforderlich. Sie können in einer Zeile angegeben werden, wobei ein einziges Leerzeichen zwischen den Eigenschaften und Werten besteht. Die Anmeldeinformationen werden in Anführungszeichen eingeschlossen und **nicht** durch Kommas getrennt.

```python
conn = psycopg2.connect('''sslmode=require host=<YOUR_HOST_CREDENTIAL> port=80 dbname=prod:all user=<YOUR_ORGANIZATION_ID> password=<YOUR_PASSWORD>''')"
```

Ihre [!DNL Jupyter Notebook] ist jetzt mit dem Abfrage-Service verbunden.

## Beispielhafte Abfrageausführung

Nachdem Sie nun [!DNL Jupyter Notebook] mit dem Abfrage-Service verbunden haben, können Sie mit Ihren [!DNL Notebook] Abfragen für Ihre Datensätze durchführen. Im folgenden Beispiel wird eine einfache Abfrage verwendet, um den Prozess zu demonstrieren.

Geben Sie die folgenden Werte ein:

```python
cur = conn.cursor()
cur.execute('''<YOUR_QUERY_HERE>''')
data = [r for r in cur]
```

Rufen Sie anschließend den Parameter auf (`data` im obigen Beispiel), um die Abfrageergebnisse in einer unformatierten Antwort anzuzeigen.

Um die Ergebnisse besser lesbar zu formatieren, verwenden Sie die folgenden Befehle:

- `colnames = [desc[0] for desc in cur.description]`
- `import pandas as pd`
- `import numpy as np`
- `df = pd.DataFrame(samples,columns=colnames)`
- `df.fillna(0,inplace=True)`

Diese Befehle erzeugen keine Erfolgsmeldung. Wenn keine Fehlermeldung vorliegt, können Sie eine Funktion verwenden, um die Ergebnisse Ihrer SQL-Abfrage in einem Tabellenformat auszugeben.

Geben Sie die Funktion `df.head()` ein und führen Sie sie aus, um die tabellarischen Abfrageergebnisse anzuzeigen.

## Nächste Schritte

Nachdem Sie sich mit dem Abfrage-Service verbunden haben, können Sie [!DNL Jupyter Notebook] verwenden, um Abfragen zu schreiben. Weitere Informationen dazu, wie Sie Abfragen formulieren und ausführen, finden Sie im Handbuch zum Thema [Ausführen von Abfragen](../best-practices/writing-queries.md).
