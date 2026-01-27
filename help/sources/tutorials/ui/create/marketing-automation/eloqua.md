---
title: Verbinden von Oracle Eloqua (V2) mit Experience Platform über die Benutzeroberfläche
description: Erfahren Sie, wie Sie in der Benutzeroberfläche Ihr Oracle Eloqua-Konto mit Experience Platform verbinden.
source-git-commit: 180754969d4ae8dbd1308dfc85dae73baf64f759
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 7%

---

# Verbinden von [!DNL Oracle Eloqua] (V2) mit Experience Platform über die Benutzeroberfläche

Mit dem [!DNL Oracle Eloqua (V2)]-Quell-Connector können Sie Ihr Oracle Eloqua-Konto mit Adobe Experience Platform verbinden, sodass wichtige B2B-Marketing-Daten, einschließlich Kontakten, Konten, Kampagnen und Interaktionsaktivitäten, automatisiert und skalierbar aufgenommen werden können.

Verwenden Sie diesen Quell-Connector, um eine sichere Authentifizierung zu konfigurieren, die benötigten Eloqua-Datenentitäten auszuwählen und sie standardisierten XDM-Schemata (Experience-Datenmodell) zuzuordnen. Flexible Zeitplanoptionen ermöglichen es Ihnen, sowohl anfängliche Datenladevorgänge als auch wiederkehrende, inkrementelle Synchronisierungen einzurichten, um sicherzustellen, dass Ihre Marketing-Daten aktuell und verwertbar bleiben.

Der [!DNL Oracle Eloqua (V2)]-Quell-Connector basiert auf dem Enterprise Ingestion Framework von Adobe und bietet eine zuverlässige, erweiterbare Grundlage für die Kampagnenoptimierung, Leistungsmessung und kanalübergreifende Personalisierung.

Lesen Sie dieses Handbuch, um zu erfahren, wie Sie Ihr [!DNL Oracle Eloqua]-Konto mithilfe des Arbeitsbereichs „Quellen“ in der Benutzeroberfläche von Experience Platform mit Adobe Experience Platform verbinden.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

### Sammeln erforderlicher Anmeldedaten {#credentials}

Informationen zur Authentifizierung [[!DNL Eloqua]  Sie in &#x200B;](../../../../connectors/marketing-automation/eloqua.md)Übersicht“.

## Navigieren im Quellkatalog {#catalog}

Wählen Sie in der Benutzeroberfläche von Experience Platform in der linken Navigationsleiste die Option **[!UICONTROL Sources]** , um auf den *[!UICONTROL Sources]*-Arbeitsbereich zuzugreifen. Wählen Sie eine Kategorie aus oder verwenden Sie die Suchleiste, um Ihre Quelle zu finden.

Um eine Verbindung zu [!DNL Eloqua] herzustellen, navigieren Sie zur Kategorie *[!UICONTROL Marketing Automation]*, wählen Sie die Karte **[!UICONTROL (V2) Oracle Eloqua]** und dann **[!UICONTROL Set up]** aus.

>[!TIP]
>
>Quellen im Quellkatalog zeigen die **[!UICONTROL Set up]** an, wenn eine bestimmte Quelle noch kein authentifiziertes Konto hat. Nachdem ein authentifiziertes Konto erstellt wurde, ändert sich diese Option in **[!UICONTROL Add data]**.

![Die Eloqua-Quellkarte im Quellkatalog mit der hervorgehobenen Schaltfläche „Einrichten“.](../../../../images/tutorials/create/eloqua/catalog.png)

## Vorhandenes Konto verwenden {#existing}

Um ein vorhandenes Konto zu verwenden, klicken Sie auf **[!UICONTROL Existing account]** und wählen Sie dann das [!DNL Eloqua] Konto aus, das Sie verwenden möchten.

![Die Option „Vorhandenes Konto“, die in der Benutzeroberfläche zur Kontoerstellung ausgewählt wurde.](../../../../images/tutorials/create/eloqua/existing.png)

## Neues Konto erstellen {#new}

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL New account]** aus und geben Sie einen Namen und eine Beschreibung unter Ihrem [!UICONTROL Source connection details] an. Geben Sie als Nächstes unter [!UICONTROL Account authentication] Werte für Ihre **Client-ID**, **Client-Geheimnis**, **Benutzername**, **Kennwort** und **Basisendpunkt** an. Weitere Informationen zu diesen Anmeldeinformationen finden [&#x200B; im &#x200B;](../../../../connectors/marketing-automation/eloqua.md) zur Authentifizierung . Wenn Sie fertig sind, wählen Sie **[!UICONTROL Connect to source]** aus und warten Sie einige Sekunden, bis Ihre Verbindung hergestellt ist.

![Die neue Kontoschnittstelle mit Feldern für Details zur Quellverbindung und Authentifizierungsberechtigungen.](../../../../images/tutorials/create/eloqua/new.png)

## Daten auswählen

Verwenden Sie die Datenschnittstelle auswählen , um die [!DNL Eloqua]-Entität auszuwählen, die Sie in Experience Platform aufnehmen möchten.

>[!TIP]
>
>Bei der Auswahl von Daten werden Sie feststellen, dass die anderen Entitäten mit Ausnahme von Kampagnen repräsentative Beispieldaten anzeigen. Dieser Ansatz stellt sicher, dass Sie eine Vorschau der verfügbaren Felder und Strukturen anzeigen können, da [!DNL Eloqua] öffentlichen APIs derzeit nur echte Daten für Kampagnen abrufen. Für die übrigen Entitäten werden Beispieldaten zur Unterstützung Ihres Konfigurations-Workflows bereitgestellt.

![Die Datenauswahlschnittstelle mit den verfügbaren Eloqua-Datenentitäten.](../../../../images/tutorials/create/eloqua/select-data.png)

## Datensatz- und Datenflussdetails {#details}

Als Nächstes müssen Sie Informationen zu Ihrem Datensatz und Datenfluss angeben. In diesem Schritt können Sie entweder einen vorhandenen Datensatz verwenden oder einen neuen Datensatz erstellen. Darüber hinaus können Sie in diesem Schritt optional Ihren Datensatz für die Aufnahme in das Echtzeit-Kundenprofil aktivieren.

![Die Benutzeroberfläche mit Details zu Datensätzen und Datenflüssen mit Optionen zum Konfigurieren von Datensatzeigenschaften.](../../../../images/tutorials/create/eloqua/details.png)

## Zuordnung {#mapping}

Zuordnungen für [!DNL Eloqua] sind in vier Hauptentitätstypen unterteilt:

* **Konten** - Firmen-/Organisationsdatensätze aus [!DNL Eloqua].
* **Aktivitäten** - Marketing-Aktivitäten und Interaktionsereignisse aus [!DNL Eloqua].
* **Kampagnen** - Datensätze von Marketing-Kampagnen aus [!DNL Eloqua].
* **Kontakte** - Einträge einzelner Personen aus [!DNL Eloqua].

Wenn Sie Zugriff auf zusätzliche Felder benötigen, die über die standardmäßig bereitgestellten hinausgehen, können Sie diese Felder mithilfe des Prozesses Datenvorbereitung und Zuordnung in Experience Platform hinzufügen. Wenn das Standardschema einige Ihrer erforderlichen Felder nicht unterstützt, haben Sie die Möglichkeit, ein benutzerdefiniertes Schema in Experience Platform zu definieren. Verwenden Sie diese Funktion, um die erforderlichen Felder zu erstellen und zuzuordnen, damit Sie alle relevanten Daten aus [!DNL Eloqua] nahtlos in Experience Platform aufnehmen können.

Zusammenfassung der nächsten Schritte:

* Überprüfen Sie die standardmäßig zugeordneten Felder, die mit der -Integration verfügbar sind.
* Fügen Sie während des Zuordnungsschritts alle zusätzlichen Felder hinzu, die von [!DNL Eloqua] benötigt werden.
* Wenn neue Felder im Standardschema nicht vorhanden sind, erweitern oder erstellen Sie ein benutzerdefiniertes Schema in Experience Platform, das diese Felder enthält.
* Schließen Sie die Zuordnung ab, um sicherzustellen, dass alle gewünschten Daten aufgenommen werden.

Um sicherzustellen, dass Ihre externen CRM-Informationen korrekt wiedergegeben werden, verwenden Sie einfach die Funktion für berechnete Felder in der Datenvorbereitung, um den `{CRM_INSTANCE_ID}`-Platzhalter mit Ihrer spezifischen CRM-Instanz-ID im Quelldatenfeld zu aktualisieren. Dadurch erhalten Sie die Flexibilität, die Integration an die individuelle Einrichtung Ihres Unternehmens anzupassen.

Um den Editor für berechnete Felder zu verwenden, wählen Sie das Quellfeld aus, das Sie aktualisieren möchten.

![Das Eloqua-Quellfeld mit berechneten Feldern.](../../../../images/tutorials/create/eloqua/select-calculated-field.png)

>[!BEGINTABS]

>[!TAB Salesforce]

Verwenden Sie für [!DNL Salesforce] Benutzer den Editor für berechnete Felder und aktualisieren Sie die `{CRM_INSTANCE_ID}` mit der entsprechenden Instanz-ID.

![Das berechnete Feld für Salesforce.](../../../../images/tutorials/create/eloqua/sf-field.png)

>[!TAB Microsoft Dynamics]

Verwenden Sie für [!DNL Microsoft] Benutzer den Editor für berechnete Felder und aktualisieren Sie die `{CRM_INSTANCE_ID}` mit der entsprechenden Instanz-ID.

![Das berechnete Feld für Dynamics.](../../../../images/tutorials/create/eloqua/dynamics-field.png)

>[!ENDTABS]

Nachdem Sie die berechneten Felder aktualisiert haben, wählen Sie **[!UICONTROL Next]** aus, um fortzufahren.

![Die Zuordnungsschnittstelle mit Feldzuordnungen für Eloqua-Datenentitäten.](../../../../images/tutorials/create/eloqua/mapping.png)

## Planung

>[!NOTE]
>
>Im Folgenden finden Sie die Delta-Felder, die intern für das inkrementelle Laden von Daten verwendet werden:
>
>* **Kontakte:** `C_DateModified`
>* **Konten:** `M_DateModified`
>* **Aktivität:** `CreatedAt`
>* **Benutzerdefinierte Objekte:** `UpdatedAt`
>* **Kampagne:** `updatedAt`

Nach Abschluss der Zuordnung können Sie jetzt einen Aufnahmezeitplan für Ihren Datenfluss konfigurieren. Legen Sie Ihre [!UICONTROL Frequency] auf `Once` fest, um einen einmaligen Aufnahmevorgang zu konfigurieren. Für die inkrementelle Aufnahme können Sie Ihre [!UICONTROL Frequency] auf `Hour`, `Day` oder `Week` festlegen. Bei Verwendung der inkrementellen Aufnahme müssen Sie auch den [!UICONTROL Interval] konfigurieren, um die Zeit zu definieren, die zwischen der Aufnahme vergeht. Wenn beispielsweise die Aufnahmefrequenz auf `Day` und das Intervall auf `15` festgelegt ist, bedeutet dies, dass der Datenfluss alle 15 Tage Daten aufnehmen soll.

Die Aufnahmefrequenz pro Minute ist für die [!DNL Eloqua] nicht verfügbar. Der häufigste Zeitplan, den Sie auswählen können, ist stündlich. Wählen Sie einen Zeitplan aus, der Ihren Anforderungen an die Datenaktualität entspricht. Beachten Sie, dass die Auswahl eines häufigeren Zeitplans die Rechenkosten erhöht.

![Die Planungsschnittstelle mit Optionen zum Konfigurieren der Aufnahmefrequenz und des Intervalls.](../../../../images/tutorials/create/eloqua/scheduling.png)

## Überprüfung

Verwenden Sie nach der Konfiguration des Aufnahmezeitplans die [!UICONTROL Review], um die Details Ihres Datenflusses zu bestätigen. Wählen Sie **[!UICONTROL Finish]** aus, um die Einrichtung abzuschließen, und warten Sie einige Augenblicke, bis Ihr Datenfluss gestartet ist.

![Die Überprüfungsschnittstelle mit einer Zusammenfassung der Datenflusskonfiguration vor Abschluss.](../../../../images/tutorials/create/eloqua/review.png)

## Überwachen

Sobald der Datenfluss ausgewählt ist, wird eine einmalige Aufstockung der Daten und anschließend eine inkrementelle Synchronisierung gemäß dem angegebenen Zeitplan durchgeführt. Der Status der Synchronisierung kann überwacht werden, indem zum Datenfluss navigiert wird. Weitere Informationen finden Sie im Handbuch unter [Überwachen von Quelldatenflüssen in der Benutzeroberfläche](../../../../../dataflows/ui/monitor-sources.md).

## Nächste Schritte

Sie haben jetzt die Einrichtung und Konfiguration Ihrer [!DNL Eloqua] in Experience Platform abgeschlossen. Wenn Ihr Datenfluss eingerichtet ist, werden Ihre [!DNL Eloqua] Daten gemäß Ihrem ausgewählten Zeitplan aufgenommen und Standard-Experience-Datenmodell (XDM)-Schemata zugeordnet. Fahren Sie mit der Überwachung Ihrer Datenflüsse fort und untersuchen Sie Ihre aufgenommenen Daten in Platform, um Erkenntnisse zu gewinnen und Ihre Marketing-Anwendungsfälle zu aktivieren. Weitere Informationen zu erweiterten Konfigurationen und zur Fehlerbehebung finden Sie in der entsprechenden Dokumentation oder wenden Sie sich an die Support-Ressourcen für Adobe.

Weitere Informationen finden Sie in der folgenden Dokumentation:

* [Quellen – Übersicht](../../../../home.md)
* [Real-Time CDP B2B Edition](../../../../../rtcdp/b2b-overview.md)
