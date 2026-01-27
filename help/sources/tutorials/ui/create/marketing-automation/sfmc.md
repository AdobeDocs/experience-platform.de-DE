---
title: Verbinden Ihres Salesforce Marketing Cloud (v2)-Kontos mit Experience Platform über die Benutzeroberfläche
description: Erfahren Sie, wie Sie Ihr Salesforce Marketing Cloud (V2)-Konto über die Benutzeroberfläche mit Experience Platform verbinden.
source-git-commit: 91bf8bf6e6f7030574d693484ce9797800c2d5dd
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 10%

---

# Verbinden von [!DNL Salesforce Marketing Cloud] mit Experience Platform

Lesen Sie dieses Handbuch, um zu erfahren, wie Sie Ihr [!DNL Salesforce Marketing Cloud]-Konto mithilfe des Arbeitsbereichs „Quellen“ in der Benutzeroberfläche von Experience Platform mit Adobe Experience Platform verbinden.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

### Sammeln erforderlicher Anmeldedaten

Informationen zur Authentifizierung [[!DNL Salesforce Marketing Cloud]  Sie in &#x200B;](../../../../connectors/marketing-automation/sfmc.md#prerequisites)Übersicht“.

## Navigieren im Quellkatalog

Wählen Sie in der Benutzeroberfläche von Experience Platform in der linken Navigationsleiste die Option **[!UICONTROL Sources]** , um auf den *[!UICONTROL Sources]*-Arbeitsbereich zuzugreifen. Wählen Sie eine Kategorie aus oder verwenden Sie die Suchleiste, um Ihre Quelle zu finden.

Um eine Verbindung zu [!DNL Salesforce Marketing Cloud] herzustellen, navigieren Sie zur Kategorie *[!UICONTROL Marketing Automation]*, wählen Sie die Karte **[!UICONTROL (V2) Salesforce Marketing Cloud]** und dann **[!UICONTROL Set up]** aus.

>[!TIP]
>
>Quellen im Quellkatalog zeigen die **[!UICONTROL Set up]** an, wenn eine bestimmte Quelle noch kein authentifiziertes Konto hat. Nachdem ein authentifiziertes Konto erstellt wurde, ändert sich diese Option in **[!UICONTROL Add data]**.

![Der Quellkatalog, wobei die Salesforce Marketing Cloud-Quelle ausgewählt wurde.](../../../../images/tutorials/create/sfmc/catalog.png)

## Vorhandenes Konto verwenden {#existing}

Um ein vorhandenes Konto zu verwenden, klicken Sie auf **[!UICONTROL Existing account]** und wählen Sie dann das [!DNL Salesforce Marketing Cloud] Konto aus, das Sie verwenden möchten.

![Die vorhandene Kontoschnittstelle des Quell-Workflows](../../../../images/tutorials/create/sfmc/existing.png)

## Neues Konto erstellen {#new}

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL New account]** aus und geben Sie einen Namen und eine Beschreibung unter Ihrem [!UICONTROL Source connection details] an. Geben Sie als Nächstes unter [!UICONTROL Account authentication] Werte für Ihren **Client-ID**, **Client-Geheimnis** und **Basis-Endpunkt** an. Weitere Informationen zu diesen Anmeldeinformationen finden [&#x200B; im &#x200B;](../../../../connectors/marketing-automation/sfmc.md#gather-required-credentials) zur Authentifizierung . Wenn Sie fertig sind, wählen Sie **[!UICONTROL Connect to source]** aus und warten Sie einige Sekunden, bis Ihre Verbindung hergestellt ist.

![Die neue Kontoschnittstelle des Quell-Workflows.](../../../../images/tutorials/create/sfmc/new.png)

## Daten auswählen

Die [!DNL Salesforce Marketing Cloud]-Quelle unterstützt die Datenaufnahme nur aus [!DNL Salesforce Marketing Cloud] Datenerweiterungen.

Verwenden Sie die [!UICONTROL Select data], um die Datenerweiterung auszuwählen, die Sie aus Ihrer [!DNL Salesforce Marketing Cloud]-Instanz aufnehmen möchten. Nachdem Sie die Datenerweiterung ausgewählt haben, können Sie im Bedienfeld Vorschau überprüfen, ob der Datensatz die erwarteten Felder enthält, bevor Sie fortfahren.

![Der Schritt „Daten auswählen“ des Quell-Workflows](../../../../images/tutorials/create/sfmc/select-data.png)

## Datensatz- und Datenflussdetails

Als Nächstes müssen Sie Informationen zu Ihrem Datensatz und Datenfluss angeben. In diesem Schritt können Sie entweder einen vorhandenen Datensatz verwenden oder einen neuen Datensatz erstellen. Darüber hinaus können Sie in diesem Schritt optional Ihren Datensatz für die Aufnahme in das Echtzeit-Kundenprofil aktivieren.

![Der Schritt „Datensatz- und Datenflussdetails“ des Quell-Workflows.](../../../../images/tutorials/create/sfmc/dataset-details.png)

## Zuordnung

[!DNL Salesforce Marketing Cloud] werden Datenerweiterungen nicht als Standardobjekte betrachtet. Daher gibt es keine vordefinierten oder festen Zuordnungsfelder zu einem Experience Platform-Schema. Während die Datenvorbereitung in Experience Platform eine bestmögliche Abstimmung zwischen Quellfeldern aus [!DNL Salesforce Marketing Cloud] und dem Ziel-Experience-Datenmodell (XDM)-Schema durchführt, kann es dennoch einige Fälle geben, in denen eine manuelle Überprüfung oder Anpassung erforderlich ist, um nicht zugeordnete oder fehlerhafte Felder aufzulösen.

![Der Zuordnungsschritt des Quell-Workflows.](../../../../images/tutorials/create/sfmc/mapping.png)

## Planen eines Datenflusses

Nach Abschluss der Zuordnung können Sie jetzt einen Aufnahmezeitplan für Ihren Datenfluss konfigurieren. Legen Sie Ihre [!UICONTROL Frequency] auf `Once` fest, um einen einmaligen Aufnahmevorgang zu konfigurieren. Für die inkrementelle Aufnahme können Sie Ihre [!UICONTROL Frequency] auf `Hour`, `Day` oder `Week` festlegen. Bei Verwendung der inkrementellen Aufnahme müssen Sie auch den [!UICONTROL Interval] konfigurieren, um die Zeit zu definieren, die zwischen der Aufnahme vergeht. Wenn beispielsweise die Aufnahmefrequenz auf `Day` und das Intervall auf `15` festgelegt ist, bedeutet dies, dass der Datenfluss alle 15 Tage Daten aufnehmen soll.

>[!TIP]
>
> Die Aufnahmefrequenz pro Minute ist für die [!DNL Salesforce Marketing Cloud] nicht verfügbar. Der häufigste Zeitplan, den Sie auswählen können, ist stündlich. Wählen Sie einen Zeitplan aus, der Ihren Anforderungen an die Datenaktualität entspricht. Beachten Sie, dass die Auswahl eines häufigeren Zeitplans die Rechenkosten erhöht.

Sie müssen ein Delta-Feld (Datum/Uhrzeit) in Ihrem Datensatz auswählen, um die inkrementelle Synchronisierung zu aktivieren. Wenn Ihr Datensatz kein geeignetes Delta-Feld enthält, können Sie den Datenfluss nicht erstellen.

![Der Planungsschritt des Quell-Workflows.](../../../../images/tutorials/create/sfmc/schedule.png)

## Überprüfung

Verwenden Sie nach der Konfiguration des Aufnahmezeitplans die [!UICONTROL Review], um die Details Ihres Datenflusses zu bestätigen. Wählen Sie **[!UICONTROL Finish]** aus, um die Einrichtung abzuschließen, und warten Sie einige Augenblicke, bis Ihr Datenfluss gestartet ist.

![Der Überprüfungsschritt des Quell-Workflows.](../../../../images/tutorials/create/sfmc/review.png)

## Überwachen

Sobald der Datenfluss ausgewählt ist, wird eine einmalige Aufstockung der Daten und anschließend eine inkrementelle Synchronisierung gemäß dem angegebenen Zeitplan durchgeführt. Der Status der Synchronisierung kann überwacht werden, indem zum Datenfluss navigiert wird. Weitere Informationen finden Sie im Handbuch unter [Überwachen von Quelldatenflüssen in der Benutzeroberfläche](../../../../../dataflows/ui/monitor-sources.md).

## Nächste Schritte

In diesem Tutorial erfahren Sie, wie Sie Ihr [!DNL Salesforce Marketing Cloud] (V2)-Konto mithilfe der Benutzeroberfläche mit Experience Platform verbinden. Sie haben gelernt, wie Sie ein Quellkonto auswählen oder erstellen, die erforderlichen Anmeldeinformationen bereitstellen, Datenerweiterungen für die Aufnahme auswählen, Datensatz- und Datenflussdetails angeben, Ihre Daten zuordnen, einen Zeitplan für die Datenaufnahme einrichten und Ihre Datenflüsse überwachen. Mithilfe dieser Schritte haben Sie Ihre [!DNL Salesforce Marketing Cloud] erfolgreich in Experience Platform integriert, um sie zu aktivieren und zu analysieren.

Weitere Informationen finden Sie in der folgenden Dokumentation:

* [Quellen – Übersicht](../../../../home.md)
* [Real-Time CDP B2B Edition](../../../../../rtcdp/b2b-overview.md)

