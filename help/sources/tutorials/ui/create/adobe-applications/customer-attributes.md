---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erstellen eines Quell-Connectors für Kundenattribute in der Benutzeroberfläche
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# Erstellen eines Quell-Connectors für Kundenattribute in der Benutzeroberfläche

In diesem Lernprogramm wird beschrieben, wie Sie in der Benutzeroberfläche einen Quellanschluss für die Erfassung von Kundenattributdaten in Adobe Experience Platform erstellen können. Weitere Informationen zu Kundenattributen finden Sie im Dokument [Überblick](https://docs.adobe.com/content/help/de-DE/core-services/interface/customer-attributes/attributes.html).

## Erstellen einer Quellverbindung

Melden Sie sich bei <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> an und wählen Sie dann in der linken Navigationsleiste die Option &quot; **Quellen** &quot;, um auf den Quellarbeitsbereich zuzugreifen. Im Anzeigebereich &quot; *Katalog* &quot;werden verfügbare Quellen zum Erstellen von eingehenden Verbindungen angezeigt. Jede Quelle zeigt die Anzahl der vorhandenen Verbindungen an, die mit ihnen verbunden sind. Wählen Sie die Option für **Kundenattribute** und klicken Sie dann auf Quelle **verbinden**. Warten Sie einige Zeit, bis die Verbindung hergestellt ist. Sie werden umgeleitet, wenn eine Verbindung erfolgreich hergestellt wurde.

>[!NOTE] Wenn Sie bereits einen Quell-Connector für Kundenattributdaten eingerichtet haben, wird die Option zum Herstellen einer Verbindung mit dem Profil deaktiviert.

![](../../../../images/tutorials/create/customer-attributes/CA-sources_catalog.png)

Im Bildschirm &quot; *Source-Aktivität* &quot;werden alle zuvor eingerichteten Verbindungen für Kundenattributdaten Liste. Sie können eine neue Verbindung erstellen, indem Sie auf Daten **auswählen** klicken.

>[!NOTE] Es können mehrere eingehende Verbindungen zu einer Quelle hergestellt werden, um verschiedene Daten einzubringen.

![](../../../../images/tutorials/create/customer-attributes/CA-source_activity.png)

Wählen Sie in der Liste der verfügbaren Kundenattributdatasets die Profil-Datensätze aus, die Sie in die Plattform aufnehmen möchten, und klicken Sie auf **Weiter**.

>[!NOTE] Pro Quellenverbindung zu Kundenattributen kann nur ein Datensatz ausgewählt werden.

![](../../../../images/tutorials/create/customer-attributes/CA-select_data.png)

Der Schritt *Überprüfen* wird angezeigt, mit dem Sie Ihre neue eingehende Verbindung überprüfen können, bevor sie erstellt wird. Die Verbindungsdetails werden nach Kategorien gruppiert, darunter:

* *Quelldetails*: Zeigt den Typ der Quellverbindung und die ausgewählten Quelldaten an.
* *Angaben* zur Zielgruppe: Beim Erstellen anderer Quell-Connectors zeigt dieser Container, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, das der Datensatz einhält. Kundenattribute Profil-Daten werden automatisch zugeordnet und in Echtzeit-Kundendaten erfasst.

![](../../../../images/tutorials/create/customer-attributes/CA-review.png)

## Nächste Schritte

Nachdem die Verbindung erstellt wurde, wird automatisch ein Zielgruppe-Schema und ein Dataset erstellt, die die eingehenden Daten enthalten. Nach Abschluss der anfänglichen Erfassung können Kundenattributdaten-Profil-Daten von den nachgeschalteten Plattformdiensten wie dem Echtzeit-Kundendienst und dem Segmentierungsdienst verwendet werden. Weitere Informationen finden Sie in den folgenden Dokumenten:

* [Übersicht über das Echtzeit-Kundenprofil](../../../../../profile/home.md)
* [Übersicht über den Segmentierungsdienst](../../../../../segmentation/home.md)
