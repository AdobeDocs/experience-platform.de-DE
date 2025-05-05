---
title: Acxiom Data Enhancement
description: Verwenden Sie diesen Connector, um Erstanbieter-Adobe-Profile in Real-Time CDP für Acxiom zu aktivieren, um Daten anzureichern und kanalübergreifend zu verwenden. Anschließend können Sie die Acxiom-Quelle verwenden, um die Profile mit erweiterten Daten zu importieren und mit ihnen in Real-Time CDP zu arbeiten.
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
>Das [!DNL Acxiom Data Enhancement]-Ziel befindet sich in der Beta-Phase.  Dieser Ziel-Connector und diese Dokumentationsseite werden vom Acxiom-Team erstellt und gepflegt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an acxiom-adobe-help@acxiom.com.

## Übersicht {#overview}

Verwenden Sie den [!DNL Acxiom Data Enhancement]-Connector, um Ihren Kundenprofilen zusätzliche beschreibende Daten zur Verwendung in Analyse-, Segmentierungs- und Targeting-Anwendungen bereitzustellen. Hunderte von Elementen stehen zur Verfügung, sodass Sie Daten besser segmentieren und modellieren können, was zu einem genaueren Targeting und einer prädiktiven Modellierung führt.

![Marketing-Diagramm zum Exportieren von First-Party-Daten nach Acxiom und anschließendem Importieren der angereicherten Daten zurück in Real-Time CDP](/help/destinations/assets/catalog/data-partner/acxiom/marketing-workflow-data-enhancement.png)

In diesem Tutorial werden Schritte zum Erstellen einer [!DNL Acxiom Data Enhancement] Zielverbindung und eines Datenflusses mithilfe der Adobe Experience Platform-Benutzeroberfläche beschrieben. Dieser Connector wird verwendet, um Daten mithilfe von Amazon S3 als Droppoint an den Acxiom Enhancement Service zu senden.

![Der Zielkatalog mit dem ausgewählten Acxiom-Ziel.](../../assets/catalog/data-partner/acxiom/image-destination-enhancement-catalog.png)

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das [!DNL Acxiom Data Enhancement]-Ziel verwenden sollten, finden Sie hier einige Beispielanwendungsfälle, die Kundinnen und Kunden von Adobe Experience Platform mit diesem Ziel bewältigen können.

### Verbessern von Kundendaten {#enhance-customer-data}

Dieser Connector sollte von Marketing-Fachleuten verwendet werden, die die Effektivität ihrer Strategien für die Öffentlichkeitsarbeit verbessern möchten, indem sie ausgewählte beschreibende Elemente an ihre Kundenprofile anhängen und diese verwenden, um Kampagnen gezielter durchzuführen.

Als Marketing-Experte können Sie beispielsweise Ihre bestehenden Zielgruppen besser verstehen, indem Sie ihre Profile mit zusätzlichen Daten anreichern. Auf diese Weise werden Ihre Segmentierungs- und Zielgruppenbestimmungsstrategien verbessert, was zu einer verstärkten Personalisierung und Konversion von Kampagnen führt.

Der Anwendungsfall wird durch eine Kombination aus Ziel- und Quell-Connectoren ausgeführt.

Sie würden zunächst Ihre vorhandenen Kundendatensätze zur Anreicherung mit diesem Ziel-Connector exportieren. Der Service von Acxiom würde nach der Datei suchen, sie abrufen, sie mit den Daten von Acxiom anreichern und eine Datei erzeugen.

Der Kunde würde dann die entsprechende [Acxiom Data Ingestion](/help/sources/connectors/data-partners/acxiom-data-ingestion.md)-Quellkarte verwenden, um die hydratisierten Kundenprofile wieder in Adobe Real-Time CDP aufzunehmen.

## Voraussetzungen {#prerequisites}

>[!IMPORTANT]
>
>* Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die Berechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffssteuerung](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Art von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|-----------------------------|-----------|---------------------------------------------------------------------------------------------------------------------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die über den Experience Platform ([-Service) generiert ](../../../segmentation/home.md). |
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
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Datensatzziele verwalten und aktivieren]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Zielkonfigurations-Workflow die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

Um auf Ihren Bucket auf Experience Platform zuzugreifen, müssen Sie gültige Werte für die folgenden Anmeldeinformationen angeben:

| Anmeldedaten | Beschreibung |
|---------------|----------------------------------------------------------------------------------------------------------|
| S3-Zugriffsschlüssel | Die Zugriffsschlüssel-ID für Ihren Bucket. Sie können diesen Wert vom [!DNL Acxiom]-Team abrufen. |
| S3 - Geheimer Schlüssel | Die geheime Schlüssel-ID für Ihren Bucket. Sie können diesen Wert vom [!DNL Acxiom]-Team abrufen. |
| Behältername | Dies ist der Bucket, in dem Dateien freigegeben werden. Sie können diesen Wert vom [!DNL Acxiom]-Team abrufen. |

### Neues Konto

So definieren Sie einen neuen Speicherort für Acxiom Managed S3:

![Neues Konto](../../assets/catalog/data-partner/acxiom/image-destination-new-account.png)

### Vorhandenes Konto

Konten, die bereits mit dem [!DNL Acxiom Data Enhancement] Ziel definiert wurden, werden in einem Popup-Fenster mit einer Liste angezeigt. Wenn diese Option aktiviert ist, werden Details zum Konto in der rechten Leiste angezeigt. Sehen Sie sich das Beispiel über die Benutzeroberfläche an, wenn Sie zu **[!UICONTROL Ziele]** > **[!UICONTROL Konten]** navigieren.

![Vorhandenes Konto](../../assets/catalog/data-partner/acxiom/image-destination-enhancement-account.png)

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

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
>
>* Zum Aktivieren von Daten benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**&#x200B;[Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die Berechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffssteuerung](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](/help/destinations/ui/activate-batch-profile-destinations.md).

### Zuordnungsvorschläge

Die korrekte Verarbeitung von Dateien auf der Acxiom-Seite erfordert die Elemente Name und Adresse. Es sind zwar nicht alle Elemente erforderlich, doch die Bereitstellung von so viel wie möglich hilft bei der erfolgreichen Zuordnung.

Mapping-Vorschläge sind in der folgenden Tabelle aufgeführt. Attribute auf Ihrer Zielseite, die von der Acxiom-Verarbeitung verwendet werden und denen Kunden Profilattribute zuordnen können, werden aufgelistet. Behandeln Sie diese Elemente als Vorschläge, da nicht alle Elemente erforderlich sind und die Quellwerte von den Anforderungen des Kontos abhängen.

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

>[!NOTE]
>
>Wenn Sie zusätzliche Felder zuordnen, die oben nicht im Datenfluss aufgeführt sind, werden diese in den Datenexport einbezogen, aber von der Acxiom-Verarbeitung ignoriert.

## Überprüfen des Datenexports {#exported-data}

Um festzustellen, ob die Daten erfolgreich exportiert wurden, überprüfen Sie Ihren [!DNL Amazon S3 Storage]-Behälter und stellen Sie sicher, dass die exportierten Dateien die erwarteten Profilpopulationen enthalten.

## Nächste Schritte

In diesem Tutorial haben Sie erfolgreich einen Datenfluss erstellt, um Profildaten von der Experience Platform in Ihren [!DNL Acxiom] verwalteten S3-Speicherort zu exportieren. Als Nächstes müssen Sie sich mit dem Namen des Kontos, den Dateinamen und dem Bucket-Pfad an Ihren Acxiom-Support-Mitarbeiter wenden, damit die Verarbeitung eingerichtet werden kann.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).

## Zusätzliche Ressourcen {#additional-resources}

*Acxiom InfoBase:* https://www.acxiom.com/wp-content/uploads/2022/02/fs-acxiom-infobase_AC-0268-22.pdf
