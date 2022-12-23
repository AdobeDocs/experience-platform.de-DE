---
title: Abfragevorlagen
description: Abfragevorlagen sind wiederverwendbare gespeicherte SQL-Abfragen, die von anderen Benutzenden wiederverwendet werden können, um Zeit und Mühe zu sparen. Sie können mit dem Abfrage-Editor oder der Abfrage-Service-API erstellt werden und sind für alle Experience Platform-Datensätze verfügbar.
exl-id: e74d058f-bb89-45ed-83cc-2e3a33401270
source-git-commit: a085bac6b4ee825d534710ae91d6690fa076e873
workflow-type: ht
source-wordcount: '436'
ht-degree: 100%

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

Wählen Sie im Arbeitsbereich „Abfragen“ der Platform-Benutzeroberfläche die Option **[!UICONTROL Vorlagen]**, um die Liste der verfügbaren gespeicherten Abfragen anzuzeigen.

![Der Arbeitsbereich „Abfragen“ mit hervorgehobener Registerkarte „Vorlagen“.](../images/ui/query-templates/query-templates.png)

Um relevante Vorlageninformationen zu finden, klicken Sie auf eine beliebige Abfragevorlage aus der verfügbaren Liste, um das Detailbedienfeld zu öffnen.

![Das Detailbedienfeld im Arbeitsbereich „Abfragen“ mit hervorgehobener Abfrage-ID.](../images/ui/query-templates/details-panel.png)

### Erstellen einer Vorlage mithilfe der Abfrage-Service-API

In der Dokumentation finden Sie Anweisungen dazu, wie Sie mit der Abfrage-Service-API [eine Abfragevorlage erstellen](../api/query-templates.md#create-a-query-template). Die Details einer neu erstellten Abfragevorlage sind im Antworttext enthalten.

>[!NOTE]
>
>Vorlagen, die mit der API erstellt wurden, sind auch auf der Registerkarte „Abfrage-Service-Vorlagen“ der Platform-Benutzeroberfläche sichtbar.

## Nächste Schritte

Durch das Lesen dieses Dokuments können Sie jetzt besser verstehen, wie Sie im Abfrage-Service Abfragevorlagen erstellen. Weitere Informationen über die Funktionen des Abfrage-Services finden Sie in der [Benutzeroberflächen-Übersicht](./overview.md) oder im [Handbuch zur Abfrage-Service-API](../api/getting-started.md).

Weitere Informationen zum Planen von Abfragen mithilfe der API finden Sie im [Handbuch zu Endpunkten für geplante Abfragen](../api/scheduled-queries.md) oder im [Handbuch zum Abfrage-Editor](./user-guide.md#scheduled-queries) für die Benutzeroberfläche.
