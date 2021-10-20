---
keywords: Experience Platform;Fehlerbehebung;Data Science Workspace;beliebte Themen
solution: Experience Platform
title: Data Science Workspace - Fehlerbehebungshandbuch
topic-legacy: Troubleshooting
description: Dieses Dokument beantwortet häufig gestellte Fragen zum Adobe Experience Platform Data Science Workspace.
exl-id: fbc5efdc-f166-4000-bde2-4aa4b0318b38
source-git-commit: ec42d80e695ccf57c10c539ae1b5104c7948c473
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 0%

---

# [!DNL Data Science Workspace] Handbuch zur Fehlerbehebung

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu Adobe Experience Platform [!DNL Data Science Workspace]. Für Fragen und Fehlerbehebung in Bezug auf [!DNL Platform] APIs im Allgemeinen, siehe [Adobe Experience Platform API-Fehlerbehebungsleitfaden](../landing/troubleshooting.md).

## Status der JupyterLab-Notebook-Abfrage im Ausführungszustand fixiert

Ein JupyterLab-Notebook kann darauf hindeuten, dass sich eine Zelle im Ausführungszustand befindet, auf unbestimmte Zeit, in einigen nicht genügend Speicher-Bedingungen. So kann das JupyterLab-Notebook bei der Abfrage eines großen Datasets oder bei der Ausführung mehrerer nachfolgender Abfragen nicht über genügend Speicher verfügen, um das sich ergebende Datenobjekt zu speichern. Es gibt einige Indikatoren, die sich in dieser Situation zeigen lassen. Zunächst tritt der Kernel in den Leerlauf ein, obwohl die Zelle als ausgeführt angezeigt wird, wie durch die [`*`] Symbol neben der Zelle. Darüber hinaus gibt die untere Leiste den verwendeten/verfügbaren RAM an.

![Verfügbarer RAM](./images/jupyterlab/user-guide/allocate-ram.png)

Während der Daten kann der Speicher wachsen, bis er den maximal zugewiesenen Speicher erreicht. Der Speicher wird freigegeben, sobald der maximale Speicher erreicht ist und der Kernel neu gestartet wird. Das bedeutet, dass der verwendete Speicher in diesem Szenario aufgrund des Neustarts des Kernels sehr niedrig sein kann, während der Speicher kurz vor dem Neustart sehr nahe am maximal zugewiesenen RAM gelegen hätte.

Um dieses Problem zu beheben, wählen Sie das Zahnradsymbol rechts oben im JupyterLab aus und schieben Sie den Schieberegler nach rechts, gefolgt von der Auswahl von **[!UICONTROL Konfigurationen aktualisieren]** um mehr Arbeitsspeicher zuzuweisen. Wenn Sie mehrere Abfragen ausführen und sich Ihr RAM-Wert dem maximal zugewiesenen Wert nähert, starten Sie den Kernel neu, um den verfügbaren RAM-Speicher zurückzusetzen. Dadurch wird sichergestellt, dass die maximale RAM-Menge für die aktuelle Abfrage verfügbar ist.

![mehr RAM zuweisen](./images/jupyterlab/user-guide/notebook-gpu-config.png)

In dem Ereignis, dem Sie die maximale Speicherkapazität (RAM) zuweisen und das Problem weiterhin besteht, können Sie Ihre Abfrage so ändern, dass sie auf eine kleinere Datenmenge angewendet wird, indem Sie die Spalten oder den Datenbereich reduzieren. Um die gesamte Datenmenge zu nutzen, wird empfohlen, ein Spark-Notebook zu verwenden.

## [!DNL JupyterLab] Umgebung wird nicht geladen in [!DNL Google Chrome]

>[!IMPORTANT]
>
>Dieses Problem wurde behoben, konnte jedoch im Google Chrome 80.x-Browser weiterhin auftreten. Stellen Sie sicher, dass Ihr Chrome-Browser auf dem neuesten Stand ist.

Mit [!DNL Google Chrome] Browser Version 80.x, alle Drittanbieter-Cookies sind standardmäßig blockiert. Diese Politik kann [!DNL JupyterLab] von der Beladung innerhalb von Adobe Experience Platform.

Gehen Sie wie folgt vor, um dieses Problem zu beheben:

In [!DNL Chrome] , navigieren Sie rechts oben und wählen Sie **Einstellungen** (Alternativ können Sie &quot;chrome://settings/&quot; in der Adressleiste kopieren und einfügen). Führen Sie anschließend einen Bildlauf zum Ende der Seite durch und klicken Sie auf **Erweitert** herunterladen.

![Chrome erweitert](./images/faq/chrome-advanced.png)

Die **Datenschutz und Sicherheit** angezeigt. Als Nächstes klicken Sie auf **Site-Einstellungen** gefolgt von **Cookies und Site-Daten**.

![Chrome erweitert](./images/faq/privacy-security.png)

![Chrome erweitert](./images/faq/cookies.png)

Aktivieren Sie schließlich die Option &quot;Drittanbieter-Cookies blockieren&quot; in &quot;AUS&quot;.

![Chrome erweitert](./images/faq/toggle-off.png)

>[!NOTE]
>
>Alternativ können Sie Cookies von Drittanbietern deaktivieren und hinzufügen [*.]ds.adobe.net zur Zulassungsliste.

Navigieren Sie in der Adressleiste zu &quot;chrome://flags/&quot;. Suchen und deaktivieren Sie das Flag mit dem Titel *&quot;SameSite by default cookies&quot;* über das Dropdown-Menü rechts.

![samesite-Flag deaktivieren](./images/faq/samesite-flag.png)

Nach Schritt 2 werden Sie aufgefordert, Ihren Browser neu zu starten. Nach dem Neustart [!DNL Jupyterlab] muss zugänglich sein.

## Warum kann ich nicht darauf zugreifen [!DNL JupyterLab] in Safari?

Safari deaktiviert Cookies von Drittanbietern standardmäßig in Safari &lt; 12. weil [!DNL Jupyter] Virtual Machine-Instanz befindet sich auf einer anderen Domäne als der übergeordnete Frame. Adobe Experience Platform benötigt derzeit die Aktivierung von Drittanbieter-Cookies. Aktivieren Sie Cookies von Drittanbietern oder wechseln Sie zu einem anderen Browser, z. B. [!DNL Google Chrome].

Für Safari 12 müssen Sie Ihren Benutzeragent auf &#39;[!DNL Chrome]&#39; oder &#39;[!DNL Firefox]&quot;. Um den User Agent zu wechseln, öffnen Sie den Beginn *Safari* Menü und wählen **Voreinstellungen**. Das Fenster Voreinstellungen wird angezeigt.

![Safari-Voreinstellungen](./images/faq/preferences.png)

Wählen Sie im Fenster Safari-Voreinstellungen die Option **Erweitert**. Überprüfen Sie dann *Entwicklungsmenü in Menüleiste anzeigen* Feld. Sie können das Voreinstellungsfenster nach Abschluss dieses Schritts schließen.

![Safari Advanced](./images/faq/advanced.png)

Wählen Sie anschließend in der oberen Navigationsleiste die **Entwickeln** Menü. Von innerhalb von **Entwickeln** Dropdown, hover over **Benutzeragent**. Sie können **[!DNL Chrome]** oder **[!DNL Firefox]** Benutzeragentenzeichenfolge, die Sie verwenden möchten.

![Entwicklungsmenü](./images/faq/user-agent.png)

## Warum wird eine &#39;403 Verbotene&#39; Meldung angezeigt, wenn ich versuche, eine Datei hochzuladen oder zu löschen in [!DNL JupyterLab]?

Wenn Ihr Browser mit Advertising-Blocker-Software wie z. B. [!DNL Ghostery] oder [!DNL AdBlock] Außerdem muss die Domäne &quot;\*.adobe.net&quot; in jeder Werbeblockiersoftware für [!DNL JupyterLab] , um normal zu arbeiten. Das liegt daran, dass [!DNL JupyterLab] virtuelle Maschinen werden auf einer anderen Domäne als [!DNL Experience Platform] Domäne.

## Warum einige Teile meiner [!DNL Jupyter Notebook] aussehen oder nicht als Code rendern?

Dies kann vorkommen, wenn die betreffende Zelle versehentlich von &quot;Code&quot; in &quot;Markdown&quot; geändert wird. Während eine Codezelle den Fokus hat, drücken Sie die Tastenkombination **ESC+M** ändert den Zelltyp in &quot;Markdown&quot;. Der Zellentyp kann durch den Dropdown-Indikator oben im Notebook für die ausgewählten Zellen geändert werden. Um einen Zellentyp in Code zu ändern, wählen Sie die zu ändernde Zelle aus, um den Beginn auszuwählen. Klicken Sie dann auf das Dropdown-Menü, das den aktuellen Zellentyp angibt, und wählen Sie dann &quot;Code&quot;.

![](./images/faq/code_type.png)

## Benutzerdefinierte Installation [!DNL Python] Bibliotheken?

Die [!DNL Python] Kernel wird mit vielen beliebten Maschinen-Lernbibliotheken vorinstalliert. Sie können jedoch zusätzliche benutzerdefinierte Bibliotheken installieren, indem Sie den folgenden Befehl in einer Codezelle ausführen:

```shell
!pip install {LIBRARY_NAME}
```

Für eine vollständige Liste der vorinstallierten [!DNL Python] Bibliotheken, siehe [Anhang des JupyterLab-Benutzerhandbuchs](./jupyterlab/overview.md#supported-libraries).

## Kann ich benutzerdefinierte PySpark-Bibliotheken installieren?

Leider können Sie keine zusätzlichen Bibliotheken für den PySpark-Kernel installieren. Sie können sich jedoch an Ihren Kundenbetreuer wenden, um benutzerdefinierte PySpark-Bibliotheken für Sie zu installieren.

Eine Liste vorinstallierter PySpark-Bibliotheken finden Sie in der [Anhang des JupyterLab-Benutzerhandbuchs](./jupyterlab/overview.md#supported-libraries).

## Ist die Konfiguration möglich? [!DNL Spark] Cluster-Ressourcen für [!DNL JupyterLab] [!DNL Spark] oder PySpark-Kernel?

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

Weitere Informationen unter [!DNL Spark] Cluster-Ressourcenkonfiguration, einschließlich der vollständigen Liste konfigurierbarer Eigenschaften, finden Sie unter [JupyterLab-Benutzerhandbuch](./jupyterlab/overview.md#kernels).

## Warum erhalte ich einen Fehler, wenn ich versuche, bestimmte Aufgaben für größere Datensätze auszuführen?

Wenn Sie einen Fehler aus einem Grund wie z. B. `Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.` Dies bedeutet normalerweise, dass dem Treiber oder einem Manager der Speicher ausgeht. JupyterLab-Notebooks [Datenzugriff](./jupyterlab/access-notebook-data.md) Dokumentation für weitere Informationen über Datenbeschränkungen und die Ausführung von Aufgaben in großen Datensätzen. Normalerweise kann dieser Fehler durch Ändern der `mode` von `interactive` nach `batch`.

Zusätzlich werden beim Schreiben großer Spark-/PySpark-Datensätze Daten zwischengespeichert (`df.cache()`) vor dem Ausführen des Schreibcodes kann die Leistung erheblich verbessern.

<!-- remove this paragraph at a later date once the sdk is updated -->

Wenn beim Lesen von Daten ein Problem auftritt und Sie Transformationen auf die Daten anwenden, versuchen Sie, die Daten vor den Transformationen im Cache zu speichern. Durch das Zwischenspeichern Ihrer Daten werden mehrere Lesevorgänge im Netzwerk verhindert. Beginn durch Lesen der Daten. Als Nächstes wird der Cache (`df.cache()`) die Daten. Führen Sie schließlich Ihre Transformationen durch.

## Warum brauchen meine Spark/PySpark Notebooks so lange, um Daten zu lesen und zu schreiben?

Wenn Sie Datentransformationen durchführen, z. B. `fit()`, können die Transformationen mehrere Male ausgeführt werden. Um die Leistung zu erhöhen, speichern Sie Ihre Daten im Cache ab mit `df.cache()` vor der Durchführung `fit()`. Dadurch wird sichergestellt, dass die Transformationen nur ein einziges Mal ausgeführt werden und mehrere Lesevorgänge im Netzwerk verhindert werden.

**Empfohlene Bestellung:** Beginn durch Lesen der Daten. Führen Sie als Nächstes Transformationen durch, gefolgt vom Zwischenspeichern (`df.cache()`) die Daten. Schließlich führen Sie `fit()`.

## Warum laufen meine Spark/PySpark Notebooks nicht?

Wenn Sie einen der folgenden Fehler erhalten:

- Auftrag aufgrund eines Bühnenfehlers abgebrochen ... Kann nur RDDs mit derselben Anzahl von Elementen in jeder Partition zitieren.
- Remote-RPC-Client getrennt und andere Speicherfehler.
- Schlechte Leistung beim Lesen und Schreiben von Datensätzen.

Aktivieren, um sicherzustellen, dass die Daten im Cache gespeichert werden (`df.cache()`) vor dem Schreiben der Daten. Wenn Code in Notebooks ausgeführt wird, verwenden Sie `df.cache()` vor einer Aktion wie `fit()` kann die Leistung von Notebooks erheblich verbessern. Verwenden `df.cache()` vor dem Schreiben eines Datasets stellt sicher, dass die Transformationen nur ein einziges Mal statt mehrmals ausgeführt werden.

## [!DNL Docker Hub] Beschränkungen in Data Science Workspace

Ab dem 20. November 2020 wurden Preislimits für die anonyme und kostenlose, authentifizierte Nutzung von Docker Hub in Kraft gesetzt. Anonym und kostenlos [!DNL Docker Hub] Benutzer sind auf 100 Container-Pull-Anfragen alle sechs Stunden beschränkt. Wenn Sie von diesen Änderungen betroffen sind, erhalten Sie diese Fehlermeldung: `ERROR: toomanyrequests: Too Many Requests.` oder `You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`.

Diese Beschränkung wirkt sich derzeit nur auf Ihr Unternehmen aus, wenn Sie versuchen, innerhalb von sechs Stunden 100 Notebook-Rezepte zu erstellen, oder wenn Sie in Data Science Workspace auf Spark-Basis basierende Notebooks verwenden, die häufig nach oben oder unten skaliert werden. Dies ist jedoch unwahrscheinlich, da der Cluster, auf dem diese ausgeführt werden, zwei Stunden lang aktiv bleibt, bevor er ausgeschaltet wird. Dadurch wird die Anzahl der Pulle reduziert, die benötigt werden, wenn der Cluster aktiv ist. Wenn Sie einen der oben genannten Fehler erhalten, müssen Sie warten, bis Ihr [!DNL Docker] Grenzwert wird zurückgesetzt.

Für weitere Informationen über [!DNL Docker Hub] Ratenbeschränkungen, besuchen Sie die [DockerHub-Dokumentation](https://www.docker.com/increase-rate-limits). Eine Lösung dafür wird in einer späteren Version erarbeitet und erwartet.
