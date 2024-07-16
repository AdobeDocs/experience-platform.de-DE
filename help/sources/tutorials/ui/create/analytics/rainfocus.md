---
title: Verbinden Ihres RainFocus-Kontos mit Experience Platform über die Benutzeroberfläche
description: Erfahren Sie, wie Sie Ihr RainFocus-Konto über die Benutzeroberfläche mit Experience Platform verbinden.
badge: Beta
exl-id: a349e37e-9f2c-47ff-8360-ccbe578dce27
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '988'
ht-degree: 26%

---

# Verbinden Sie Ihr [!DNL RainFocus]-Konto über die Benutzeroberfläche mit Experience Platform.

>[!NOTE]
>
>Die [!DNL RainFocus]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta-beschrifteten Quellen finden Sie in der [Quellenübersicht](../../../../home.md#terms-and-conditions) .

In diesem Tutorial erfahren Sie, wie Sie Ihr [!DNL RainFocus]-Konto verbinden und Ereignismanagement- und Analysedaten mit Adobe Experience Platform streamen.

>[!IMPORTANT]
>
>Diese Quell-Connector- und Dokumentationsseite wird vom [!DNL RainFocus]-Team erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an clientcare<span>@rainfocus.com oder besuchen Sie das [[!DNL RainFocus] Help Center](https://help.rainfocus.com/hc/en-us)

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

### Voraussetzungen

Bevor Sie Ihr [!DNL RainFocus]-Konto mit dem Experience Platform verbinden können, müssen Sie zunächst die folgenden erforderlichen Aufgaben durchführen:

* [Sammeln erforderlicher Anmeldeinformationen](../../../../connectors/analytics/rainfocus.md#gather-required-credentials)
* [Erstellen eines XDM-Schemas und Definieren des Identitätsfelds](../../../../connectors/analytics/rainfocus.md#create-an-xdm-schema-and-define-the-identity-field)
* [Erstellen eines Integrationsprofils in RainFocus](../../../../connectors/analytics/rainfocus.md#create-an-integration-profile-in-rainfocus)

Nach Abschluss der erforderlichen Einrichtung können Sie mit den unten beschriebenen Schritten fortfahren.

## RainFocus-Konto mit Experience Platform verbinden

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste **[!UICONTROL Quellen]** aus, um auf den Arbeitsbereich &quot;Quellen&quot;zuzugreifen. Die *[!UICONTROL Katalog]* zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie *[!UICONTROL Analytics]* die Option **[!UICONTROL RainFocus Experience]** und klicken Sie dann auf **[!UICONTROL Daten hinzufügen]**.

![Der Quellkatalog auf der Experience Platform-Benutzeroberfläche mit ausgewählter RainFocus-Quelle.](/help/sources/images/tutorials/create/rainfocus/rainfocus_sources-rf.png)

## Daten auswählen

Der Schritt Daten auswählen wird angezeigt und bietet eine Oberfläche zur Auswahl der Daten, die Sie zum Experience Platform mitbringen.

* Der linke Teil der Benutzeroberfläche ist ein Browser, mit dem Sie die verfügbaren Datenströme in Ihrem Konto anzeigen können.
* Im rechten Bereich der Benutzeroberfläche können Sie eine Vorschau von bis zu 100 Zeilen mit Daten aus einer JSON-Datei anzeigen.

Wählen Sie **[!UICONTROL Dateien hochladen]** aus, um eine JSON-Datei von Ihrem lokalen System hochzuladen. Alternativ können Sie die JSON-Datei, die Sie hochladen möchten, per Drag-and-Drop in den Bereich Dateien ziehen und ablegen.

Laden Sie die JSON-Beispielnutzlast hoch, die von **RainFocus** heruntergeladen wurde.

![Der Schritt &quot;Daten auswählen&quot;im Ursprungs-Workflow.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-json-upload.png)

Nach dem Hochladen Ihrer Datei wird die Vorschau-Oberfläche aktualisiert, um eine Vorschau des hochgeladenen Schemas anzuzeigen. Über die Vorschau-Oberfläche können Sie den Inhalt und die Struktur einer Datei überprüfen. Sie können auch das Dienstprogramm &quot;Suchfeld&quot;verwenden, um auf bestimmte Elemente innerhalb Ihres Schemas zuzugreifen.

Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![Der Schritt der Datenvorschau des Ursprungs-Workflows.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-json-preview.png)

## Datenflussdetails

Der Schritt **Datenfluss-Detail** wird angezeigt und bietet Ihnen Optionen zur Verwendung eines vorhandenen Datensatzes oder zur Einrichtung eines neuen Datensatzes für Ihren Datenfluss sowie die Möglichkeit, einen Namen und eine Beschreibung für Ihren Datenfluss anzugeben. In diesem Schritt können Sie auch Einstellungen für die Profilerfassung, Fehlerdiagnose, partielle Erfassung und Warnhinweise konfigurieren.

Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![Der Schritt &quot;Datenfluss-Detail&quot;des Ursprungs-Workflows.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-dataflow-setup.png)

## Zuordnung {#mapping}

Der Schritt &quot;Zuordnung&quot;wird angezeigt und bietet eine Schnittstelle zum Zuordnen der Quellfelder aus Ihrem Quellschema zu den entsprechenden Ziel-XDM-Feldern im Zielschema.

Experience Platform bietet intelligente Empfehlungen für automatisch zugeordnete Felder, die auf dem ausgewählten Zielschema oder Datensatz basieren. Sie können die Zuordnungsregeln manuell an Ihre Anwendungsfälle anpassen. Je nach Bedarf können Sie wahlweise Felder direkt zuordnen oder mithilfe von Datenvorbereitungsfunktionen Quelldaten transformieren, um berechnete oder anderweitig ermittelte Werte abzuleiten. Umfassende Schritte zur Verwendung der Zuordnungsoberfläche und der berechneten Felder finden Sie im Handbuch [Data Prep UI guide](../../../../../data-prep/ui/mapping.md).

Nachdem die Quelldaten erfolgreich zugeordnet wurden, wählen Sie **[!UICONTROL Weiter]** aus.

![Der Zuordnungsschritt des Ursprungs-Workflows.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-mappings.png)

## Überprüfung

Der Schritt **Überprüfung** wird angezeigt, sodass Sie Ihren neuen Datenfluss überprüfen können, bevor er hergestellt wird. Die Details lassen sich wie folgt kategorisieren:

* **Verbindung**: Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quelldatei und die Anzahl der Spalten innerhalb dieser Quelldatei an.
* **Datensatz- und Zuordnungsfelder zuweisen**: Zeigt an, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, dem der Datensatz entspricht.

Nachdem Sie Ihren Datenfluss überprüft haben, klicken Sie auf **Beenden** und gewähren Sie etwas Zeit für die Erstellung des Datenflusses.

![Der Überprüfungsschritt des Ursprungs-Workflows.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-compelete.png)

## Abrufen der Streaming-Endpunkt-URL {#get-your-streaming-endpoint-url}

Mit dem erstellten Streaming-Datenfluss können Sie jetzt Ihre Streaming-Endpunkt-URL abrufen. Dieser Endpunkt wird zum Abonnieren Ihres Webhooks verwendet, sodass Ihre Streaming-Quelle mit Experience Platform kommunizieren kann.

Um Ihren Streaming-Endpunkt abzurufen, rufen Sie die Seite *[!UICONTROL Datenfluss-Aktivität]* des soeben erstellten Datenflusses auf und kopieren Sie den Endpunkt vom unteren Rand des Bereichs *[!UICONTROL Eigenschaften]* .

![Die Seite mit der Datenfluss-Aktivität im Arbeitsbereich &quot;Quellen&quot;, wobei die Streaming-Endpunkt-URL hervorgehoben ist.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-dataflow-api.png)

## Aktivieren Sie Ihr Integrationsprofil in RainFocus

Sobald Ihr Datenfluss abgeschlossen ist und Sie Ihre Streaming-Endpunkt-URL abgerufen haben, können Sie jetzt die [!DNL Integration Profile] in [!DNL RainFocus] aktivieren.

* Melden Sie sich bei [[!DNL RainFocus] platform](https://app.rainfocus.com) an. Wählen Sie im primären Navigationsbereich **[!DNL Libraries]** und **[!DNL Integration Profiles]** aus.
* Öffnen Sie die zuvor als Teil von [Voraussetzungen](../../../../connectors/analytics/rainfocus.md#create-an-integration-profile-in-rainfocus) erstellte [!DNL Integration Profile].
* Fügen Sie die aus dem Datenfluss kopierte **Datenfluss-ID** und den aus dem Datenfluss kopierten **Streaming-Endpunkt** ein und wählen Sie **Speichern** aus.

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung für Ihre [!DNL RainFocus]-Quelle hergestellt, über die Sie Ihre Ereignismanagement- und Analysedaten an Experience Platform streamen können.

## Zusätzliche Ressourcen

Die folgenden Dokumente enthalten zusätzliche Anleitungen zu den Nuancen rund um die [!DNL RainFocus]-Quelle.

* [RainFocus Help Center](https://help.rainfocus.com/hc/en-us)
* [Erstellen eines Adobe Service-Kontos (JWT) im Adobe Developer Portal](https://developer.adobe.com/developer-console/docs/guides/authentication/ServiceAccountIntegration/)
* [Erstellen eines Schemas in der API](../../../../../xdm/tutorials/create-schema-api.md)
* [Erstellen eines Schemas in der Benutzeroberfläche](../../../../../xdm/tutorials/create-schema-ui.md)
* [Identitätsfelder in der Benutzeroberfläche definieren](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/fields/identity.html)
