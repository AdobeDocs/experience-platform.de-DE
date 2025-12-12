---
title: Veröffentlichungsablauf
description: Erfahren Sie mehr über den Prozess der Erstellung von Bibliotheken, das Testen von Builds und die Freigabe für die Produktion in Adobe Experience Platform.
exl-id: 4885f60b-6401-4ec7-aa1a-29c135087847
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '1362'
ht-degree: 84%

---

# Veröffentlichungsablauf {#publishing-flow}

>[!CONTEXTUALHELP]
>id="platform_tags_publishing_flow"
>title="Veröffentlichungsablauf"
>abstract="Machen Sie sich mit den Ebenen der Benutzerberechtigungen vertraut, die für den Veröffentlichungsfluss erforderlich sind, einschließlich der Rechte zum Entwickeln, Genehmigen und Veröffentlichen."

Der Veröffentlichungsablauf für Tags in Adobe Experience Platform bezieht sich auf den Prozess der Erstellung von Bibliotheken, des Testens von Builds und der Freigabe für die Produktion.

Welche Aktionen Sie mit einer Bibliothek ausführen können, hängt vom Status der Bibliothek und der Berechtigungsstufe ab. Darüber hinaus wirkt sich der Status einer Bibliothek auch auf die darin enthaltenen Ressourcen (Regeln, Datenelemente und Erweiterungen) aus, je nachdem, was im Veröffentlichungsablauf vorangeht.

In den folgenden Abschnitten werden die Details zu Berechtigungen, zum Bibliotheksstatus und das Vorhergehende in Bezug auf den Veröffentlichungsablauf beschrieben.

## Berechtigungen {#permissions}

Es gibt verschiedene Stufen von Benutzerberechtigungen, die für den Veröffentlichungsfluss wichtig sind. Insbesondere sind dies die Rechte für die Eigenschaften [!UICONTROL Develop], [!UICONTROL Approve] und [!UICONTROL Publish]:

* **[!UICONTROL Develop]**: Umfasst die Möglichkeit, Bibliotheken zu erstellen und Builds für die Entwicklung zu erzeugen und sie zur Genehmigung einzureichen.
* **[!UICONTROL Approve]**: Umfasst die Möglichkeit, Builds für das Staging zu erstellen und gestaffelte Builds zu genehmigen.
* **[!UICONTROL Publish]**: Umfasst die Fähigkeit, eine genehmigte Bibliothek zu veröffentlichen.

Diese Berechtigungen beinhalten nicht die jeweils untergeordneten Rechte. Damit eine Person den Workflow von Anfang bis Ende ausführen kann, müssen dieser Person alle drei Berechtigungen für die jeweilige Eigenschaft gewährt werden.

Weitere Informationen zum Verwalten von Berechtigungen für Tags finden Sie im [Handbuch zu Benutzerberechtigungen](../administration/user-permissions.md).

## Bibliotheksstatus {#state}

Was den Veröffentlichungsablauf betrifft, gibt es vier Grundzustände, in denen sich eine Bibliothek befinden kann:

* [[!UICONTROL Development]](#development)
* [[!UICONTROL Submitted]](#submitted)
* [[!UICONTROL Approved]](#approved)
* [[!UICONTROL Published]](#published)

Diese vier Status werden auf der Registerkarte **[!UICONTROL Publishing Flow]** als Spalten dargestellt.

![](./images/approval-workflow/flow-ui.png)

Es müssen bestimmte Aktionen vorgenommen werden, um einer Bibliothek einen neuen Status zuzuweisen. Das folgende Diagramm zeigt jede Aktion, die eine Bibliothek zwischen den Status verschiebt:

![](./images/approval-workflow/library-state.png)

### [!UICONTROL Development] {#development}

Wenn neue Bibliotheken erstellt werden, befinden sie sich anfangs im Zustand [!UICONTROL Development]. Alle Änderungen an einer Bibliothek müssen vorgenommen werden, solange sich die Bibliothek im [!UICONTROL Development] befindet. Nach Abschluss der Entwicklung und der Tests kann die Bibliothek zur Genehmigung eingereicht werden.

In der folgenden Tabelle sind die Aktionen, die für eine Bibliothek im Zustand [!UICONTROL Development] verfügbar sind, aufgeführt:

| Aktion | Beschreibung |
| --- | --- |
| [!UICONTROL Edit] | Verwenden Sie den Bildschirm [!UICONTROL Edit Library], um Komponenten einer Bibliothek hinzuzufügen oder aus ihr zu entfernen. |
| [!UICONTROL Build to Development] | Erstellen Sie einen Build für die Bibliothek. Der Build wird kompiliert und in der Umgebung bereitgestellt, der die Bibliothek zugewiesen ist. Dieser Schritt schlägt fehl, wenn die Bibliothek keiner Umgebung zugewiesen wurde oder eine Änderung enthält, die bereits vorab definiert worden ist. |
| [!UICONTROL Submit for Approval] | Heben Sie die Zuweisung der Bibliothek zur Entwicklungsumgebung auf und verschieben Sie sie in die Spalte [!UICONTROL Submitted], damit ein Benutzer mit Berechtigungen zum Genehmigen sie bearbeiten kann. Diese Option wird nur aktiviert, wenn der letzte Build für die Bibliothek erfolgreich ist. |
| [!UICONTROL Submit & Build to Staging] | Dies kann nur von einem Anwender mit den Berechtigungen „Entwickeln“ und „Genehmigen“ durchgeführt werden. Durch diese Aktion wird die Zuweisung der Bibliothek zur Entwicklungsumgebung aufgehoben, die Bibliothek in den [!UICONTROL Submitted] Status verschoben und die Bibliothek in der Staging-Umgebung erstellt. Diese Option wird nur aktiviert, wenn der letzte Build für die Bibliothek erfolgreich ist. |
| [!UICONTROL Approve for Publishing] | Dies kann nur von einem Anwender mit den Berechtigungen „Entwickeln“ und „Genehmigen“ durchgeführt werden. Durch diese Aktion wird die Zuweisung der Bibliothek aus der Entwicklungsumgebung aufgehoben und sie in den [!UICONTROL Approved] Status verschoben - Staging-Umgebung und [!UICONTROL Submitted] Status werden vollständig übersprungen. Diese Option wird nur aktiviert, wenn der letzte Build für die Bibliothek erfolgreich ist. |
| [!UICONTROL Approve & Publish to Production] | Dies kann nur von einem Anwender mit den Berechtigungen „Entwickeln“, „Genehmigen“ und „Veröffentlichen“ durchgeführt werden. Durch diese Aktion wird die Zuweisung der Bibliothek aus der Entwicklungsumgebung aufgehoben, sie in den Status [!UICONTROL Approved] verschoben und in der Produktion veröffentlicht. Nach Abschluss des Produktions-Builds wechselt die Bibliothek in den [!UICONTROL Published]. Diese Option wird nur aktiviert, wenn der letzte Build für die Bibliothek erfolgreich ist. |
| [!UICONTROL Delete] | Entfernen Sie die Bibliothek aus dem System. Damit wird der Build nicht aus der Umgebung entfernt. |

### [!UICONTROL Submitted] {#submitted}

Befindet sich eine Bibliothek im Zustand [!UICONTROL Submitted], kann ein Benutzer mit Berechtigungen zum Genehmigen sie in der Staging-Umgebung testen. Nach Abschluss der Tests wird die Bibliothek genehmigt oder abgelehnt. Abgelehnte Builds kehren zurück in den Zustand [!UICONTROL Development], sodass weitere Änderungen vorgenommen werden können, bevor der Veröffentlichungsfluss neu gestartet wird.

In der folgenden Tabelle sind die Aktionen, die für eine Bibliothek im Zustand [!UICONTROL Submitted] verfügbar sind, aufgeführt:

| Aktion | Beschreibung |
| --- | --- |
| [!UICONTROL Open] | Zeigen Sie die Inhalte der Bibliothek an. Änderungen sind an Bibliotheken außerhalb der Spalte [!UICONTROL Development] nicht zulässig. Wenn Änderungen nötig sind, sollte die Bibliothek abgelehnt werden, sodass im Zustand [!UICONTROL Development] Änderungen daran vorgenommen werden können. |
| [!UICONTROL Build for Staging] | Erstellen Sie die Bibliothek in der Staging-Umgebung für die Bereitstellung. |
| [!UICONTROL Approve for Publishing] | Verschieben Sie die Bibliothek in die Spalte [!UICONTROL Approved], damit ein Anwender mit Veröffentlichungsberechtigungen sie bearbeiten kann. |
| [!UICONTROL Approve & Publish to Production] | Dies kann nur von einem Anwender mit den Berechtigungen „Genehmigen“ und „Veröffentlichen“ durchgeführt werden. Durch diese Aktion wird die Zuweisung der Bibliothek aus der Staging-Umgebung aufgehoben, sie in den [!UICONTROL Approved] Status verschoben und in der Produktion veröffentlicht. Nach Abschluss des Produktions-Builds wechselt die Bibliothek in den [!UICONTROL Published]. Dies kann mit oder ohne erfolgreichen Build in der Staging-Umgebung durchgeführt werden. |
| [!UICONTROL Reject] | Heben Sie die Zuweisung der Bibliothek zur Staging-Umgebung auf und verschieben Sie sie zwecks weiterer Änderungen zurück in die Spalte [!UICONTROL Development]. |

### [!UICONTROL Approved] {#approved}

Nachdem eine Bibliothek genehmigt wurde, kann ein Benutzer mit Veröffentlichungsberechtigungen die Bibliothek veröffentlichen oder ablehnen. Abgelehnte Builds werden wieder in die Spalte [!UICONTROL Development] verschoben, damit Änderungen vorgenommen werden können, bevor der Veröffentlichungsprozess erneut gestartet wird.

In der folgenden Tabelle sind die Aktionen, die für eine Bibliothek im Zustand [!UICONTROL Approved] verfügbar sind, aufgeführt:

| Aktion | Beschreibung |
| --- | --- |
| [!UICONTROL Open] | Zeigen Sie die Inhalte der Bibliothek an. Änderungen sind an Bibliotheken außerhalb der Spalte [!UICONTROL Development] nicht zulässig. Wenn Änderungen nötig sind, sollte die Bibliothek abgelehnt werden, sodass im Zustand [!UICONTROL Development] Änderungen daran vorgenommen werden können. |
| [!UICONTROL Build and Publish to Production] | Hebt die Zuweisung der Bibliothek zur Staging-Umgebung auf, weist die Bibliothek der Produktionsumgebung zu und stellt sie bereit.<br><br>**Wichtig**: Wenn diese Option aktiviert ist, wird die Bibliothek in Ihrer Produktionsumgebung verfügbar. Stellen Sie sicher, dass die Bibliothek die gewünschten Änderungen enthält, bevor Sie diese Option auswählen. |
| [!UICONTROL Reject] | Hebt die Bibliothekszuweisung zur Staging-Umgebung auf und verschiebt die Bibliothek zu Änderungszwecken in die Spalte [!UICONTROL Development]. |

### [!UICONTROL Published] {#published}

Die Spalte [!UICONTROL Published] zeigt an, welche Bibliotheken veröffentlicht wurden, einschließlich des Veröffentlichungsdatums. Die aktuell veröffentlichte Bibliothek wird mit einem grünen Punkt markiert. Sofern Sie keine erneute Veröffentlichung einer vorherigen Bibliothek durchgeführt haben, ist dies immer die Bibliothek ganz oben in der Spalte.

| Aktion | Beschreibung |
| --- | --- |
| [!UICONTROL Open] | Zeigen Sie die Inhalte der Bibliothek an. Änderungen sind an Bibliotheken außerhalb der Spalte [!UICONTROL Development] nicht zulässig. Wenn Sie den Inhalt Ihrer Produktionsumgebung ändern möchten, müssen Sie eine neue Bibliothek erstellen und den gesamten Veröffentlichungsprozess durchlaufen. |
| [!UICONTROL Republish] | Diese Aktion ist nur für die fünf zuletzt veröffentlichten Bibliotheken verfügbar und nur, wenn die Produktionsumgebung (a) mit der Option „Archiv ausgeschaltet“ konfiguriert ist und (b) zum Zeitpunkt des Builds einen [!UICONTROL Managed by Adobe]-Host verwendet. |
| [!UICONTROL Download] | Diese Aktion ist nur für die fünf zuletzt veröffentlichten Bibliotheken verfügbar und nur, wenn die Produktionsumgebung (a) mit der Option „Archiv eingeschaltet“ konfiguriert ist und (b) zum Zeitpunkt des Builds einen [!UICONTROL Managed by Adobe]-Host verwendet. |

## Upstream {#upstream}

Nachdem Sie die erste Bibliothek veröffentlicht haben, wird es wichtig, dass Sie die Rolle von Upstream verstehen, während Sie mit neueren Bibliotheken den Publishing-Ablauf durchlaufen.

Wenn sich eine Bibliothek derzeit in der Phase [!UICONTROL Development], [!UICONTROL Submitted] oder [!UICONTROL Approved] befindet, erbt diese Bibliothek die Regeln, Datenelemente und Erweiterungen aller Bibliotheken, die sich im Upstream befinden. Diese vererbten Ressourcen bilden eine „Baseline“ für jede Bibliothek, die den Veröffentlichungsablauf durchläuft. Im Grunde können Sie sich jede neue Bibliothek einfach als eine Reihe von Änderungen der Baseline vorstellen, die durch den Upstream festgelegt wird. Dadurch wird sichergestellt, dass bei der Veröffentlichung einer neuen Iteration nichts aus einer vorherigen Bibliothek unerwartet überschrieben wird.

Was im Upstream enthalten ist, hängt vom aktuellen Stand der Bibliothek ab. Beispielsweise erben Bibliotheken in der Spalte [!UICONTROL Approved] nur Ressourcen aus der Bibliothek [!UICONTROL Published], während Bibliotheken unter [!UICONTROL Development] Ressourcen aus allen anderen Spalten erben.

![](./images/approval-workflow/upstream.png)

Beim Bearbeiten einer Bibliothek in der Benutzeroberfläche werden alle Ressourcen, die von Upstream-Elementen geerbt werden, im Abschnitt **[!UICONTROL Resources Upstream]** angezeigt. Um diese Ressourcen anzuzeigen, wählen Sie den Tab „Erweitern“ unter der Abschnittsüberschrift aus.

![](./images/approval-workflow/upstream-collapse.png)

Der Abschnitt wird erweitert, um die einzelnen Ressourcen anzuzeigen, die vom Upstream geerbt werden. Sie können die linke Leiste verwenden, um zwischen [!UICONTROL Rules], [!UICONTROL Data Elements] und [!UICONTROL Extensions] zu filtern, oder Sie können die Suchleiste verwenden, um eine bestimmte Ressource anhand des Namens nachzuschlagen.

![](./images/approval-workflow/upstream-resources.png)

## Nächste Schritte

Dieses Handbuch bietet einen Überblick über den Veröffentlichungsablauf für Bibliotheken in Adobe Experience Platform. Weitere Informationen zum Veröffentlichen von Bibliotheken finden Sie unter [Übersicht über das Veröffentlichen](./overview.md).
