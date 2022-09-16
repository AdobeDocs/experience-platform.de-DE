---
title: Abfragevorlagen
description: Abfragevorlagen sind wiederverwendbare gespeicherte SQL-Abfragen, die von anderen Benutzern wiederverwendet werden können, um Zeit und Mühe zu sparen. Sie können mit dem Abfrage-Editor oder der Query Service-API erstellt werden und sind für alle Experience Platform-Datensätze verfügbar.
exl-id: e74d058f-bb89-45ed-83cc-2e3a33401270
source-git-commit: b6aaa3baaf8b3ff139ba6ebc7f14ac283ad52241
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 2%

---

# Abfragevorlagen

Mit Adobe Experience Platform Query Service können Sie SQL-Code in Form von Abfragevorlagen speichern und wiederverwenden. Vorlagen ersparen Aufwand, da häufig ausgeführte Aufgaben nicht wiederholt werden. Sie können Vorlagen in Ihrem Unternehmen freigeben und die Abfragewerte einfach ändern, ohne auf die zugrunde liegende SQL zugreifen oder sie verstehen zu müssen.

Dieses Dokument enthält die Informationen, die zum Erstellen von Abfragevorlagen in Query Service erforderlich sind.

## Voraussetzungen

Sie müssen über die [!UICONTROL Abfragen verwalten] Zugriff auf den Abfrage-Editor und die Anzeige des Abfragen-Dashboards in der Platform-Benutzeroberfläche aktiviert. Die Berechtigung wird über die Adobe aktiviert [Admin Console](https://adminconsole.adobe.com/). Wenden Sie sich an den Administrator Ihrer Organisation, wenn Sie keine Administratorberechtigungen haben, um diese Berechtigung zu aktivieren. Weitere Informationen finden Sie in der Dokumentation zur Zugriffskontrolle für [Vollständige Anweisungen zum Hinzufügen von Berechtigungen über die Admin Console](../../access-control/home.md).

## Abfragevorlage erstellen

Sie können Abfragevorlagen auf zwei Arten erstellen, indem Sie entweder eine POST-Anfrage an die Query Service-API richten `query-templates` -Endpunkt oder durch Schreiben, Benennen und Speichern einer Abfrage im Abfrage-Editor.

### Verwenden Sie den Abfrage-Editor, um eine Abfrage zu erstellen und als Vorlage zu speichern.

In der Dokumentation finden Sie Anweisungen zur Verwendung des Abfrage-Editors für [schreiben](./user-guide.md#query-authoring) und [Abfragen speichern](./user-guide.md#saving-queries). Nachdem Sie Ihre Abfrage benannt und gespeichert haben, kann sie als Abfragevorlage aus dem [!UICONTROL Durchsuchen] Registerkarte.

Wählen Sie im Arbeitsbereich Abfragen der Platform-Benutzeroberfläche die Option **[!UICONTROL Durchsuchen]** , um die Liste der verfügbaren gespeicherten Abfragen anzuzeigen.

![Der Arbeitsbereich &quot;Abfragen&quot;mit der Registerkarte &quot;Durchsuchen&quot;wurde hervorgehoben.](../images/ui/query-templates/query-templates.png)

Um relevante Vorlageninformationen zu finden, wählen Sie eine beliebige Abfragevorlage aus der verfügbaren Liste aus, um den Detailbereich zu öffnen.

![Das Detailbedienfeld im Arbeitsbereich &quot;Abfragen&quot;mit hervorgehobener Abfrage-ID.](../images/ui/query-templates/details-panel.png)

### Verwenden der Query Service-API zum Erstellen einer Vorlage

Anweisungen finden Sie in der Dokumentation zu [Erstellung einer Abfragevorlage](../api/query-templates.md#create-a-query-template) Verwendung der Query Service-API. Die Details einer neu erstellten Abfragevorlage sind im Antworttext enthalten.

>[!NOTE]
>
>Vorlagen, die mit der API erstellt wurden, sind auch auf der Registerkarte &quot;Query Service&quot;der Platform-Benutzeroberfläche sichtbar.

## Nächste Schritte

Durch Lesen dieses Dokuments können Sie jetzt besser verstehen, wie Sie in Query Service Abfragevorlagen erstellen. Siehe [Übersicht über die Benutzeroberfläche](./overview.md)oder [Handbuch zur Query Service-API](../api/getting-started.md) , um mehr über die Funktionen von Query Service zu erfahren.

Siehe [Endpunktleitfaden für geplante Abfragen](../api/scheduled-queries.md) , um zu erfahren, wie Sie Abfragen mithilfe der API planen, oder die [Anleitung zum Abfrage-Editor](./user-guide.md#scheduled-queries) für die Benutzeroberfläche.
