---
keywords: Experience Platform; Fehlerbehebung; Data Science Workspace; beliebte Themen
solution: Experience Platform
title: Data Science Workspace - Anleitung zur Fehlerbehebung
topic-legacy: Troubleshooting
description: Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu Adobe Experience Platform Data Science Workspace.
exl-id: fbc5efdc-f166-4000-bde2-4aa4b0318b38
source-git-commit: c2c2b1684e2c2c3c76dc23ad1df720abd6c4356c
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 1%

---

# [!DNL Data Science Workspace] Handbuch zur Fehlerbehebung

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu Adobe Experience Platform [!DNL Data Science Workspace]. Fragen und die Fehlerbehebung für [!DNL Platform]-APIs im Allgemeinen finden Sie im [Handbuch zur Fehlerbehebung bei Adobe Experience Platform-API](../landing/troubleshooting.md).

## [!DNL JupyterLab] -Umgebung wird nicht in geladen  [!DNL Google Chrome]

>[!IMPORTANT]
>
>Dieses Problem wurde behoben, konnte jedoch im Google Chrome 80.x-Browser noch vorhanden sein. Stellen Sie sicher, dass Ihr Chrome-Browser aktuell ist.

Mit der Browser-Version 80.x von [!DNL Google Chrome] werden alle Drittanbieter-Cookies standardmäßig blockiert. Diese Richtlinie kann verhindern, dass [!DNL JupyterLab] in Adobe Experience Platform geladen wird.

Gehen Sie wie folgt vor, um dieses Problem zu beheben:

Navigieren Sie in Ihrem [!DNL Chrome]-Browser nach oben rechts und wählen Sie **Einstellungen** aus (alternativ können Sie &quot;chrome://settings/&quot;in die Adressleiste kopieren). Scrollen Sie dann zum unteren Rand der Seite und klicken Sie auf das Dropdown-Menü **Erweitert** .

![Chrome Advanced](./images/faq/chrome-advanced.png)

Der Abschnitt **Datenschutz und Sicherheit** wird angezeigt. Klicken Sie anschließend auf **Site-Einstellungen** , gefolgt von **Cookies und Site-Daten**.

![Chrome Advanced](./images/faq/privacy-security.png)

![Chrome Advanced](./images/faq/cookies.png)

Schalten Sie abschließend &quot;Drittanbieter-Cookies blockieren&quot;in &quot;AUS&quot;.

![Chrome Advanced](./images/faq/toggle-off.png)

>[!NOTE]
>
>Alternativ können Sie Drittanbieter-Cookies deaktivieren und [* hinzufügen.]ds.adobe.net zur Zulassungsliste hinzugefügt.

Navigieren Sie in Ihrer Adressleiste zu &quot;chrome://flags/&quot;. Suchen und deaktivieren Sie die Markierung *&quot;SameSite standardmäßig Cookies&quot;*, indem Sie das Dropdown-Menü rechts verwenden.

![SameSite-Markierung deaktivieren](./images/faq/samesite-flag.png)

Nach Schritt 2 werden Sie aufgefordert, Ihren Browser neu zu starten. Nach dem Neustart sollte [!DNL Jupyterlab] verfügbar sein.

## Warum kann ich in Safari nicht auf [!DNL JupyterLab] zugreifen?

Safari deaktiviert in Safari &lt; 12 standardmäßig Drittanbieter-Cookies. Da sich Ihre [!DNL Jupyter]-Virtual-Machine-Instanz in einer anderen Domäne befindet als der übergeordnete Frame, erfordert Adobe Experience Platform derzeit, dass Drittanbieter-Cookies aktiviert werden. Aktivieren Sie Drittanbieter-Cookies oder wechseln Sie zu einem anderen Browser, z. B. [!DNL Google Chrome].

Für Safari 12 müssen Sie Ihren Benutzeragenten auf &quot;[!DNL Chrome]&quot;oder &quot;[!DNL Firefox]&quot;umstellen. Um den Benutzeragenten zu wechseln, öffnen Sie zunächst das Menü *Safari* und wählen Sie **Voreinstellungen** aus. Das Fenster Voreinstellungen wird angezeigt.

![Safari-Voreinstellungen](./images/faq/preferences.png)

Wählen Sie im Fenster der Safari-Voreinstellungen die Option **Erweitert** aus. Aktivieren Sie dann das Menü *Entwickeln anzeigen in der Menüleiste* . Sie können das Fenster mit den Voreinstellungen schließen, nachdem dieser Schritt abgeschlossen ist.

![Safari Advanced](./images/faq/advanced.png)

Wählen Sie dann in der oberen Navigationsleiste das Menü **Entwickeln** aus. Bewegen Sie von der Dropdown-Liste **Entwickeln** den Mauszeiger über **Benutzeragent**. Sie können die zu verwendende **[!DNL Chrome]**- oder **[!DNL Firefox]** Benutzeragenten-Zeichenfolge auswählen.

![Menü &quot;Entwickeln&quot;](./images/faq/user-agent.png)

## Warum wird beim Versuch, eine Datei in [!DNL JupyterLab] hochzuladen oder zu löschen, die Meldung &quot;403 Verboten&quot;angezeigt?

Wenn Ihr Browser mit Advertising-Blocker-Software wie [!DNL Ghostery] oder [!DNL AdBlock] Plus aktiviert ist, muss die Domäne &quot;\*.adobe.net&quot;in jeder Advertising-Blocker-Software zugelassen sein, damit [!DNL JupyterLab] normal funktioniert. Dies liegt daran, dass [!DNL JupyterLab] virtuelle Maschinen auf einer anderen Domäne als der [!DNL Experience Platform]-Domäne ausgeführt werden.

## Warum sehen einige Teile von [!DNL Jupyter Notebook] verwirrt aus oder werden nicht als Code gerendert?

Dies kann vorkommen, wenn die betreffende Zelle versehentlich von &quot;Code&quot;in &quot;Markdown&quot;geändert wird. Während eine Codezelle fokussiert ist, ändert das Drücken der Tastenkombination **ESC+M** den Zelltyp in Markdown. Der Zelltyp kann durch die Dropdown-Anzeige oben im Notebook für die ausgewählten Zellen geändert werden. Um einen Zellentyp in Code zu ändern, wählen Sie zunächst die Zelle aus, die Sie ändern möchten. Klicken Sie anschließend auf das Dropdown-Menü, das den aktuellen Zellentyp angibt, und wählen Sie &quot;Code&quot;.

![](./images/faq/code_type.png)

## Wie installiere ich benutzerdefinierte [!DNL Python]-Bibliotheken?

Der [!DNL Python]-Kernel wird mit vielen gängigen maschinellen Lernbibliotheken vorinstalliert. Sie können jedoch zusätzliche benutzerdefinierte Bibliotheken installieren, indem Sie den folgenden Befehl in einer Code-Zelle ausführen:

```shell
!pip install {LIBRARY_NAME}
```

Eine vollständige Liste der vorinstallierten [!DNL Python]-Bibliotheken finden Sie im Abschnitt [Anhang des JupyterLab-Benutzerhandbuchs](./jupyterlab/overview.md#supported-libraries).

## Kann ich benutzerdefinierte PySpark-Bibliotheken installieren?

Leider können Sie keine zusätzlichen Bibliotheken für den PySpark-Kernel installieren. Sie können sich jedoch an Ihren Kundenbetreuer von Adobe wenden, um für Sie benutzerdefinierte PySpark-Bibliotheken zu installieren.

Eine Liste der vorinstallierten PySpark-Bibliotheken finden Sie im Abschnitt [Anhang des JupyterLab-Benutzerhandbuchs](./jupyterlab/overview.md#supported-libraries).

## Ist es möglich, [!DNL Spark] Cluster-Ressourcen für [!DNL JupyterLab] [!DNL Spark]- oder PySpark-Kernel zu konfigurieren?

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

Weitere Informationen zur Konfiguration von Cluster-Ressourcen, einschließlich der vollständigen Liste der konfigurierbaren Eigenschaften, finden Sie im [JupyterLab-Benutzerhandbuch](./jupyterlab/overview.md#kernels).[!DNL Spark]

## Warum erhalte ich eine Fehlermeldung, wenn ich versuche, bestimmte Aufgaben für größere Datensätze auszuführen?

Wenn Sie einen Fehler mit einem Grund wie `Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.` erhalten, bedeutet dies normalerweise, dass dem Treiber oder einem Executor der Arbeitsspeicher ausgeht. Weitere Informationen zu Datenbeschränkungen und zum Ausführen von Aufgaben für große Datensätze finden Sie in der Dokumentation JupyterLab Notebooks [Datenzugriff](./jupyterlab/access-notebook-data.md) . Normalerweise kann dieser Fehler durch Ändern von `mode` von `interactive` in `batch` behoben werden.

Außerdem kann das Zwischenspeichern Ihrer Daten (`df.cache()`) vor dem Ausführen des Schreibcodes beim Schreiben großer Spark-/PySpark-Datensätze die Leistung erheblich verbessern.

<!-- remove this paragraph at a later date once the sdk is updated -->

Wenn beim Lesen von Daten Probleme auftreten und Transformationen auf die Daten angewendet werden, versuchen Sie, die Daten vor den Transformationen zwischenzuspeichern. Das Zwischenspeichern Ihrer Daten verhindert mehrere Lesevorgänge im Netzwerk. Lesen Sie zunächst die Daten. Als Nächstes zwischenspeichern (`df.cache()`) Sie die Daten. Führen Sie abschließend eine Transformation durch.

## Warum dauert es so lange, bis meine Spark-/PySpark-Notebooks Daten lesen und schreiben?

Wenn Sie Datenumwandlungen durchführen, z. B. `fit()`, werden die Umwandlungen möglicherweise mehrmals ausgeführt. Um die Leistung zu steigern, zwischenspeichern Sie Ihre Daten mit `df.cache()`, bevor Sie `fit()` ausführen. Dadurch wird sichergestellt, dass die Transformationen nur einmal ausgeführt werden und dass im Netzwerk mehrere Lesevorgänge verhindert werden.

**Empfohlene Reihenfolge:**  Lesen Sie zunächst die Daten. Führen Sie als Nächstes Transformationen durch, gefolgt von Caching (`df.cache()`) der Daten. Führen Sie abschließend einen `fit()` aus.

## Warum werden meine Spark-/PySpark-Notebooks nicht ausgeführt?

Wenn Sie einen der folgenden Fehler erhalten:

- Vorgang aufgrund von Staging-Fehler abgebrochen ... Kann nur RDDs mit derselben Anzahl von Elementen in jeder Partition komprimieren.
- Remote RPC Client getrennt und andere Speicherfehler.
- Schlechte Leistung beim Lesen und Schreiben von Datensätzen.

Stellen Sie sicher, dass Sie die Daten (`df.cache()`) zwischenspeichern, bevor Sie die Daten schreiben. Beim Ausführen von Code in Notebooks kann die Verwendung von `df.cache()` vor einer Aktion wie `fit()` die Notebook-Leistung erheblich verbessern. Durch Verwendung von `df.cache()` vor dem Schreiben eines Datensatzes wird sichergestellt, dass die Umwandlungen nur ein einziges Mal statt mehrmals ausgeführt werden.

## [!DNL Docker Hub] Beschränkungen in Data Science Workspace

Ab dem 20. November 2020 sind die Ratenbeschränkungen für die anonyme und kostenlose authentifizierte Verwendung von Docker Hub in Kraft getreten. Anonyme und kostenlose [!DNL Docker Hub] -Benutzer sind auf 100 Container-Bildabruf-Anfragen alle sechs Stunden beschränkt. Wenn Sie von diesen Änderungen betroffen sind, erhalten Sie diese Fehlermeldung: `ERROR: toomanyrequests: Too Many Requests.` oder `You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`.

Derzeit wirkt sich diese Beschränkung nur auf Ihr Unternehmen aus, wenn Sie versuchen, innerhalb des sechsstündigen Zeitraums 100-Notebook-Rezepte zu erstellen oder wenn Sie Spark-basierte Notebooks in Data Science Workspace verwenden, die häufig nach oben und unten skaliert werden. Dies ist jedoch unwahrscheinlich, da der Cluster, auf dem diese ausgeführt werden, zwei Stunden lang aktiv bleibt, bevor er ausfällt. Dadurch wird die Anzahl der erforderlichen Abrufe reduziert, wenn der Cluster aktiv ist. Wenn Sie einen der oben genannten Fehler erhalten, müssen Sie warten, bis Ihr [!DNL Docker] -Limit zurückgesetzt wird.

Weitere Informationen zu den Ratenbeschränkungen für [!DNL Docker Hub] finden Sie in der [DockerHub-Dokumentation](https://www.docker.com/increase-rate-limits). Eine Lösung dafür wird derzeit erarbeitet und in einer nachfolgenden Version erwartet.
