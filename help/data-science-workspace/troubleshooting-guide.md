---
keywords: Experience Platform;troubleshooting;Data Science Workspace;popular topics
solution: Experience Platform
title: Data Science Workspace - Anleitung zur Fehlerbehebung
topic: Troubleshooting
translation-type: tm+mt
source-git-commit: 1f756e7bc71c9ff227757aee64af29e0772c24af

---


# Data Science Workspace - Anleitung zur Fehlerbehebung

In diesem Dokument finden Sie Antworten auf häufig gestellte Fragen zum Adobe Experience Platform Data Science Workspace. Fragen und Fehlerbehebung zu Plattform-APIs im Allgemeinen finden Sie im Handbuch zur Fehlerbehebung für die [Adobe Experience Platform-APIs](../landing/troubleshooting.md).

## JupyterLab-Umgebung wird in Google Chrome nicht geladen

Mit der neuesten Aktualisierung des Google Chrome-Browsers auf Version 80.x werden alle Drittanbieter-Cookies standardmäßig blockiert. Diese neue Richtlinie kann verhindern, dass JupyterLab in Adobe Experience Platform geladen wird.

>[!NOTE] Das ist ein vorübergehendes Problem. Die Abhängigkeit von Drittanbieter-Cookies wird in einer zukünftigen Version entfernt.

Gehen Sie wie folgt vor, um dieses Problem zu beheben:

Navigieren Sie in Ihrem Chrome-Browser oben rechts und wählen Sie **Einstellungen** (alternativ können Sie &quot;chrome://settings/&quot;kopieren und in die Adressleiste einfügen). Führen Sie anschließend einen Bildlauf zum unteren Rand der Seite durch und klicken Sie auf das Dropdownmenü **Erweitert** .

![Chrome Advanced](./images/faq/chrome-advanced.png)

Der Abschnitt *Datenschutz und Sicherheit* wird angezeigt. Klicken Sie anschließend auf **Site-Einstellungen** , gefolgt von **Cookies und Site-Daten**.

![Chrome Advanced](./images/faq/privacy-security.png)

![Chrome Advanced](./images/faq/cookies.png)

Schalten Sie schließlich &quot;Drittanbieter-Cookies blockieren&quot;auf &quot;AUS&quot;.

![Chrome Advanced](./images/faq/toggle-off.png)

>[!NOTE] Alternativ können Sie Drittanbieter-Cookies und Whitelist [* deaktivieren.]ds.adobe.net

Navigieren Sie in Ihrer Adressleiste zu &quot;chrome://flags/&quot;. Suchen und deaktivieren Sie das Flag *&quot;SameSite by default cookies&quot;* über das Dropdown-Menü rechts.

![samesite-Flag deaktivieren](./images/faq/samesite-flag.png)

Nach Schritt 2 werden Sie aufgefordert, Ihren Browser neu zu starten. Nach dem Neustart sollte auf Jupyterlab zugegriffen werden können.

## Warum kann ich nicht auf JupyterLab in Safari zugreifen?

Safari deaktiviert Cookies von Drittanbietern standardmäßig. Da sich Ihre virtuelle Jupyter-Computerinstanz in einer anderen Domäne befindet als der übergeordnete Rahmen, erfordert Adobe Experience Platform derzeit die Aktivierung von Drittanbieter-Cookies. Aktivieren Sie Drittanbieter-Cookies oder wechseln Sie zu einem anderen Browser wie Google Chrome.

## Warum wird beim Versuch, eine Datei in JupyterLab hochzuladen oder zu löschen, die Meldung &quot;403 Verboten&quot;angezeigt?

Wenn Ihr Browser mit einer Werbeblockiersoftware wie Ghostery oder AdBlock Plus aktiviert ist, muss die Domäne &quot;\*.adobe.net&quot;in jeder Werbeblockiersoftware auf die Positivliste gesetzt werden, damit JupyterLab normal funktioniert. Dies liegt daran, dass virtuelle JupyterLab-Computer unter einer anderen Domäne als die Experience Platform-Domäne ausgeführt werden.

## Warum sehen einige Teile meines Jupyter-Notebooks verwirrt aus oder werden nicht als Code gerendert?

Dies kann vorkommen, wenn die betreffende Zelle versehentlich von &quot;Code&quot;in &quot;Markup&quot;geändert wird. Während eine Codezelle fokussiert ist, ändert sich durch Drücken der Tastenkombination **ESC+M** der Zellentyp in Markdown. Der Zelltyp kann durch die Dropdown-Liste oben im Notebook für die ausgewählte(n) Zelle(n) geändert werden. Um einen Zellentyp in Code zu ändern, wählen Sie die zu ändernde Zelle aus, indem Sie den Beginn auswählen. Klicken Sie anschließend auf das Dropdown-Menü, das den aktuellen Zellentyp angibt, und wählen Sie dann &quot;Code&quot;.

![](./images/faq/code_type.png)

## Wie installiere ich benutzerdefinierte Python-Bibliotheken?

Der Python-Kernel wird mit vielen gängigen Maschinen-Lernbibliotheken vorinstalliert. Sie können jedoch zusätzliche benutzerdefinierte Bibliotheken installieren, indem Sie den folgenden Befehl in einer Codezelle ausführen:

```shell
!pip install {LIBRARY_NAME}
```

Eine vollständige Liste vorinstallierter Python-Bibliotheken finden Sie im JupyterLab- [Benutzerhandbuch](./jupyterlab/overview.md#supported-libraries)im Anhang.

## Kann ich benutzerdefinierte PySpark-Bibliotheken installieren?

Leider können Sie keine zusätzlichen Bibliotheken für den PySpark-Kernel installieren. Sie können sich jedoch an Ihren Adobe-Kundendienstmitarbeiter wenden, um benutzerdefinierte PySpark-Bibliotheken für Sie zu installieren.

Eine Liste vorinstallierter PySpark-Bibliotheken finden Sie im [Anhang des JupyterLab-Benutzerhandbuchs](./jupyterlab/overview.md#supported-libraries).

## Kann man Spark-Cluster-Ressourcen für JupyterLab Spark oder PySpark-Kernel konfigurieren?

Sie können Ressourcen konfigurieren, indem Sie den folgenden Block zur ersten Zelle Ihres Notebooks hinzufügen:

```python
%%configure -f 
{
    "numExecutors": 10,
    "executorMemory": "8G",
    "executorCores":4,
    "driverMemory":"2G",
    "driverCores":2,
    "conf": {
        "spark.cores.max": "40"
    }
}
```

Weitere Informationen zur Spark-Clusterressourcenkonfiguration, einschließlich der vollständigen Liste konfigurierbarer Eigenschaften, finden Sie im [JupyterLab-Benutzerhandbuch](./jupyterlab/overview.md#pyspark-spark-execution-resource).