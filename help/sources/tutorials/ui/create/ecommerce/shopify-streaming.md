---
title: Erstellen einer Streaming-Verbindung mit Shopify und eines Datenflusses in der Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Benutzeroberfläche von Platform eine Verbindung mit der Shopify Streaming-Quelle und einen Datenfluss erstellen.
badge: Beta
exl-id: d53f4ab5-8bdc-4647-83d5-ee898abda0f2
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 34%

---

# Erstellen einer Quellverbindung und eines Datenflusses für [!DNL Shopify Streaming] -Daten mithilfe der Benutzeroberfläche

In diesem Tutorial werden Schritte zum Erstellen einer [!DNL Shopify Streaming]-Quellverbindung und eines Datenflusses mithilfe der Platform-Benutzeroberfläche beschrieben.

## Erste Schritte {#getting-started}

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

>[!IMPORTANT]
>
>Für dieses Tutorial müssen Sie die erforderliche Einrichtung für Ihr [!DNL Shopify Streaming]-Konto abgeschlossen haben. Anweisungen zum Einrichten des Kontos finden Sie in der [[!DNL Shopify Streaming] Übersicht](../../../../connectors/ecommerce/shopify-streaming.md) .

## Verbinden Ihres [!DNL Shopify Streaming]-Kontos

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Quellen]** in der linken Navigationsleiste, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie **eCommerce** die Option [!DNL Shopify Streaming] und dann **[!UICONTROL Daten hinzufügen]** aus.

![Der Experience Platform-Quellkatalog](../../../../images/tutorials/create/shopify-streaming/catalog.png)

## Daten auswählen

Der Schritt **[!UICONTROL Daten auswählen]** wird angezeigt und bietet eine Oberfläche zur Auswahl der Daten, die Sie an Platform übermitteln.

* Der linke Teil der Benutzeroberfläche ist ein Browser, mit dem Sie die verfügbaren Datenströme in Ihrem Konto anzeigen können.
* Im rechten Bereich der Benutzeroberfläche können Sie eine Vorschau von bis zu 100 Zeilen mit Daten aus einer JSON-Datei anzeigen.

Wählen Sie **[!UICONTROL Dateien hochladen]** aus, um eine JSON-Datei von Ihrem lokalen System hochzuladen. Alternativ können Sie die JSON-Datei, die Sie hochladen möchten, per Drag-and-Drop in den Bereich [!UICONTROL Dateien ziehen und ablegen] ziehen.

![Der Schritt zum Hinzufügen von Daten des Ursprungs-Workflows.](../../../../images/tutorials/create/shopify-streaming/select-data.png)

Nach dem Hochladen Ihrer Datei wird die Vorschau-Oberfläche aktualisiert, um eine Vorschau des hochgeladenen Schemas anzuzeigen. Über die Vorschau-Oberfläche können Sie den Inhalt und die Struktur einer Datei überprüfen. Sie können auch das Dienstprogramm [!UICONTROL Suchfeld] verwenden, um auf bestimmte Elemente innerhalb Ihres Schemas zuzugreifen.

Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![Der Vorschauschritt des Ursprungs-Workflows.](../../../../images/tutorials/create/shopify-streaming/preview.png)

## Datenflussdetails

Der Schritt **Datenfluss-Detail** wird angezeigt und bietet Ihnen Optionen zur Verwendung eines vorhandenen Datensatzes oder zur Einrichtung eines neuen Datensatzes für Ihren Datenfluss sowie die Möglichkeit, einen Namen und eine Beschreibung für Ihren Datenfluss anzugeben. In diesem Schritt können Sie auch Einstellungen für die Profilerfassung, Fehlerdiagnose, partielle Erfassung und Warnhinweise konfigurieren.

Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![Der Schritt &quot;Datenfluss-Detail&quot;des Ursprungs-Workflows.](../../../../images/tutorials/create/shopify-streaming/dataflow-detail.png)

## Zuordnung

Es erfolgt der Schritt der [!UICONTROL Zuordnung], in dem Ihnen eine Schnittstelle zum Zuordnen der Quellfelder aus Ihrem Quellschema zu den entsprechenden XDM-Zielfeldern im Zielschema bereitgestellt wird.

Platform bietet intelligente Empfehlungen für automatisch zugeordnete Felder, die auf dem ausgewählten Zielschema oder Datensatz basieren. Sie können die Zuordnungsregeln manuell an Ihre Anwendungsfälle anpassen. Je nach Bedarf können Sie wahlweise Felder direkt zuordnen oder mithilfe von Datenvorbereitungsfunktionen Quelldaten transformieren, um berechnete oder anderweitig ermittelte Werte abzuleiten. Umfassende Schritte zur Verwendung der Zuordnungsoberfläche und der berechneten Felder finden Sie im Handbuch [Data Prep UI guide](https://experienceleague.adobe.com/docs/experience-platform/data-prep/ui/mapping.html).

Nachdem die Quelldaten erfolgreich zugeordnet wurden, wählen Sie **[!UICONTROL Weiter]** aus.

![Der Zuordnungsschritt des Ursprungs-Workflows.](../../../../images/tutorials/create/shopify-streaming/mapping.png)

## Überprüfung

Der Schritt **[!UICONTROL Überprüfung]** wird angezeigt, sodass Sie Ihren neuen Datenfluss überprüfen können, bevor er hergestellt wird. Die Details lassen sich wie folgt kategorisieren:

* **[!UICONTROL Verbindung]**: Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quelldatei und die Anzahl der Spalten in dieser Quelldatei an.
* **[!UICONTROL Datensatz- und Zuordnungsfelder zuweisen]**: Zeigt an, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, dem der Datensatz entspricht.

Nachdem Sie Ihren Datenfluss überprüft haben, klicken Sie auf **[!UICONTROL Beenden]** und gewähren Sie etwas Zeit für die Erstellung des Datenflusses.

![Der Überprüfungsschritt des Ursprungs-Workflows.](../../../../images/tutorials/create/shopify-streaming/review.png)

## Abrufen der Streaming-Endpunkt-URL

Mit dem erstellten Streaming-Datenfluss können Sie jetzt Ihre Streaming-Endpunkt-URL abrufen. Dieser Endpunkt wird zum Abonnieren Ihres Webhooks verwendet, sodass Ihre Streaming-Quelle mit Experience Platform kommunizieren kann.

Um Ihren Streaming-Endpunkt abzurufen, rufen Sie die Seite [!UICONTROL Datenfluss-Aktivität] des soeben erstellten Datenflusses auf und kopieren Sie den Endpunkt vom unteren Rand des Bereichs [!UICONTROL Eigenschaften] .

![ Der Streaming-Endpunkt in der Datenflug-Aktivität.](../../../../images/tutorials/create/shopify-streaming/endpoint.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Quellverbindung und einen Datenfluss zu Ihrem [!DNL Shopify Streaming]-Konto eingerichtet. Anweisungen zum Verbinden Ihres [!DNL Shopify Streaming]-Kontos mithilfe der API finden Sie im Tutorial zum Erstellen einer Quellverbindung und eines Datenflusses zum Streamen von  [!DNL Shopify] Daten mithilfe der Flow Service-API](../../../api/create/ecommerce/shopify-streaming.md).[
