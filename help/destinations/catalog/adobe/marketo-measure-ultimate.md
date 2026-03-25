---
title: Marketo Measure Ultimate-Ziel
description: Erfahren Sie, wie Sie Daten mit dem Marketo Measure Ultimate-Ziel verbinden und aktivieren.
last-substantial-update: 2023-03-07T00:00:00Z
exl-id: b4220841-8908-41ff-b977-dbeebfa787c8
source-git-commit: d946d3dbb09c1fe0163fba3a892b4c0f1b331f87
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 26%

---

# Marketo Measure Ultimate-Ziel {#mmu-destination}

## Überblick {#overview}

Mit Marketo Measure (ehemals Bizible) erhalten Marketing-Fachleute in insight Informationen darüber, welche Marketing-Maßnahmen zur Steigerung des Umsatzes und der Maximierung des ROI für ihr Unternehmen am effektivsten sind. Marketo Measure ist eine Marketing-Attributionslösung, mit der die Kanalleistung automatisch verfolgt und Berichte darüber erstellt werden. So erhalten Sie Einblick in die Kanäle, die die meiste Kundeninteraktion fördern, und können Ihre Marketing-Ausgaben entsprechend optimieren.

Das -Ziel ermöglicht Business-to-Business-Datenflüsse (B2B) von [!DNL Adobe Experience Platform] zu Marketo Measure. Die Karte steht nur Kunden von Marketo Measure Ultimate zur Verfügung.

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das Marketo Measure-Ziel verwenden sollten, finden Sie hier einige Beispielanwendungsfälle, die [!DNL Adobe Experience Platform] Kunden mit diesem Ziel bewältigen können. Diese Integration:

* Erfüllt die komplexen Daten- und Performance-Reporting-Anforderungen großer Unternehmen.
* Ermöglicht das Reporting über B2B-Attributionen mit mehreren CRM- und Marketing-Automatisierungssystemen.
* Ermöglicht das einfache Einbringen von Offline-Touchpoint-Daten von Drittanbietern.

## Voraussetzungen {#prerequisites}

Beachten Sie die folgenden Voraussetzungen für das Marketo Measure-Ziel:

* Die Experience Platform-Sandbox-Zuordnung sollte vom Administrator auf der Seite &quot;Marketo Measure-Einstellungen“ abgeschlossen werden. Ohne die Sandbox-Zuordnung können Sie den Workflow zum Herstellen einer Verbindung mit dem Ziel und zum Speichern und Aktivieren von Daten nicht abschließen.
* Nur Datensätze von B2B-XDM-Klassen können exportiert werden (siehe z. B. die Klassen XDM Business Account und XDM Business Opportunity ). Sie können nicht mehrere Datensätze derselben B2B-XDM-Klasse für eine bestimmte Datenquelle einbringen.
* Jeder Datensatz kann nur in einem Datenfluss zum Marketo Measure-Ziel enthalten sein.

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Arten von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Zielgruppen, die über den Experience Platform-[ (Segmentierungs-Service) generiert ](../../../segmentation/home.md). |
| Alle anderen Ursprünge der Zielgruppe | Nein | Diese Kategorie enthält alle Ursprünge der Zielgruppe außerhalb der Zielgruppen, die durch die [!DNL Segmentation Service] generiert wurden. Lesen Sie mehr über [verschiedene Ursprünge von Audiences](/help/segmentation/ui/audience-portal.md#customize). Einige Beispiele: <ul><li> benutzerdefinierte Upload-Zielgruppen [importiert](../../../segmentation/ui/audience-portal.md#import-audience) aus CSV-Dateien in Experience Platform,</li><li> Lookalike-Zielgruppen, </li><li> Federated Audiences, </li><li> Zielgruppen, die in anderen Experience Platform-Apps generiert werden, z. B. [!DNL Adobe Journey Optimizer], </li><li> und mehr. </li></ul> |

{style="table-layout:auto"}



Unterstützte Zielgruppen nach Zielgruppen-Datentyp:

| Datentyp der Zielgruppe | Unterstützt | Beschreibung | Anwendungsfälle |
|--------------------|-----------|-------------|-----------|
| [Personen-Zielgruppen](/help/segmentation/types/people-audiences.md) | Nein | Basierend auf Kundenprofilen können Sie bestimmte Personengruppen für Marketing-Kampagnen ansprechen. | Häufige Käufer, Warenkorbabbrüche |
| [Konto-Zielgruppen](/help/segmentation/types/account-audiences.md) | Nein | Targeting von Personen in bestimmten Organisationen für Account-basierte Marketing-Strategien. | B2B-Marketing |
| [Interessenten-Zielgruppen](/help/segmentation/types/prospect-audiences.md) | Nein | Targeting von Personen, die noch keine Kunden sind, aber Merkmale mit Ihrer Zielgruppe teilen. | Akquise mit Drittanbieterdaten |
| [Datensatzexporte](/help/catalog/datasets/overview.md) | Ja | Sammlungen strukturierter Daten, die im Data Lake von [!DNL Adobe Experience Platform] gespeichert sind. | Reporting, Datenwissenschaft-Workflows |

{style="table-layout:auto"}


## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Dataset export]** | Sie exportieren Rohdatensätze, die nicht nach Zielgruppeninteressen oder Qualifikationen gruppiert oder strukturiert sind. Lesen Sie mehr über [Datensatzexporte](/help/destinations/destination-types.md#dataset-export-destinations). |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Dieses Batch-Ziel exportiert Dateien alle zwei Stunden auf die Marketo Measure-Plattform. Lesen Sie mehr über [Planen von Datensatzexporten](/help/destinations/ui/export-datasets.md#scheduling). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage and Activate Dataset Destinations]** Zugriffssteuerungsberechtigungen[. ](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die im folgenden Abschnitt aufgeführt sind.

### Ausfüllen der Zieldetails {#destination-details}

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Description]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.

![Der Workflow „Mit Ziel verbinden“ für das Marketo Measure-Ziel.](/help/destinations/assets/catalog/adobe/marketo-measure-ultimate/marketo-measure-connect-to-destination.png)

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

## Datensätze an dieses Ziel exportieren {#export-datasets}

>[!IMPORTANT]
>
>Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage and Activate Dataset Destinations]** Zugriffssteuerungsberechtigungen[ ](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Lesen Sie das [Exportieren von Datensätzen](/help/destinations/ui/export-datasets.md)-Tutorial für ausführliche Anweisungen zum Exportieren von Datensätzen zu diesem Ziel.

## Überprüfen des Datenexports {#exported-data}

Um einen erfolgreichen Datensatzexport zu validieren, können Sie überprüfen, ob Ihr Datensatz erfolgreich in Ihr [Snowflake Data Warehouse](https://experienceleague.adobe.com/docs/marketo-measure/using/marketo-measure-data-warehouse/data-warehouse-access-reader-account.html) gelangt ist.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).
