---
keywords: Experience Platform;Modell planen;Data Science Workspace;beliebte Themen;Bewertung planen;Schulung planen
solution: Experience Platform
title: Planen eines Modells in der Data Science Workspace-Benutzeroberfläche
type: Tutorial
description: Mit Adobe Experience Platform Data Science Workspace können Sie geplante Scoring- und Trainings-Läufe in einem Service für maschinelles Lernen einrichten. Die Automatisierung des Trainings- und Bewertungsvorgangs kann dazu beitragen, die Effizienz eines Service im Laufe der Zeit zu erhalten und zu verbessern, indem Sie über Muster in Ihren Daten auf dem Laufenden bleiben.
exl-id: 51f6f328-7c63-4de1-9184-2ba526bb82e2
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 17%

---

# Planen eines Modells in der Data Science Workspace-Benutzeroberfläche

>[!NOTE]
>
>Data Science Workspace ist nicht mehr erhältlich.
>
>Diese Dokumentation richtet sich an Bestandskunden mit vorherigen Berechtigungen für Data Science Workspace.

Mit Adobe Experience Platform [!DNL Data Science Workspace] können Sie geplante Scoring- und Trainings-Läufe in einem maschinellen Lerndienst einrichten. Die Automatisierung des Trainings- und Bewertungsprozesses kann dazu beitragen, die Effizienz eines Service im Laufe der Zeit zu erhalten und zu verbessern, indem Muster in Ihren Daten beibehalten werden.

Dieses Tutorial führt Sie durch die Schritte, die Sie zum Konfigurieren von Trainings- und Scoring-Zeitplänen für einen vorhandenen Service über die [!UICONTROL Dienstgalerie] ausführen müssen. Es ist in die folgenden Hauptabschnitte unterteilt:

- [Geplantes Scoring konfigurieren](#configure-scheduled-scoring)
- [Geplantes Training konfigurieren](#configure-scheduled-training)

## Erste Schritte

Um dieses Tutorial abzuschließen, benötigen Sie Zugriff auf [!DNL Experience Platform]. Wenn Sie in [!DNL Experience Platform] keinen Zugriff auf eine Organisation haben, wenden Sie sich an Ihren Systemadministrator, bevor Sie fortfahren.

Für dieses Tutorial ist ein bestehender Service erforderlich. Wenn Sie über keinen Service verfügen, mit dem Sie arbeiten können, können Sie einen Service erstellen, indem Sie dem Tutorial zum Veröffentlichen [&#x200B; Modells als Service &#x200B;](./publish-model-service-ui.md).

## Geplantes Scoring konfigurieren {#configure-scheduled-scoring}

Das Modell-Scoring kann als automatisierter Prozess auf geplanter Basis konfiguriert werden. Nachdem ein Service erstellt wurde, können Sie die folgenden Schritte ausführen, um einen Scoring-Zeitplan zu konfigurieren und anzuwenden:

Wählen Sie in Adobe Experience Platform die Registerkarte **[!UICONTROL Services]** in der linken Navigationsspalte aus, um auf die **[!DNL Service Gallery]** zuzugreifen. Suchen Sie den Service, für den Sie einen Scoring-Lauf planen möchten, und wählen Sie **[!UICONTROL Öffnen]**, um die zugehörige **[!UICONTROL Übersicht]** anzuzeigen.

![](../images/models-recipes/schedule/select_service.png)

Auf der Übersichtsseite werden die Scoring-Informationen des Diensts angezeigt. Wählen Sie den **[!UICONTROL Zeitplan aktualisieren]**, um einen Scoring-Zeitplan zu konfigurieren.

![](../images/models-recipes/schedule/update_scoring.png)

Konfigurieren Sie die Häufigkeit, das Anfangsdatum, das Enddatum, den Eingabedatensatz und den Ausgabedatensatz für den Scoring-Zeitplan. Wenn Sie mit den Konfigurationen zufrieden sind, wählen Sie **[!UICONTROL Erstellen]** aus, um den Scoring-Zeitplan für den Service zu aktualisieren.

![](../images/models-recipes/schedule/set_scoring_schedule.png)

Der aktualisierte Scoring-Zeitplan wird auf der Seite „Überblick **[!UICONTROL des]** angezeigt.

![](../images/models-recipes/schedule/scoring_set.png)

## Geplantes Training konfigurieren {#configure-scheduled-training}

Durch das Konfigurieren geplanter Trainings-Läufe für einen Service wird sichergestellt, dass das Modell für maschinelles Lernen auf die neuesten Datenmuster aktualisiert wird. Bei jedem Abschluss eines geplanten Trainings-Laufs wird das resultierende trainierte Modell verwendet, um den Service bis zum nächsten geplanten Trainings-Lauf zu unterstützen.

Nachdem ein Service erstellt wurde, können Sie die folgenden Schritte ausführen, um einen Trainings-Zeitplan zu konfigurieren und anzuwenden:

Wählen Sie in Adobe Experience Platform die Registerkarte **[!UICONTROL Services]** in der linken Navigationsspalte aus, um auf die **[!UICONTROL Service-Galerie]** zuzugreifen. Suchen Sie den Service, für den Sie Trainings-Läufe planen möchten, und wählen Sie **[!UICONTROL Öffnen]** aus, um die zugehörige **[!UICONTROL Übersicht]** anzuzeigen.

![](../images/models-recipes/schedule/select_service.png)

Auf der Seite Übersicht werden die Schulungsinformationen des Service angezeigt. Wählen Sie den **[!UICONTROL Zeitplan aktualisieren]**, um einen Trainings-Zeitplan zu konfigurieren.

![](../images/models-recipes/schedule/update_training.png)

Konfigurieren Sie die Häufigkeit, das Anfangsdatum, das Enddatum und den Eingabedatensatz, die für den Trainings-Zeitplan verwendet werden sollen. Wenn Sie mit den Konfigurationen zufrieden sind, wählen Sie **[!UICONTROL Erstellen]** aus, um den Trainings-Zeitplan für den Service zu aktualisieren.

![](../images/models-recipes/schedule/set_training_schedule.png)

Ihr aktualisierter Trainings-Zeitplan wird auf der Seite „Überblick **[!UICONTROL des]** angezeigt.

![](../images/models-recipes/schedule/training_set.png)

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie erfolgreich automatische Trainings- und Scoring-Läufe für einen Service geplant und den Workflow der Benutzeroberfläche des [!DNL Data Science Workspace] Tutorials abgeschlossen. Wenn Sie dies noch nicht getan haben, sollten Sie [das Tutorial neu starten](./create-retails-sales-dataset.md) und dem API-Workflow folgen, um ein Modell zu erstellen, zu trainieren, zu bewerten und zu veröffentlichen.
