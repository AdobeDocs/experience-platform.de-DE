---
title: Erstellen einer Streaming-Verbindung mit Shopify und eines Datenflusses in der Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Benutzeroberfläche von Platform eine Verbindung mit der Shopify Streaming-Quelle und einen Datenfluss erstellen.
badge: „Beta“
hidefromtoc: y
hide: y
source-git-commit: 279d8e307c8ca5a799a47c6f903b9a082d9cf034
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 35%

---

# Erstellen Sie eine Quellverbindung und einen Datenfluss für [!DNL Shopify Streaming] Daten über die Benutzeroberfläche

In diesem Tutorial werden Schritte zum Erstellen eines [!DNL Shopify Streaming] Quellverbindung und Datenfluss über die Platform-Benutzeroberfläche.

## Erste Schritte {#getting-started}

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemas vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

>[!IMPORTANT]
>
>Für dieses Tutorial müssen Sie die erforderliche Einrichtung für Ihre [!DNL Shopify Streaming] -Konto. Anweisungen zum Einrichten des Kontos finden Sie in der [[!DNL Shopify Streaming] Übersicht](../../../../connectors/ecommerce/shopify-streaming.md).

## Verbinden Ihres [!DNL Shopify Streaming]-Kontos

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Quellen]** in der linken Navigationsleiste, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Unter dem **eCommerce** category, select [!DNL Shopify Streaming]und wählen Sie **[!UICONTROL Daten hinzufügen]**.

![Der Experience Platform Sources-Katalog](../../../../images/tutorials/create/shopify-streaming/catalog.png)

## Daten auswählen

Die **[!UICONTROL Daten auswählen]** angezeigt, um eine Oberfläche zur Auswahl der Daten bereitzustellen, die Sie in Platform importieren.

* Der linke Teil der Benutzeroberfläche ist ein Browser, mit dem Sie die verfügbaren Datenströme in Ihrem Konto anzeigen können.
* Im rechten Bereich der Benutzeroberfläche können Sie eine Vorschau von bis zu 100 Zeilen mit Daten aus einer JSON-Datei anzeigen.

Auswählen **[!UICONTROL Dateien hochladen]** , um eine JSON-Datei von Ihrem lokalen System hochzuladen. Alternativ können Sie die JSON-Datei, die Sie hochladen möchten, per Drag-and-Drop in die [!UICONTROL Dateien per Drag &amp; Drop verschieben] Bereich.

![Der Schritt Daten hinzufügen des Ursprungs-Workflows.](../../../../images/tutorials/create/shopify-streaming/select-data.png)

Nach dem Hochladen Ihrer Datei wird die Vorschau-Oberfläche aktualisiert, um eine Vorschau des hochgeladenen Schemas anzuzeigen. Über die Vorschau-Oberfläche können Sie den Inhalt und die Struktur einer Datei überprüfen. Sie können auch die [!UICONTROL Suchfeld] -Dienstprogramm zum Zugreifen auf bestimmte Elemente aus Ihrem Schema.

Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![Der Vorschauschritt des Ursprungs-Workflows.](../../../../images/tutorials/create/shopify-streaming/preview.png)

## Datenflussdetails

Die **Datenflussdetails** -Schritt angezeigt, der Ihnen Optionen zur Verwendung eines vorhandenen Datensatzes oder zur Einrichtung eines neuen Datensatzes für Ihren Datenfluss sowie die Möglichkeit bietet, einen Namen und eine Beschreibung für Ihren Datenfluss bereitzustellen. In diesem Schritt können Sie auch Einstellungen für die Profilerfassung, Fehlerdiagnose, partielle Erfassung und Warnhinweise konfigurieren.

Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![Der Schritt dataflow-detail des Ursprungs-Workflows.](../../../../images/tutorials/create/shopify-streaming/dataflow-detail.png)

## Zuordnung

Es erfolgt der Schritt der [!UICONTROL Zuordnung], in dem Ihnen eine Schnittstelle zum Zuordnen der Quellfelder aus Ihrem Quellschema zu den entsprechenden XDM-Zielfeldern im Zielschema bereitgestellt wird.

Platform bietet intelligente Empfehlungen für automatisch zugeordnete Felder, die auf dem ausgewählten Zielschema oder Datensatz basieren. Sie können die Zuordnungsregeln manuell an Ihre Anwendungsfälle anpassen. Je nach Bedarf können Sie wahlweise Felder direkt zuordnen oder mithilfe von Datenvorbereitungsfunktionen Quelldaten transformieren, um berechnete oder anderweitig ermittelte Werte abzuleiten. Umfassende Schritte zur Verwendung der Mapper-Oberfläche und der berechneten Felder finden Sie im Abschnitt [Handbuch zur Datenvorbereitung-Benutzeroberfläche](https://experienceleague.adobe.com/docs/experience-platform/data-prep/ui/mapping.html).

Nachdem die Quelldaten erfolgreich zugeordnet wurden, wählen Sie **[!UICONTROL Nächste]**.

![Der Zuordnungsschritt des Ursprungs-Workflows.](../../../../images/tutorials/create/shopify-streaming/mapping.png)

## Überprüfung

Der Schritt **[!UICONTROL Überprüfung]** wird angezeigt, sodass Sie Ihren neuen Datenfluss überprüfen können, bevor er hergestellt wird. Die Details lassen sich wie folgt kategorisieren:

* **[!UICONTROL Verbindung]**: Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quelldatei und die Anzahl der Spalten in dieser Quelldatei an.
* **[!UICONTROL Datensatz- und Zuordnungsfelder zuweisen]**: Zeigt an, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, dem der Datensatz entspricht.

Nachdem Sie Ihren Datenfluss überprüft haben, klicken Sie auf **[!UICONTROL Beenden]** und gewähren Sie etwas Zeit für die Erstellung des Datenflusses.

![Der Überprüfungsschritt des Ursprungs-Workflows.](../../../../images/tutorials/create/shopify-streaming/review.png)

## Abrufen der Streaming-Endpunkt-URL

Mit dem erstellten Streaming-Datenfluss können Sie jetzt Ihre Streaming-Endpunkt-URL abrufen. Dieser Endpunkt wird zum Abonnieren Ihres Webhooks verwendet, sodass Ihre Streaming-Quelle mit Experience Platform kommunizieren kann.

Um Ihren Streaming-Endpunkt abzurufen, navigieren Sie zum [!UICONTROL Datenfluss-Aktivität] Seite des soeben erstellten Datenflusses und kopieren Sie den Endpunkt vom unteren Rand des [!UICONTROL Eigenschaften] Bereich.

![Der Streaming-Endpunkt in der Datenfluss-Aktivität.](../../../../images/tutorials/create/shopify-streaming/endpoint.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Quellverbindung und einen Datenfluss zu Ihrem [!DNL Shopify Streaming] -Konto. Anweisungen zum Verbinden Ihrer [!DNL Shopify Streaming] -Konto mithilfe der API nutzen, lesen Sie bitte das Tutorial unter [Erstellen einer Quellverbindung und eines Datenflusses zum Streamen [!DNL Shopify] Daten mithilfe der Flow Service-API](../../../api/create/ecommerce/shopify-streaming.md).

