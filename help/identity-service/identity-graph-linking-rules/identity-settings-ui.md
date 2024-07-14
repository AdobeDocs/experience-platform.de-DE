---
title: Benutzeroberfläche für Identitätseinstellungen
description: Erfahren Sie, wie Sie die Benutzeroberfläche für Identitätseinstellungen verwenden.
badge: Beta
source-git-commit: 72773f9ba5de4387c631bd1aa0c4e76b74e5f1dc
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---

# Benutzeroberfläche für Identitätseinstellungen

>[!AVAILABILITY]
>
>Diese Funktion ist noch nicht verfügbar. Das Betaprogramm für Regeln zur Identitätsdiagrammverlinkung wird voraussichtlich im Juli für Entwicklungs-Sandboxes beginnen. Wenden Sie sich an Ihr Adobe-Account-Team, um Informationen zu den Teilnahmekriterien zu erhalten.

Identitätseinstellungen sind eine Funktion in der Benutzeroberfläche des Adobe Experience Platform Identity Service , mit der Sie eindeutige Namespaces bestimmen und die Namespace-Priorität konfigurieren können.

In diesem Handbuch erfahren Sie, wie Sie Ihre Identitätseinstellungen in der Benutzeroberfläche konfigurieren.

## Voraussetzungen

Lesen Sie die folgenden Dokumente, bevor Sie mit der Arbeit mit Identitätseinstellungen beginnen:

* [Konfigurationshandbuch für Regeln zur Verknüpfung von Identitätsdiagrammen](./configuration.md)
* [Identitätsoptimierungsalgorithmus](./identity-optimization-algorithm.md)
* [Namespace-Priorität](./namespace-priority.md)
* [Diagrammsimulation](./graph-simulation.md)

## Identitätseinstellungen konfigurieren

Um auf Identitätseinstellungen zuzugreifen, navigieren Sie in der Adobe Experience Platform-Benutzeroberfläche zum Arbeitsbereich &quot;Identity Service&quot;und wählen Sie dann **[!UICONTROL Einstellungen]** aus.

![Die ausgewählte Schaltfläche für die Identitätseinstellungen.](../images/rules/identities-ui.png)

Die Seite mit den Identitätseinstellungen ist in zwei Abschnitte unterteilt: [!UICONTROL Personen-Namespaces] und [!UICONTROL Geräte- oder Cookie-Namespaces]. Personen-Namespaces sind Bezeichner für einzelne Personen. Dabei kann es sich um geräteübergreifende IDs, E-Mail-Adressen und Telefonnummern handeln. Geräte- oder Cookie-Namespaces sind Kennungen für Geräte und Webbrowser und können nicht höher als Personen-Namespaces eingestuft werden. Sie können auch keinen Geräte- oder Cookie-Namespace als eindeutigen Namespace festlegen.

### Namespace-Priorität konfigurieren

Um die Namespace-Priorität zu konfigurieren, wählen Sie im Menü für Identitätseinstellungen einen Namespace aus und ziehen Sie diesen Namespace per Drag-and-Drop in die Reihenfolge Ihrer Vorlieben. Platzieren Sie einen Namespace höher auf der Liste, um ihm eine höhere Priorität zu geben, und setzen Sie umgekehrt einen Namespace unter der Liste, um ihm eine niedrigere Priorität zu geben. Der Namespace mit der höchsten Priorität sollte auch als eindeutiger Namespace gekennzeichnet werden.

![Der Arbeitsbereich für Identitätseinstellungen mit einem Personen-Namespace hervorgehoben.](../images/rules/namespace-priority.png)

### Eindeutigen Namespace bestimmen

Um einen eindeutigen Namespace zu bestimmen, aktivieren Sie das Kontrollkästchen [!UICONTROL Eindeutig pro Diagramm] , das diesem Namespace entspricht. Sie können mehr als einen eindeutigen Namespace für Ihre Identitätseinstellungen auswählen.

![Zwei Namespaces wurden ausgewählt und als eindeutig definiert.](../images/rules/unique-namespace.png)

Sobald Ihre eindeutigen Namespaces eingerichtet sind, können Diagramme nicht mehr mehrere Identitäten aufweisen, die einen eindeutigen Namespace enthalten. Wenn Sie beispielsweise die CRM-ID als eindeutigen Namespace festgelegt haben, darf ein Diagramm nur eine Identität mit dem CRM-ID-Namespace enthalten. Weitere Informationen finden Sie in der Übersicht zum [Identitätsoptimierungsalgorithmus](./identity-optimization-algorithm.md#unique-namespace) .

Wenn Sie mit Ihren Konfigurationen fertig sind, wählen Sie **[!UICONTROL Weiter]** aus. Es wird eine Bestätigungsmeldung angezeigt. Verwenden Sie diese Gelegenheit, um zu überprüfen, ob Ihre Konfigurationen korrekt sind, und wählen Sie dann **[!UICONTROL Beenden]** aus.

![Die Überprüfungsseite mit hervorgehobenem Abschluss.](../images/rules/finish.png)

Es wird eine Warnung angezeigt, die angibt, dass Ihre neuen Einstellungen keine Auswirkungen auf vorhandene Links in einem Identitätsdiagramm und auf bereits erfasste Experience-Ereignisprofilfragmente haben. Außerdem werden Sie darüber informiert, dass es bis zu sechs Stunden dauern wird, bis Ihre neuen Einstellungen im System angezeigt werden. Geben Sie zur Bestätigung Ihren Sandbox-Namen ein und wählen Sie dann **[!UICONTROL Bestätigen]** aus.

![Das Bestätigungsfenster, das eine Warnung über eine sechsstündige Verzögerung anzeigt, bevor Konfigurationen verarbeitet werden.](../images/rules/confirm-settings.png)

## Nächste Schritte

Sie haben jetzt Ihre Namespace-Prioritäten konfiguriert und Ihre eindeutigen Namespaces mithilfe der UI-Seite mit den Identitätseinstellungen zugewiesen. Weitere Informationen finden Sie in der Übersicht über die Regeln zur Verknüpfung von Identitätsdiagrammen](./overview.md).[