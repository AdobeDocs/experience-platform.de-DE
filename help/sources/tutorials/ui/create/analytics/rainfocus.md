---
title: RainFocus-Konto über die Benutzeroberfläche mit der Experience Platform verbinden
description: Erfahren Sie, wie Sie Ihr RainFocus-Konto über die Benutzeroberfläche mit Experience Platform verbinden.
badge: Beta
source-git-commit: 1ed82798125f32fe392f2a06a12280ac61f225c6
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 29%

---

# Verbinden Sie [!DNL RainFocus] Konto für die Experience Platform über die Benutzeroberfläche

>[!NOTE]
>
>Die [!DNL RainFocus]-Quelle befindet sich in der Beta-Phase. Siehe [Quellen - Übersicht](../../../../home.md#terms-and-conditions) für weitere Informationen zur Verwendung von Beta-beschrifteten Quellen.

In diesem Tutorial erfahren Sie, wie Sie Ihre [!DNL RainFocus] Konto- und Stream-Ereignisverwaltung und -analysedaten an Adobe Experience Platform.

>[!IMPORTANT]
>
>Diese Quell-Connector- und Dokumentationsseite wird von der [!DNL RainFocus] Team. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an den Kundendienst<span>@rainfocus.com oder besuchen Sie die [[!DNL RainFocus] Hilfe-Center](https://help.rainfocus.com/hc/en-us)

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemas vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

### Voraussetzungen

Bevor Sie Ihre [!DNL RainFocus] -Konto in Experience Platform verwenden, müssen Sie zunächst die folgenden erforderlichen Aufgaben ausführen:

* [Sammeln erforderlicher Anmeldeinformationen](../../../../connectors/analytics/rainfocus.md#gather-required-credentials)
* [Erstellen eines XDM-Schemas und Definieren des Identitätsfelds](../../../../connectors/analytics/rainfocus.md#create-an-xdm-schema-and-define-the-identity-field)
* [Erstellen eines Integrationsprofils in RainFocus](../../../../connectors/analytics/rainfocus.md#create-an-integration-profile-in-rainfocus)

Nach Abschluss der erforderlichen Einrichtung können Sie mit den unten beschriebenen Schritten fortfahren.

## RainFocus-Konto mit Experience Platform verbinden

Wählen Sie in der Platform-Benutzeroberfläche die Option **[!UICONTROL Quellen]** über die linke Navigationsleiste auf den Arbeitsbereich &quot;Quellen&quot;zugreifen. Die *[!UICONTROL Katalog]* zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Unter dem *[!UICONTROL Analytics]* category, select **[!UICONTROL RainFocus-Erlebnis]** und wählen Sie **[!UICONTROL Daten hinzufügen]**.

![Der Quellkatalog zur Benutzeroberfläche der Experience Platform mit der ausgewählten Quelle RainFocus .](/help/sources/images/tutorials/create/rainfocus/rainfocus_sources-rf.png)

## Daten auswählen

Der Schritt Daten auswählen wird angezeigt und bietet eine Oberfläche zur Auswahl der Daten, die Sie zur Experience Platform mitbringen.

* Der linke Teil der Benutzeroberfläche ist ein Browser, mit dem Sie die verfügbaren Datenströme in Ihrem Konto anzeigen können.
* Im rechten Bereich der Benutzeroberfläche können Sie eine Vorschau von bis zu 100 Zeilen mit Daten aus einer JSON-Datei anzeigen.

Auswählen **[!UICONTROL Dateien hochladen]** , um eine JSON-Datei von Ihrem lokalen System hochzuladen. Alternativ können Sie die JSON-Datei, die Sie hochladen möchten, per Drag-and-Drop in den Bereich Dateien ziehen und ablegen.

Laden Sie die JSON-Beispielnutzlast hoch, die von heruntergeladen wurde. **RainFocus**.

![Der Schritt Daten auswählen im Ursprungs-Workflow.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-json-upload.png)

Nach dem Hochladen Ihrer Datei wird die Vorschau-Oberfläche aktualisiert, um eine Vorschau des hochgeladenen Schemas anzuzeigen. Über die Vorschau-Oberfläche können Sie den Inhalt und die Struktur einer Datei überprüfen. Sie können auch das Dienstprogramm &quot;Suchfeld&quot;verwenden, um auf bestimmte Elemente innerhalb Ihres Schemas zuzugreifen.

Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![Der Schritt Datenvorschau des Ursprungs-Workflows.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-json-preview.png)

## Datenflussdetails

Die **Datenflussdetails** -Schritt angezeigt, der Ihnen Optionen zur Verwendung eines vorhandenen Datensatzes oder zur Einrichtung eines neuen Datensatzes für Ihren Datenfluss sowie die Möglichkeit bietet, einen Namen und eine Beschreibung für Ihren Datenfluss bereitzustellen. In diesem Schritt können Sie auch Einstellungen für die Profilerfassung, Fehlerdiagnose, partielle Erfassung und Warnhinweise konfigurieren.

Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![Der Schritt &quot;Datenfluss-Detail&quot;des Ursprungs-Workflows.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-dataflow-setup.png)

## Zuordnung {#mapping}

Es erfolgt der Schritt der Zuordnung, in dem Ihnen eine Schnittstelle zum Zuordnen der Quellfelder aus Ihrem Quellschema zu den entsprechenden XDM-Zielfeldern im Zielschema bereitgestellt wird.

Experience Platform bietet intelligente Empfehlungen für automatisch zugeordnete Felder, die auf dem ausgewählten Zielschema oder Datensatz basieren. Sie können die Zuordnungsregeln manuell an Ihre Anwendungsfälle anpassen. Je nach Bedarf können Sie wahlweise Felder direkt zuordnen oder mithilfe von Datenvorbereitungsfunktionen Quelldaten transformieren, um berechnete oder anderweitig ermittelte Werte abzuleiten. Umfassende Schritte zur Verwendung der Mapper-Oberfläche und der berechneten Felder finden Sie im Abschnitt [Handbuch zur Datenvorbereitung-Benutzeroberfläche](../../../../../data-prep/ui/mapping.md).

Nachdem die Quelldaten erfolgreich zugeordnet wurden, wählen Sie **[!UICONTROL Nächste]**.

![Der Zuordnungsschritt des Ursprungs-Workflows.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-mappings.png)

## Überprüfung

Der Schritt **Überprüfung** wird angezeigt, sodass Sie Ihren neuen Datenfluss überprüfen können, bevor er hergestellt wird. Die Details lassen sich wie folgt kategorisieren:

* **Verbindung**: Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quelldatei und die Anzahl der Spalten innerhalb dieser Quelldatei an.
* **Datensatz- und Zuordnungsfelder zuweisen**: Zeigt an, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, dem der Datensatz entspricht.

Nachdem Sie Ihren Datenfluss überprüft haben, klicken Sie auf **Beenden** und gewähren Sie etwas Zeit für die Erstellung des Datenflusses.

![Der Überprüfungsschritt des Ursprungs-Workflows.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-compelete.png)

## Abrufen der Streaming-Endpunkt-URL {#get-your-streaming-endpoint-url}

Mit dem erstellten Streaming-Datenfluss können Sie jetzt Ihre Streaming-Endpunkt-URL abrufen. Dieser Endpunkt wird zum Abonnieren Ihres Webhooks verwendet, sodass Ihre Streaming-Quelle mit Experience Platform kommunizieren kann.

Um Ihren Streaming-Endpunkt abzurufen, navigieren Sie zum *[!UICONTROL Datenfluss-Aktivität]* Seite des soeben erstellten Datenflusses und kopieren Sie den Endpunkt vom unteren Rand des *[!UICONTROL Eigenschaften]* Bedienfeld.

![Die Seite mit der Datenfluss-Aktivität im Arbeitsbereich &quot;Quellen&quot;, wobei die Streaming-Endpunkt-URL hervorgehoben ist.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-dataflow-api.png)

## Aktivieren Sie Ihr Integrationsprofil in RainFocus

Sobald Ihr Datenfluss abgeschlossen ist und Sie Ihre Streaming-Endpunkt-URL abgerufen haben, können Sie jetzt die [!DNL Integration Profile] in [!DNL RainFocus].

* Anmelden bei der [[!DNL RainFocus] platform](https://app.rainfocus.com). Wählen Sie im primären Navigationsmenü die Option **[!DNL Libraries]** und **[!DNL Integration Profiles]**
* Öffnen Sie die [!DNL Integration Profile] die Sie zuvor als Teil der [Voraussetzungen](../../../../connectors/analytics/rainfocus.md#create-an-integration-profile-in-rainfocus).
* Fügen Sie die **Dataflow-ID** und **Streaming-Endpunkt** aus dem Datenfluss in Experience Platform kopiert wurde, und wählen Sie **Speichern**

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung für Ihre [!DNL RainFocus] -Quelle, mit der Sie Ihre Ereignismanagement- und Analysedaten an Experience Platform streamen können.

## Zusätzliche Ressourcen

Die folgenden Dokumente enthalten zusätzliche Hinweise zu Nuancen in Bezug auf [!DNL RainFocus] -Quelle.

* [RainFocus Help Center](https://help.rainfocus.com/hc/en-us)
* [Erstellen eines Adobe Service-Kontos (JWT) im Adobe Developer Portal](https://developer.adobe.com/developer-console/docs/guides/authentication/ServiceAccountIntegration/)
* [Erstellen eines Schemas in der API](../../../../../xdm/tutorials/create-schema-api.md)
* [Erstellen eines Schemas in der Benutzeroberfläche](../../../../../xdm/tutorials/create-schema-ui.md)
* [Identitätsfelder in der Benutzeroberfläche definieren](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/fields/identity.html)