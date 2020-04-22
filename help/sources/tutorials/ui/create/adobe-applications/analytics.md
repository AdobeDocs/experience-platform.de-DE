---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Adobe Analytics-Quell-Connectors in der Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: ac1e5dbe435d9e85e8ce3ad90c60dd31ba9248ff

---


# Erstellen eines Adobe Analytics-Quell-Connectors in der Benutzeroberfläche

In diesem Lernprogramm werden Schritte zum Erstellen eines Adobe Analytics-Quell-Connectors in der Benutzeroberfläche beschrieben, um Verbraucherdaten in die Adobe Experience Platform zu übertragen.

## Erstellen einer Quellverbindung mit Adobe Analytics

Melden Sie sich bei <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> an und wählen Sie dann in der linken Navigationsleiste die Option &quot; **Quellen** &quot;, um auf den Quellarbeitsbereich zuzugreifen. Im Anzeigebereich &quot; *Katalog* &quot;werden verfügbare Quellen zum Erstellen von gebundenen Verbindungen angezeigt. Jede Quelle zeigt die Anzahl der vorhandenen Verbindungen an, die mit ihnen verbunden sind. Wählen Sie die Option für **Adobe Analytics** und klicken Sie dann auf **Ansicht-Quelle** , um alle etablierten In-bound-Verbindungen anzuzeigen.

![](../../../../images/tutorials/create/analytics/AA-sources_catalog.png)

Im Bildschirm &quot; *Quellverbindung* &quot;werden alle zuvor eingerichteten Verbindungen zu Adobe Analytics Liste. Sie können eine neue Aktivität erstellen, indem Sie auf Daten **auswählen** klicken.

>[!NOTE] Es können mehrere eingehende Verbindungen zu einer Quelle hergestellt werden, um verschiedene Daten einzubringen.

![](/help/sources/images/tutorials/create/analytics/AA-source_activity.png)

Wählen Sie in der Liste der verfügbaren Report Suites die Report Suites aus, die Sie in die Plattform aufnehmen möchten, und klicken Sie auf **Weiter**.

>[!NOTE] Pro Analytics-Quellverbindung kann nur eine Report Suite ausgewählt werden. Darüber hinaus kann nur eine Report Suite in einer Sandbox vorhanden sein.

![](../../../../images/tutorials/create/analytics/AA-select_data.png)

Der *Review* -Schritt wird angezeigt, mit dem Sie Ihre neue Analytics-gebundene Verbindung überprüfen können, bevor sie erstellt wird. Die Verbindungsdetails werden nach Kategorien gruppiert, darunter:

* *Quelldetails*: Zeigt den Typ der Quellverbindung und die ausgewählte Report Suite an.
* *Angaben* zur Zielgruppe: Beim Erstellen anderer Quell-Connectors zeigt dieser Container, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, das der Datensatz einhält. Analytics-Daten werden automatisch zugeordnet und in Echtzeit-Kundendaten eingefügt.

![](../../../../images/tutorials/create/analytics/AA-review.png)

## Nächste Schritte

Nachdem die Verbindung erstellt wurde, wird automatisch ein Zielgruppe-Schema und ein Dataset erstellt, die die eingehenden Daten enthalten. Darüber hinaus erfolgt die Datensicherung und erfasst bis zu 13 Monate historische Daten. Nach Abschluss der anfänglichen Erfassung werden Analytics-Daten verwendet und von nachgeschalteten Plattformdiensten wie dem Echtzeit-Kundendienst und dem Segmentierungsdienst verwendet. Weitere Informationen finden Sie in den folgenden Dokumenten:

* [Übersicht über das Echtzeit-Kundenprofil](../../../../../profile/home.md)
* [Übersicht über den Segmentierungsdienst](../../../../../segmentation/home.md)
* [Übersicht über den Data Science Workspace](../../../../../data-science-workspace/home.md)
* [Übersicht über den Abfrage Service](../../../../../query-service/home.md)

