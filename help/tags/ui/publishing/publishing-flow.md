---
title: Publishing-Ablauf
description: Erfahren Sie mehr über den Prozess der Erstellung von Bibliotheken, das Testen von Builds und die Freigabe für die Produktion in Adobe Experience Platform.
exl-id: 4885f60b-6401-4ec7-aa1a-29c135087847
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Publishing-Ablauf

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Der Veröffentlichungsablauf für Tags in Adobe Experience Platform bezieht sich auf den Prozess der Erstellung von Bibliotheken, des Testens von Builds und der Freigabe für die Produktion.

Welche Aktionen Sie mit einer Bibliothek ausführen können, hängt vom Status der Bibliothek und der Berechtigungsstufe ab. Darüber hinaus wirkt sich der Status einer Bibliothek auch auf die darin enthaltenen Ressourcen (Regeln, Datenelemente und Erweiterungen) aus, je nachdem, was im Publishing-Ablauf vorangeht.

In den folgenden Abschnitten werden die Details zu Berechtigungen, zum Bibliotheksstatus und das Vorhergehende in Bezug auf den Publishing-Ablauf beschrieben.

## Berechtigungen {#permissions}

Es gibt verschiedene Stufen von Benutzerberechtigungen, die für den Publishing-Ablauf wichtig sind. Insbesondere sind dies die Rechte zum [!UICONTROL Entwickeln], [!UICONTROL Genehmigen] und [!UICONTROL Veröffentlichen].

* **[!UICONTROL Entwickeln]**: Umfasst die Möglichkeit, Bibliotheken zu erstellen, sie für die Entwicklung aufzubauen und sie zur Genehmigung einzureichen.
* **[!UICONTROL Genehmigen]**: Umfasst die Möglichkeit, Builds für das Staging zu erstellen und gestaffelte Builds zu genehmigen.
* **[!UICONTROL Veröffentlichen]**: Umfasst die Fähigkeit, eine genehmigte Bibliothek zu veröffentlichen.

Diese Berechtigungen beinhalten nicht die jeweils untergeordneten Rechte. Damit eine Person den Workflow von Anfang bis Ende ausführen kann, müssen dieser Person alle drei Berechtigungen für die jeweilige Eigenschaft gewährt werden.

Weitere Informationen zum Verwalten von Berechtigungen für Tags finden Sie im [Handbuch zu Benutzerberechtigungen](../administration/user-permissions.md).

## Bibliotheksstatus {#state}

Was den Publishing-Ablauf betrifft, gibt es vier Grundzustände, in denen sich eine Bibliothek befinden kann:

* [[!UICONTROL Entwicklung]](#development)
* [[!UICONTROL Gesendet]](#submitted)
* [[!UICONTROL Genehmigt]](#approved)
* [[!UICONTROL Veröffentlicht]](#published)

Diese vier Status werden auf der Registerkarte **[!UICONTROL Veröffentlichungsablauf]** der Datenerfassungs-Benutzeroberfläche als Spalten dargestellt.

![](./images/approval-workflow/flow-ui.png)

Es müssen bestimmte Aktionen vorgenommen werden, um einer Bibliothek einen neuen Status zuzuweisen. Das folgende Diagramm zeigt jede Aktion, die eine Bibliothek zwischen den Status verschiebt:

![](./images/approval-workflow/library-state.png)

### [!UICONTROL Entwicklung] {#development}

Wenn neue Bibliotheken erstellt werden, befinden sie sich anfangs im Zustand [!UICONTROL Entwicklung]. Alle Änderungen an einer Bibliothek müssen vorgenommen werden, während sich die Bibliothek in [!UICONTROL Entwicklung] befindet. Nach Abschluss der Entwicklung und der Tests kann die Bibliothek zur Genehmigung eingereicht werden.

In der folgenden Tabelle sind die Aktionen aufgeführt, die für eine Bibliothek im Zustand [!UICONTROL Entwicklung] verfügbar sind:

| Aktion | Beschreibung |
| --- | --- |
| [!UICONTROL Vorlage] | Verwenden Sie den Bildschirm [!UICONTROL Bibliothek bearbeiten], um Komponenten zu einer Bibliothek hinzuzufügen oder aus ihr zu entfernen. |
| [!UICONTROL Build zur Entwicklung] | Erstellen Sie einen Build für die Bibliothek. Der Build wird kompiliert und in der Umgebung bereitgestellt, der die Bibliothek zugewiesen ist. Dieser Schritt schlägt fehl, wenn die Bibliothek keiner Umgebung zugewiesen wurde oder eine Änderung enthält, die bereits vorab definiert worden ist. |
| [!UICONTROL Einreichen zur Genehmigung] | Heben Sie die Zuweisung der Bibliothek zur Entwicklungsumgebung auf und verschieben Sie sie in die Spalte [!UICONTROL Eingereicht], damit sie ein Benutzer mit Berechtigungen zum Genehmigen bearbeiten kann. Diese Option wird nur aktiviert, wenn der letzte Build für die Bibliothek erfolgreich ist. |
| [!UICONTROL Senden und für Staging erstellen] | Dies kann nur von einem Anwender mit den Berechtigungen „Entwickeln“ und „Genehmigen“ durchgeführt werden. Durch diese Aktion wird die Zuweisung der Bibliothek zur Entwicklungsumgebung aufgehoben, die Bibliothek zum Status [!UICONTROL Gesendet] verschoben und die Bibliothek in der Staging-Umgebung erstellt. Diese Option wird nur aktiviert, wenn der letzte Build für die Bibliothek erfolgreich ist. |
| [!UICONTROL Zur Veröffentlichung genehmigen] | Dies kann nur von einem Anwender mit den Berechtigungen „Entwickeln“ und „Genehmigen“ durchgeführt werden. Durch diese Aktion wird die Zuweisung der Bibliothek aus der Entwicklungsumgebung aufgehoben und sie in den Status [!UICONTROL Genehmigt] verschoben - Staging-Umgebung und Status [!UICONTROL Gesendet] werden vollständig übersprungen. Diese Option wird nur aktiviert, wenn der letzte Build für die Bibliothek erfolgreich ist. |
| [!UICONTROL Genehmigen und in Produktion veröffentlichen] | Dies kann nur von einem Anwender mit den Berechtigungen „Entwickeln“, „Genehmigen“ und „Veröffentlichen“ durchgeführt werden. Durch diese Aktion wird die Zuweisung der Bibliothek aus der Entwicklungsumgebung aufgehoben, sie in den Status [!UICONTROL Genehmigt] verschoben und in der Produktion veröffentlicht. Nach Abschluss des Produktions-Builds wechselt die Bibliothek in den Status [!UICONTROL Veröffentlicht]. Diese Option wird nur aktiviert, wenn der letzte Build für die Bibliothek erfolgreich ist. |
| [!UICONTROL Löschen] | Entfernen Sie die Bibliothek aus dem System. Damit wird der Build nicht aus der Umgebung entfernt. |

### [!UICONTROL Gesendet] {#submitted}

Befindet sich eine Bibliothek im Zustand [!UICONTROL Eingereicht], kann sie ein Benutzer mit Berechtigungen zum Genehmigen in der Staging-Umgebung testen. Nach Abschluss der Tests wird die Bibliothek genehmigt oder abgelehnt. Abgelehnte Builds kehren zurück in den Zustand [!UICONTROL Entwicklung], sodass weitere Änderungen vorgenommen werden können, bevor der Publishing-Ablauf erneut gestartet wird.

In der folgenden Tabelle sind die Aktionen aufgeführt, die für eine Bibliothek im Zustand [!UICONTROL Eingereicht] verfügbar sind:

| Aktion | Beschreibung |
| --- | --- |
| [!UICONTROL Öffnen] | Zeigen Sie die Inhalte der Bibliothek an. Änderungen sind an Bibliotheken außerhalb der Spalte [!UICONTROL Entwicklung] nicht zulässig. Wenn Änderungen nötig sind, sollte die Bibliothek abgelehnt werden, sodass Änderungen in [!UICONTROL Entwicklung] vorgenommen werden können. |
| [!UICONTROL Build für das Staging] | Erstellen Sie die Bibliothek in der Staging-Umgebung für die Implementierung. |
| [!UICONTROL Zur Veröffentlichung genehmigen] | Verschieben Sie die Bibliothek in die Spalte [!UICONTROL Genehmigt], damit sie ein Anwender mit Veröffentlichungsberechtigungen bearbeiten kann. |
| [!UICONTROL Genehmigen und in Produktion veröffentlichen] | Dies kann nur von einem Anwender mit den Berechtigungen „Genehmigen“ und „Veröffentlichen“ durchgeführt werden. Durch diese Aktion wird die Zuweisung der Bibliothek aus der Staging-Umgebung aufgehoben, sie in den Status [!UICONTROL Genehmigt] verschoben und in der Produktion veröffentlicht. Nach Abschluss des Produktions-Builds wechselt die Bibliothek in den Status [!UICONTROL Veröffentlicht]. Dies kann mit oder ohne erfolgreichen Build in der Staging-Umgebung durchgeführt werden. |
| [!UICONTROL Ablehnen] | Heben Sie die Zuweisung der Bibliothek zur Staging-Umgebung auf und verschieben Sie sie zwecks weiterer Änderungen zurück in die Spalte [!UICONTROL Entwicklung]. |

### [!UICONTROL Genehmigt] {#approved}

Nachdem eine Bibliothek genehmigt wurde, kann ein Benutzer mit Veröffentlichungsberechtigungen die Bibliothek veröffentlichen oder ablehnen. Abgelehnte Builds werden wieder in die Spalte [!UICONTROL Entwicklung] verschoben, damit Änderungen vorgenommen werden können, bevor der Publishing-Ablauf erneut gestartet wird.

In der folgenden Tabelle sind die Aktionen, die für eine Bibliothek im Zustand [!UICONTROL Genehmigt] verfügbar sind, aufgeführt:

| Aktion | Beschreibung |
| --- | --- |
| [!UICONTROL Öffnen] | Zeigen Sie die Inhalte der Bibliothek an. Änderungen sind an Bibliotheken außerhalb der Spalte [!UICONTROL Entwicklung] nicht zulässig. Wenn Änderungen nötig sind, sollte die Bibliothek abgelehnt werden, sodass Änderungen in [!UICONTROL Entwicklung] vorgenommen werden können. |
| [!UICONTROL Erstellen und in Produktion veröffentlichen] | Hebt die Zuweisung der Bibliothek zur Staging-Umgebung auf, weist die Bibliothek der Produktionsumgebung zu und stellt sie bereit.<br><br>**Wichtig**: Wenn diese Option aktiviert ist, wird die Bibliothek in Ihrer Produktionsumgebung verfügbar. Stellen Sie sicher, dass die Bibliothek die gewünschten Änderungen enthält, bevor Sie diese Option auswählen. |
| [!UICONTROL Ablehnen] | Heben Sie die Bibliothekszuweisung zur Staging-Umgebung auf und verschieben Sie die Bibliothek zu Änderungszwecken in die Spalte [!UICONTROL Entwicklung]. |

### [!UICONTROL Veröffentlicht] {#published}

Diese Spalte [!UICONTROL Veröffentlicht] zeigt, welche Bibliotheken veröffentlicht wurden, einschließlich des Veröffentlichungsdatums. Die aktuell veröffentlichte Bibliothek wird mit einem grünen Punkt markiert. Sofern Sie keine erneute Veröffentlichung einer vorherigen Bibliothek durchgeführt haben, ist dies immer die Bibliothek ganz oben in der Spalte.

| Aktion | Beschreibung |
| --- | --- |
| [!UICONTROL Öffnen] | Zeigen Sie die Inhalte der Bibliothek an. Änderungen sind an Bibliotheken außerhalb der Spalte [!UICONTROL Entwicklung] nicht zulässig. Wenn Sie den Inhalt Ihrer Produktionsumgebung ändern möchten, müssen Sie eine neue Bibliothek erstellen und den gesamten Veröffentlichungsprozess durchlaufen. |
| [!UICONTROL Neu veröffentlichen] | Diese Aktion ist nur für die fünf zuletzt veröffentlichten Bibliotheken verfügbar und nur, wenn die Produktionsumgebung (a) mit der Option „Archiv ausgeschaltet“ konfiguriert ist und (b) zum Zeitpunkt des Builds einen Host des Typs [!UICONTROL Verwaltet von Adobe] verwendet. |
| [!UICONTROL Herunterladen] | Diese Aktion ist nur für die fünf zuletzt veröffentlichten Bibliotheken verfügbar und nur, wenn die Produktionsumgebung (a) mit der Option „Archiv eingeschaltet“ konfiguriert ist und (b) zum Zeitpunkt des Builds einen Host des Typs [!UICONTROL Verwaltet von Adobe] verwendet. |

## Upstream {#upstream}

Nachdem Sie die erste Bibliothek veröffentlicht haben, wird es wichtig, dass Sie die Rolle von Upstream verstehen, während Sie mit neueren Bibliotheken den Publishing-Ablauf durchlaufen.

Wenn sich eine Bibliothek derzeit in der Phase [!UICONTROL Entwicklung], [!UICONTROL Eingereicht] oder [!UICONTROL Genehmigt] befindet, erbt diese Bibliothek die Regeln, Datenelemente und Erweiterungen aller Bibliotheken, die sich im Upstream befinden. Diese vererbten Ressourcen bilden eine „Grundlinie“ für jede Bibliothek, die den Publishing-Ablauf durchläuft. Im Grunde können Sie sich jede neue Bibliothek einfach als eine Reihe von Änderungen der Grundlinie vorstellen, die durch den Upstream festgelegt wird. Dadurch wird sichergestellt, dass bei der Veröffentlichung einer neuen Iteration nichts aus einer vorherigen Bibliothek unerwartet überschrieben wird.

Was im Upstream enthalten ist, hängt vom aktuellen Stand der Bibliothek ab. Beispielsweise erben Bibliotheken in der Spalte [!UICONTROL Genehmigt] nur Ressourcen aus der Bibliothek [!UICONTROL Veröffentlicht], während Bibliotheken unter [!UICONTROL Entwicklung] Ressourcen aus allen anderen Spalten erben.

![](./images/approval-workflow/upstream.png)

Wenn Sie eine Bibliothek in der Datenerfassungs-Benutzeroberfläche bearbeiten, werden alle Ressourcen, die von Upstream-Elementen übernommen werden, im Abschnitt **[!UICONTROL Upstream-Ressourcen]** angezeigt. Um diese Ressourcen anzuzeigen, wählen Sie den Tab „Erweitern“ unter der Abschnittsüberschrift aus.

![](./images/approval-workflow/upstream-collapse.png)

Der Abschnitt wird erweitert, um die einzelnen Ressourcen anzuzeigen, die vom Upstream geerbt werden. Sie können die linke Leiste verwenden, um nach [!UICONTROL Regeln], [!UICONTROL Datenelementen] oder [!UICONTROL Erweiterungen] zu filtern, oder Sie können die Suchleiste verwenden, um eine bestimmte Ressource anhand des Namens nachzuschlagen.

![](./images/approval-workflow/upstream-resources.png)

## Nächste Schritte

Dieses Handbuch bietet einen Überblick über den Veröffentlichungsablauf für Bibliotheken in Adobe Experience Platform. Weitere Informationen zum Veröffentlichen von Bibliotheken finden Sie unter [Übersicht über das Veröffentlichen](./overview.md).
