---
keywords: Experience Platform;home;popular topics; analytics;classifications
description: Erfahren Sie, wie Sie einen Adobe Analytics-Quell-Connector über die Benutzeroberfläche erstellen, um Klassifizierungsdaten in Adobe Experience Platform zu importieren.
solution: Experience Platform
title: Erstellen einer Adobe Analytics Source-Verbindung für Classification-Daten in der Benutzeroberfläche
type: Tutorial
exl-id: d606720d-f1ca-47cc-919b-643a8fc61e07
source-git-commit: fcebef97ba9cc667f80afd55980c5460912a56fb
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 15%

---

# Erstellen einer Adobe Analytics-Quellverbindung für Klassifizierungsdaten in der Benutzeroberfläche

In diesem Tutorial erfahren Sie, wie Sie eine Adobe Analytics Classifications-Datenquellenverbindung in der Benutzeroberfläche erstellen, um Classification-Daten in Adobe Experience Platform zu importieren.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): Experience Platform stellt virtuelle Sandboxes bereit, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen aufteilen, um die Entwicklung und Weiterentwicklung von Programmen für digitale Erlebnisse zu erleichtern.

Der Data Connector von Analytics Classifications erfordert, dass Ihre Daten vor der Verwendung in die neue [!DNL Classifications] -Infrastruktur von Adobe Analytics migriert wurden. Wenden Sie sich zur Bestätigung des Migrationsstatus Ihrer Daten an Ihr Adobe-Account-Team.

## Auswählen Ihrer Classifications

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann in der linken Navigationsleiste **[!UICONTROL Quellen]** aus, um auf den Arbeitsbereich &quot;Quellen&quot;zuzugreifen. Der Bildschirm **[!UICONTROL Katalog]** zeigt verfügbare Quellen zum Erstellen von eingehenden Verbindungen an. Jede Quellkarte enthält eine Option zum Konfigurieren eines neuen Kontos oder zum Hinzufügen von Daten zu einem vorhandenen Konto.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie **[!UICONTROL Adobe Applications]** die Karte **[!UICONTROL Adobe Analytics]** und dann **[!UICONTROL Add data]** aus, um mit den Analytics Classifications Data zu arbeiten.

![](../../../../images/tutorials/create/classifications/catalog.png)

Der Schritt **[!UICONTROL Analytics-Quelle – Daten hinzufügen]** wird angezeigt. Wählen Sie **[!UICONTROL Klassifizierungen]** aus der oberen Kopfzeile aus, um eine Liste mit [!DNL Classifications] Datensätzen anzuzeigen, einschließlich Informationen zu ihrer Dimensions-ID, dem Report Suite-Namen und der Report Suite-ID.

Jede Seite zeigt bis zu zehn verschiedene [!DNL Classifications] Datensätze an, aus denen Sie wählen können. Wählen Sie &quot;**[!UICONTROL Weiter]**&quot;unten auf der Seite aus, um nach weiteren Optionen zu suchen. Das Bedienfeld auf der rechten Seite zeigt die Gesamtzahl der von Ihnen ausgewählten [!DNL Classifications] Datensätze sowie deren Namen an. In diesem Bedienfeld können Sie auch alle [!DNL Classifications] Datensätze entfernen, die Sie versehentlich ausgewählt haben, oder alle Auswahlen mit einer Aktion löschen.

Sie können bis zu 30 verschiedene [!DNL Classifications] Datensätze auswählen, die in [!DNL Platform] aufgenommen werden sollen.

Nachdem Sie Ihre [!DNL Classifications] -Datensätze ausgewählt haben, wählen Sie oben rechts auf der Seite die Option **[!UICONTROL Weiter]** aus.

![](../../../../images/tutorials/create/classifications/add-data.png)

## Überprüfen Sie Ihre Klassifizierungen

Der Schritt **[!UICONTROL Überprüfen]** wird angezeigt, mit dem Sie Ihre ausgewählten [!DNL Classifications] Datensätze überprüfen können, bevor sie erstellt werden. Die Details lassen sich wie folgt kategorisieren:

* **[!UICONTROL Verbindung]**: Zeigt die Quellplattform und den Status der Verbindung an.
* **[!UICONTROL Datentyp]**: Zeigt die Anzahl der ausgewählten [!DNL Classifications] an.
* **[!UICONTROL Planung]**: Zeigt die Häufigkeit der Synchronisation für [!DNL Classifications] -Daten an.

Nachdem Sie Ihren Datenfluss überprüft haben, klicken Sie auf **[!UICONTROL Beenden]** und lassen Sie die Erstellung des Datenflusses etwas Zeit zu.

![](../../../../images/tutorials/create/classifications/review.png)

## Überwachen des Datenflusses zu Classifications

Nachdem Ihr Datenfluss erstellt wurde, können Sie die Daten überwachen, die über ihn aufgenommen werden. Wählen Sie im Bildschirm **[!UICONTROL Katalog]** die Option **[!UICONTROL Datenflüsse]** aus, um eine Liste der eingerichteten Flüsse anzuzeigen, die mit Ihrem [!DNL Classifications]-Konto verknüpft sind.

![](../../../../images/tutorials/create/classifications/dataflows.png)

Der Bildschirm **[!UICONTROL Datenflüsse]** wird angezeigt. Auf dieser Seite finden Sie eine Liste von Datenflüssen, einschließlich Informationen zu ihrem Namen, Quelldaten und Datenfluss-Ausführungsstatus. Rechts befindet sich das Bedienfeld &quot;**[!UICONTROL Eigenschaften]**&quot;, das Metadaten zu Ihrem [!DNL Classifications]-Datenfluss enthält.

Wählen Sie den **[!UICONTROL Ziel-Datensatz]** aus, auf den Sie zugreifen möchten.

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

Auf der Seite **[!UICONTROL Datensatzaktivität]** werden Informationen zum ausgewählten Zieldatensatz angezeigt, einschließlich Details zum Batch-Status, zur Datensatz-ID und zum Schema.

![](../../../../images/tutorials/create/classifications/dataset.png)

## Nächste Schritte

In diesem Tutorial haben Sie einen Data Connector für Analytics Classifications erstellt, der [!DNL Classifications] -Daten in [!DNL Platform] bringt. Weitere Informationen zu [!DNL Analytics] - und [!DNL Classifications] -Daten finden Sie in den folgenden Dokumenten:

* [Übersicht über den Analytics Data Connector](../../../../connectors/adobe-applications/analytics.md)
* [Erstellen einer Analytics-Datenverbindung in der Benutzeroberfläche](./analytics.md)
* [Über Klassifizierungen](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html)
