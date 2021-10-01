---
keywords: Experience Platform; Modell planen; Data Science Workspace; beliebte Themen; Scoring planen; Schulungen planen
solution: Experience Platform
title: Planen eines Modells in der Benutzeroberfläche von Data Science Workspace
topic-legacy: tutorial
type: Tutorial
description: Mit Adobe Experience Platform Data Science Workspace können Sie geplante Scoring- und Trainings-Läufe auf einem Dienst für maschinelles Lernen einrichten. Die Automatisierung des Trainings- und Bewertungsvorgangs kann dazu beitragen, die Effizienz eines Service im Laufe der Zeit zu erhalten und zu verbessern, indem Sie über Muster in Ihren Daten auf dem Laufenden bleiben.
exl-id: 51f6f328-7c63-4de1-9184-2ba526bb82e2
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 20%

---

# Planen eines Modells in der Benutzeroberfläche von Data Science Workspace

Mit Adobe Experience Platform [!DNL Data Science Workspace] können Sie geplante Scoring- und Trainings-Läufe für einen Dienst für maschinelles Lernen einrichten. Die Automatisierung des Trainings- und Scoring-Prozesses kann dazu beitragen, die Effizienz eines Dienstes im Laufe der Zeit zu erhalten und zu verbessern, indem Sie mit den Mustern in Ihren Daten Schritt halten.

Dieses Tutorial führt Sie durch die Schritte zum Konfigurieren von Trainings- und Scoring-Zeitplänen für einen vorhandenen Dienst über die [!UICONTROL Service Gallery]. Es ist in die folgenden Hauptabschnitte unterteilt:

- [Geplantes Scoring konfigurieren](#configure-scheduled-scoring)
- [Geplantes Training konfigurieren](#configure-scheduled-training)

## Erste Schritte

Um dieses Tutorial abzuschließen, benötigen Sie Zugriff auf [!DNL Experience Platform]. Wenn Sie keinen Zugriff auf eine IMS-Organisation in [!DNL Experience Platform] haben, wenden Sie sich an Ihren Systemadministrator, bevor Sie fortfahren.

Für dieses Tutorial ist ein vorhandener Dienst erforderlich. Wenn Sie über keinen zugänglichen Dienst verfügen, mit dem Sie arbeiten können, können Sie einen erstellen, indem Sie dem Tutorial für [Veröffentlichen eines Modells als Dienst](./publish-model-service-ui.md) folgen.

## Geplantes Scoring konfigurieren {#configure-scheduled-scoring}

Das Modell-Scoring kann als automatisierter Prozess auf geplanter Basis konfiguriert werden. Nachdem ein Dienst erstellt wurde, können Sie die folgenden Schritte ausführen, um einen Scoring-Zeitplan zu konfigurieren und anzuwenden:

Wählen Sie in Adobe Experience Platform in der linken Navigationsspalte die Registerkarte **[!UICONTROL Dienste]** aus, um auf die Registerkarte **[!DNL Service Gallery]** zuzugreifen. Suchen Sie den Dienst, für den Sie die Scoring-Ausführung planen möchten, und wählen Sie **[!UICONTROL Öffnen]** aus, um die zugehörige Seite **[!UICONTROL Übersicht]** anzuzeigen.

![](../images/models-recipes/schedule/select_service.png)

Auf der Übersichtsseite werden die Scoring-Informationen des Diensts angezeigt. Wählen Sie den Link **[!UICONTROL Zeitplan aktualisieren]** aus, um einen Scoring-Zeitplan zu konfigurieren.

![](../images/models-recipes/schedule/update_scoring.png)

Konfigurieren Sie die Häufigkeit, das Anfangsdatum, das Enddatum, den Eingabedatensatz und den Ausgabedatensatz für den Scoring-Zeitplan. Wenn Sie mit den Konfigurationen zufrieden sind, wählen Sie **[!UICONTROL Erstellen]** aus, um den Scoring-Zeitplan des Dienstes zu aktualisieren.

![](../images/models-recipes/schedule/set_scoring_schedule.png)

Ihr aktualisierter Scoring-Zeitplan wird auf der Seite **[!UICONTROL Übersicht]** des Dienstes angezeigt.

![](../images/models-recipes/schedule/scoring_set.png)

## Geplantes Training konfigurieren {#configure-scheduled-training}

Durch die Konfiguration geplanter Trainings-Läufe für einen Dienst wird sichergestellt, dass das Modell für maschinelles Lernen auf die neuesten Datenmuster aktualisiert wird. Bei jedem Abschluss eines geplanten Trainings-Laufs wird das resultierende trainierte Modell verwendet, um den Dienst bis zum nächsten geplanten Trainings-Lauf zu unterstützen.

Nachdem ein Dienst erstellt wurde, können Sie die folgenden Schritte ausführen, um einen Trainings-Zeitplan zu konfigurieren und anzuwenden:

Wählen Sie in Adobe Experience Platform in der linken Navigationsspalte die Registerkarte **[!UICONTROL Dienste]** aus, um auf die **[!UICONTROL Dienstgalerie]** zuzugreifen. Suchen Sie den Dienst, für den Sie Trainings-Läufe planen möchten, und wählen Sie **[!UICONTROL Öffnen]** aus, um die zugehörige Seite **[!UICONTROL Übersicht]** anzuzeigen.

![](../images/models-recipes/schedule/select_service.png)

Auf der Seite Übersicht werden die Trainings-Informationen des Dienstes angezeigt. Wählen Sie den Link **[!UICONTROL Zeitplan aktualisieren]** aus, um einen Trainings-Zeitplan zu konfigurieren.

![](../images/models-recipes/schedule/update_training.png)

Konfigurieren Sie die Häufigkeit, das Anfangsdatum, das Enddatum und den Eingabedatensatz, die für den Trainings-Zeitplan verwendet werden sollen. Wenn Sie mit den Konfigurationen zufrieden sind, wählen Sie **[!UICONTROL Erstellen]** aus, um den Trainings-Zeitplan des Dienstes zu aktualisieren.

![](../images/models-recipes/schedule/set_training_schedule.png)

Ihr aktualisierter Trainings-Zeitplan wird auf der Seite **[!UICONTROL Übersicht]** des Dienstes angezeigt.

![](../images/models-recipes/schedule/training_set.png)

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich automatisierte Trainings- und Scoring-Läufe für einen Dienst geplant und den Arbeitsablauf für die Benutzeroberfläche des Tutorials [!DNL Data Science Workspace] abgeschlossen. Wenn Sie dies noch nicht getan haben, sollten Sie [das Tutorial](./create-retails-sales-dataset.md) neu starten und dem API-Workflow folgen, um ein Modell zu erstellen, zu trainieren, zu bewerten und zu veröffentlichen.
