---
keywords: Experience Platform; Startseite; beliebte Themen; Streaming-Verbindung; Streaming-Verbindung erstellen; Handbuch; Tutorial; Erstellen einer Streaming-Verbindung; Streaming-Erfassung; Erfassung;
solution: Experience Platform
title: Erstellen einer Streaming-Verbindung über die Benutzeroberfläche
topic-legacy: tutorial
type: Tutorial
description: Diese Anleitung für die Benutzeroberfläche hilft Ihnen beim Erstellen einer Streaming-Verbindung für Adobe Experience Platform.
exl-id: 7932471c-a9ce-4dd3-8189-8bc760ced5d6
source-git-commit: df6ddf52f5cab7e5faae591594f060d641977783
workflow-type: tm+mt
source-wordcount: '1061'
ht-degree: 10%

---


# Aufbauen einer Streaming-Verbindung über die Benutzeroberfläche

In diesem Tutorial werden Schritte zum Erstellen einer Streaming-Quellverbindung mithilfe des Arbeitsbereichs [!UICONTROL Quellen] beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten  [!DNL Experience Platform] organisiert werden.
   - [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   - [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) zum Schema Editor: Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

## Aufbauen einer Streaming-Verbindung

Wählen Sie in der Platform-Benutzeroberfläche **[!UICONTROL Quellen]** aus dem linken Navigationsbereich aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] enthält eine Vielzahl von Quellen, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie **[!UICONTROL Streaming]** die Option **[!UICONTROL HTTP-API]** und klicken Sie dann auf **[!UICONTROL Daten hinzufügen]**.

![Katalog](../../../../images/tutorials/create/http/catalog.png)

Die Seite **[!UICONTROL HTTP-API-Konto verbinden]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das HTTP-API-Konto, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![vorhandenes Konto](../../../../images/tutorials/create/http/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** aus. Geben Sie im angezeigten Formular einen Kontonamen und eine optionale Beschreibung ein. Sie erhalten außerdem die Möglichkeit, die folgenden Konfigurationseigenschaften anzugeben:

- **[!UICONTROL Authentifizierung]:** Diese Eigenschaft bestimmt, ob für die Streaming-Verbindung eine Authentifizierung erforderlich ist. Authentifizierung stellt sicher, dass Daten aus vertrauenswürdigen Quellen erfasst werden. Wenn Sie es mit persönlich identifizierbaren Informationen (PII) zu tun haben, sollte diese Eigenschaft aktiviert sein. Standardmäßig ist diese Eigenschaft deaktiviert.
- **[!UICONTROL XDM-kompatibel]:**  Diese Eigenschaft gibt an, ob diese Streaming-Verbindung Ereignisse sendet, die mit XDM-Schemas kompatibel sind. Standardmäßig ist diese Eigenschaft deaktiviert.

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![new-account](../../../../images/tutorials/create/http/new.png)

## Daten auswählen

Nach Erstellung der HTTP-API-Verbindung wird der Schritt **[!UICONTROL Daten auswählen]** angezeigt, der Ihnen eine Benutzeroberfläche zum Hochladen und Anzeigen einer Vorschau Ihrer Daten bietet.

Wählen Sie **[!UICONTROL Hochladen von Dateien]** aus, um Ihre Daten hochzuladen. Alternativ können Sie Ihre Daten per Drag-and-Drop in den Bereich [!UICONTROL Drag-and-Drop von Dateien] der Benutzeroberfläche ziehen.

![add-data](../../../../images/tutorials/create/http/add-data.png)

Nach dem Hochladen Ihrer Daten können Sie die rechte Seite der Benutzeroberfläche verwenden, um eine Vorschau Ihrer Dateihierarchie anzuzeigen. Wählen Sie **[!UICONTROL Weiter]** aus, um fortzufahren.

![preview-sample-data](../../../../images/tutorials/create/http/preview-sample-data.png)

## Zuordnen von Datenfeldern zu einem XDM-Schema

Der Schritt [!UICONTROL Zuordnung] wird angezeigt und stellt eine Schnittstelle bereit, über die die Quelldaten einem Platform-Datensatz zugeordnet werden können.

Parquet-Dateien müssen XDM-konform sein und erfordern keine manuelle Konfiguration der Zuordnung. Bei CSV-Dateien ist es erforderlich, die Zuordnung explizit zu konfigurieren. Sie können jedoch festlegen, welche Quelldatenfelder zugeordnet werden sollen. JSON-Dateien, die als XDM-Beschwerde gekennzeichnet sind, erfordern keine manuelle Konfiguration. Wenn es jedoch nicht als XDM-kompatibel markiert ist, müssen Sie die Zuordnung explizit konfigurieren.

Wählen Sie einen Datensatz für eingehende Daten aus, die in aufgenommen werden sollen. Sie können entweder einen vorhandenen Datensatz verwenden oder einen neuen erstellen.

### Neuen Datensatz erstellen

Um einen neuen Datensatz zu erstellen, wählen Sie **[!UICONTROL Neuer Datensatz]** aus. Geben Sie im angezeigten Formular den Namen, eine optionale Beschreibung sowie das Zielschema für den Datensatz an. Wenn Sie ein [!DNL Profile]-aktiviertes Schema auswählen, können Sie festlegen, ob der Datensatz auch [!DNL Profile]-fähig sein soll.

![new-dataset](../../../../images/tutorials/create/http/new-dataset.png)

### Vorhandenen Datensatz verwenden

Um einen vorhandenen Datensatz zu verwenden, wählen Sie **[!UICONTROL Vorhandenen Datensatz]** aus. Wählen Sie im angezeigten Formular den Datensatz aus, den Sie verwenden möchten. Nachdem Sie einen Datensatz ausgewählt haben, können Sie auswählen, ob der Datensatz [!DNL Profile]-fähig sein soll.

![existing-dataset](../../../../images/tutorials/create/http/existing-dataset.png)

### Standardfelder zuordnen

Je nach Bedarf können Sie Felder direkt zuordnen oder mithilfe von Datenvorbereitungsfunktionen Quelldaten transformieren, um berechnete oder berechnete Werte abzuleiten. Weiterführende Informationen zu Zuordnungsfunktionen und berechneten Feldern finden Sie im [Handbuch zu Datenvorbereitung-Funktionen](../../../../../data-prep/functions.md) oder im Handbuch [Berechnete Felder](../../../../../data-prep/calculated-fields.md).

Um ein neues Quellfeld hinzuzufügen, wählen Sie **[!UICONTROL Neue Zuordnung hinzufügen]** aus.

![add-new-mapping](../../../../images/tutorials/create/http/add-new-mapping.png)

Eine neue Quell- und Zielfeldpaarung wird angezeigt. Um ein neues Quellfeld hinzuzufügen, wählen Sie das Pfeilsymbol neben der EingabebLeiste [!UICONTROL Quellfeld] auswählen aus.

![select-source-field](../../../../images/tutorials/create/http/select-source-field.png)

Im Bedienfeld [!UICONTROL Attribute auswählen] können Sie Ihre Dateihierarchie untersuchen und ein bestimmtes Quellfeld auswählen, das einem Ziel-XDM-Feld zugeordnet werden soll. Nachdem Sie das Quellfeld ausgewählt haben, das Sie zuordnen möchten, wählen Sie **[!UICONTROL Wählen Sie]** aus, um fortzufahren.

![select-attributes](../../../../images/tutorials/create/http/select-attributes.png)

Wenn ein Quellfeld ausgewählt ist, können Sie jetzt das entsprechende Ziel-XDM-Feld identifizieren, das zugeordnet werden soll. Wählen Sie das Schemensymbol unter dem Abschnitt Zielfeld aus.

![select-target-field](../../../../images/tutorials/create/http/select-target-field.png)

Das Fenster [!UICONTROL Quellfeld dem Zielfeld zuordnen] wird angezeigt und bietet eine Schnittstelle zur Erforschung des Schemas Ihres Zieldatensatzes. Wählen Sie das Zielfeld aus, das Ihrem Quellfeld entspricht, und wählen Sie dann **[!UICONTROL Wählen Sie]** aus, um fortzufahren.

![map-to-target-field](../../../../images/tutorials/create/http/map-to-target-field.png)

Nachdem alle Quellfelder den entsprechenden XDM-Zielfeldern zugeordnet sind, wählen Sie **[!UICONTROL Weiter]** aus.

![data-prep-complete](../../../../images/tutorials/create/http/data-prep-complete.png)

## Datenflussdetails

Der Schritt **[!UICONTROL Datenfluss-Detail]** wird angezeigt. Auf dieser Seite können Sie Details zum erstellten Datenfluss angeben, indem Sie einen Namen und eine optionale Beschreibung angeben.

Nachdem Sie Details für den Datenfluss angegeben haben, wählen Sie **[!UICONTROL Weiter]** aus.

![dataflow-detail](../../../../images/tutorials/create/http/dataflow-detail.png)

## Überprüfung

Der Schritt **[!UICONTROL Überprüfen]** wird angezeigt, mit dem Sie die Details Ihres Datenflusses überprüfen können, bevor er erstellt wird. Details sind in den folgenden Kategorien gruppiert:

- **[!UICONTROL Verbindung]**: Zeigt den Kontonamen, die Quellplattform und den Quellnamen an.
- **[!UICONTROL Zuweisen von Datensatz- und Zuordnungsfeldern]**: Zeigt den Zieldatensatz und das Schema an, dem der Datensatz entspricht.

Nachdem Sie bestätigt haben, dass die Details korrekt sind, wählen Sie **[!UICONTROL Finish]** aus.

![Überprüfung](../../../../images/tutorials/create/http/review.png)

## Abrufen der Streaming-Endpunkt-URL

Nach der Erstellung der Verbindung wird die Detailseite der Quellen angezeigt. Auf dieser Seite finden Sie Details zu Ihrer neu erstellten Verbindung, einschließlich zuvor ausgeführter Datenflüsse, ID und Streaming-Endpunkt-URL.

![Endpunkt](../../../../images/tutorials/create/http/endpoint.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Streaming-HTTP-Verbindung erstellt, über die Sie über den Streaming-Endpunkt auf verschiedene [!DNL Data Ingestion]-APIs zugreifen können. Anweisungen zum Erstellen einer Streaming-Verbindung in der API finden Sie in der [Anleitung zum Erstellen einer Streaming-Verbindung](../../../api/create/streaming/http.md).

Informationen zum Streamen von Daten an Platform finden Sie im Tutorial zu [Streaming-Zeitreihendaten](../../../../../ingestion/tutorials/streaming-time-series-data.md) oder im Tutorial zu [Streaming-Datensatzdaten](../../../../../ingestion/tutorials/streaming-record-data.md).
