---
title: Erstellen dynamischer Datenspeicherkonfigurationen
description: Erfahren Sie, wie Sie dynamische Datastream-Konfigurationen erstellen, um Ihre Daten basierend auf Regeln an verschiedene Experience Cloud-Dienste weiterzuleiten.
hide: true
hidefromtoc: true
badge: label="Beta" type="Informative"
source-git-commit: 615318744c233930fb9bc20e55ff42c3a396e651
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 1%

---


# Erstellen dynamischer Datenspeicherkonfigurationen

>[!AVAILABILITY]
>
>* Die Option zum Definieren dynamischer Datenspeicherkonfigurationen befindet sich derzeit in Beta und steht nur einer begrenzten Anzahl von Kunden zur Verfügung. Wenden Sie sich an Ihren Adobe-Support-Mitarbeiter, um Zugriff auf diese Funktion zu erhalten. Dokumentation und Funktionalitäten können sich ändern.

Standardmäßig sendet das Experience Platform-Edge Network alle Ereignisse, die einen Datastream erreichen, an alle Experience Cloud [services](configure.md#add-services), die Sie für Ihre Datenspeicher aktiviert haben. Dieser Workflow ist je nach Anwendungsfall möglicherweise nicht immer der ideale Arbeitsablauf für Sie.

Dynamische Datastream-Konfigurationen lösen diese Bedenken durch benutzerkonfigurierbare Regelsätze aus, die Sie für jeden für Ihren Datastream aktivierten Dienst definieren, die bestimmen, welche Experience Cloud-Lösung die einzelnen Datentypen empfangen soll.

## Voraussetzungen {#prerequisites}

Um eine dynamische Konfiguration für Ihren Datastream zu erstellen, müssen Sie zwei Bedingungen erfüllen:

* Sie müssen *mindestens* einen Datenspeicher erstellt haben, mit dem Sie arbeiten können. Detaillierte Informationen finden Sie in der Dokumentation zum Erstellen eines Datastreams ](configure.md) .[
* Sie müssen über *mindestens* einen Experience Cloud-Dienst verfügen, der Ihrem Datastream hinzugefügt wird. Detaillierte Informationen finden Sie in der Dokumentation zum Hinzufügen von [Diensten](configure.md#add-services) zu einem Datenspeicher.

Nachdem Sie einen Datastream erstellt und ihm einen Experience Cloud-Dienst hinzugefügt haben, können Sie [eine dynamische Konfiguration erstellen](#create-dynamic-configuration).

## Dynamische Datenspeicherkonfiguration erstellen {#create-dynamic-configuration}

Nachdem Sie [einen Datastream](configure.md) erstellt und [einen Dienst](configure.md#add-services) hinzugefügt haben, führen Sie die folgenden Schritte aus, um dem Dienst eine dynamische Konfiguration hinzuzufügen.

1. Gehen Sie zur Seite **[!UICONTROL Datenerfassung]** > **[!UICONTROL Datenspeicher]** und wählen Sie den von Ihnen erstellten Datastream aus.

   ![Bild der Benutzeroberfläche von Datastreams, das die Liste der Datenspeicher anzeigt.](assets/configure-dynamic-datastream/select-datastream.png)

1. Wählen Sie die Option **[!UICONTROL Bearbeiten]** für den Dienst aus, für den Sie eine dynamische Konfiguration definieren möchten.

   ![Bild der Benutzeroberfläche von Datastreams, das die zu einem Datastream hinzugefügten Dienste anzeigt.](assets/configure-dynamic-datastream/select-service.png)

1. Wählen Sie auf der Seite **[!UICONTROL Konfigurieren]** die Option **[!UICONTROL Dynamische Konfiguration speichern und bearbeiten]** aus.

   ![Bild der Benutzeroberfläche von datastreams, das die Seite zur Konfiguration des Datastreams anzeigt.](assets/configure-dynamic-datastream/save-and-edit.png)

1. Wählen Sie **[!UICONTROL Dynamische Konfiguration hinzufügen]** aus.

   ![Bild der Benutzeroberfläche von Datastraams, das die dynamische Konfiguration der Meldung &quot;Keine Regel hinzugefügt&quot; anzeigt.](assets/configure-dynamic-datastream/add-dynamic-config.png)

1. Ziehen Sie die Elemente, mit denen Sie Ihre Regel erstellen möchten, aus dem Bedienfeld **[!UICONTROL Ressourcen]** in den rechten Bereich des Fensters. Sie können mehrere Ressourcen kombinieren, um komplexe Regeln zu erstellen.

   Verwenden Sie die Optionen der einzelnen Ressourcen, z. B. **[!UICONTROL gleich]**, **[!UICONTROL nicht gleich]**, **[!UICONTROL vorhanden]** und mehr, um Ihre Regeln anzupassen.

   ![Bild der Benutzeroberfläche von Datastraams mit der dynamischen Konfigurationsregel.](assets/configure-dynamic-datastream/drag-resources.png)

1. Schalten Sie im Abschnitt **[!UICONTROL Konfiguration]** die Dienste, die Sie für jede Regel aktivieren oder deaktivieren möchten, je nachdem, ob die Daten an jeden Dienst gesendet werden sollen. Wenn Sie den Umschalter deaktivieren, ist das Service-Routing deaktiviert und *keine Daten* werden an den Upstream-Dienst gesendet.

   ![Bild der Benutzeroberfläche von Datastraams mit der dynamischen Konfigurationsregel.](assets/configure-dynamic-datastream/enable-service.png)

1. Wenn Sie die Konfiguration der Regeln abgeschlossen haben, wählen Sie **[!UICONTROL Speichern]** aus.

## Überlegungen zur Regelpriorität {#considerations}

Sie können für jede dynamische Datastream-Konfiguration mehrere Regeln definieren. Wenn Ihre Daten jedoch mit den Bedingungen mehrerer Regeln übereinstimmen, wird nur die erste übereinstimmende Regel in der Liste berücksichtigt und alle anderen Übereinstimmungsregeln werden ignoriert.

Beachten Sie zum Erzielen des gewünschten Daten-Routing-Verhaltens die Reihenfolge, in der Sie die Regeln anordnen.

Um die Regelreihenfolge zu konfigurieren, können Sie die Regelfenster in die gewünschte Reihenfolge ziehen.

![GIF, die zeigt, wie die Reihenfolge der Regeln durch Ziehen und Ablegen geändert werden kann.](assets/configure-dynamic-datastream/move-rules.gif)