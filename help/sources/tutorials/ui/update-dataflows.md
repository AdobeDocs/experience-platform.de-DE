---
description: Erfahren Sie, wie Sie einen vorhandenen Quell-Datenfluss in der Experience Platform-Benutzeroberfläche aktualisieren.
title: Aktualisieren eines Source-Verbindungsdatenflusses in der Benutzeroberfläche
exl-id: 0499a2a3-5a22-47b1-ac0e-76a432bd26c0
source-git-commit: 4c4f221a5060360fa0381c8532227e854ad40a77
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 9%

---

# Aktualisieren von Datenflüssen in der Benutzeroberfläche

Lesen Sie dieses Tutorial, um zu erfahren, wie Sie einen vorhandenen Datenfluss aktualisieren können, einschließlich seines Zeitplans und seiner Zuordnungskonfigurationen, indem Sie den Arbeitsbereich „Quellen“ in der Benutzeroberfläche von Adobe Experience Platform verwenden.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [Quellen](../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse besser entwickeln und weiterentwickeln können.

## Aktualisieren von Datenflüssen {#update-dataflows}

>[!CONTEXTUALHELP]
>id="platform_sources_dataflows_daysRemaining"
>title="Ablaufdatum des Datensatzes"
>abstract="Diese Spalte gibt die Anzahl der Tage an, die verbleiben, bis der Zieldatensatz automatisch abläuft.<br>Ein Datenfluss schlägt fehl, wenn der Zieldatensatz abgelaufen ist. Um zu verhindern, dass ein Datenfluss fehlschlägt, muss sichergestellt werden, dass der Zieldatensatz am richtigen Datum abläuft. Informationen zum Aktualisieren der Ablaufdaten finden Sie in der Dokumentation."

Wählen Sie in der Experience Platform-Benutzeroberfläche im linken Navigationsbereich die Option **[!UICONTROL Sources]** und dann in der oberen Zeile die Option **[!UICONTROL Dataflows]** aus.

![Der Quellkatalog mit der ausgewählten Kopfzeile „Datenflüsse“.](../../images/tutorials/update-dataflows/catalog.png)

>[!TIP]
>
>Mit Filterfunktionen können Sie Ihre Datenflüsse sortieren und filtern. Weitere Informationen finden Sie [ Handbuch unter „Filtern von Quellobjekten in ](./filter.md) Benutzeroberfläche“.

Auf der Seite [!UICONTROL Dataflows] wird eine Liste aller vorhandenen Datenflüsse in Ihrer Organisation angezeigt. Suchen Sie den Datenfluss, den Sie aktualisieren möchten, und wählen Sie die Auslassungspunkte (`...`) daneben aus. Es wird ein Dropdown-Menü mit einer Liste von Optionen angezeigt, aus denen Sie auswählen können, um zusätzliche Konfigurationen an Ihrem vorhandenen Datenfluss vorzunehmen.

Um Ihren Datenfluss zu aktualisieren, wählen Sie **[!UICONTROL Update dataflow]** aus.

![Das Dropdown-Menü, in dem Optionen zum Aktualisieren von Datenflüssen aufgeführt sind.](../../images/tutorials/update-dataflows/dropdown_update.png)

Sie werden zum Quellen-Workflow weitergeleitet, in dem Sie Aspekte Ihres Datenflusses aktualisieren können, einschließlich der Details im [!UICONTROL Provide dataflow details] Schritt.

### Aktualisieren der Zuordnung {#update-mapping}

>[!NOTE]
>
>Die Funktion „Zuordnung bearbeiten“ wird derzeit für die folgenden Quellen nicht unterstützt: Adobe Analytics, Adobe Audience Manager, HTTP-API und [!DNL Marketo Engage].

Während dieses Vorgangs können Sie auch die mit Ihrem Datenfluss verknüpften Zuordnungssätze aktualisieren.  In der Zuordnungsschnittstelle wird die vorhandene Zuordnung Ihres Datenflusses angezeigt und nicht ein neuer empfohlener Zuordnungssatz. Zuordnungsaktualisierungen werden nur auf Datenflussausführungen angewendet, die in der Zukunft geplant sind. Bei einem Datenfluss, der für eine einmalige Aufnahme geplant war, können die Zuordnungssätze nicht aktualisiert werden.

Verwenden Sie die Zuordnungsschnittstelle, um die auf Ihren Datenfluss angewendeten Zuordnungssätze zu ändern. Eine ausführliche Anleitung zur Verwendung der Zuordnungsschnittstelle finden Sie im [Handbuch zur Datenvorbereitungs-](../../../data-prep/ui/mapping.md)).

![Der Zuordnungsschritt des Quell-Workflows. Verwenden Sie diesen Schritt, um die mit Ihrem Datenfluss verknüpften Zuordnungen zu aktualisieren.](../../images/tutorials/update-dataflows/mapping.png)

### Zeitplan aktualisieren

Nachdem Sie die Zuordnungen Ihres Datenflusses aktualisiert haben, können Sie Ihren Aufnahmezeitplan aktualisieren, um Ihren Datenfluss mit den neuen Zuordnungsdaten aufzunehmen. Sie können den Aufnahmezeitplan nur von Datenflüssen aktualisieren, die für die Aufnahme in einem wiederkehrenden Zeitplan konfiguriert wurden. Sie können einen Datenfluss, der für eine einmalige Aufnahme konfiguriert wurde, nicht neu planen.

Sie können den Aufnahmezeitplan Ihres Datenflusses auch mithilfe der Option Inline-Aktualisierung aktualisieren, die auf der Seite Datenflüsse bereitgestellt wird.

Wählen Sie auf der Seite Datenflüsse die Auslassungszeichen (`...`) neben dem Namen des Datenflusses und wählen Sie dann **[!UICONTROL Edit schedule]** aus dem angezeigten Dropdown-Menü.

![Der Planungsschritt des Quell-Workflows. Verwenden Sie diesen Schritt, um den Zeitplan Ihres Datenflusses zu aktualisieren.](../../images/tutorials/update-dataflows/dropdown_edit.png)

Das Dialogfeld &quot;**[!UICONTROL Edit schedule]**&quot; enthält Optionen zum Aktualisieren der Aufnahmefrequenz und der Intervallrate Ihres Datenflusses. Nachdem Sie die aktualisierten Werte für Häufigkeit und Intervall festgelegt haben, wählen Sie **[!UICONTROL Save]** aus.

![Ein Popup-Fenster, mit dem Sie den Aufnahmezeitplan Ihres Datenflusses bearbeiten können.](../../images/tutorials/update-dataflows/edit_schedule.png)

Lesen Sie den folgenden Abschnitt für Details zur Funktionsweise wöchentlicher Aufnahmezeitpläne.

#### Grundlagen zum wöchentlichen Aufnahmezeitplan {#weekly}

Wenn Sie Ihren Datenfluss so einstellen, dass er nach einem wöchentlichen Zeitplan ausgeführt wird, wird der Datenfluss auf der Grundlage eines der folgenden Szenarien ausgeführt:

* Wenn Ihre Datenquelle erstellt wurde, aber noch keine Daten aufgenommen wurden, wird der erste wöchentliche Datenfluss 7 Tage nach dem Erstellungsdatum der Quelle ausgeführt. Dieses 7-Tage-Intervall beginnt immer mit dem Zeitpunkt, zu dem die Quelle erstellt wurde, unabhängig davon, wann Sie den Zeitplan einrichten. Nach der ersten Ausführung wird der Datenfluss weiterhin wöchentlich gemäß dem konfigurierten Zeitplan ausgeführt.
* Wenn Daten aus Ihrer Quelle zuvor aufgenommen wurden und Sie sie erneut für die wöchentliche Aufnahme planen, wird der nächste Datenfluss 7 Tage nach der letzten erfolgreichen Aufnahme ausgeführt.

### Datenfluss deaktivieren

Sie können Ihren Datenfluss mithilfe desselben Dropdown-Menüs deaktivieren. Um Ihren Datenfluss zu deaktivieren, wählen Sie **[!UICONTROL Disable dataflow]** aus.

![Das Dropdown-Menü mit der Option zum Deaktivieren des Datenflusses.](../../images/tutorials/update-dataflows/dropdown_disable.png)

Wählen Sie als Nächstes [!UICONTROL Disable] aus dem angezeigten Popup-Fenster aus.

![Das Popup-Fenster, in dem Sie bestätigen müssen, dass Sie Ihren Datenfluss deaktivieren möchten.](../../images/tutorials/update-dataflows/disable_dataflow.png)

Wenn Sie diesen Datenfluss später erneut aktivieren, plant Experience Platform automatisch Aufstockungsausführungen, um den Zeitraum abzudecken, in dem der Datenfluss deaktiviert wurde. Wenn der Datenfluss beispielsweise für die stündliche Ausführung konfiguriert und für 48 Stunden deaktiviert wurde, erstellt Experience Platform nach der erneuten Aktivierung dieses Datenflusses 48 Aufstockungsausführungen, um die fehlenden Intervalle zu verarbeiten.

## Nächste Schritte

In diesem Tutorial haben Sie den [!UICONTROL Sources]-Arbeitsbereich erfolgreich verwendet, um den Aufnahmezeitplan und die Zuordnungssätze Ihres Datenflusses zu aktualisieren.

Anweisungen zum programmgesteuerten Ausführen dieser Vorgänge mithilfe der [!DNL Flow Service]-API finden Sie im Tutorial zum [Aktualisieren von Datenflüssen mithilfe der Flow Service-API](../../tutorials/api/update-dataflows.md).
