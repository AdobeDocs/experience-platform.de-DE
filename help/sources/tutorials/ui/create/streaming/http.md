---
keywords: Experience Platform;Home;beliebte Themen;Streaming-Verbindung;Streaming-Verbindung erstellen;UI-Handbuch;Tutorial;Erstellen einer Streaming-Verbindung;Streaming-Verbindung;Erfassung;
solution: Experience Platform
title: Erstellen einer Streaming-Verbindung mithilfe der Benutzeroberfläche
topic: tutorial
type: Tutorial
description: Diese Anleitung für die Benutzeroberfläche hilft Ihnen beim Erstellen einer Streaming-Verbindung für Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: a4019227abaddd9dbe143899d273580ebf21849e
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 17%

---


# Aufbauen einer Streaming-Verbindung über die Benutzeroberfläche

Diese Anleitung für die Benutzeroberfläche hilft Ihnen beim Erstellen einer Streaming-Verbindung für Adobe Experience Platform.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten  [!DNL Experience Platform] organisiert werden.
   - [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   - [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

## Aufbauen einer Streaming-Verbindung

Nach der Anmeldung bei der [!DNL Experience Platform]-Benutzeroberfläche wählen Sie **[!UICONTROL Quellen]** in der linken Navigationsleiste, um auf den Arbeitsbereich **[!UICONTROL Quellen]** zuzugreifen. Der Bildschirm **[!UICONTROL Katalog]** zeigt eine Reihe von Quellen an, für die Sie ein Konto erstellen können.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle mit der Suchoption finden.

Wählen Sie unter der Kategorie **[!UICONTROL Streaming]** **[!UICONTROL HTTP API]**. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie **[!UICONTROL Konfigurieren]**. Andernfalls wählen Sie **[!UICONTROL Hinzufügen Daten]** aus, um einen neuen HTTP-Streaming-Connector zu erstellen.

![](../../../../images/tutorials/create/http/catalog.png)

Die Seite **[!UICONTROL HTTP-API-Konto verbinden]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie **[!UICONTROL Neues Konto]**. Geben Sie im eingeblendeten Eingabebild einen Kontonamen und eine optionale Beschreibung ein. Sie haben außerdem die Möglichkeit, die folgenden Konfigurationseigenschaften anzugeben:

- **[!UICONTROL Authentifizierung]:** Diese Eigenschaft bestimmt, ob die Streaming-Verbindung authentifiziert werden muss. Authentifizierung stellt sicher, dass Daten aus vertrauenswürdigen Quellen erfasst werden. Wenn Sie mit personenbezogenen identifizierbaren Informationen (PII) zu tun haben, sollte diese Eigenschaft aktiviert werden. Standardmäßig ist diese Eigenschaft deaktiviert.
- **[!UICONTROL XDM-Schema-Kompatibilität]:** Diese Eigenschaft gibt an, ob diese Streaming-Verbindung Ereignis sendet, die mit XDM-Schemas kompatibel sind. Standardmäßig ist diese Eigenschaft aktiviert.

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und dann **[!UICONTROL Weiter]** aus, um fortzufahren.

![](../../../../images/tutorials/create/http/new-account.png)

### Vorhandenes Konto

Um eine Verbindung mit vorhandenen Anmeldeinformationen herzustellen, wählen Sie die zu verwendende HTTP-API-Verbindung aus und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![](../../../../images/tutorials/create/http/existing-account.png)

## Daten auswählen

Nach dem Erstellen der HTTP-API-Verbindung wird der Schritt **[!UICONTROL Daten auswählen]** angezeigt und stellt eine Schnittstelle bereit, mit der Sie auswählen können, mit welchem Datensatz eine Verbindung hergestellt werden soll. Sie können entweder einen neuen Datensatz erstellen oder eine Verbindung zu einem vorhandenen Datensatz herstellen.

### Neuen Datensatz erstellen

Um einen neuen Datensatz zu erstellen, wählen Sie **[!UICONTROL Neuer Datensatz]**. Geben Sie im angezeigten Formular den Namen, eine optionale Beschreibung sowie das Schema Zielgruppe für den Datensatz ein. Wenn Sie ein Schema mit aktiviertem Profil auswählen, können Sie festlegen, ob auch Profil aktiviert werden soll.

![](../../../../images/tutorials/create/http/new-dataset.png)

### Vorhandenen Datensatz verwenden

Um einen vorhandenen Datensatz zu verwenden, wählen Sie **[!UICONTROL Vorhandener Datensatz]**. Wählen Sie im angezeigten Formular den zu verwendenden Datensatz aus. Nach Auswahl eines Datensatzes können Sie auswählen, ob das Profil des Datensatzes aktiviert werden soll.

![](../../../../images/tutorials/create/http/existing-dataset.png)

## Datenaflow-Detail

Der Schritt **[!UICONTROL Datenaflow detail]** wird angezeigt. Auf dieser Seite können Sie Details zum erstellten Datenpfad angeben, indem Sie einen Namen und eine optionale Beschreibung angeben.

Nachdem Sie Details zum Datenflug bereitgestellt haben, wählen Sie **[!UICONTROL Weiter]**.

![](../../../../images/tutorials/create/http/dataflow-detail.png)

## Überprüfung

Der Schritt **[!UICONTROL Überprüfen]** wird angezeigt, mit dem Sie die Details Ihres Datenflusses überprüfen können, bevor er erstellt wird. Details sind in den folgenden Kategorien gruppiert:

- **[!UICONTROL Verbindung]**: Zeigt den Kontonamen, die Quellplattform und den Quellnamen an.
- **[!UICONTROL Zuweisen von Dataset- und Zuordnungsfeldern]**: Zeigt den Dataset der Zielgruppe und das Schema an, das der Datensatz einhält.

Nachdem Sie bestätigt haben, dass die Details korrekt sind, wählen Sie **[!UICONTROL Finish]**.

![](../../../../images/tutorials/create/http/review.png)

## Abrufen der Streaming-Endpunkt-URL

Bei der Erstellung der Verbindung wird die Seite mit den Quelldetails angezeigt. Auf dieser Seite werden Details zu Ihrer neu erstellten Verbindung angezeigt, einschließlich der zuvor ausgeführten Datenflüsse, ID und Streaming-Endpunkt-URL.

![](../../../../images/tutorials/create/http/get-streaming-url.png)

## Nächste Schritte

In diesem Lernprogramm haben Sie eine Streaming-HTTP-Verbindung erstellt, über die Sie den Streaming-Endpunkt verwenden können, um auf eine Vielzahl von [!DNL Data Ingestion]-APIs zuzugreifen. Anweisungen zum Erstellen einer Streaming-Verbindung in der API finden Sie in der [Anleitung zum Erstellen einer Streaming-Verbindung](../../../api/create/streaming/http.md).

Informationen zum Streamen von Daten auf die Plattform finden Sie im Tutorial zu [Streaming-Zeitreihendaten](../../../../../ingestion/tutorials/streaming-time-series-data.md) oder im Tutorial zu [Streaming-Datensatzdaten](../../../../../ingestion/tutorials/streaming-record-data.md).
