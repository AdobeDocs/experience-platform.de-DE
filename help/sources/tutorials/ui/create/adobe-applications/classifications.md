---
keywords: Experience Platform;Home;beliebte Themen; Analyse;Klassifizierungen
description: Erfahren Sie, wie Sie einen Adobe Analytics-Quellanschluss in der Benutzeroberfläche erstellen, um Classification-Daten in Adobe Experience Platform zu importieren.
solution: Experience Platform
title: Erstellen einer Adobe Analytics-Quellverbindung für Classification-Daten in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
exl-id: d606720d-f1ca-47cc-919b-643a8fc61e07
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 6%

---

# Erstellen einer Adobe Analytics-Quellverbindung für Classification-Daten in der Benutzeroberfläche

In diesem Lernprogramm werden Schritte zum Erstellen einer Adobe Analytics Classifications-Datenquelle-Verbindung in der Benutzeroberfläche beschrieben, um Classification-Daten in Adobe Experience Platform zu importieren.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

Der Analytics Classifications Data Connector erfordert, dass Ihre Daten vor der Verwendung in die neue Infrastruktur von Adobe Analytics migriert wurden. [!DNL Classifications] Wenden Sie sich zur Bestätigung des Migrationsstatus Ihrer Daten an Ihren Kundenbetreuer für Adobe.

## Wählen Sie Ihre Klassifizierungen aus

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Quellarbeitsbereich zuzugreifen. Der Bildschirm **[!UICONTROL Katalog]** zeigt verfügbare Quellen zum Erstellen von eingehenden Verbindungen an. Jede Quellkarte zeigt eine Option zum Konfigurieren eines neuen Kontos oder zum Hinzufügen von Daten zu einem vorhandenen Konto.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle mit der Suchoption finden.

Wählen Sie unter der Kategorie **[!UICONTROL Adobe applications]** die Karte **[!UICONTROL Adobe Analytics]** aus und wählen Sie **[!UICONTROL Hinzufügen Daten]** aus, um den Beginn mit Analytics-Klassifizierungsdaten zu bearbeiten.

![](../../../../images/tutorials/create/classifications/catalog.png)

Der Schritt **[!UICONTROL Analytics-Quelle Daten hinzufügen]** wird angezeigt. Wählen Sie **[!UICONTROL Klassifizierungen]** aus der oberen Kopfzeile, um eine Liste von [!DNL Classifications]-Datensätzen anzuzeigen, einschließlich Informationen zu ihrer Dimension-ID, dem Report Suite-Namen und der Report Suite-ID.

Jede Seite zeigt bis zu zehn verschiedene [!DNL Classifications]-Datensätze an, aus denen Sie auswählen können. Wählen Sie **[!UICONTROL Weiter]** unten auf der Seite, um nach weiteren Optionen zu suchen. Das Bedienfeld auf der rechten Seite zeigt die Gesamtanzahl der von Ihnen ausgewählten [!DNL Classifications]-Datensätze sowie deren Namen an. In diesem Bedienfeld können Sie auch alle [!DNL Classifications]-Datensätze entfernen, die Sie versehentlich ausgewählt haben, oder alle Auswahlen mit einer Aktion löschen.

Sie können bis zu 30 verschiedene [!DNL Classifications]-Datensätze auswählen, die in [!DNL Platform] geladen werden sollen.

Nachdem Sie die [!DNL Classifications]-Datensätze ausgewählt haben, wählen Sie **[!UICONTROL Weiter]** oben rechts auf der Seite aus.

![](../../../../images/tutorials/create/classifications/add-data.png)

## Überprüfen Sie Ihre Klassifizierungen

Der Schritt **[!UICONTROL Überprüfen]** wird angezeigt, sodass Sie die ausgewählten [!DNL Classifications]-Datensätze überprüfen können, bevor sie erstellt werden. Details werden in den folgenden Kategorien gruppiert:

* **[!UICONTROL Verbindung]**: Zeigt die Quellplattform und den Status der Verbindung an.
* **[!UICONTROL Datentyp]**: Zeigt die Anzahl der ausgewählten Elemente an  [!DNL Classifications].
* **[!UICONTROL Planung]**: Zeigt die Häufigkeit der Synchronisierung von  [!DNL Classifications] Daten.

Klicken Sie nach Überprüfung Ihres Datenflusses auf **[!UICONTROL Fertig stellen]** und lassen Sie etwas Zeit für die Erstellung des Datenflusses zu.

![](../../../../images/tutorials/create/classifications/review.png)

## Überwachen Sie Ihren Classification-Datenfluss.

Nachdem der Datenfluss erstellt wurde, können Sie die Daten überwachen, die über ihn aufgenommen werden. Wählen Sie im Bildschirm **[!UICONTROL Katalog]** die Option **[!UICONTROL Datenflüsse]** aus, um eine Liste der mit Ihrem [!DNL Classifications]-Konto verknüpften Abläufe Ansicht.

![](../../../../images/tutorials/create/classifications/dataflows.png)

Der Bildschirm **[!UICONTROL Datenflüsse]** wird angezeigt. Auf dieser Seite finden Sie eine Liste von Datenflüssen, einschließlich Informationen zu ihrem Namen, ihren Quelldaten und ihrem Datenflug-Ausführungsstatus. Rechts befindet sich das Bedienfeld **[!UICONTROL Eigenschaften]**, das Metadaten zu Ihrem [!DNL Classifications]-Datendurchlauf enthält.

Wählen Sie den Datensatz **[!UICONTROL Zielgruppe]** aus, auf den Sie zugreifen möchten.

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

Auf der Seite **[!UICONTROL Aktivität des Datensatzes]** werden Informationen über den ausgewählten Datensatz der Zielgruppe angezeigt, einschließlich Informationen über den Stapelstatus, die Datensatzkennung und das Schema.

>[!IMPORTANT]
>
>Das Löschen von Datensätzen ist zwar für andere Quell-Connectors möglich, wird aber derzeit nicht für den Analytics Classifications Data Connector unterstützt. Wenn Sie einen Datensatz versehentlich löschen, wenden Sie sich bitte an die Kundenunterstützung der Adobe.

![](../../../../images/tutorials/create/classifications/dataset.png)


## Nächste Schritte

In diesem Lernprogramm haben Sie einen Analytics Classifications Data Connector erstellt, der [!DNL Classifications]-Daten in [!DNL Platform] einfügt. Weitere Informationen zu [!DNL Analytics]- und [!DNL Classifications]-Daten finden Sie in den folgenden Dokumenten:

* [Überblick über Analytics Data Connector](../../../../connectors/adobe-applications/analytics.md)
* [Erstellen einer Analytics-Datenverbindung in der Benutzeroberfläche](./analytics.md)
* [Informationen über Klassifizierungen](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html)
