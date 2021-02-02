---
keywords: Experience Platform;Startseite;beliebte Themen;Kundenattribute
solution: Experience Platform
title: Erstellen eines Quell-Connectors für Kundenattribute in der Benutzeroberfläche
topic: overview
type: Tutorial
description: In diesem Lernprogramm wird beschrieben, wie Sie in der Benutzeroberfläche einen Quellanschluss für die Erfassung von Kundenattributdaten in Adobe Experience Platform erstellen können.
translation-type: tm+mt
source-git-commit: 2dbd92efbd992b70f4f750b09e9d2e0626e71315
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 6%

---


# Erstellen eines Quell-Connectors für Kundenattribute in der Benutzeroberfläche

In diesem Lernprogramm wird beschrieben, wie Sie in der Benutzeroberfläche einen Quellanschluss für die Erfassung von Kundenattributdaten in Adobe Experience Platform erstellen können. Weitere Informationen zu Kundenattributen finden Sie im Dokument [overview](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html).

## Erstellen einer Quellverbindung

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Quellarbeitsbereich zuzugreifen. Der Bildschirm **[!UICONTROL Katalog]** zeigt verfügbare Quellen zum Erstellen von eingehenden Verbindungen an. Jede Quelle zeigt die Anzahl der vorhandenen Verbindungen an, die mit ihnen verbunden sind. Wählen Sie die Option für **[!UICONTROL Kundenattribute]** und wählen Sie **[!UICONTROL Hinzufügen Daten]**. Warten Sie einige Zeit, bis die Verbindung hergestellt ist. Sie werden umgeleitet, wenn eine Verbindung erfolgreich hergestellt wurde.

>[!NOTE]
>
>Wenn Sie bereits einen Quell-Connector für Kundenattributdaten eingerichtet haben, wird die Option zum Herstellen einer Verbindung mit dem Profil deaktiviert.

![](../../../../images/tutorials/create/customer-attributes/catalog.png)

Im Bildschirm **Source Aktivität** werden alle zuvor eingerichteten Verbindungen für Kundenattributdaten-Profil-Daten Liste. Sie können eine neue Verbindung erstellen, indem Sie auf **Select data** klicken.

>[!NOTE]
>
>Es können mehrere eingehende Verbindungen zu einer Quelle hergestellt werden, um verschiedene Daten einzubringen.

![](../../../../images/tutorials/create/customer-attributes/source_activity.png)

Wählen Sie in der Liste der verfügbaren Kundenattributdatasets die Profil aus, die Sie in [!DNL Platform] einbinden möchten, und klicken Sie auf **Weiter**.

>[!NOTE]
>
>Pro Quellenverbindung zu Kundenattributen kann nur ein Datensatz ausgewählt werden.

![](../../../../images/tutorials/create/customer-attributes/select_data.png)

Der Schritt **Überprüfen** wird angezeigt, mit dem Sie Ihre neue eingehende Verbindung überprüfen können, bevor sie erstellt wird. Die Verbindungsdetails werden nach Kategorien gruppiert, darunter:

* **Quelldetails**: Zeigt den Typ der Quellverbindung und die ausgewählten Quelldaten an.
* **Angaben** zur Zielgruppe: Beim Erstellen anderer Quell-Connectors zeigt dieser Container, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, das der Datensatz einhält. Kundenattribute Profil-Daten werden automatisch zugeordnet und in Echtzeit-Kundendaten erfasst.

![](../../../../images/tutorials/create/customer-attributes/review.png)

## Nächste Schritte

Nachdem die Verbindung erstellt wurde, werden automatisch ein Zielgruppenschema und ein Datensatz erstellt, die die eingehenden Daten enthalten. Nach Abschluss der ersten Erfassung können Kundenattributdaten-Profil-Daten von nachgeschalteten [!DNL Platform]-Diensten wie [!DNL Real-time Customer Profile] und [!DNL Segmentation Service] verwendet werden. Weitere Informationen finden Sie in den folgenden Dokumenten:

* [[!DNL Real-time Customer Profile] Übersicht](../../../../../profile/home.md)
* [[!DNL Segmentation Service] Übersicht](../../../../../segmentation/home.md)
