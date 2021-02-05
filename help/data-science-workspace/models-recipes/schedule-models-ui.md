---
keywords: Experience Platform;Modellplanen;Arbeitsbereich für Datenwissenschaften;beliebte Themen;Planen der Punktzahl;Planen der Schulung
solution: Experience Platform
title: Planen eines Modells in der Benutzeroberfläche des Arbeitsbereichs für Datenwissenschaften
topic: tutorial
type: Tutorial
description: Mit dem Adobe Experience Platform Data Science Workspace können Sie planmäßige Scoring- und Schulungsabläufe auf einem maschinellen Lerndienst einrichten. Die Automatisierung des Trainings- und Bewertungsvorgangs kann dazu beitragen, die Effizienz eines Service im Laufe der Zeit zu erhalten und zu verbessern, indem Sie über Muster in Ihren Daten auf dem Laufenden bleiben.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 79%

---


# Planen eines Modells in der Benutzeroberfläche von Data Science Workspace

Mit Adobe Experience Platform [!DNL Data Science Workspace] können Sie geplante Scoring- und Schulungsläufe auf einem maschinellen Lerndienst einrichten. Die Automatisierung des Trainings- und Bewertungsvorgangs kann dazu beitragen, die Effizienz eines Service im Laufe der Zeit zu erhalten und zu verbessern, indem Sie über Muster in Ihren Daten auf dem Laufenden bleiben.

Dieses Tutorial führt Sie durch die Schritte, die Sie zum Konfigurieren von Trainings- und Scoring-Zeitplänen für einen vorhandenen Dienst über die [!UICONTROL Dienstgalerie] ausführen müssen. Es ist in die folgenden Hauptabschnitte unterteilt:

- [Geplantes Scoring konfigurieren](#configure-scheduled-scoring)
- [Geplantes Training konfigurieren](#configure-scheduled-training)

## Erste Schritte

Um dieses Tutorial abzuschließen, benötigen Sie Zugriff auf [!DNL Experience Platform]. Wenn Sie keinen Zugriff auf eine IMS-Organisation in [!DNL Experience Platform] haben, wenden Sie sich bitte an Ihren Systemadministrator, bevor Sie fortfahren.

Für dieses Tutorial ist ein bestehender Dienst erforderlich. Wenn Sie über keinen Dienst verfügen, mit dem Sie arbeiten können, können Sie einen Dienst erstellen, indem Sie dem Tutorial [Ihr Modell als Dienst in der Benutzeroberfläche veröffentlichen](./publish-model-service-ui.md) folgen.

## Geplantes Scoring konfigurieren {#configure-scheduled-scoring}

Das Modell-Scoring kann als automatisierter Prozess auf geplanter Basis konfiguriert werden. Nach der Erstellung eines Diensts können Sie die folgenden Schritte ausführen, um einen Scoring-Zeitplan zu konfigurieren und anzuwenden:

1. Klicken Sie in Adobe Experience Platform in der linken Navigationsspalte auf die Registerkarte **[!UICONTROL Services]**, um auf die **[!DNL Service Gallery]** zuzugreifen. Suchen Sie den Dienst, für den Sie einen Scoring-Lauf planen möchten, und klicken Sie auf **[!UICONTROL Öffnen]**, um die zugehörige **Übersichtsseite** anzuzeigen.
   ![](../images/models-recipes/schedule/click_to_open.png)

2. Auf der Übersichtsseite werden die Scoring-Informationen des Diensts angezeigt. Klicken Sie auf den Link **[!UICONTROL Zeitplan aktualisieren]**, um einen Scoring-Zeitplan zu konfigurieren.
   ![](../images/models-recipes/schedule/service_overview_score.png)

3. Konfigurieren Sie die Häufigkeit, das Anfangsdatum, das Enddatum, den Eingabedatensatz und den Ausgabedatensatz für den Scoring-Zeitplan. Wenn Sie mit den Einstellungen zufrieden sind, klicken Sie auf **[!UICONTROL Erstellen]**, um den Scoring-Zeitplan für den Dienst zu aktualisieren.
   ![](../images/models-recipes/schedule/14_configure_scoring_schedule.png)

4. Ihr aktualisierter Scoring-Zeitplan wird auf der **Übersichtsseite** des Diensts angezeigt.
   ![](../images/models-recipes/schedule/service_with_scoring_schedule.png)


## Geplantes Training konfigurieren  {#configure-scheduled-training}

Durch die Konfiguration geplanter Trainings-Läufe für einen Dienst können Sie sicherstellen, dass das Modell für maschinelles Lernen auf die neuesten Datenmuster aktualisiert wird. Bei jedem Abschluss eines geplanten Trainings-Laufs wird das resultierende trainierte Modell verwendet, um den Dienst bis zum nächsten geplanten Trainings-Lauf zu unterstützen.

Nach der Erstellung eines Diensts können Sie folgende Schritte ausführen, um einen Trainings-Zeitplan zu konfigurieren und anzuwenden:

1. Klicken Sie in Adobe Experience Platform in der linken Navigationsspalte auf die Registerkarte **[!UICONTROL Dienste]**, um die **[!UICONTROL Dienstgalerie]** aufzurufen. Suchen Sie den Dienst, für den Sie Trainings-Läufe planen möchten, und klicken Sie auf **[!UICONTROL Öffnen]**, um die zugehörige **Übersichtsseite** anzuzeigen.
   ![](../images/models-recipes/schedule/click_to_open.png)

2. Auf der Übersichtsseite werden die Trainings-Informationen des Diensts angezeigt. Klicken Sie auf den Link **[!UICONTROL Zeitplan aktualisieren]**, um einen Trainings-Zeitplan zu konfigurieren.
   ![](../images/models-recipes/schedule/service_overview_train.png)

3. Konfigurieren Sie die Häufigkeit, das Anfangsdatum, das Enddatum und den Eingabedatensatz, die für den Trainings-Zeitplan verwendet werden sollen. Wenn Sie mit den Konfigurationen zufrieden sind, klicken Sie auf **[!UICONTROL Erstellen]**, um den Trainings-Zeitplan für den Dienst zu aktualisieren.
   ![](../images/models-recipes/schedule/12_configure_training_schedule.png)

4. Ihr aktualisierter Trainings-Zeitplan wird auf der **Übersichtsseite** des Diensts angezeigt.
   ![](../images/models-recipes/schedule/service_with_training_schedule.png)

## Nächste Schritte

Durch Befolgen dieses Lernprogramms haben Sie die automatische Schulung und Auswertung für einen Dienst erfolgreich geplant und den Arbeitsablauf für die Benutzeroberfläche des Lehrgangs [!DNL Data Science Workspace] abgeschlossen. Wenn Sie es noch nicht getan haben, können Sie das [Tutorial neu starten](./create-retails-sales-dataset.md) und dem API-Workflow folgen, um ein Modell zu erstellen, zu trainieren, zu bewerten und zu veröffentlichen.
