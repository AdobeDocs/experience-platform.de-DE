---
keywords: Experience Platform;Startseite;beliebte Themen;Datenflüsse aktualisieren;Zeitplan bearbeiten
description: In diesem Tutorial werden die Schritte zum Aktualisieren eines Datenflusszeitplans beschrieben, einschließlich der Erfassungsfrequenz und der Intervallrate, die mithilfe des Arbeitsbereichs "Quellen"vorgenommen werden.
solution: Experience Platform
title: Aktualisieren eines Datenflusses für die Quellverbindung in der Benutzeroberfläche
type: Tutorial
exl-id: 0499a2a3-5a22-47b1-ac0e-76a432bd26c0
source-git-commit: cef5c203acf3318445399669336166e6627ebe66
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 13%

---

# Aktualisieren von Datenflüssen in der Benutzeroberfläche

In diesem Tutorial erfahren Sie, wie Sie einen vorhandenen Datenfluss mithilfe des Arbeitsbereichs &quot;Quellen&quot;aktualisieren, einschließlich Zeitplan und Zuordnung.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

## Aktualisieren von Datenflüssen {#update-dataflows}

>[!CONTEXTUALHELP]
>id="platform_sources_dataflows_daysRemaining"
>title="Datensatzablauf"
>abstract="Diese Spalte gibt die Anzahl der Tage an, die der Zieldatensatz vor seinem automatischen Ablauf vergangen ist.<br>Ein Datenfluss schlägt fehl, wenn der Zieldatensatz abgelaufen ist. Um zu verhindern, dass ein Datenfluss fehlschlägt, stellen Sie sicher, dass ein Zieldatensatz am richtigen Datum abläuft. Informationen zum Aktualisieren der Ablaufdaten finden Sie in der Dokumentation ."

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste die Option **[!UICONTROL Quellen]**, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Auswählen **[!UICONTROL Datenflüsse]** aus der oberen Kopfzeile, um eine Liste der vorhandenen Datenflüsse anzuzeigen.

![Katalog](../../images/tutorials/update-dataflows/catalog.png)

Die [!UICONTROL Datenflüsse] -Seite enthält eine Liste aller vorhandenen Datenflüsse, einschließlich Informationen zu ihrem entsprechenden Zieldatensatz, ihrer Quelle und ihrem Kontonamen.

Um die Liste zu sortieren, wählen Sie das Filtersymbol aus ![filter](../../images/tutorials/update/filter.png) oben links, um das Sortierfeld zu verwenden.

![filter-dataflows](../../images/tutorials/update-dataflows/filter-dataflows.png)

Das Sortierungsfenster bietet eine Liste aller verfügbaren Quellen. Sie können mehrere Quellen aus der Liste auswählen, um auf eine gefilterte Auswahl von Datenflüssen aus verschiedenen Quellen zuzugreifen.

Wählen Sie die Quelle aus, mit der Sie arbeiten möchten, um eine Liste der vorhandenen Datenflüsse anzuzeigen. Nachdem Sie den zu aktualisierenden Datenfluss identifiziert haben, wählen Sie die Auslassungszeichen (`...`) neben dem Namen des Datenflusses.

![edit-source](../../images/tutorials/update-dataflows/edit-source.png)

Es wird ein Dropdown-Menü mit Optionen zum Aktualisieren des ausgewählten Datenflusses angezeigt. Von hier aus können Sie die Zuordnungs- und Erfassungszeitpläne eines Datenflusses aktualisieren. Sie können auch Optionen zum Überprüfen des Datenflusses im Monitoring-Dashboard auswählen, Warnhinweise abonnieren sowie den Datenfluss deaktivieren oder löschen.

Um die Informationen Ihres Datenflusses zu aktualisieren, wählen Sie **[!UICONTROL Aktualisieren des Datenflusses]**.

![update-dataflow](../../images/tutorials/update-dataflows/update-dataflow.png)

### Daten hinzufügen

Der Schritt [!UICONTROL Daten hinzufügen] wird angezeigt. Wählen Sie das geeignete Datenformat aus, um den Inhalt der ausgewählten Daten zu überprüfen, und wählen Sie dann **[!UICONTROL Nächste]** um fortzufahren.

![add-data](../../images/tutorials/update-dataflows/add-data.png)

### Datenflussdetails

Im [!UICONTROL Datenflussdetails] -Seite können Sie einen aktualisierten Namen und eine Beschreibung für Ihren Datenfluss angeben und den Fehlerschwellenwert Ihres Datenflusses neu konfigurieren. Während dieses Schritts können Sie auch Einstellungen für Ihr Warnhinweis-Abonnement konfigurieren oder ändern.

Nachdem Sie die aktualisierten Werte angegeben haben, wählen Sie **[!UICONTROL Nächste]**.

![dataflow-detail](../../images/tutorials/update-dataflows/dataflow-detail.png)

### Zuordnung

>[!NOTE]
>
>Die Bearbeitungszuordnungsfunktion wird für die folgenden Quellen derzeit nicht unterstützt: Adobe Analytics, Adobe Audience Manager, HTTP-API und [!DNL Marketo Engage].

Die [!UICONTROL Zuordnung] -Seite bietet eine Benutzeroberfläche, über die Sie Zuordnungssätze hinzufügen und entfernen können, die mit Ihrem Datenfluss verknüpft sind.

In der Zuordnungsschnittstelle wird der vorhandene Zuordnungssatz Ihres Datenflusses und nicht der neue empfohlene Zuordnungssatz angezeigt. Zuordnungsaktualisierungen werden nur auf in der Zukunft geplante Datenfluss-Läufe angewendet. Für einen Datenfluss, der für die einmalige Erfassung geplant war, können die Zuordnungssätze nicht aktualisiert werden.

Von hier aus können Sie die Zuordnungsschnittstelle verwenden, um die auf Ihren Datenfluss angewendeten Zuordnungssätze zu ändern. Umfassende Schritte zur Verwendung der Zuordnungsschnittstelle finden Sie in der [Benutzerhandbuch zur Datenvorbereitung](../../../data-prep/ui/mapping.md) für weitere Informationen.

![Zuordnung](../../images/tutorials/update-dataflows/mapping.png)

### Planung

Die [!UICONTROL Planung] angezeigt, sodass Sie den Aufnahmezeitplan Ihres Datenflusses aktualisieren und die ausgewählten Quelldaten automatisch mit den aktualisierten Zuordnungen erfassen können.

>[!NOTE]
>
>Sie können einen Datenfluss, der für die einmalige Erfassung geplant war, nicht neu planen.

![new-schedule](../../images/tutorials/update-dataflows/new-schedule.png)

Sie können auch den Aufnahmezeitplan Ihres Datenflusses aktualisieren, indem Sie die Option Inline-Update verwenden, die auf der Datenflussseite bereitgestellt wird.

Wählen Sie auf der Seite &quot;Datenflüsse&quot;die Auslassungspunkte (`...`) neben dem Namen des Datenflusses und wählen Sie dann **[!UICONTROL Zeitplan bearbeiten]** aus dem Dropdown-Menü, das angezeigt wird.

![edit-schedule](../../images/tutorials/update-dataflows/edit-schedule.png)

Die **[!UICONTROL Zeitplan bearbeiten]** bietet Optionen zum Aktualisieren der Erfassungsfrequenz und Intervallrate Ihres Datenflusses. Nachdem Sie die aktualisierten Häufigkeits- und Intervallwerte festgelegt haben, wählen Sie **[!UICONTROL Speichern]**.

![schedule-pop-up](../../images/tutorials/update-dataflows/schedule-pop-up.png)

### Überprüfung

Die **[!UICONTROL Überprüfen]** angezeigt, sodass Sie Ihren Datenfluss überprüfen können, bevor er aktualisiert wird.

Nachdem Sie Ihren Datenfluss überprüft haben, wählen Sie **[!UICONTROL Beenden]** und lassen Sie etwas Zeit für den Datenfluss zu, wobei die neuen Zuordnungssätze erstellt werden.

![überprüfen](../../images/tutorials/update-dataflows/review.png)

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich die [!UICONTROL Quellen] Arbeitsbereich zum Aktualisieren des Erfassungszeitplans und der Zuordnungssätze Ihres Datenflusses.

Anweisungen zum programmgesteuerten Ausführen dieser Vorgänge mit dem [!DNL Flow Service] API, siehe Tutorial zu [Aktualisieren von Datenflüssen mithilfe der Flow Service-API](../../tutorials/api/update-dataflows.md).
