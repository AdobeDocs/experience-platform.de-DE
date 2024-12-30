---
title: Verbinden Ihres RainFocus-Kontos mit dem Experience Platform über die Benutzeroberfläche
description: Erfahren Sie, wie Sie Ihr RainFocus-Konto über die Benutzeroberfläche mit dem Experience Platform verbinden.
badge: Beta
exl-id: a349e37e-9f2c-47ff-8360-ccbe578dce27
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '988'
ht-degree: 26%

---

# Verbinden Ihres [!DNL RainFocus]-Kontos mit dem Experience Platform über die Benutzeroberfläche

>[!NOTE]
>
>Die [!DNL RainFocus]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta[gekennzeichneten Quellen finden Sie ](../../../../home.md#terms-and-conditions) „Quellen - Übersicht“ .

In diesem Tutorial erfahren Sie, wie Sie Ihr [!DNL RainFocus]-Konto verbinden und Ereignisverwaltungs- und Analysedaten mit Adobe Experience Platform streamen.

>[!IMPORTANT]
>
>Dieser Quell-Connector und diese Dokumentationsseite werden vom [!DNL RainFocus]-Team erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an clientcare<span>@rainfocus.com oder besuchen Sie das [[!DNL RainFocus] Hilfezentrum](https://help.rainfocus.com/hc/en-us)

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

### Voraussetzungen

Bevor Sie Ihr [!DNL RainFocus]-Konto mit Experience Platform verbinden können, müssen Sie zunächst die folgenden erforderlichen Aufgaben ausführen:

* [Sammeln erforderlicher Anmeldedaten](../../../../connectors/analytics/rainfocus.md#gather-required-credentials)
* [Erstellen eines XDM-Schemas und Definieren des Identitätsfelds](../../../../connectors/analytics/rainfocus.md#create-an-xdm-schema-and-define-the-identity-field)
* [Erstellen eines Integrationsprofils in RainFocus](../../../../connectors/analytics/rainfocus.md#create-an-integration-profile-in-rainfocus)

Nachdem Sie die erforderliche Einrichtung abgeschlossen haben, können Sie mit den unten beschriebenen Schritten fortfahren.

## RainFocus-Konto mit Experience Platform verbinden

Wählen Sie in der Platform-Benutzeroberfläche **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich „Quellen“ zuzugreifen. Die *[!UICONTROL Katalog]* zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter *[!UICONTROL Kategorie]* die Option **[!UICONTROL RainFocus Experience]** und dann **[!UICONTROL Daten hinzufügen]**.

![Der Quellkatalog auf der Experience Platform-Benutzeroberfläche mit der ausgewählten RainFocus-Quelle.](/help/sources/images/tutorials/create/rainfocus/rainfocus_sources-rf.png)

## Daten auswählen

Der Schritt Daten auswählen wird angezeigt und bietet Ihnen eine Schnittstelle zur Auswahl der Daten, die Sie zum Experience Platform bringen.

* Der linke Teil der Benutzeroberfläche ist ein Browser, mit dem Sie die verfügbaren Datenströme in Ihrem Konto anzeigen können.
* Im rechten Teil der Benutzeroberfläche können Sie eine Vorschau von bis zu 100 Datenzeilen aus einer JSON-Datei anzeigen.

Wählen Sie **[!UICONTROL Dateien hochladen]** aus, um eine JSON-Datei von Ihrem lokalen System hochzuladen. Alternativ können Sie die JSON-Datei, die Sie hochladen möchten, per Drag-and-Drop in das Bedienfeld Dateien per Drag-and-Drop ziehen.

Laden Sie die JSON-Beispiel-Payload hoch, die von **RainFocus) heruntergeladen**.

![Der Schritt „Daten auswählen“ im Quellen-Workflow.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-json-upload.png)

Nachdem Ihre Datei hochgeladen wurde, wird die Vorschau-Oberfläche aktualisiert, um eine Vorschau des hochgeladenen Schemas anzuzeigen. In der Vorschauoberfläche können Sie den Inhalt und die Struktur einer Datei überprüfen. Sie können auch das Dienstprogramm für die Suche verwenden, um auf bestimmte Elemente in Ihrem Schema zuzugreifen.

Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![Der Datenvorschau-Schritt des Quell-Workflows.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-json-preview.png)

## Datenflussdetails

Der Schritt **Datenflussdetails** wird angezeigt und bietet Ihnen Optionen zum Verwenden eines vorhandenen Datensatzes oder zum Einrichten eines neuen Datensatzes für Ihren Datenfluss sowie die Möglichkeit, einen Namen und eine Beschreibung für Ihren Datenfluss anzugeben. In diesem Schritt können Sie auch Einstellungen für die Profilaufnahme, Fehlerdiagnose, partielle Aufnahme und Warnhinweise konfigurieren.

Wenn Sie fertig sind, klicken Sie auf die Schaltfläche **[!UICONTROL Weiter]**.

![Der Schritt „Datenflussdetails“ des Quell-Workflows.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-dataflow-setup.png)

## Zuordnung {#mapping}

Der Schritt Zuordnung wird angezeigt und bietet Ihnen eine Schnittstelle zum Zuordnen der Quellfelder aus Ihrem Quellschema zu den entsprechenden XDM-Zielfeldern im Zielschema.

Experience Platform bietet intelligente Empfehlungen für automatisch zugeordnete Felder, die auf dem ausgewählten Zielschema oder Datensatz basieren. Sie können die Zuordnungsregeln manuell an Ihre Anwendungsfälle anpassen. Je nach Bedarf können Sie wahlweise Felder direkt zuordnen oder mithilfe von Datenvorbereitungsfunktionen Quelldaten transformieren, um berechnete oder anderweitig ermittelte Werte abzuleiten. Eine ausführliche Anleitung zur Verwendung der Zuordnungsschnittstelle und berechneter Felder finden Sie im [Handbuch zur Datenvorbereitungs-Benutzeroberfläche](../../../../../data-prep/ui/mapping.md).

Nachdem Ihre Quelldaten erfolgreich zugeordnet wurden, klicken Sie auf **[!UICONTROL Weiter]**.

![Der Zuordnungsschritt des Quell-Workflows.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-mappings.png)

## Überprüfung

Der Schritt **Überprüfung** wird angezeigt, sodass Sie Ihren neuen Datenfluss überprüfen können, bevor er hergestellt wird. Die Details lassen sich wie folgt kategorisieren:

* **Verbindung**: Zeigt den Quelltyp, den relevanten Pfad der ausgewählten Quelldatei und die Anzahl der Spalten innerhalb dieser Quelldatei an.
* **Datensatz- und Zuordnungsfelder zuweisen**: Zeigt an, in welchen Datensatz die Quelldaten aufgenommen werden, einschließlich des Schemas, dem der Datensatz entspricht.

Nachdem Sie Ihren Datenfluss überprüft haben, klicken Sie auf **Beenden** und gewähren Sie etwas Zeit für die Erstellung des Datenflusses.

![Der Überprüfungsschritt des Quell-Workflows.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-compelete.png)

## Abrufen der Streaming-Endpunkt-URL {#get-your-streaming-endpoint-url}

Nachdem Sie Ihren Streaming-Datenfluss erstellt haben, können Sie jetzt Ihre Streaming-Endpunkt-URL abrufen. Dieser Endpunkt wird verwendet, um Ihren Webhook zu abonnieren, sodass Ihre Streaming-Quelle mit Experience Platform kommunizieren kann.

Um Ihren Streaming-Endpunkt abzurufen, gehen Sie zur Seite *[!UICONTROL Datenflussaktivität]* des soeben erstellten Datenflusses und kopieren Sie den Endpunkt am unteren Rand des Bedienfelds *[!UICONTROL Eigenschaften]*.

![Die Seite mit der Datenflussaktivität im Quellarbeitsbereich, wobei die Streaming-Endpunkt-URL hervorgehoben ist.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-dataflow-api.png)

## Aktivieren des Integrationsprofils in RainFocus

Sobald Ihr Datenfluss abgeschlossen ist und Sie Ihre Streaming-Endpunkt-URL abgerufen haben, können Sie die [!DNL Integration Profile] in [!DNL RainFocus] aktivieren.

* Melden Sie sich bei [[!DNL RainFocus] Plattform](https://app.rainfocus.com) an. Wählen Sie in der primären Navigation **[!DNL Libraries]** und **[!DNL Integration Profiles]** aus
* Öffnen Sie die [!DNL Integration Profile], die Sie zuvor im Rahmen der [Voraussetzungen](../../../../connectors/analytics/rainfocus.md#create-an-integration-profile-in-rainfocus) erstellt haben.
* Fügen Sie die **Datenfluss-ID** und **Streaming-Endpunkt** aus dem Datenfluss in Experience Platform ein und wählen Sie **Speichern**

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung für Ihre [!DNL RainFocus] hergestellt, sodass Sie Ihre Ereignis-Management- und Analysedaten auf Experience Platform streamen können.

## Zusätzliche Ressourcen

Die folgenden Dokumente bieten zusätzliche Anleitungen zu den Nuancen im Zusammenhang mit der [!DNL RainFocus].

* [RainFocus Hilfezentrum](https://help.rainfocus.com/hc/en-us)
* [Erstellen eines Adobe Service-Kontos (JWT) im Adobe Developer-Portal](https://developer.adobe.com/developer-console/docs/guides/authentication/ServiceAccountIntegration/)
* [Erstellen eines Schemas in der API](../../../../../xdm/tutorials/create-schema-api.md)
* [Erstellen eines Schemas in der Benutzeroberfläche](../../../../../xdm/tutorials/create-schema-ui.md)
* [Definieren von Identitätsfeldern in der Benutzeroberfläche](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/fields/identity.html)
