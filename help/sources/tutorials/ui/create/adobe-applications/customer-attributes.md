---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Quell-Connectors für Kundenattribute in der Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: 41fe3e5b2a830c3182b46b3e0873b1672a1f1b03
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 10%

---


# Create a customer attributes source connector in the UI

In diesem Lernprogramm wird beschrieben, wie Sie in der Benutzeroberfläche einen Quellanschluss für die Erfassung von Kundenattributdaten in Adobe Experience Platform erstellen können. Weitere Informationen zu Kundenattributen finden Sie im Dokument [Überblick](https://docs.adobe.com/content/help/de-DE/core-services/interface/customer-attributes/attributes.html).

## Erstellen einer Quellverbindung

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann in der linken Navigationsleiste die Option &quot; **[!UICONTROL Quellen]** &quot;, um auf den Quellarbeitsbereich zuzugreifen. Im Anzeigebereich &quot; **[!UICONTROL Katalog]** &quot;werden verfügbare Quellen angezeigt, mit denen eingehende Verbindungen erstellt werden können. Jede Quelle zeigt die Anzahl der vorhandenen Verbindungen an, die mit ihnen verbunden sind. Wählen Sie die Option für **[!UICONTROL Kundenattribute]** und dann **[!UICONTROL Hinzufügen Daten]**. Warten Sie einige Zeit, bis die Verbindung hergestellt ist. Sie werden umgeleitet, wenn eine Verbindung erfolgreich hergestellt wurde.

>[!NOTE]
>
>Wenn Sie bereits einen Quell-Connector für Kundenattributdaten eingerichtet haben, wird die Option zum Herstellen einer Verbindung mit dem Profil deaktiviert.

![](../../../../images/tutorials/create/customer-attributes/catalog.png)

Im Bildschirm &quot; *Source-Aktivität* &quot;werden alle zuvor eingerichteten Verbindungen für Kundenattributdaten Liste. Sie können eine neue Verbindung erstellen, indem Sie auf Daten **auswählen** klicken.

>[!NOTE]
>
>Es können mehrere eingehende Verbindungen zu einer Quelle hergestellt werden, um verschiedene Daten einzubringen.

![](../../../../images/tutorials/create/customer-attributes/source_activity.png)

Wählen Sie in der Liste der verfügbaren Kundenattributdatasets die Profil-Datensätze aus, die Sie in die Plattform aufnehmen möchten, und klicken Sie auf **Weiter**.

>[!NOTE]
>
>Pro Quellenverbindung zu Kundenattributen kann nur ein Datensatz ausgewählt werden.

![](../../../../images/tutorials/create/customer-attributes/select_data.png)

Der Schritt *Überprüfen* wird angezeigt, mit dem Sie Ihre neue eingehende Verbindung überprüfen können, bevor sie erstellt wird. Die Verbindungsdetails werden nach Kategorien gruppiert, darunter:

* *Quelldetails*: Zeigt den Typ der Quellverbindung und die ausgewählten Quelldaten an.
* *Angaben* zur Zielgruppe: Beim Erstellen anderer Quell-Connectors zeigt dieser Container, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, das der Datensatz einhält. Kundenattribute Profil-Daten werden automatisch zugeordnet und in Echtzeit-Kundendaten erfasst.

![](../../../../images/tutorials/create/customer-attributes/review.png)

## Nächste Schritte

Nachdem die Verbindung erstellt wurde, werden automatisch ein Zielgruppenschema und ein Datensatz erstellt, die die eingehenden Daten enthalten. When the initial ingestion completes, customer attributes profile data can be used by downstream Platform services such as Real-time Customer Profile and Segmentation Service. Weitere Informationen finden Sie in den folgenden Dokumenten:

* [Übersicht über das Echtzeit-Kundenprofil](../../../../../profile/home.md)
* [Übersicht über den Segmentierungsdienst](../../../../../segmentation/home.md)
