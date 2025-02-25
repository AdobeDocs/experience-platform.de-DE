---
title: Benutzeroberfläche für Identitätseinstellungen
description: Erfahren Sie, wie Sie die Benutzeroberfläche für Identitätseinstellungen verwenden.
exl-id: 738b7617-706d-46e1-8e61-a34855ab976e
source-git-commit: 7c2e5cad997b7e7b9e0a08d3a3a1f5c9b218329e
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 4%

---

# Benutzeroberfläche für Identitätseinstellungen

>[!AVAILABILITY]
>
>Regeln zur Identitätsdiagramm-Verknüpfung sind derzeit nur eingeschränkt verfügbar. Wenden Sie sich an Ihr Adobe-Accountteam, um Informationen zum Zugriff auf die Funktion in Entwicklungs-Sandboxes zu erhalten.

Identitätseinstellungen sind eine Funktion in der Adobe Experience Platform Identity Service-Benutzeroberfläche, mit der Sie eindeutige Namespaces festlegen und die Namespace-Priorität konfigurieren können.

Lesen Sie dieses Handbuch, um zu erfahren, wie Sie Ihre Identitätseinstellungen in der Benutzeroberfläche konfigurieren.

## Voraussetzungen

Lesen Sie die folgenden Dokumente, bevor Sie mit Identitätseinstellungen arbeiten:

* [Verknüpfungsregeln für Identitätsdiagramme](./overview.md)
* [Algorithmus zur Identitätsoptimierung](./identity-optimization-algorithm.md)
* [Implementierungshandbuch](./implementation-guide.md)
* [Beispiele für Diagrammkonfigurationen](./example-configurations.md)
* [Namespace-Priorität](./namespace-priority.md)
* [Diagrammsimulation](./graph-simulation.md)

## Konfigurieren der Identitätseinstellungen

Um auf die Identitätseinstellungen zuzugreifen, navigieren Sie in der Benutzeroberfläche von Adobe Experience Platform zum Arbeitsbereich Identity Service und wählen Sie **[!UICONTROL Einstellungen]** aus.

![Die Schaltfläche Identitätseinstellungen ist ausgewählt.](../images/rules/identities-ui.png)

Die Seite mit den Identitätseinstellungen ist in zwei Abschnitte unterteilt: [!UICONTROL Personen-]) und [!UICONTROL Geräte- oder Cookie-]. Personen-Namespaces sind Bezeichner für einzelne Personen. Dabei kann es sich um geräteübergreifende IDs, E-Mail-Adressen und Telefonnummern handeln. Geräte- oder Cookie-Namespaces sind Bezeichner für Geräte und Webbrowser und können keine höhere Priorität als Personen-Namespaces erhalten. Sie können auch nicht festlegen, dass ein Geräte- oder Cookie-Namespace ein eindeutiger Namespace ist.

### Namespace-Priorität konfigurieren

Um die Namespace-Priorität zu konfigurieren, wählen Sie im Menü Identitätseinstellungen einen Namespace aus und ziehen Sie diesen Namespace dann per Drag-and-Drop in die gewünschte Reihenfolge. Platzieren Sie einen Namespace höher auf der Liste, um ihm eine höhere Priorität zu verleihen, und platzieren Sie umgekehrt einen Namespace niedriger auf der Liste, um ihm eine niedrigere Priorität zu verleihen. Der Namespace mit der höchsten Priorität sollte auch als eindeutiger Namespace gekennzeichnet werden.

![Der Arbeitsbereich „Identitätseinstellungen“ mit hervorgehobenem Namespace für Personen.](../images/rules/namespace-priority.png)

### Eindeutigen Namespace festlegen

Um einen eindeutigen Namespace festzulegen, aktivieren Sie das Kontrollkästchen [!UICONTROL Eindeutig pro Diagramm], das diesem Namespace entspricht. Sie können bis zu drei eindeutige Namespaces für Ihre Identitätskonfigurationseinstellungen auswählen.

![Zwei Namespaces ausgewählt und als eindeutig definiert.](../images/rules/unique-namespace.png)

Sobald Ihre eindeutigen Namespaces eingerichtet sind, können Diagramme nicht mehr mehrere Identitäten haben, die einen eindeutigen Namespace enthalten. Wenn Sie beispielsweise CRMID als eindeutigen Namespace angegeben haben, kann ein Diagramm nur eine Identität mit dem CRMID-Namespace haben. Weitere Informationen finden Sie unter [Übersicht über den Identitätsoptimierungsalgorithmus](./identity-optimization-algorithm.md#unique-namespace).

Wenn Sie mit den Konfigurationen fertig sind, klicken Sie auf **[!UICONTROL Weiter]**. Wenn eine Bestätigungsmeldung angezeigt wird, verwenden Sie diese Möglichkeit, um zu überprüfen, ob Ihre Konfigurationen korrekt sind, und wählen Sie dann **[!UICONTROL Beenden]**.

![Die Validierungsseite mit hervorgehobener Option „Beenden“.](../images/rules/finish.png)

Es wird eine Warnmeldung angezeigt, die darauf hinweist, dass vorhandene Diagramme nur dann vom Diagrammalgorithmus betroffen sind, wenn die Diagramme aktualisiert werden (**Speichern Ihrer Einstellungen** und dass die primäre Identität von Ereignisfragmenten im Echtzeit-Kundenprofil auch nach Änderungen der Namespace-Priorität nicht aktualisiert wird. Darüber hinaus erhalten Sie eine Benachrichtigung, dass es bis zu **sechs Stunden** dauern wird, bis Ihre neuen oder aktualisierten Einstellungen wirksam werden. Geben Sie zur Bestätigung Ihren Sandbox-Namen ein und wählen Sie **[!UICONTROL Bestätigen]**.

![Das Bestätigungsfenster, das eine Warnung zu einer sechsstündigen Verzögerung anzeigt, bevor Konfigurationen verarbeitet werden.](../images/rules/confirm-settings.png)

## Nächste Schritte

Weitere Informationen zu Verknüpfungsregeln für Identitätsdiagramme finden Sie in der folgenden Dokumentation:

* [Übersicht über Verknüpfungsregeln für Identitätsdiagramme](./overview.md)
* [Algorithmus zur Identitätsoptimierung](./identity-optimization-algorithm.md)
* [Implementierungshandbuch](./implementation-guide.md)
* [Beispiele für Diagrammkonfigurationen](./example-configurations.md)
* [Fehlerbehebung und häufig gestellte Fragen](./troubleshooting.md)
* [Namespace-Priorität](./namespace-priority.md)
* [Benutzeroberfläche für die Diagrammsimulation](./graph-simulation.md)