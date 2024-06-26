---
title: Erstellen einer HTTP-API-Streaming-Verbindung über die Benutzeroberfläche
description: Diese Anleitung für die Benutzeroberfläche hilft Ihnen beim Erstellen einer Streaming-Verbindung für Adobe Experience Platform.
exl-id: 7932471c-a9ce-4dd3-8189-8bc760ced5d6
source-git-commit: de721d204cda8e55c72ac5f530b89b2275d94306
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 28%

---


# Erstellen Sie eine [!DNL HTTP API] Streaming-Verbindung über die Benutzeroberfläche

In diesem Tutorial werden Schritte zum Erstellen einer Streaming-Quell-Verbindung mit dem [!UICONTROL Quellen] Arbeitsbereich.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   - [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemas vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   - [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

## Aufbauen einer Streaming-Verbindung

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste die Option **[!UICONTROL Quellen]**, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Unter dem **[!UICONTROL Streaming]** category, select **[!UICONTROL HTTP-API]** und wählen Sie **[!UICONTROL Daten hinzufügen]**.

![Katalog](../../../../images/tutorials/create/http/catalog.png)

Die **[!UICONTROL HTTP-API-Konto verbinden]** angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das HTTP-API-Konto aus, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Nächste]** um fortzufahren.

![vorhandenes Konto](../../../../images/tutorials/create/http/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]**. Geben Sie im angezeigten Formular einen Kontonamen und eine optionale Beschreibung ein. Sie erhalten außerdem die Möglichkeit, die folgenden Konfigurationseigenschaften anzugeben:

- **[!UICONTROL Authentifizierung]:** Diese Eigenschaft bestimmt, ob für die Streaming-Verbindung eine Authentifizierung erforderlich ist. Authentifizierung stellt sicher, dass Daten aus vertrauenswürdigen Quellen erfasst werden. Wenn Sie es mit persönlich identifizierbaren Informationen (PII) zu tun haben, sollte diese Eigenschaft aktiviert sein. Standardmäßig ist diese Eigenschaft deaktiviert.
- **[!UICONTROL XDM-kompatibel]:** Diese Eigenschaft gibt an, ob diese Streaming-Verbindung Ereignisse sendet, die mit XDM-Schemas kompatibel sind. Standardmäßig ist diese Eigenschaft deaktiviert.

Wählen Sie zum Abschluss **[!UICONTROL Verbindung mit Quelle herstellen]** und wählen Sie **[!UICONTROL Nächste]** um fortzufahren.

![new-account](../../../../images/tutorials/create/http/new.png)

## Daten auswählen

Nach der Erstellung der HTTP-API-Verbindung muss die **[!UICONTROL Daten auswählen]** angezeigt, und erhalten Sie eine Oberfläche zum Hochladen und Anzeigen einer Vorschau Ihrer Daten.

Auswählen **[!UICONTROL Dateien hochladen]** , um Ihre Daten hochzuladen. Alternativ können Sie Ihre Daten per Drag-and-Drop in die [!UICONTROL Dateien per Drag &amp; Drop verschieben] -Abschnitt der -Oberfläche.

![add-data](../../../../images/tutorials/create/http/add-data.png)

Nach dem Hochladen Ihrer Daten können Sie die rechte Seite der Benutzeroberfläche verwenden, um eine Vorschau Ihrer Dateihierarchie anzuzeigen. Klicken Sie auf **[!UICONTROL Weiter]**, um fortzufahren.

![preview-sample-data](../../../../images/tutorials/create/http/preview-sample-data.png)

## Zuordnen von Datenfeldern zu einem XDM-Schema

Die [!UICONTROL Zuordnung] -Schritt angezeigt und stellt eine Schnittstelle zum Zuordnen der Quelldaten zu einem Platform-Datensatz bereit.

Die [!DNL HTTP API] -Quelle unterstützt die Erfassung von JSON-Dateien. JSON-Dateien erfordern keine manuelle Konfiguration, wenn sie als XDM-Beschwerde gekennzeichnet sind. Andernfalls müssen Sie die Zuordnung explizit konfigurieren.

Wählen Sie einen Datensatz aus, in den eingehende Daten aufgenommen werden sollen. Sie können entweder einen vorhandenen Datensatz verwenden oder einen neuen erstellen.

### Erstellen eines neuen Datensatzes

Um einen neuen Datensatz zu erstellen, wählen Sie **[!UICONTROL Neuer Datensatz]**. Geben Sie im angezeigten Formular den Namen, eine optionale Beschreibung sowie das Zielschema für den Datensatz an. Wenn Sie eine [!DNL Profile]-aktiviertes Schema können Sie festlegen, ob der Datensatz auch [!DNL Profile]-enabled.

![new-dataset](../../../../images/tutorials/create/http/new-dataset.png)

### Verwenden eines vorhandenen Datensatzes

Um einen vorhandenen Datensatz zu verwenden, wählen Sie **[!UICONTROL Vorhandener Datensatz]**. Wählen Sie im angezeigten Formular den Datensatz aus, den Sie verwenden möchten. Nachdem Sie einen Datensatz ausgewählt haben, können Sie auswählen, ob der Datensatz [!DNL Profile]-enabled.

![existing-dataset](../../../../images/tutorials/create/http/existing-dataset.png)

### Standardfelder zuordnen

Je nach Bedarf können Sie wahlweise Felder direkt zuordnen oder mithilfe von Datenvorbereitungsfunktionen Quelldaten transformieren, um berechnete oder anderweitig ermittelte Werte abzuleiten. Umfassende Schritte zur Verwendung der Mapper-Oberfläche und der berechneten Felder finden Sie im Abschnitt [Handbuch zur Datenvorbereitung-Benutzeroberfläche](../../../../../data-prep/ui/mapping.md).

Um ein neues Quellfeld hinzuzufügen, wählen Sie **[!UICONTROL Neues Mapping hinzufügen]**.

![add-new-mapping](../../../../images/tutorials/create/http/add-new-mapping.png)

Eine neue Quell- und Zielfeldpaarung wird angezeigt. Um ein neues Quellfeld hinzuzufügen, wählen Sie das Pfeilsymbol neben dem [!UICONTROL Quellfeld auswählen] Eingabefelder.

![select-source-field](../../../../images/tutorials/create/http/select-source-field.png)

Die [!UICONTROL Attribute auswählen] können Sie Ihre Dateihierarchie untersuchen und ein bestimmtes Quellfeld auswählen, das einem Ziel-XDM-Feld zugeordnet werden soll. Nachdem Sie das Quellfeld ausgewählt haben, das Sie zuordnen möchten, wählen Sie **[!UICONTROL Auswählen]** um fortzufahren.

![select-attributes](../../../../images/tutorials/create/http/select-attributes.png)

Wenn ein Quellfeld ausgewählt ist, können Sie jetzt das entsprechende Ziel-XDM-Feld identifizieren, das zugeordnet werden soll. Wählen Sie das Schemensymbol unter dem Abschnitt Zielfeld aus.

![select-target-field](../../../../images/tutorials/create/http/select-target-field.png)

Die [!UICONTROL Zuordnen des Quellfelds zum Zielfeld] -Fenster angezeigt, in dem Sie eine Benutzeroberfläche zum Erkunden des Schemas Ihres Zieldatensatzes erhalten. Wählen Sie das Zielfeld aus, das Ihrem Quellfeld entspricht, und wählen Sie dann **[!UICONTROL Auswählen]** um fortzufahren.

![map-to-target-field](../../../../images/tutorials/create/http/map-to-target-field.png)

Sobald Ihre Quellfelder allen entsprechenden Ziel-XDM-Feldern zugeordnet sind, wählen Sie **[!UICONTROL Nächste]**

![data-prep-complete](../../../../images/tutorials/create/http/data-prep-complete.png)

## Datenflussdetails

Die **[!UICONTROL Datenflussdetails]** wird angezeigt. Auf dieser Seite können Sie Details zum erstellten Datenfluss angeben, indem Sie einen Namen und eine optionale Beschreibung angeben.

Nachdem Sie Details für den Datenfluss angegeben haben, wählen Sie **[!UICONTROL Nächste]**.

![dataflow-detail](../../../../images/tutorials/create/http/dataflow-detail.png)

## Überprüfung

Die **[!UICONTROL Überprüfen]** angezeigt, sodass Sie die Details Ihres Datenflusses vor der Erstellung überprüfen können. Details sind in den folgenden Kategorien gruppiert:

- **[!UICONTROL Verbindung]**: Zeigt den Kontonamen, die Quellplattform und den Quellnamen an.
- **[!UICONTROL Datensatz- und Zuordnungsfelder zuweisen]**: Zeigt den Zieldatensatz und das Schema an, dem der Datensatz entspricht.

Nachdem Sie bestätigt haben, dass die Details korrekt sind, wählen Sie **[!UICONTROL Beenden]**.

![überprüfen](../../../../images/tutorials/create/http/review.png)

## Abrufen der Streaming-Endpunkt-URL

Nach der Erstellung der Verbindung wird die Detailseite der Quellen angezeigt. Auf dieser Seite finden Sie Details zu Ihrer neu erstellten Verbindung, einschließlich zuvor ausgeführter Datenflüsse, ID und Streaming-Endpunkt-URL.

![Endpunkt](../../../../images/tutorials/create/http/endpoint.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Streaming-HTTP-Verbindung erstellt, über die Sie mithilfe des Streaming-Endpunkts auf eine Vielzahl von [!DNL Data Ingestion] APIs. Anweisungen zum Erstellen einer Streaming-Verbindung in der API finden Sie in der [Anleitung zum Erstellen einer Streaming-Verbindung](../../../api/create/streaming/http.md).

Informationen zum Streamen von Daten an Platform finden Sie im Tutorial zu [Streaming von Zeitreihendaten](../../../../../ingestion/tutorials/streaming-time-series-data.md) oder das Tutorial zu [Streaming von Datensatzdaten](../../../../../ingestion/tutorials/streaming-record-data.md).
