---
keywords: Experience Platform;Startseite;beliebte Themen;Kundenattribute
solution: Experience Platform
title: Erstellen einer Quellenverbindung für Kundenattribute in der Benutzeroberfläche
topic: Übersicht
type: Tutorial
description: Erfahren Sie, wie Sie eine Quellverbindung in der Benutzeroberfläche erstellen, um Kundenattributdaten-Profil-Daten in Adobe Experience Platform zu erfassen.
translation-type: tm+mt
source-git-commit: 08a3026e969a8739a8b57226c35a6d1d3150006e
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 5%

---


# Erstellen einer Quellverbindung zu Kundenattributen in der Benutzeroberfläche

In diesem Lernprogramm werden die Schritte zum Erstellen einer Quellverbindung in der Benutzeroberfläche zum Sammeln der Daten des Profils &quot;Kundenattribute&quot;in Adobe Experience Platform beschrieben. Weitere Informationen zu Kundenattributen finden Sie unter [Übersicht über Kundenattribute](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html).

>[!IMPORTANT]
>
>Die Funktionen zum Deaktivieren, Aktivieren und Löschen von Datenflüssen werden derzeit nicht für die Kundenattributquelle unterstützt.

## Erstellen einer Quellverbindung

Wählen Sie in der Plattform-Benutzeroberfläche **[!UICONTROL Quellen]** aus der linken Navigation, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie eine Verbindung herstellen können.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle über die Suchleiste finden.

Wählen Sie unter der Kategorie [!UICONTROL Adobe applications] **[!UICONTROL Kundenattribute]** und dann **[!UICONTROL Hinzufügen data]**.

>[!NOTE]
>
>Wenn Sie bereits eine Quellverbindung für die Daten des Profils &quot;Kundenattribute&quot;eingerichtet haben, ist die Option zum Herstellen einer Verbindung mit der Quelle deaktiviert.

![](../../../../images/tutorials/create/customer-attributes/catalog.png)

Der Bildschirm [!UICONTROL Hinzufügen data] Liste alle verfügbaren Datenquellen für Kundenattribute. Um eine neue Verbindung zu erstellen, wählen Sie eine Datenquelle aus der Liste und dann **[!UICONTROL Weiter]**.

>[!NOTE]
>
>Pro Quellenverbindung zu Kundenattributen kann nur ein Datensatz ausgewählt werden.

![](../../../../images/tutorials/create/customer-attributes/add-data.png)

Der Schritt [!UICONTROL Datenfelddetails] wird angezeigt, mit dem Sie einen Namen eingeben und eine kurze Beschreibung für Ihren neuen Datenpfad bereitstellen können.

Während dieses Prozesses können Sie auch die Optionen [!UICONTROL Partielle Erfassung] und [!UICONTROL Fehlerdiagnose] aktivieren. [!UICONTROL Die teilweise ] Erfassung bietet die Möglichkeit, Daten mit Fehlern bis zu einem bestimmten Schwellenwert zu erfassen, den Sie einstellen können, während die  [!UICONTROL Fehlerdiagnose Details zu fehlerhaften Daten ] angibt, die separat gestapelt werden. Weitere Informationen finden Sie unter [Übersicht über die teilweise Stapelverarbeitung](../../../../../ingestion/batch-ingestion/partial.md).

![](../../../../images/tutorials/create/customer-attributes/dataflow-detail.png)

Der Schritt [!UICONTROL Überprüfen] wird angezeigt, mit dem Sie Ihren neuen Datenpfad überprüfen können, bevor er erstellt wird. Details werden in den folgenden Kategorien gruppiert:

* **[!UICONTROL Verbindung]**: Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quelldatei und die Anzahl der Spalten in dieser Quelldatei an.
* **[!UICONTROL Zuweisen von Dataset- und Zuordnungsfeldern]**: Zeigt, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, das der Datensatz einhält.

![](../../../../images/tutorials/create/customer-attributes/review.png)

## Nächste Schritte

Nachdem die Verbindung erstellt wurde, werden automatisch ein Zielgruppenschema und ein Datensatz erstellt, die die eingehenden Daten enthalten. Nach Abschluss der anfänglichen Erfassung können Kundenattributdaten-Profil-Daten von nachgeschalteten Plattformdiensten wie [!DNL Real-time Customer Profile] und [!DNL Segmentation Service] verwendet werden. Weitere Informationen finden Sie in den folgenden Dokumenten:

* [[!DNL Real-time Customer Profile] Übersicht](../../../../../profile/home.md)
* [[!DNL Segmentation Service] Übersicht](../../../../../segmentation/home.md)
