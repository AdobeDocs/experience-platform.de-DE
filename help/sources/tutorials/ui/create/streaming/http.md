---
keywords: Experience Platform;Home;beliebte Themen;Streaming-Verbindung;Streaming-Verbindung erstellen;UI-Handbuch;Tutorial;Erstellen einer Streaming-Verbindung;Streaming-Verbindung;Erfassung;
solution: Experience Platform
title: Erstellen einer Streaming-Verbindung mithilfe der Benutzeroberfläche
topic: Tutorial
type: Tutorial
description: Diese Anleitung für die Benutzeroberfläche hilft Ihnen beim Erstellen einer Streaming-Verbindung für Adobe Experience Platform.
exl-id: 7932471c-a9ce-4dd3-8189-8bc760ced5d6
translation-type: tm+mt
source-git-commit: 3b71f1399a770e097cf75827e626d6d4e289ab77
workflow-type: tm+mt
source-wordcount: '1061'
ht-degree: 9%

---


# Aufbauen einer Streaming-Verbindung über die Benutzeroberfläche

Dieses Lernprogramm enthält Schritte zum Erstellen einer Streaming-Quellverbindung mit dem Arbeitsbereich [!UICONTROL Quellen].

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten  [!DNL Experience Platform] organisiert werden.
   - [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   - [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

## Aufbauen einer Streaming-Verbindung

Wählen Sie in der Plattform-Benutzeroberfläche **[!UICONTROL Quellen]** aus der linken Navigation, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] enthält eine Reihe von Quellen, mit denen Sie ein Konto erstellen können.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle mit der Suchoption finden.

Wählen Sie unter der Kategorie **[!UICONTROL Streaming]** **[!UICONTROL HTTP-API]** und dann **[!UICONTROL Hinzufügen Daten]**.

![Katalog](../../../../images/tutorials/create/http/catalog.png)

Die Seite **[!UICONTROL HTTP-API-Konto verbinden]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das HTTP-API-Konto, mit dem Sie einen neuen Datenflug erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![existing-account](../../../../images/tutorials/create/http/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]**. Geben Sie im eingeblendeten Eingabebild einen Kontonamen und eine optionale Beschreibung ein. Sie haben außerdem die Möglichkeit, die folgenden Konfigurationseigenschaften anzugeben:

- **[!UICONTROL Authentifizierung]:** Diese Eigenschaft bestimmt, ob die Streaming-Verbindung authentifiziert werden muss. Authentifizierung stellt sicher, dass Daten aus vertrauenswürdigen Quellen erfasst werden. Wenn Sie mit personenbezogenen identifizierbaren Informationen (PII) zu tun haben, sollte diese Eigenschaft aktiviert werden. Standardmäßig ist diese Eigenschaft deaktiviert.
- **[!UICONTROL XDM-kompatibel]:** Diese Eigenschaft gibt an, ob diese Streaming-Verbindung Ereignis sendet, die mit XDM-Schemas kompatibel sind. Standardmäßig ist diese Eigenschaft deaktiviert.

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und dann **[!UICONTROL Weiter]** aus, um fortzufahren.

![new-account](../../../../images/tutorials/create/http/new.png)

## Daten auswählen

Nach dem Erstellen der HTTP-API-Verbindung wird der Schritt **[!UICONTROL Daten auswählen]** angezeigt, der Ihnen eine Oberfläche zum Hochladen und Vorschau Ihrer Daten bietet.

Wählen Sie **[!UICONTROL Dateien hochladen]**, um Ihre Daten hochzuladen. Alternativ können Sie Ihre Daten per Drag &amp; Drop in den Bereich [!UICONTROL Drag &amp; Drop von Dateien] der Oberfläche ziehen.

![add-data](../../../../images/tutorials/create/http/add-data.png)

Beim Hochladen der Daten können Sie die Dateihierarchie auf der rechten Seite der Benutzeroberfläche Vorschau haben. Wählen Sie **[!UICONTROL Weiter]**, um fortzufahren.

![Vorschau-Muster-Daten](../../../../images/tutorials/create/http/preview-sample-data.png)

## Zuordnen von Datenfeldern zu einem XDM-Schema

Der Schritt [!UICONTROL Zuordnung] wird angezeigt und stellt eine Schnittstelle bereit, über die die Quelldaten einem Platform-Datensatz zugeordnet werden können.

Parquet-Dateien müssen XDM-konform sein und müssen die Zuordnung nicht manuell konfigurieren, während für CSV-Dateien explizit die Zuordnung konfiguriert werden muss. Sie müssen jedoch festlegen, welche Quelldatenfelder zugeordnet werden sollen. JSON-Dateien, die als XDM-Beschwerde markiert sind, erfordern keine manuelle Konfiguration. Wenn es jedoch nicht als XDM-kompatibel markiert ist, müssen Sie die Zuordnung explizit konfigurieren.

Wählen Sie einen Datensatz, in den eingehende Daten aufgenommen werden sollen. Sie können entweder einen vorhandenen Datensatz verwenden oder einen neuen erstellen.

### Neuen Datensatz erstellen

Um einen neuen Datensatz zu erstellen, wählen Sie **[!UICONTROL Neuer Datensatz]**. Geben Sie im angezeigten Formular den Namen, eine optionale Beschreibung sowie das Schema Zielgruppe für den Datensatz ein. Wenn Sie ein [!DNL Profile]-aktiviertes Schema auswählen, können Sie festlegen, ob das Dataset auch [!DNL Profile]-fähig sein soll.

![new-dataset](../../../../images/tutorials/create/http/new-dataset.png)

### Vorhandenen Datensatz verwenden

Um einen vorhandenen Datensatz zu verwenden, wählen Sie **[!UICONTROL Vorhandener Datensatz]**. Wählen Sie im angezeigten Formular den zu verwendenden Datensatz aus. Wenn Sie einen Datensatz ausgewählt haben, können Sie auswählen, ob der Datensatz [!DNL Profile] aktiviert sein soll.

![existing-dataset](../../../../images/tutorials/create/http/existing-dataset.png)

### Standardfelder zuordnen

Je nach Bedarf können Sie festlegen, ob Felder direkt zugeordnet werden sollen, oder Sie können mithilfe der Datenvorgabefunktionen Quelldaten transformieren, um berechnete oder berechnete Werte abzuleiten. Weitere Informationen zu Datenzuordnungs- und -zuordnungsfunktionen finden Sie im Lernprogramm [Zuordnen von CSV-Daten zu XDM-Schema-Feldern](../../../../../ingestion/tutorials/map-a-csv-file.md).

Um ein neues Quellfeld hinzuzufügen, wählen Sie **[!UICONTROL Hinzufügen neue Zuordnung]**.

![add-new-mapping](../../../../images/tutorials/create/http/add-new-mapping.png)

Eine neue Quell- und Zielgruppe-Feldpaarung wird angezeigt. Um ein neues Quellfeld hinzuzufügen, wählen Sie das Pfeilsymbol neben der Eingabebeleiste [!UICONTROL Quellfeld] auswählen.

![select-source-field](../../../../images/tutorials/create/http/select-source-field.png)

Mit dem Bedienfeld [!UICONTROL Attribute auswählen] können Sie Ihre Dateihierarchie untersuchen und ein bestimmtes Quellfeld auswählen, das einem XDM-Feld der Zielgruppe zugeordnet werden soll. Nachdem Sie das zu zuordnende Quellfeld ausgewählt haben, wählen Sie **[!UICONTROL Wählen Sie]** aus, um fortzufahren.

![select-attribute](../../../../images/tutorials/create/http/select-attributes.png)

Wenn ein Quellfeld ausgewählt ist, können Sie jetzt das entsprechende XDM-Feld für die Zielgruppe identifizieren, dem Sie zuordnen möchten. Wählen Sie das Symbol Schema unter dem Feldabschnitt Zielgruppe aus.

![select-Zielgruppe-field](../../../../images/tutorials/create/http/select-target-field.png)

Das Fenster [!UICONTROL Quellfeld der Zielgruppe zuordnen] wird angezeigt und bietet eine Oberfläche, über die Sie das Schema Ihres Zielgruppe-Datasets erkunden können. Wählen Sie das Feld &quot;Zielgruppe&quot;, das mit dem Quellfeld übereinstimmt, und klicken Sie dann auf **[!UICONTROL Wählen Sie]**, um fortzufahren.

![map-to-Zielgruppe-field](../../../../images/tutorials/create/http/map-to-target-field.png)

Sobald die Quellfelder allen entsprechenden XDM-Feldern der Zielgruppe zugeordnet sind, wählen Sie **[!UICONTROL Weiter]**

![data-prep-complete](../../../../images/tutorials/create/http/data-prep-complete.png)

## Datenaflow-Detail

Der Schritt **[!UICONTROL Datenaflow detail]** wird angezeigt. Auf dieser Seite können Sie Details zum erstellten Datenpfad angeben, indem Sie einen Namen und eine optionale Beschreibung angeben.

Nachdem Sie Details zum Datenflug bereitgestellt haben, wählen Sie **[!UICONTROL Weiter]**.

![dataflow-detail](../../../../images/tutorials/create/http/dataflow-detail.png)

## Überprüfung

Der Schritt **[!UICONTROL Überprüfen]** wird angezeigt, mit dem Sie die Details Ihres Datenflusses überprüfen können, bevor er erstellt wird. Details sind in den folgenden Kategorien gruppiert:

- **[!UICONTROL Verbindung]**: Zeigt den Kontonamen, die Quellplattform und den Quellnamen an.
- **[!UICONTROL Zuweisen von Dataset- und Zuordnungsfeldern]**: Zeigt den Dataset der Zielgruppe und das Schema an, das der Datensatz einhält.

Nachdem Sie bestätigt haben, dass die Details korrekt sind, wählen Sie **[!UICONTROL Finish]**.

![überprüfen](../../../../images/tutorials/create/http/review.png)

## Abrufen der Streaming-Endpunkt-URL

Bei der Erstellung der Verbindung wird die Seite mit den Quelldetails angezeigt. Auf dieser Seite werden Details zu Ihrer neu erstellten Verbindung angezeigt, einschließlich der zuvor ausgeführten Datenflüsse, ID und Streaming-Endpunkt-URL.

![endpoint](../../../../images/tutorials/create/http/endpoint.png)

## Nächste Schritte

In diesem Lernprogramm haben Sie eine Streaming-HTTP-Verbindung erstellt, über die Sie den Streaming-Endpunkt verwenden können, um auf eine Vielzahl von [!DNL Data Ingestion]-APIs zuzugreifen. Anweisungen zum Erstellen einer Streaming-Verbindung in der API finden Sie in der [Anleitung zum Erstellen einer Streaming-Verbindung](../../../api/create/streaming/http.md).

Informationen zum Streamen von Daten auf die Plattform finden Sie im Tutorial zu [Streaming-Zeitreihendaten](../../../../../ingestion/tutorials/streaming-time-series-data.md) oder im Tutorial zu [Streaming-Datensatzdaten](../../../../../ingestion/tutorials/streaming-record-data.md).
