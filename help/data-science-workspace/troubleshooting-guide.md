---
keywords: Experience Platform;troubleshooting;Data Science Workspace;popular topics
solution: Experience Platform
title: Data Science Workspace - Anleitung zur Fehlerbehebung
topic: Troubleshooting
translation-type: tm+mt
source-git-commit: 1447196da7dbf59c1f498de40f12ed74c328c0e6
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 0%

---


# Data Science Workspace - Anleitung zur Fehlerbehebung

In diesem Dokument finden Sie Antworten auf häufig gestellte Fragen zum Adobe Experience Platform Data Science Workspace. Fragen und Fehlerbehebung zu Plattform-APIs im Allgemeinen finden Sie im Handbuch zur Fehlerbehebung für die [Adobe Experience Platform-APIs](../landing/troubleshooting.md).

## JupyterLab-Umgebung wird in Google Chrome nicht geladen

>[!IMPORTANT] Dieses Problem wurde behoben, könnte aber weiterhin im Browser Google Chrome 80.x vorhanden sein. Stellen Sie sicher, dass Ihr Chrome-Browser auf dem neuesten Stand ist.

Bei der Google Chrome-Browserversion 80.x werden alle Drittanbieter-Cookies standardmäßig blockiert. Diese Richtlinie kann verhindern, dass JupyterLab in Adobe Experience Platform geladen wird.

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

Safari deaktiviert Cookies von Drittanbietern standardmäßig in Safari &lt; 12. Da sich Ihre virtuelle Jupyter-Computerinstanz in einer anderen Domäne befindet als der übergeordnete Rahmen, erfordert Adobe Experience Platform derzeit die Aktivierung von Drittanbieter-Cookies. Aktivieren Sie Drittanbieter-Cookies oder wechseln Sie zu einem anderen Browser wie Google Chrome.

Für Safari 12 müssen Sie Ihren Benutzeragent auf &quot;Chrome&quot;oder &quot;Firefox&quot;umstellen. Um den Benutzeragent zu wechseln, öffnen Sie das *Safari* -Menü und wählen Sie &quot; **Voreinstellungen&quot;**. Das Fenster &quot;Voreinstellungen&quot;wird angezeigt.

![Safari-Voreinstellungen](./images/faq/preferences.png)

Wählen Sie im Fenster &quot;Safari-Voreinstellungen&quot;die Option **Erweitert**. Markieren Sie dann das Menü &quot;Entwicklung *anzeigen&quot;in der Menüleiste* . Nach Abschluss dieses Schritts können Sie das Fenster &quot;Voreinstellungen&quot;schließen.

![Safari Advanced](./images/faq/advanced.png)

Wählen Sie dann in der oberen Navigationsleiste das Menü &quot; **Entwicklung** &quot;aus. Bewegen Sie den Mauszeiger über den *Benutzeragent* im Dropdownmenü *Entwickeln*. Sie können die **Chrome** - oder **Firefox** -Benutzeragenten-Zeichenfolge auswählen, die Sie verwenden möchten.

![Entwicklungsmenü](./images/faq/user-agent.png)

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

Weitere Informationen zur Spark-Clusterressourcenkonfiguration, einschließlich der vollständigen Liste konfigurierbarer Eigenschaften, finden Sie im [JupyterLab-Benutzerhandbuch](./jupyterlab/overview.md#kernels).