---
keywords: Experience Platform;home;popular topics; analytics; classifications
description: In diesem Lernprogramm werden Schritte zum Erstellen eines Adobe Analytics Classifications Data Connectors in der Benutzeroberfläche beschrieben, um Classification-Daten in Adobe Experience Platform zu importieren.
solution: Experience Platform
title: Adobe Analytics Classifications Data Connector in der Benutzeroberfläche erstellen
topic: overview
translation-type: tm+mt
source-git-commit: abb15e3daac4aebd46012822c790b056d0b3d2c1
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 5%

---


# Adobe Analytics Classifications Data Connector in der Benutzeroberfläche erstellen

In diesem Lernprogramm werden Schritte zum Erstellen eines Adobe Analytics Classifications Data Connectors in der Benutzeroberfläche beschrieben, um Classification-Daten in Adobe Experience Platform zu importieren.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM) System]](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
* [[!DNL Echtzeit-Profil]](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxen, die eine einzelne Plattforminstanz in separate virtuelle Umgebung aufteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

## Wählen Sie Ihre Klassifizierungen aus

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann in der linken Navigationsleiste die Option &quot; **[!UICONTROL Quellen]** &quot;, um auf den Quellarbeitsbereich zuzugreifen. Im Anzeigebereich &quot; **[!UICONTROL Katalog]** &quot;werden verfügbare Quellen zum Erstellen von eingehenden Verbindungen angezeigt. Jede Quellkarte zeigt eine Option zum Konfigurieren eines neuen Kontos oder zum Hinzufügen von Daten zu einem vorhandenen Konto.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle mit der Suchoption finden.

Wählen Sie unter der Kategorie **[!UICONTROL Adoben-Anwendungen]** die **[!UICONTROL Adobe Analytics]** -Karte und wählen Sie dann **[!UICONTROL Hinzufügen Daten]** aus, die Beginn mit Analytics-Klassifizierungsdaten verwendensollen.

![](../../../../images/tutorials/create/classifications/catalog.png)

Der Schritt zum Hinzufügen von Daten **[!UICONTROL zur]** Analytics-Quelle wird angezeigt. Wählen Sie **[!UICONTROL Klassifizierungen]** aus der oberen Kopfzeile, um eine Liste der [!DNL Classifications] Datensätze anzuzeigen, einschließlich Informationen zu ihrer **[!UICONTROL Dimensionen-ID]**, ihrem **[!UICONTROL Report Suite-Namen]** und ihrer **[!UICONTROL Report Suite-ID]**.

Jede Seite zeigt bis zu zehn verschiedene [!DNL Classifications] Datensätze an, aus denen Sie auswählen können. Wählen Sie **[!UICONTROL Weiter]** unten auf der Seite, um nach weiteren Optionen zu suchen. Das Bedienfeld auf der rechten Seite zeigt die Gesamtanzahl der ausgewählten [!DNL Classifications] Datensätze sowie deren Namen an. In diesem Bedienfeld können Sie außerdem alle [!DNL Classifications] Datensätze entfernen, die Sie versehentlich ausgewählt haben, oder alle Auswahlen mit einer Aktion löschen.

Sie können bis zu 30 verschiedene [!DNL Classifications] Datensätze auswählen, die Sie einsetzen möchten [!DNL Platform].

Nachdem Sie die [!DNL Classifications] Datensätze ausgewählt haben, wählen Sie oben rechts auf der Seite die Option **[!UICONTROL Weiter]** .

![](../../../../images/tutorials/create/classifications/add-data.png)

## Überprüfen Sie Ihre Klassifizierungen

Der **[!UICONTROL Schritt zum Überprüfen]** wird angezeigt, mit dem Sie die ausgewählten [!DNL Classifications] Datensätze überprüfen können, bevor sie erstellt werden. Details werden in den folgenden Kategorien gruppiert:

* **[!UICONTROL Verbindung]**: Zeigt die Quellplattform und den Status der Verbindung an.
* **[!UICONTROL Datentyp]**: Zeigt die Anzahl der ausgewählten Elemente an [!DNL Classifications].
* **[!UICONTROL Planung]**: Zeigt die Häufigkeit der Synchronisierung von [!DNL Classifications] Daten.

Klicken Sie nach Überprüfung des Datenflusses auf **[!UICONTROL Fertig stellen]** und lassen Sie die Erstellung des Datenflusses etwas Zeit.

![](../../../../images/tutorials/create/classifications/review.png)

## Überwachen und Löschen Ihrer Classification-Daten

Nachdem der Datenfluss erstellt wurde, können Sie die Daten überwachen, die über ihn aufgenommen werden. Wählen Sie im Bildschirm &quot; **[!UICONTROL Katalog]** &quot;die Option &quot; **[!UICONTROL Datenflüsse]** &quot;, um eine Liste der mit Ihrem [!DNL Classifications] Konto verknüpften Abläufe Ansicht.

![](../../../../images/tutorials/create/classifications/dataflows.png)

Der Bildschirm &quot; **[!UICONTROL Datenflüsse]** &quot;wird angezeigt. Auf dieser Seite finden Sie eine Liste von Datenflüssen, einschließlich Informationen zu ihrem Namen, ihren Quelldaten und ihrem Datenflug-Ausführungsstatus. Auf der rechten Seite befindet sich das Bedienfeld &quot; **[!UICONTROL Eigenschaften]** &quot;, das Metadaten zu Ihrem [!DNL Classifications] Datenflug enthält.

Wählen Sie den **[!UICONTROL Zielgruppe-Datensatz]** aus, auf den Sie zugreifen möchten.

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

Auf der Seite &quot; **[!UICONTROL Datensatzdataset-Aktivität]** &quot;werden Informationen über den ausgewählten Dataset angezeigt, einschließlich Informationen zum Stapelstatus, zur Dataset-ID und zum Schema. Wählen Sie **[!UICONTROL Zu löschenden Datensatz]** löschen.

![](../../../../images/tutorials/create/classifications/batch-screen.png)

Es wird ein Dialogfeld angezeigt, das den Löschvorgang bestätigt. Wählen Sie **[!UICONTROL Löschen]** , um den Vorgang abzuschließen.

![](../../../../images/tutorials/create/classifications/delete-confirm.png)

## Nächste Schritte

In diesem Lernprogramm haben Sie einen Analytics Classifications Data Connector erstellt, der [!DNL Classifications] Daten einbezieht [!DNL Platform]. See the following documents for more information on [!DNL Analytics] and [!DNL Classifications] data:

* [Überblick über Analytics Data Connector](../../../../connectors/adobe-applications/analytics.md)
* [Erstellen eines Analytics-Data Connectors in der Benutzeroberfläche](./analytics.md)
* [Informationen über Klassifizierungen](https://docs.adobe.com/content/help/de-DE/analytics/components/classifications/c-classifications.html#)