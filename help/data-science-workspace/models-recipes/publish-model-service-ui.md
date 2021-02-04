---
keywords: Experience Platform;Veröffentlichen eines Modells;Arbeitsbereich für Datenwissenschaften;beliebte Themen;Erstellen eines Dienstes
solution: Experience Platform
title: Modell als Service veröffentlichen (Benutzeroberfläche)
topic: tutorial
type: Tutorial
description: Mit dem Adobe Experience Platform Data Science Workspace können Sie Ihr trainiertes und bewertetes Modell als Service veröffentlichen, damit Benutzer in Ihrer IMS-Organisation Daten bewerten können, ohne eigene Modelle erstellen zu müssen.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 89%

---


# Modell als Service veröffentlichen (Benutzeroberfläche)

Mit dem Adobe Experience Platform Data Science Workspace können Sie Ihr trainiertes und bewertetes Modell als Service veröffentlichen, damit Benutzer in Ihrer IMS-Organisation Daten bewerten können, ohne eigene Modelle erstellen zu müssen.

## Erste Schritte

Um dieses Tutorial abzuschließen, benötigen Sie Zugriff auf [!DNL Experience Platform]. Wenn Sie keinen Zugriff auf eine IMS-Organisation in [!DNL Experience Platform] haben, wenden Sie sich bitte an Ihren Systemadministrator, bevor Sie fortfahren.

Diese Anleitung setzt ein vorhandenes Modell mit einem erfolgreichen Trainings-Lauf voraus. Wenn Sie über kein veröffentlichungsfähiges Modell verfügen, führen Sie die Anleitung [Modell in der Benutzeroberfläche trainieren und bewerten](./train-evaluate-model-ui.md) aus, bevor Sie fortfahren.

Wenn Sie ein Modell lieber mithilfe von Sensei Machine Learning-APIs veröffentlichen möchten, lesen Sie die [API-Anleitung](./publish-model-service-api.md).

## Modell veröffentlichen {#publish-a-model}

1. Klicken Sie in Adobe Experience Platform in der linken Navigationsspalte auf den Link **[!UICONTROL Modelle]**, um alle vorhandenen Modelle aufzulisten. Suchen Sie nach dem Namen des Modells, das Sie als Service veröffentlichen möchten, und klicken Sie darauf.
   ![](../images/models-recipes/publish-model/1_browse_model.png)
2. Klicken Sie oben rechts auf der Modellübersichtsseite auf **[!UICONTROL Veröffentlichen]**, um einen Prozess zur Service-Erstellung zu starten.
   ![](../images/models-recipes/publish-model/2_view_training_runs.png)
3. Geben Sie den gewünschten Namen für den Service und optional eine Service-Beschreibung ein. Klicken Sie anschließend auf **[!UICONTROL Weiter]**.
   ![](../images/models-recipes/publish-model/3_configure_service.png)
4. Alle erfolgreichen Trainings-Läufe für das Modell werden aufgelistet. Der neue Service übernimmt die Trainings- und Scoring-Konfigurationen aus dem ausgewählten Trainings-Lauf.
   ![](../images/models-recipes/publish-model/4_select_training_run.png)
5. Klicken Sie auf **[!UICONTROL Fertig stellen]**, um den Service zu erstellen und zur **[!UICONTROL Service Gallery]** zur gelangen, wo alle verfügbaren Services einschließlich des neu erstellten Services angezeigt werden.
   ![](../images/models-recipes/publish-model/service_gallery.png)

## Mit einem Service bewerten  {#access-a-service}

1. Klicken Sie in Adobe Experience Platform in der linken Navigationsspalte auf die Registerkarte **[!UICONTROL Services]**, um auf die **[!UICONTROL Service Gallery]** zuzugreifen. Suchen Sie nach dem gewünschten Service und klicken Sie auf **[!UICONTROL Score]**.
   ![](../images/models-recipes/publish-model/click_to_score.png)
2. Wählen Sie einen geeigneten Eingabedatensatz für den Scoring-Lauf und klicken Sie dann auf **[!UICONTROL Weiter]**.
   ![](../images/models-recipes/publish-model/6_scoring_input.png)
3. Wählen Sie einen geeigneten Ausgabedatensatz für die Scoring-Ergebnisse und klicken Sie dann auf **[!UICONTROL Weiter]**.
   ![](../images/models-recipes/publish-model/7_scoring_output.png)
4. Wenn ein Service erstellt wird, übernimmt er die standardmäßigen Scoring-Konfigurationen. Sie können diese Konfigurationen überprüfen und nach Bedarf anpassen, indem Sie auf die Werte doppelklicken. Wenn Sie mit den Konfigurationen zufrieden sind, klicken Sie auf **[!UICONTROL Fertig stellen]**, um den Scoring-Lauf zu starten.
   ![](../images/models-recipes/publish-model/8_scoring_configure.png)
5. Auf der Seite **Übersicht** des Services werden Details zum neuen Scoring-Auftrag und zu dessen Fortschritt angezeigt. Sobald der Auftrag abgeschlossen ist, wird die Kopfzeile **[!UICONTROL Zuletzt verwendet]** im Container **[!UICONTROL Punktzahl]** aktualisiert.
   ![](../images/models-recipes/publish-model/score_pending.png)

## Nächste Schritte {#next-steps}

In diesem Tutorial haben Sie erfolgreich ein Modell als aufrufbaren Service veröffentlicht und mithilfe des neuen Services Daten über die [!UICONTROL Service Gallery] bewertet. Fahren Sie mit der nächsten Anleitung fort, um zu erfahren, wie Sie [automatisierte Trainings- und Scoring-Läufe für einem Service planen](./schedule-models-ui.md) können.
