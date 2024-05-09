---
keywords: Experience Platform; Modell veröffentlichen; Data Science Workspace; beliebte Themen; Dienst bewerten
solution: Experience Platform
title: Veröffentlichen eines Modells als Dienst in der Benutzeroberfläche von Data Science Workspace
type: Tutorial
description: Mit Adobe Experience Platform Data Science Workspace können Sie Ihr trainiertes und ausgewertetes Modell als Service veröffentlichen, sodass Benutzer in Ihrem Unternehmen Daten bewerten können, ohne eigene Modelle erstellen zu müssen.
exl-id: ebbec1b1-20d3-43b5-82d3-89c79757625a
source-git-commit: d6a4b149b911cd6e7dbbd6c1289fce64be76b506
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 33%

---

# Veröffentlichen eines Modells als Dienst in der Benutzeroberfläche von Data Science Workspace {#publish-a-model-as-a-service}

>[!CONTEXTUALHELP]
>id="platform_intelligentservices_publishmodel"
>title="Veröffentlichen eines Modells als Dienst"
>abstract=""

Mit Adobe Experience Platform Data Science Workspace können Sie Ihr trainiertes und ausgewertetes Modell als Service veröffentlichen, sodass Benutzer in Ihrem Unternehmen Daten bewerten können, ohne eigene Modelle erstellen zu müssen.

## Erste Schritte

Um dieses Tutorial abzuschließen, benötigen Sie Zugriff auf [!DNL Experience Platform]. Wenn Sie keinen Zugriff auf eine Organisation in [!DNL Experience Platform]Wenden Sie sich an Ihren Systemadministrator, bevor Sie fortfahren.

Diese Anleitung setzt ein vorhandenes Modell mit einem erfolgreichen Trainings-Lauf voraus. Wenn Sie über kein veröffentlichungsfähiges Modell verfügen, führen Sie die Anleitung [Modell in der Benutzeroberfläche trainieren und auswerten](./train-evaluate-model-ui.md) aus, bevor Sie fortfahren.

Wenn Sie ein Modell lieber mithilfe von Sensei Machine Learning-APIs veröffentlichen möchten, lesen Sie die [API-Anleitung](./publish-model-service-api.md).

## Modell veröffentlichen {#publish-a-model}

Wählen Sie in Adobe Experience Platform **[!UICONTROL Modelle]** Wählen Sie in der linken Navigationsspalte die Option **[!UICONTROL Durchsuchen]** um alle vorhandenen Modelle aufzulisten. Wählen Sie den Namen des Modells aus, das Sie als Dienst veröffentlichen möchten.

![](../images/models-recipes/publish-model/browse_model.png)

Auswählen **[!UICONTROL Veröffentlichen]** oben rechts auf der Modellübersichtsseite, um einen Prozess zur Diensterstellung zu starten.

![](../images/models-recipes/publish-model/view_training.png)

Geben Sie einen gewünschten Namen für den Dienst ein und geben Sie optional eine Dienstbeschreibung ein, wählen Sie **[!UICONTROL Nächste]** wenn fertig.

![](../images/models-recipes/publish-model/configure_training.png)

Alle erfolgreichen Trainings-Läufe für das Modell werden aufgelistet. Der neue Service übernimmt die Trainings- und Scoring-Konfigurationen aus dem ausgewählten Trainings-Lauf.

![](../images/models-recipes/publish-model/select_training_run.png)

Auswählen **[!UICONTROL Beenden]** , um den Dienst zu erstellen und zur **[!UICONTROL Service Gallery]** , um alle verfügbaren Dienste anzuzeigen, einschließlich des neu erstellten Dienstes.

![](../images/models-recipes/publish-model/service_gallery.png)

## Mit einem Service bewerten {#access-a-service}

Wählen Sie in Adobe Experience Platform die **[!UICONTROL Dienste]** in der linken Navigationsspalte, um auf die **[!UICONTROL Service Gallery]**. Suchen Sie den Dienst, den Sie verwenden möchten, und wählen Sie **[!UICONTROL Öffnen]**.

![](../images/models-recipes/publish-model/open_service.png)

Wählen Sie auf der Dienstübersichtsseite die Option **[!UICONTROL Ergebnis]**.

![](../images/models-recipes/publish-model/score_service.png)

Wählen Sie einen entsprechenden Eingabedatensatz für den Scoring-Lauf aus und wählen Sie dann **[!UICONTROL Nächste]**. Sie werden aufgefordert, denselben Schritt für den Scoring-Datensatz durchzuführen. Nachdem Sie den Eingabe- und Ausgabedatensatz ausgewählt haben, können Sie die Konfigurationen aktualisieren.

![](../images/models-recipes/publish-model/select_datasets.png)

Wenn ein Service erstellt wird, übernimmt er die standardmäßigen Scoring-Konfigurationen. Sie können diese Konfigurationen überprüfen und nach Bedarf anpassen, indem Sie auf die Werte doppelklicken. Wenn Sie mit den Konfigurationen zufrieden sind, wählen Sie **[!UICONTROL Beenden]** , um den Scoring-Lauf zu starten.

![](../images/models-recipes/publish-model/scoring_configs.png)

Auf der Seite **Übersicht** des Services werden Details zum neuen Scoring-Auftrag und zu dessen Fortschritt angezeigt. Sobald der Auftrag abgeschlossen ist, wird die **[!UICONTROL Zuletzt verwendet]** -Kopfzeile innerhalb der **[!UICONTROL Bewertung]** -Container aktualisiert wird.

![](../images/models-recipes/publish-model/pending_scoring.png)

## Nächste Schritte {#next-steps}

In diesem Tutorial haben Sie erfolgreich ein Modell als aufrufbaren Service veröffentlicht und mithilfe des neuen Services Daten über die [!UICONTROL Service Gallery] bewertet. Fahren Sie mit der nächsten Anleitung fort, um zu erfahren, wie Sie [automatisierte Trainings- und Scoring-Läufe für einem Service planen](./schedule-models-ui.md) können.
