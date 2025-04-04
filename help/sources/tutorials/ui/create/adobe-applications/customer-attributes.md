---
keywords: Experience Platform;Startseite;beliebte Themen;Kundenattribute
solution: Experience Platform
title: Erstellen einer Source-Verbindung für Kundenattribute über die Benutzeroberfläche
type: Tutorial
description: Erfahren Sie, wie Sie eine Quellverbindung über die Benutzeroberfläche erstellen, um Kundenattributprofildaten in Adobe Experience Platform zu importieren.
exl-id: 66bdab8f-c00e-4ebe-8b8e-f9e12cf86bbe
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 33%

---

# Erstellen einer Quellverbindung für Kundenattribute in der Benutzeroberfläche

In diesem Tutorial werden Schritte zum Erstellen einer -Quellverbindung über die Benutzeroberfläche beschrieben, um Kundenattribut-Profildaten in Adobe Experience Platform zu importieren. Weitere Informationen zu Kundenattributen finden Sie in der [Übersicht Kundenattribute](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html?lang=de).

>[!IMPORTANT]
>
>Die Kundenattributquelle unterstützt derzeit nicht das Aktivieren oder Deaktivieren von Datenflüssen.

## Erstellen einer Quellverbindung

>[!NOTE]
>
>Wenn Sie bereits eine Quellverbindung für Kundenattribut-Profildaten hergestellt haben, ist die Option zum Herstellen einer Verbindung mit der Quelle deaktiviert.

Wählen Sie in der Experience Platform-Benutzeroberfläche **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie eine Verbindung herstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchleiste finden.

Wählen Sie unter der ] [!UICONTROL Adobe-Programme **[!UICONTROL die Option „Kundenattribute]** und dann **[!UICONTROL Daten hinzufügen]** aus.

![Katalog](../../../../images/tutorials/create/customer-attributes/catalog.png)

### Datenquelle für Kundenattribute auswählen

Der Bildschirm [!UICONTROL Daten hinzufügen] listet alle verfügbaren Datenquellen für Kundenattribute auf. Pro Quellverbindung für Kundenattribute kann nur ein Datensatz ausgewählt werden.

>[!NOTE]
>
>Feldergruppen, Schemata und Datensätze werden im Rahmen der Flussbereitstellung vorkonfiguriert erstellt. Sie bleiben unverändert und müssen bei Bedarf manuell gelöscht werden.

Die Schemaentwicklung wird von der Kundenattributquelle nicht unterstützt. Wenn die Schemaeingabe einer Datenquelle für Kundenattribute geändert wird, wird sie mit Experience Platform inkompatibel. Als Problemumgehung können Sie einen vorhandenen Datenfluss mit Kundenattributen zusammen mit dem zugehörigen Datensatz, Schema und der Feldergruppe löschen und dann einen neuen mit dem aktualisierten Schema und der aktualisierten Datenquelle erstellen.

>[!IMPORTANT]
>
>Sie können zwar einen Datenfluss mit Kundenattributen löschen, der entsprechende Datensatz bleibt jedoch auch nach dem Löschen des Datenflusses erhalten. Anweisungen zum manuellen Löschen eines Datensatzes finden [ im Handbuch ](../../../../../catalog/datasets/user-guide.md) Löschen eines Datensatzes .

Um eine neue Verbindung zu erstellen, wählen Sie eine Datenquelle aus der Liste aus und klicken Sie dann auf **[!UICONTROL Weiter]**.

![add-data](../../../../images/tutorials/create/customer-attributes/add-data.png)

### Angeben von Datenflussdetails

Der Schritt [!UICONTROL Datenflussdetails] wird angezeigt, in dem Sie einen Namen und eine kurze Beschreibung für Ihren Datenfluss angeben können. Während dieses Vorgangs können Sie auch Einstellungen für [!UICONTROL Fehlerdiagnose], [!UICONTROL Partielle Aufnahme] und [!UICONTROL Warnhinweise] konfigurieren.

[!UICONTROL Fehlerdiagnose] ermöglicht eine detaillierte Erstellung von Fehlermeldungen für alle fehlerhaften Datensätze, die in Ihrem Datenfluss auftreten, während [!UICONTROL Partielle Aufnahme] die Aufnahme von fehlerhaften Daten bis zu einem gewissen Schwellenwert, den Sie manuell definieren, ermöglicht. Weitere Informationen finden Sie in der [Übersicht zur partiellen Batch-Aufnahme](../../../../../ingestion/batch-ingestion/partial.md).

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status Ihres Datenflusses zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Warnhinweisen zu Quellen über die Benutzeroberfläche](../../alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihren Datenfluss fertig sind, klicken Sie auf **[!UICONTROL Weiter]**.

![dataflow-detail](../../../../images/tutorials/create/customer-attributes/dataflow-detail.png)

### Datenfluss überprüfen

Der Schritt [!UICONTROL Überprüfung] wird angezeigt, sodass Sie Ihren neuen Datenfluss überprüfen können, bevor er hergestellt wird. Die Details lassen sich wie folgt kategorisieren:

* **[!UICONTROL Verbindung]**: Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quelldatei und die Anzahl der Spalten innerhalb dieser Quelldatei an.
* **[!UICONTROL Datensatz- und Zuordnungsfelder zuweisen]**: Zeigt an, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, dem der Datensatz entspricht.

![überprüfen](../../../../images/tutorials/create/customer-attributes/review.png)

## Nächste Schritte

Nachdem die Verbindung erstellt wurde, werden automatisch ein Zielschema und ein Datensatz erstellt, die die eingehenden Daten enthalten. Wenn die anfängliche Aufnahme abgeschlossen ist, können Kundenattributprofildaten von nachgelagerten Experience Platform-Services wie [!DNL Real-Time Customer Profile] und [!DNL Segmentation Service] verwendet werden. Weiterführende Informationen finden Sie in folgenden Dokumenten:

* [[!DNL Real-Time Customer Profile] – Übersicht](../../../../../profile/home.md)
* [[!DNL Segmentation Service] – Übersicht](../../../../../segmentation/home.md)
