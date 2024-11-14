---
title: Benutzeroberfläche für Identitätseinstellungen
description: Erfahren Sie, wie Sie die Benutzeroberfläche für Identitätseinstellungen verwenden.
exl-id: 738b7617-706d-46e1-8e61-a34855ab976e
source-git-commit: ee0f6d6dbbbdf55a1a0f10038b785e48f2b41474
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 1%

---

# Benutzeroberfläche für Identitätseinstellungen

>[!AVAILABILITY]
>
>Die Regeln zur Verknüpfung von Identitätsdiagrammen sind derzeit nur eingeschränkt verfügbar. Wenden Sie sich an Ihr Adobe-Account-Team, um Informationen zum Zugriff auf die Funktion in Entwicklungs-Sandboxes zu erhalten.

Identitätseinstellungen sind eine Funktion in der Benutzeroberfläche des Adobe Experience Platform Identity Service , mit der Sie eindeutige Namespaces bestimmen und die Namespace-Priorität konfigurieren können.

In diesem Handbuch erfahren Sie, wie Sie Ihre Identitätseinstellungen in der Benutzeroberfläche konfigurieren.

## Voraussetzungen

Lesen Sie die folgenden Dokumente, bevor Sie mit der Arbeit mit Identitätseinstellungen beginnen:

* [Verknüpfungsregeln für Identitätsdiagramme](./overview.md)
* [Identitätsoptimierungsalgorithmus](./identity-optimization-algorithm.md)
* [Implementierungshandbuch](./implementation-guide.md)
* [Beispiele für Diagrammkonfigurationen](./example-configurations.md)
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

Sobald Ihre eindeutigen Namespaces eingerichtet sind, können Diagramme nicht mehr mehrere Identitäten aufweisen, die einen eindeutigen Namespace enthalten. Wenn Sie beispielsweise CRMID als eindeutigen Namespace festgelegt haben, kann ein Diagramm nur eine Identität mit dem CRMID-Namespace enthalten. Weitere Informationen finden Sie in der Übersicht zum [Identitätsoptimierungsalgorithmus](./identity-optimization-algorithm.md#unique-namespace) .

Wenn Sie mit Ihren Konfigurationen fertig sind, wählen Sie **[!UICONTROL Weiter]** aus. Es wird eine Bestätigungsmeldung angezeigt. Verwenden Sie diese Gelegenheit, um zu überprüfen, ob Ihre Konfigurationen korrekt sind, und wählen Sie dann **[!UICONTROL Beenden]** aus.

![Die Überprüfungsseite mit hervorgehobenem Abschluss.](../images/rules/finish.png)

Es wird eine Warnmeldung angezeigt, die besagt, dass vorhandene Diagramme nur dann vom Diagrammalgorithmus betroffen sind, wenn die Diagramme nach dem Speichern Ihrer Einstellungen aktualisiert werden **und dass die primäre Identität von Ereignisfragmenten im Echtzeit-Kundenprofil nicht aktualisiert wird, selbst wenn sich die Namespace-Priorität ändert.** Darüber hinaus werden Sie benachrichtigt, dass es bis zu **sechs Stunden** dauern wird, bis Ihre neuen oder aktualisierten Einstellungen wirksam werden. Geben Sie zur Bestätigung Ihren Sandbox-Namen ein und wählen Sie dann **[!UICONTROL Bestätigen]** aus.

![Das Bestätigungsfenster, das eine Warnung über eine sechsstündige Verzögerung anzeigt, bevor Konfigurationen verarbeitet werden.](../images/rules/confirm-settings.png)

## Nächste Schritte

Weitere Informationen zu Regeln zur Verknüpfung von Identitätsdiagrammen finden Sie in der folgenden Dokumentation:

* [Übersicht über die Verknüpfungsregeln von Identitätsdiagrammen](./overview.md)
* [Identitätsoptimierungsalgorithmus](./identity-optimization-algorithm.md)
* [Implementierungshandbuch](./implementation-guide.md)
* [Beispiele für Diagrammkonfigurationen](./example-configurations.md)
* [Fehlerbehebung und häufig gestellte Fragen](./troubleshooting.md)
* [Namespace-Priorität](./namespace-priority.md)
* [Benutzeroberfläche der Diagrammsimulation](./graph-simulation.md)