---
title: Erstellen einer Google BigQuery Source-Verbindung über die Benutzeroberfläche
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Google BigQuery-Quellverbindung erstellen.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 3c0902de-48b9-42d8-a4bd-0213ca85fc7f
source-git-commit: ae322ee421edd73cd5a3fb8499267cd417491318
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 33%

---

# Erstellen eines Quell-Connectors für [!DNL Google BigQuery] in der Benutzeroberfläche

>[!IMPORTANT]
>
>Die [!DNL Google BigQuery] ist im Quellkatalog für Benutzende verfügbar, die Real-time Customer Data Platform Ultimate erworben haben.

Lesen Sie dieses Tutorial, um zu erfahren, wie Sie Ihr [!DNL Google BigQuery]-Konto über die Benutzeroberfläche mit Adobe Experience Platform verbinden.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL Google BigQuery]-Verbindung verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Konfigurieren eines Datenflusses](../../dataflow/databases.md) fortfahren.

### Sammeln erforderlicher Anmeldedaten

Ausführliche Schritte zum Sammeln [[!DNL Google BigQuery]  erforderlichen Anmeldeinformationen finden Sie ](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials) Authentifizierungshandbuch .

## Verbinden Ihres Google BigQuery-Kontos

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste die Option **[!UICONTROL Quellen]**, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können. Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchleiste finden.

Wählen Sie unter [!UICONTROL  Kategorie ] die Option **[!UICONTROL Google BigQuery]** und dann **[!UICONTROL Daten hinzufügen]**.

>[!TIP]
>
>Quellen im Quellkatalog zeigen die Option **[!UICONTROL Einrichten]** an, wenn eine bestimmte Quelle noch kein authentifiziertes Konto hat. Sobald ein authentifiziertes Konto vorhanden ist, ändert sich diese Option in **[!UICONTROL Daten hinzufügen]**.

![Der Quellkatalog mit ausgewählter Google BigQuery.](../../../../images/tutorials/create/google-big-query/catalog.png)

Die **[!UICONTROL „Mit Google Big Query verbinden]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das [!DNL Google BigQuery] Konto, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![Die Seite mit dem vorhandenen Konto, auf der eine Liste der vorhandenen Konten angezeigt wird.](../../../../images/tutorials/create/google-big-query/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen und eine optionale Beschreibung für Ihr neues [!DNL Google BigQuery]-Konto an.

![Die neue Kontoschnittstelle im Quell-Workflow.](../../../../images/tutorials/create/google-big-query/new.png)

>[!BEGINTABS]

>[!TAB Einfache Authentifizierung verwenden]

Um die Standardauthentifizierung zu verwenden, wählen Sie **[!UICONTROL Standardauthentifizierung]** aus und geben Sie Werte für Ihr [Projekt, Ihre Client-ID, Ihr Client-Geheimnis, Ihr Aktualisierungs-Token und (optional) die Datensatz-ID für große Ergebnisse](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials) an. Wenn Sie fertig sind, wählen **[!UICONTROL Mit Quelle verbinden]** und warten Sie einige Augenblicke, bis die Verbindung hergestellt ist.

![Die neue Kontoschnittstelle, in der die Standardauthentifizierung ausgewählt ist.](../../../../images/tutorials/create/google-big-query/basic_auth.png)

>[!TAB Service-Authentifizierung verwenden]

Um die Service-Authentifizierung zu verwenden **[!UICONTROL wählen Sie]** Service-Authentifizierung“ aus und geben Sie Werte für Ihre [Projekt-ID, den Inhalt der Schlüsseldatei und (optional) die Datensatz-ID für große Ergebnisse](../../../../connectors/databases/bigquery.md#generate-your-google-bigquery-credentials) an. Wenn Sie fertig sind, wählen **[!UICONTROL Mit Quelle verbinden]** und warten Sie einige Augenblicke, bis die Verbindung hergestellt ist.

![Die neue Kontoschnittstelle, in der die Service-Authentifizierung ausgewählt ist.](../../../../images/tutorials/create/google-big-query/service_auth.png)

>[!ENDTABS]

### Vorschau der Beispieldaten überspringen {#skip-preview-of-sample-data}

Während des Datenauswahlschritts kann es bei der Aufnahme großer Datentabellen oder -dateien zu einer Zeitüberschreitung kommen. Sie können die Datenvorschau überspringen, um die Zeitüberschreitung zu umgehen, und Ihr Schema dennoch anzeigen, wenn auch ohne Beispieldaten. Um die Datenvorschau zu überspringen, aktivieren Sie den Umschalter **[!UICONTROL Vorschau von Beispieldaten überspringen]**.

Der Rest des Workflows bleibt unverändert. Der einzige Nachteil besteht darin, dass das Überspringen der Datenvorschau verhindert, dass berechnete und erforderliche Felder während des Zuordnungsschritts automatisch validiert werden. Diese Felder müssen dann während der Zuordnung manuell validiert werden.

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL Google BigQuery]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und einen [Datenfluss konfigurieren, um Daten in Platform zu importieren](../../dataflow/databases.md).
