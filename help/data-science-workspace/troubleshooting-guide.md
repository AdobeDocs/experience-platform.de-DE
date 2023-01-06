---
keywords: Experience Platform; Fehlerbehebung; Data Science Workspace; beliebte Themen
solution: Experience Platform
title: Data Science Workspace - Anleitung zur Fehlerbehebung
description: Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu Adobe Experience Platform Data Science Workspace.
exl-id: fbc5efdc-f166-4000-bde2-4aa4b0318b38
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 0%

---

# [!DNL Data Science Workspace] Handbuch zur Fehlerbehebung

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu Adobe Experience Platform [!DNL Data Science Workspace]. Für Fragen und zur Fehlerbehebung in [!DNL Platform] Allgemeine APIs finden Sie unter [Handbuch zur Fehlerbehebung bei Adobe Experience Platform API](../landing/troubleshooting.md).

## JupyterLab Notebook-Abfragestatus im Ausführungsstatus stecken geblieben

Ein JupyterLab Notebook kann darauf hinweisen, dass sich eine Zelle in einigen Speicherbedingungen unbegrenzt im Ausführungsstatus befindet. Wenn Sie beispielsweise einen großen Datensatz abfragen oder mehrere nachfolgende Abfragen ausführen, kann dem JupyterLab-Notebook der verfügbare Speicher zum Speichern des resultierenden Dataframe-Objekts ausgehen. Es gibt einige Indikatoren, die in dieser Situation zu sehen sind. Zunächst wechselt der Kernel in den Leerlauf-Status, obwohl die Zelle als Ausführung angezeigt wird, wie durch die [`*`] neben der Zelle. Darüber hinaus gibt die untere Leiste die Menge des verwendeten/verfügbaren RAM an.

![Verfügbarer Speicher](./images/jupyterlab/user-guide/allocate-ram.png)

Während der Datenausgabe kann der Speicher anwachsen, bis er Ihren maximal zugewiesenen Speicher erreicht. Der Speicher wird freigegeben, sobald der maximale Speicher erreicht ist und der Kernel neu gestartet wird. Dies bedeutet, dass der verwendete Speicher in diesem Szenario aufgrund des Neustart des Kernels sehr gering sein kann, während der Speicher kurz vor dem Neustart sehr nahe am maximal zugewiesenen RAM lag.

Um dieses Problem zu beheben, wählen Sie das Zahnradsymbol oben rechts in JupyterLab aus und schieben Sie den Schieberegler nach rechts, gefolgt von der Auswahl **[!UICONTROL Konfigurationen aktualisieren]** um mehr RAM zuzuweisen. Wenn Sie mehrere Abfragen ausführen und sich Ihr RAM-Wert dem maximal zugewiesenen Betrag nähert, es sei denn, Sie benötigen die Ergebnisse früherer Abfragen, starten Sie den Kernel neu, um die verfügbare RAM-Menge zurückzusetzen. Dadurch wird sichergestellt, dass die maximale RAM-Menge für die aktuelle Abfrage verfügbar ist.

![mehr Diagramm zuweisen](./images/jupyterlab/user-guide/notebook-gpu-config.png)

Wenn Sie die maximale Speicherkapazität (RAM) zuweisen und dieses Problem weiterhin beheben, können Sie Ihre Abfrage so ändern, dass sie mit einer kleineren Datensatzgröße arbeitet, indem Sie die Spalten oder den Datenbereich reduzieren. Um die gesamte Datenmenge zu nutzen, wird empfohlen, ein Spark-Notebook zu verwenden.

## [!DNL JupyterLab] -Umgebung wird nicht in geladen [!DNL Google Chrome]

>[!IMPORTANT]
>
>Dieses Problem wurde behoben, konnte jedoch im Google Chrome 80.x-Browser noch vorhanden sein. Stellen Sie sicher, dass Ihr Chrome-Browser aktuell ist.

Mit dem [!DNL Google Chrome] Browserversion 80.x, sind alle Drittanbieter-Cookies standardmäßig blockiert. Diese Richtlinie kann [!DNL JupyterLab] aus dem Laden in Adobe Experience Platform.

Gehen Sie wie folgt vor, um dieses Problem zu beheben:

In [!DNL Chrome] Browser, navigieren Sie oben rechts und wählen Sie **Einstellungen** (Alternativ können Sie &quot;chrome://settings/&quot; kopieren und in die Adressleiste einfügen). Scrollen Sie dann zum unteren Seitenrand und klicken Sie auf die Schaltfläche **Erweitert** Dropdown-Liste.

![Chrome Advanced](./images/faq/chrome-advanced.png)

Die **Datenschutz und Sicherheit** angezeigt. Klicken Sie anschließend auf **Site-Einstellungen** gefolgt von **Cookies und Site-Daten**.

![Chrome Advanced](./images/faq/privacy-security.png)

![Chrome Advanced](./images/faq/cookies.png)

Schalten Sie abschließend &quot;Drittanbieter-Cookies blockieren&quot;in &quot;AUS&quot;.

![Chrome Advanced](./images/faq/toggle-off.png)

>[!NOTE]
>
>Alternativ können Sie Drittanbieter-Cookies deaktivieren und [*.]ds.adobe.net zur Zulassungsliste hinzugefügt.

Navigieren Sie in Ihrer Adressleiste zu &quot;chrome://flags/&quot;. Suchen und deaktivieren Sie das Flag mit dem Titel *&quot;Standard-SameSite-Cookies&quot;* über das Dropdown-Menü rechts.

![SameSite-Markierung deaktivieren](./images/faq/samesite-flag.png)

Nach Schritt 2 werden Sie aufgefordert, Ihren Browser neu zu starten. Nach dem Neustart [!DNL Jupyterlab] sollte zugänglich sein.

## Warum kann ich nicht zugreifen [!DNL JupyterLab] in Safari?

Safari deaktiviert in Safari &lt; 12 standardmäßig Drittanbieter-Cookies. Da [!DNL Jupyter] Virtual Machine-Instanz befindet sich in einer anderen Domäne als der übergeordnete Frame. Für Adobe Experience Platform ist derzeit die Aktivierung von Drittanbieter-Cookies erforderlich. Aktivieren Sie Drittanbieter-Cookies oder wechseln Sie zu einem anderen Browser, z. B. [!DNL Google Chrome].

Für Safari 12 müssen Sie Ihren Benutzeragenten auf &quot;[!DNL Chrome]&#39; or &#39;[!DNL Firefox]&quot;. Um Ihren Benutzeragenten zu wechseln, öffnen Sie zunächst das *Safari* Menü und wählen Sie **Voreinstellungen**. Das Fenster Voreinstellungen wird angezeigt.

![Safari-Voreinstellungen](./images/faq/preferences.png)

Wählen Sie im Fenster der Safari-Voreinstellungen die Option **Erweitert**. Überprüfen Sie dann die *Menü &quot;Entwickeln&quot;in der Menüleiste anzeigen* ankreuzen. Sie können das Fenster mit den Voreinstellungen schließen, nachdem dieser Schritt abgeschlossen ist.

![Safari Advanced](./images/faq/advanced.png)

Wählen Sie als Nächstes in der oberen Navigationsleiste die **Entwickeln** Menü. Von innerhalb der **Entwickeln** Dropdown, herüber fahren **Benutzeragent**. Sie können die **[!DNL Chrome]** oder **[!DNL Firefox]** Benutzeragenten-Zeichenfolge, die Sie verwenden möchten.

![Menü &quot;Entwickeln&quot;](./images/faq/user-agent.png)

## Warum wird mir beim Versuch, eine Datei in hochzuladen oder zu löschen, die Meldung &quot;403 Verboten&quot;angezeigt? [!DNL JupyterLab]?

Wenn Ihr Browser mit Advertising-Blocker-Software wie [!DNL Ghostery] oder [!DNL AdBlock] Außerdem muss die Domäne &quot;\*.adobe.net&quot;in jeder Software zur Werbeblockierung für [!DNL JupyterLab] für den normalen Betrieb. Dies liegt daran, dass [!DNL JupyterLab] virtuelle Maschinen werden auf einer anderen Domäne als der [!DNL Experience Platform] Domäne.

## Warum mache ich einige Teile meiner [!DNL Jupyter Notebook] Sehen Sie verwirrt aus oder werden Sie nicht als Code gerendert?

Dies kann vorkommen, wenn die betreffende Zelle versehentlich von &quot;Code&quot;in &quot;Markdown&quot;geändert wird. Während eine Codezelle fokussiert ist, drücken Sie die Tastenkombination **ESC+M** ändert den Zelltyp in Markdown. Der Zelltyp kann durch die Dropdown-Anzeige oben im Notebook für die ausgewählten Zellen geändert werden. Um einen Zellentyp in Code zu ändern, wählen Sie zunächst die Zelle aus, die Sie ändern möchten. Klicken Sie anschließend auf das Dropdown-Menü, das den aktuellen Zellentyp angibt, und wählen Sie &quot;Code&quot;.

![](./images/faq/code_type.png)

## Wie installiere ich benutzerdefinierte [!DNL Python] Bibliotheken?

Die [!DNL Python] Kernel wird mit vielen gängigen Bibliotheken für maschinelles Lernen vorinstalliert. Sie können jedoch zusätzliche benutzerdefinierte Bibliotheken installieren, indem Sie den folgenden Befehl in einer Code-Zelle ausführen:

```shell
!pip install {LIBRARY_NAME}
```

Für eine vollständige Liste der vorinstallierten [!DNL Python] -Bibliotheken, siehe [Anhang des JupyterLab-Benutzerhandbuchs](./jupyterlab/overview.md#supported-libraries).

## Kann ich benutzerdefinierte PySpark-Bibliotheken installieren?

Leider können Sie keine zusätzlichen Bibliotheken für den PySpark-Kernel installieren. Sie können sich jedoch an Ihren Kundenbetreuer von Adobe wenden, um für Sie benutzerdefinierte PySpark-Bibliotheken zu installieren.

Eine Liste der vorinstallierten PySpark-Bibliotheken finden Sie unter [Anhang des JupyterLab-Benutzerhandbuchs](./jupyterlab/overview.md#supported-libraries).

## Ist es möglich, [!DNL Spark] Clusterressourcen für [!DNL JupyterLab] [!DNL Spark] oder PySpark-Kernel?

Sie können Ressourcen konfigurieren, indem Sie der ersten Zelle Ihres Notebooks den folgenden Block hinzufügen:

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

Weitere Informationen finden Sie unter [!DNL Spark] Die Konfiguration der Clusterressource, einschließlich der vollständigen Liste der konfigurierbaren Eigenschaften, finden Sie in der [JupyterLab-Benutzerhandbuch](./jupyterlab/overview.md#kernels).

## Warum erhalte ich eine Fehlermeldung, wenn ich versuche, bestimmte Aufgaben für größere Datensätze auszuführen?

Wenn Sie einen Fehler aus einem Grund wie `Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.` Dies bedeutet normalerweise, dass dem Treiber oder einem Executor der Speicher ausgeht. Siehe JupyterLab Notebooks [Datenzugriff](./jupyterlab/access-notebook-data.md) Dokumentation finden Sie weitere Informationen zu Datenbeschränkungen und zur Ausführung von Aufgaben für große Datensätze. Normalerweise kann dieser Fehler durch Ändern der `mode` von `interactive` nach `batch`.

Außerdem sollten Sie beim Schreiben großer Spark-/PySpark-Datensätze Ihre Daten zwischenspeichern (`df.cache()`) vor dem Ausführen des Schreib-Codes kann die Leistung erheblich verbessern.

<!-- remove this paragraph at a later date once the sdk is updated -->

Wenn beim Lesen von Daten Probleme auftreten und Transformationen auf die Daten angewendet werden, versuchen Sie, die Daten vor den Transformationen zwischenzuspeichern. Das Zwischenspeichern Ihrer Daten verhindert mehrere Lesevorgänge im Netzwerk. Lesen Sie zunächst die Daten. Als Nächstes wird der Cache (`df.cache()`) die Daten. Führen Sie abschließend eine Transformation durch.

## Warum dauert es so lange, bis meine Spark-/PySpark-Notebooks Daten lesen und schreiben?

Wenn Sie Datenumwandlungen durchführen, z. B. mithilfe von `fit()`, können die Umwandlungen mehrmals ausgeführt werden. Um die Leistung zu steigern, zwischenspeichern Sie Ihre Daten mit `df.cache()` vor dem Ausführen der `fit()`. Dadurch wird sichergestellt, dass die Transformationen nur einmal ausgeführt werden und dass im Netzwerk mehrere Lesevorgänge verhindert werden.

**Empfohlene Bestellung:** Lesen Sie zunächst die Daten. Führen Sie als Nächstes Umwandlungen und dann Caching durch (`df.cache()`) die Daten. Führen Sie abschließend eine `fit()`.

## Warum werden meine Spark-/PySpark-Notebooks nicht ausgeführt?

Wenn Sie einen der folgenden Fehler erhalten:

- Vorgang aufgrund von Staging-Fehler abgebrochen ... Kann nur RDDs mit derselben Anzahl von Elementen in jeder Partition komprimieren.
- Remote RPC Client getrennt und andere Speicherfehler.
- Schlechte Leistung beim Lesen und Schreiben von Datensätzen.

Stellen Sie sicher, dass Sie die Daten zwischenspeichern (`df.cache()`) vor dem Schreiben der Daten. Beim Ausführen von Code in Notebooks verwenden Sie `df.cache()` vor einer Aktion wie `fit()` kann die Notebook-Leistung erheblich verbessern. Verwenden `df.cache()` vor dem Schreiben eines Datensatzes stellt sicher, dass die Transformationen nur einmal statt mehrmals ausgeführt werden.

## [!DNL Docker Hub] Beschränkungen in Data Science Workspace

Ab dem 20. November 2020 sind die Ratenbeschränkungen für die anonyme und kostenlose authentifizierte Verwendung von Docker Hub in Kraft getreten. Anonym und kostenlos [!DNL Docker Hub] -Benutzer sind alle sechs Stunden auf 100 Pull-Anforderungen für Containerbilder beschränkt. Wenn Sie von diesen Änderungen betroffen sind, erhalten Sie diese Fehlermeldung: `ERROR: toomanyrequests: Too Many Requests.` oder `You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`.

Derzeit wirkt sich diese Beschränkung nur auf Ihr Unternehmen aus, wenn Sie versuchen, innerhalb des sechsstündigen Zeitraums 100-Notebook-Rezepte zu erstellen oder wenn Sie Spark-basierte Notebooks in Data Science Workspace verwenden, die häufig nach oben und unten skaliert werden. Dies ist jedoch unwahrscheinlich, da der Cluster, auf dem diese ausgeführt werden, zwei Stunden lang aktiv bleibt, bevor er ausfällt. Dadurch wird die Anzahl der erforderlichen Abrufe reduziert, wenn der Cluster aktiv ist. Wenn Sie einen der oben genannten Fehler erhalten, müssen Sie warten, bis Ihre [!DNL Docker] -Grenze zurückgesetzt wird.

Weitere Informationen finden Sie unter [!DNL Docker Hub] Ratenbeschränkungen, besuchen Sie die [DockerHub-Dokumentation](https://www.docker.com/increase-rate-limits). Eine Lösung dafür wird derzeit erarbeitet und in einer nachfolgenden Version erwartet.
