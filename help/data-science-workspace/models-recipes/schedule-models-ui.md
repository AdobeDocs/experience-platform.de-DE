---
keywords: Experience Platform;Modellplanen;Arbeitsbereich für Datenwissenschaften;beliebte Themen;Planen der Punktzahl;Planen der Schulung
solution: Experience Platform
title: Planen eines Modells in der Benutzeroberfläche des Arbeitsbereichs für Datenwissenschaften
topic-legacy: tutorial
type: Tutorial
description: Mit dem Adobe Experience Platform Data Science Workspace können Sie planmäßige Scoring- und Schulungsabläufe auf einem maschinellen Lerndienst einrichten. Die Automatisierung des Trainings- und Bewertungsvorgangs kann dazu beitragen, die Effizienz eines Service im Laufe der Zeit zu erhalten und zu verbessern, indem Sie über Muster in Ihren Daten auf dem Laufenden bleiben.
exl-id: 51f6f328-7c63-4de1-9184-2ba526bb82e2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 20%

---

# Planen eines Modells in der Benutzeroberfläche von Data Science Workspace

Mit Adobe Experience Platform [!DNL Data Science Workspace] können Sie geplante Scoring- und Schulungsläufe auf einem maschinellen Lerndienst einrichten. Die Automatisierung des Schulungs- und Bewertungsvorgangs kann dazu beitragen, die Effizienz eines Dienstes im Laufe der Zeit zu erhalten und zu verbessern, indem Sie die Muster in Ihren Daten beibehalten.

Dieses Lernprogramm führt Sie durch die Schritte zum Konfigurieren von Schulungs- und Bewertungszeitplänen für einen vorhandenen Dienst mithilfe der [!UICONTROL Servicegalerie]. Es ist in die folgenden Hauptabschnitte unterteilt:

- [Geplantes Scoring konfigurieren](#configure-scheduled-scoring)
- [Geplantes Training konfigurieren](#configure-scheduled-training)

## Erste Schritte

Um dieses Tutorial abzuschließen, benötigen Sie Zugriff auf [!DNL Experience Platform]. Wenn Sie keinen Zugriff auf eine IMS-Organisation in [!DNL Experience Platform] haben, wenden Sie sich bitte an Ihren Systemadministrator, bevor Sie fortfahren.

Für dieses Lernprogramm ist ein vorhandener Dienst erforderlich. Wenn Sie über keinen verfügbaren Dienst verfügen, mit dem Sie arbeiten können, können Sie einen erstellen, indem Sie dem Tutorial für [Veröffentlichen eines Modells als Dienst](./publish-model-service-ui.md) folgen.

## Geplantes Scoring konfigurieren {#configure-scheduled-scoring}

Das Modell-Scoring kann als automatisierter Prozess auf geplanter Basis konfiguriert werden. Nachdem ein Dienst erstellt wurde, können Sie die folgenden Schritte ausführen, um einen Bewertungszeitplan zu konfigurieren und anzuwenden:

Wählen Sie in Adobe Experience Platform die Registerkarte **[!UICONTROL Dienste]** in der linken Navigationsspalte aus, um auf das **[!DNL Service Gallery]** zuzugreifen. Suchen Sie den Dienst, für den Sie die Bewertung planen möchten, und wählen Sie **[!UICONTROL Öffnen]**, um die **[!UICONTROL Übersichtsseite]** Ansicht.

![](../images/models-recipes/schedule/select_service.png)

Auf der Übersichtsseite werden die Scoring-Informationen des Diensts angezeigt. Klicken Sie auf den Link **[!UICONTROL Plan aktualisieren]**, um einen Bewertungszeitplan zu konfigurieren.

![](../images/models-recipes/schedule/update_scoring.png)

Konfigurieren Sie die Häufigkeit, das Anfangsdatum, das Enddatum, den Eingabedatensatz und den Ausgabedatensatz für den Scoring-Zeitplan. Wenn Sie mit den Konfigurationen zufrieden sind, wählen Sie **[!UICONTROL Erstellen]**, um den Bewertungszeitplan des Dienstes zu aktualisieren.

![](../images/models-recipes/schedule/set_scoring_schedule.png)

Ihr aktualisierter Bewertungszeitplan wird auf der Seite **[!UICONTROL Übersicht]** des Dienstes angezeigt.

![](../images/models-recipes/schedule/scoring_set.png)

## Geplantes Training konfigurieren {#configure-scheduled-training}

Durch die Konfiguration geplanter Schulungen, die auf einem Dienst ausgeführt werden, wird sichergestellt, dass das Modell für maschinelles Lernen auf die neuesten Datenmuster aktualisiert wird. Bei jedem Abschluss eines geplanten Schulungslaufs wird das resultierende geschulte Modell verwendet, um den Dienst bis zum nächsten geplanten Schulungslauf zu aktivieren.

Nachdem ein Dienst erstellt wurde, können Sie die folgenden Schritte ausführen, um einen Schulungsplan zu konfigurieren und anzuwenden:

Wählen Sie in Adobe Experience Platform in der linken Navigationsspalte die Registerkarte **[!UICONTROL Dienste]**, um auf die **[!UICONTROL Dienstgalerie]** zuzugreifen. Suchen Sie den Dienst, für den Sie Schulungen planen möchten, und wählen Sie **[!UICONTROL Öffnen]**, um dessen **[!UICONTROL Übersichtsseite]** Ansicht.

![](../images/models-recipes/schedule/select_service.png)

Auf der Seite Überblick werden die Schulungsinformationen des Dienstes angezeigt. Klicken Sie auf den Link **[!UICONTROL Plan aktualisieren]**, um einen Schulungsplan zu konfigurieren.

![](../images/models-recipes/schedule/update_training.png)

Konfigurieren Sie die Häufigkeit, das Anfangsdatum, das Enddatum und den Eingabedatensatz, die für den Trainings-Zeitplan verwendet werden sollen. Wenn Sie mit den Konfigurationen zufrieden sind, wählen Sie **[!UICONTROL Erstellen]**, um den Schulungsplan des Dienstes zu aktualisieren.

![](../images/models-recipes/schedule/set_training_schedule.png)

Ihr aktualisierter Schulungsplan wird auf der Seite **[!UICONTROL Übersicht]** des Dienstes angezeigt.

![](../images/models-recipes/schedule/training_set.png)

## Nächste Schritte

Durch Befolgen dieses Lernprogramms haben Sie die automatische Schulung und Auswertung für einen Dienst erfolgreich geplant und den Arbeitsablauf für die Benutzeroberfläche des Lehrgangs [!DNL Data Science Workspace] abgeschlossen. Wenn Sie dies noch nicht getan haben, können Sie [das Tutorial](./create-retails-sales-dataset.md) erneut starten und dem API-Arbeitsablauf folgen, um ein Modell zu erstellen, auszubilden, zu bewerten und zu veröffentlichen.
