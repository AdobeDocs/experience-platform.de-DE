---
description: Erfahren Sie, wie Sie einen Datenfluss für vorhandene Quellen in der Experience Platform-Benutzeroberfläche aktualisieren.
title: Aktualisieren eines Source-Verbindungsdatenflusses in der Benutzeroberfläche
exl-id: 0499a2a3-5a22-47b1-ac0e-76a432bd26c0
source-git-commit: c3082a8769f317407197b3fd05b36cfe00b36470
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 17%

---

# Aktualisieren von Datenflüssen in der Benutzeroberfläche

In diesem Tutorial erfahren Sie, wie Sie einen vorhandenen Datenfluss aktualisieren, einschließlich Zeitplan- und Zuordnungskonfigurationen, indem Sie den Arbeitsbereich &quot;Quellen&quot;in der Benutzeroberfläche von Adobe Experience Platform verwenden.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [Quellen](../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

## Aktualisieren von Datenflüssen {#update-dataflows}

>[!CONTEXTUALHELP]
>id="platform_sources_dataflows_daysRemaining"
>title="Ablaufdatum des Datensatzes"
>abstract="Diese Spalte gibt die Anzahl der Tage an, die verbleiben, bis der Zieldatensatz automatisch abläuft.<br>Ein Datenfluss schlägt fehl, wenn der Zieldatensatz abgelaufen ist. Um zu verhindern, dass ein Datenfluss fehlschlägt, muss sichergestellt werden, dass der Zieldatensatz am richtigen Datum abläuft. Informationen zum Aktualisieren der Ablaufdaten finden Sie in der Dokumentation."

Wählen Sie in der Experience Platform-Benutzeroberfläche im linken Navigationsbereich **[!UICONTROL Quellen]** und dann **[!UICONTROL Datenflüsse]** aus der oberen Kopfzeile.

![Der Quellkatalog mit der ausgewählten Registerkarte &quot;Datenfluss-Kopfzeile&quot;.](../../images/tutorials/update-dataflows/catalog.png)

>[!TIP]
>
>Sie können Ihre Datenflüsse mithilfe von Filterfunktionen sortieren und filtern. Weitere Informationen finden Sie im Handbuch zum [Filtern von Quellenobjekten in der Benutzeroberfläche](./filter.md) .

Auf der Seite [!UICONTROL Datenflüsse] wird eine Liste aller vorhandenen Datenflüsse in Ihrer Organisation angezeigt. Suchen Sie den zu aktualisierenden Datenfluss und wählen Sie dann die Auslassungspunkte (`...`) daneben aus. Es wird ein Dropdown-Menü mit einer Liste von Optionen angezeigt, aus denen Sie auswählen können, um zusätzliche Konfigurationen für Ihren vorhandenen Datenfluss vorzunehmen.

Um Ihren Datenfluss zu aktualisieren, wählen Sie **[!UICONTROL Datenfluss aktualisieren]** aus.

![Das Dropdown-Menü, in dem Optionen zum Aktualisieren von Datenflüssen aufgelistet sind.](../../images/tutorials/update-dataflows/dropdown_update.png)

Sie werden zum Ursprungs-Workflow geleitet, in dem Sie mit der Aktualisierung von Aspekten Ihres Datenflusses fortfahren können, einschließlich der Details im Schritt [!UICONTROL Datenfluss-Details bereitstellen] .

### Aktualisieren der Zuordnung {#update-mapping}

>[!NOTE]
>
>Die Bearbeitungszuordnungsfunktion wird für die folgenden Quellen derzeit nicht unterstützt: Adobe Analytics, Adobe Audience Manager, HTTP-API und [!DNL Marketo Engage].

Während dieses Vorgangs können Sie auch die Ihrem Datenfluss zugeordneten Zuordnungssätze aktualisieren.  Die Zuordnungsschnittstelle zeigt die vorhandene Zuordnung Ihres Datenflusses und keinen neuen empfohlenen Zuordnungssatz an. Zuordnungsaktualisierungen werden nur auf in der Zukunft geplante Datenfluss-Läufe angewendet. Für einen Datenfluss, der für die einmalige Erfassung geplant war, können die Zuordnungssätze nicht aktualisiert werden.

Verwenden Sie die Zuordnungsschnittstelle, um die auf Ihren Datenfluss angewendeten Zuordnungssätze zu ändern. Umfassende Schritte zur Verwendung der Zuordnungsschnittstelle finden Sie im [UI-Handbuch zur Datenvorbereitung](../../../data-prep/ui/mapping.md) weitere Informationen.

![Der Zuordnungsschritt des Ursprungs-Workflows. Verwenden Sie diesen Schritt, um die mit Ihrem Datenfluss verknüpften Zuordnungen zu aktualisieren.](../../images/tutorials/update-dataflows/mapping.png)

### Zeitplan aktualisieren

Nachdem Sie die Zuordnungen Ihres Datenflusses aktualisiert haben, können Sie Ihren Aufnahmeplan aktualisieren, um Ihren Datenfluss mit den neuen Zuordnungsdaten zu erfassen. Sie können nur den Erfassungszeitplan der Datenflüsse aktualisieren, die für die Aufnahme in einem wiederkehrenden Zeitplan konfiguriert wurden. Sie können einen Datenfluss, der für die einmalige Erfassung konfiguriert wurde, nicht neu planen.

Sie können auch den Aufnahmezeitplan Ihres Datenflusses aktualisieren, indem Sie die Option Inline-Update verwenden, die auf der Datenflussseite bereitgestellt wird.

Wählen Sie auf der Seite &quot;Datenflüsse&quot;die Auslassungszeichen (`...`) neben dem Namen des Datenflusses aus und wählen Sie dann **[!UICONTROL Zeitplan bearbeiten]** aus dem angezeigten Dropdown-Menü.

![Der Planungsschritt des Ursprungs-Workflows. Verwenden Sie diesen Schritt, um den Zeitplan Ihres Datenflusses zu aktualisieren.](../../images/tutorials/update-dataflows/dropdown_edit.png)

Das Dialogfeld **[!UICONTROL Zeitplan bearbeiten]** bietet Optionen zum Aktualisieren der Erfassungsfrequenz und Intervallrate Ihres Datenflusses. Nachdem Sie die aktualisierten Werte für Häufigkeit und Intervall festgelegt haben, wählen Sie **[!UICONTROL Speichern]** aus.

![Ein Popup-Fenster, in dem Sie den Aufnahmezeitplan Ihres Datenflusses bearbeiten können.](../../images/tutorials/update-dataflows/edit_schedule.png)

### Datenfluss deaktivieren

Sie können Ihren Datenfluss über dasselbe Dropdown-Menü deaktivieren. Um den Datenfluss zu deaktivieren, wählen Sie **[!UICONTROL Datenfluss deaktivieren]** aus.

![Das Dropdown-Menü mit der Option zum Deaktivieren des Datenflusses.](../../images/tutorials/update-dataflows/dropdown_disable.png)

Wählen Sie als Nächstes [!UICONTROL Deaktivieren] aus dem angezeigten Popup-Fenster.

![Das Popup-Fenster, in dem Sie bestätigen müssen, dass Sie Ihren Datenfluss deaktivieren möchten.](../../images/tutorials/update-dataflows/disable_dataflow.png)

Wenn Sie diesen Datenfluss später erneut aktivieren, plant Experience Platform automatisch Aufstockungsläufe, um den Zeitraum abzudecken, in dem der Datenfluss deaktiviert wurde. Wenn der Datenfluss beispielsweise so konfiguriert wurde, dass er stündlich ausgeführt wird, und 48 Stunden lang deaktiviert war, erstellt Experience Platform nach der erneuten Aktivierung dieses Datenflusses 48 Aufstockungsläufe, um die verpassten Intervalle zu verarbeiten.

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich den Arbeitsbereich [!UICONTROL Quellen] verwendet, um den Erfassungszeitplan und die Zuordnungssätze Ihres Datenflusses zu aktualisieren.

Anweisungen zum programmgesteuerten Ausführen dieser Vorgänge mithilfe der [!DNL Flow Service] -API finden Sie im Tutorial zum Aktualisieren von Datenflüssen mithilfe der Flow Service-API [.](../../tutorials/api/update-dataflows.md)
