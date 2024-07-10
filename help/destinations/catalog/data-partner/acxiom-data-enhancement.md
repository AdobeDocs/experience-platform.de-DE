---
title: Acxiom-Datenverbesserung
description: Verwenden Sie diesen Connector, um Erstanbieter-Adobe-Profile in Real-Time CDP zu Acxiom zu aktivieren, damit Daten angereichert und über Marketingkanäle hinweg verwendet werden können. Sie können dann die Acxiom-Quelle verwenden, um die Profile mit erweiterten Daten zu importieren und in Real-Time CDP mit ihnen zu arbeiten.
last-substantial-update: 2024-03-14T00:00:00Z
badge: Beta
exl-id: 59edc43d-ae8e-4c3d-820c-b5be1c4483f9
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1346'
ht-degree: 28%

---

# [!DNL Acxiom Data Enhancement] Zielverbindung

>[!NOTE]
>
>Die [!DNL Acxiom Data Enhancement] Das Ziel befindet sich in der Beta-Phase.  Diese Ziel-Connector- und Dokumentationsseite werden vom Acxiom-Team erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an acxiom-adobe-help@acxiom.com.

## Übersicht {#overview}

Verwenden Sie die [!DNL Acxiom Data Enhancement] Connector zur Bereitstellung zusätzlicher beschreibender Daten für Ihre Kundenprofile zur Verwendung in Analyse-, Segmentierungs- und Targeting-Anwendungen. Hunderte von Elementen sind verfügbar, sodass Sie Daten besser segmentieren und modellieren können, was zu einer präziseren Zielgruppenbestimmung und prädiktiven Modellierung führt.

![Marketingdiagramm zum Exportieren von Erstanbieterdaten in Acxiom und anschließendem Importieren angereicherter Daten zurück in Real-Time CDP](/help/destinations/assets/catalog/data-partner/acxiom/marketing-workflow-data-enhancement.png)

In diesem Tutorial werden Schritte zum Erstellen eines [!DNL Acxiom Data Enhancement] Zielverbindung und Datenfluss über die Adobe Experience Platform-Benutzeroberfläche. Dieser Connector wird verwendet, um Daten mithilfe von Amazon S3 als Ablagepunkt an den Acxiom Enhancement Service zu übermitteln.

![Der Zielkatalog mit dem ausgewählten Acxiom-Ziel.](../../assets/catalog/data-partner/acxiom/image-destination-enhancement-catalog.png)

## Anwendungsfälle {#use-cases}

Um Ihnen zu helfen, besser zu verstehen, wie und wann Sie die [!DNL Acxiom Data Enhancement] Ziel, hier finden Sie Beispielanwendungsfälle, die Adobe Experience Platform-Kunden mit diesem Ziel lösen können.

### Kundendaten verbessern {#enhance-customer-data}

Dieser Connector sollte von Marketing-Fachleuten verwendet werden, die die Effektivität ihrer Zielgruppenstrategien steigern, indem sie ausgewählte beschreibende Elemente an ihre Kundenprofile anhängen und diese zur gezielteren Ausrichtung von Kampagnen verwenden.

Als Marketing-Experte möchten Sie beispielsweise Ihr Verständnis für Ihre bestehenden Zielgruppen vertiefen, indem Sie deren Profile mit zusätzlichen Daten anreichern. Dadurch werden Ihre Segmentierungs- und Targeting-Strategien verbessert, was zu einer Steigerung der Kampagnenpersonalisierung und -konvertierung führt.

Der Anwendungsfall wird über eine Kombination aus Ziel- und Quell-Connectoren ausgeführt.

Exportieren Sie zunächst Ihre vorhandenen Kundendatensätze zur Anreicherung mithilfe dieses Ziel-Connectors. Der Dienst von Acxiom würde nach der Datei suchen, sie abrufen, sie mit Acxiom-Daten anreichern und eine Datei generieren.

Der Kunde würde dann die entsprechende [Acxiom-Datenerfassung](/help/sources/connectors/data-partners/acxiom-data-ingestion.md) Quellkarte, um die hydrierten Kundenprofile wieder in Adobe Real-Time CDP aufzunehmen.

## Voraussetzungen {#prerequisites}

>[!IMPORTANT]
>
>* Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Anzeigen von Profilen]**, und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Export *identities*, benötigen Sie die **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). <br> ![Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Zielgruppentypen Sie an dieses Ziel exportieren können.

| Audience Origin | Unterstützt | Beschreibung |
|-----------------------------|-----------|---------------------------------------------------------------------------------------------------------------------|
| [!DNL Segmentation Service] | ✓ | Über die Experience Platform generierte Zielgruppen [Segmentierungsdienst](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | x | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}


## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|------------------|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B. E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm „Auswählen der Profilattribute“ im [Zielaktivierungs-Workflow](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes) festgelegt. |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Weitere Informationen finden Sie unter [Batch-Datei-basierte Ziele](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Verwalten und Aktivieren von Datensatzzielen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Zielkonfigurations-Workflow die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

Um auf Ihren Bucket auf dem Experience Platform zuzugreifen, müssen Sie gültige Werte für die folgenden Anmeldedaten angeben:

| Anmeldedaten | Beschreibung |
|---------------|----------------------------------------------------------------------------------------------------------|
| S3-Zugriffsschlüssel | Die Zugriffsschlüssel-ID für Ihren Behälter. Sie können diesen Wert aus dem [!DNL Acxiom] Team. |
| S3-Geheimschlüssel | Die geheime Schlüssel-ID für Ihren Bucket. Sie können diesen Wert aus dem [!DNL Acxiom] Team. |
| Behältername | Dies ist Ihr Bucket, in dem Dateien freigegeben werden. Sie können diesen Wert aus dem [!DNL Acxiom] Team. |

### Neues Konto

So definieren Sie einen neuen Acxiom Managed S3-Speicherort:

![Neues Konto](../../assets/catalog/data-partner/acxiom/image-destination-new-account.png)

### Vorhandenes Konto

Mit der Variablen [!DNL Acxiom Data Enhancement] Das Ziel wird in einem Listen-Popup angezeigt. Wenn diese Option aktiviert ist, werden Details zum Konto in der rechten Leiste angezeigt. Zeigen Sie das Beispiel in der Benutzeroberfläche an, wenn Sie zu **[!UICONTROL Ziele]** > **[!UICONTROL Konten]**;

![Vorhandenes Konto](../../assets/catalog/data-partner/acxiom/image-destination-enhancement-account.png)

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![Zieldetails](../../assets/catalog/data-partner/acxiom/image-destination-details.png)

* **Name (erforderlich)** - Der Name, unter dem das Ziel gespeichert wird
* **Beschreibung** - Kurze Erläuterung des Ziels des Bestimmungsorts
* **Behältername (erforderlich)** - Name des auf S3 eingerichteten Amazon S3-Buckets
* **Ordnerpfad (erforderlich)** - Wenn Unterverzeichnisse in einem Behälter verwendet werden, muss ein Pfad definiert werden, oder &quot;/&quot;, um auf den Stammpfad zu verweisen.
* **Dateityp** - Wählen Sie das Format aus, das Experience Platform für die exportierten Dateien verwenden soll. Derzeit erwartet die Acxiom-Verarbeitung nur den Dateityp CSV

>[!IMPORTANT]
>
>Bei Auswahl der CSV-Option *Trennzeichen*, *Anführungszeichen*, *Escape-Zeichen*, *Leerer Wert*, *Nullwert*, *Komprimierungsformat*, und *Manifestdatei einschließen* Optionen angezeigt werden, werden diese Einstellungen im folgenden Dokument ausführlicher erläutert [Formatierungsoptionen konfigurieren](../../ui/batch-destinations-file-formatting-options.md).

![CSV-Optionen](../../assets/catalog/data-partner/acxiom/image-destination-csv-options.png)

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
>
>* Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Anzeigen von Profilen]**, und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Export *identities*, benötigen Sie die **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). <br> ![Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](/help/destinations/ui/activate-batch-profile-destinations.md).

### Vorschläge zuordnen

Für die korrekte Verarbeitung von Dateien auf der Seite &quot;Acxiom&quot;sind Name- und Adresselemente erforderlich. Auch wenn nicht alle Elemente erforderlich sind, hilft eine möglichst umfassende Bereitstellung bei der erfolgreichen Zuordnung.

Zuordnungsvorschläge finden Sie in der folgenden Tabelle, in der Attribute auf Ihrer Zielseite aufgelistet werden, die von der Acxiom-Verarbeitung verwendet werden und denen Kunden Profilattribute zuordnen können. Behandeln Sie diese Elemente als Vorschläge, da nicht alle Elemente erforderlich sind und die Quellwerte von den Anforderungen des Kontos abhängen.

| Zielfeld | Source-Beschreibung |
|--------------|-------------------------------------------------------------|
| name | Die `person.name.fullName` -Wert in Experience Platform. |
| firstName | Die `person.name.firstName` -Wert in Experience Platform. |
| lastName | Die `person.name.lastName` -Wert in Experience Platform. |
| address1 | Die `mailingAddress.street1` -Wert in Experience Platform. |
| address2 | Die `mailingAddress.street2` -Wert in Experience Platform. |
| city | Die `mailingAddress.city` -Wert in Experience Platform. |
| state | Die `mailingAddress.state` -Wert in Experience Platform. |
| zip | Die `mailingAddress.postalCode` -Wert in Experience Platform. |

>[!NOTE]
>
>Wenn Sie zusätzliche Felder zuordnen, die oben nicht im Datenfluss aufgeführt sind, werden diese im Datenexport einbezogen, aber von der Acxiom-Verarbeitung ignoriert.

## Überprüfen des Datenexports {#exported-data}

Um festzustellen, ob die Daten erfolgreich exportiert wurden, überprüfen Sie Ihren [!DNL Amazon S3 Storage]-Behälter und stellen Sie sicher, dass die exportierten Dateien die erwarteten Profilpopulationen enthalten.

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich einen Datenfluss erstellt, um Profildaten von Experience Platform in Ihre [!DNL Acxiom] verwalteter S3-Speicherort. Als Nächstes müssen Sie sich an Ihren Acxiom-Support-Mitarbeiter mit dem Namen des Kontos, den Dateinamen und dem Behälterpfad wenden, damit die Verarbeitung eingerichtet werden kann.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).

## Zusätzliche Ressourcen {#additional-resources}

*Acxiom Infobase:* https://www.acxiom.com/wp-content/uploads/2022/02/fs-acxiom-infobase_AC-0268-22.pdf
