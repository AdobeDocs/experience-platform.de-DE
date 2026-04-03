---
title: Acxiom Prospect-Suppression
description: Exportieren Sie Ihre Erstanbieter-Zielgruppen in das Acxiom-Ziel, damit Acxiom bekannte oder konvertierte Kundinnen und Kunden unterdrücken kann. Verwenden Sie dann den Acxiom-Quell-Connector, um Interessentenlisten von Acxiom aufzunehmen und zu aktivieren, wobei Ihre bekannten oder konvertierten Kunden entfernt werden.
last-substantial-update: 2024-03-14T00:00:00Z
badge: label="Beta" type="Informative"
exl-id: d82e8cd3-970c-44af-99b0-ea154eb3655e
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '1531'
ht-degree: 22%

---

# [!DNL Acxiom Prospect-Suppression] Zielverbindung

>[!NOTE]
>
>Das [!DNL Acxiom Prospect-Suppression]-Ziel befindet sich in der Beta-Phase. Dieser Ziel-Connector und diese Dokumentationsseite werden vom Acxiom-Team erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an acxiom-adobe-help@acxiom.com.

## Überblick {#overview}

Verwenden Sie [!DNL Acxiom Prospect-Suppression], um möglichst produktive Zielgruppen potenzieller Kundinnen und Kunden bereitzustellen. Dieser Connector exportiert First-Party-Daten sicher aus [!DNL Real-Time Customer Data Platform] und führt sie über eine preisgekrönte Hygiene- und Identitätsauflösung durch, die eine Datendatei erzeugt, die als Unterdrückungsliste verwendet werden kann. Diese werden mit der [!DNL Acxiom Global] abgeglichen, sodass die Listen für Interessenten maßgeschneidert importiert werden können. Verwenden Sie dann den [[!DNL Acxiom Prospecting Data Import]](/help/sources/connectors/data-partners/acxiom-prospecting-data-import.md)-Quell-Connector, um Interessentenlisten von Acxiom wieder in [!DNL Real-Time CDP] zu importieren, wobei Ihre bekannten oder konvertierten Kunden entfernt werden.

![Marketing-Diagramm zum Exportieren von First-Party-Daten nach Acxiom und zum anschließenden Importieren von potenziellen Daten zurück in Real-Time CDP](/help/destinations/assets/catalog/data-partner/acxiom/marketing-workflow.png)

Acxiom bietet die Zielgruppen mit der besten Performance der Branche mit dem größten Katalog von über 12.000 globalen Datenattributen, die speziell auf die Bereitstellung personalisierter Erlebnisse ausgerichtet sind. Nutzen Sie die unendlichen Kombinationen aus hochwertigen Daten, um Zielgruppen zu erstellen und zu verteilen, die auf bestimmte Kampagnenanforderungen zugeschnitten sind.

In diesem Tutorial finden Sie die Schritte zum Erstellen einer [!DNL Acxiom Prospect-Suppression] Zielverbindung und eines Datenflusses mithilfe der [!DNL Adobe Experience Platform]-Benutzeroberfläche. Dieser Connector stellt Daten mithilfe von Amazon S3 als Ablagepunkt für den potenziellen Kunden-Service von Acxiom bereit. Wenden Sie sich an Ihren Acxiom-Kundenbetreuer, sobald Sie mit dem Export von Dateien zum Amazon S3-Ablagepunkt beginnen.

![Der Zielkatalog mit dem ausgewählten Acxiom-Ziel.](../../assets/catalog/data-partner/acxiom/image-destination-catalog.png)

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das [!DNL Acxiom Prospect-Suppression]-Ziel verwenden sollten, finden Sie hier einige Beispielanwendungsfälle, die [!DNL Adobe Experience Platform] Kunden mit diesem Ziel bewältigen können.

### Erstellen einer Unterdrückungsliste für Datensätze bei der Kundenakquise {#create-suppression-list}

Marketing-Experten, die die Effektivität ihrer Outreach-Strategien verbessern möchten, verwenden häufig die Erstellung einer Unterdrückungsliste. Diese Liste enthält Bestandskunden und bestimmte Segmente, um sicherzustellen, dass diese während zielgerichteter Kampagnen von Aktivitäten zur Kundenakquise ausgeschlossen sind. Dieser strategische Ansatz hilft, die Zielgruppe zu verfeinern, redundante Kommunikation zu vermeiden, und trägt zu einer fokussierteren und effizienteren Marketing-Anstrengung bei.

Als Marketing-Experte können Sie beispielsweise Ihre Kampagnenreichweite erweitern, indem Sie Ihren Kampagnen zielgerichtete Interessentenprofile hinzufügen, die auf von Ihnen angegebenen Segmentierungs- und Unterdrückungskriterien basieren.

Der Anwendungsfall wird durch eine Kombination aus Ziel- und Quell-Connectoren ausgeführt.

Zunächst würden Sie Ihre vorhandenen Kundenprofile exportieren, indem Sie diesen Ziel-Connector verwenden, um sie als Unterdrückungsdatei zu verwenden. Dadurch wird sichergestellt, dass keine vorhandenen Kundendatensätze enthalten sind.

Der Service von Acxiom sucht nach der Datei, ruft sie ab und verwendet sie zusammen mit zusätzlichen Auswahlkriterien und generiert eine Interessentendatei. Anschließend würden Sie den entsprechenden [[!DNL Acxiom Prospecting Data Import]](/help/sources/connectors/data-partners/acxiom-prospecting-data-import.md)-Quell-Connector verwenden, um die Interessentenprofile in Adobe [!DNL Real-Time CDP] aufzunehmen.

## Voraussetzungen {#prerequisites}

>[!IMPORTANT]
>
>* Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die **[!UICONTROL View Identity Graph]** Zugriffssteuerungsberechtigung[ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Art von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Zielgruppen, die über den Experience Platform-[ (Segmentierungs-Service) generiert ](../../../segmentation/home.md). |
| Alle anderen Ursprünge der Zielgruppe | Nein | Diese Kategorie enthält alle Ursprünge der Zielgruppe außerhalb der Zielgruppen, die durch die [!DNL Segmentation Service] generiert wurden. Lesen Sie mehr über [verschiedene Ursprünge von Audiences](/help/segmentation/ui/audience-portal.md#customize). Einige Beispiele: <ul><li> benutzerdefinierte Upload-Zielgruppen [importiert](../../../segmentation/ui/audience-portal.md#import-audience) aus CSV-Dateien in Experience Platform,</li><li> Lookalike-Zielgruppen, </li><li> Federated Audiences, </li><li> Zielgruppen, die in anderen Experience Platform-Apps generiert werden, z. B. [!DNL Adobe Journey Optimizer], </li><li> und mehr. </li></ul> |

{style="table-layout:auto"}




Unterstützte Zielgruppen nach Zielgruppen-Datentyp:

| Datentyp der Zielgruppe | Unterstützt | Beschreibung | Anwendungsfälle |
|--------------------|-----------|-------------|-----------|
| [Personen-Zielgruppen](/help/segmentation/types/people-audiences.md) | Ja | Basierend auf Kundenprofilen können Sie bestimmte Personengruppen für Marketing-Kampagnen ansprechen. | Häufige Käufer, Warenkorbabbrüche |
| [Konto-Zielgruppen](/help/segmentation/types/account-audiences.md) | Nein | Targeting von Personen in bestimmten Organisationen für Account-basierte Marketing-Strategien. | B2B-Marketing |
| [Interessenten-Zielgruppen](/help/segmentation/types/prospect-audiences.md) | Nein | Targeting von Personen, die noch keine Kunden sind, aber Merkmale mit Ihrer Zielgruppe teilen. | Akquise mit Drittanbieterdaten |
| [Datensatzexporte](/help/catalog/datasets/overview.md) | Nein | Sammlungen strukturierter Daten, die im Data Lake von [!DNL Adobe Experience Platform] gespeichert sind. | Reporting, Datenwissenschaft-Workflows |

{style="table-layout:auto"}


## Exporttyp und -häufigkeit {#export-type-frequency}

Informationen zum Zielexporttyp und zur Häufigkeit finden Sie in der folgenden Tabelle.

| Element | Typ | Anmerkungen |
|------------------|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Exporttyp | **[!UICONTROL Profile-based]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B. E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm „Auswählen der Profilattribute“ im [Zielaktivierungs-Workflow](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes) festgelegt. |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Weitere Informationen finden Sie unter [Batch-Datei-basierte Ziele](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage Destinations]** Zugriffssteuerungsberechtigungen[. ](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Zielkonfigurations-Workflow die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Connect to destination]** aus.

Um auf Ihren Bucket in Experience Platform zuzugreifen, müssen Sie gültige Werte für die folgenden Anmeldeinformationen angeben:

| Anmeldedaten | Beschreibung |
|---------------|----------------------------------------------------------------------------------------------------------|
| S3-Zugriffsschlüssel | Die Zugriffsschlüssel-ID für Ihren Bucket. Sie können diesen Wert vom [!DNL Acxiom]-Team abrufen. |
| S3 - Geheimer Schlüssel | Die geheime Schlüssel-ID für Ihren Bucket. Sie können diesen Wert vom [!DNL Acxiom]-Team abrufen. |
| Behältername | Dies ist der Bucket, in dem Dateien freigegeben werden. Sie können diesen Wert vom [!DNL Acxiom]-Team abrufen. |

### Neues Konto {#new-account}

So definieren Sie einen neuen Speicherort für Acxiom Managed S3:

![Neues Konto](../../assets/catalog/data-partner/acxiom/image-destination-new-account.png)

### Vorhandenes Konto {#existing-account}

Konten, die bereits mit dem [!DNL Acxiom Prospect Suppression] Ziel definiert wurden, werden in einem Popup-Fenster mit einer Liste angezeigt. Wenn diese Option aktiviert ist, werden Details zum Konto in der rechten Leiste angezeigt. Sehen Sie sich das Beispiel über die Benutzeroberfläche an, wenn Sie zu **[!UICONTROL Destinations]** > **[!UICONTROL Accounts]** navigieren:

![Vorhandenes Konto](../../assets/catalog/data-partner/acxiom/image-destination-account.png)

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![Zieldetails](../../assets/catalog/data-partner/acxiom/image-destination-details.png)

* **Name (erforderlich)** - Der Name, unter dem das Ziel gespeichert wird
* **Beschreibung** - Kurze Erläuterung des Ziels
* **Behältername (erforderlich)** - Name des Amazon S3-Buckets, der auf S3 eingerichtet wurde
* **Ordnerpfad (erforderlich)** - Wenn Unterordner in einem Bucket verwendet werden, muss ein Pfad definiert werden, oder &#39;/&#39;, um auf den Stammpfad zu verweisen.
* **Dateityp** - Wählen Sie das Format aus, das Experience Platform für die exportierten Dateien verwenden soll. Derzeit ist CSV der einzige Dateityp, den Acxiom Processing erwartet

>[!IMPORTANT]
>
>Bei Auswahl der Optionen CSV *(Trennzeichen*, *Anführungszeichen*, *Escape-Zeichen*, *Leerer Wert*, *Null-Wert*, *Komprimierungsformat* und *Manifestdatei einschließen* werden im folgenden Dokument diese Einstellungen detaillierter erläutert [Konfigurieren der Formatierungsoptionen](../../ui/batch-destinations-file-formatting-options.md).

![CSV-Optionen](../../assets/catalog/data-partner/acxiom/image-destination-csv-options.png)

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
>
>* Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die **[!UICONTROL View Identity Graph]** Zugriffssteuerungsberechtigung[ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](/help/destinations/ui/activate-batch-profile-destinations.md).

### Zuordnungsvorschläge {#mapping-suggestions}

Für die Verarbeitung sind Name- und Adressenelemente erforderlich, während nicht alle Elemente erforderlich sind. Dabei wird ein möglichst guter Abgleich unterstützt.  Mapping-Vorschläge sind in der folgenden Tabelle aufgeführt. Attribute auf Ihrer Zielseite, die von der Acxiom-Verarbeitung verwendet werden und denen Kunden Profilattribute zuordnen können, werden aufgelistet.  Dies sollte als Vorschlag gewertet werden, da nicht alle Elemente erforderlich sind und die Quellwerte von den Anforderungen des Kontos abhängen.

| Zielfeld | Source-Beschreibung |
|--------------|-------------------------------------------------------------|
| name | Der `person.name.fullName` Wert in Experience Platform. |
| firstName | Der `person.name.firstName` Wert in Experience Platform. |
| lastName | Der `person.name.lastName` Wert in Experience Platform. |
| Adresse1 | Der `mailingAddress.street1` Wert in Experience Platform. |
| Adresse2 | Der `mailingAddress.street2` Wert in Experience Platform. |
| city | Der `mailingAddress.city` Wert in Experience Platform. |
| state | Der `mailingAddress.state` Wert in Experience Platform. |
| PLZ | Der `mailingAddress.postalCode` Wert in Experience Platform. |

{style="table-layout:auto"}

>[!NOTE]
>
>Zusätzliche, oben nicht aufgeführte Felder werden in den Export einbezogen, aber von der Acxiom-Verarbeitung ignoriert.

## Überprüfen des Datenflusses {#review-dataflow}

Verwenden Sie die Überprüfungsseite vor der Übermittlung für eine Zusammenfassung Ihres Datenflusses

![Überprüfung](../../assets/catalog/data-partner/acxiom/image-destination-review.png)

## Überprüfen des Datenexports {#exported-data}

Um festzustellen, ob die Daten erfolgreich exportiert wurden, überprüfen Sie Ihren [!DNL Amazon S3 Storage]-Behälter und stellen Sie sicher, dass die exportierten Dateien die erwarteten Profilpopulationen enthalten.

## Nächste Schritte {#next-steps}

Sie haben erfolgreich einen Datenfluss erstellt, um Batch-Daten aus Experience Platform an Ihren [!DNL Acxiom] verwalteten S3-Speicherort zu exportieren. Sie müssen sich mit dem Namen des Kontos, dem Dateinamen und dem Bucket-Pfad an Ihren Acxiom-Support-Mitarbeiter wenden, damit die Verarbeitung eingerichtet werden kann.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).

## Weitere Ressourcen {#additional-resources}

*Acxiom Zielgruppendaten und -verteilung:* https://www.acxiom.com/customer-data/audience-data-distribution/
