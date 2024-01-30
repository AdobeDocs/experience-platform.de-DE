---
title: Abfragevorlagen
description: Abfragevorlagen sind wiederverwendbare gespeicherte SQL-Abfragen, die von anderen Benutzenden wiederverwendet werden können, um Zeit und Mühe zu sparen. Sie können mit dem Abfrage-Editor oder der Abfrage-Service-API erstellt werden und sind für alle Experience Platform-Datensätze verfügbar.
exl-id: e74d058f-bb89-45ed-83cc-2e3a33401270
source-git-commit: 1a44be939a4678078b414658199472e07dee153b
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 73%

---

# Abfragevorlagen

Mit dem Abfrage-Service von Adobe Experience Platform können Sie SQL-Code in Form von Abfragevorlagen speichern und wiederverwenden. Vorlagen sparen Arbeit, da häufig ausgeführte Aufgaben nicht wiederholt werden müssen. Sie können Vorlagen in Ihrer Organisation freigeben und die Abfragewerte einfach ändern, ohne auf die zugrunde liegende SQL zugreifen oder sie verstehen zu müssen.

Dieses Dokument enthält die Informationen, die zum Erstellen von Abfragevorlagen im Abfrage-Service erforderlich sind.

## Voraussetzungen

Die Berechtigung [!UICONTROL Abfragen verwalten] muss aktiviert sein, damit Sie auf den Abfrage-Editor zugreifen und das Abfrage-Dashboard in der Platform-Benutzeroberfläche anzeigen können. Die Berechtigung wird über die Adobe [Admin Console](https://adminconsole.adobe.com/) aktiviert. Bitte wenden Sie sich an den Admin Ihrer Organisation, wenn Sie keine Administratorberechtigungen haben, um diese Berechtigung zu aktivieren. In der Dokumentation zur Zugriffskontrolle finden Sie [vollständige Anweisungen zum Hinzufügen von Berechtigungen über die Admin Console](../../access-control/home.md).

## Abfragevorlage erstellen

Sie können Abfragevorlagen auf zwei Arten erstellen: entweder indem Sie eine POST-Anfrage an den `query-templates`-Endpunkt der Abfrage-Service-API stellen, oder indem Sie eine Abfrage über den Abfrage-Editor schreiben, benennen und speichern.

### Erstellen und Speichern einer Abfrage als Vorlage mithilfe des Abfrage-Editors

In der Dokumentation finden Sie Anweisungen dazu, wie Sie mit dem Abfrage-Editor [Abfragen schreiben](./user-guide.md#query-authoring) und [speichern](./user-guide.md#saving-queries) können. Nachdem Sie Ihre Abfrage benannt und gespeichert haben, kann sie als Abfragevorlage über die Registerkarte [!UICONTROL Vorlagen] wiederverwendet werden.

>[!TIP]
>
>Wenn Sie eine Abfrage im Abfrage-Editor speichern, wird eine Bestätigungsmeldung angezeigt, die Sie über die erfolgreiche Aktion informiert. Diese Popup-Nachricht enthält einen Link, der eine praktische Möglichkeit bietet, zum Arbeitsbereich &quot;Planung von Abfragen&quot;zu navigieren. Siehe [Planungsabfragedokumentation](./query-schedules.md) , um zu erfahren, wie Sie Abfragen für eine benutzerdefinierte Cadence ausführen.

## Abfragevorlagen durchsuchen {#browse}

Wählen Sie im Arbeitsbereich „Abfragen“ der Platform-Benutzeroberfläche die Option **[!UICONTROL Vorlagen]**, um die Liste der verfügbaren gespeicherten Abfragen anzuzeigen.

![Der Arbeitsbereich „Abfragen“ mit hervorgehobener Registerkarte „Vorlagen“.](../images/ui/query-templates/query-templates.png)

Um relevante Vorlageninformationen zu finden, klicken Sie auf eine beliebige Abfragevorlage aus der verfügbaren Liste, um das Detailbedienfeld zu öffnen.

![Das Detailbedienfeld im Arbeitsbereich „Abfragen“ mit hervorgehobener Abfrage-ID.](../images/ui/query-templates/details-panel.png)

Im Detailbereich können Sie die folgenden Aktionen ausführen:

* Auswählen **[!UICONTROL Als CTAS ausführen]** , um eine neue Tabelle durch Auswahl von Daten aus einer oder mehreren existierenden Tabellen zu erstellen. Diese Option ist nur verfügbar, wenn Sie über eine SELECT-Abfrage verfügen.
* Auswählen **[!UICONTROL Zeitplan hinzufügen]** um mit der Bearbeitung Ihres Zeitplans für Ihre Abfragevorlage zu beginnen.
* Auswählen **[!UICONTROL Zeitplan anzeigen]** , um zur [!UICONTROL Zeitpläne] im Abfrage-Editor. Diese Ansicht enthält alle Planinformationen, die mit der Abfrage verknüpft sind.
* Auswählen **[!UICONTROL Abfrage löschen]** , um die Vorlage zu löschen.
* Wählen Sie den Vorlagennamen aus, um zum Abfrage-Editor zu navigieren, in dem die SQL vorab zur Bearbeitung ausgefüllt ist.

### Erstellen einer Vorlage mithilfe der Abfrage-Service-API

In der Dokumentation finden Sie Anweisungen dazu, wie Sie mit der Abfrage-Service-API [eine Abfragevorlage erstellen](../api/query-templates.md#create-a-query-template). Die Details einer neu erstellten Abfragevorlage sind im Antworttext enthalten.

>[!NOTE]
>
>Vorlagen, die mit der API erstellt wurden, sind auch auf der Registerkarte „Abfrage-Service-Vorlagen“ der Platform-Benutzeroberfläche sichtbar.

## Nächste Schritte

Durch das Lesen dieses Dokuments können Sie jetzt besser verstehen, wie Sie im Abfrage-Service Abfragevorlagen erstellen. Weitere Informationen über die Funktionen des Abfrage-Services finden Sie in der [Benutzeroberflächen-Übersicht](./overview.md) oder im [Handbuch zur Abfrage-Service-API](../api/getting-started.md).

Weitere Informationen zum Planen von Abfragen mithilfe der API finden Sie im [Handbuch zu Endpunkten für geplante Abfragen](../api/scheduled-queries.md) oder im [Handbuch zum Abfrage-Editor](./user-guide.md#scheduled-queries) für die Benutzeroberfläche.
