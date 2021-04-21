---
keywords: Experience Platform;Fehlerbehebung;Data Science Workspace;beliebte Themen
solution: Experience Platform
title: Data Science Workspace - Fehlerbehebungshandbuch
topic-legacy: Troubleshooting
description: Dieses Dokument beantwortet häufig gestellte Fragen zum Adobe Experience Platform Data Science Workspace.
exl-id: fbc5efdc-f166-4000-bde2-4aa4b0318b38
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 1%

---

# [!DNL Data Science Workspace] Handbuch zur Fehlerbehebung

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu Adobe Experience Platform [!DNL Data Science Workspace]. Fragen und Fehlerbehebung zu [!DNL Platform]-APIs im Allgemeinen finden Sie im Handbuch [Adobe Experience Platform API zur Fehlerbehebung](../landing/troubleshooting.md).

## [!DNL JupyterLab] Umgebung wird nicht geladen in  [!DNL Google Chrome]

>[!IMPORTANT]
>
>Dieses Problem wurde behoben, könnte aber weiterhin im Browser Google Chrome 80.x vorhanden sein. Stellen Sie sicher, dass Ihr Chrome-Browser auf dem neuesten Stand ist.

Bei der Browser-Version 80.x sind alle Drittanbieter-Cookies standardmäßig blockiert. [!DNL Google Chrome] Diese Richtlinie kann verhindern, dass [!DNL JupyterLab] in Adobe Experience Platform geladen wird.

Gehen Sie wie folgt vor, um dieses Problem zu beheben:

Navigieren Sie in Ihrem [!DNL Chrome]-Browser nach oben rechts und wählen Sie **Einstellungen** (alternativ können Sie &quot;chrome://settings/&quot;kopieren und in die Adressleiste einfügen). Führen Sie anschließend einen Bildlauf zum unteren Rand der Seite durch und klicken Sie auf das Dropdown-Menü **Erweitert**.

![Chrome Advanced](./images/faq/chrome-advanced.png)

Der Abschnitt **Datenschutz und Sicherheit** wird angezeigt. Klicken Sie anschließend auf **Site-Einstellungen**, gefolgt von **Cookies und Site-Daten**.

![Chrome Advanced](./images/faq/privacy-security.png)

![Chrome Advanced](./images/faq/cookies.png)

Schalten Sie schließlich &quot;Drittanbieter-Cookies blockieren&quot;auf &quot;AUS&quot;.

![Chrome Advanced](./images/faq/toggle-off.png)

>[!NOTE]
>
>Alternativ können Sie Drittanbieter-Cookies deaktivieren und [* hinzufügen.]ds.adobe.net zur Zulassungsliste hinzugefügt.

Navigieren Sie in Ihrer Adressleiste zu &quot;chrome://flags/&quot;. Suchen und deaktivieren Sie das Flag *&quot;SameSite by default cookies&quot;*, indem Sie das Dropdown-Menü auf der rechten Seite verwenden.

![samesite-Flag deaktivieren](./images/faq/samesite-flag.png)

Nach Schritt 2 werden Sie aufgefordert, Ihren Browser neu zu starten. Nach dem Neustart sollte [!DNL Jupyterlab] barrierefrei sein.

## Warum kann ich in Safari nicht auf [!DNL JupyterLab] zugreifen?

Safari deaktiviert Cookies von Drittanbietern standardmäßig in Safari &lt; 12. Da sich Ihre [!DNL Jupyter] virtuelle Computerinstanz in einer anderen Domäne befindet als der übergeordnete Frame, erfordert Adobe Experience Platform derzeit die Aktivierung von Drittanbieter-Cookies. Bitte aktivieren Sie Drittanbieter-Cookies oder wechseln Sie zu einem anderen Browser wie [!DNL Google Chrome].

Für Safari 12 müssen Sie Ihren Benutzeragent auf &quot;[!DNL Chrome]&quot;oder &quot;[!DNL Firefox]&quot;umstellen. Um den Benutzeragent zu wechseln, öffnen Sie den Beginn im Menü *Safari* und wählen Sie **Voreinstellungen**. Das Fenster &quot;Voreinstellungen&quot;wird angezeigt.

![Safari-Voreinstellungen](./images/faq/preferences.png)

Wählen Sie im Fenster &quot;Safari-Voreinstellungen&quot;die Option **Erweitert**. Markieren Sie dann das Menü *Entwicklung anzeigen in der Menüleiste*. Nach Abschluss dieses Schritts können Sie das Fenster &quot;Voreinstellungen&quot;schließen.

![Safari Advanced](./images/faq/advanced.png)

Wählen Sie dann in der oberen Navigationsleiste das Menü **Entwicklung**. Bewegen Sie den Mauszeiger über das Dropdownmenü **Entwicklung** und bewegen Sie den Mauszeiger über **Benutzeragent**. Sie können die **[!DNL Chrome]**- oder **[!DNL Firefox]**-Benutzeragenten-Zeichenfolge auswählen, die Sie verwenden möchten.

![Entwicklungsmenü](./images/faq/user-agent.png)

## Warum wird beim Versuch, eine Datei in [!DNL JupyterLab] hochzuladen oder zu löschen, die Meldung &#39;403 Verboten&#39; angezeigt?

Wenn Ihr Browser mit Software zum Sperren von Anzeigen wie [!DNL Ghostery] oder [!DNL AdBlock] Plus aktiviert ist, muss die Domäne &quot;\*.adobe.net&quot;in jeder Software zum Sperren von Anzeigen für [!DNL JupyterLab] zugelassen werden, damit  normal funktioniert. Der Grund dafür ist, dass virtuelle Computer unter einer anderen Domäne als [!DNL Experience Platform] ausgeführt werden.[!DNL JupyterLab]

## Warum sehen einige Teile meines [!DNL Jupyter Notebook] verwirrt aus oder werden nicht als Code gerendert?

Dies kann vorkommen, wenn die betreffende Zelle versehentlich von &quot;Code&quot;in &quot;Markup&quot;geändert wird. Während eine Codezelle fokussiert ist, ändert sich durch Drücken der Tastenkombination **ESC+M** der Zellentyp in Markdown. Der Zelltyp kann durch die Dropdown-Liste oben im Notebook für die ausgewählte(n) Zelle(n) geändert werden. Um einen Zellentyp in Code zu ändern, wählen Sie die zu ändernde Zelle aus, indem Sie den Beginn auswählen. Klicken Sie anschließend auf das Dropdown-Menü, das den aktuellen Zellentyp angibt, und wählen Sie dann &quot;Code&quot;.

![](./images/faq/code_type.png)

## Wie installiere ich benutzerdefinierte [!DNL Python] Bibliotheken?

Der [!DNL Python]-Kernel wird mit vielen gängigen maschinellen Lernbibliotheken vorinstalliert. Sie können jedoch zusätzliche benutzerdefinierte Bibliotheken installieren, indem Sie den folgenden Befehl in einer Codezelle ausführen:

```shell
!pip install {LIBRARY_NAME}
```

Eine vollständige Liste der vorinstallierten [!DNL Python]-Bibliotheken finden Sie im Abschnitt [Anhang des JupyterLab-Benutzerhandbuchs](./jupyterlab/overview.md#supported-libraries).

## Kann ich benutzerdefinierte PySpark-Bibliotheken installieren?

Leider können Sie keine zusätzlichen Bibliotheken für den PySpark-Kernel installieren. Sie können sich jedoch an Ihren Kundenbetreuer wenden, um benutzerdefinierte PySpark-Bibliotheken für Sie zu installieren.

Eine Liste vorinstallierter PySpark-Bibliotheken finden Sie im Abschnitt [Anhang des JupyterLab-Benutzerhandbuchs](./jupyterlab/overview.md#supported-libraries).

## Ist es möglich, [!DNL Spark] Cluster-Ressourcen für [!DNL JupyterLab] [!DNL Spark]- oder PySpark-Kernel zu konfigurieren?

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

Weitere Informationen zur Clusterressourcenkonfiguration, einschließlich der vollständigen Liste konfigurierbarer Eigenschaften, finden Sie im [JupyterLab Benutzerhandbuch](./jupyterlab/overview.md#kernels).[!DNL Spark]

## Warum erhalte ich eine Fehlermeldung, wenn ich versuche, bestimmte Aufgaben für größere Datensätze auszuführen?

Wenn Sie einen Fehler aus einem Grund wie `Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.` erhalten, bedeutet das in der Regel, dass dem Treiber oder einem ausführenden Programm der Arbeitsspeicher ausgeht. Weitere Informationen zu Datenbeschränkungen und zum Ausführen von Aufgaben für große Datensätze finden Sie in der Dokumentation zu JupyterLab-Notebooks [Datenzugriff](./jupyterlab/access-notebook-data.md). Normalerweise kann dieser Fehler durch Ändern von `mode` von `interactive` in `batch` behoben werden.

## [!DNL Docker Hub] Beschränkungen im Data Science Workspace

Seit dem 20. November 2020 gelten für die anonyme und kostenlose Nutzung von Docker Hub Preislimits. Anonyme und kostenlose [!DNL Docker Hub]-Benutzer sind auf 100 Container-Bildabruf-Anfragen alle sechs Stunden beschränkt. Wenn Sie von diesen Änderungen betroffen sind, erhalten Sie folgende Fehlermeldung: `ERROR: toomanyrequests: Too Many Requests.` oder `You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`.

Derzeit betrifft diese Beschränkung nur Ihre Organisation, wenn Sie innerhalb von sechs Stunden versuchen, 100 Rezepte-Notizbücher zu erstellen, oder wenn Sie in Data Science Workspace auf Spark-basierten Notebooks zugreifen, die häufig nach oben oder unten skaliert werden. Dies ist jedoch unwahrscheinlich, da der Cluster, auf dem diese ausgeführt werden, zwei Stunden lang aktiv bleibt, bevor er ausgeschaltet wird. Auf diese Weise wird die Anzahl der Pulle verringert, die erforderlich sind, wenn der Cluster aktiv ist. Wenn Sie einen der oben genannten Fehler erhalten, müssen Sie warten, bis Ihr [!DNL Docker]-Limit zurückgesetzt wird.

Weitere Informationen zu den Ratenbeschränkungen für [!DNL Docker Hub] finden Sie in der [DockerHub-Dokumentation](https://www.docker.com/increase-rate-limits). Eine Lösung hierfür wird derzeit in einer späteren Version erarbeitet und erwartet.
