---
keywords: Experience Platform; Startseite; beliebte Themen; Kundenattribute
solution: Experience Platform
title: Erstellen einer Quellverbindung für Kundenattribute in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie in der Benutzeroberfläche eine Quellverbindung zum Erfassen von Kundenattributprofildaten in Adobe Experience Platform erstellen.
exl-id: 66bdab8f-c00e-4ebe-8b8e-f9e12cf86bbe
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 6%

---

# Erstellen einer Quellverbindung für Kundenattribute in der Benutzeroberfläche

In diesem Tutorial werden Schritte zum Erstellen einer Quellverbindung in der Benutzeroberfläche zum Erfassen von Kundenattribut-Profildaten in Adobe Experience Platform beschrieben. Weitere Informationen zu Kundenattributen finden Sie unter [Übersicht über Kundenattribute](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html?lang=de).

>[!IMPORTANT]
>
>Die Funktionen zum Deaktivieren, Aktivieren und Löschen von Datenflüssen werden derzeit für die Kundenattributquelle nicht unterstützt.

## Quellverbindung erstellen

Wählen Sie in der Platform-Benutzeroberfläche **[!UICONTROL Quellen]** aus dem linken Navigationsbereich aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] enthält eine Vielzahl von Quellen, mit denen Sie eine Verbindung herstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle über die Suchleiste finden.

Wählen Sie unter der Kategorie [!UICONTROL Adobe Applications] die Option **[!UICONTROL Kundenattribute]** und klicken Sie dann auf **[!UICONTROL Daten hinzufügen]**.

>[!NOTE]
>
>Wenn Sie bereits eine Quellverbindung für Kundenattribut-Profildaten hergestellt haben, ist die Option zur Verbindung mit der Quelle deaktiviert.

![](../../../../images/tutorials/create/customer-attributes/catalog.png)

Der Bildschirm [!UICONTROL Daten hinzufügen] listet alle verfügbaren Datenquellen für Kundenattribute auf. Um eine neue Verbindung zu erstellen, wählen Sie eine Datenquelle aus der Liste aus und klicken Sie dann auf **[!UICONTROL Weiter]**.

>[!NOTE]
>
>Pro Quellverbindung mit Kundenattributen kann nur ein Datensatz ausgewählt werden.

![](../../../../images/tutorials/create/customer-attributes/add-data.png)

Der Schritt [!UICONTROL Datenfluss-Detail] wird angezeigt, mit dem Sie einen Namen eingeben und eine kurze Beschreibung für Ihren neuen Datenfluss angeben können.

Während dieses Prozesses können Sie auch [!UICONTROL Partielle Erfassung] und [!UICONTROL Fehlerdiagnose] aktivieren. [!UICONTROL Die partielle ] Erfassung bietet die Möglichkeit, Daten mit Fehlern bis zu einem bestimmten Schwellenwert zu erfassen, den Sie einstellen können, während die  [!UICONTROL Fehlerdiagnose Details zu allen falschen Daten ] anzeigt, die separat stapelt werden. Weitere Informationen finden Sie unter [Übersicht über die partielle Batch-Erfassung](../../../../../ingestion/batch-ingestion/partial.md).

![](../../../../images/tutorials/create/customer-attributes/dataflow-detail.png)

Der Schritt [!UICONTROL Überprüfen] wird angezeigt, mit dem Sie Ihren neuen Datenfluss überprüfen können, bevor er erstellt wird. Details werden in die folgenden Kategorien eingeteilt:

* **[!UICONTROL Verbindung]**: Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quelldatei und die Anzahl der Spalten in dieser Quelldatei an.
* **[!UICONTROL Zuweisen von Datensatz- und Zuordnungsfeldern]**: Zeigt, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, dem der Datensatz entspricht.

![](../../../../images/tutorials/create/customer-attributes/review.png)

## Nächste Schritte

Nachdem die Verbindung erstellt wurde, werden automatisch ein Zielgruppenschema und ein Datensatz erstellt, die die eingehenden Daten enthalten. Nach Abschluss der ersten Aufnahme können Kundenattributprofildaten von nachgelagerten Platform-Diensten wie [!DNL Real-time Customer Profile] und [!DNL Segmentation Service] verwendet werden. Weitere Informationen finden Sie in den folgenden Dokumenten:

* [[!DNL Real-time Customer Profile] Übersicht](../../../../../profile/home.md)
* [[!DNL Segmentation Service] Übersicht](../../../../../segmentation/home.md)
