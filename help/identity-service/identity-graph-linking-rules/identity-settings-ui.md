---
title: Benutzeroberfläche für Identitätseinstellungen
description: Erfahren Sie, wie Sie die Benutzeroberfläche für Identitätseinstellungen verwenden.
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 605aa5ed2db2bfd7f787f2dff9fa00cee2afbce6
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

# Benutzeroberfläche für Identitätseinstellungen

>[!AVAILABILITY]
>
>Diese Funktion ist noch nicht verfügbar. Das Betaprogramm für Regeln zur Identitätsdiagrammverlinkung wird voraussichtlich im Juli für Entwicklungs-Sandboxes beginnen. Wenden Sie sich an Ihr Adobe-Account-Team, um Informationen zu den Teilnahmekriterien zu erhalten.

Identitätseinstellungen sind eine Funktion in der Benutzeroberfläche des Adobe Experience Platform Identity Service , mit der Sie eindeutige Namespaces bestimmen und die Namespace-Priorität konfigurieren können.

In diesem Handbuch erfahren Sie, wie Sie das Tool für Identitätseinstellungen verwenden.

## Voraussetzung

Lesen Sie die folgenden Dokumente, bevor Sie mit der Arbeit mit Identitätseinstellungen beginnen:

* [Identitätsoptimierungsalgorithmus](./identity-optimization-algorithm.md)
* [Namespace-Priorität](./namespace-priority.md)
* [Diagrammsimulation](./graph-simulation.md)

## Identitätseinstellungen konfigurieren

Um auf Identitätseinstellungen zuzugreifen, navigieren Sie in der Adobe Experience Platform-Benutzeroberfläche zum Arbeitsbereich &quot;Identity Service&quot;und wählen Sie **[!UICONTROL Einstellungen]**.

![Die Schaltfläche für die Identitätseinstellungen wurde ausgewählt.](../images/rules/identity-ui.png)

Die Seite mit den Identitätseinstellungen wird angezeigt. Sie erhalten eine Bestätigungsmeldung, die Sie daran erinnert, Ihre Identitätseinstellungen zuerst in einer Entwicklungs-Sandbox zu testen und zu validieren, bevor Sie Konfigurationen in einer Produktions-Sandbox abschließen.

![Die Seite mit den Identitätseinstellungen.](../images/rules/identity-settings.png)

Die Seite mit den Identitätseinstellungen ist in zwei Abschnitte unterteilt: [!UICONTROL Personen-Namespaces] und [!UICONTROL Geräte- oder Cookie-Namespaces]. Personen-Namespaces sind Bezeichner für einzelne Personen. Dabei kann es sich um geräteübergreifende IDs, E-Mail-Adressen und Telefonnummern handeln. Geräte- oder Cookie-Namespaces sind Kennungen für Geräte und Webbrowser und können nicht höher als Personen-Namespaces eingestuft werden. Sie können auch keinen Geräte- oder Cookie-Namespace als eindeutigen Namespace festlegen.

### Eindeutigen Namespace bestimmen

Um einen eindeutigen Namespace festzulegen, wählen Sie die [!UICONTROL Eindeutig pro Diagramm] -Kontrollkästchen, das diesem Namespace entspricht. Sie können mehr als einen eindeutigen Namespace für Ihre Identitätseinstellungen auswählen.

![Zwei eindeutige Namespaces wurden ausgewählt.](../images/rules/unique-namespaces.png)

Sobald Ihre eindeutigen Namespaces eingerichtet sind, können Diagramme nicht mehr mehrere Identitäten aufweisen, die einen eindeutigen Namespace enthalten. Wenn Sie beispielsweise die benutzerdefinierte Analytics-ID als eindeutigen Namespace festgelegt haben, kann ein Diagramm nur eine Identität mit dem benutzerdefinierten ID-Namespace von Analytics aufweisen. Weitere Informationen finden Sie im Abschnitt [Übersicht über den Identitätsoptimierungsalgorithmus](./identity-optimization-algorithm.md#unique-namespace).

### Namespace-Priorität konfigurieren

Um die Namespace-Priorität zu konfigurieren, wählen Sie im Menü für Identitätseinstellungen einen Namespace aus und ziehen Sie diesen Namespace per Drag-and-Drop in die Reihenfolge Ihrer Vorlieben. Platzieren Sie einen Namespace höher auf der Liste, um ihm eine höhere Priorität zu geben, und setzen Sie umgekehrt einen Namespace unter der Liste, um ihm eine niedrigere Priorität zu geben. Der Namespace mit der höchsten Priorität sollte auch als eindeutiger Namespace gekennzeichnet werden.

Wenn Sie mit Ihren Konfigurationen fertig sind, wählen Sie **[!UICONTROL Nächste]**. Es wird eine Bestätigungsmeldung angezeigt. Verwenden Sie diese Gelegenheit, um zu überprüfen, ob Ihre Konfigurationen korrekt sind, und wählen Sie dann **[!UICONTROL Beenden]**.

![Die Überprüfungsseite.](../images/rules/validate.png)

Es wird eine Warnung angezeigt, die angibt, dass Ihre neuen Einstellungen keine Auswirkungen auf vorhandene Links in einem Identitätsdiagramm und auf bereits erfasste Experience-Ereignisprofilfragmente haben. Geben Sie zur Bestätigung Ihren Sandbox-Namen ein und wählen Sie **[!UICONTROL Bestätigen]**.

![Das Bestätigungsfenster.](../images/rules/confirm.png)